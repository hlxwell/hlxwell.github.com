---
layout: post
title: "Ruby namespace tips"
category: 
tags:
- Ruby 
---
{% include JB/setup %}

After made below test, then you don't need to use `Test::B.bbb` in everywhere of your plugin, just use `B.bbb`.

{% highlight ruby %}
class A
  def self.aaa
    puts "a"
  end
end

module Test
  class A
    def self.aaa
      puts "aaaaaaaaaa"
    end
  end
end

module Test
  class B
    def self.bbb
      A.aaa
    end
  end
end


Test::B.bbb # => aaaaaaaaaa
A.aaa # => a
{% endhighlight %}
