---
layout: post
title: "ActiveRecord's composed_of method"
category:
tags:
- Rails
---
{% include JB/setup %}

I'm rare to use AR's `composed_of` method, but always writing a method to override the default attributes to make conversion for database attributes.

Let's have look at this simple exmpale:

{% highlight ruby %}
class Website
  composed_of :domain,
    # Specify custom class name for association. default is Domain here.
    :class_name => 'WebsiteDomain',
    # mapping entity attr to value obj
    :mapping => [%w(domain_ip ip)],
    # will be called when init a value obj, all mapped attrs will be passed into the block
    :constructor => Proc.new { |sitename| WebsiteDomain.new(sitename) },
    # this will be called when a new value is assigned to the value object
    :converter => Proc.new { |domain_ip| domain_ip.is_a?(Integer) ? WebsiteDomain.new(domain_ip) : WebsiteDomain.new }
end
{% endhighlight %}