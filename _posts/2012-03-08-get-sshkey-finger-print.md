---
layout: post
title: "Get sshkey finger print"
category: 
tags:
- Linux
---
{% include JB/setup %}

{{% highlight shell %}}

$ ssh-keygen -lf /etc/ssh/ssh_host_rsa_key.pub

{{% endhighlight %}}
