---
layout: post
title: "Testing TimVideos Streaming System"
---

Timvideos make heavy use of Flumotion for streaming live videos. So, I went ahead to test the ported Flumotion with the streaming system to fix the issue.

I started out with the most important component, dvswitch-producer. For that, I needed a stream from dvswitch but it was crashing on Ubuntu 14.04 Trusty. So, as per Mithro's suggestion, I ran another Ubuntu 12.04 Precise VM simultaneously and created the stream there. Using this stream, I was able to watch the stream using this command

{% highlight bash %}

gst-launch-1.0 -v dvswitchsrc hostname=192.168.0.17 port=2000 ! dvdemux ! dvdec ! autovideosink

{% endhighlight %}


But when I tried to run Flumotion stream, it failed with the following error.


{% highlight bash %}

WARN  [ 4699] "producer-audio-video"           feedcomponent     Aug 01 00:10:39      element /GstPipeline:pipeline-producer-audio-video/GstGDPPay:feeder:dv-pay error The stream is in the wrong format. gstgdppay.c(620): gst_gdp_pay_chain (): /GstPipeline:pipeline-producer-audio-video/GstGDPPay:feeder:dv-pay:
first received buffer does not have caps set (flumotion/component/feedcomponent010.py:260)
WARN  [ 4699]                                  twisted           Aug 01 00:10:39      A twisted traceback occurred. (twisted/python/threadable.py:53)

Twisted traceback:
Traceback (most recent call last):
Failure: flumotion.common.errors.GStreamerGstError: (<__main__.GstGDPPay object at 0x7f4e6bc43eb0 (GstGDPPay at 0x18cc2e0)>, GError('The stream is in the wrong format.',), 'gstgdppay.c(620): gst_gdp_pay_chain (): /GstPipeline:pipeline-producer-audio-video/GstGDPPay:feeder:dv-pay:\nfirst received buffer does not have caps set')

INFO  [ 4699] "producer-audio-video"           component         Aug 01 00:10:39      Logged in to manager (flumotion/component/component.py:87)
WARN  [ 4699] "producer-audio-video"           feedcomponent     Aug 01 00:10:39      element /GstPipeline:pipeline-producer-audio-video/GstDvswitchSrc:src error Internal data flow error. gstbasesrc.c(2865): gst_base_src_loop (): /GstPipeline:pipeline-producer-audio-video/GstDvswitchSrc:src:
streaming task paused, reason not-negotiated (-4) (flumotion/component/feedcomponent010.py:260)

{% endhighlight %}