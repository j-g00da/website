+++
title = "Are We Embedded Yet? #1"
date = "2025-05-03"
in_search_index = true
description="soft_ratatui, updates on no_std ratatui and mousefood"
[extra]
og_image="/are-we-embedded-yet.png"
+++

<div style="width:100%; text-align:center;">

_This series is meant to document and promote the joint effort of making ratatui truly portable._

</div>

## soft_ratatui

---

> Software rendering backend for [ratatui](https://github.com/ratatui/ratatui). No GPU required. TUI everywhere.

Another new [Ratatui](https://github.com/ratatui/ratatui) backend just dropped - 
[soft_ratatui](https://github.com/gold-silver-copper/soft_ratatui)
by [@gold-silver-copper](https://github.com/gold-silver-copper), 
the creator of [egui_ratatui](https://github.com/gold-silver-copper/egui_ratatui). 
The crate uses [tiny-skia](https://github.com/linebender/tiny-skia) to render efficiently directly to a window, 
ditching the terminal emulator completely. 
This allows for much higher frame rates out of the box (~200 FPS). 
It will be especially useful for TUI games or interactive tools where smooth performance really matters!

{{ image(
src="TODO",
alt="soft_ratatui") }}

## no_std ratatui

---

[`Backend::Error` merged!](https://github.com/ratatui/ratatui/pull/1778)
One of the blockers for no_std ratatui was the explicit use of `std::io::Error` in `Backend` (and
by extension, in `Terminal` as well).
Now, `Backend` implementations must define an associated `Error` type.
Built-in backends will still use `std::io::Error`, but third-party ones
like [mousefood](https://github.com/j-g00da/mousefood)
can now use a different error type - which will enable a proper `no_std` compatibility!

I’m actually working on a [follow-up PR](https://github.com/ratatui/ratatui/pull/1817)
and ran into a pretty interesting issue,
so if anyone reading this has ideas, feel free to jump in and comment.

As for the layout cache problem I mentioned in the last post - 
since there's no great solution, [the decision for now
is to simply **not provide a cache in `no_std` mode**](https://github.com/ratatui/ratatui/pull/1795).

_We are one step closer to no_std ratatui._


## mousefood

---

Mousefood recently got italic modifier support as well as readme section about bold/italic fonts.
Additionally v0.2.1 patch was released 


