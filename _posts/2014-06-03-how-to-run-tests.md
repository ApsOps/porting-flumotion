---
layout: post
title: "How to run tests?"
---

Running all the tests in module was broken due to mixing of gobject and gi. So, I've created a `working-tests.txt` and a `run_tests.sh` to read this file and run the tests. As a result, Travis build is passing now as seen on badge on sidebar of this blog.

Again with the Gstreamer version 1.2.1 issues, some overrides are not implemented (like Gst.Fraction class). So, I'm adding the implementation myself (which I shall remove when the whole thing is ported).
