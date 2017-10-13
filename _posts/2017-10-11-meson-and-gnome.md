---
layout:     post
title:      Adventures with meson and GNOME
date:       2017-10-11 00:30:00
summary:    meson, gnome
---

I read something about meson in planet GNOME earlier this year.
Someone was interested and blogged about it. A new fast and user
friendly build system.

I've been using autotools for so many years now, that I can't
remember. It wasn't very pleasant to work with it, but it worked.
However, I was curious about meson and I started playing with it.

I used it in different projects at work and it fitted very well.
Usual mistakes in the build files were easily detected and I began
to realize that I did not spent as much time as before on the
build system and that I was more focused on coding.

After sending some patches to `bijiben`, while they were waiting
for review, I started working on the meson port of another GNOME's
application I had been looking at: gnome-todo.

This first meson patch was sent at the end of may. Soon after [an
initiative](https://wiki.gnome.org/Initiatives/GnomeGoals/MesonPorting)
arose to port GNOME's packages to meson. Yesterday, less than 5
months later, I sent my last patch porting another package to meson,
which makes it port number 23.

The list of GNOME's applications ported and their status is as
follows:

* gnome-todo: [done](https://bugzilla.gnome.org/show_bug.cgi?id=781908).
* bijiben: [in-progress](https://bugzilla.gnome.org/show_bug.cgi?id=782707).
* gnome-calendar: [done](https://bugzilla.gnome.org/show_bug.cgi?id=782843).
* libgepub: [done](https://bugzilla.gnome.org/show_bug.cgi?id=782994).
* totem: [done](https://bugzilla.gnome.org/show_bug.cgi?id=783205).
* devhelp: [in-progress](https://bugzilla.gnome.org/show_bug.cgi?id=783819).
* eog: [in-progress](https://bugzilla.gnome.org/show_bug.cgi?id=784354).
* vte: [blocked](https://bugzilla.gnome.org/show_bug.cgi?id=784561).
* gnome-terminal: [blocked](https://bugzilla.gnome.org/show_bug.cgi?id=784762).
* dconf: [in-progress](https://bugzilla.gnome.org/show_bug.cgi?id=784910).
* dconf-editor: [in-progress](https://bugzilla.gnome.org/show_bug.cgi?id=784922).
* gnome-disk-utility: [done](https://bugzilla.gnome.org/show_bug.cgi?id=784975).
* gnome-control-center: [in-progress](https://bugzilla.gnome.org/show_bug.cgi?id=785414)
* gvfs: [in-progress](https://bugzilla.gnome.org/show_bug.cgi?id=786149).
* gnome-bluetooth: [done](https://bugzilla.gnome.org/show_bug.cgi?id=785737).
* glib-networking: [in-progress](http://bugzilla.gnome.org/show_bug.cgi?id=786639).
* telepathy-account-widgets: [in-progress](https://bugzilla.gnome.org/show_bug.cgi?id=786969).
* gnome-documents: [done](https://bugzilla.gnome.org/show_bug.cgi?id=787013).
* gnome-photos: [in-progress](https://bugzilla.gnome.org/show_bug.cgi?id=787094).
* gnome-online-accounts: [in-progress](https://bugzilla.gnome.org/show_bug.cgi?id=787634).
* gnome-session: [in-progress](https://bugzilla.gnome.org/show_bug.cgi?id=787806).
* network-manager-applet: [in-progress](https://bugzilla.gnome.org/show_bug.cgi?id=788146).
* gitg: [in-progress](https://bugzilla.gnome.org/show_bug.cgi?id=788796).

Although meson has nice features, in my case, its ease of use is the
biggest win. meson is usually also faster than autotools, and some
of these ports, particularly the big packages, build a lot faster. 
Here are some raw numbers using the `time` command in a *full build*
(`configure`, `build` and + `install`):

gnome-control-center:

||autotools|meson|
|---|---|---|
|real|4m29,223s|1m34,726s|
|user|3m59,784s|5m22,009s|
|sys|0m33,556s|0m21,560s|

gnome-online-accounts:

||autotools|meson|
|---|---|---|
|real|2m25,265s|0m38,212s|
|user|2m2,687s|1m16,560s|
|sys|0m12,824s|0m5,317s|

gvfs:

||autotools|meson|
|---|---|---|
|real|2m22,357s|0m34,689s|
|user|1m58,643s|1m49,066s|
|sys|0m14,816s|0m9,439s|

network-manager-applet:

||autotools|meson |
|---|---|---|
|real|2m9,749s|0m36,627s|
|user|1m55,974s|1m43,569s
|sys|0m12,887s|0m9,874s|

At the moment, only 7 packages merged the patches. However, most
maintainers are positive about adopting meson at some point.

Let's see how this goes.
