---
layout: post
title: "New xcode uncomfortable things"
category:
tags:
- ios
- xcode
---
{% include JB/setup %}

Haven't been working on latest version of Xcode so far, today I tried to use it found many things are different.

1. You have to add Files to "Compile Sources" List in Build Phases.

2. You have to add "-fno-objc-arc" for files which no need support ARC.

3. You have to add the "xib" or "nib" to the "Compile Sources" also.

4. You should not drag .h files into "Compile Sources".

5. Font or some images you have to add them into "Copy Bundle Resources".
