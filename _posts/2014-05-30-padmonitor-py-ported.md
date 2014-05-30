---
layout: post
title: "padmonitor.py ported"
description: ""
category: 
tags: []
---

I did the required changes and hence, flumotion/component/padmonitor.py is ported and tests pass:

{% highlight bash %}
flumotion.test.test_component_padmonitor
  TestPadMonitor
    testPadMonitorActivation ...                                           [OK]
    testPadMonitorTimeout ...                                              [OK]

-------------------------------------------------------------------------------
Ran 2 tests in 0.663s

PASSED (successes=2)
{% endhighlight %}

I faced some problems and following is what I did to fix them:

### 1

While changing [this line] code, as per [Gstreamer docs], if maximum time to poll is negative(-1), this function will block indefinitely. But, keeping the value -1 gives the error:

{% highlight bash %}
===============================================================================
[ERROR]
Traceback (most recent call last):
  File "/home/aps/workspace/gsoc/flumotion-orig/flumotion/test/test_component_padmonitor.py", line 51, in testPadMonitorActivation
    self._run_pipeline(pipeline)
  File "/home/aps/workspace/gsoc/flumotion-orig/flumotion/test/test_component_padmonitor.py", line 37, in _run_pipeline
    pipeline.get_bus().poll(Gst.MessageType.EOS, Gst.CLOCK_TIME_NONE)
  File "/usr/lib/python2.7/dist-packages/gi/types.py", line 43, in function
    return info.invoke(*args, **kwargs)
exceptions.ValueError: -1 not in range 0 to 18446744073709551615
{% endhighlight %}

So, reading some other documentation suggests me to use Gst.CLOCK_TIME_NONE in place of -1. Now, another problem. Value of Gst.CLOCK_TIME_NONE should be and is 18446744073709551615L on Gstreamer 1.2.4 on Ubuntu 14.04. But, on my system (Ubuntu 12.04, Gstreamer 1.2.1) I get value as -1. I'm not able to install any Gstreamer version newer than 1.2.1 either (I don't think its available on Ubuntu 12.04 precise). Hence, to fix this, I'm manually putting in the correct value as an argument.

### 2

Again, due to this Gstreamer version problem, a function Gst.TIME_ARGS is not available. So, I'm writing that myself here:

{% highlight python %}
if not hasattr(Gst, 'TIME_ARGS'):
    def TIME_ARGS(time):
        if time == Gst.CLOCK_TIME_NONE:
            return 'CLOCK_TIME_NONE'

        return '%u:%02u:%02u.%09u' % (time / (Gst.SECOND * 60 * 60),
                                      (time / (Gst.SECOND * 60)) % 60,
                                      (time / (Gst.SECOND) % 60),
                                      time % Gst.SECOND)

    Gst.TIME_ARGS = TIME_ARGS
{% endhighlight %}

[this line]: https://github.com/aps-sids/flumotion-orig/commit/be7714ab8a0ce4be743d670a969ab4b1f0f5ca06#diff-47651c297ba46f72039cff6584808cf6L35
[Gstreamer docs]: http://gstreamer.freedesktop.org/data/doc/gstreamer/head/gstreamer/html/GstBus.html#gst-bus-poll
