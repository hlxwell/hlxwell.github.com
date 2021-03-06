--- 
layout: post
title: Installing SystemTap on Ubuntu
tags: 
- Linux
- Monitoring
status: publish
type: post
published: true
---
This article is from <a href="http://posulliv.github.com/2010/02/26/installing-stap.html">http://posulliv.github.com/2010/02/26/installing-stap.html</a>

I'm presenting at the MySQL user's conference this year and one of my <a href="http://en.oreilly.com/mysql2010/public/schedule/detail/12472">talks</a> is on using SystemTap and DTrace with MySQL and Drizzle. I'm also doing a tutorial with <a href="http://jpipes.com/">Jay Pipes</a> on developing replication plugins for Drizzle and that should be a lot of fun.
I wanted to write some posts before the conference that I can reference within my talk which detail how to install <a href="http://sourceware.org/systemtap/">SystemTap</a> and configure Drizzle and MySQL for use with SystemTap. Thus, this post is on how to install SystemTap on Ubuntu while my next post will go in to details about how to configure MySQL and Drizzle for use with SystemTap.
Before starting, its worth noting that this post is specific to Ubuntu 9.10. The procedure to follow may be different on other versions so its worth keeping that in my mind. The first thing we do is install systemtap and some associated packages which will be needed by Drizzle and MySQL:

{% highlight bash %}
$ sudo apt-get install systemtap
$ sudo apt-get install systemtap-sdt-dev
{% endhighlight %}

Now, being used to Ubuntu, you would think you are good to go now. Unfortunately, attempting to run SystemTap will probably give you the following error:

{% highlight bash %}
$ stap -e 'probe kernel.function("sys_open") {log("hello world") exit()}'
semantic error: libdwfl failure (missing x86_64 kernel/module debuginfo under
'/lib/modules/2.6.31-19-generic/build'): No such file or directory while resolving probe point
kernel.function("sys_open")
semantic error: no probes found
Pass 2: analysis failed.  Try again with another '--vp 01' option.
$
{% endhighlight %}

The above error occurs because SystemTap needs to have a debug version of the kernel available. Unfortunately, installing the debug information for a kernel on ubuntu is not a trivial operation to perform. In fact, there is a <a href="https://bugs.launchpad.net/ubuntu/+source/linux/+bug/289087">bug</a> on Launchpad about this issue. Thus, we will build a kernel debug package from source ourselves. This can be done as follows:


{% highlight bash %}
$ cd $HOME
$ sudo apt-get install dpkg-dev debhelper gawk
$ mkdir tmp
$ cd tmp
$ sudo apt-get build-dep --no-install-recommends linux-image-$(uname -r)
$ apt-get source linux-image-$(uname -r)
$ cd linux-2.6.31 (this is currently the kernel version of 9.10)
$ fakeroot debian/rules clean
$ AUTOBUILD=1 fakeroot debian/rules binary-generic skipdbg=false
$ sudo dpkg -i ../linux-image-debug-2.6.31-19-generic_2.6.31-19.56_amd64.ddeb
{% endhighlight %}

This builds a debug image of the kernel and so will take quite a while. Once we have the above completed, we can try running our hello world example with SystemTap again. In order to get some output, you should open or create some file on the system in another terminal window. In this example, I backgrounded the stap process and created a file:

{% highlight bash %}
$ sudo stap -e 'probe kernel.function("sys_open") {log("hello world") exit()}' &
[1] 951
$ touch /tmp/padraig
$ hello world
$ [1]+ Done
{% endhighlight %}

Installing SystemTap on CentOS is significantly easier since it is primarily developed by Red Hat. A good article on how to install it on CentOS is available <a href="http://sourceware.org/systemtap/wiki/SystemTapOnCentOS">here</a>.
In my next post on the topic, I'll explain how to configure MySQL and Drizzle for SystemTap and give some simple examples of using SystemTap with them.
