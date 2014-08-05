---
layout: post
title: "Hunting the bugs in DVSwitch plugin"
---

With help of thaytan, slomo and mithro, I was able to figure out that the problem mentioned in previous post was that dvswitchsrc doesn't know any caps, and gdppay needs it. thaytan suggested me to use typefind element that can automatically get the caps. Using this, I could run the pipeline without error using gst-launch but running with flumotion still gives following error:

{% highlight python %}

Twisted traceback:
Traceback (most recent call last):
Failure: flumotion.common.errors.GStreamerGstError: (<__main__.GstDvswitchSrc object at 0x7f10c8c5f410 (GstDvswitchSrc at 0x18a7be0)>, GError('Internal data flow error.',), 'gstbasesrc.c(2865): gst_base_src_loop (): /GstPipeline:pipeline-producer-audio-video/GstDvswitchSrc:src:\nstreaming task paused, reason not-negotiated (-4)')
 
DEBUG [19679] twisted Aug 04 16:52:36 [-] Traceback (most recent call last):
Failure: flumotion.common.errors.GStreamerGstError: (<__main__.GstDvswitchSrc object at 0x7f10c8c5f410 (GstDvswitchSrc at 0x18a7be0)>, GError('Internal data flow error.',), 'gstbasesrc.c(2865): gst_base_src_loop (): /GstPipeline:pipeline-producer-audio-video/GstDvswitchSrc:src:\nstreaming task paused, reason not-negotiated (-4)')

{% endhighlight %}

This shows that some link is not negotiated somewhere in the pipeline. To find the root of this problem, I got out this [DEBUG log]. Now this log gave some insights about what is going on and I find these questions to start with:

1. Line 81 -- linking src:(any) to typefindelement0:(any) (0/0) with caps "(NULL)"  -- Does this mean that caps must be set by dvswitchsrc plugin?

2. Line 119 -- no such pad 'video' in element "demux"  -- Is this causing the problem as pads can't be linked?

There are various such error, but the failure occus at Line 1373 - ` gstbasetransform.c:2115:gst_base_transform_handle_buffer:<videorate0> warning: not negotiated `

So, I'm now going to inspect all these problems and hopefully fix them.

[DEBUG log]: http://paste.ubuntu.com/7954475/
