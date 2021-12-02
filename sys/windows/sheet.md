---
title: Windows OpenSSH
description: 
published: true
date: 2021-02-06T08:03:16.268Z
tags: windows, sheet
editor: markdown
dateCreated: 2020-12-15T08:03:16.268Z
---

# Listing the open ports with program name 

````powershell
PS C:\git\xperience_react_native> netstat -aon

Connexions actives

  Proto  Adresse locale         Adresse distante       État
  TCP    0.0.0.0:445            AD-PF1EZXBV:0          LISTENING       4
  TCP    0.0.0.0:808            AD-PF1EZXBV:0          LISTENING       4892
  TCP    0.0.0.0:2179           AD-PF1EZXBV:0          LISTENING       5364
````

the n switch should speed up the command becase it do not resolve the host name

## List and kill openned port program (ex for react)

````cmd
Compiled successfully!
? Something is already running on port 3000.

Would you like to run the app on another port instead? » (Y/n)
````

find the application in background

````cmd
PS C:\git\xperience-react\web> netstat -aon | findstr :3000  
  TCP    0.0.0.0:3000           0.0.0.0:0              LISTENING       8968
PS C:\git\xperience-react\web>
````

kill the application in background

````cmd
PS C:\git\xperience-react\web> taskkill /PID 8968 /F 
Opération réussie : le processus avec PID 8968 a été terminé.
PS C:\git\xperience-react\web>
````

````cmd
Compiled successfully!
? Something is already running on port 3000.

Would you like to run the app on another port instead? » (Y/n)

````
find the application in background

````cmd
PS C:\git\xperience-react\web> netstat -aon | findstr :3000  
  TCP    0.0.0.0:3000           0.0.0.0:0              LISTENING       8968
PS C:\git\xperience-react\web>
````

kill the application in background

````cmd
PS C:\git\xperience-react\web> taskkill /PID 8968 /F 
Opération réussie : le processus avec PID 8968 a été terminé.
PS C:\git\xperience-react\web>
````


