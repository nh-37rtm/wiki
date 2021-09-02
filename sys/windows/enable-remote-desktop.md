---
title: Remote desktop quick settings
description: Easily enable remote desktop
published: true
date: 2021-01-18T23:05:10.410Z
tags: 
editor: markdown
dateCreated: 2021-01-18T23:05:02.163Z
---

# Activating Remote Desktop
## Enabling the remote desktop in registry
```cmd
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
```
## Configure the firewall
````cmd
netsh advfirewall firewall set rule group="remote desktop" new enable=Yes
````
# Access Rights
by adding the user Remote Desktop Users group :

## Adding a user
```cmd
net localgroup "Remote Desktop Users" "UserName" /add
```
## Removing the user
````cmd
net localgroup "Remote Desktop Users" "UserName" /delete
````

# Références
- https://pureinfotech.com/enable-remote-desktop-command-prompt-windows-10/
- https://www.top-password.com/blog/add-user-to-remote-desktop-users-group-in-windows-10/


