---
layout: post
title: "Audiotest ported and a problem with blocking probes"
---

I went ahead and completed porting of Audiotest producer, volume effects and Vorbis encoder. With this, I successfully created and "listened" the test audio stream.

But, when I tried adding both Videotest and Audiotest components together, the ogg muxer component did not run successfully.

The main reason for this seems to be error while trying to link srcpad and sinkpad as evident from the following traceback. I suspect this might be due to problem in adding and removing of blocking probes as well.

{% highlight bash %}

  File "/home/aps/workspace/gsoc/flumotion-orig/cache/component/524cbc57eee2c130a83653aa7be9bcbc/flumotion/component/feedcomponent.py", line 153, in gotFeed
    self.comp.eatFromFD(eaterAlias, feedId, fd)
  File "/home/aps/workspace/gsoc/flumotion-orig/cache/component/524cbc57eee2c130a83653aa7be9bcbc/flumotion/component/feedcomponent010.py", line 931, in eatFromFD
    srcpad.link(sinkpad)
  File "/usr/lib/python2.7/dist-packages/gi/overrides/Gst.py", line 102, in link
    raise LinkError(ret)
gi.overrides.Gst.LinkError: <enum GST_PAD_LINK_NOFORMAT of type GstPadLinkReturn>

{% endhighlight %}

This error means linking failed because the caps of two pads weren't compatible.
