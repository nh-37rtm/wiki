

# Aria2

Aria2 is a very fast library to download in multiples protocol including Torrent, FTP, HTTP ...
you can easily install it from binaries, source or debian repository

it provide an RDP api to be externally controlled for example by an UI !

some websites show many existing UI

my choice at the moment is :

[aria2_remote_control_url] https://sourceforge.net/projects/aria2cremote/ "ARIA2 Remote Control" because of it's robust and clear (to me), ``Transmission Controller`` like's UI.

## Let's run it with RPC server enabled

````
aria2c --enable-rpc --rpc-listen-all --rpc-allow-origin-all --daemon --dir /APPBOX_DATA/storage/
````

it gives back control to the shell (as i used the ``--daemon`` switch)

and we now have aria2 listening on the default 6800 port

````bash
nheim@vnc:~$ netstat -tulpn | grep aria
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
tcp        0      0 0.0.0.0:6800            0.0.0.0:*               LISTEN      71846/aria2c
nheim@vnc:~$
````

## Connect the UI

### Direct access

if you are not using a remote server to run Aria2 no need to worry just connect to your 6800 local port.

### Tunneling

Somme time calls the poor man VPN, or SSH tunnels, ssh tunnelling can be usefull in the case your server has no published ports over internet or if you just don't want to publish any.

using putty or with only ssh command line like 

````
ssh -L6800:localhost:6800 user@remote.server -N
````

## Let's download

let's download really fast and with multiple parallel sources if you like!







