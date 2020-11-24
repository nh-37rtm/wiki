---
title: snapcraft and easy-openvpn
description: Building customized snap package of the easy-openvpn package
published: true
date: 2020-11-24T16:10:29.205Z
tags: snap snapcraft openvpn easy-openvpn
editor: markdown
dateCreated: 2020-11-24T15:22:24.265Z
---

# Snap
You can tell .. snap is yet another packaging tool. but i think it add some interesting feature like isolating execution, decomposition with groups of low level access features called ``interfaces`` for exemple :
- account-control
- audio-record
- docker

you can compare this to the android applications fonctionnalities wich i think aim the security issues. it's also an ease of use for the application developper/packager, and it forces the packager to be aware of the software features ... the packager box is smaller and reduce the zone of a potential side effect.

Snap is compatible with some others linux distribs


## references 
- https://snapcraft.io/about
- https://www.reddit.com/r/Ubuntu/comments/a364ii/proscons_of_snap_vs_apt/
- https://medium.com/@Aenon/are-you-serious-about-this-opinion-cc170a236e1f

# Snapcraft
Snapcraft is a snap application (i like the concept of the application packaged by itself ^^) to build snap package described by a yaml file.
To have more information on how to build a snapcraft package let's have a look at https://snapcraft.io/docs/creating-snapcraft-yaml

An application can have multiples channels, it's considered as a group of branches witch can contains for exemple the stable channel, the candidate channel etc ...

During packaging and to help you with confinement/interfaces customisation and see in real time the features that are required are required you can use the snappy-debug tool (which is a snap too) ans will let you know whitch calls are blocked by the confinement tool.

references :

- https://www.youtube.com/watch?v=BEp_l2oUcD8
- https://en.wikipedia.org/wiki/Snap_(package_manager)