---
layout:     post
title:      Work continues
date:       2018-02-26 19:00:00
summary:    meson, gnome, freedesktop
---

It's been a while since my last post. I had many things in my to-do
list  and I wanted to finish some of them before writing this. This
is not entirely the case, but quite a few things have been done
along the way.

One of my major goals was to port `NetworkManager` to meson. The
fact that it is a fairly large software made the task difficult.
However, maintainers have been very open about meson adoption and
have helped a lot, so it [has received preliminary meson
support](https://mail.gnome.org/archives/networkmanager-list/2017-December/msg00041.html).
It's fully working, but there are still some open issues, so I should
make a come back one of these days and fix them.

One of these issues, which is shared by a number of packages, arose
from `gvfs`' [meson port](https://bugzilla.gnome.org/show_bug.cgi?id=789877#c16).
`gdbus-codegen` generates both source code and header at the same
time, so meson is not able to generate individual targets and,
therefore, is unable to generate dependencies only on the header.
The fix for this required modifications in both `glib` and `meson`.
After some iterations and some help, `glib` is finally [fixed](https://bugzilla.gnome.org/show_bug.cgi?id=791015)
and `meson`'s fix is [on its way](https://github.com/mesonbuild/meson/pull/2930).

During this time I have also continued porting some more packages to
meson, and there are already some [patches](https://bugs.freedesktop.org/show_bug.cgi?id=104273)
[waiting](https://bugzilla.gnome.org/show_bug.cgi?id=793087) for
[review](https://bugs.freedesktop.org/show_bug.cgi?id=105209).

Still, it's not all new work. While my meson skills are improving,
I like going back to previous ports and making [some](https://bugzilla.gnome.org/show_bug.cgi?id=793627)
[improvements](https://bugzilla.gnome.org/show_bug.cgi?id=793719).
I've also had the opportunity to help and [some](https://bugzilla.gnome.org/show_bug.cgi?id=791421)
[more](https://bugzilla.gnome.org/show_bug.cgi?id=792699) packages
have taken a step forward and removed autotools.

Some areas look a [little greener now](https://wiki.gnome.org/Initiatives/GnomeGoals/MesonPorting)
:smile:.
