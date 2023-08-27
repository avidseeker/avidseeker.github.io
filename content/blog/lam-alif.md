---
title: Arabic Lam Alif problem in Linux
date: 2022-08-29
---

[Video of the problem in Gedit](https://i.imgur.com/T1DYO3b.mp4)

Problem: letter La (لا) keypress results in a single Unicode character (U+FEFB),
instead of Lam (ل) and Alif (ا) (U+0644, U+0627) combined in one ligature. The
same problem for La variants: ﻷ، ﻵ، ﻹ.

For non-Arabic speakers, this is like having a key to type two characters: `fi`
(U+0046 U+0049), but types instead `ﬁ` (U+FB01).

This problem has been fixed in ibus. Since Gnome uses ibus by default, Gnome
desktops should have this problem resolved. If you're using KDE or other desktop
environment, this problem may still persist.

## Solution using ibus
Note: use a recent enough ibus version and make sure it is running and
really used. Do not set any environment variables that avoid using ibus.

1. Run `ibus-setup`. Make sure to set the env var: `GTK_IM_MODULE=ibus, QT_IM_MODULE=ibus, XMODIFIERS=@im=ibus`
2. Run `ibus-daemon`.
3. Go to input methods, add `ar-kbd-m17n`
4. Finally, run `im-chooser` and choose `ibus`.

## gnome

Solution on gnome: select ar-kbd(m17n) from the keyboard layouts ([issue](https://bugzilla.redhat.com/show_bug.cgi?id=2122899#c8)). Some distros like ubuntu don't come with it installed. You must install `ibus-m17n` and `ibus-typing-booster` then refresh gnome to find it. [User documentation](https://mike-fabian.github.io/ibus-typing-booster/docs/user/#1) for using ibus-typing-booster.

On Xorg, ar-kbd(m17n) layout will send English keyboard layout keys unless you set the environment variable `GTK_IM_MODULE=ibus`. This env variable doesn't have a clear effect on Wayland yet.

## KDE

Qt mysteriously handles this issue, i.e Qt-based apps like Kate don't have this issue. However, GTK-based apps, like Firefox and Chromium,  still have it.

Setting the environment variable QT_IM_MODULE=ibus doesn't have clear effect yet. Qt is suspected to implement XKB original compose mode to  deal with this issue.

Readings while figuring out how Qt handles this issue:

1. [Qt official i18n docs](https://doc.qt.io/qt-6/internationalization.html)
2. [Qt3 brief ligature docs](https://web.mit.edu/~firebird/arch/sun4x_59/doc/html/scripts.html)
3. [XKB limitation](https://www.freedesktop.org/wiki/Software/XKeyboardConfig/XKB2Dreams/): can't map a key to two characters.

## Issue tracker

1. Gnome: make m17n version the default ([issue](https://gitlab.gnome.org/GNOME/gnome-desktop/-/issues/212)).
2. Ubuntu: ar-kbd(m17n) keyboard layout not available.
3. [KDE](https://bugs.kde.org/show_bug.cgi?id=458442).
4. [Ubuntu](https://bugs.launchpad.net/ubuntu/+bug/1988133),

Compose support:

1. [Xorg](https://gitlab.freedesktop.org/xorg/lib/libx11/-/commit/21e464ec682ab23ba20ddf6bd72c6db214cfbe01): supported since 2008-06-20. ([xdg](https://bugs.freedesktop.org/show_bug.cgi?id=8195), [gitlab](https://gitlab.freedesktop.org/xorg/xserver/-/issues/346))
2. Ibus: [ibus-typing-booster](https://github.com/mike-fabian/ibus-typing-booster/issues/379), [ibus](https://bugzilla.redhat.com/show_bug.cgi?id=2125153).
3. [GTK](https://bugzilla.redhat.com/show_bug.cgi?id=2125163): [GTK fix](https://gitlab.gnome.org/GNOME/gtk/-/commit/952f85c12de13e978294af58f26694eddb3a1ee0): Fix regressed.
4. https://gitlab.gnome.org/GNOME/gtk/-/issues/5172

Other related discussions: [Google](https://code.google.com/archive/p/ibus/issues/1630), [askubuntu](https://askubuntu.com/questions/1426252/arabic-keyboard-layout-sends-ligatures-as-one-character-laa-problem), [arch forums](https://bbs.archlinux.org/viewtopic.php?id=277850), [Khaled Hosny blog post](https://khaledhosny.github.io/2009/05/01/حل-مشكلة-اللام-ألف-في-التوزيعات-الحديثة.html), [gnome](https://bugzilla.gnome.org/show_bug.cgi?id=537457).
