+++
title = "Drawing ASCII-art using pwd and a DNS"
date = "2026-01-09"
in_search_index = true
description="Exactly what the title says, I swear."
[extra]
og_image="me_v2.png"
+++

Did you know you can have newlines in pathnames?
The design is very human and this absolutely doesn't have any unforeseen consequences!

Also a friendly reminder that you can store anything on a nameserver if you try hard enough.

> Originally posted by me on donotsta.re (2025-12-23)

<!-- more -->

So a funny POSIX thing is it doesn't explicitly forbid newlines in pathnames. Of course this breaks a lot of stuff that doesn't expect this, because why would you have a newline in a filename. Anyway, `ls` escapes these, but for example `pwd` does not. This means you can draw ascii art using `pwd`.

So like everyone I had already some ascii art stored in a remote key value store (a TXT record on a DNS), and yes this works as expected, just run:

```
mkdir -p "$(dig +short TXT konkuter.kamiokan.de | sed 's/" "/\n\//g')" && cd "$_"
```

This will create a nested directory structure with each subdir being a line of ascii art ending with newline and `cd` into the most nested one.

Then just run `pwd`.

```
$ pwd
/home/j-g00da/"                       .,,uod8B8bou,,.
/              ..,uod8BBBBBBBBBBBBBBBBRPFT?l!i:.
/         ,=m8BBBBBBBBBBBBBBBRPFT?!||||||||||||||
/         !...:!TVBBBRPFT||||||||||!!^^**'   ||||
/         !.......:!?|||||!!^^**'            ||||
/         !.........||||                     ||||
/         !.........||||  ##                 ||||
/         !.........||||                     ||||
/         !.........||||  Hi, I'm a konkuter ||||
/         !.........||||  I live in a TXT    ||||
/         !.........||||  record ^3^         ||||
/         `.........||||                    ,||||
/          .;.......||||               _.-!!|||||
/   .,uodWBBBBb.....||||       _.-!!|||||||||!:'
/!YBBBBBBBBBBBBBBb..!|||:..-!!|||||||!iof68BBBBBb....
/!..YBBBBBBBBBBBBBBb!!||||||||!iof68BBBBBBRPFT?!::   `.
/!....YBBBBBBBBBBBBBBbaaitf68BBBBBBRPFT?!:::::::::     `.
/!......YBBBBBBBBBBBBBBBBBBBRPFT?!::::::;:!^*`;:::       `.
/!........YBBBBBBBBBBRPFT?!::::::::::^''...::::::;         iBBbo.
/`..........YBRPFT?!::::::::::::::::::::::::;iof68bo.      WBBBBbo.
/  `..........:::::::::::::::::::::::;iof688888888888b.     `YBBBP^'
/    `........::::::::::::::::;iof688888888888888888888b.     `
/      `......:::::::::;iof688888888888888888888888888888b.
/        `....:::;iof688888888888888888888888888888888899fT!
/          `..::!8888888888888888888888888888888899fT|!^*'
/            `' !!988888888888888888888888899fT|!^*'
/                `!!8888888888888888899fT|!^*'
/                  `!988888888899fT|!^*'
/                    `!9899fT|!^*'
/                      `!^*'"
```

Also this thing returned to me in chaos post on 39c3. I still have no idea who sent that to me!
(inb4 yes, I know it says puter, but we are still "6 months away from AGI", so I doubt it).

{{ image(
src="/ascii-art/chaos_post.jpeg",
alt="Chaos post to j-g00da, hackerspace żyrardów table at cebula cluster. From konkuter at 39c3. Ascii art of a computer with text on screen: Hi I'm a konkuter. I live in a txt record") }}

Anyway, stay tuned - in the next episode we will be building bash from source hosted on a nameserver
(If I can get [servfail](https://servfail.network/) to increase `client_max_body_size` in nginx, currently I was only able to store an image of demon core there).