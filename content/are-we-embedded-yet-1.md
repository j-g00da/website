+++
title = "Are We Embedded Yet? #1"
date = "2025-05-04"
in_search_index = true
description="Updates on no_std ratatui and mousefood, new backend - soft_ratatui."
[extra]
og_image="/are-we-embedded-yet.png"
+++

<div style="width:100%; text-align:center;">

_This series is meant to document and promote the joint effort of making ratatui truly portable._

</div>

## Update: no_std ratatui

<!-- more -->

---

[`Backend::Error` merged!](https://github.com/ratatui/ratatui/pull/1778)
One of the blockers for no_std ratatui was the explicit use of `std::io::Error` in `Backend` (and
by extension, in `Terminal` as well).
Now, `Backend` implementations must define an associated `Error` type.
Built-in backends will still use `std::io::Error`, but third-party ones
like [mousefood](https://github.com/j-g00da/mousefood)
can now use a different error type - which will enable a proper `no_std` compatibility!

I'm actually working on a [follow-up PR](https://github.com/ratatui/ratatui/pull/1817)
and ran into a pretty interesting issue,
so if anyone reading this has ideas, feel free to jump in and comment.

As for the layout cache problem I mentioned in the last post - 
since there's no great solution, [the decision for now
is to simply **not provide a cache in `no_std` mode**](https://github.com/ratatui/ratatui/pull/1795).
When this is merged, the last things left would be just few minor tweaks and adding `std` feature flag.

<div style="width:100%; text-align:center;">

> _We are one step closer to no_std ratatui._ \
██████████████████░░ 90%

</div>


## Update: mousefood

---

[Mousefood](https://github.com/j-g00da/mousefood) recently got italic modifier support
as well as readme section about bold/italic fonts that also points out some limitations.
Additionally, v0.2.1 patch was released that mainly targeted some inaccuracies in the docs.

{{ image(
src="/projects/mousefood/bold_italic.png",
alt="bold and italic fonts on mousefood") }}
_Bold and italic modifiers in mousefood, italic will be available with the next release._

The development of mousefood may be a bit slower right now,
as I'm focusing on finalizing `no_std` support in Ratatui -
but I'm still making sure to work on it regularly.
_If you'd like to help out, feel free to reach out!_

Full changelog of v0.2.1:
### 🚜 Refactor

- *(examples)* Remove unnecessary `extern crate` from simulator example

### 📚 Documentation

- *(readme)* Fix simulator code snippet

### ⚙️ Miscellaneous Tasks

- *(examples)* Configure simulator example in Cargo.toml
- Update list of excluded paths in Cargo.toml

## soft_ratatui

---

> Software rendering backend for [ratatui](https://github.com/ratatui/ratatui). No GPU required. TUI everywhere.

Another new [Ratatui](https://github.com/ratatui/ratatui) backend just dropped - 
[soft_ratatui](https://github.com/gold-silver-copper/soft_ratatui)
by [@gold-silver-copper](https://github.com/gold-silver-copper), 
the creator of [egui_ratatui](https://github.com/gold-silver-copper/egui_ratatui). 
The crate uses [tiny-skia](https://github.com/linebender/tiny-skia) to render efficiently directly to a window, 
ditching the terminal emulator completely. 
This allows for much higher frame rates out of the box (up to 200 FPS). 
It will be especially useful for TUI games or interactive tools where smooth performance really matters!

Soft_ratatui is under heavy development and I was told that it will eventually move away from
tiny-skia in favor of a custom lightweight renderer.

{{ image(
src="/other/soft_ratatui.png",
alt="colors_rgb example running at 140 FPS using soft_ratatui") }}

_colors_rgb running at over 140 FPS, "s" in "fps" gets cut off as the example doesn't expect that many digits!_

## Thanks!

---

Huge thanks for the response to the last post -
it got way more attention than I expected, and even made its way into
[*This Week in Rust #596*](https://this-week-in-rust.org/blog/2025/04/23/this-week-in-rust-596/)
and [*The Embedded Rustacean #44*](https://www.theembeddedrustacean.com/p/the-embedded-rustacean-issue-44).
Thanks to everyone who helped spread Ratatui even further!
