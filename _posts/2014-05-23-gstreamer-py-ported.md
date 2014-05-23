---
layout: post
title: "gstreamer.py ported"
description: ""
category: 
tags: []
---

After a bit of struggle, the tests for gstreamer.py module pass. The two tests (out of six) that were [failing] last year were due to some changes in the gst.caps_from_string function. While gst returned a caps object that could be converted directly to string using python str() method, gi requires using to_string() method of caps object.

Another problem is that despite presence of gi in sys.modules, twisted is importing gtk2reactor which it shouldn't be doing. I haven't been able to figure out the reason for this so I had to comment the \_\_init\_\_ of tests module, for now.

Also, trying to create a test stream given following error:

{% highlight bash %}
Twisted traceback:
Traceback from remote host -- Traceback unavailable
flumotion.common.errors.RemoteRunError: RemoteRunError on method 'module flumotion.worker.checks.check could not be imported (exception ImportError at flumotion/common/package.py:54: import_module(): No module named 'gi')'
{% endhighlight %}

FIXME: fix problems with gtk2reactor and uncomment \_\_init\_\_.py

[failing]: http://portingflumotion.blogspot.in/2013/06/gstreamerpy-and-testcommongstreamerpy_20.html
