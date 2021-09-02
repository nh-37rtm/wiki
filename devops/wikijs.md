---
title: Manage Wikijs git repository
description: 
published: true
date: 2020-12-05T12:35:47.428Z
tags: 
editor: undefined
dateCreated: 2020-12-05T12:35:39.739Z
---

# Wikijs and git
WikiJS as a nice ``storage`` plugin which synchronise git remository with the wikiJs content.

wikijs seems use a classic git instance and git local repository installed on the Docker package i used https://docs.requarks.io/install/docker

the local repository is at :
````bash
bash-5.0$ pwd
/wiki/data/repo
bash-5.0$      
````
because is allow bi-directional synchronisation you may fall in the confilting git state in which you should help WikiJs doing synchronisation

let's just shell the container 
with ``docker exec``
````bash
bash-5.0$ cd /wiki/data/repo
bash-5.0$ docker exec -it ${CONTAINER} bash
````

and let's fix the issue !




