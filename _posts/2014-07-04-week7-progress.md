---
layout: post
title: "Week 7 Progress"
---

I've been traveling for past 3 days for some university related work. But, I have been working on my project as well. I somehow got an internet connection for posting this update.

First thing I did was porting of the disker consumer after fixing some issues. After this was ported, I was able to save the output from Videotest + Audiotest components to my disk as an OGG file.

Other than that, I fixed the problems with the "Feeder component Test" and it passes the test now. Basically, the feeder component is now using GstStructure instead of a simple tuple, but the test was sending a tuple. I changed that to send a GstStructure and test pass now.

I am going to work on other components in coming days.
