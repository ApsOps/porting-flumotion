---
layout: post
title: "Week 9 Progress"
---

This week, I ported dvswitch gstreamer plugin to 1.0 version. It was compiled and I tested both dvswitch source and sink plugins. Tests run properly, but I'm unable to successfully build it as a debian package.

I also ported [dvsource-v4l2-other] to gstreamer-1.0 so it could create the dvswitch stream from a DV file or any v4l2 source for that matter.

Now, I'm working on porting the flumotion ugly components that are required for running the TimVideos streaming-system properly.

[dvsource-v4l2-other]: https://github.com/aps-sids/dvsource-v4l2-other