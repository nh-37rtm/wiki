---
title: install android tools
description: 
published: true
date: 2021-01-20T10:35:47.428Z
tags: 
editor: markdown
dateCreated: 2021-01-20T10:35:47.428Z
---

# installing tools to build and debug on the smartphone
## prepare environment 

### sdkmanager (3.0)
- on the android studio download page go to options (https://developer.android.com/studio#downloads)
- download the ``Command line tools only`` (https://dl.google.com/android/repository/commandlinetools-linux-6858069_latest.zip)

you should have this kind of arborescence (or prepare it yourself):
+- android-sdk
    +- cmdline-tools
        +- latest

else you will have this kind of error :

````
Error: Could not determine SDK root.
Error: Either specify it explicitly with --sdk_root= or move this package into its expected location: <sdk>/cmdline-tools/latest/
````

### update path
why not adding the bin folder to the path ? 

````
export PATH=$PATH:/media/nheim/Maxtor/android/linux/sdk/cmdline-tools/latest/bin
````

### download packages
sdkmanager --list
sdkmanager "build-tools;30.0.3"

you should have this directories tree :

````
.
├── build-tools
├── cmdline-tools
├── emulator
├── licenses
├── patcher
├── platform-tools
└── tools
````

# references

- https://stackoverflow.com/questions/37505709/how-do-i-download-the-android-sdk-without-downloading-android-studio
- https://developer.android.com/studio/command-line