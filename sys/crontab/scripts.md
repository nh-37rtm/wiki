---
title: Untitled Page
description: practice unix users crontabs
published: true
date: 2020-11-21T22:52:32.207Z
tags: crontabs sys unix
editor: markdown
dateCreated: 2020-11-20T10:49:49.158Z
---

# Informations on environement
the global crontab is the root crontab file.
the crontab user manual says about the working files :
>Each user can have their own crontab, and though
these are files in `/var/spool/cron/crontabs`, they are not
intended to be edited directly.

these files are considered "internal" to the system and may not be changed to avoid problems like data lost etc ...

# Testing crontab scripts
who did never made a script working all well and when inside the crontab environment .. it crashes
This is often because the environment is not all fully initialised. To run a script inside the crontab environment you can "extract" the ennvironment inside the cron with a simple :
```bash
env > crontab.env
```
then the  `env` can help us by spawing a new program with an empty environmenent as said by the manual :
```
 The  first  form  of  this  command is used to install a new crontab from some named file or standard input if the pseudo-filename
       ``-'' is given.
```

```bash
env -i sh -c '. crontab.env; myscript.sh'
```


# references
- https://askubuntu.com/questions/216692/where-is-the-user-crontab-stored
- https://benohead.com/blog/2012/09/10/linux-simulate-the-cron-environment-to-test-run-your-scripts/

