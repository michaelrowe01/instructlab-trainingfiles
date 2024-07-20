META:TOPICINFO{author="chevalie" date="1453991193" format="1.1"
reprev="1.3" version="1.3"}
META:TOPICPARENT{name="RTCTroubleshootingBasicsandDataCollection"}

# Enabling the IBM Data Server driver for JDBC and SQLJ DKGRAY Authors: Main.PhillipeChevalier, Main.TWikiUser Build basis: Products, editions, or versions that apply to the content. If no build basis applies to this content, set the build basis to None. [enabling-the-ibm-data-server-driver-for-jdbc-and-sqlj-dkgray-authors-main.phillipechevalier-main.twikiuser-build-basis-products-editions-or-versions-that-apply-to-the-content.-if-no-build-basis-applies-to-this-content-set-the-build-basis-to-none.]

ENDCOLOR

TOC{title="Page contents"}

It is possible that when investigating concerns with JAZZ products
utilizing DB2 that you will be requested to collect IBM Data server
Trace for the db2 JDBC.

The following procedure will guide you to enable a JDBC driver trace on
a Websphere Application Server Profile (Java virtual Machine \[JVM\]).

## Enabling the IBM Data Server Driver for JDBC and SQLJ

**First step please read the details in the following technote**

***Collecting Data: Tracing with the IBM Data Server driver for JDBC and
SQLJ***

<http://www-01.ibm.com/support/docview.wss?uid=swg21196160>

**Create the DB2JccConfiguration.properties in the WebSphere profile's
properties directory \$WAS_HOME/profiles/\$PROF_NAME/properties**

Example
/opt/IBM/WebSphere/AppServer/profiles/CSST01/properties/DB2JccConfiguration.properties

Enter the following entry in the DB2JccConfiguration.properties

Example of DB2JccConfiguration.properties

\[<root@chevalie> properties\]# more DB2JccConfiguration.properties

db2.jcc.traceDirectory=/tmp/jcctrace db2.jcc.traceFile=trace
db2.jcc.traceFileAppend=false db2.jcc.traceLevel=-1

NOTE: This location is already part of the WAS CLASSPATH, and is the
reason why it is selected. Also, make sure you have plenty of room and
that write permission on the targeted path for the
db2.jcc.traceDirectory location is correctly set for the owner of the
JVM processes.

**Setup the Java option for a\enabling the trace on the JVM:**

In this next steps we will be adding a java argument to the Java virtual
Machine properties.

-Ddb2.jcc.propertiesFile=/\$WAS_HOME/profiles/PROF_NAME/properties/DB2JccConfiguration.properties

Example:

Add the this java argument java option to the Generic JVM arguments,
bread crumb trail from the WAS Admin console is Application servers \>
server1 \> Process definition \> Java Virtual Machine

Restart the Application server profile to load the new java argument in
the Generic options

**Once JCC trace is enabled on Jazz product, DB2 server trace has to be
enabled on the DB2 database server**

1.  Turn on the trace: db2trc on -t -f trace.dmp
2.  Recreate the problem on the Jazz application affected by the concern
    being investigated
3.  Stop the db2trace: db2trc off
4.  Stop the JCC trace on the application server: Remove the the
    DB2JccConfiguration.properties from Generic JVM arguments in the
    WebSphere JVM propertiesand, recycle the application server.
5.  Flow the trace: db2trc flw -t trace.dmp trace.flw
6.  Format the trace: db2trc fmt trace.dmp trace.fmt
7.  Format the communications buffers: db2trc fmt trace.dmp trace.fmtc
    -c

**Send trace.flw, trace.fmt, trace.fmtc files and JCC traces back to
your support organization requesting the information for review.**

Please use the following tool to upload to the IBM support organization.

***Enhanced Customer Data Repository(ECuRep)***

<https://www.secure.ecurep.ibm.com/app/upload>

***How to upload and attach file(s)/data to my PMR***

<http://www-01.ibm.com/support/docview.wss?uid=swg21293683>

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]

META:FILEATTACHMENT{name="JVM_GENERIC.JPG" attachment="JVM_GENERIC.JPG"
attr="" comment="" date="1453986426" path="JVM_GENERIC.JPG" size="24536"
user="chevalie" version="1"}
META:FILEATTACHMENT{name="BreadCrumToJVMProp.JPG"
attachment="BreadCrumToJVMProp.JPG" attr="" comment="" date="1453986552"
path="BreadCrumToJVMProp.JPG" size="49979" user="chevalie" version="1"}
