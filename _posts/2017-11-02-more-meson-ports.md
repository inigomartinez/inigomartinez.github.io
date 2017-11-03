---
layout:     post
title:      More meson ports
date:       2017-11-03 19:00:00
summary:    meson, gnome
---

It's been a hard working month, but it has resulted in 7 more meson
ports merged:

* [bijiben](https://bugzilla.gnome.org/show_bug.cgi?id=782707).
* [dconf](https://bugzilla.gnome.org/show_bug.cgi?id=784910).
* [dconf-editor](https://bugzilla.gnome.org/show_bug.cgi?id=784922).
* [gitg](https://bugzilla.gnome.org/show_bug.cgi?id=788796).
* [glib-networking](https://bugzilla.gnome.org/show_bug.cgi?id=786639).
* [gvfs](https://bugzilla.gnome.org/show_bug.cgi?id=786149).
* [network-manager-applet](https://bugzilla.gnome.org/show_bug.cgi?id=788146).

I had been hacking `bijiben` a bit before the summer, so I knew how
its source code was structured. This has paved the way towards
merging the meson port. After meson's merge, its build time
has been nicely reduced:

||autotools|meson|
|---|---|---|
|real|1m29,952s|0m24,149s|
|user|1m18,044s|0m48,021s|
|sys|0m10,002s|0m6,129s| 

`dconf` and `dconf-editor` being small packages, have not presented
any major difficulties. On the other hand, this has not allowed
meson to shine in build times.

*dconf*:

||autotools|meson|
|---|---|---|
|real|0m18,584s|0m12,910s|
|user|0m15,887s|0m21,702s|
|sys|0m2,069s|0m2,404s|

*dconf-editor*:

||autotools|meson|
|---|---|---|
|real|0m18,137s|0m8,387s|
|user|0m15,272s|0m14,628s|
|sys|0m1,966s|0m1,506s|

`gitg` presents a very pleasant graphical view of the repository
status. I have been using it for a while so I wanted to port it to
meson.

Just as `dconf`, it is an application entirely written in Vala, but
it is bigger and uses more dependencies. It even builds some shared
libraries that are then linked to the application executable. I went
through a number of issues that made me doubt if a meson port would
be possible, but meson was up to the task and eventually, I was able
to fully build `gitg`. However, one feature is missing, `valadoc`
support, though this could also be [solved](https://github.com/mesonbuild/meson/issues/894)
in the future.

The improvement in the build time is also noticeable:

||autotools|meson|
|---|---|---|
|real|2m13,239s|0m50,967s|
|user|1m56,893s|2m50,207s|
|sys|0m13,334s|0m14,923s|

`gvfs` and `glib-networking` have been an excellent teamwork
experience. [Ondrej](https://wiki.gnome.org/OndrejHoly) and
[Michael](https://wiki.gnome.org/MichaelCatanzaro) have been very
involved, and thanks to their testing, suggestions and improvements,
the meson ports have been very successful.

Although `glib-networking` is a rather small package, meson is able
to fully `configure`, `build` and `install` in less than 10 seconds:

||autotools|meson|
|---|---|---|
|real|0m37,635s|0m8,436s|
|user|0m33,423s|0m9,599s|
|sys|0m4,267s|0m1,465s|

(`gvfs` and `network-manager-applet` numbers can be found in a
[previous post](https://inigomartinez.github.io/2017/10/11/meson-and-gnome/))

I hope this trend continues in the future and results in more
packages being ported to meson.
