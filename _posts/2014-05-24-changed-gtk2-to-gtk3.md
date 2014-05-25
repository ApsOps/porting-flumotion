---
layout: post
title: "Changed Gtk2Reactor to Gtk3Reactor"
description: ""
category: 
tags: []
---

With the help of a mentor, I figured out the cause of the error in previous post (ported gstreamer.py). This was due to flumotion using Gtk2Reactor which is incompatible with gi. So, I changed it to use Gtk3Reactor.

Tests fail since there is still some use of gobject, particularly in flumotion/common/boot.py, which cannot be mixed with gi. This is causing the error and consequently some tests fail.

In addition to this, while changing the reactor to gtk3reactor, I noticed that pygtk2 is a dependency for flumotion which also needs to be ported since its not compatible with gi. Also, it uses a wrapper framework named kiwi that's unmaintained so that might need to be replaced as well (I don't know replaced with what, yet).

TODO:  Port PyGTK to PyGObject (aka PyGI)
