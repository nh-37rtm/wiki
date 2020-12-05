---
title: openvpn and systemd
description: openvpn client systemd integration
published: true
date: 2020-11-27T00:04:45.320Z
tags: 
editor: undefined
dateCreated: 2020-11-27T00:04:37.820Z
---


# openvpn configuration systemd integration
Openvpn (a least on the raspbian distribution) come with a systemd generator script installed at ``/lib/systemd/system-generators/openvpn-generator``as said in the ``systemd.generator`` man page :
````
Generators are small executables that live in /usr/lib/systemd/system-generators/ and other directories listed above. systemd(1) will execute those binaries very early at bootup and at configuration reload time — before unit files are loaded. Their main purpose is to convert configuration that is not native into dynamically generated unit files.
````
as we can read in the openvpn README file :
````
Configuration files
-------------------
These new unit files expects client configuration files to be made available
in /etc/openvpn/client.  Similar for the server configurations, it is expected
to be found in /etc/openvpn/server.  The configuration files must have a .conf
file extension.
````
as we can see in the openvpn systemd generator (writen in shell on my system):
````bash
nheim@raspberrypi:~ $ cat /lib/systemd/system-generators/openvpn-generator
#!/bin/sh

# This systemd generator creates dependency symlinks that make all OpenVPN
# tunnels listed in /etc/default/openvpn's AUTOSTART be started/stopped/reloaded
# when openvpn.service is started/stopped/reloaded.

set -eu

GENDIR="$1"
WANTDIR="$1/openvpn.service.wants"
SERVICEFILE="/lib/systemd/system/openvpn@.service"
AUTOSTART="all"
CONFIG_DIR=/etc/openvpn

mkdir -p "$WANTDIR"

if test -e /etc/default/openvpn ; then
        . /etc/default/openvpn
fi

# No VPNs automatically started
if test "x$AUTOSTART" = "xnone" ; then
        exit 0
fi

if test "x$AUTOSTART" = "xall" -o -z "$AUTOSTART" ; then
        for CONFIG in `cd $CONFIG_DIR; ls *.conf 2> /dev/null`; do
                NAME=${CONFIG%%.conf}
                ln -s "$SERVICEFILE" "$WANTDIR/openvpn@$NAME.service"
        done
else
        for NAME in $AUTOSTART ; do
                if test -e $CONFIG_DIR/$NAME.conf ; then
                        ln -s "$SERVICEFILE" "$WANTDIR/openvpn@$NAME.service"
                fi
        done
fi
````
by default all files Matching *.conf in the /etc/openvpn are taken as a new openvpn configuration.
i'm not sure to understand everything .. because we have a systemd template  for client/server configuration :
````bash
nheim@raspberrypi:/lib/systemd/system $ cat  openvpn-client@.service
[Unit]
Description=OpenVPN tunnel for %I
After=network-online.target
Wants=network-online.target
Documentation=man:openvpn(8)
Documentation=https://community.openvpn.net/openvpn/wiki/Openvpn24ManPage
Documentation=https://community.openvpn.net/openvpn/wiki/HOWTO

[Service]
Type=notify
PrivateTmp=true
WorkingDirectory=/etc/openvpn/client
ExecStart=/usr/sbin/openvpn --suppress-timestamps --nobind --config %i.conf
CapabilityBoundingSet=CAP_IPC_LOCK CAP_NET_ADMIN CAP_NET_RAW CAP_SETGID CAP_SETUID CAP_SYS_CHROOT CAP_DAC_OVERRIDE
LimitNPROC=10
DeviceAllow=/dev/null rw
DeviceAllow=/dev/net/tun rw
ProtectSystem=true
ProtectHome=true
KillMode=process

[Install]
WantedBy=multi-user.target
````
in this use case the configuration file should be in ``/etc/openvpn/client/FILE.conf`` for a client configuration and ``/etc/openvpn/server/FILE.conf`` for a server configurations.but the generator seems like not using these dirs !?but the generator fileopenvpn-client@.service Template
<strong>to restart the system generators</strong> you can do ``nheim@vps157959:~$ systemctl daemon-reload``

i think openvpn@server.service will look at /etc/openvpn/server.conf
and openvpn-server@server.service will look at /etc/openvpn/server/server.conf

# last versions
In the last versions i had no more problems and this logic seem to be right :

for exemple with the ``37rtm`` server name add the ``.ovpn`` file in the ``/etc/openvpn/client/37rtm.conf`` (the extension ``.conf`` is important)
run 

````
systemctl daemon-reload
sudo systemctl start openvpn-client@37rtm.service
````

the ``openvpn-client@37rtm.service`` will look at the ``/etc/openvpn/client/37rtm.conf`` and the ``openvpn-server@37rtm.service``at the ``/etc/openvpn/server/37rtm.conf``