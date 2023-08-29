---
title: Bidi issues
date: 2023-08-25
tags:
 - tracker
---

* [Software support status](https://wiki.archlinux.org/title/Bidirectional_text)

Xorg problems:
* [Laam Alif problem](https://wiki.archlinux.org/title/Localization/Arabic#XKB_Lam_Alif_problem)

Gnome problems:
* [Keyboard layouts preview](https://gitlab.gnome.org/GNOME/gnome-control-center/-/issues/2434)
* [Gedit](https://gitlab.gnome.org/GNOME/gnome-text-editor/-/issues/561)
* [Nautilu](https://gitlab.gnome.org/GNOME/nautilus/-/issues/3039)
* [Gnome Terminal](https://gitlab.gnome.org/GNOME/gnome-terminal/-/issues/7992)

KDE problems:
* [Laa Problem on Konsole](https://bugs.kde.org/show_bug.cgi?id=471898)

## Libreoffice
* [Libreoffice metabug thread](https://bugs.documentfoundation.org/show_bug.cgi?id=112810)
* [Non-persisting text direction](https://bugs.documentfoundation.org/show_bug.cgi?id=151857)
* [Break line on text direction change](https://bugs.documentfoundation.org/show_bug.cgi?id=56408)

Fixed:
* [Squiggly lines covering misspelled Arabic words](https://bugs.documentfoundation.org/show_bug.cgi?id=151968): libreoffice-7-5

## Kashida justification
Arabic is one of the few languages that are cursive and connected by their nature.

This makes justifying text different for Arabic. In addition to justifying text
by spaces, there's Kashida justification.

This is a compilation of resources related to implementing Kashida justification
in various programs:

1. [Algorithm by Microsoft](https://web.archive.org/web/20130308140133/http://www.microsoft.com/middleeast/msdn/JustifyingText-CSS.aspx).
2. [LaTeX implementation](https://andreasmhallberg.github.io/stretchable-kashida/) by [Andreas Hallberg](https://github.com/andreasmhallberg).
3. [W3 Full Justification Proposal](https://www.w3.org/International/articles/typography/justification.en).

Open issues:
* [Incorrect display of Arabic](https://bugs.documentfoundation.org/show_bug.cgi?id=150516)
* [Syriac problem](https://bugs.documentfoundation.org/show_bug.cgi?id=140767).

## Websites
* 2022-08-30: [Reddit](https://www.reddit.com/r/bugs/comments/x1qdu6/)
* 2020-06-16: [element.io](https://github.com/vector-im/element-web/issues/14520)
* 2021-05-03: [Fluffy Chat](https://gitlab.com/famedly/fluffychat/-/issues/390)
* 2018-11-03: [Discord](https://support.discord.com/hc/en-us/community/posts/360030086752-Add-Right-to-Left-RTL-support-to-Discord)
* 2023-06-03: [Tutanota](https://www.reddit.com/r/tutanota/comments/13z584n/)
* 2021-07-21: [Lemmy](https://github.com/LemmyNet/lemmy-ui/issues/347)

## Workarounds
* [add-bidi-support](https://github.com/ahangarha/add-bidi-support): a Firefox addon to demonstrate bidi support on web pages.
* [markdown-it-bidi](https://github.com/dobidi/markdown-it-bidi): a plugin for markdown-it project to add bidi support to md-to-html parsers.
