+++
title = "Are We Embedded Yet? #0"
date = "2025-04-18"
in_search_index = true
+++

<div style="width:100%; text-align:center;">

> _**Ratatui** gave us beautiful TUIs._ \
_**Ratzilla** expanded it to the web._ \
_But why shall we stop there?_ \
_**Why shall we stop anywhere?**_
> <h1 style="justify-content:center;"> --- Are We Embedded Yet? --- </h1>
> This series is meant to document and promote the joint effort of making ratatui truly portable.

</div>

## no_std ratatui

---

I've started the [discussion](https://github.com/ratatui/ratatui/discussions/1746)
on making `ratatui-core` crate no_std just two weeks ago, when I realized 
that [mousefood](https://github.com/j-g00da/mousefood) can't become anything more than
just a gimmick without few upstream changes.
Today, thanks to commitment of the maintainers and help from the community,
I'm pretty optimistic that we can see ratatui on stm32 in just few weeks.
And I'm not talking about just `ratatui-core` (which was planned for the "first stage"), 
but `ratatui-widgets` is no_std already!

Check out the [tracking issue](https://github.com/ratatui/ratatui/issues/1750)!

The last major thing to resolve is to provide an alternative, no_std implementation
of layout caching.

## {{ image(
src="https://github.com/j-g00da/mousefood/blob/99b654737ff30c08a9abdfcdee99eef6bc876712/assets/logo/mousefood_text_light.svg?raw=true",
alt="mousefood")}}

---

**[Mousefood](https://github.com/j-g00da/mousefood) v0.2 is out!** 
This is the point, where the project stops being just a proof of concept and due to that,
most of the changes since v0.1 are refactoring ones. 
I decided that this also is the time to finally write tests - currently coverage is just around 60%,
but this should greatly improve in the coming weeks.
This doesn't mean there are no new features! The new version comes with an optional support of EPDs!

{{ image(
src="/projects/mousefood/epd-weact.jpg",
alt="mousefood on epd") }}

More on that in the [docs](https://docs.rs/mousefood/0.2.0/mousefood/#epd-support).

### What's next?

The obvious next step after ratatui becoming no_std would be adapting
mousefood to use that and testing it out on some previously unsupported device
(I actually already have a stm32f7 waiting for that.)
_But_ there is still a lot of other things to complete in mousefood
such as cursor support (currently cursor is hardcoded at (0,0) and hidden),
handling the rest of modifiers (there's a PR by [@y5](https://github.com/y5) waiting 
for the next release of ratatui that will also add colored underlines) 
or color conversion from indexed colors.
I also want to eventually add terminal themes.

_Also_ I want to finally start writing some actual apps using it, instead of just demos!
I've got some interesting ideas for that, but first I need to find some more time...
If you haven't seen already, [@micielski](https://github.com/micielski) actually managed to
[read IRC messages on esp32 and display them on SPI screen using mousefood!](https://github.com/intuis/mnyaoo32)

## ratatui-uefi

---

Something I didn’t know until recently: there _are_ UEFI targets with std support in nightly Rust.
Even crazier - just a few days ago, I didn’t expect to see **Ratatui running on UEFI** this week! Check out
[@reubeno](https://github.com/reubeno)'s new ratatui backend - 
[`ratatui-uefi` and a companion crate for handling inputs - `terminput-uefi`](https://github.com/reubeno/tui-uefi?tab=readme-ov-file)
A truly amazing project that opens doors to some fun ideas.

{{ image(
src="/other/ratatui-uefi.png",
alt="mousefood")}}
