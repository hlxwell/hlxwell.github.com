---
layout: post
title: "Get an error from eventmachine"
category:
tags:
- Ruby
---
{% include JB/setup %}

Today I am doing a test to see how many concurrent connections that a eventmachine can support, but got a error like this.

`ruby: ed.cpp:938: void ConnectionDescriptor::_WriteOutboundData(): Assertion `nbytes > 0' failed.`

After investigation I found the solution:

* Only call EM.epoll before calling EM.run
* Only call EM.set_descriptor_table_size before calling EM.run

