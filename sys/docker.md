---
title: Windows docker client
description: Installing the docker client alone (without the engine)
published: true
date: 2020-11-30T00:50:04.789Z
tags: 
editor: undefined
dateCreated: 2020-11-30T00:49:57.718Z
---

# Docker-Desktop
Docker Desktop is powerfull but in my opinion it should not be installed on every computer, it cusumes a lot of memory/cpu. why not installing docker on a server and work only connect to the docker host to work ?
The problem was that to connect to the docker host with the docker protocol you should have installed docker. the official way to install docker is officialy the docker-desktop package.
it exists another way to just install the client using this link : https://github.com/StefanScherer/docker-cli-builder/releases.
this is perfect no need to install the full engine, then for exemple you can connect vscode to containers hosted on any server publishing the docker engine port. for this just set the ``DOCKER_HOST`` environement variable 
````set DOCKER_HOME=tcp://10.0.0.2:2375````