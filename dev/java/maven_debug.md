---
title: debug tests with maven
description: option of surefire plugin to listen for a IDE debugger
published: true
date: 2020-12-01T09:36:22.296Z
tags: java, surefire, debug, maven
editor: markdown
dateCreated: 2020-12-01T09:36:22.296Z
---

# Maven
to run tests with maven use 
````
mvn test
````
to run test with a listenning debugger :
````
mvn test -Dmaven.surefire.debug
...
-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Listening for transport dt_socket at address: 5005
````

you can then connect your debugger to the port ``5005``

to use another port or some more fine options :
````
mvn -Dmaven.surefire.debug="-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=y,address=8000 -Xnoagent -Djava.compiler=NONE" test
````

## reference
- https://maven.apache.org/plugins/maven-surefire-plugin/index.html
- https://doc.nuxeo.com/corg/how-to-debug-a-test-run-with-maven/