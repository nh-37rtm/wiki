---
title: links to coopalim projects
description: 
published: true
date: 2020-12-05T15:26:17.852Z
tags: 
editor: undefined
dateCreated: 2020-12-05T15:26:14.183Z
---

# CoopAlim infra
Message de Alex :

@channel merci à tous pour votre présence ce matin. je vous fournis un mémo dans l'aprem / soirée.
En attendant, les liens des trucs que nous avons vu :

- Dépôt coopalim-infra : https://gitlab.com/coopalim/coopalim-infra/
- Infos swarm (WIP) https://gitlab.com/coopalim/coopalim-infra/-/blob/master/Swarm.md
- Infos stack MySQL : https://gitlab.com/coopalim/coopalim-infra/-/blob/master/stacks/README_mysql.md
- Infos stack Proxy : https://gitlab.com/coopalim/coopalim-infra/-/blob/master/stacks/README_proxy.md
- Dépôt wordpress : https://gitlab.com/coopalim/wordpress
- Dépôt mysql : https://gitlab.com/coopalim/mysql
- Dépôt proxy (HTTP) : https://gitlab.com/coopalim/proxy


Les scripts utilitaires pour client docker
- https://gitlab.com/coopalim/coopalim-infra/-/blob/master/bin/loadMachine.sh
- https://gitlab.com/coopalim/coopalim-infra/-/blob/master/bin/deploy-test.sh
- https://gitlab.com/coopalim/coopalim-infra/-/blob/master/bin/service-exec.sh

Les schémas "swarm" :

![schémas_cluster_swarm.png](/schémas_cluster_swarm.png)https://chat.coopalimstrasbourg.com/files/tan8jc8ucbrf7g9eqes5kqophr/public?h=N8MzaxB_fSzcSohPFXlPQndpkWemwqPib2CEF_EEwLQ


## Docs

passbolt : https://docs.google.com/document/d/15cQyd3DIlfgBm14fTf4izsBtABuDkV43-EPUWI-Aocg/edit


## Dyndns
Configuration à priori bonne de ddclient

````
nheim@nheim-virtual-machine:~$ sudo cat /etc/ddclient.conf 
# Configuration file for ddclient generated by debconf
#
# /etc/ddclient.conf

protocol=dyndns2
# use=if, if=ens33
use=web, web=my.ip.fi/
server=www.ovh.com
login=coopalimstrasbourg.com-n.heim
password='PSrRUU25iWHaLBAqzHm8rivAb41oCjY'
n-heim.dev.coopalimstrasbourg.com
````


## windows

fonctionne avec les clef : copiées ici : ``C:\Users\heimn\.docker\machine\certs\coopalim``

````
set DOCKER_HOST=tcp://188.165.245.14:12378
set DOCKER_TLS_VERIFY=1
set DOCKER_CERT_PATH=C:\Users\heimn\.docker\machine\certs\coopalim\test1
````