---
layout: post
title: "pygobject.py and feeder.py ported"
description: ""
category: 
tags: []
---

Ported flumotion/common/pygobject.py
Tests pass:

{% highlight bash %}
flumotion.test.test_common_pygobject
  SetProperty
    testButton ...                                                         [OK]
  TestPyGObject
    testPyGObject ...                                                      [OK]

-------------------------------------------------------------------------------
Ran 2 tests in 0.040s

PASSED (successes=2)
{% endhighlight %}

Ported flumotion/component/feeder.py
Tests pass:

{% highlight bash %}
flumotion.test.test_component_feeder
  TestFeeder
    testReconnect ...                                                      [OK]
    test_clientConnected ...                                               [OK]

-------------------------------------------------------------------------------
Ran 2 tests in 0.003s

PASSED (successes=2)
{% endhighlight %}

Tomorrow, I plan to port padmonitor, feedcomponent and other remaining base modules.
