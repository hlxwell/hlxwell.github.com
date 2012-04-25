---
layout: post
title: "RVM install REE got error on Lion"
category: 
tags: []
---
{% include JB/setup %}

Today I install json gem, got a an error, then googled a little bit found I need to reinstall my ruby in RVM,
then I updated rvm and reinstalled ruby 1.9.3, but got problem when install REE, got following errors:

{% highlight bash %}
* Non-broken C compiler... not found 
* Non-broken C++ compiler... not found 
* The 'make' tool... found at /usr/bin/make 
* The 'patch' tool... found at /usr/bin/patch 
* Zlib development headers... found 
* OpenSSL development headers... found 
* GNU Readline development headers... found
{% endhighlight %}

After I installed the 
[osx-gcc-installer](https://github.com/kennethreitz/osx-gcc-installer)

Then things solved.

Since Lion is using LLVM-gcc instead of gcc, so it can't compile REE.
