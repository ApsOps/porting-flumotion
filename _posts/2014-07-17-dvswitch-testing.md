---
layout: post
title: "DVSwitch Testing"
---

I ported the DVSwitch Gstreamer Element yesterday, but it had to be tested to know if it works or not. So, I worked on testing this today. I used following commands to test it:

{% highlight bash %}

#In terminal 1

dvswitch --host=localhost --port=2000

#In terminal 2

gst-launch-1.0 -v videotestsrc is-live=true ! videoconvert ! avenc_dvvideo ! avmux_dv ! dvswitchsink host=localhost port=2000

#Some more such gst pipelines in other terminals
{% endhighlight %}

These videos could be seen in dvswitch ui. Here is a screenshot.

<img src="http://i.imgur.com/qpI8tWX.png" alt="screenshot" style="width: 100%;" />

I also noticed that we need to port [dvsource-v4l2-other] as well. I'll probably be working on that now.

[dvsource-v4l2-other]: https://github.com/timvideos/dvsource-v4l2-other