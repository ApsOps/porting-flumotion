---
layout: post
title: "Week 1 Progress"
description: ""
category: 
tags: []
---

This was a quick week. I did a couple of initial changes required for porting. A good thing done was that I was able to fix some errors and pass the test cases that failed last year. I successfully ported gstreamer.py base dependency module and changed the Gtk2Reactor (incompatible with gi) to Gtk3Reactor.

Tests still fail as "ImportError: Introspected and static glib/gtk bindings must not be mixed; can't import gireactor since pygtk2 module is already imported." So, I figured out we need to port PyGTK to PyGObject (aka PyGI) as well. As an initial quick approach, I tried using PyGTK compatibility layer ([PyGTKCompat]). This didn't turn out to very successful and tests gave segmentation fault.

I think converting the code manually would be a better idea since we can avoid using any layers and use the supported API directly. Still, I want to port other modules using 0.10 API first and try PyGTKCompat before going ahead and porting PyGTK to PyGI manually.

In Week 2, I will be completing the porting of other base and dependency modules.

[PyGTKCompat]: https://wiki.gnome.org/Projects/PyGObject/PyGTKCompat
