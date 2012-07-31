---
layout: post
title: "Capistrano with bundler"
category:
tags:
- Bundler
- Capistrano
- Deployment
---
{% include JB/setup %}

Today I suddenly got an error on website, it said there is one gem doesn't been installed somehow. but when I ssh to server, use `bundle install`, found both server was installed all gems that application needs.

Finally I got the reason, the passenger doesn't loading the gems correctly from bundler, so you have to run bundle install like this way `bundle install --deployment`. This installation will move all gems to "vendor/bundle", which will freeze all version of gems into the project.

For capistrano, add below lines into deploy.rb file:

```
  set :bundle_roles, [:app]
  require 'bundler/capistrano'
```

