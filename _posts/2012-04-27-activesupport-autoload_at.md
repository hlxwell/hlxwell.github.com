---
layout: post
title: "ActiveSupport autoload_at"
category: 
tags:
- Rails
---
{% include JB/setup %}


What does below code means?

{% highlight ruby %}
autoload_at "action_view/template/resolver" do
   autoload :Resolver
   autoload :PathResolver
   autoload :FileSystemResolver
   autoload :OptimizedFileSystemResolver
   autoload :FallbackFileSystemResolver
end
{% endhighlight %}

Pretty simple, it will load all Modules in that block in `action_view/template/resolver.rb` file.
