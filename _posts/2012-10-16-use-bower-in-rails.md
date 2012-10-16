---
layout: post
title: "Use bower in rails"
category:
tags:
- rails
- jquery
---
{% include JB/setup %}

Bower is a very good tool, it can help you to manage the javascript or css like the way of bundler.


This is what does the config file looks like:

```
  {
    "dependencies": {
      "jquery": "http://code.jquery.com/jquery-1.8.1.js"
    }
  }
```

This is the command lines to use the bower.

```
  $ npm install -g bower
  $ mkdir -p vendor/assets
  $ cd vendor/assets/
  $ curl https://raw.github.com/gist/3667224/component.json > component.json
  $ bower install
```
