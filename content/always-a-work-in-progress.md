+++
title = "Always a work in progress"
date = "2025-11-12"
in_search_index = true
description="I think I'll be fine."
[extra]
og_image="/do_stuff/scrible.png"
+++

I think 2025 was a good year (for me, it would be hard to say it was that great in general). 
Well, it still _is_ because as I'm writing this, it's 12th November.
I wanted to wait for the end of the year before starting to draft this post, but well - 
I'm in the right mood, and it makes more sense to act instead of holding back (this is probably a foreshadowing).

<!-- more -->

If you haven't read my last post, please read it first, because this is a kind-of-a-spin-off in the same universe,
and it may be worth to know the lore first.

This year I had countless breakdowns, had multiple moments where I didn't know at all what I want to do with my life
(so just a regular year) and if that's not enough - in April I lost my job,
which gave me a lot of reasons to be absolutely stressed out.
Wait... why do I think it was a good year then?

I made a lot of progress, but I won't talk about the high-level, calculable achievements, this is not LinkedIn.
I'm writing this post to dissect the real, low-level changes that made that happen -
so I can keep working on myself and be a happier person on average overall.
I will also write about what I currently struggle with and ramble about things that are vaguely related.
As with the last post - _it will be chaotic_ (That's the point) and very subjective,
unplug your computer from the wall **NOW** if you don't like this kind of things.

{{ image(
src="/always-a-wip/beam.gif",
alt="separator decoration") }}

For a few years I've been stuck in some kind of limbo where I wasn't able to start working on something new.
It was always either:

> I have absolutely no idea what to do, nothing feels interesting.

or

> I have a thousand ideas, and I'm in decision paralysis.

It's not like I don't fight these at all today, but it _is_ getting better. Let's dive into that.

## Just do it mentality

I've learned that very often how I feel about doing something has a large discrepancy with how
I _will_ feel if I actually take action upon it. If I can afford (and I'm not talking about just money) doing something,
and I think it's cool or interesting, or even just used to be interesting when I was't feeling down;
even if I don't "feel it" right now, I should just do it, because maybe I _will_ feel it.

> I was told that I use too long sentences back in elementary school. I will continue doing so till I die.

I'm not a talking just about creating things or starting new hobbies, but much more generally -
things like hanging out with people you like or traveling.
I just came to conclusion that sometimes you have to force yourself;
be your own parent that tells you to leave that damn phone and go touch the grass...
I've traveled to more countries this year alone, than I did my whole life up to 2025 - because I... just did it
(and I have no regrets).

The other part of what I call "just do it" mentality is about impulses.
Sometimes I have random ideas that maybe are just _mildly_ interesting, but don't require much work to become real.
It's like a quick time event. As a person who is not that spontaneous, I miss most of these -
but I'm slowly getting there and I like the results.

During Jesień Linuksowa (a FOSS conf), I gave a talk about Ratatui.
A big part of it was a showcase of Ratatui running in unexpected places,
I went back to my hotel room quite late that day, around 2 or 3AM and had this thought...
Hey can ratatui run within itself?
**Quick time event** - and I passed it.
I present to you [Ratrioshka](https://github.com/j-g00da/ratrioshka) -
a Ratatui matrioshka. It's not stupid - it's perfect, this is the kind of stuff that makes you keep going.

{{ image(
src="/always-a-wip/ratrioshka.png",
alt="Ratatui TUI running inside another ratatui TUI using kitty terminal protocol and soft_ratatui backend") }}

Anyway I passed another quick time event yesterday (as of writing this). I needed a `serde` feature that didn't exist -
I just instantly started working on it and got it to work as I wanted after few hours (my first proc macro, be gentle) -
released it as [serde_more](https://github.com/j-g00da/serde-more) crate.

```rust
use serde_more::SerializeMore;
use serde_json::json;

#[derive(SerializeMore)]
#[more(key="next")]
#[more(key="previous", position="front")]
struct Index {
    current: u32,
}

impl Index {
    fn next(&self) -> u32 {
        self.current.saturating_add(1)
    }
    fn previous(&self) -> u32 {
        self.current.saturating_sub(1)
    }
}

fn main() {
    let idx = Index { current: 5 };
    let value = serde_json::to_value(&idx).unwrap();
    assert_eq!(value, json!({
        "previous": 4,
        "current": 5,
        "next": 6
    }));
}
```

> Wow, this one is even useful!

You never know what you will get with quick time events, if you think about it - you loose.

I know this may be obvious but I also can't resist the urge to make it clear -
quick time events are not just about rust or even coding -
_I just spend way too much time in front of my computer_.

## Enjoy the process

When I was about 12, I found out about Minecraft, it was I think beta 1.7.3, they just added pistons,
there were no villagers, endermen or creative mode, and hostile mobs were just trying to reach you in straight
line, because A<sup>*</sup> was still a TODO. This game had me hooked up to the screen for hours every day,
I mined resources to build a longer railroad and when I was out of rails to place, I mined more.
Then when I slept (irl) I dreamt about mining iron and building railroads...

{{ image(
src="/always-a-wip/floppy.gif",
alt="separator decoration") }}

Did I have any end goal in that? Not really, I was just building longer and longer rail not thinking about it,
and I loved every single second. When I think about it now, I lost something very important at some point -
and when I talk to people my age, I'm far from being alone in this.
**I wish I could feel the same as I felt when I played Minecraft as a kid**.
You may say that there's just less and less new things to do when you get older... and you are partially right,
but I literally just did the same thing in a loop for months - mined iron and placed rails.
There must be something more to it and I think it's as simple as it's hard to master.

I won't be quoting Camus here, you know the Sisyphus myth.
I think what I _really_ lost was the ability to _not care_ about the end result and having satisfaction purely from
**JUST** _doing things_. Now hold on and take it with a grain... boulder of salt,
because we are reaching Freud-levels of what in Poland we call "chłopski rozum".
I do think we are born very good at "enjoying the process" and we lose it due to effect-driven mindset,
that our society forces upon us from a very young age (e.g. grades). One would ask - why so serious?

...Anyway

> Since my brain is already cooked, can I do something about it?

I don't know.

I'm trying to stop focusing on results when doing things for fun by simply monitoring my thought process -
when my thoughts fall into fantasizing about end results -
I backtrack to the last healthy node and redirect my thoughts into different branch. 

> Maybe I'm meta-thinking too much.

Of course this is not easy and I fail constantly, but it's too early to know if this is or is not the way to go...
will see.

There's also one more related problem - if you want to start enjoying the process,
the reason for that can easily be to be able to finish greater projects etc.,
which creates a contradiction... _I'm yet to learn how to genuinely not care_.

## We should all stare at the wall more

I've quited Instagram completely this year and have no regrets.
I've never had TikTok since I knew when it came out that I have to keep a safe distance or this thing will annihilate
my attention span. I was a fool because while keeping doors closed,
Instagram got in through the window with Reels.

> Darn it! We have [negative attention span](https://www.smbc-comics.com/comics/1762309096-20251105.png) at home!

Anyway, I progressively got off most of the social media,
I mostly use just Mastodon these days and can't be happier about it... _Well, I would like to use it less too though._

Getting back to the topic... - what I'm trying to do is to let myself get bored, and I'm not saying _bored_ as we all
already are, but _really_ bored, no stimulation, **staring-at-a-blank-wall-bored**.
I think this is what made me able to enjoy video games again - letting yourself to get bored _for real_.
Sadly I think I'm doing a little regress here as I have nothing on my phone to look at but still muscle memory makes me
open mail app and refresh it for no reason, or re-scroll the same timeline on Mastodon.

> There are like 5 people on fedi anyway

I think I need to get even more radical with it.
I wish I was able to get rid of the phone completely, but it's just too inconvenient these days to not have one...

## I'm still struggling

> TW: Suffering from success ahead

With all the changes taking place, I'm somehow getting new first world problems.
I've spent the previous year mostly trying to find something I can do in free time and constantly failing to get hooked
to it. At some point I decided I will just start reading books whenever I feel down and don't know what to do -
better option than just wasting time being stressed out.

So... I read "Hail Mary", "Do Androids Dream Of Electric Sheep", "Childhood's End", "Solaris",
"The Left Hand of Darkness", "The Word for World is Forest", "The Lathe of Heaven",
"Five Ways to Forgiveness" and "The Dispossessed"...

You may have noticed I really liked Le Guin's works. Anyway, this year I'm really busy, don't get me wrong -
in a good way mostly, _but_ I don't read as much anymore.
I have unfinished "The Wind's Twelve Quarters" on my nightstand for few months now.
It's not just books - remember how enthusiastic I was about pastagang in the last post?
I'm out of the loop completely right now! I simply don't have enough time.
Somehow by unblocking the creativity I'm now struggling with "not enough time in a lifetime".
I'm currently involved in multiple open source projects, my local hackerspace, I'm making music,
creating a video game and have ideas on many other projects.
I also still want to spend time with my SO and friends, travel and attend events,
and don't get me started on the backlog of media I want to read/watch/listen/experience;
_oh_ and then there are also chores.
There's simply not enough time to do it all and some activities will suffer..., 
some projects will never happen..., 
some things won't be experienced... 
and it's driving me nuts.

## I'll be fine

On one hand I think I started to "figure it out", on the other it feels like there's another Pandora's box
on the bottom of any Pandora's box I open. I have no idea what's gonna happen next, but maybe that's a good thing?
Life is hard and random, but for the first time - I think I'll be fine.

This will be continued...  
See ya!

[{{ image(
src="/always-a-wip/helium.gif",
alt="Helium atom animated") }}](https://jslazak.com/atom.xml)

_Btw. In case you didn't know - I have RSS/Atom feeds, just click the atom!_
