---
layout: post
title: "Check how many client connected to your internet sharing on your mac"
category: 
tags:
- Linux
---
{% include JB/setup %}

`arp -i en1 -a`

```
? (192.168.2.7) at c0:9f:42:8f:88:a2 on bridge0 ifscope [bridge]
? (192.168.2.9) at b0:65:bd:6e:e2:55 on bridge0 ifscope [bridge]
? (192.168.2.255) at ff:ff:ff:ff:ff:ff on bridge0 ifscope [bridge]
```
