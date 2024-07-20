META:TOPICINFO{author="paulellis" date="1614100594" format="1.1"
reprev="1.24" version="1.24"}
META:TOPICPARENT{name="DeploymentMonitoring"}

# Jazz monitoring through JMX [jazz-monitoring-through-jmx]

DKGRAY Authors: Main.JorgeAlbertoDiaz, Main.PaulEllis,
Main.GeraldMitchell Build basis: Enterprise Lifecycle Management suite
6.x, 7.x ENDCOLOR

TOC{title="Page contents"}

Note: Updated February 2021 with a significant update on how to use
WebSphere Liberty in both local connector or REST connector mode.

Knowing how your application server is behaving is very important, and a
good administrator can identify these things: when Jazz servers need
more resources, deployment usage patterns, the potential cause of
issues. If you need to know how your JVM is running, or how many threads
are in use, a simple and relatively fast way of setting up monitoring by
using Java Management Extensions (JMX) is described below.

Java Management Extensions (JMX) is a Java technology standard for the
management and monitoring of Java applications. JMX provides a set of
tools and APIs for the instrumentation and monitoring of Java
applications, and these are included as part of standard Java libraries
since J2SE 5.0. Both Apache Tomcat and WebSphere Application Server
implement JMX, which provides interfaces for administration and exposes
resource monitoring information. This page will focus on how to leverage
JMX for basic monitoring of your Jazz servers.

While enterprise-level monitoring tools will define ways of connecting
to the servers to gather and use this JMX information (some with custom
clients that are API based), this topic will show how you can connect
using **JConsole** for real-time monitoring of your servers as a simple
and fast approach for gaining insight on your servers' status. JConsole
is a lightweight monitoring tool that you can find as part of JDK
located in `JDK_HOME/bin`. You can use the JConsole-based examples as
guideline for configuring some other similar clients of your choice. You
can learn about JConsole, and how to use it while applying the
configuration options in this topic, at [Using
JConsole](http://docs.oracle.com/javase/7/docs/technotes/guides/management/jconsole.html)

You can learn more about JMX technology
[here](http://www.oracle.com/technetwork/java/javase/tech/articles-jsp-135975.html).

## Connecting to WebSphere Liberty by using JMX

Liberty supports two JMX connectors: local connector and REST connector.
Each connector is enabled through a different Liberty feature:

\* The local connector is enabled through the Liberty feature
localConnector-1.0. Access through the local connector is protected by
the policy implemented by the SDK in use. Currently the SDKs require
that the client runs on the same host as Liberty, and under the same
user ID.

\* The REST connector is enabled through the Liberty feature
restConnector-2.0. The restConnector-2.0 feature supersedes the
restConnector-1.0 feature. Remote access through the REST connector is
protected by a single administrator role through the HTTPS port defined
by the default httpEndpoint. In addition, SSL is required to keep the
communication confidential. The REST connector features already include
the ssl-1.0 feature.

### Restriction

Do not use JDK options that start with com.sun.management.jmxremote,
which are described in [\[Monitoring and Management Using JMX
Technology](https://docs.oracle.com/javase/8/docs/technotes/guides/management/agent.html),
with the Liberty JMX support. Those JDK options adversely affect the
Liberty MBean registration framework.

### Connecting to Liberty by local connector

You can access the local Java Management Extensions (JMX) connector on
Liberty. The local connector is enabled through the Liberty feature
localConnector-1.0. Currently the SDKs require that the client runs on
the same host as Liberty.

#### Procedure

1\) Enable the local connector by using the following code in the
server.xml file(/server/liberty/servers/clm).

localConnector-1.0

2\) Restart the server

3\) After restarting a file "com.ibm.ws.jmx.local.address" at location
/server/liberty/servers/clm/logs/state/com.ibm.ws.jmx.local.address will
be generated

4\) Copy the content of "com.ibm.ws.jmx.local.address" on clipboard or
on a note.

5\) Launch the JConsole app from /bin

6\) For the JConsole tool, paste the contents of the clipboard into the
"Remote Process" field, then click Connect.

7\) When the connection succeeds, JConsole starts monitoring you can see
the MBeans.

### Connecting to Liberty by REST connector

