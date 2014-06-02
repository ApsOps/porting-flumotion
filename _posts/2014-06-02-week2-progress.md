---
layout: post
title: "Week 2 Progress"
---

I continued with the porting of base dependency modules not covered in previous week. To fix the failing tests, I ported boot.py first which led to tests for other modules passing again. After this, I ported pygobject.py and feeder.py followed by padmonitor.py where I faced some problems due to version 1.2.1 of Gstreamer. This is the latest available version in Ubuntu 12.04 precise. I fixed these by implementing some changes manually.

Eventually, I have started working on porting of Videotest Producer and creating a test stream. I am using following configuration for creating a stream only using the Videotest Producer. Getting Producer compnent's mood as "happy" will imply success.

{% highlight xml %}
<planet name="example-planet">

  <manager name="example-planet-manager">
    <component name="manager-bouncer" type="htpasswdcrypt-bouncer">
      <property name="data">user:PSfNpHTkpTx1M</property>
    </component>
  </manager>

  <atmosphere>
  </atmosphere>
  
  <flow name="default">
    <component name="producer-video"
               type="videotest-producer"
               label="producer-video"
               worker="localhost"
               project="flumotion"
               version="0.11.0.1">
      <property name="pattern">0</property>
      <property name="framerate">50/10</property>
      <property name="width">320</property>
      <property name="height">240</property>
      <clock-master>false</clock-master>
    </component>
  </flow>

</planet>
{% endhighlight %}

This shows component as "sad" (not running) and shows respective errors. This led to discovery of some problems in modules I have already ported. A weird problem I faced is that module GstNet is not being imported in feedcomponent010.py but it can be imported in the console.

I realized that we need to import and initialize this in boot.py first, like we do for Gst and GObject and doing that solves this problem. I also had to move function TIME_ARGS I wrote in padmonitor to `__init__.py` since it is used by other modules as well. In newer versions of Gstreamer, this function is available in library.

These steps fixed all the errors except the following one and the Videotest component is shown as "happy". I'll look into this error tomorrow.

{% highlight python %}
Traceback (most recent call last):
  File "/home/aps/workspace/gsoc/flumotion-orig/flumotion/common/gstreamer.py", line 53, in verbose_deep_notify_cb
    value = orig.get_property(pspec.name)
AttributeError: 'NoneType' object has no attribute 'name'
{% endhighlight %}


In Week 3, I will be porting Video Encoder and HTTP streamer so that I can "watch" the stream working.
