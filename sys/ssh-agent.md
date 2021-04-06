---
title: ssh agent
description: tricks and command for ssh and the agent
published: true
date: 2021-04-06T09:29:42.398Z
tags: ssh, agent, key
editor: markdown
dateCreated: 2021-04-06T09:22:44.276Z
---

# Ssh agent memo

## list ssh agent forwarded keys

````shell
nheim@vps-982e47f4:~/src/containers/xperience$ ssh-add -l
2048 SHA256:E3Qat0BqwjkJRYR3PfMKy39/LWXdUjK5re4vR0BBhVo nheim@vps-982e47f4 (RSA)
2048 SHA256:fS50l0od1tWMBK1YoKUX2CtPNeScGng1bVySqM2hxfk C:\Users\heimn\.ssh\id_rsa_coopalim (RSA)
2048 SHA256:i4Htn7qrDJ68s6zv1TGqhwgLjz5Sv82vhLKisvO2gFY C:\Users\heimn\.ssh\id_rsa (RSA)
````

## vscode remote config file 

the default file used is in ``%HOMEPATH%/.ssh/config``

````
Host "vps03 (10.0.0.1 via Openvpn)"
  HostName 10.0.0.1
  User nheim
  ForwardAgent true
````