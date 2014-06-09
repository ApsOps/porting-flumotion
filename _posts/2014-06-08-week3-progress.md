---
layout: post
title: "Week 3 Progress"
---

In this week, I fixed the running tests first of all. Running all the tests using `trial -rselect flumotion.test` was freezing due to mixing of gobject and gi. So, I created a working-tests.txt and a run_tests.sh to read this file and run only the tests for ported module.

There were some issues due to missing overrides. These were implemented in gst-python1.0 version 1.2.0 (maybe 1.1.9 as well) and above, but this package is not available for Ubuntu 12.04 precise. Compiling gst-python1.0 from source fixed these problems.

I continued and completed the porting of check.py and the Videotest producer. I also fixed a troubling issue about pspec set to None. Further, I've posted instructions about how to [run a test stream].

After this, Theora encoder was also ported and encoder component's mood is also set to 'happy'.

Final step needed to "watch" a stream is a sink, httpstreamer. After porting this and running the stream, I get following error:

{% highlight bash %}
(flumotion-job:7808): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-depay:src> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:7808): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-identity:src> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:7808): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<videoconvert0:src> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:7808): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<encoder:sink> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:7808): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<videoconvert0:sink> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:7808): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-identity:sink> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:7806): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-depay:src> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:7806): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-identity:src> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:7806): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<sink:sink> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:7806): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-identity:sink> Sticky event misordering, got 'segment' before 'caps'

{% endhighlight %}

In week 4, I will fix this issue, run a complete test stream successfully and continue with porting of Audiotest producer.

[run a test stream]: http://aps-sids.github.io/porting-flumotion/2014/06/06/run-a-test-stream/
