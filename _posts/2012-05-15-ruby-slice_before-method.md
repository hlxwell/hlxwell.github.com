---
layout: post
title: "ruby slice_before method"
category:
tags: []
---
{% include JB/setup %}

Today I got a requirement to separate a array into slices when encounter several specific marks.

After search ruby api I found `slice_before` method.

```
[1,2,3,'a',4,5,6,'a',7,8,9,'a',1,3,5].slice_before {|i| i == 'a'}.map{|n| n}
=>
[[1, 2, 3], ["a", 4, 5, 6], ["a", 7, 8, 9], ["a", 1, 3, 5]]
```

Pretty cool ;)

