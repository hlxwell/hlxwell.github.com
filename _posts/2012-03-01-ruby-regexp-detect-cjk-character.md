---
layout: post
title: "Ruby regexp detect CJK character"
category: 
tags: []
---
{% include JB/setup %}

{{% highlight ruby linenos %}}
#encoding: UTF-8
class String
  def contains_cjk?
    !!(self =~ /\p{Han}|\p{Katakana}|\p{Hiragana}|\p{Hangul}/)
  end
end

strings= ['中国国際放送局', '광고 프로그램', '真是牛阿', 'This is english.']
strings.each{|s| puts s.contains_cjk?}
{{% endhighlight %}}

Result will be:

true
true
true
false