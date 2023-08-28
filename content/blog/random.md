---
title: Random notes
date: 2023-08-25
---

Xorg DE button support:
* XF86RotateWindows
* XF86TaskPane

## Obscure Windows features
* [Binding files to files](https://bbs.archlinux.org/viewtopic.php?pid=2114455#p2114455): html pages are binded to their asset directories.
* [Create shortcut (Desktpo entries)](https://wiki.archlinux.org/title/Desktop_entries#Usage): different than a symlink in the sense that it just launches. There are many alternatives
(E.g: scripts using readlink, etc.) but file manager support would be cool.
* [Detailed disk usage](https://lemm.ee/post/5648489)

## XDG extended attributes
* A standardized tag for marking files as "favorite" (E.g: featured by Nautilus but without using xattrs).
* Attribute for binding files with each other. See [here](https://bbs.archlinux.org/viewtopic.php?pid=2114455#p2114455).
* [Dolphin ASCII xattrs](https://discuss.kde.org/t/4392)

## Spreadsheet editor
A spreadsheet program that sucks less:
* Support for custom number of rows and columns. ([LO](https://ask.libreoffice.org/t/86321), [sc-im](https://github.com/andmarti1424/sc-im/issues/818))
* Vim as a spreadsheet editor: [Filter view](https://neovim.discourse.group/t/4070)
* [Issue commands by typing](https://bugs.documentfoundation.org/show_bug.cgi?id=153002): [Styling commands](https://bugs.documentfoundation.org/show_bug.cgi?id=153001)
* Easily imports from other formats: [html](https://bugs.documentfoundation.org/show_bug.cgi?id=152984), [MediaWiki](https://bugs.documentfoundation.org/show_bug.cgi?id=156691)
* [Reorder rows and columns](https://bugs.documentfoundation.org/show_bug.cgi?id=156695)
* [Alternative cell colors support](https://bugs.documentfoundation.org/show_bug.cgi?id=155907)
* [Clip cell wrapping](https://bugs.documentfoundation.org/show_bug.cgi?id=155800)

LO bugs:
* [Can't undo/redo freezing actions](https://bugs.documentfoundation.org/show_bug.cgi?id=155803)
* [Dark theme problems](https://bugs.documentfoundation.org/show_bug.cgi?id=155906)
* [Access keys not available in tabbed UI](https://bugs.documentfoundation.org/show_bug.cgi?id=156633)

## Random notes
* You don't need a syncing service. Use the one and [only one sync thing](https://github.com/avidseeker/awesome-syncthing) for all of your applications.
* You don't need [Vimium](https://github.com/philc/vimium): It adds to your browser fingerprint. Instead, use `'` on Firefox to quickly click a link. And `space,shift+space` for going up or down.
