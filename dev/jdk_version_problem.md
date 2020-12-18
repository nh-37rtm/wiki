---
title: yet another jdk version error identification
description: 
published: true
date: 2020-12-18T10:19:02.782Z
tags: java, openjdk14
editor: markdown
dateCreated: 2020-11-30T08:58:38.630Z
---

# Arquillian exemples
i was trying to run some JPA persistence test using the Arquillian framework using a glassfish embeded server.
The project is a quickstart from the Arquillian project :
````
heim@nheim-virtual-machine:~/src/arquillian-examples$ git remote -vv
origin	https://github.com/arquillian/arquillian-examples.git (fetch)
origin	https://github.com/arquillian/arquillian-examples.git (push)
````
# The Error
the test only insert some data and do some manipulation with the entityManager. but it fails at a early state in the deploy simulation method. when i run the unit tests. the stack trace begin with  :
````
java.lang.RuntimeException: Could not setup GlassFish Embedded Bootstrap
...
Caused by: java.lang.reflect.InaccessibleObjectException: Unable to make public java.util.Enumeration jdk.internal.loader.BuiltinClassLoader.findResources(java.lang.String) throws java.io.IOException accessible: module java.base does not "exports jdk.internal.loader" to unnamed module @418e7838
````

I felt like (to confirm) the problem was security access to reflexion object.
I was using the OpenJDK14 version and just changing it to the OpenJDK8 worked.


- allo
	- à l'huile
		- dfgfdg
- dfgfdg

  

>
> this is somme info
> - allo
>  - à l'huile
>    - yop
{.is-info}


