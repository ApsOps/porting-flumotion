---
layout: post
title: "Videotest component ported"
---

An important requirement, gst-python1.0 is not available for Ubuntu 12.04 precise in the Gstreamer developers PPA so I compiled it from source. This provided overrides that were missing in my system and this solved various problems including Gst.Fraction (previous blog post) and Gst.TIME_ARGS (that I had implemented myself).

I did some missed changes, ported the Videotest component completely and ported `flumotion/worker/checks/check.py` as well. There is just a minor problem in `gstreamer.py`. After solving this, I will post about how to create and test a stream using just the Videotest producer.

{% highlight python %}
Traceback (most recent call last):
  File "/home/aps/workspace/gsoc/flumotion-orig/flumotion/common/gstreamer.py", line 55, in verbose_deep_notify_cb
    value = orig.get_property(pspec.name)
AttributeError: 'NoneType' object has no attribute 'name'
{% endhighlight %}

This error is not creating problems with stream though and mood of component is still "happy". One fix could be adding following code in [this] function.

{% highlight python %}
if pspec == None:
    return
{% endhighlight %}

[this]: https://github.com/aps-sids/flumotion-orig/blob/porting-to-gst1.0/flumotion/common/gstreamer.py#L49
