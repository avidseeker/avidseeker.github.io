---
title: Type-ahead find
date: 2023-10-27
---

## Type-ahead find
Type-ahead find is such an underrated feature that I don't think people really
paid attention to despite being from the file explorer of WindowsXP.

It lets you select a file by typing its initial characters. So far, the best
GUI file managers implementing this are Thunar and Dolphin (I think even Windows
Explorer has it). But Dolphin annoyingly added a "filtering" feature that made
pressing a space an annoyance. This made me look into terminal file managers
that I can set them precisely how I want without being affected by such annoying
updates.

I don't know why terminal file managers insist on vim keybindings. They could be
the best for editing text but not for navigating between files. This is like
using `j,k` to move up and down inkscape tools instead of just pressing `p` for
pen or `t` for text.

### Workaround
Ranger almost has this feature, but you need to type `f` to enter
"find" mode. If there is a way to enable "find" mode in Ranger by default, this
will solve the problem.

I'm currently using [lf](https://github.com/gokcehan/), and the current
[workaround](https://github.com/gokcehan/lf/issues/1118) I figured was remapping of all keys

```
# Nav
map <a-h> updir
map <a-j> down
map <a-k> up
map <a-l> open
map <enter> open
map <space> :toggle
map <c-w> quit
map <f-2> rename

map q push :find<enter>q
map w push :find<enter>w
map e push :find<enter>e
map r push :find<enter>r
map t push :find<enter>t
map y push :find<enter>y
```

## See also
* [Incremental search](https://en.wikipedia.org/wiki/Incremental_search#Searches_for_files_and_media)
