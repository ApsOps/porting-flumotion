---
layout: post
title: "Problems with Overlay component"
---

As per my last post, I was facing some problems with overlay component. With help of Sebastian Dröge (slomo) from #gstreamer, I was able to fix the data flow error but the following error still remains.

{% highlight bash %}
GStreamer-CRITICAL **: gst_segment_to_running_time: assertion `segment->format == format' failed
{% endhighlight %}

I'm looking into the DEBUG logs and stack traces, and hope to fix this soon.
