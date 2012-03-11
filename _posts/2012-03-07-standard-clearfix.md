---
layout: post
title: "Standard clearfix"
category: 
tags:
- css
---
{% include JB/setup %}

{% highlight css %}
.clearfix {
  zoom: 1;
}

.clearfix:after {
  content: '';
  clear: both;
  display: table;
}
{% endhighlight %}