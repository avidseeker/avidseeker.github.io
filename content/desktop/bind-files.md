---
title: Binding files to belong to other files
---

There was an old feature in Windows that somehow bind files to each other. Try
this on Windows: Ctrl+S to save this page as HTML, then rename the HTML file,
you'll get a dialog like:

> If you rename this file, it will no longer blong to the folder 'Linux -
> Wikipedia_files'

![Dialog showing the prompt](https://i.imgur.com/lSNh2Cn.png)

And when the html file is moved to another location, its asset directory is also
moved.

The use cases for this are plenty. The most common one is when you have a lot of
markdown files with corresponding asset directories (think of static websites
generators).

When I switched to Linux, I just accepted this might require a lot of work to
get implemented. But I was just looking into [Extended attributes](https://wiki.archlinux.org/title/Extended_attributes) and thought it
might be way easier. Of course, every file manager (and perhaps CLI utilities)
might need to be reworked to respect the attached xattr, but it still simplifies
the job.

## See also
* [Discussion](https://bbs.archlinux.org/viewtopic.php?pid=2114455)
