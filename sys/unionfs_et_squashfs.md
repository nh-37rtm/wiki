---
title: Unionfs et Squashfs
description: 
published: true
date: 2020-12-18T21:17:40.246Z
tags: unionfs, squashfs
editor: markdown
dateCreated: 2020-12-18T21:17:40.246Z
---

# Overlay
The overlay filesystem allow you to merge multiple dirs content one over the other. this allow you to make some sort of hierarchy in filesystems.

exemple used with the snap tool : 

````
mount -t overlay -o lowerdir=/snap/code-insiders/535_lower,upperdir=/home/dev/lib/,workdir=/tmp overlay /snap/code-insiders/535
````