---
layout: post
title: "Simple Javascript Inheritance"
category: 
tags:
- Javascript
---
{% include JB/setup %}

You can understand what is below coding doing.

{% highlight javascript %}

var Person = Class.extend({
  init: function(isDancing){
    this.dancing = isDancing;
  },
  dance: function(){
    return this.dancing;
  }
});
var Ninja = Person.extend({
  init: function(){
    this._super( false );
  },
  dance: function(){
    // Call the inherited version of dance()
    return this._super();
  },
  swingSword: function(){
    return true;
  }
});

var p = new Person(true);
p.dance(); // => true

var n = new Ninja();
n.dance(); // => false
n.swingSword(); // => true

// Should all be true
p instanceof Person && p instanceof Class &&
n instanceof Ninja && n instanceof Person && n instanceof Class

{% endhighlight %}

I found this because I read it from the souce code of a opensource online game (BrowserQuest), which is based on node.js and html5 websocket.

[Original article](http://ejohn.org/blog/simple-javascript-inheritance/)



