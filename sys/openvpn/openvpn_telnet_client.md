---
title: Openvpn telnet client
description: connect to the openvpn telnet clientand manage the openvpn state
published: true
date: 2021-05-01T00:04:45.320Z
tags: 
editor: vscode
dateCreated: 2021-05-01T00:04:45.320Z
---
# Openvpn telnet client

the community version of openvpn has a telnet client to get the global status, and more :

## help message overview
````
>INFO:OpenVPN Management Interface Version 1 -- type 'help' for more info
help
Management Interface for OpenVPN 2.4.4 x86_64-pc-linux-gnu [SSL (OpenSSL)] [LZO] [LZ4] [EPOLL] [PKCS11] [MH/PKTINFO] [AEAD] built on May 14 2019
Commands:
auth-retry t           : Auth failure retry mode (none,interact,nointeract).
bytecount n            : Show bytes in/out, update every n secs (0=off).
echo [on|off] [N|all]  : Like log, but only show messages in echo buffer.
exit|quit              : Close management session.
forget-passwords       : Forget passwords entered so far.
help                   : Print this message.
hold [on|off|release]  : Set/show hold flag to on/off state, or
                         release current hold and start tunnel.
kill cn                : Kill the client instance(s) having common name cn.
kill IP:port           : Kill the client instance connecting from IP:port.
load-stats             : Show global server load stats.
log [on|off] [N|all]   : Turn on/off realtime log display
                         + show last N lines or 'all' for entire history.
mute [n]               : Set log mute level to n, or show level if n is absent.
needok type action     : Enter confirmation for NEED-OK request of 'type',
                         where action = 'ok' or 'cancel'.
needstr type action    : Enter confirmation for NEED-STR request of 'type',
                         where action is reply string.
net                    : (Windows only) Show network info and routing table.
password type p        : Enter password p for a queried OpenVPN password.
remote type [host port] : Override remote directive, type=ACCEPT|MOD|SKIP.
proxy type [host port flags] : Enter dynamic proxy server info.
pid                    : Show process ID of the current OpenVPN process.
pkcs11-id-count        : Get number of available PKCS#11 identities.
pkcs11-id-get index    : Get PKCS#11 identity at index.
client-auth CID KID    : Authenticate client-id/key-id CID/KID (MULTILINE)
client-auth-nt CID KID : Authenticate client-id/key-id CID/KID
client-deny CID KID R [CR] : Deny auth client-id/key-id CID/KID with log reason
                             text R and optional client reason text CR
client-kill CID [M]    : Kill client instance CID with message M (def=RESTART)
env-filter [level]     : Set env-var filter level
client-pf CID          : Define packet filter for client CID (MULTILINE)
rsa-sig                : Enter an RSA signature in response to >RSA_SIGN challenge
                         Enter signature base64 on subsequent lines followed by END
certificate            : Enter a client certificate in response to >NEED-CERT challenge
                         Enter certificate base64 on subsequent lines followed by END
signal s               : Send signal s to daemon,
                         s = SIGHUP|SIGTERM|SIGUSR1|SIGUSR2.
state [on|off] [N|all] : Like log, but show state history.
status [n]             : Show current daemon status info using format #n.
test n                 : Produce n lines of output for testing/debugging.
username type u        : Enter username u for a queried OpenVPN username.
verb [n]               : Set log verbosity level to n, or show if n is absent.
version                : Show current version number.
END
````
(this is the help message of the telnet server listing functions to use)

## run and access the telnet server

using the management directive in the configuration file you can tell openvpn to run it on start ``management IP port [pw-file]``

### management option manual

this can be used as an option when running from command line utility or in the configuration file

````
--management IP port [pw-file]
Enable a TCP server on IP:port to handle daemon management functions. pw-file, if specified, is a password file (password on first line) or "stdin" to prompt from standard input. The password provided will set the password which TCP clients will need to provide in order to access management functions.
The management interface can also listen on a unix domain socket, for those platforms that support it. To use a unix domain socket, specify the unix socket pathname in place of IP and set port to 'unix'. While the default behavior is to create a unix domain socket that may be connected to by any process, the --management-client-user and --management-client-group directives can be used to restrict access.

The management interface provides a special mode where the TCP management link can operate over the tunnel itself. To enable this mode, set IP = "tunnel". Tunnel mode will cause the management interface to listen for a TCP connection on the local VPN address of the TUN/TAP interface.

