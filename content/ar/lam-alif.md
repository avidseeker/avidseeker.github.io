---
title: Arabic Lam Alif problem on Linux
date: 2022-08-29
tags:
 - arabic
---

![Screenshot of the problem in Gedit](https://i.imgur.com/SrUKXuc.jpeg)

[Video of the problem in Gedit](https://i.imgur.com/T1DYO3b.mp4)

Problem: letter La (لا) keypress results in a single Unicode character (U+FEFB),
instead of Lam (ل) and Alif (ا) (U+0644, U+0627) combined in one ligature. The
same problem for La variants: ﻷ، ﻵ، ﻹ.

For non-Arabic speakers, this is like having a key that is supposed to send two
characters: `fi` (U+0046 U+0049), but it sends instead one ligature: `ﬁ` (U+FB01).

This problem has been fixed in ibus. Since Gnome uses ibus by default, Gnome
desktops should have this problem resolved. If you're using KDE or other desktop
environment, this problem may still persist.

## Solution: install ibus
1. Install ibus v1.5.28 or later:

For Arch Linux
```bash
# pacman -S ibus
```

For Ubuntu/Debian-based:
```bash
# apt install ibus
```

For Fedora:
```bash
# dnf install ibus
```

2. Run `ibus-setup`
3. Run `ibus-daemon`.
4. Run `im-chooser` and choose `ibus`.
5. Restart Xorg session

Some distributions like [Arch](https://bbs.archlinux.org/viewtopic.php?id=287812) may not have
`im-chooser`. In that case make sure the following [environment variables](https://wiki.archlinux.org/title/Environment_variables) are
set
```
GTK_IM_MODULE=ibus
QT_IM_MODULE=ibus
XMODIFIERS=@im=ibus
```

## Applications affected
Qt mysteriously handles this issue, so Qt-based apps like Kate are not affected
by this. On the other hand, gtk-based apps, like Firefox and Chromium, do have
this problem.

Setting the environment variable `QT_IM_MODULE=ibus` doesn't have clear effect
yet. Qt is suspected to solve this issue by implementing XKB original compose
mode.

Readings while figuring out how Qt handles this issue:
1. [Qt official i18n docs](https://doc.qt.io/qt-6/internationalization.html)
2. [Qt3 brief ligature docs](https://web.mit.edu/~firebird/arch/sun4x_59/doc/html/scripts.html)

## Technical details
The problem originates from [XKB limitation](https://www.freedesktop.org/wiki/Software/XKeyboardConfig/XKB2Dreams/)
that prevents it from mapping a single keypress to multiple keysyms. The
current solution works by utilizing [compose tables](https://en.wikipedia.org/wiki/Compose_key) support of input methods.
The idea is to map a key sequence of length 1 consisting of the ligature
(U+FEFB) into the 2 characters: (U+0644, U+0627). This is why it is considered
"hacky": compose function was never designed to be used that way. And this can
actually be seen from where XCompose reads from:

```
cat /usr/share/X11/locale/en_US.UTF-8/Compose | grep LAM
---
<UFEFB>	: "لا" # ARABIC LIGATURE LAM WITH ALEF
```

So virtually any input method having this hack of "single-letter compose
sequence" can actually solve this problem. And so despite [XIM](https://en.wikipedia.org/wiki/Xim)
being an old and unrecommended input method, it still solve this problem since
it supports the "hack". Try setting this as an environment variable:

```
GTK_IM_MODULE=xim
```

## Single-key compose sequence:
* [Xorg](https://gitlab.freedesktop.org/xorg/lib/libx11/-/commit/21e464ec682ab23ba20ddf6bd72c6db214cfbe01): supported since 2008-06-20.
* [XDG](https://bugs.freedesktop.org/show_bug.cgi?id=8195): [Gitlab](https://gitlab.freedesktop.org/xorg/xserver/-/issues/346)
* [ibus-typing-booster](https://github.com/mike-fabian/ibus-typing-booster/issues/379) supported since v2.19.0.
* [ibus](https://bugzilla.redhat.com/show_bug.cgi?id=2125153): supported since ibus-1.5.27-9.fc38.

GTK changelog:
* 2022-09-08: [bugzilla](https://bugzilla.redhat.com/show_bug.cgi?id=2125163)
* 2022-09-12: [Gitlab](https://gitlab.gnome.org/GNOME/gtk/-/issues/5172)
* 2022-09-13: [Proposed fix for GTK4](https://gitlab.gnome.org/GNOME/gtk/-/commit/952f85c12de13e978294af58f26694eddb3a1ee0)
* 2022-08-08: [Fix regressed](https://gitlab.gnome.org/GNOME/gtk/-/merge_requests/6358)

## Issue tracker
Archived discussions:
* [Gnome](https://bugzilla.gnome.org/show_bug.cgi?id=537457)
* [KDE](https://bugs.kde.org/show_bug.cgi?id=458442)
* [Ubuntu](https://bugs.launchpad.net/ubuntu/+bug/1988133)
* [askubuntu](https://askubuntu.com/questions/1426252/arabic-keyboard-layout-sends-ligatures-as-one-character-laa-problem)
* [Google](https://code.google.com/archive/p/ibus/issues/1630)
* [arch forums](https://bbs.archlinux.org/viewtopic.php?id=277850)
* [Khaled Hosny blog post](https://khaledhosny.github.io/2009/05/01/حل-مشكلة-اللام-ألف-في-التوزيعات-الحديثة.html)

## Credits
Thanks for your contributions and responsiveness to closing these issues.
* Fujiwara San
* Matthias Clasen
* Mike Fabian

On an unrelated note, single-key compose sequence might be an easy implementation for
[Tom Scott's](https://youtu.be/lIFE7h3m40U) emoji keyboard.
