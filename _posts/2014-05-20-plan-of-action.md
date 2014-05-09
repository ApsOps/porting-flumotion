---
layout: post
title: "Plan of Action"
description: ""
category: 
tags: []
---

I just reached back home after the college exams. Phew, what a semester it was. I have started working on the project and as a first step, I have prepared a plan of action which will help me work and track the results better, I hope.

A quick grep of "import gst" gives me a list of files that need to be changed first for using gst-1.0 API. I will be porting Audio and Video Test producers as the initial porting target in the following week. Before that, dependency modules for these test producers need to be ported. The dependency modules (recursively) for Videotest producer are:

* flumotion/common/gstreamer.py
* flumotion/component/feedcomponent.py
* flumotion/component/feedcomponent010.py
* flumotion/component/padmonitor.py
* flumotion/component/feeder.py

So, these modules will be ported in this week. Following this will be the porting of the Test producers and the respective unit tests.