While the management port is designed for programmatic control of OpenVPN by other applications, it is possible to telnet to the port, using a telnet client in "raw" mode. Once connected, type "help" for a list of commands.

For detailed documentation on the management interface, see the management-notes.txt file in the management folder of the OpenVPN source distribution.

It is strongly recommended that IP be set to 127.0.0.1 (localhost) to restrict accessibility of the management server to local clients.
````
### using a unix socket

as you can read in the ``management`` option manual you can configure the telnet server to listen on a unix socket.

exemple :

````
management /root/snap/easy-openvpn-server/current/unix-domain-socket
````
openvpn will just create an unix domain socket on start and the telnet server will listen on it

### references
- https://linux.die.net/man/8/openvpn


## using netcat to connect terminal to unix domain socket

the well know ``netcat`` command line can help to connect unix domain socket and user terminal in the ``netcat-bsd`` we can find a ``-U`` flag to do it :

````shell
user# apt install netcat-openbsd
user# nc -U ./uds
>INFO:OpenVPN Management Interface Version 1 -- type 'help' for more info
````

### references
- https://unix.stackexchange.com/questions/26715/how-can-i-communicate-with-a-unix-domain-socket-via-the-shell-on-debian-squeeze


## status command

the status command return an easily parsable string with clients and daemon infos : 

````text
status
TITLE,OpenVPN 2.4.4 x86_64-pc-linux-gnu [SSL (OpenSSL)] [LZO] [LZ4] [EPOLL] [PKCS11] [MH/PKTINFO] [AEAD] built on May 14 2019
TIME,Sat Dec  4 11:35:28 2021,1638617728
HEADER,CLIENT_LIST,Common Name,Real Address,Virtual Address,Virtual IPv6 Address,Bytes Received,Bytes Sent,Connected Since,Connected Since (time_t),Username,Client ID,Peer ID
CLIENT_LIST,kube-ace,80.13.93.113,10.0.0.5,,24504361,23212564,Wed Oct 13 07:41:54 2021,1634110914,UNDEF,173,4
CLIENT_LIST,vps02,51.91.250.103,10.0.0.2,,221343237,61770357,Wed Oct 13 08:25:25 2021,1634113525,UNDEF,176,5
CLIENT_LIST,debian001,78.203.52.83,10.0.0.4,,24939939,10314809,Sat Nov 27 02:34:05 2021,1637980445,UNDEF,278,1
CLIENT_LIST,rasp002,78.203.52.83,10.0.0.102,,340029,321424,Fri Dec  3 18:31:24 2021,1638556284,UNDEF,298,7
CLIENT_LIST,boulot0,2a01:e34:ecb3:4530:5c0c:b94b:28ff:2ca3,10.0.0.20,,1415881,468483,Fri Dec  3 10:33:41 2021,1638527621,UNDEF,296,0
CLIENT_LIST,adigitale,80.13.93.113,10.0.0.3,fd1d:cc55:893:1b4c::1001,1587375452,440316391,Wed Oct 13 07:41:50 2021,1634110910,UNDEF,172,3
CLIENT_LIST,gamingpc001,78.203.52.83,10.0.0.11,,3801481,6655343,Sat Dec  4 00:56:57 2021,1638579417,UNDEF,303,2
HEADER,ROUTING_TABLE,Virtual Address,Common Name,Real Address,Last Ref,Last Ref (time_t)
ROUTING_TABLE,10.0.0.102,rasp002,78.203.52.83,Sat Dec  4 11:27:36 2021,1638617256
ROUTING_TABLE,10.0.0.2,vps02,51.91.250.103,Sat Dec  4 11:35:28 2021,1638617728
ROUTING_TABLE,10.0.0.3,adigitale,80.13.93.113,Fri Dec  3 00:09:58 2021,1638490198
ROUTING_TABLE,fd1d:cc55:893:1b4c::1001,adigitale,80.13.93.113,Wed Oct 13 07:41:50 2021,1634110910
ROUTING_TABLE,10.0.0.11,gamingpc001,78.203.52.83,Sat Dec  4 11:35:28 2021,1638617728
ROUTING_TABLE,10.0.0.4,debian001,78.203.52.83,Sat Dec  4 11:27:49 2021,1638617269
ROUTING_TABLE,10.0.0.20,boulot0,2a01:e34:ecb3:4530:5c0c:b94b:28ff:2ca3,Fri Dec  3 10:33:41 2021,1638527621
GLOBAL_STATS,Max bcast/mcast queue length,1
END
````
