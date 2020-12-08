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


this link provide detailed informations on the way Arquillian is woking : https://docs.jboss.org/arquillian/reference/1.0.0.Alpha2/en-US/html_single/

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

## WildFly : What a new application server ?
``Wildfly`` is only a ``codename`` for the AS version of JBoss, this is like the comunity edition of the Red Hat ``JBoss EAP``.

## Which version this application is using ?
the application server provide a ``standalone.sh`` script to run it, you can use it with the ``--version``
````
./standalone.sh --version
````

Another way is to use the ``jboss-cli.sh`` :
````
bash-4.4$ ./bin/jboss-cli.sh -c --controller=127.0.0.1:9990 --user=admin --password=admin --command=":read-attribute(name=product-version)"{
    "outcome" => "success",
    "result" => "11.0.0"
}
bash-4.4$ 
````
## Providing you own Persistence Provider version
to do it let's use the ``providerModule`` in the persistence.xml file as in :
````
<property name="jboss.as.jpa.providerModule" value="application" />
````

## references
- http://www.mastertheboss.com/jboss-server/jboss-configuration/find-out-the-jboss-version-you-are-running
- https://stackoverflow.com/questions/31756933/what-is-the-difference-between-jboss-eap-wildfly-jboss-web-and-jboss-server#:~:text=JBoss%20AS%2FWildFly%20is%20the,which%20stood%20for%20Application%20Server.&text=JBoss%20Web%20was%20the%20name,JBoss%20EAP%206%20and%20earlier.

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

the Arquillian Wildfly adapter for remote servers is described here : https://docs.jboss.org/author/display/ARQ/JBoss%20AS%207.1,%20JBoss%20EAP%206.0%20-%20Remote.html

## reference
- https://docs.wildfly.org/20/Testsuite.html
- https://github.com/wildfly/wildfly/blob/master/testsuite/integration/manualmode/src/test/config/arq/arquillian.xml
- https://docs.jboss.org/author/display/WFLY/WildFly%20Testsuite%20Test%20Developer%20Guide.html


# Maven

````
mvn clean verify -Darquillian=jbossas-managed-7

````


# Errors
## org.hibernate.HibernateException: Access to DialectResolutionInfo cannot be null when 'hibernate.dialect' not set"}}
This is a high level error only telling there is a problem while the datasource initialisation it could be a lot of things !

i found i made a mistake in the user password by adding some verbosity to the ``org.hibernate``â package :
by adding in the logging.properties file : 
````
logging.level.org.hibernate=DEBUG
````

giving the error (with a lot more information)
````
Caused by: org.h2.jdbc.JdbcSQLException: Wrong user name or password [28000-197]
        at com.h2database.h2@1.4.197//org.h2.message.DbException.getJdbcSQLException(DbException.java:357)
        at com.h2database.h2@1.4.197//org.h2.message.DbException.get(DbException.java:179)
        at com.h2database.h2@1.4.197//org.h2.message.DbException.get(DbException.java:155)
        at com.h2database.h2@1.4.197//org.h2.message.DbException.get(DbException.java:144)
        at com.h2database.h2@1.4.197//org.h2.engine.Engine.validateUserAndPassword(Engine.java:341)
        at com.h2database.h2@1.4.197//org.h2.engine.Engine.createSessionAndValidate(Engine.java:165)
        at com.h2database.h2@1.4.197//org.h2.engine.Engine.createSession(Engine.java:140)
        at com.h2database.h2@1.4.197//org.h2.engine.Engine.createSession(Engine.java:28)
        at com.h2database.h2@1.4.197//org.h2.engine.SessionRemote.connectEmbeddedOrServer(SessionRemote.java:351)
        at com.h2database.h2@1.4.197//org.h2.jdbc.JdbcConnection.<init>(JdbcConnection.java:124)
        at com.h2database.h2@1.4.197//org.h2.jdbc.JdbcConnection.<init>(JdbcConnection.java:103)
        at com.h2database.h2@1.4.197//org.h2.Driver.connect(Driver.java:69)
        at org.jboss.ironjacamar.jdbcadapters@1.4.22.Final//org.jboss.jca.adapters.jdbc.local.LocalManagedConnectionFactory.createLocalManagedConnection(LocalManagedConn
        ... 38 more
````
