---
title: CPAN and building modules
description: Problem when installing a module via CPAN
published: true
date: 2020-11-22T20:56:08.769Z
tags: 
editor: undefined
dateCreated: 2020-11-22T20:47:53.040Z
---

# The problem
i had an error when compiling (like i ever did) one perl module using 
````
cpan IO::AIO
...
Continue anyways?  [y] y
checking for gcc... x86_64-linux-gnu-gcc
checking whether the C compiler works... no
configure: error: in `/root/.cpan/build/IO-AIO-4.72-0':
configure: error: C compiler cannot create executables
See `config.log' for more details
Warning: No success on command[/usr/bin/perl Makefile.PL INSTALLDIRS=site]
  MLEHMANN/IO-AIO-4.72.tar.gz
  /usr/bin/perl Makefile.PL INSTALLDIRS=site -- NOT OK
````

the module required to install the ``libperl-dev`` ubuntu package or to patch the Makefile.pl :
````patch
diff --git a/Makefile.PL b/Makefile.PL
index bb72a57..9573cce 100644
--- a/Makefile.PL
+++ b/Makefile.PL
@@ -62,7 +62,7 @@ EOF
       $ENV{CFLAGS}   = $Config{ccflags};
       $ENV{LDFLAGS}  = "$Config{ldflags} $Config{ccdlflags}";
       $ENV{LINKER}   = $Config{ld}; # nonstandard
-      $ENV{LIBS}     = "-L$Config{archlibexp}/CORE -L$Config{privlibexp} -lperl $Config{perllibs}";
+      $ENV{LIBS}     = "-L$Config{archlibexp}/CORE -L$Config{privlibexp} $Config{perllibs}";
 
       system $ENV{SHELL}, -c => "./configure --prefix \Q$Config{prefixexp}\E"
          and exit $? >> 8;
````

# References
- https://rt.cpan.org/Public/Bug/Display.html?id=126277
