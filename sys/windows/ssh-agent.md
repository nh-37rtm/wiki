---
title: Windows OpenSSH
description: 
published: true
date: 2020-12-15T08:03:16.268Z
tags: windows, ssh, client, openssh
editor: markdown
dateCreated: 2020-12-15T08:03:16.268Z
---

# Installing openSSH
A version for windows of openSSH exists, you can install it easily using. Powershell :
checking the versions availlable
````
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'

# This should return the following output:

Name  : OpenSSH.Client~~~~0.0.1.0
State : NotPresent
Name  : OpenSSH.Server~~~~0.0.1.0
State : NotPresent
````

install it :
````
# Install the OpenSSH Client
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Install the OpenSSH Server
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

# Both of these should return the following output:

Path          :
Online        : True
RestartNeeded : False
````


## reference :
- https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse

# The agent

As in other exploitation systems you have the ssh-agent deployed.

# Testing the agent

````
C:\Users\heimn>ssh-agent
C:\Users\heimn>
C:\Users\heimn>ssh-add
Identity added: C:\Users\heimn/.ssh/id_rsa (C:\Users\heimn/.ssh/id_rsa)
C:\Users\heimn>ssh nheim@10.0.0.1
warning: agent returned different signature type ssh-rsa (expected rsa-sha2-512)
nheim@10.0.0.1's password:
````

## reference :
- https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement


# Updating the agent

## Downloading
Using the git repository : ``https://github.com/PowerShell/Win32-OpenSSH/releases/latest/`` i managed to replace the ``C:\Windows\System32\OpenSSH\`` files helped by these powershell instructions :

## Stopping the ssh agent
````
Stop-Service ssh-agent
````

## Taking the own of the system OpenSSH files
````
icacls.exe 'C:\Windows\System32\OpenSSH' /grant 'BUILTIN\Administrators:(OI)(CI)F'
icacls.exe 'C:\Windows\System32\OpenSSH' /grant 'BUILTIN\Administrators:F' /t
````

## Backing up the system files

replace the system files :

````
copy * C:\Windows\System32\OpenSSH\
````

# reference 
- https://github.com/PowerShell/Win32-OpenSSH/wiki/How-to-retrieve-links-to-latest-packages
- https://superuser.com/questions/1395962/is-it-possible-to-update-the-built-in-openssh-client-in-windows-10

# Resolving setup problems

After updating the files following the previous steps, i fall into this error :
````
PS C:\Users\heimn\Downloads\OpenSSH-Win64\OpenSSH-Win64> ssh-add C:\Users\heimn\.ssh\id_rsa
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions for 'C:\\Users\\heimn\\.ssh\\id_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
````

I think the more recent version of OpenSSH is more secure and do not allow the file to be unprocected.

let's fix the rights allowing only the current user to access the key :


````
PS C:\Users\heimn\.ssh> icacls .ssh/id_rsa /inheritance:d /grant "heimn:(F)"
````

It works ! :

````
PS C:\Users\heimn\.ssh> ssh-agent
PS C:\Users\heimn\.ssh> ssh-add .\id_rsa
Identity added: .\id_rsa (.\id_rsa)
PS C:\Users\heimn\.ssh> ssh nheim@10.0.0.1
Linux vps-982e47f4 4.19.0-12-cloud-amd64 #1 SMP Debian 4.19.152-1 (2020-10-18) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Web console: https://vps-982e47f4.vps.ovh.net:9090/ or https://51.77.214.35:9090/

Last login: Mon Dec 14 12:28:43 2020 from 82.67.52.83
nheim@vps-982e47f4:~$
````