Configuring secure JMX connection to Liberty:- You can access the
secured Java Management Extensions (JMX) connectors on Liberty by using
SSL. The secured JMX connection is enabled by the Liberty feature
restConnector-2.0.

The REST connector is enabled through the Liberty feature
restConnector-2.0. Remote access through the REST connector is protected
by a single administrator role through the HTTPS port defined by the
default httpEndpoint. In addition, SSL is required to keep the
communication confidential. The REST connector features already include
the ssl-1.0 feature.

Example from server.xml

#### Procedure

1\) Enable the REST connector by using the following code in the
server.xml file.

restConnector-2.0

2\) Default Certificate information and keystore password The keystore
ibm-team-ssl.p12 is in
JazzInstallDir/server/liberty/servers/clm/resources/security. The
password and type of the keystore is in the server.xml file in
JazzInstallDir/server/liberty/servers/clm/ specified in the section,
with the password encoded. The default keystore password is set to
ibm-team. This keystore includes a self-signed certificate that
identifies the server as localhost.

3\) Restart the server

4\) After restarting a file "com.ibm.ws.jmx.rest.address" at location
/server/liberty/servers/clm/logs/state/ will be generated

5\) Copy the content of "com.ibm.ws.jmx.rest.address" on clipboard or on
a note. e.g. <service:jmx:rest://localhost:9443/IBMJMXConnectorREST>

6\) Configure a user or group to the administrator role in the
server.xml file, e.g. clmadmin

clmadmin JazzAdmins

7\) Use the following properties for SSL certificates:
-J-Djavax.net.ssl.trustStore= -J-Djavax.net.ssl.trustStorePassword=
-J-Djavax.net.ssl.trustStoreType=

The following example shows the jConsole tool and SSL configurations in
use together: jconsole -J-Djava.class.path=JAVA_HOME/lib/jconsole.jar;
JAVA_HOME/lib/tools.jar; WLP_HOME/clients/restConnector.jar
-J-Djavax.net.ssl.trustStore=/server/liberty/servers/clm/resources/security/ibm-team-ssl.p12
-J-Djavax.net.ssl.trustStorePassword=ibm-team
-J-Djavax.net.ssl.trustStoreType=PKCS12

8\) After the jConsole starts, select Remote Process, and enter the JMX
service URL copied in step 5. Ex:
<service:jmx:rest://localhost:port/IBMJMXConnectorREST> Provide Username
and Password of the administrator-role role user specified in the
server.xml file.

9\) Click Connect. when the connection succeeds, JConsole starts
monitoring you can see the MBeans .

### References

