---
layout: post
title: "Bug hunting continues"
---

I'm running a stream from dvswitch and this is the gstreamer pipeline I'm using:

{% highlight bash %}

gst-launch-1.0 -v dvswitchsrc name=src uri="dvswitch://192.168.1.11:2000" ! typefind ! tee name=t ! queue leaky=2 max-size-time=1000000000 ! dvdemux name=demux demux. ! queue ! dvdec name=decoder ! gdppay name=feeder:video-pay ! multifdsink sync=false name=feeder:video buffers-max=500 buffers-soft-max=450 recover-policy=1 demux. ! queue ! audio/x-raw ! volume name=setvolume ! level name=volumelevel message=true ! gdppay name=feeder:audio-pay ! multifdsink sync=false name=feeder:audio buffers-max=500 buffers-soft-max=450 recover-policy=1 t. ! queue ! gdppay name=feeder:dv-pay ! multifdsink sync=false name=feeder:dv buffers-max=500 buffers-soft-max=450 recover-policy=1

{% endhighlight %}

Here a [GST_DEBUG=4 DEBUG LOG] to get an overall picture of what is going on. There I see that "Could not link pads: demux:(null) - queue1:(null)".

To get more info about this, this is the part of the [GST_DEBUG=5 DEBUG LOG].

[GST_DEBUG=4 DEBUG LOG]: http://paste.ubuntu.com/7969281/
[GST_DEBUG=5 DEBUG LOG]: http://paste.ubuntu.com/7969398/
