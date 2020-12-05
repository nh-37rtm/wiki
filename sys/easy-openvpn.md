---
title: Easy-openvpn snap package rebuild
description: let's rebuild the `easy-openvpn` package to customize some parameters
published: true
date: 2020-11-21T23:05:10.410Z
tags: 
editor: undefined
dateCreated: 2020-11-21T23:05:02.163Z
---

# Let's build it !
to refresh the easy-openvpn-server configuration i had to do : 

this package works with python and the jinja template language. the topology, and some options are defined in a jinja template file positionned inside the package at :

```bash
find ./templates/
./templates/
./templates/RFC3526-dh4096.pem
./templates/client.ovpn
./templates/server.conf
```

i customised :
- adding the client-to-client for each client to communicate with each others
- change old `net30` topology to subnet

here is the end of the server.conf template :

```bash
tail ./server.conf 
  # the VPN is the default gateway. NetworkManager does this automatically but
  # the `update-systemd-resolved` script used by the openvpn CLI requires this
  # option.
  # https://github.com/jonathanio/update-systemd-resolved#usage
  # https://github.com/systemd/systemd/issues/6076#issuecomment-432177655
  push "dhcp-option DOMAIN-ROUTE ."
{% endif %}

topology net30
```

i also would like my servers to have fixed ip address so i created a `~/snap/easy-openvpn-server/current/client-configs/vps02` file with the only content is:
```
ifconfig-push 10.0.0.5 255.255.255.0
```

you can now juste build the package with the `snapcraft` without parameter


