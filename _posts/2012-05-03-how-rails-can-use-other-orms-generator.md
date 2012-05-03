---
layout: post
title: "How rails can use other orm's generator"
category: 
tags:
- Rails
---
{% include JB/setup %}

I'm just suddenly curious about this, so I looked up a little about Rails source code.

I found this code is how it get the other ORM class.

{% highlight ruby %}
"#{options[:orm].to_s.camelize}::Generators::ActiveModel".constantize
{% endhighlight %}

Then I checked mongoid, found it has the class: `Mongoid::Generators::ActiveModel` in `lib/rails/mongoid_generator.rb`.
