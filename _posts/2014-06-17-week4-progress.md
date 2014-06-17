---
layout: post
title: "Week 4 Progress"
---

I started with some missed changes and continued with porting of Theora encoder, Ogg muxer and httpstreamer consumer. With these components, I was able to "watch" a test video stream.

After this, I continued with porting volume effects, audiotest producer and Vorbis encoder. This led to a successful test audio stream which I could "hear".

When I tried to combine audiotest and videotest stream components, I was getting errors in linking srcpad and sinkpad due to incompatible caps of the pad. As I had suspected, it was due to improper blocking and unblocking of pads. Gst 0.10 used `set_blocked_async` function for blocking and unblocking pads while Gst 1.0 uses a probe of type 'BLOCK'. Blocking was working fine but unblocking caused problems since it needed the particular probe id to remove it. Also, for some reason, callbacks for adding BLOCK probe were being called repeatedly.

Hence, I did these [changes] to fix this issue and everything worked perfectly (except a few gstreamer warnings). You can see it for yourself using these [instructions] and this [configuration].

I'm really happy to see that I'm on schedule with my project timeline :) I'll be fixing any bugs, writing documentation and then continue with porting of other components in week 5.

[changes]: https://github.com/aps-sids/flumotion-orig/commit/6f1e924ff9412d4c01f9c454f4d271572f12e4e6
[instructions]: http://aps-sids.github.io/porting-flumotion/2014/06/06/run-a-test-stream/
[configuration]: https://github.com/aps-sids/flumotion-orig/blob/8223a46cacf0beb8889dcfe704343ed20ca5be7f/test_config.xml
