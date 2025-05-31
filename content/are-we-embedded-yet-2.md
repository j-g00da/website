+++
title = "Are We Embedded Yet? #2"
date = "2025-06-01"
in_search_index = true
description="No-std support in ratatui 0.30.0-alpha.4!"
[extra]
og_image="/are-we-embedded-yet.png"
+++

<div style="width:100%; text-align:center;">

_This series is meant to document and promote the joint effort of making ratatui truly portable._

</div>

## Ratatui alpha with no-std support released!

---

I’ve been between jobs lately, so I haven’t had much time to write an update.
**But great news - no_std support in [Ratatui](https://github.com/ratatui/ratatui) has landed!**
You can try it out in version `0.30.0-alpha.4`.

{{ image(
src="/other/no_std_ratatui_build.png",
alt="Ratatui compiled for aarch64-unknown-none") }}
_Ratatui compiled for `aarch64-unknown-none`._

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

If all goes well, I'm planning to give a lightning talk about [Ratatui](https://github.com/ratatui/ratatui) and [Mousefood](https://github.com/j-g00da/mousefood) at [piwo.sh](https://piwo.sh)
and bring a few flashed demo boards along!

By the way, [@orhun](https://github.com/orhun) - maintainer of [Ratatui](https://github.com/ratatui/ratatui) and author of
[git-cliff](https://github.com/orhun/git-cliff) and [ratzilla](https://github.com/orhun/ratzilla) -
is currently using [Mousefood](https://github.com/j-g00da/mousefood)
in his [tuitar](https://github.com/orhun/tuitar/tree/feat/mousefood) project and livestreaming his progress.
Check it out [here](https://www.youtube.com/@orhundev/streams)!

We're also planning a joint [future project](https://github.com/ratutility), so stay _tuned_. 👀
