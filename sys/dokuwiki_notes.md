---
title: Dokuwiki install notes
description: 
published: true
date: 2020-11-21T23:12:18.860Z
tags: 
editor: undefined
dateCreated: 2020-11-21T23:12:04.991Z
---

# Setting up dokuwiki
at the end of the archive extraction i had to :
- activate the `acl` property in conf/dokuwiki.php
- move the exemples dist files (users.auth.php.dist ⇒ users.auth.php and acl.auth.php.dist ⇒ acl.auth.php) as said in the acl initialisation article https://www.dokuwiki.org/acl
  
- add the first admin user, i had to add to create an entry inside the users.auth.php, the default hash method for the password storage is SMD5, i used this website to generate one : https://sprhost.com/tools/SMD5.php.
- these two last steps can be done by visiting the install.php page first
- install the tag plugin
- install the pagelist plugin




