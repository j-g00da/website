+++
title = "Reverse engineering package name validation on PyPI"
date = "2025-11-16"
in_search_index = true
description="It's almost deterministic!"
[extra]
og_image="/pypi/sn8k.png"
+++

If you've ever tried to publish a package on [PyPI](https://pypi.org/),
you _might_ have encountered a quite interesting error message:

```
error: Failed to publish [..] to https://upload.pypi.org/legacy/
  Caused by: Upload failed with status code 400 Bad Request.
  Server says: 400 The name [..] is too similar to an existing project.
  See https://pypi.org/help/#project-name for more information.
```

Sadly it's not very clear what "too similar" means in this context.
Also there's no way to check if your name is acceptable before actually trying to upload the package.

Luckily, PyPI warehouse is open source, so let's just check how the validation is implemented.

<!-- more -->

{{ image(
src="/pypi/sn8k.png",
alt="pixelart of a snake with a shovel.",
style="width: 200px;")
}}

> I know "reverse engineering" sounds like a big word here since we have the source code, but hey - it's interesting anyway I swear.

```python
def check_project_name(self, name: str) -> None:
    """
    Check if a project name is valid and available.

    This method will raise an exception if the project name is invalid or
    unavailable for any reason.
    """
    if not PROJECT_NAME_RE.match(name):
        raise ProjectNameUnavailableInvalidError()

    # Also check for collisions with Python Standard Library modules.
    if canonicalize_name(name) in STDLIB_PROHIBITED:
        raise ProjectNameUnavailableStdlibError()

    if existing_project := self.db.scalars(
        select(Project).where(
            Project.normalized_name == func.normalize_pep426_name(name)
        )
    ).first():
        raise ProjectNameUnavailableExistingError(existing_project)

    if self.db.query(
        exists().where(
            ProhibitedProjectName.name == func.normalize_pep426_name(name)
        )
    ).scalar():
        raise ProjectNameUnavailableProhibitedError()

    if similar_project_name := self.db.scalars(
        select(Project.name).where(
            func.ultranormalize_name(Project.name) == func.ultranormalize_name(name)
        )
    ).first():
        raise ProjectNameUnavailableSimilarError(similar_project_name)

    # Check for typo-squatting.
    cached_corpus = self._query_results_cache.get("top_dependents_corpus")
    if typo_check_match := typo_check_name(
        canonicalize_name(name), corpus=cached_corpus
    ):
        raise ProjectNameUnavailableTypoSquattingError(
            check_name=typo_check_match[0],
            existing_project_name=typo_check_match[1],
        )

    return None
```

src: [services.py#L449-L494](https://github.com/pypi/warehouse/blob/691680fa603cce2375505b3b265fe72c0e5ca451/warehouse/packaging/services.py#L449-L494)

First the name is checked with a simple regex to ensure it only contains allowed characters.

```python
PROJECT_NAME_RE = re.compile(
    r"^([A-Z0-9]|[A-Z0-9][A-Z0-9._-]*[A-Z0-9])\Z", re.IGNORECASE
)
```
src: [project.py#L30C1-L32C2](https://github.com/pypi/warehouse/blob/691680fa603cce2375505b3b265fe72c0e5ca451/warehouse/utils/project.py#L30C1-L32C2)

Then the canonical name is checked against the standard library.

```python
STDLIB_PROHIBITED = {
    canonicalize_name(s.rstrip("-_.").lstrip("-_."))
    for s in chain.from_iterable(
        _namespace_stdlib_list(stdlib_list.stdlib_list(version))
        for version in stdlib_list.short_versions
    )
}
```
src: [services.py#L67C1-L73C2](https://github.com/pypi/warehouse/blob/691680fa603cce2375505b3b265fe72c0e5ca451/warehouse/packaging/services.py#L67C1-L73C2)

There are few SQL functions for normalizing the package name, first the name normalized using `normalize_pep426_name`
(underscores and dots turned into dashes + lowercase) checks it against all other (also normalized this way)
packages in the index. The same check runs against the list of prohibited names.

```sql
SELECT lower(regexp_replace($1, '(\.|_|-)+', '-', 'ig'))
```
src: [3af8d0006ba_normalize_runs_of_characters_to_a_.py#L21C17-L21C73](https://github.com/pypi/warehouse/blob/691680fa603cce2375505b3b265fe72c0e5ca451/warehouse/migrations/versions/3af8d0006ba_normalize_runs_of_characters_to_a_.py#L21C17-L21C73)


NOW interesting things start to happen - yet again it checks the normalized name against normalized names of all
packages, but this time it uses SQL function named `ultranormalize_name`.

You will ask - what is this so called ultranormalization? 
- removes dots, dashes and underscores
- changes L, l, I, i to 1
- changes o and O to 0
- lowercase

So e.g. `my-epic-bloom-filter` turns into `myep1cb100mf11ter`.

(It's very easy for package to be rejected by this filter.)

```sql
SELECT lower(
    regexp_replace(
        regexp_replace(
            regexp_replace($1, '(\.|_|-)', '', 'ig'),
            '(l|L|i|I)', '1', 'ig'
        ),
        '(o|O)', '0', 'ig'
    )
)
```

After this it runs a typo-squatting check called "TypoSnyper" which checks the canonical name against common typo
permutations of the "top dependents corpus" - a list of 200 "most relied upon" projects on PyPI.

Anyway, I took the typosniper source, reimplemented the SQL functions in Python and made myself a simple script to run
these checks locally. Maybe I can polish it a little and release it on PyPI (haha). I wasn't able to find some existing
script that does this, there's `nameisok` but it just runs a simple similarity check with predefined threshold which
doesn't match what PyPI actually does.

> Anyway, here it is: [please-release-this](https://github.com/j-g00da/please-release-this)

Oh and also, this script will tell you exactly which package your name collides with and why, which PyPI won't tell you.

e.g. when checking a name `bloom-filter`, you will get: 
`collision with 'BloomFilter' (ultranormalized to 'b100mf11ter')`

It's not much of a help though, it's not like you can just nuke someone else's project haha. WAIT DON'T DO THAT.

{{ image(
src="/pypi/sn8k_hole.png",
alt="a hole in the ground",
style="width: 200px;")
}}
