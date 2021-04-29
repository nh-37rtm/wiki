---
title: vscode and perl remote dev module
description: This is the short description
published: true
date: 2021-04-17T14:59:10.150Z
tags: 
editor: undefined
dateCreated: 2021-04-17T14:59:10.150Z
---

# perl language server configuration with vscode

to enable easy remote development with perl dans vscode you have to install the perl language server package

else you will have this kind of error :

````
[Info  - 2:58:58 PM] Connection to server got closed. Server will restart.
Can't locate Perl/LanguageServer.pm in @INC (you may need to install the Perl::LanguageServer module) (@INC contains: /home/nheim/perl5/lib/perl5/5.26.1/x86_64-linux-gnu-thread-multi /home/nheim/perl5/lib/perl5/5.26.1 /home/nheim/perl5/lib/perl5/x86_64-linux-gnu-thread-multi /home/nheim/perl5/lib/perl5 /home/nheim/perl5/lib/perl5/5.26.1/x86_64-linux-gnu-thread-multi /home/nheim/perl5/lib/perl5/5.26.1 /home/nheim/perl5/lib/perl5/x86_64-linux-gnu-thread-multi /home/nheim/perl5/lib/perl5 /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.26.1 /usr/local/share/perl/5.26.1 /usr/lib/x86_64-linux-gnu/perl5/5.26 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl/5.26 /usr/share/perl/5.26 /home/nheim/perl5/lib/perl5/5.26.0 /home/nheim/perl5/lib/perl5/5.26.0/x86_64-linux-gnu-thread-multi /home/nheim/perl5/lib/perl5/5.26.0 /home/nheim/perl5/lib/perl5/5.26.0/x86_64-linux-gnu-thread-multi /usr/local/lib/site_perl /usr/lib/x86_64-linux-gnu/perl-base).
BEGIN failed--compilation aborted.
[Error - 2:58:58 PM] Connection to server got closed. Server will not be restarted.
````

## Prerequisites

### libperl-dev

to allow system to build perl executable let's add the libperl-dev if not you may have this error during the configure execution :
````
configure: error: C compiler cannot create executables
````

````shell
sudo apt install libperl-dev
````

### AnyEvent::AIO Coro IO::AIO

let's install these perl library using :

````shell
cpan -i AnyEvent::AIO Coro IO::AIO
````

it may ask you to configure the ``cpan`` package manager if you never used it before, just install it for the user that should use the Language Server .

## the perl Language server

now you may know :

````shell
sudo cpan -i Perl::LanguageServer
````

if you do not install Perl::LanguagreServer on the global perl installation you should look ho to source correctly the bash profile modified by cpan, else it's by default not sourced




