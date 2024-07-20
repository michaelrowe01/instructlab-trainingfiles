# Backing up the Rational solution for Collaborative Lifecycle Management (CLM)

Authors: [Ralph Schoon](Main.RalphSchoon), [Tim Feeney](Main.TimFeeney) 

Build basis: Rational solution for Collaborative Lifecycle Management 2011 - Rational Team Concert, Rational Quality Manager, Rational Requirements Composer 3.0.1.1. This article is also valid for the product versions 4.x and later. [backing-up-the-rational-solution-for-collaborative-lifecycle-management-clm-dkgray-authors-ralph-schoon-tim-feeney-build-basis-rational-solution-for-collaborative-lifecycle-management-2011---rational-team-concert-rational-quality-manager-rational-requirements-composer-3.0.1.1.-this-article-is-also-valid-for-the-product-versions-4.x-and-later.]

In version 5.0 the database storage for the RM application changed. RM
has now its own database and index files that need to be taken care of
in the backup. This has been added to below.

This article has been preliminary updated to include new applications
delivered as part of 6.0 as well as the Liberty application server
replacement of Tomcat.

Please note, in version 7.x the product names have been changed and each
application has been updated to address log4j2. Relevant changes have
been made below.


After you start using the IBM solution for Engineering Lifecycle
Management (ELM), it will contain more and more important data.
Therefore, it is essential to make regular backups of the data to avoid
losing it. The [Rational solution for Collaborative Lifecycle Management
Information Center](https://jazz.net/help-dev/clm/) contains information
on how to [back up the
databases](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.repository.web.admin.doc/topics/t_jfs_backup.html).
To minimize down time, you can increase the reliability of the IBM
solution for ELM by using hardware that provides high reliability.
However, failure can still happen. Since whole development teams depend
on the infrastructure, it is desirable to be able to recover it as
quickly as possible. This article provides specifics about what to
consider when backing up the IBM solution for ELM.

## Deployment topology to back up

For the purposes of this article, assume that the IBM solution for ELM
is deployed in a fully distributed topology.

-   Jazz Team Server is installed on its own server; for example,
    JTS_SERVER.
-   The Change and Configuration Management (CCM) application
    (Engineering Workflow Management) is installed on its own server:
    CCM_SERVER.
-   The Quality Management (QM) application (Engineering Test
    Management) is installed on its own server: QM_SERVER.
-   The Requirements Management (RM) application (Engineering
    Requirements Management DOORS Next) is installed on its own server:
    RM_SERVER.
-   For simplicity, assume that the installation is new and without a
    migration from prior versions. The context roots are /jts, /ccm,
    /rm, /qm.
-   Additional supporting applications such as Global Configuration
    Management, Reporting etc. may be installed. The context roots are
    /am, /gc, /rs and potentially others.
-   The databases are hosted on one or more servers.

As described in [Building products from
applications](https://jazz.net/blog/index.php/2010/08/16/building-products-from-applications/),
the IBM solution for ELM is now built around a central Jazz Team Server
and several applications that share this Jazz Team Server. In this
topic, the following abbreviations are used:

1 Jazz Team Server is referred to as JTS. 1 The Change and Configuration
Management application is referred to as the CCM application. 1 The
Quality Management application is referred to as the QM application. 1
The Requirements Management application is referred to as the RM
application. 1 Additional supporting applications may be installed and
subsumed under SUP. The assumptions above will result in a deployment
topology as shown below. Each application node has an application server
installed and the application is deployed on it. JTS, the CCM
application, and the QM application have their own own database to store
data. The RM application below Version 5.x uses JTS to store its data.
Since version 5.x RM has its own database. In the example topology, the
databases hosted on the database nodes are referred to as JTS_DB, which
are used by JTS and the RM application; CCM_DB, which is used by the CCM
application; and QM_DB, which is used by the QM application.

**Note:** Since 5.0 the RM Application has its own database RM_DB that
needs to be backed up.

Additional ELM applications such as Design Manager and Rhapsody Model
Manager require backup like any other Jazz application, if deployed.

In case a data warehouse such as Rational Reporting for Development
Intelligence or Rational Insight is set up, keep in mind that setting up
a separate backup procedure for its database and configuration data is
also needed.

## Relevant data for backup operations

This section answers the question, "What could happen?" In the topology
described above, you must plan for the following potential failure
scenarios:

1 Loss of one or more database server nodes 1 Loss of one or more
application server nodes The loss of the database server or the
application server node would each require a substitute or replacement.
In the worst case, this could mean reinstalling or reconfiguring a
machine as a replacement. You can minimize downtime also by providing
replacement systems already configured to take over as described in
[setting up a basic high
availability](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.install.doc/topics/t_setting_up_ha.html)
configuration for the application server node. In any case, it is
necessary to have all required data available.

The data needed to restore a complete deployment as described above
consists of:

1 The [databases](#Backing_up_the_databases) with consistent data 1 The
[application configuration data](#Backing_up_the_Jazz_application)
created and maintained during setup and administration 1 The
[application server configuration
data](#Backing_up_the_Jazz_application) for each application server 1
The [JFS index](#Backing_up_the_JFS_index_files) files used by each
application 1 The [Fulltext index](#Backing_up_the_Fulltext_index_fi)
files for the CCM and QM applications 1 Any custom server extensions and
applied patches

## Practicing your backup and restore procedure

A backup procedure is worthless if data is missing, inconsistent,
unreadable, or not working for other reasons. Practice and test your
backup and restore procedure on an [isolated test
infrastructure](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.install.doc/topics/c_upgrade_staging_env.html)
on a regular basis, to be sure that it works.

## Synchronizing server clocks

For normal operations as well as for backup and restore, it is important
that the clocks of your machines that run the IBM solution for ELM are
closely synchronized. The applications that require the synchronization
provide [setting up a connection to a NTP
server](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.install.doc/topics/c_cluster_prerequisites.html)
to monitor the machine clocks in the advanced server properties.

## Backing up the Jazz application configuration files

While installing the products, you choose install directories. For
example, if you installed by using IBM Installation Manager on Linux,
the default server installation directory is `/opt/IBM/JazzTeamServer`.
If you installed on Windows, the default server installation directory
is `C:\Program Files(X86)\IBM\JazzTeamServer`. This installation
directory will be referred to as *server-install-dir* in the following
text. The image below shows a typical folder structure after installing
all applications on Apache Tomcat.

During the setup and configuration of Jazz Team Server and the other
applications, several files are changed either automatically or
manually. Some files that are updated during administration operations
and should therefore be included in a regular backup as well.

In this article, the backup of the Jazz application configuration files
will be represented by the following pseudocode:

`backup APP_CONFIG`

In the pseudocode, *APP*, represents the application node that must be
backed up. In the pseudocode for a specific application, *APP* must be
replaced with the acronym that represents the application, which will be
JTS, CCM, QM, RM or SUP, where SUP stands for the other applications.
This pattern is kept in the article. The pseudocode below would do the
backup for all applications:

backup SUPP_CONFIG backup CCM_CONFIG backup QM_CONFIG backup RM_CONFIG
backup JTS_CONFIG

### Files to include in the Jazz application configuration files backup

All the Jazz application configuration files are stored in one or more
folders underneath the configuration data folder:

server-install-dir/server/conf

The options for backing up the Jazz application configuration files are
a [full backup](#Full_backup) and [selective backup](#Selective_backup).

#### Full backup

You can back up the whole folder structure underneath:

server-install-dir/server/conf

for each application. This option will safely back up all data that
might be necessary to restore the Jazz application configuration. On the
other hand, it backs up more data than is actually needed.

**Note:** By default, the index files for the [JFS
index](#Backing_up_the_JFS_index_files) and the [Fulltext
index](#Backing_up_the_Fulltext_index_fi) are also stored in this
location. If you use a full backup for the folder, make sure that the
backup of the index files is successful or change the server
configuration and place the index files into a location outside of the
`server-install-dir/server/conf` folder. See below for more information.

#### Selective backup

The configuration folder also contains program code which is often not
desired to be included in backups. To be more selective, it is possible
to only include the most important files and folders into the back up.
This can especially exclude all data that is installed with the product.

Each application has its own [configuration
folder](#Configuration_folder). An application can use more than one
folder. The folders must be backed up together.

JTS uses the following folders for JTS and the Lifecycle Project
Application (LPA):

server-install-dir/server/conf/jts server-install-dir/server/conf/admin

The CCM application stores its data in the folder:

server-install-dir/server/conf/ccm

The QM application stores its data in the folder:

server-install-dir/server/conf/qm

The RM application stores its data in the folder:

server-install-dir/server/conf/rm

Each application has its own configuration files as shown below:

For each application, at least back up the following files from the
configuration folder:

teamserver.properties log4j.properties

**Beginning with ELM 7.0.2 SR1 (iFix015) and ELM 7.0.1 SR1 (iFix018)** -
log4j.properties file has been changed to log4j2.xml, on those servers
you should backup the following files from the configuration folder:

teamserver.properties log4j2.xml

In general, back up all files of this format:

\*.properties

Some applications store data in RDF format. Check for files of the
following format and back them up in case there are any:

\*.rdf

Other files created during the installation are typically not modified.
If in doubt, check the modification date and time, and include files
that changed after the installation finished.

### Configuration folder

As mentioned above, if you use this as a general advice for Jazz based
solutions; for example, to back up Design Manager, or for newer versions
of the tool, back up all of the relevant data in all available
configuration folders in:

server-install-dir/server/conf

Like JTS, Design Manager uses more than one configuration folder; in
this particular case, `dm` and `vvc`. Be sure to catch all relevant data
from these folders. Other applications add their own folders here. For
example

1 `am` - Rhapsody Model Manager 1 `dcc` - Data Collection Component 1
`gc` - Global Configuration Management application 1 `ldx` - Link
Indexer; see the documentation about backing up the data 1 `lqe` -
Lifecycle Query Engine; See the documentation about backing up the data
1 `relm` - Engineering Lifecycle Manager 1 `rs` - Jazz Reporting Service

All these applications behave in similar ways and have configuration and
potentially other data such as their own database to back up. JRS also
provides a mechanism to export the custom reports.

Do not add any folders to the server-install-dir/server/conf folder.
Especially do not create copies of the existing folders and store them
in this folder. This will cause issues with your application; for
example, if you run setup again in an upgrade scenario.

#### Backing up custom server extensions

A [full backup](#Full_backup) contains all the required data. If you
deployed any custom server extensions, and do a [selective
backup](#Selective_backup), either back up the corresponding files or at
least have the files available for rapid redeployment. The files that
are needed to deploy custom server extensions are typically stored in
the folder:

server-install-dir/server/conf/APP/provision_profiles

The files that must be backed up are the provision profile `.ini` file
and the corresponding update `site` folder.

#### Backing up the deployed patches

A [full backup](#Full_backup) contains all the required data. If you
deployed any patches, and do a [selective backup](#Selective_backup),
either back up the corresponding files or at least have the files
available for rapid redeployment. See the patch description for the
files that need to be included in a backup.

## Backing up the application server configuration

Back up the application server configuration data for all application
servers, in order to be able to restore it later. How to back up this
data and which data needs to be included in the backup depends on the
application server in use. The application server configuration changes
only due to administrative tasks. It should be sufficient to use an
incremental backup once a day.

Backing up the application server configuration files for the *APP*
application will be be represented below by the following pseudocode:

backup APP_APPSERVER_CONFIG

The following pseudocode shows the steps to back up all application
server configuration files for all nodes:

backup SUPP_APPSERVER_CONFIG backup CCM_APPSERVER_CONFIG backup
QM_APPSERVER_CONFIG backup RM_APPSERVER_CONFIG backup
JTS_APPSERVER_CONFIG

### Tomcat

When installing on Tomcat, the application server configuration data is
in server-install-dir/server/tomcat/conf/. Some of these files are
modified during the setup process and during operation and should be
included in the backup procedure.

The following files are typically modified during the setup and should
be backed up:

server-install-dir/server/tomcat/conf/server.xml
server-install-dir/server/tomcat/conf/web.xml

If you provide a server certificate, include it in your backup. You can
find information about the storage location of the used certificate in
the `server.xml` file. The Connector element contains a keystoreFile
property that contains the file location.

If you edited the application's `web.xml` files; for instance, when
using Tomcat with LDAP, include these files in your backup. The
`web.xml` files to backup are stored in this location:

server-install-dir/server/tomcat/webapps/APP/WEB-INF/web.xml

For example:

server-install-dir/server/tomcat/webapps/jts/WEB-INF/web.xml
server-install-dir/server/tomcat/webapps/ccm/WEB-INF/web.xml

If you are using Tomcat for user authorization, also back up the user
registry file:

server-install-dir/server/tomcat/conf/tomcat-users.xml

### WebSphere Application Server

When using WebSphere Application Server, back up the profile used to
deploy the application. See the [WebSphere Application Server Knowledge
Center](http://www.ibm.com/support/knowledgecenter/SSEQTP/mapfiles/product_welcome_was.html)
for your version of the WebSphere Application Server for more
information. One option is to use the
[manageprofiles](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.installation.base.doc/ae/rxml_manageprofiles.html)
command.

### WebSphere Liberty

As of 6.0, WebSphere Liberty replaced Tomcat as the application server
packaged out of the box with CLM.

When installing on WebSphere Liberty, the application server
configuration data is in these folders
server-install-dir/server/liberty/servers/clm/
server-install-dir/server/liberty/servers/clm/conf/

Some of the files underneath these folders are modified during the setup
process and during operation and should be included in the backup
procedure.

The following files are typically modified during the setup and should
be backed up:

server-install-dir/server/liberty/servers/clm/server.xml
server-install-dir/server/liberty/servers/clm/conf/ldapUserRegistry.xml
server-install-dir/server/liberty/servers/clm/conf/application.xml

If you are using the built in local user authorization, also back up the
user registry file:

server-install-dir/server/liberty/servers/clm/conf/basicUserRegistry.xml

If you provide a server certificate, include it in your backup. You can
find information about the storage location of the used certificate in
the `server.xml` file. The element keyStore contains a location property
that contains the file location. If this shows a file or a relative path
the default location for the file is in

server-install-dir/server/liberty/servers/clm/conf/resources/security/

## Backing up the databases

It is necessary to backup all databases used by the applications. The RM
application since version 5.0 has its own database. In versions before
5.0 RM used the JTS database to store its data and therefore did not
have a separate database to back up. If you use a data warehouse, also
set up a backup procedure for its database.

Backing up the application database for the *APP* application will be be
represented below by the following pseudocode:

backup APP_DB

The pseudocode below represents all steps and the sequence needed to
back up for all databases for all applications:

backup SUP_DBs backup CCM_DB backup QM_DB backup RM_DB backup JTS_DB

### Ensuring a consistent database backup

When backing up a database, make sure that the database backup is
complete and consistent from a transaction perspective. A backup is
consistent if taken offline, while the database is inactive, or when it
is locked for write operations. Some enterprise databases allow
consistent online backups with transaction logging or vendor specific
procedures and tools.

There are several databases to back up and the applications interact.
JTS creates elements in the registered applications. The JTS cannot
create an element if it is already there because the database of the
registered application is ahead of the JTS. To avoid conflicts and
ensure consistency, the databases for all registered applications must
be backed up to a point in time equal or earlier than the JTS database.
In the example topology, this holds for the CCM and the QM databases.
This has an [impact on the database restore
operation](https://jazz.net/library/article/795#Temporal_Database_Consistency_During),
especially for online backups.

### Derby databases

If a Derby database is used, the application server must be shut down to
perform the database backup.

To back up the databases, compress and back up the directory and its
content used by Derby as repository. By default, the directory is called
repositoryDB. The default location for this directory is the `derby`
folder in the configuration folder of each application:

server-install-dir/server/conf/ccm/derby/repositoryDB
server-install-dir/server/conf/qm/derby/repositoryDB
server-install-dir/server/conf/rm/derby/repositoryDB
server-install-dir/server/conf/jts/derby/repositoryDB

Verify the location of your setup by checking the
`com.ibm.team.repository.db.jdbc.location` property in the
`teamserver.properties` file of each application.

### Enterprise databases

See the system requirements on the **Getting Started** tab of the
individual product download page for the supported database management
systems. Also see the [information
center](https://jazz.net/help-dev/clm/) and the
[library](https://jazz.net/library/) for information about how to backup
other databases. For detailed information on how to backup your
database, see the documentation for the database management system you
are using.

In general, the options provided by enterprise database management
systems are:

#### Offline backup

It is always possible to do an offline backup. Before you back up the
database, stop the application server so that no user interaction occurs
during the backup. This ensures the backup is consistent. You can also
consistently back up all other data related to the server while it is
shut down.

#### Online backup

Some database management systems, such as DB2, support online backup.
This can be used to continuously back up the databases. For more details
about DB2 online backup, see [this
article](https://jazz.net/wiki/bin/view/Deployment/OnlineBackupCLMDB2).

If using online backup, you still want to back up the [Jazz application
configuration files](#Backing_up_the_Jazz_application) as well as the
[application server configuration
files](#Backing_up_the_application_serve). You will most likely not be
able to back up and restore the configuration files consistently with
the online backup. However, these files are only changed when
configuring the application server or administrating the capabilities of
the server configuration. Back up these files after performing any of
these tasks. Otherwise you must redo changes that did not make it into
the last backup.

You also must have a consistent backup of the [JFS
index](#Backing_up_the_JFS_index_files) and the [Fulltext
index](#Backing_up_the_Fulltext_index_fi) files. Since version 4.0.5 the
[JFS index](#Backing_up_the_JFS_index_files) provides a capability to
back up the work item index along withe the [JFS
index](#Backing_up_the_JFS_index_files). See [Fulltext
index](#Backing_up_the_Fulltext_index_fi) for considerations, especially
for online backup. For backing up DNG indices, see [Backup and
restoration of Jazz Foundation Service index files for Rational DOORS
Next
Generation](https://jazz.net/wiki/bin/view/Deployment/DngJfsIndexBackup)

If a consistent online backup of the work index is the primary concern,
A complete offline backup is still the preferred option to get a fully
consistent backup of the databases and the other files.

## Backing up the JFS index files

The applications use [JFS index](#Backing_up_the_JFS_index_files) files
for various query and search operations. These files must be backed up.
The [JFS index](#Backing_up_the_JFS_index_files) files can be backed up
independent from the database. See [Query, Search and indexing
technologies in CLM](DeploymentJazzIndicesTechnology) and [Indices
storage and management: Backup, recovery and
recreation](DeploymentJazzIndicesStorage) for more information on the
indexes.

### Ensuring a consistent backup of database and index files

To create a consistent backup of the [JFS
index](#Backing_up_the_JFS_index_files) files and restore from it, back
up the [JFS index](#Backing_up_the_JFS_index_files) files before or
during the backup of the database. The indexing service will re-create
index information for database content not found in the index over time.
Backing up the indexes will be be represented below by the following
pseudocode:

backup APP_JFSINDEXES

In the pseudocode above, *APP* represents the application node that must
backed up. The following code backs up all nodes:

backup CCM_JFSINDEXES backup QM_JFSINDEXES backup RM_JFSINDEXES backup
JTS_JFSINDEXES

**Note:** Up to version 5.0 the RM application did not have its own [JFS
index](#Backing_up_the_JFS_index_files) files and these indexes where
maintained by JTS.

### JFS index file locations

The location of the [JFS index](#Backing_up_the_JFS_index_files) files
can be found in the `teamserver.properties` file for each application as
value of the following properties:

com.ibm.team.jfs.index.root.directory

The location of the index files is, by default, relative to the folder
where the `teamserver.properties` file is located. This should be
changed to an absolute path.

### Backup of the JFS index files in version 3.x products

To avoid a corrupted backup of the [JFS
index](#Backing_up_the_JFS_index_files) files in **3.x products**, stop
the indexing service during the backup period or shut down the server.
Stopping the indexing services can increase the server up time when
running backups. It is necessary to resume the indexing services after
the backup has been performed.

The indexing service can be stopped by using the -suspendIndexer
repotools command:

repotools-APP -suspendIndexer APP_PARAMETER

The indexing service can be restarted by using the -resumeIndexer
repotools command:

repotools-APP -resumeIndexer APP_PARAMETER

In the above pseudocode, repotools-APP needs to be replaced by the
repotools command for the application that is backed up. For example,
`repotools-ccm` for the CCM application. In addition, APP_PARAMETER
represents the required parameters for the command, such as the
repository URL of the server and the login information for an
administrative user. For the syntax and options, see the repotools
command help. As an example for JTS, the command looks like this:

repotools-jts -suspendIndexer
repositoryURL=[https://JTS_SERVER:JTS_SERVER_PORT/jts](https://JTS_SERVER:JTS_SERVER_PORT/jts)
adminUserID=\*\*\***\*** adminPassword=\*\*\***\***

For simplicity, this article uses the pseudocode below to describe the
detailed [JFS index](#Backing_up_the_JFS_index_files) backup for the
*APP* node:

suspendIndexing APP_SERVER backup APP_JFSINDEXES resumeIndexing
APP_SERVER

The following code shows the detailed pseudocode for all nodes:

suspendIndexing CCM_SERVER backup CCM_JFSINDEXES resumeIndexing
CCM_SERVER

suspendIndexing QM_SERVER backup QM_JFSINDEXES resumeIndexing QM_SERVER

suspendIndexing RM_SERVER backup RM_JFSINDEXES resumeIndexing RM_SERVER

suspendIndexing JTS_SERVER backup JTS_JFSINDEXES resumeIndexing
JTS_SERVER

### Backing up the JFS index files in 4.0 - 4.0.4

In version 4.0, a new repotools command was introduced that does the
backup of the [JFS index](#Backing_up_the_JFS_index_files) files for an
application, with the server online.

Backing up the [JFS index](#Backing_up_the_JFS_index_files) in version
4.0. and later is described by using the same pseudocode:

backup APP_JFSINDEXES

Where repotools-APP must be replaced by the repotools command for the
application that is backed up. For example, `repotools-ccm` for the CCM
application. In addition, APP_PARAMETER represents the required
parameters for the command, such as the repository URL of the server and
the login information for an administrative user. For the syntax and
options, see the repotools command help. As an example for JTS, the
command looks like this:

repotools-jts -backupJFSIndexes
repositoryURL=[https://JTS_SERVER:JTS_SERVER_PORT/jts](https://JTS_SERVER:JTS_SERVER_PORT/jts)
adminUserID=\*\*\***\*** adminPassword=\*\*\***\***
toFile=FILELOCATION_AND_NAME

Using this command maintains the consistency of the [JFS
index](#Backing_up_the_JFS_index_files) files and does not require to
stop and restart the indexer.

**Note:** In versions before 4.0.5 the defect [Defect
245648](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=245648)
prevents from suspending indexing the [Fulltext
index](#Backing_up_the_Fulltext_index_fi). In these versions it is
necessary to do a consistent backup of these indexes, while the server
is running.

### Backing up the JFS index files in 4.0.5 and later

Since version 4.0.5 the [JFS index](#Backing_up_the_JFS_index_files)
provides a capability to back up the work item index along with the [JFS
index](#Backing_up_the_JFS_index_files). See [Fulltext
index](#Backing_up_the_Fulltext_index_fi) for considerations, especially
for online backup.

## Backing up the Fulltext index files

Some applications, such as CCM and QM, also use a [Fulltext
index](#Backing_up_the_Fulltext_index_fi) to support various search and
query operations. You must back up the [Fulltext
index](#Backing_up_the_Fulltext_index_fi) files to be able to restore
the applications consistently. The [Fulltext
index](#Backing_up_the_Fulltext_index_fi) cannot be backed up
independent of the database.

Backing up the indexes is represented by the following pseudocode:

backup APP_FULLTEXTINDEX

In the pseudocode above, *APP* represents the application node that
needs to be backed up. The code below backs up all nodes. JTS does not
have a [Fulltext index](#Backing_up_the_Fulltext_index_fi):

backup CCM_FULLTEXTINDEX backup QM_FULLTEXTINDEX

### Ensuring a consistent backup of database and Fulltext index

Beginning with version 4.0.5 the work item index backup is now included
in the back up of the [JFS index](#Backing_up_the_JFS_index_files).

However, the work item index is still built up during work item
operations. If restored from an online backup of the [JFS
index](#Backing_up_the_JFS_index_files), it does not index operations
that are not included in the backup. So other than the rest of the [JFS
index](#Backing_up_the_JFS_index_files) files, the work item index does
not catch up with later changes and will remain inconsistent with later
work item operations. RED Note as of 5.0.1, the fulltext work item index
does catch up with the database similarly to how the JFS indices
catching up. ENDCOLOR

To get a consistent backup of the work item index files a recreation of
the index might still be necessary. If a consistent online backup of the
work index is the primary concern, a complete offline backup should then
be performed in order to get a fully consistent backup of the databases
and the other files.

### Fulltext index file locations

The location of the [Fulltext index](#Backing_up_the_Fulltext_index_fi)
files can be found in the `teamserver.properties` file for each
application as value of the following properties:

com.ibm.team.fulltext.indexLocation

The location of the [Fulltext index](#Backing_up_the_Fulltext_index_fi)
files is, by default a relative path. It will be based on the
application relative runtime location. If your CLM application is
running on Tomcat this will be the same as the application configuration
directory; if your CLM application is running on WebSphere Application
Server, this will be the profile path, for example: //profiles/AppSrv01/

This should be changed to an absolute path.

## Other Considerations

### Export the reports from Report Service

You can export the reports from the report service and also import them
in a different system. This is especially interesting when using backup
and restore as a means to create test systems.

### CCM Cluster

In a CCM clustered configuration backup the database and at least one of
the cluster nodes with the configuration and index data. To restore use
that node as template to create additional nodes.

### Other systems that might need backup

Check your topology to determine if there are additional systems that
need to be backed up such as **Jazz Authorization Server**, **Reverse
Proxies**, **Caching Proxies** and other applications that play a role
in your setup. All these might contain configuration data that could be
important to be backed up.

## Backup scenarios

With all relevant backup operations described above, it is now possible
to look at different scenarios and provide the sequence of backup
operations.

### Offline backup

#### Shutting down and starting up ELM

If you shut down an ELM environment that uses multiple distributed
servers, make sure to

-   Start up JTS first
-   Shutdown JTS last

You can start up and shut down the other applications in any order, if
you make sure the JTS is handled as described above.

#### Offline backup sequence for a single application on a single server

A complete offline backup procedure for one application on a single
server machine would perform the following sequence of activities:

shutdown \${APP}\_SERVER backup \${APP}\_CONFIG backup
\${APP}\_SERVER_CONFIG backup \${APP}\_JFSINDEXES backup
\${APP}\_FULLTEXTINDEX backup \${APP}\_DB startup \${APP}\_SERVER

Offline backup is the easiest, safest option and easiest to implement
option for co-located and distributed topologies.

**Note:** Since version 5.0 The RM application does require backing up
of the index files or the database. In versions before this was done
with the JTS backup

#### Offline backup sequence for the IBM solution for ELM

A full offline backup for all nodes could look like this example:

shutdown CCM_SERVER shutdown QM_SERVER shutdown RM_SERVER shutdown
JTS_SERVER

backup CCM_CONFIG backup QM_CONFIG backup RM_CONFIG backup JTS_CONFIG

backup CCM_SERVER_CONFIG backup QM_SERVER_CONFIG backup RM_SERVER_CONFIG
backup JTS_SERVER_CONFIG

backup CCM_JFSINDEXES backup QM_JFSINDEXES backup RM_JFSINDEXES backup
JTS_JFSINDEXES

backup CCM_FULLTEXTINDEX backup QM_FULLTEXTINDEX

backup CCM_DB backup QM_DB backup RM_DB backup JTS_DB

startup JTS-server startup CCM-server startup QM-server startup
RM-server

In the scenario above the backup of the [JFS
index](#Backing_up_the_JFS_index_files) files assumes suspending the
indexer in 3.x and using the backupJFSIndexes command in 4.x. During
startup in a distributed environment, start JTS first, then start the
other servers.

#### Offline backup with reduced server downtime

The example above has the longest downtime for offline backup scenarios.
There are several options to reduce downtime, dependent on the systems
and infrastructure in use. These include:

-   Backing up the application configuration files while the server is
    up
-   Backing up the application server configuration while the server is
    up
-   Stopping indexing for backing up the [JFS
    index](#Backing_up_the_JFS_index_files) and keeping the server
    operational during the backup
-   Isolating the server from users while backing up the database
-   Online backup of the database

The following example only takes the server offline to backup the
databases and the [Fulltext index](#Backing_up_the_Fulltext_index_fi)
files:

backup CCM_CONFIG backup QM_CONFIG backup RM_CONFIG backup JTS_CONFIG

backup CCM_SERVER_CONFIG backup QM_SERVER_CONFIG backup RM_SERVER_CONFIG
backup JTS_SERVER_CONFIG

backup CCM_JFSINDEXES backup QM_JFSINDEXES backup RM_JFSINDEXES backup
JTS_JFSINDEXES

shutdown CCM-server shutdown QM-server shutdown RM-server shutdown
JTS-server

backup CCM_FULLTEXTINDEX backup QM_FULLTEXTINDEX

backup CCM_DB backup QM_DB backup RM_DB backup JTS_DB

startup JTS-server startup CCM-server startup QM-server startup
RM-server

### Online backup

As of 5.0.1, a continuous online backup is possible which means both the
[JFS index](#Backing_up_the_JFS_index_files) and [Fulltext
index](#Backing_up_the_Fulltext_index_fi) files can be backed up online.
However, for versions prior to 5.0.1, it is necessary to take the server
offline at least to back up the [Fulltext
index](#Backing_up_the_Fulltext_index_fi). In that case, to restore from
an online backup without a consistent backup of the [Fulltext
index](#Backing_up_the_Fulltext_index_fi), you must re-create the
[Fulltext index](#Backing_up_the_Fulltext_index_fi) files from the
restored databases.

## Restoring from a backup

Replace backup by restore in the pseudocode to get a restore strategy.

### Temporal database consistency during a restore

Keep a valid temporal sequence of the database states during backup and
restore. Make sure to restore the databases for all applications
registered to a JTS; for example, the CCM and the QM database, from a
point in time shortly before or equal to the JTS database backup last
transaction. This is especially important for using online backup for
the database, but also holds for offline backup. In offline backups, you
can create a consistent backup if all servers are down at the same time.
This requirement is due to the JTS creating elements in the registered
applications and potential conflicts in case the database of the
registered application is ahead of the JTS database.

When restoring the [JFS index](#Backing_up_the_JFS_index_files) files
from a backup, make sure that the time of the backup of the index files
is from before the application's database backup. If you restore a
backup of the [JFS index](#Backing_up_the_JFS_index_files) files that is
more recent than the backup of the database of that application, error
messages will indicate that the index is ahead of the database. In this
case, you must re-create the index files.

You also must restore a backup of the [Fulltext
index](#Backing_up_the_Fulltext_index_fi) files that is consistent with
the databases or you must re-create the [Fulltext
index](#Backing_up_the_Fulltext_index_fi). A complete restore procedure
will perform the following sequence of activities:

restore CCM_CONFIG restore QM_CONFIG restore RM_CONFIG restore
JTS_CONFIG

restore CCM_SERVER_CONFIG restore QM_SERVER_CONFIG restore
RM_SERVER_CONFIG restore JTS_SERVER_CONFIG

restore CCM_JFSINDEXES restore QM_JFSINDEXES restore RM_JFSINDEXES
restore JTS_JFSINDEXES

restore CCM_FULLTEXTINDEX restore QM_FULLTEXTINDEX

restore CCM_DB restore QM_DB restore RM_DB restore JTS_DB

### Complex scenarios

Since CLM 2011, you can install more than one CCM and QM application on
different servers and run them against a common JTS. In that case, you
must add these additional servers to the backup and perform all backup
steps for each individual server. It is necessary to keep the temporal
consistency for the JTS and all the applications registered to it. If
you use more than one JTS, there is no requirement to keep the temporal
consistency between the different groups of JTS and its registered
applications.

### Summary

This article described the data and steps required to back up a
deployment of the IBM solution for ELM. The article provides several
options for backing up and also provides information about how to back
up more complex Jazz deployments.

## Appendix

### Backing up applications that were upgraded from a release of version 2

In the case of an installation that was upgraded to a version of the 3.0
release, the upgraded applications use the `/jazz` path instead of
`/ccm` or `/qm`. Therefore, all occurrences of these strings in this
article must be replaced with `/jazz`.

### Re-creating the index files

You can re-create the index files from a restored database backup. Be
aware that re-creation of the index files is an expensive operation and
must performed with the server shut down.

#### Recreating the Fulltext index

You can re-create the [Fulltext
index](#Backing_up_the_Fulltext_index_fi) files by using this command:

repotools-APP -rebuildTextIndices

#### Re-creating the JFS index

You can re-create the [JFS index](#Backing_up_the_JFS_index_files) files
by using this command:

repotools-APP -reindex all

### Oracle backups

See [this
technote](https://www-304.ibm.com/support/docview.wss?uid=swg21454793)
about Oracle backup, especially if you intend to use datapump.

There is a known issue with Oracle databases that are restored from a
backup in 3.0.x. For details, see [work item
180771](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=180771).
If this issue occurs, Support can provide a solution.

### Backing up products that were upgraded from a release of version 2

In the case of an installation that was upgraded from a release of
version 2, the context root will be `jazz` instead of `ccm` or `qm`. In
these cases, all occurrences of the context root in the URLs and paths
above must be replaced with `jazz`.

##### Related topics: 
* [Disaster Recovery](DisasterRecovery) [related-topics-disaster-recovery]

##### External links: [external-links]

\* [Transitioning to online backup of CLM databases using IBM
DB2](OnlineBackupCLMDB2) \* [Query, Search and indexing technologies in
CLM](DeploymentJazzIndicesTechnology) \* [Indices storage and
management: Backup, recovery and
recreation](DeploymentJazzIndicesStorage)

##### Additional contributors:
* Main.StevenBeard [additional-contributors-main.stevenbeard]
