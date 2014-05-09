---
layout: post
title: "Import errors"
description: ""
category: 
tags: []
---

While porting the base modules and running the respective tests, I have encountered the same error which was there for previous GSoC student. Basically, its the ImportError conflict since introspected and static glib/gtk bindings must not be mixed as evident by the following error:

{% highlight python %}
flumotion
  test
    test_common_gstreamer ...                                           [ERROR]

===============================================================================
[ERROR]
Traceback (most recent call last):
  File "/usr/lib/python2.7/dist-packages/twisted/trial/runner.py", line 660, in loadByNames
    things.append(self.findByName(name))
  File "/usr/lib/python2.7/dist-packages/twisted/trial/runner.py", line 470, in findByName
    return reflect.namedAny(name)
  File "/usr/lib/python2.7/dist-packages/twisted/python/reflect.py", line 464, in namedAny
    topLevelPackage = _importAndCheckStack(trialname)
  File "/home/aps/workspace/gsoc/flumotion-orig/flumotion/test/test_common_gstreamer.py", line 21, in <module>
    from flumotion.common import gstreamer
  File "/home/aps/workspace/gsoc/flumotion-orig/flumotion/common/gstreamer.py", line 25, in <module>
    import gi
  File "/usr/lib/python2.7/dist-packages/gi/__init__.py", line 23, in <module>
    from ._gi import _API, Repository
exceptions.ImportError: could not import gobject (error was: ImportError('When using gi.repository you must not import static modules like "gobject". Please change all occurrences of "import gobject" to "from gi.repository import GObject".',))

flumotion.test.test_common_gstreamer
-------------------------------------------------------------------------------
Ran 1 tests in 0.003s

FAILED (errors=1)
{% endhighlight %}

Now, I suspect there could be two reasons for this:

1. We need to port all the modules before testing
2. Twisted 12 is not compatible with gi

I am looking into this issue right now. Previous student's blog posts suggest some ideas but those seem unclear/wrong.