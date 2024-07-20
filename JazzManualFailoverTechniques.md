META:TOPICINFO{author="shubjit" date="1701963398" format="1.1"
reprev="1.12" version="1.12"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Understanding how to install manual failover techniques with the Jazz solution [understanding-how-to-install-manual-failover-techniques-with-the-jazz-solution]

DKGRAY Authors: Main.MichaelAfshar Build basis: Jazz applications in CLM
version 4.0, SSE version 4.0, and ELM version 7.0 or later with
WebSphere Application Server 7 or later ENDCOLOR

TOC{title="Page contents"}

`Note: Support removed for IBM !WebSphere Application Server (Traditional WAS) with ELM version 7.0.3. Use !WebSphere Liberty, either embedded and installed with ELM applications, or separately installed`

Deploy each of the jts.war, ccm.war, rm.war (cold standby only), and
qm.war on their respective Primary and Backup servers so that you can
use idle standby as a strategy for failover in high availability
environments.

The following table lists the abbreviations that are used throughout
these deployment instructions:

Table 1. Acronyms

Acronym Term

URI Uniform Resource Identifier

JTS Jazz Team Server

CCM Change and Configuration Management

QM Quality Management

RM Requirements Management

LPA Lifecycle Project Administration

CLM Rational solution for Collaborative Lifecycle Management (CLM),
which includes JTS, the CCM application, the QM application, and the RM
application

ELM IBM solution for Engineering Lifecycle Management (ELM), which
includes JTS, the CCM application, the QM application, and the RM
application. CLM was renamed to ELM beginning with release 7.0

## Requirements

The following table lists the basic high availability requirements:

**Note:** To configure high availability in a fully distributed
environment for all ELM applications, you need 8 application servers.

Table 2. Basic high availability requirements

Server Software Operating system

IBM HTTP Server

IBM HTTP Server 7.0 Fix Pack 18 or greater Web server plug-ins for
WebSphere Application Server 7.0 Fix Pack 23 or 8.0.0.3 IBM Key
Management v7.0.3.28

Windows, Linux, AIX

WebSphere Application Server Primary Server A

WebSphere Application Server 7.0 Fix Pack 23 or 8.0.0.3 IBM solution for
ELM products (JTS and the CCM, QM, and RM applications)

Windows, Linux, AIX

WebSphere Application Server Backup Server B

WebSphere Application Server 7.0 Fix Pack 23 or 8.0.0.3 IBM solution for
ELM products (JTS and the CCM, QM, and RM applications)

Windows, Linux, AIX

File Server, Shared Disk Lucene Index: file-based indexes used by the
applications Windows, Linux, AIX

## Limitations

The following is a list of known issues in the active CCM backup server:

-   The Jazz Build Engines will not run the scheduled builds, but can
    only run those explicitly requested builds.
-   The Rational Build Forge Build Engines will not run the scheduled or
    requested builds.
-   Due to the issue with the Rational Build Forge Build Engines, the
    Dependency Based Builds will not work while using the CCM standby.
-   Rational ClearQuest Synchronizer will not automatically synchronize
    the outgoing change requests.

## Setting up servers for a basic high-availability configuration

The following sections describe setting up and configuring your primary
and backup servers for a basic high-availability environment.

### Installing and configuring the IBM HTTP Server and Web server plug-ins

**Note:** If you use the Developer for Workgroups client access license,
high availability is not supported.

To install and configure the IBM HTTP Server and Web server plug-ins,
see these resources:

1.  Installing the IBM HTTP Server:
    -   For WebSphere Application Server 7, see [IBM HTTP Server,
        Version
        7](http://pic.dhe.ibm.com/infocenter/wasinfo/v7r0/index.jsp?topic=/com.ibm.websphere.ihs.doc/info/ihs/ihs/welcome_ihs.html)
    -   For WebSphere Application Server 8, see [IBM HTTP Server,
        Version
        8](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/index.jsp?topic=/com.ibm.websphere.ihs.doc/info/ihs/ihs/welcome_ihs.html)
2.  Installing the Web server plug-ins:
    -   For WebSphere Application Server 7, see [Installing web server
        plug-ins](http://pic.dhe.ibm.com/infocenter/wasinfo/v7r0/index.jsp?topic=2Fcom.ibm.websphere.base.doc2Finfo2Faes2Fae2Ftins_webplugins.html)
    -   For WebSphere Application Server 8, see [Installing and
        configuring web server
        plug-ins](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/index.jsp?topic=2Fcom.ibm.websphere.base.doc2Finfo2Faes2Fae2Ftins_webplugins.html)
3.  Configuring a Web server and an application server on separate
    computes remotely:
    -   For WebSphere Application Server 7, see [Setting up a remote Web
        server](http://pic.dhe.ibm.com/infocenter/wasinfo/v7r0/index.jsp?topic=/com.ibm.websphere.base.doc/info/aes/ae/tihs_remotesetup.html)
    -   For WebSphere Application Server 8, see [Setting up a remote web
        server](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/index.jsp?topic=/com.ibm.websphere.base.doc/info/aes/ae/tihs_remotesetup.html)
4.  Securing transmissions between the Web server and the client and
    enable SSL on the IBM HTTP Server:
    -   For WebSphere Application Server 7, see [Securing IBM HTTP
        Server](http://pic.dhe.ibm.com/infocenter/wasinfo/v7r0/index.jsp?topic=2Fcom.ibm.websphere.ihs.doc2Finfo2Fihs2Fihs2Fwelc6topsecureihs.html)
    -   For WebSphere Application Server 8, see [Securing IBM HTTP
        Server](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/index.jsp?topic=2Fcom.ibm.websphere.ihs.doc2Finfo2Fihs2Fihs2Ftihs_sectaskov.html)

**Note:** If you plan to replace the self-signed SSL certificates with
those that belong to your organization, see the IBM Documentation
Installing a security certificate.

### Installing and configuring a Jazz application on primary and backup servers

The jts.war, ccm.war, and qm.war applications use the idle standby
environment, while the rm.war and admin.war (Lifecycle Project
Administration) remain in a stopped state on the backup server (cold
standby). Also note that the admin.war (LPA) and jts.war applications
must be installed on the same server. In the event of a failover of the
Jazz Team Server, stop the primary server completely, fail over to the
backup server, and start the admin.war application on the backup server.

To install and configure copies of the IBM solution for Engineering
Lifecycle Management (ELM) applications on the primary and backup
servers, follow these steps.

1.  Install the ELM applications on the primary and backup servers.
2.  Configure WebSphere Application Server and deploy the .WAR files on
    the primary and backup servers.
3.  Run the setup wizard **ONLY** on the primary server. Do not run the
    setup wizard on the backup servers.
4.  Set the public URL to point to the IBM HTTP Server and not the
    application server.
5.  After installing and configuring the primary server, shut it down
    and copy its configuration files into the backup server
    installation.

For information about installing ELM applications, configuring WebSphere
Application Server and deploying .WAR files, see the IBM Documentation
\[<https://www.ibm.com/docs/en/elm/7.0.2?topic=installing-interactive-guides>\]\[Interactive
Installation Guide\]\].

### Configuring high availability for both primary and backup servers

**Note:** Examples in this section are for the jts.war application. You
can use the same procedure for the ccm.war and qm.war applications.

The jts.war application is typically installed with a single application
server as its target. With the introduction of the Web server, the
application container configuration must be modified to allow routing
through the Web server.

To modify the application:

1.  In the WebSphere Console, click the jts.war application link under
    **Enterprise Applications**.
2.  Select **Manage Modules**.
3.  Select the check box for the jts.war application module.
4.  In the list of clusters and servers, choose both the Web server and
    application server, and then click **Apply**.
5.  Click **OK**, and then save the changes.
6.  Restart the jts.war application.

Reconfigure both the primary and backup Jazz Team Server instances to
reference the same location for the full text index. To keep the index
up to date and available to both the primary and back up servers, update
the `com.ibm.team.fulltext.indexLocation` and
`com.ibm.team.jfs.index.root.directory` properties in the
`teamserver.properties` files on both the primary and backup servers to
store the index on a shared drive.

-   This property value is an example of what you can see on Windows:

com.ibm.team.fulltext.indexLocation=I\\/sharedIndexFolder/workitemindex

-   This property setting is an example of what you can see on Linux:

com.ibm.team.fulltext.indexLocation=/net/LinuxHost/sharedIndex/workitemindex

### Turning off asynchronous tasks on the backup server

To avoid any possible data contention between the two running Jazz Team
Servers, asynchronous (or background) tasks must be turned off on the
backup server.

1.  Add the following line to the `teamserver.properties` file on the
    Backup server:

com.ibm.team.repository.scheduler.migration.mode.enabled=true

1.  Restart the jts.war application on the backup server.

**Note:** Ensure that the preceding property is preserved on the backup
server after any updates are applied to the asynchronous task that
changes the configuration file on the primary server.

When asynchronous tasks are turned off, the backup server will not run
the asynchronous tasks. If circumstances dictate that the backup server
is used as the primary server for an extended period of time, this
property should be reset to false to enable the background tasks in the
Advanced Properties. Make sure to set it to true before restarting the
primary server.

### Editing the web server plugin_cfg.xml file for idle standby

Each time a WebSphere Application Server is configured to route requests
through a web server to an application server, the web server
`plugin.xml` file is updated with the connection information for that
application server. At this point, you have partially configured the
`plugin-cfg.xml` file. Replace and then edit the following section of
the `plugin-cfg.xml` file on the Web server to complete the
configuration. This `plugin-cfg.xml` file is located in the
`plugin\config\webserver1` folder of the web server, where webserver1 is
the name that you assigned to the web server in the previous section,
"Installing and configuring the IBM HTTP Server and Web Server
plug-ins".

### URI groups

Depending on the high-availability environment setup and whether you
intend to have a single WebSphere Application Server instance for each
application or one application server for all applications, you must
plan accordingly. The URI groups is a logical grouping of the URIs that
a cluster serves up. For example, if a single WebSphere Application
Server instance per application is used, declare a cluster for each
application. One URI group is applied to a single cluster. A URI
grouping might look like this example:

### Setting up a server cluster

If you set up one WebSphere Application Server instance per application,
a server cluster must be set up to include all servers that serve up
that one application URI. A server cluster for the ELM applications
might look like this example:

\>

### Route element

The route element is where the URI group and server cluster get bound
together. The rout element tells the plug-in which URIs are served up by
which cluster. Using the preceding example, the example route elements
will bind the application URIs to their respective clusters as shown:

### Synchronizing the configuration files for the primary and backup servers

Customized server properties are not automatically synchronized between
the primary and backup servers. In order to ensure that the backup
servers have consistent configuration attributes, all customized
settings must be propagated to the backup servers before they become
active. Periodically backing up from the primary server and restoring
those files to the backup server are sufficient to keep customizable
server properties in sync.

**Note:** If there are any configuration changes that require that you
restart the primary server, then the backup server must also be
restarted to get these changes.

This list includes configuration files (by ELM Application) that might
need to be synchronized between the primary and backup servers. **Note
for versions 7.0.1 SR1 / 7.0.2 SR1 and beyond, replace log4j.properties
references with log4j2.xml.** log4j.properties

-   JTS

JazzInstallDir/server/conf/jts/teamserver.properties
JazzInstallDir/server/conf/jts/log4j.properties

-   CCM

JazzInstallDir/server/conf/ccm/teamserver.properties
JazzInstallDir/server/conf/ccm/log4j.properties

-   QM

JazzInstallDir/server/conf/qm/teamserver.properties
JazzInstallDir/server/conf/qm/log4j.properties
JazzInstallDir/server/conf/qm/integration_config.xml

-   RM

JazzInstallDir/server/conf/rm/log4j.properties
JazzInstallDir/server/conf/rm/fronting.properties
JazzInstallDir/server/conf/rm/friendsconfig.rdf
JazzInstallDir/server/rrcweb/composerweb.properties
JazzInstallDir/server/rrcweb/log4j.properties

-   ADMIN

JazzInstallDir/server/conf/admin/friends.rtf
JazzInstallDir/server/conf/admin/log4j.properties
JazzInstallDir/server/conf/admin/admin.properties

### Verifying the server setup for manual failover ability

To verify the manual failover ability of the WebSphere Application
Server, edit the `plugin-cfg.xml` file on the web server so that on the
PrimaryNode01 \_server1 the LoadBalanceWeight = 0 property is set and on
the BackupNode01_server1 the LoadBalanceWeight = 1 property is set. Save
the `plugin-cfg.xml` file.

1.  With both primary and backup servers online, run the WebSphere
    sample Snoop servlet to get the name of the server that is handling
    the request.
2.  Invoke the Snoop servlet from an HTML browser by going to
    `https://webserver/snoop`.
3.  The requested information displays the host that is serving the
    request as the localhost. In this case the server with the
    LoadBalanceWeight =1 property is displayed.
4.  Try trading the LoadBalanceWeight property between the primary and
    backup servers, and note which server handles the Snoop servlet
    request.

### Detecting failure on the primary server

**Important:** You must ensure that the primary server is completely
stopped before switching over to the failover server. Also be sure that
there are no running processes that are interacting with the database.

To achieve high availability, you must know when the primary server is
down. This knowledge is especially important for this basic
high-availability solution, which does not support automatic failover of
the primary server to the backup server.

The process of detecting a failed server is a critical and
time-sensitive task. Several factors can indicate that a server has
failed, such as network problems, configuration problems, application
overloading, or user error. Whatever solution you choose to detect
server failures, you must ensure that the alert is as rapid as possible.

## Taking the primary servers offline

If your primary servers fail, or if you suspect your server is
experiencing problems and requires maintenance, the first priority is to
redirect clients to a backup server so that client applications work
with as little interruption as possible.

Sometimes, you can fix the failed application server by restarting it.
If you suspect the repair or maintenance of the primary application
server might take more time to fix, then it is best to mark the primary
server as unavailable.

**Important:** You must ensure that the primary server is completely
stopped before switching over to the failover server. Also be sure that
there are no running processes that are interacting with the database on
the primary server.

1.  In the web server `plugin-cfg.xml` file, locate the following line:
    `LoadBalanceWeight ="1" ...`
2.  Change the `LoadBalanceWeight` attribute from 1 to 0.
3.  Save the `plugin-cfg.xml` file.
4.  After the backup servers are started, run the following commands to
    resume the indexer on the backup servers for Jazz Team Server,
    Change and Configuration Management (CCM), and Quality Management
    (QM) applications:

repotools-jts -resumeIndexer
repositoryURL=<https://server.example.com/jts> adminUserId=wasadmin
adminPassword=wasadmin repotools-ccm -resumeIndexer
repositoryURL=<https://server.example.com/ccm> adminUserId=wasadmin
adminPassword=wasadmin repotools-qm -resumeIndexer
repositoryURL=<https://server.example.com/qm> adminUserId=wasadmin
adminPassword=wasadmin When failing over to the Jazz Team Server backup,
start the LPA application from the WebSphere console.

When the `LoadBalanceWeight` property is set to 0, no requests can be
sent to the server even if it becomes available. To restore availability
to the server, change the `LoadBalanceWeight` property setting back to
1.

## Restoring the primary server

To restore the primary server to operation, you must schedule the server
startup, and switch the `LoadBalanceWeight` property attributes so that
you prevent the primary and backup servers from communicating to the
repository at the same time.

During the recovery process, some users might experience a brief
disconnection or delay. However, after the primary server is back up,
the server resumes taking requests from the web server.

1.  Make sure the primary server is turned off.
2.  In the web server `plugin-cfg.xml` file, locate the entry for the
    `PrimaryNode01_server1` property, and change the `LoadBalanceWeight`
    attribute from 0 to 1.
3.  In the web server `plugin-cfg.xml` file, locate the entry for the
    `BackupNode01_server1` property, and change the `LoadBalanceWeight`
    attribute from 1 to 0.
4.  Save the edits to the web server `plugin-cfg.xml` file.
5.  Shut down the backup server before switching back to the primary
    server to prevent concurrent database access or stale cached data in
    the application. After the backup server is turned off, start the
    primary server.
6.  When the primary server is back up and has resumed taking requests,
    you can start the backup server again.

##### Related topics: None [related-topics-none]

##### External links: \* WebSphere Application Server version 7: [external-links-websphere-application-server-version-7]

-   [IBM HTTP
    Server](http://pic.dhe.ibm.com/infocenter/wasinfo/v7r0/index.jsp?topic=/com.ibm.websphere.ihs.doc/info/ihs/ihs/welcome_ihs.html)
-   [Installing web server
    plug-ins](http://pic.dhe.ibm.com/infocenter/wasinfo/v7r0/index.jsp?topic=2Fcom.ibm.websphere.base.doc2Finfo2Faes2Fae2Ftins_webplugins.html)
-   [Setting up a remote Web
    server](http://pic.dhe.ibm.com/infocenter/wasinfo/v7r0/index.jsp?topic=/com.ibm.websphere.base.doc/info/aes/ae/tihs_remotesetup.html)
-   [Securing IBM HTTP
    Server](http://pic.dhe.ibm.com/infocenter/wasinfo/v7r0/index.jsp?topic=2Fcom.ibm.websphere.ihs.doc2Finfo2Fihs2Fihs2Fwelc6topsecureihs.html)

<!-- -->

-   WebSphere Application Server version 8:
    -   [IBM HTTP
        Server](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/index.jsp?topic=/com.ibm.websphere.ihs.doc/info/ihs/ihs/welcome_ihs.html)
    -   [Installing and configuring web server
        plug-ins](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/index.jsp?topic=2Fcom.ibm.websphere.base.doc2Finfo2Faes2Fae2Ftins_webplugins.html)
    -   [Setting up a remote web
        server](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/index.jsp?topic=/com.ibm.websphere.base.doc/info/aes/ae/tihs_remotesetup.html)
    -   [Securing IBM HTTP
        Server](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/index.jsp?topic=2Fcom.ibm.websphere.ihs.doc2Finfo2Fihs2Fihs2Ftihs_sectaskov.html)

##### Additional contributors: Main.StevenBeard [additional-contributors-main.stevenbeard]

META:TOPICMOVED{by="sbeard" date="1396186102"
from="Deployment.ManualFailoverTechniques"
to="Deployment.JazzManualFailoverTechniques"}
