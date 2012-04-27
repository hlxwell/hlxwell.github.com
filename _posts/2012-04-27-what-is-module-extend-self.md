---
layout: post
title: "what is module extend self?"
category: 
tags:
- Ruby
---
{% include JB/setup %}

Today when I reading about rails source code found

{% highlight ruby %}
module Dependencies
  extend self
end
{% endhighlight %}

Yes, I never saw this usage before, this actually is a efficient way to change all instance methods into class methods.

Reference: (http://ozmm.org/posts/singin_singletons.html)[http://ozmm.org/posts/singin_singletons.html]
