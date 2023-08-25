---
title: JPEG XL support status
date: 2023-08-25
tags:
 - tracker
---

This is an issue tracker for software with no support for JPEG XL. Check [this list](https://github.com/libjxl/libjxl/blob/main/doc/software_support.md) for supported software.

* [Libreoffice](https://bugs.documentfoundation.org/show_bug.cgi?id=156931)
* [Kolourpaint](https://bugs.kde.org/show_bug.cgi?id=462109)
* [Ghostwriter](https://bugs.kde.org/show_bug.cgi?id=473776)
* [Ueberzug](https://github.com/ueber-devel/ueberzug/issues/17). But its fork:
[Ueberzugpp](https://github.com/jstkdng/ueberzugpp) supports jxl.
* [Pillow](https://github.com/python-pillow/Pillow/issues/4247)
* [Ghostscript](https://bugs.ghostscript.com/show_bug.cgi?id=703844)
* [SumatraPDF](https://github.com/sumatrapdfreader/sumatrapdf/issues/1943)
* [VSCodium](https://github.com/microsoft/vscode/issues/191376)

Metadata:
* [Exiftool](https://github.com/exiftool/exiftool/issues/157): not all metadata supported.
* [libjxl](https://github.com/libjxl/libjxl/issues/1806): support uncompressed metadata encoding

## Browsers
* Chromium: behind a flag from version 91 to 109, [tracking bug](https://bugs.chromium.org/p/chromium/issues/detail?id=1178058)
* Firefox: behind a flag since version 90, [tracking bug](https://bugzilla.mozilla.org/show_bug.cgi?id=1539075)
* Safari: supported since version 17 beta [release notes](https://developer.apple.com/documentation/safari-release-notes/safari-17-release-notes), [tracking bug](https://bugs.webkit.org/show_bug.cgi?id=208235)
* Edge: behind a flag since version 91, start with `.\msedge.exe --enable-features=JXL`
* Opera: behind a flag since version 77.
* Basilisk: supported since version v2023.01.07, [release notes](https://www.basilisk-browser.org/releasenotes.shtml)
* Pale Moon: supported since version 31.4.0, [release notes](https://www.palemoon.org/releasenotes-archived.shtml#v31.4.0)
* Waterfox: [enabled by default](https://github.com/WaterfoxCo/Waterfox/pull/2936)

## Android
* [AOSP Gallery](https://issuetracker.google.com/issues/259900694)
* [Simple Gallery](https://github.com/SimpleMobileTools/Simple-Gallery/issues/2669)
* [Material Files](https://github.com/zhanghai/MaterialFiles/issues/995)

## Messaging apps
* [Signal](https://community.signalusers.org/t/50331)
* [Telegram Desktop](https://github.com/telegramdesktop/tdesktop/pull/25572)
* [Matrix](https://github.com/matrix-org/matrix-spec-proposals/pull/4030)
* Telegram iOS
* Telegram Android
