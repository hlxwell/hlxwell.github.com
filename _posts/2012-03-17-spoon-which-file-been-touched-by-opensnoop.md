---
layout: post
title: "Spoon which file been touched by opensnoop"
category: 
tags:
- Macosx
---
{% include JB/setup %}

opensnoop tracks file opens. As a process issues a file open, details such as UID, PID and pathname are printed out.

The  returned  file descriptor is printed, a value of -1 indicates an error. This can be useful for troubleshooting to determine
if appliacions are attempting to open files that do not exist.

Since this uses DTrace, only users with root privileges can run this command.
