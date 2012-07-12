---
layout: post
title: "Problem with carrierwave when you have two servers"
category: 
tags: [Rails]
---
{% include JB/setup %}

Today I got a very strange problem when I using carrierwave, When I upload some pictures and the form validator told me some fields need to be filled, then I fill them and submit the form again, the uploaded file supposed to be cached, but it randomly told me some file supposed to be cached are missing.

After investigate a little bit I found I have 2 servers, and the cache file only stored on one of the server, so when request goes to another server which doesn't has cache file, it will report no file uploaded.

For solving this, I just mount one directly to another server, make the cache directly the same.

Steps:

1. On NFS server side: `sudo apt-get install nfs-server portmap nfs-common`

2. On NFS client side: `sudo apt-get install nfs-client nfs-common`

3. Add below line to `/etc/exports`
`/path_to_tmp_folder/tmp client_server_ip(rw,sync,no_subtree_check,no_root_squash)`

4. Restart service
`exportfs -ra`
`/etc/init.d/nfs-kernel-server restart`
`/etc/init.d/portmap restart`

5. Mount the directory on another server:
`sudo mount -o soft,intr,rsize=16384,wsize=16384 server_ip:/path_to_tmp_folder/tmp /local_path_to_empty_tmp_folder/tmp`

6. Add below line to /etc/fstab, this is for auto mount when server reboot:
`server_ip:/path_to_tmp/tmp /local_empty_folder/tmp nfs rsize=16384,wsize=16384,rw,auto,nolock`
