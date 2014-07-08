---
layout: post
title: "FGDP Ported"
---

I have been working on porting FGDP producer and consumer for a while now. It's ported completely and the test pass, but I need to test it with the streams. Basically the FGDP sink and src elements register functions do not register the plugins automatically and we need to explicitly register them. There were a few other regular API changes as well.