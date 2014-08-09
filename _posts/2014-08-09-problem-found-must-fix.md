---
layout: post
title: "PROBLEM FOUND. MUST FIX."
---

I've become a sleep deprived bug hunter now, feel like a robo though :P

Anyway, I finally figured out that problem is a caps negotiation problem in one of the effects in the EffectBin (Deinterlace + Videorate + Videoscale + Audioconvert) applied over DVSwitch flumotion component. By removing this Effect Bin, I was able to successfully stream the video.

Let's see if we really need to fix this or we can live without these effects.