[Connecting to Liberty by using
JMX](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_admin_jmx.html)
[Configuring secure JMX connection to
Liberty](https://www.ibm.com/support/knowledgecenter/en/SSAW57_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html)

## WebSphere Application Server, JMX, and JConsole

The system management functionality of WebSphere Application Server is
based on the use of Java Management Extensions (JMX). Therefore, the
WebSphere Application Server administrative console and "wsadmin"
scripting client use JMX. In addition, the JMX API can be used to
provide custom client programs or contribute custom MBeans. WebSphere
Application Server comes with a set of connectors that can be used to
interact with its JMX infrastructure ([WebSphere Application Server
connectors in the information
center](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/index.jsp?topic=2Fcom.ibm.websphere.base.doc2Finfo2Faes2Fae2Fuagt_rconnector.html)).

While enterprise monitoring solutions will typically provide their own
clients for WebSphere, or provide instructions for using WebSphere
connectors; the focus of this topic is to provide some easy steps you
can take to connect to JConsole and inspect monitoring information. It
is important, however, to take the following points into consideration:

-   The focus of this topic is on WebSphere Application Server versions
    7 and 8.0. JConsole is not supported for these application server
    versions, but some possible configurations based on experience are
    introduced.
-   WebSphere Application Server 8.5 provides a new connector that eases
    connectivity for using JConsole.

### Platform MBean server for connecting with JConsole

This method consists of customizing the server JVM properties with a set
of properties to override the WebSphere Application Server custom MBean
server and force the configuration of platform MBean server. This method
is simple to implement but has a some disadvantages:

-   The configuration is not supported.
-   It is not integrated with WebSphere Application Server security
    infrastructure.
-   WebSphere custom MBeans are not exposed with this configuration.

Complete the following steps for this configuration:

1.  Open the WebSphere administrative console and navigate to this
    location: \*Servers \> Server Types \> WebSphere Application Server
    \> \*

2\. On the server configuration page navigate to this location: **Java
and Process Management \> Process Definition \> Additional Properties \>
Java Virtual Machine**

3\. Add the following entries to the **Generic JVM Arguments** section:

-Djavax.management.builder.initial= -Dcom.sun.management.jmxremote=true
-Dcom.sun.management.jmxremote.port=1099
-Dcom.sun.management.jmxremote.ssl=false
-Dcom.sun.management.jmxremote.authenticate=false

Note there is a space in the "-Djavax.management.builder.initial= "
argument after the equals sign.

4\. Click **OK** and **Save to master configuration** when prompted.

This configuration is only meant for testing purposes. If you launch
JConsole you will be able to connect to your WebSphere server at the
specified port (1099 in this case), without the need to specify
credentials .

### Using JSR160RMI Connector for JConsole

By default, the CLM Server Monitoring will use the default JVM platform
MBean server. On WebSphere using the default JVM MBean server is an
unsupported configuration so an extra flag needs to be supplied as a JVM
initialization parameter to instruct CLM Server Monitoring to use the
WebSphere Mbean Server instead of the JVM one.

Complete the following steps for this configuration:

1.  Open the WebSphere administrative console and navigate to this
    location: \*Servers \> Server Types \> WebSphere Application Server
    \> \*

2\. On the server configuration page navigate to this location: **Java
and Process Management \> Process Definition \> Additional Properties \>
Java Virtual Machine**

3\. Add the following entries to the **Generic JVM Arguments** section:

-Dcom.ibm.team.server.monitoring.mbean.server=WebSphere

4\. Click **OK** and **Save to master configuration** when prompted.

This example shows how to use the WebSphere JSR160RMI connector. Beyond
some basic configuration steps for the connector, connecting with
JConsole will have to take into account that special libraries are
needed to connect to a custom WebSphere JMX MBean server, and that the
connector is integrated with WebSphere security.

The following configuration steps for the connector are needed:

-   **Enable JSR160RMI Connector:** In the WebSphere Application Server
    administrative console, navigate to **Servers \> Server Types \> App
    Servers \> \> Administration \> Administration Services \> JMX
    Connectors**. If the "JSR160RMI Connector" is not enabled, enable it
    and click **OK** and **Save to master configuration** when prompted.

<!-- -->

-   **Check RMI port:** This is the port that will be used for
    connecting with JConsole, so check the value of "BOOTSTRAP_ADDRESS"
    (default is usually 2809), at **Servers \> Server Types \> App
    Servers \> \> Ports**.

The following JConsole scripst that will connect to the JSR160RMI
connector. Note that the script is in Linux format, for Microsoft
Windows adapt it accordingly. An explanation of the main scritpt
elements will follow, so it can be tailored to match your environment:

Windows CMD:

@echo off set WAS_HOME=C:\Program Files\IBM\WebSphere\AppServer set
HOST=clmjts.jazz.net set PORT=2809 set PROTOCOL=rmi set
PROFILE=nodeagent

call "WAS_HOME\profiles\PROFILE\bin\setupCmdLine.bat"

set CLASSPATH="JAVA_HOME\lib\jconsole.jar" set
CLASSPATH=CLASSPATH;"JAVA_HOME\lib\tools.jar" set
CLASSPATH=CLASSPATH;"JAVA_HOME\jre\lib\ibmpkcs.jar" set
CLASSPATH=CLASSPATH;"JAVA_HOME\jre\lib\ext\ibmkeycert.jar" set
CLASSPATH=CLASSPATH;"JAVA_HOME\jre\lib\ext\ibmjceprovider.jar" set
CLASSPATH=CLASSPATH;"WAS_HOME\runtimes\com.ibm.ws.admin.client_8.0.0.jar"
set
CLASSPATH=CLASSPATH;"WAS_HOME\runtimes\com.ibm.ws.ejb.thinclient_8.0.0.jar"
set CLASSPATH=CLASSPATH;"WAS_HOME\runtimes\com.ibm.ws.orb_8.0.0.jar"

"JAVA_HOME\bin\java" -classpath CLASSPATH
-Dcom.ibm.IPC.ConfigURL=[file:"WAS_HOME\profiles\PROFILE/properties/ipc.client.props](file:%22WAS_HOME\profiles\PROFILE/properties/ipc.client.props)"
-Dcom.ibm.CORBA.ConfigURL=[file:"WAS_HOME\profiles\PROFILE/properties/sas.client.props](file:%22WAS_HOME\profiles\PROFILE/properties/sas.client.props)"
-Dcom.ibm.SOAP.ConfigURL=[file:"WAS_HOME\profiles\PROFILE/properties/soap.client.props](file:%22WAS_HOME\profiles\PROFILE/properties/soap.client.props)"
-Dcom.ibm.SSL.ConfigURL=[file:"WAS_HOME\profiles\PROFILE/properties/ssl.client.props](file:%22WAS_HOME\profiles\PROFILE/properties/ssl.client.props)"
sun.tools.jconsole.JConsole
<service:jmx:PROTOCOL://HOST:PORT/jndi/JMXConnector>

Unix BASH:

\#/bin/bash WAS_HOME=/opt/IBM/WebSphere/AppServer HOST=clmjts.jazz.net
PORT=2809 PROTOCOL=rmi PROFILE=nodeagent

. \$WAS_HOME/profiles/\$PROFILE/bin/setupCmdLine.sh

CLASSPATH=\$JAVA_HOME/lib/jconsole.jar
CLASSPATH=\$CLASSPATH:\$JAVA_HOME/jre/lib/ibmpkcs.jar
CLASSPATH=\$CLASSPATH:\$JAVA_HOME/jre/lib/ext/ibmkeycert.jar
CLASSPATH=\$CLASSPATH:\$JAVA_HOME/jre/lib/ext/ibmjceprovider.jar
CLASSPATH=\$CLASSPATH:\$WAS_HOME/runtimes/com.ibm.ws.admin.client_8.0.0.jar
CLASSPATH=\$CLASSPATH:\$WAS_HOME/runtimes/com.ibm.ws.ejb.thinclient_8.0.0.jar
CLASSPATH=\$CLASSPATH:\$WAS_HOME/runtimes/com.ibm.ws.orb_8.0.0.jar
CLASSPATH=\$CLASSPATH:\$WAS_HOME/plugins/javax.j2ee.management.jar

\$JAVA_HOME/bin/java \\ -classpath \$CLASSPATH \\ \$CLIENTSAS
\$CLIENTSSL \\ \$CLIENTSOAP \\ \$CLIENTIPC \\
sun.tools.jconsole.JConsole \\
<service:jmx:$PROTOCOL://$HOST:$PORT/jndi/JMXConnector>

From the script you can configure. (Take note of the values configured
here for future reference and configuration):

-   `WAS_HOME`: The base directory of the WebSphere installation
-   `HOST`: The host to connect to (where WebSphere is installed)
-   `PORT`: The port to connect (eg. 2809)
-   `PROTOCOL`: The protocol to use (eg. rmi)
-   `PROFILE`: The Websphere profile being used by the WebSphere server
    being monitored

This configuration works for WebSphere Application Server versions 7,
8.0, and 8.5

The scripts will run and may prompt for a WebSphere username/password
(depending on your WebSphere authentication.) You can use the WebSphere
administrator.

### Interacting with the WebSphere JMX API and scripting

Beyond the introduced possible configurations for connecting with
JConsole, you can also build a custom application using JMX API to
retrieve information from MBeans. You can check the following
information center topics:

-   [Developing an administrative client
    program](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/index.jsp?topic=2Fcom.ibm.websphere.base.doc2Finfo2Faes2Fae2Ftjmx_develop.html)
-   [Developing a Java Management Extensions client program using Java
    Management Extensions Remote application programming
    interface](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/index.jsp?topic=2Fcom.ibm.websphere.base.doc2Finfo2Faes2Fae2Ftjmx_develop_jsr160.html)

## What you can glean from monitoring with JConsole

First, this is not a tool that will provide you with historical data.
This is a tool to see how your system is running and over the time that
JConsole is running. For detailed information on how to use this
console, see the guides provided by the web server application vendor.
The main theme of this page is to show how to set up the monitoring.

So, what can you now see? At a glance, via the Overview tab, you can
see:

1.  Threads b. Heap memory usage c. CPU usage d. Classes

There is also a VM Summary tab that provides you and any troubleshooter,
such as Rational Client Support, a host of valuable information about
your setup.

## Setting up your Jazz Team Server on Apache Tomcat to use JMX

Note: Apache Tomcat is not a supported webserver since ELM 7.0, see
[System Requirements for
7.0](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=BD41C8E05A1C11E982882C5D069DA07A&osPlatforms=Windows&duComponentIds=D004|D002|D001|D003|S005|S006&mandatoryCapIds=30|9|24|35|13|132|42|19|16|26|40&optionalCapIds=133|66|135|7|5|1|242|187|74|19|137|27|4&_ga=2.71870102.40607982.1613982689-167280282.1607089627&cm_mc_uid=99877615785715740976049&cm_mc_sid_50200000=99671021614099257351#prereqs-0).
The following information is intended for ELM 6.x customers, or those
who chose to continue with Tomcat in 7.x, but are not entitled to
support on questions relating to the webserver.

Activating JMX is achieved by setting a set of Java system properties
for the Apache Tomcat server JVM. These can be appended in your
`CLMAPPHOME/server/server.startup` script using the "JAVA_OPTS"
notation, as other options you find in the script. The following list
provides a set of commonly used configuration options. You can find a
complete set of available properties for JMX configuration on [J2SE 5.0
JMX](http://docs.oracle.com/javase/1.5.0/docs/guide/management/agent.html#properties)
and [J2SE 6.0
JMX](http://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html).

There is also additional information regarding JMX and the parameters
that can be set within [Monitoring and managing Apache
Tomcat](http://tomcat.apache.org/tomcat-7.0-doc/monitoring.html)

### Option 1: JMX not secured

The following properties would activate JMX on Apache Tomcat with no
authentication. You could, therefore, connect to the server's JMX
interface at the port specified by the option
`com.sun.management.jmxremote.port`, without providing any type of
credentials. This is something you won't set up in your production
environments, but it's a good starting point if you want to look at the
type of information that is exposed with JMX in a test or local
environment.

Linux:

\# for JMX monitoring JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote=true" JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote.port=1099" JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote.ssl=false" JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote.authenticate=false"

Microsoft Windows:

rem for JMX monitoring set JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote=true set JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote.port=1099 set JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote.ssl=false set JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote.authenticate=false

Note that in this option `com.sun.management.jmxremote.authenticate` and
`com.sun.management.jmxremote.ssl` properties are set to "false". The
following examples will show options for securing the JMX server using
that properties.

**Connecting with JConsole:** No special parameters need to be used for
JConsole, as no security is configured. You can simply run JConsole and
connect to <service:jmx:rmi:///jndi/rmi://:1099/jmxrmi>

### Option 2: JMX with client authentication - No SSL

In this case, the example will show the properties needed to require
client authentication based on a user ID and password, without SSL. The
first important property to modify from the previous example is
`com.sun.management.jmxremote.authenticate`, now setting it to "true"
(which is the default value). The authentication is managed by two
additional properties and configuration files:

-   com.sun.management.jmxremote.access.file: This property specifies
    the location of the file that contains the information about access
    user roles and associated permissions.
-   com.sun.management.jmxremote.password.file: This property specifies
    the location of the file that contains the passwords for each role.

Sample files are located in the `CLMAPPHOME/server/jre/lib/management`
folder, called `jmxremote.access` and `jmxremote.password.template`. An
easy approach would be to perform the following steps:

1.  Make a copy of the files.
2.  Modify the copy to fit your needs.
3.  (**Mandatory for the configuration to work**) Change permissions to
    files so that only the Apache Tomcat server user is allowed to see
    its contents.

Following is an example of the JMX properties and sample files. You can
use them as guidelines but check the official documentation to fine tune
permissions:

Linux:

\# for JMX monitoring JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote=true" JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote.port=1099" JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote.ssl=false" JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote.authenticate=true" JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote.access.file=/jmxremote.access"
JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote.password.file=/jmxremote.password"

Microsoft Windows:

rem for JMX monitoring set JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote=true set JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote.port=1099 set JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote.ssl=false set JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote.authenticate=true set JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote.access.file=\jmxremote.access set
JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote.password.file=\jmxremote.password

Sample `jmxremote.access` file defining two user roles:
`monitorRoleUser`, which will have just read permissions to MBeans
information; and `controlRoleUser`, which will have read-write
permissions as well as the option to create some MBeans objects:

monitorRoleUser readonly controlRoleUser readwrite \\ create
javax.management.monitor.**,javax.management.timer.** \\ unregister

Sample `jmxremote.password` file with the passwords that each user role
will have:

monitorRoleUser pass1 controlRoleUser pass2

\#AuthConnect **Connecting with JConsole:** With this configuration,
connecting by using JMX requires you to specify one of these
`monitorRoleUser` or `controlRoleUser` users with its password in
JConsole. You can launch JConsole with "jconsole
<service:jmx:rmi:///jndi/rmi://:1099/jmxrmi> and then specify the user
ID and password in the tool UI.

### Option 3: JMX with SSL

The following information describes how to enable SSL in JMX for Apache
Tomcat. There are, however, different degrees of securing with SSL that
you can use:

1.  **Securing server communication to use SSL:** This is default
    configuration that in previous examples was overridden by setting
    `com.sun.management.jmxremote.ssl=false`. This first option will
    secure communications via SSL by using a server certificate.
2.  **JMX RMI registry SSL secured:** Starting with **JDK 6**, an
    additional parameter was added to force the creation of an
    SSL-secured RMI registry as well.
3.  **Set up client SSL authentication:** The method enables client-side
    SSL-based authentication.

For a full SSL secured scenario you will implement all three options.
The examples will cover a phased approach showing which additional
parameters and steps are required in each case:

#### JMX with SSL for the server

For this configuration to work, the Apache Tomcat server must already be
configured to use SSL. The Apache Tomcat server bundled with the Jazz
applications already has SSL configured with a self-signed certificate,
so this example shows how to use this existing configuration from your
deployment for the JMX Tomcat interface (note that same steps would be
applicable if you have modified the default self-signed certificate with
your own).

First, you must identify the SSL configuration in Apache Tomcat to use
it for JMX; so you must look at the `server.xml` Apache Tomcat
configuration file that is located in `CLMAPPHOME/server/tomcat/conf`.
The following sample shows a standard CLM deployment `server.xml` file:

From that configuration file, important parameters to use are the
`keystoreFile` and `keystorePass`. Putting it all together, you can
modify the `server.startup` script as follows to enable SSL with the
certificates from the server:

Linux:

\# for JMX monitoring JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote=true" JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote.port=1099" JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote.ssl=true" JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote.authenticate=false"
JAVA_OPTS="\$JAVA_OPTS
-Dcom.sun.management.jmxremote.ssl.need.client.auth=false"
JAVA_OPTS="\$JAVA_OPTS -Djavax.net.ssl.keyStorePassword=ibm-team"
JAVA_OPTS="\$JAVA_OPTS
-Djavax.net.ssl.keyStore=tomcat/ibm-team-ssl.keystore"

Microsoft Windows:

rem for JMX monitoring set JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote=true set JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote.port=1099 set JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote.ssl=true set JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote.authenticate=false set
JAVA_OPTS=JAVA_OPTS
-Dcom.sun.management.jmxremote.ssl.need.client.auth=false set
JAVA_OPTS=JAVA_OPTS -Djavax.net.ssl.keyStorePassword=ibm-team set
JAVA_OPTS=JAVA_OPTS
-Djavax.net.ssl.keyStore=tomcat/ibm-team-ssl.keystore

\#SslConnect **Connecting with JConsole:** The JConsole client will need
to import the certificate from the server and use it for the connection
to take place. The following information describes how to use `keytool`
to perform these steps. You can use alternative tools to accomplish the
same tasks, so adjust the instructions if you use a different tool.

-   Export the certificate: From `CLMAPPHOME/server/tomcat`, you can run
    the following command to generate a file with the export of the
    public certificate (in the example called "jazz.cer"):

keytool -export -alias ibm-team -keystore ibm-team-ssl.keystore -file
jazz.cer -storepass ibm-team

-   Copy the generated "jazz.cer" file to your preferred location.
-   Generate a trust store and import the certificate to be used by
    JConsole: For simplicity, the example uses "jconsole.truststore" and
    "password".

keytool -import -alias jconsole -file jazz.cer -keystore
jconsole.truststore -storepass password -noprompt

-   Specify the "truststore" and "password" parameters when launching
    JConsole:

jconsole -J-Djavax.net.ssl.trustStore=jconsole.truststore
-J-Djavax.net.ssl.trustStorePassword=ibm-team
<service:jmx:rmi:///jndi/rmi://:1099/jmxrmi>

#### JMX RMI registry SSL secured

You can enable this option by adding the following property to the set
discussed for enabling SSL for the server:

Linux:

JAVA_OPTS="\$JAVA_OPTS -Dcom.sun.management.jmxremote.registry.ssl=true"

Windows:

set JAVA_OPTS=JAVA_OPTS -Dcom.sun.management.jmxremote.registry.ssl=true

The rest of the SSL configuration parameters remain the same. This will
make the VM create an SSL-secured RMI registry at startup to use by the
clients.

\#SslConnect2 **Connecting with JConsole:** You would use the same
configuration and parameters as discussed in "JMX with SSL for the
server" subtopic.

Note that from this point, a full SSL-secured solution requires that you
also activate client-level SSL authentication, which is discussed in the
next example.

#### Set up client SSL authentication

Client authentication for JMX can be configured to be SSL-certificate
based. The example shows how to configure JConsole this way, but similar
steps are required for any other client to be configured this way. As a
guideline, the general steps for this configuration are as follows:

1.  Create SSL key stores and trust stores for the client and server.
2.  Export certificates on each side.
3.  Exchange and import the certificates at the server and client level.

The bundled Apache Tomcat server has a key store, and previous steps
have demonstrated how to export the certificate and import it in the
client. The following examples will show the rest of configuration steps
needed for implementing client authentication for JConsole. Sample
values and self-signed certificates are used in the examples for
clarity; you should adjust them to your environment policies:

\* Create key store for JConsole: First, you must create a key store for
the client.

keytool -genkey -alias jconsole -keyalg RSA -validity 365 -keystore
jconsole.keystore -storepass password -keypass password

-   Export the certificate from JConsole client: Export the public
    certificate.

keytool -export -alias jconsole -keystore jconsole.keystore -file
client.cer -storepass password

-   Import into the Apache Tomcat trust store: The following command
    will generate a new trust store.

keytool -import -alias jconsole-ibm-team -file client.cer -keystore
ibm-team-ssl.truststore -storepass ibm-team -noprompt

-   Configure the server with the trust store: Add relevant properties
    to `server.startup` (Linux example), in addition to the ones for
    previous SSL configurations.

JAVA_OPTS="\$JAVA_OPTS
-Djavax.net.ssl.trustStore=/ibm-team-ssl.truststore"
JAVA_OPTS="\$JAVA_OPTS -Djavax.net.ssl.trustStorePassword=ibm-team"

-   Connect to the server by using the new configuration: The following
    sample JConsole call uses these new assets. The authentication will
    be based on certificates exchange.

jconsole -J-Djavax.net.ssl.trustStore=jconsole.truststore
-J-Djavax.net.ssl.trustStorePassword=ibm-team
-J-Djavax.net.ssl.keyStore=jconsole.keystore
-J-Djavax.net.ssl.keyStorePassword=password
<service:jmx:rmi:///jndi/rmi://:1099/jmxrmi>

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [Monitoring your Rational solution for Collaborative Lifecycle
    Management servers in your
    environment](https://jazz.net/library/article/1017/)
-   [Using
    JConsole](http://docs.oracle.com/javase/7/docs/technotes/guides/management/jconsole.html)

##### Additional contributors: Main.ShubjitNaik, Main.BorisKuschel [additional-contributors-main.shubjitnaik-main.boriskuschel]

META:TOPICMOVED{by="sbeard" date="1371560380"
from="Deployment.JmxMonitoring"
to="Deployment.JazzMonitoringThroughJMX"}
