---
layout: post
title: "Default logger level for environments"
category: 
tags:
- Rails
---
{% include JB/setup %}

Logger level has:

`logger.(debug|info|warn|error|fatal)`

The default Rails log level is `info` in production mode and `debug` in development and test mode.

Since the log out put also consumed the system IO resource so please take care.