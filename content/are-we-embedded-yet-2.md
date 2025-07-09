+++
title = "Are We Embedded Yet? #2"
date = "2025-06-11"
in_search_index = true
description="No-std support, RITW challenge, Mousefood-based guitar tuner and more!"
[extra]
og_image="/are-we-embedded-yet.png"
+++

<div style="width:100%; text-align:center;">

_This series is meant to document and promote the joint effort of making ratatui truly portable._

</div>


## Ratatui alpha with no-std support released!

<!-- more -->

---

I’ve been between jobs lately, so I haven’t had much time to write an update.
**But great news - no_std support in [Ratatui](https://github.com/ratatui/ratatui) has landed!**
You can try it out in version `0.30.0-alpha.4`.

{{ image(
src="/other/no_std_ratatui_build.png",
alt="Ratatui compiled for aarch64-unknown-none") }}
_Ratatui compiled for `aarch64-unknown-none`._


## Rat in The Wild Challenge

---

We've launched a [RITW challenge](https://github.com/ratatui/ratatui/discussions/1886)
to inspire you to push [Ratatui](https://github.com/ratatui/ratatui) to its limits—and beyond!
With `0.30.0-alpha.4`, it's theoretically possible to run [Ratatui](https://github.com/ratatui/ratatui)
apps even on platforms like the PlayStation 1.

{{ image(
src="/projects/ratatui/ritw.jpg",
alt="Rat in The Wild Challenge") }}
_Read challenge rules [here](https://github.com/ratatui/ratatui/discussions/1886)_


## Update: mousefood

---

The obvious next step is to make [Mousefood](https://github.com/j-g00da/mousefood) compile without `std`,  
and I've already done that! I just need a bit more time to write documentation and test it on real hardware.

In the meantime, I've also been working on a simple [demo app](https://github.com/j-g00da/mousefood-esp32-demo) for [Mousefood](https://github.com/j-g00da/mousefood).  
It’s still in the early stages, but it will likely end up in the `examples/` directory of the main repo eventually.

{{ image(
src="/projects/mousefood/esp32_demo.gif",
alt="Mousefood demo running on esp32") }}
_Mousefood demo running on esp32._

By the way, [@orhun](https://github.com/orhun) - maintainer of [Ratatui](https://github.com/ratatui/ratatui) and author of
[git-cliff](https://github.com/orhun/git-cliff) and [ratzilla](https://github.com/orhun/ratzilla) -
is currently using [Mousefood](https://github.com/j-g00da/mousefood)
in his [tuitar](https://github.com/orhun/tuitar/) project and livestreaming his progress.
Check it out [here](https://www.youtube.com/@orhundev/streams)!

<video style="width: 100%; max-height: 80vh; margin-left: auto; margin-right: auto;" controls>
  <source src="/other/tuitar.mp4" type="video/mp4">
</video>

We're also planning a joint [future project](https://github.com/ratutility), so stay _tuned_. 👀


## Talks!

---

Last weekend I gave a 5 minute lightning talk at [Poznańska Impreza Wolnego Oprogramowania](https://piwo.sh) showing off what the
[Ratatui](https://github.com/ratatui/ratatui) community is cooking.

Besides talking about [Mousefood](https://github.com/j-g00da/mousefood)
and [RITW challenge](https://github.com/ratatui/ratatui/discussions/1886),
I showcased demos of:
- [tachyonfx](https://github.com/junkdog/tachyonfx)
- [bevy_ratatui_camera](https://github.com/cxreiff/bevy_ratatui_camera)
- [ratzilla](https://github.com/orhun/ratzilla)

{{ image(
src="/other/piwo2025.png",
alt="Me giving a Ratatui lightning talk at Poznańska Impreza Wolnego Oprogramowania") }}


Next month I will be giving a talk about [Mousefood](https://github.com/j-g00da/mousefood)
and porting [Ratatui](https://github.com/ratatui/ratatui) _everywhere_ 
at [Rust Gdańsk](https://www.meetup.com/pl-PL/rust-gdansk/). See you there!

{{ image(
src="/other/rust_gdansk.webp.avif",
alt="Rust Gdansk Meetup #9 - Jagoda Ślązak - Ratatui - Are We Embedded Yet? 1 July, 6 - 9 pm, Europejskie Centrum Solidarności") }}
