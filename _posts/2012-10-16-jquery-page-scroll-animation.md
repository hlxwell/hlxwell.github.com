---
layout: post
title: "jquery page scroll animation"
category: 
tags:
- jquery
---
{% include JB/setup %}

```
$('html, body').animate({
  scrollTop: $(".top").offset().top
}, 2000);
```
