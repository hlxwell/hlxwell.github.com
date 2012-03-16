---
layout: post
title: "Parslet a very cool Parsing Expression Grammar parser"
category:
tags:
- Ruby
---
{% include JB/setup %}

# -*- encoding : utf-8 -*-
require 'rubygems'
require 'parslet'
include Parslet

Recently I made a japanese language learning tool, which is very cool :) . In this tool we need to create
a mark language parser to parse this like `[kanji|furigana]`, My colleague zete, use his very professional regexp
skill to make a regexp to parse this text.

{% highlight ruby %}
WORD_PARSER = /
  (?<kanji>        [\p{Han}\p{Hiragana}\p{Katakana}]+          ){0}
  (?<furi>         \p{Hiragana}+                               ){0}
  (?<oword>        [^\]]+                                      ){0}
  (?<invalid>      .                                           ){0}
  (?<word>         \[ \g<sp> \g<word_content> \g<sp> \]        ){0}

  (?<word_content> \g<kanji> \g<sp> \g<right> | \g<oword>      ){0}
  (?<right>        \| \g<sp> \g<furi>                          ){0}
  (?<sp>           [\t\ ]*                                     ){0}

  \g<word> | \g<invalid>
/ux
{% endhighlight %}

Look at above stunning regular expression. I never toughed this level of complexity of regexp.
But later on when I was looking at http header parser, then found a good tool, called `parslet`.
It just could help me doing exact thing, and even could more complicated things like a new language.

{% highlight ruby %}
furidown = "[中国|ちゅうごく][雲南|うんなん][省|しょう][の][昆|こん][明|あきら][市|し][在住|ざいじゅう][の][27][歳|さい][の][アメリカ][人|じん][。]"

# Constructs a parser using a Parser Expression Grammar
class Furidown < Parslet::Parser
  rule(:space)      { match('\s').repeat(1) }
  rule(:space?)     { space.maybe }

  rule(:lbracket)   { str('[') >> space? }
  rule(:rbracket)   { str(']') >> space? }
  rule(:split)      { str("|") >> space? }

  rule(:kanji) { match('[^\]\|]').repeat.as(:kanji) }
  rule(:furigana) { split >> match('[^\]\[]').repeat.as(:furigana) }

  rule(:word) { lbracket >> kanji >> furigana.maybe >> rbracket }
  rule(:words) { word.repeat }

  root(:words)
end

parser = Furidown.new
p parser.parse(furidown)

# the result like
=> [{:kanji=>"中国"@1, :furigana=>"ちゅうごく"@8}, {:kanji=>"雲南"@25, :furigana=>"うんなん"@32}, {:kanji=>"省"@46, :furigana=>"しょう"@50}, {:kanji=>"の"@61}, {:kanji=>"昆"@66, :furigana=>"こん"@70}, {:kanji=>"明"@78, :furigana=>"あきら"@82}, {:kanji=>"市"@93, :furigana=>"し"@97}, {:kanji=>"在住"@102, :furigana=>"ざいじゅう"@109}, {:kanji=>"の"@126}, {:kanji=>"27"@131}, {:kanji=>"歳"@135, :furigana=>"さい"@139}, {:kanji=>"の"@147}, {:kanji=>"アメリカ"@152}, {:kanji=>"人"@166, :furigana=>"じん"@170}, {:kanji=>"。"@178}]
{% endhighlight %}

Fantastic!!!

Reference:
[DSL doc](http://rubydoc.info/github/kschiess/parslet/master/Parslet/Atoms/DSL)
[Examples](https://github.com/kschiess/parslet/tree/master/example/)
[Get started](http://kschiess.github.com/parslet/get-started.html)
[Parslet intro - very good intro to parse erb](http://florianhanke.com/blog/2011/02/01/parslet-intro.html)

