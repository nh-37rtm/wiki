---
title: Wsl
description: memory sheet for windows wsl
published: true
date: 2020-11-30T10:29:17.928Z
tags: 
editor: undefined
dateCreated: 2020-11-30T09:53:45.689Z
---

# WSL
Windows Subsystem for Linux is in my opinion a response and complement to the docker desktop, the last version (WSL 2) provide some optimisations over the WSL 1.

## WSL2 prerequirement
> WSL 2 requires Windows 10 version 1903 or higher, with Build 18362 or higher, for x64 systems, and Version 2004 or higher, with Build 19041 or higher, for ARM64 systems.[40]

## WSL1 vs WSL2
WSL2 is clearly an optimisation provided by microsoft of WSL1.
Microsoft says :
> The primary difference and reasons for updating the Windows Subsystem for Linux from WSL 1 to WSL 2 are to:
> 
> - increase file system performance,
> - support full system call compatibility.
> WSL 2 uses the latest and greatest in virtualization technology to run a Linux kernel inside of a lightweight utility virtual machine (VM). However, WSL 2 is not a traditional VM experience.

## installing WSL2
it require some manual steps as it's a edge microsoft feature
- https://docs.microsoft.com/en-us/windows/wsl/install-win10#set-a-distro-to-be-backed-by-wsl-2-using-the-command-line
## upgrading existing WSL1 containerd to WSL2
first, of course you need to install WSL2
````
Microsoft Windows [version 10.0.19041.630]
(c) 2020 Microsoft Corporation. Tous droits réservés.

C:\Users\heimn>
C:\Users\heimn>wsl -l -v
  NAME      STATE           VERSION
* Debian    Running         1

C:\Users\heimn>wsl --set-version Debian 2
La conversion est en cours. Cette opération peut prendre quelques minutes...
Pour plus d’informations sur les différences de clés avec WSL 2, visitez https://aka.ms/wsl2
La conversion est terminée.

C:\Users\heimn>wsl -l -v
  NAME      STATE           VERSION
* Debian    Stopped         2

C:\Users\heimn>
````
### references
- https://medium.com/@callback.insanity/upgrading-to-wsl-2-9883688fcfa5

## VSCode and WSL

### The remote developpement plugin
As a software developper and tools developper on environements with multiple servers for many years i realy like this plugin. As i suspected (i never gone this far) we can work over networks and ssh connection like ... just if not ! (or nearly). i don't know exactly how it works but i see in the forground multiple ssh connexion of the plugin to the remote machine, and then a wrapper arround compatible VSCode features is created (file openning, terminal, etc ...). i think a kind of daemon is spawned executing tasks like a ``RPC`` Server
With a recent linux distribution you don't require nothing and the plugin will install itselves requirements on the remote machine. It do not require any specific privilege (dependecies seems installed in the user home dir so you can works as a simple user.
The Plugin allow us to do the same thing inside a WSL container.

- https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack
- https://code.visualstudio.com/docs/remote/remote-overview
- https://code.visualstudio.com/docs/remote/wsl

# others references

- https://docs.microsoft.com/en-us/windows/wsl/wsl2-mount-disk
- https://www.digitalocean.com/community/posts/trying-the-new-wsl-2-its-fast-windows-subsystem-for-linux
- https://docs.microsoft.com/en-us/windows/wsl/compare-versions