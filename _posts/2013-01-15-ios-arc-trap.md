---
layout: post
title: "iOS ARC trap"
category: 
tags:
- iOS
---
{% include JB/setup %}

ARC will release object after block, so if something like AVAudioPlayer, you have to make a class variable to keep it, or else this player object will be release.