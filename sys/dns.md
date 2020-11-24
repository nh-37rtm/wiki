---
title: DNS configuration
description: Modification of the auto generated resolvconf configuration file
published: true
date: 2020-11-24T14:39:06.205Z
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
