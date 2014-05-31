---
layout: post
title: "feedcomponent ported"
---

Changed flumotion/component/feedcomponent010.py and flumotion/component/feedcomponent.py 

As a result, feedcomponent is ported.

{% highlight bash %}
flumotion.test.test_component_feedcomponent
  TestFeedComponentMedium
    test1277 ...                                                           [OK]
    testRemoteEatFrom ...                                                  [OK]
  TestMuxer
    testPipelineString ...                                                 [OK]

-------------------------------------------------------------------------------
Ran 3 tests in 0.042s

PASSED (successes=3)
{% endhighlight %}

This completes the porting of base dependency modules for Videotest producer. Next, I will try to create a simple stream and consequently port Videotest producer.
