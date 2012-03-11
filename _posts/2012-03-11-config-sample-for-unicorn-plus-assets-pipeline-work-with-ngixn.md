---
layout: post
title: "Config sample for Unicorn plus assets pipeline work with ngixn"
category: 
tags: 
- Rails
---
{% include JB/setup %}


{% highlight nginx %}

upstream app {
  server unix:/srv/app/current/tmp/sockets/unicorn.sock fail_timeout=0;
}
server {
        listen   80;
        server_name  www.app.com;
        rewrite ^/(.*) http://app.com/$1 permanent;
}

server {
  listen 80;
  client_max_body_size 2G;
  server_name app.com;
  keepalive_timeout 5;
  root /srv/app/current/public;
  access_log  off;
  error_log off;

  if ($request_method !~ ^(GET|HEAD|PUT|POST|DELETE|OPTIONS)$ ){
    return 405;
  }

  location ~ ^/(assets)/  {  
    gzip_static on;
    expires     max;
    add_header  Cache-Control public;
  } 

  location / {
    try_files $uri/index.html $uri.html $uri @app;
    error_page 404              /404.html;
    error_page 422              /422.html;
    error_page 500 502 503 504  /500.html;
    error_page 403              /403.html;
  }

  location @app {
    proxy_pass http://app;
  }

  location = /favicon.ico {
    expires    max;
    add_header Cache-Control public;
  }

  location ~ \.php$ {
    deny  all;
  }
}

{% endhighlight %}