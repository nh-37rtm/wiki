---
title: Windows with multiple tap devices
description: how to add a tap interface on windows
published: true
date: 2020-11-22T15:12:25.907Z
tags: 
editor: undefined
dateCreated: 2020-11-22T15:12:18.541Z
---

# Openvpn sur windows
![openvpngui.png](/openvpngui.png)
## Installation
Of course a Windows client with a little GUI exists.
It install a TUN interface using `TAP-Windows` installed in `C:\Program Files\TAP-Windows`.
in most of time i use the `OpenVpnGUI` installer wich install the tool.
## Configuration
You can easily configure it if you export a file with the `.ovpn` which should be an all in one configuration file containing :
- configuration of the client (which contain a lot of the server configuration itself). we can find for exemple :
  - the interface to create
  - the server adress/ip with it's openvpn port on wich client can connect to.
- some keys for the crypted exchanges
  - client private key
  - client certificate
  - static key
 
if you use a `ovpn` file you can just click on import file.
In the case you do have not an embeded keys configuration file. you have to copy all files into a subfolder of the the openvpn installation folder `C:\Users\%USER%\OpenVPN\config\%PROFILE_NAME%`
# Multiple TUN devices
You can use the `TAP-Windows tool` wich include a script called `addtap.bat` it will add one more device usable by openVPN
just call the script without arguments:
````
c:\> cd C:\Program Files\TAP-Windows\bin
C:\Program Files\TAP-Windows\bin\>addtap.bat
"devcon.exe" install "C:\Program Files\TAP-Windows\driver\OemWin2k.inf" tap0901
Device node created. Install is complete when drivers are installed...
Updating drivers for tap0901 from C:\Program Files\TAP-Windows\driver\OemWin2k.inf.
Drivers installed successfully.
````

```
Unknown adapter Local Area Connection:

   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : TAP-Windows Adapter V9
   Physical Address. . . . . . . . . : 00-FF-90-03-D7-B9
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes

Unknown adapter Local Area Connection 2:

   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : TAP-Windows Adapter V9 #2
   Physical Address. . . . . . . . . : 00-FF-75-A2-95-54
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
```

# References
- https://michlstechblog.info/blog/openvpn-connect-to-multiple-vpns-on-windows/


