---
layout: post
title: "Get sshkey finger print"
category: 
tags:
- Linux
---
{% include JB/setup %}

Since recently github got a security issue, we need to update the sshkey, 
then require you to check the finger print, below is the code to get finger print.

{% highlight bash %}

$ ssh-keygen -lf /etc/ssh/ssh_host_rsa_key.pub

{% endhighlight %}
