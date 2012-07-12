---
layout: post
title: "Capistrano with rvm installed on server"
category:
tags:
- Rails
---
{% include JB/setup %}

Add below code to "deploy.rb"

{% highlight ruby %}

require "bundler/capistrano"
$:.unshift(File.expand_path("./lib", ENV["rvm_path"]))
require "rvm/capistrano"
# specify the ruby version
set :rvm_ruby_string, "ruby-1.9.2-p180"
# rvm installed at 'system' or 'user' level
set :rvm_type, :user

{% endhighlight %}

You can look at [this article](http://blog.ninjahideout.com/posts/rvm-system-wide-installs-and-capistrano-integration)