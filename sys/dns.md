---
title: DNS configuration
description: Modification of the auto generated resolvconf configuration file
published: true
date: 2020-11-24T14:40:33.649Z
tags: dns, opendns, configuration, resolvconf
editor: markdown
dateCreated: 2020-11-24T14:39:06.205Z
---

# /etc/resolv.conf
the old ``/etc/resolv.conf`` containig parameters on how to do DNS resolutions is yet managed by other tools like ``systemd-resolved.service`` and/or resolvconf.

contains for exemple :
````
nameserver 208.67.222.222
nameserver 208.67.220.220
nameserver 8.8.8.8
````
in the managed state it's a link to the effective file version : ``/etc/resolvconf/run/resolv.conf ``
````
nheim@vps-982e47f4:~$ ls -altr /etc/resolv.conf
lrwxrwxrwx 1 root root 31 Sep 26 17:37 /etc/resolv.conf -> /etc/resolvconf/run/resolv.conf

````