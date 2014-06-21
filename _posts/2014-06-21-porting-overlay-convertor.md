---
layout: post
title: "Porting Overlay Convertor"
---

I started with porting the Overlay Convertor element which is used to add any text or logo over a video feed. This required a lot of work as I had to port Pango and PangoCairo to the new PyGI. I did the changes and tried to create a stream which resulted in these errors:

{% highlight bash %}

GStreamer-CRITICAL **: gst_segment_to_running_time: assertion `segment->format == format' failed

WARN  [42266] "overlay-video"                  feedcomponent     Jun 21 05:56:39      element /GstPipeline:pipeline-overlay-video/GstBin:bin0/GstAppSrc:source error Internal data flow error. gstbasesrc.c(2865): gst_base_src_loop (): /GstPipeline:pipeline-overlay-video/GstBin:bin0/GstAppSrc:source:
streaming task paused, reason not-negotiated (-4) (flumotion/component/feedcomponent010.py:260)
WARN  [42266]                                  twisted           Jun 21 05:56:39      A twisted traceback occurred. (twisted/internet/defer.py:648)

{% endhighlight %}

{% highlight python %}

Twisted traceback:
Traceback (most recent call last):
Failure: flumotion.common.errors.GStreamerGstError: (<__main__.GstAppSrc object at 0x2cd8550 (GstAppSrc at 0x2c60170)>, GError('Internal data flow error.',), 'gstbasesrc.c(2865): gst_base_src_loop (): /GstPipeline:pipeline-overlay-video/GstBin:bin0/GstAppSrc:source:\nstreaming task paused, reason not-negotiated (-4)')

{% endhighlight %}

This error seems to be due to change in GstBuffer and Buffers not being pushed to Pads properly. Another reason might be due to a problem with GstBin. I'll look further into this error tomorrow.
