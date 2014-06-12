---
layout: post
title: "I watched the stream!"
---

Great news! I just completed porting of ogg muxer and httpstreamer consumer component. And with that, I "watched" a stream using Videotest producer + Theora encoder + ogg muxer + httpstreamer. The stream was created using this [configuration] and here is the screenshot:

![screenshot]

Same instructions in my earlier post could be used to watch this stream now. Even easier method is using the configuration assistant in flumotion-admin gui. Just check the Videotest producer option, uncheck the overlay options and choose other default options. The stream was okay, there were the following gstreamer warnings though. I'm going to port the audio test producer now.

{% highlight bash %}
(flumotion-job:23247): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-depay:src> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:23247): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-identity:src> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:23247): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<videoconvert0:src> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:23247): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<encoder:sink> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:23247): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<videoconvert0:sink> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:23247): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-identity:sink> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:23249): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-depay:src> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:23249): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-identity:src> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:23249): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-identity:sink> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:23248): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-depay:src> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:23248): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-identity:src> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:23248): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<sink:sink> Sticky event misordering, got 'segment' before 'caps'

(flumotion-job:23248): GStreamer-WARNING **: gstpad.c:4506:store_sticky_event:<eater:default-identity:sink> Sticky event misordering, got 'segment' before 'caps'
{% endhighlight %}

[configuration]: https://github.com/aps-sids/flumotion-orig/blob/08ddcaae8321a1e3c970277b059fe889d21bcec4/test_config.xml
[screenshot]: http://i.imgur.com/hurHQGb.png =100%
