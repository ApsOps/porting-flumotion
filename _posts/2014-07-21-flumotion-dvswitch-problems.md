---
layout: post
title: "Problems porting DVSwitch Flumotion component"
---

While porting flumotion dvswitch producer, I'm stuck with a problem. Here's the [DEBUG LOG].

Line 72 -- I'm not getting what is that referring to.

Also, in line 68 -- I'm not able to understand reason for this. Refer to this piece of code -- [feedcomponent010.py#L201-L208]

{% highlight python %}

# >> self.feeders.values()
[<Feeder dv (0 client(s))>, <Feeder audio (0 client(s))>, <Feeder video (0 client(s))>]

# When feeder is <Feeder dv (0 client(s))>
pipeline.get_by_name(feeder.elementName)   #  gives None

# I haven't changed the pipeline so I don't know why there is no feeder in pipeline

{% endhighlight %}

[DEBUG LOG]: http://pastebin.com/D8xr98Nt
[feedcomponent010.py#L201-L208]: https://github.com/aps-sids/flumotion-orig/blob/porting-to-gst1.0/flumotion/component/feedcomponent010.py#L201-L208
