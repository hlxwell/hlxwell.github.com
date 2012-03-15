---
layout: post
title: "How to use ruby to detect iPad"
category: 
tags:
- Ruby
---
{% include JB/setup %}

{% highlight ruby %}

# Request from an iPhone or iPod touch? (Mobile Safari user agent)
def iphone_user_agent?
  request.env["HTTP_USER_AGENT"] && request.env["HTTP_USER_AGENT"][/(Mobile\/.+Safari)/]
end

{% endhighlight %}