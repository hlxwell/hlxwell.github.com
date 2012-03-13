---
layout: post
title: "Add ruby load path"
category: 
tags:
- ruby
---
{% include JB/setup %}

Only after you add load path, then you would be able to `require 'xxx.rb'`

{% highlight ruby %}
$: << File.expand_path(File.dirname(__FILE__))
{% endhighlight %}