---
layout: post
title: "Week 10 Progress"
---

This week, I was eagerly waiting for some good results so I can post on this blog. I was initially working on porting of DVSwitch flumotion component. The code changes were done but stream was still giving errors that caps aren't set or stream format is not compatible.

I wasn't able to fix this after various efforts. Then I realized that this might be due to the fact that decoder was not ported and that missing component might be creating problems. So, I diverted towards porting generic decoder.

Now this decoder code uses a custom plugin 'synckeeper'. For porting, when I used `Gst.Pad.new_from_template()` as seen in this [diff], it led to a crash. Some research about this issue hinted that this might be a problem due to older python-gi an gobject bindings since I have been working on Ubuntu 12.04 Precise.

This whole idea of working on precise was just a temporary measure and we (me and mithro) realized that this was about time to shift to latest Ubuntu 14.04 Trusty since most of the components are ported.

But there was still one more issue, incompatibility with latest Twisted Python. There was some twisted features used in flumotion core that were deprecated and subsequently removed in newer Twisted versions. Mithro did some work regarding that. He found out a patch by someone that was supposed to fix this issue. With that, along with some other changes, mithro created a modern-twisted branch.

I merged that with my code and was able to run a test audio + video stream successfully on Trusty. There were the following errors though:

{% highlight bash %}

DEBUG [40686] "/default/http-audio-video"      jobmedium         Jul 28 11:33:56      creating ComponentClientFactory (flumotion/job/job.py:285)
DEBUG [40686] "/default/http-audio-video"      jobmedium         Jul 28 11:33:56 : int() argument must be a string or a number, not 'NoneType'
TypeError     created ComponentClientFactory <flumotion.component.component.ComponentClientFactory instance at 0x7f6848ac2b00> (flumotion/job/job.py:288)
DEBUG [40686] "/default/http-audio-video"      jobmedium         Jul 28 11:33:56 : int() argument must be a string or a number, not 'NoneType'
TypeError: int() argument must be a string or a number, not 'NoneType'
TypeError     logging in with authenticator <flumotion.twisted.pb.RemoteAuthenticator instance at 0x7f6848c069e0> (flumotion/job/job.py:295)
INFO  [40686] "/default/http-audio-video"      jobmedium         Jul 28 11:33:56 : int() argument must be a string or a number, not 'NoneType'
     Connecting to manager localhost:8642 with TCP (flumotion/job/job.py:304)
LOG   [40686]                                  twisted           Jul 28 11:33:56 TypeError: int() argument must be a string or a number, not 'NoneType'
TypeError: int() argument must be a string or a number, not 'NoneType'
TypeError      [JobClientBroker,client] Starting factory <flumotion.component.component.ComponentClientFactory instance at 0x7f6848ac2b00>
 (twisted/python/threadable.py:53)
DEBUG [40686] "/default/http-audio-video"      jobmedium         Jul 28 11:33:56 : int() argument must be a string or a number, not 'NoneType'
TypeError: int() argument must be a string or a number, not 'NoneType'
TypeError: int() argument must be a string or a number, not 'NoneType'

{% endhighlight %}

So, from now on, I'm going to tie the loose ends and fix the issues with this and other unported components. With Trusty and latest libraries, hopefully I will be able to fix remaining problems.

[diff]: https://github.com/aps-sids/flumotion-orig/commit/cf3cfbf09f6e8234d95836b30181ad4ed9e5eddc#diff-9d30e92cb49af87d67d5cb9dea9b6783R71
