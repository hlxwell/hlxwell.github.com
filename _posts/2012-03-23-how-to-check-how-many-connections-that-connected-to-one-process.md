---
layout: post
title: "How to check how many connections that connected to one process"
category: 
tags:
- Ruby
---
{% include JB/setup %}

Since I am going to look how many connections conntected to one process, so I need such a command:

`lsof -a -p pid`

And how many open file descriptors are currently being used

`cat /proc/sys/fs/file-nr`