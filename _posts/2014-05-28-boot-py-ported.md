---
layout: post
title: "boot.py ported"
description: ""
category: 
tags: []
---

I figured out that I need to port flumotion/common/boot.py first to get the tests working again and porting other modules without tests would be a really bad idea. Also, I needed to port PyGTK to PyGI + Gtk3 at the same time. We cannot use PyGI and any of the static python-gobject based bindings together in the same process. As a result, boot.py is ported and gstreamer.py (already ported) tests pass again!

{% highlight bash %}
flumotion.test.test_common_gstreamer
  Caps
    testCaps ...                                                           [OK]
    testCapsStreamheader ...                                               [OK]
  DeepNotify
    testDeepNotify ...                                                     [OK]
  Factory
    testFakeSrc ...                                                        [OK]
  TestProperty
    testHasProperty ...                                                    [OK]
    testHasPropertyValue ...                                               [OK]

-------------------------------------------------------------------------------
Ran 6 tests in 0.094s

PASSED (successes=6)
{% endhighlight %}
