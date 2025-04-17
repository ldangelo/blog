+++
categories= ["Productivity"]
tags= ["Keyboard", "Shortcuts", "Mouseless" , "Home Row Mods"]
title= "Remap your keyboard to make your workflow more efficient"
date = "2025-03-17"
draft= true
comments=true
+++

It was 2:30 AM, and I was frantically trying to fix a critical production bug before the morning standup. Reach for the mouse, click through menus, back to the keyboard, type a few lines, reach for the mouse again... I could feel the rhythm breaking with each context switch. That's when it hit me: what if I never had to leave my keyboard at all?

## Overview

I've been on a mission lately to stop using my mouse. Why, one might ask?

The reason is simple. I'm much more productive if I can keep my hands on my keyboard!

Moving my hands off my 'home row' interrupts my train of thought and slows me down.

I've tried many ways to accomplish this task. From an external programmable keyboard like the [Glove80](https://www.moergo.com/) to only using emacs with a browser and builtin MacOS shortcuts to switch between apps.

Honestly, the Glove80 is a spectacular keyboard and I use it while I'm tied to my desk.

But this has one glaring issue! When I'm not using my external keyboard, I lose my productivity shortcuts.

This led me on a journey to find a way to remap my laptop keyboard to use the same shortcuts I use with the Glove80.

There are a number of tools that can be used to remap your keyboard. Depending on the operating system you may be using, there are various options available.

I'm using MacOS, so my choices were limited (somewhat). Below is a list of tools I've tried:

- [Karabiner Elements](https://karabiner-elements.pqrs.org/): This tool is a great way to remap your keyboard.
- [kmonad](https://github.com/kmonad/kmonad): This tool works for MacOS but I found it's configuration cumbersome.
- [Hammerspoon](https://www.hammerspoon.org/): Hammerspoon is much more than a keyboard remapping tool.
- [Kanata](https://github.com/jtroo/kanata): This is my choice and my configuration is below.

## What are Home Row Mods?

Let's first deconstruct the term. The "home row" refers to the middle row of
alpha keys. On an English QWERTY keyboard this would be ASDFGHJKL;. This row is
called the "home row" because if one were to follow touch typing technique, this
is the row of keys on which your fingers are supposed to rest on. The bars or
the dish found on F and J help to find back the home position without looking at
the keyboard — this is especially important for relatively big keyboards which
require you to move your hands to hit some of the keys like for example
Backspace or the arrow keys on a classic TKL and thus throw you off home
position.

> **🔑 KEY TAKEAWAY**  
> The home row is where your fingers naturally rest while typing (ASDFGHJKL;).
> By placing modifiers here, you never need to move your hands from their optimal position.

![Home Row](https://precondition.github.io/assets/images/home-row-mods/f-j-bumps-on-keyboard.jpg)

Next is "mods". What is meant by "mods"? In this case, "mods" refer to
modifiers, that is to say ⇧ Shift, ⎈ Control, ⎇ Alt, and ◆ GUI. The last
modifier in the list is also known as WinKey on Windows, Command on MacOS or
Super/Meta1 on Linux and BSD. Do not confuse the term with actual graphical user
interfaces.

So this means that "home row mods" are about placing modifiers on the home row.

> **💡 TIP**  
> Home row mods use tap for letters, hold for modifiers. For example, tapping 'F' types 'f',
> but holding 'F' activates Shift, allowing powerful key combinations without moving your hands.

## Kanata

I have settled on using kanata (which technically uses the virtual keyboard driver from Karabiner Elements). The reasons for this are simple:

- Simple to configure
- Runs in the background
- Works on MacOS

## My Kanata Configuration

```

(defcfg
  process-unmapped-keys yes
)

(defsrc
    esc  f1   f2   f3   f4   f5   f6   f7   f8   f9   f10  f11  f12
    lsgt 1    2    3    4    5    6    7    8    9    0    -    =    bspc
    tab  q    w    e    r    t    y    u    i    o    p    [    ]
    caps a    s    d    f    g    h    j    k    l    ;    '    \    ret
    lsft grv  z    x    c    v    b    n    m    ,    .    /    rsft
    fn   lctl lalt lmet           spc            rmet ralt
)

(deflayer base
    ;; everything is exactly the same, only the f-row is changed.
    ;; you can of course change any of the other mappings.
    esc  🔅   🔆    ✗    ✗    ✗    ✗    ◀◀   ▶⏸   ▶▶   🔇   🔉   🔊
    lsgt 1    2    3    4    5    6    7    8    9    0    -    =    bspc
    tab  q    w    @e    r    t    y    u    @i    o    p    [    ]
    caps @a  @s    @d    @f    g    h    @j    @k    @l    @;    '    \    ret
    lsft grv  z    x    c    v    b    n    m    ,    .    /    rsft
    fn   lctl lalt lmet           spc            rmet ralt
)

(deflayer nomods
    ;; everything is exactly the same, only the f-row is changed.
    ;; you can of course change any of the other mappings.
    -  -   -    -    -    -    -    -   -   -   -   -   -
    - -    -    -    -    -    -    -    -    -    -    -    -    -
    -  -    -    e    -    -    -    -    i    -    -    -    -
    - a  s    d    f    -    -    j    k    l    ;    -    -    -
    - -  -    -    -    -    -    -    -    -    -    -    -
    -   - - -           -            - -
)

(defvar
  ;; Note: consider using different time values for your different fingers.
  ;; For example, your pinkies might be slower to release keys and index
  ;; fingers faster.
  tap-time 200
  hold-time 400
  slow-hold-time 500)

(deftemplate charmod (char mod)
  (switch
    ((key-timing 3 less-than 450)) $char break
    () (tap-hold-release $tap-time $slow-hold-time $char $mod) break
  )
)

(defalias
  ;; hold e or i for hyper key
  hyper (multi lctl lalt lmet lshift)
  e (t! charmod e (multi lctl lalt lmet lshift))
  i (t! charmod i (multi rctl ralt rmet rshift))
  a (t! charmod a lctl)
  s (t! charmod s lalt)
  d (t! charmod d lmet)
  f (t! charmod f lsft)
  j (t! charmod j rsft)
  k (t! charmod k rmet)
  l (t! charmod l ralt)
  ; (t! charmod ; rctl)
)

```

Hopefully you can figure out how this works from the configuration. If not
there is plenty of documentation, samples and a very helpful discussions
forum on the kanata website. Essentially, this configuration means that
if I hold down the f or j keys they turn into shift, the d or k keys turn into gui (CMD on MacOS), s or l turn into alt and a or ; turn into control.

> **🔧 PRO TIP**  
> The secret to a productive home row mod setup is the timing. Adjust tap-time and hold-time values
> to prevent accidental activations while still keeping modifiers easily accessible.

Additionally I have mapped e or i to hyper (a special MacOS modifier) that
I use for creating application shortcuts with [raycast](https://www.raycast.com/).

## Conclusion

Using home row mods I limit the movement of my fingers to 'control' my
computer, making the experience much more enjoyable.

Remapping my home row is a foundational component to the rest of my
keyboard productivity system. I use other tools like [Raycast](https://raycast.com/),
[WezTerm](https://wezterm.org/), neovim and emacs to round out my system.
I will be producing additional blog posts on these other tools followed
up by a video of using the entire system in anger. With my entire 'system' in place I can launch apps, switch between apps, scroll windows, edit text, etc... All without ever leaving the keyboard. For the rare occassion where
I actually need to use the mouse I use [mouseless](https://mouseless.org/) to do it
from the comfort of my keyboard.
