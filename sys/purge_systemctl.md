---
title: Clean systemctl failed units
description: 
published: true
date: 2020-12-18T21:26:52.457Z
tags: systemctl, fail, units, remove, purge, clean
editor: markdown
dateCreated: 2020-12-18T21:26:52.457Z
---

# Header
It's some time annoying that old units stay in the list-units list.

let's use :

````
systemctl reset-failed
````

it will purge the list

## References

- https://unix.stackexchange.com/questions/418792/systemctl-remove-unit-from-failed-list