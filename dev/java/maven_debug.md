---
title: debug tests with maven
description: option of surefire plugin to listen for a IDE debugger
published: true
date: 2020-12-05T11:20:37.635Z
tags: 
editor: undefined
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

# Arquillian

Arquillian is a debbugging tool for JavaEE. It manage a protocol to connect to an application server (or just spawn a temporary local managed application server for the test) and run whatever tests you would like, using the application server environement !

it use a configuration file positionned in ``src/test/resources/arquillian.xml`` for exemple it can be :

the specification of this file can be found (depending on the adapter used) at https://docs.jboss.org/author/index.html


````xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- JBoss, Home of Professional Open Source Copyright 2012, Red Hat, Inc.
	and/or its affiliates, and individual contributors by the @authors tag. See
	the copyright.txt in the distribution for a full listing of individual contributors.
	Licensed under the Apache License, Version 2.0 (the "License"); you may not
	use this file except in compliance with the License. You may obtain a copy
	of the License at http://www.apache.org/licenses/LICENSE-2.0 Unless required
	by applicable law or agreed to in writing, software distributed under the
	License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS
	OF ANY KIND, either express or implied. See the License for the specific
	language governing permissions and limitations under the License. -->
<arquillian xmlns="http://jboss.org/schema/arquillian"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://jboss.org/schema/arquillian
        http://jboss.org/schema/arquillian/arquillian_1_0.xsd">
    <!-- Example configuration for a remote JBoss AS 7 instance -->
    <defaultProtocol type="jmx-as7" />
    <container qualifier="wildfly-remote" default="true" >
        <configuration>
            <property name="managementAddress">10.0.0.2</property>
            <property name="managementPort">9990</property>
            <property name="username">admin</property>
            <property name="password">admin</property>
            <property name="allowConnectingToRunningServer">true</property>
        </configuration>
    </container>
    <container qualifier="wildfly-remote2">
<!--        <protocol type="Servlet 3.0">
            <property name="host">10.0.0.1</property>
            <property name="port">9990</property>
        </protocol>-->
        <configuration>
            <property name="managementAddress">10.0.0.1</property>
            <property name="managementPort">9990</property>
            <property name="username">admin</property>
            <property name="password">admin</property>
            <property name="allowConnectingToRunningServer">true</property>
        </configuration>
    </container>
</arquillian>

````

we can see two profiles in this configuration, to select an Arquillian profile when running the maven command just use the ``arquillian.launch`` option :
````
nheim@nheim-virtual-machine:~/src/javaTest$ mvn test -Parq-wildfly-remote -Darquillian.lauch=wildfly-remote2
````



## selecting 

## Arquillian and Wildfly

to connect to a remote existing wildfly application server


# Wildfly

````
docker exec 0c67c1364637 /opt/jboss/keycloak/bin/add-user-keycloak.sh -u admin -p admin
docker exec -it 0c67c1364637  /opt/jboss/keycloak/bin/add-user.sh -u admin -p admin
docker run -e KEYCLOAK_USER=admin -e KEYCLOAK_PASSWORD=admin \
    -e KEYCLOAK_IMPORT=/tmp/example-realm.json -v ./quickstart-realm.json:/tmp/example-realm.json jboss/keycloak


docker run -p 8080:8080 jboss/keycloak

docker run -e JAVA_OPTS_APPEND="-agentlib:jdwp=transport=dt_socket,address=0.0.0.0:8787,server=y,suspend=n" -e KEYCLOAK_USER=admin -e KEYCLOAK_PASSWORD=admin -e ROOT_LOGLEVEL=DEBUG -p 8080:8080 -p 9990:9990 -p 8787:8787 -it jboss/keycloak -b 0.0.0.0 -bmanagement 0.0.0.0

docker run -e KEYCLOAK_USER=admin -e KEYCLOAK_PASSWORD=admin \
    -e KEYCLOAK_IMPORT=/tmp/quickstart-realm.json -v ./quickstart-realm.json:/tmp/quickstart-realm.json jboss/keycloak
````

## reference
- https://docs.wildfly.org/20/Testsuite.html
- https://github.com/wildfly/wildfly/blob/master/testsuite/integration/manualmode/src/test/config/arq/arquillian.xml

# Maven

````
mvn clean verify -Darquillian=jbossas-managed-7

````