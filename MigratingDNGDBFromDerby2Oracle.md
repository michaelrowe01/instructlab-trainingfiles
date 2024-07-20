META:TOPICINFO{author="natarajan_2ethirumeni" date="1704360983"
format="1.1" version="1.4"}
META:TOPICPARENT{name="DeploymentMigratingAndEvolving"}

# ELM - Migrating Derby to Oracle database DKGRAY Authors: Main.Natarajan Thirumeni Build basis: Engineering Lifecycle Management 7.0.2 [elm---migrating-derby-to-oracle-database-dkgray-authors-main.natarajan-thirumeni-build-basis-engineering-lifecycle-management-7.0.2]

ENDCOLOR

TOC{title="Page contents"}

This wiki talks about moving a Derby Database to Oracle of DNG
application. In theory, same process is applicable moving a JTS / CCM /
RQM databases from Derby to Oracle.

**The steps outlined here is for IBM support personal use. Even if
you're an expert in CLM & DB export / import , is still highly
recommended to touch base IBM ELM support team prior to run through
these steps**

-   You must have administrative privileges on the database server.

<!-- -->

-   A supported version of a database that you are moving to must be
    installed.

<!-- -->

-   Use the repotools -export and -import commands only to change
    database vendors; for example, by changing from Derby to Oracle. The
    repotool command are available out of box to export and import
    database.

<!-- -->

-   The DB migration is feasible if DB content is relatively smaller in
    size. If the size of the DB is large, the export / import could take
    longer. Please, check with IBM ELM Support team if you have a
    question related to DB sizes.

<!-- -->

-   The out of the box repotool command may not work well if the server
    is renamed (that is, PUBLIC URI of the server renamed from abc to
    xyz). On that case, check with IBM ELM support team for an
    alternative approach.

<!-- -->

-   The DB migration includes:
    -   Setting an Oracle DB for DNG application,
    -   Exporting Derby DB ,
    -   Preparing teamserver.properties for import to work
    -   Finally validation.

## DB migration - Setting an Oracle DB for DNG application

Before running a import, you must ensure Oracle table space for DNG is
created. It means, you'd create a table space in Oracle not tables. My
example is based on Oracle on Windows and this can be replaced as per
your DB environment.

RM and RM_TEMP tablespace (you can call it different name as per set
your company) must be created. And the followed by create DB user,
RM_DB_USER and a password (in my case it was set to DNGonOracle1). And
grant permission (last line SQL statement see below)

-   Note: The steps outlined in thewiki are based on older versions of
    CLM, and this is still good for ELM v702 and above.

CREATE BIGFILE TABLESPACE RM DATAFILE
'C:\app\Administrator\virtual\oradata\VISION1\RM.DBF' SIZE 1G AUTOEXTEND
ON EXTENT MANAGEMENT LOCAL AUTOALLOCATE;

CREATE TEMPORARY TABLESPACE RM_TEMP TEMPFILE
'C:\app\Administrator\virtual\oradata\VISION1\RM_TEMP.DBF' SIZE 20M
AUTOEXTEND ON EXTENT MANAGEMENT LOCAL UNIFORM SIZE 1M;

CREATE USER RM_DB_USER IDENTIFIED BY DNGonOracle1 DEFAULT TABLESPACE RM
QUOTA UNLIMITED ON RM TEMPORARY TABLESPACE RM_TEMP; GRANT CREATE
PROCEDURE, CREATE SESSION, CREATE TABLE, CREATE VIEW TO RM_DB_USER;

Note : Oracle DB was created based on ELM product documentation at [ELM
Docs](http://https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/t_migrate_dbs.html)

## DB migration - Exporting Derby DB

-   Our aim is move an existing Derby DNG (Doors Next Generation
    application) from Derby to Oracle. The platform was using all ELM
    application, however a user unknowingly left DNG application to use
    Derby Database that was provided out of the box. Our goal to move
    Derby to Oracle.

<!-- -->

-   Prior to migration of Derby, take a back-up of Derby database of
    DNG. Since this a derby DB, you can back-up Derby file system

**High level steps**

1\. Get a count of the number of objects in the DB using
"[https://server:port/context/repodebug/repository/itemCount](https://server:port/context/repodebug/repository/itemCount)"

2\. Save the page in HTML

3\. Stop all ELM application including DNG.

4\. Backup of the Derby DB of DNG

eg: cd to /opt/IBM/JazzTeamServer/server/conf/rm cp derby
derby.ORG.{date}

5\. Run the export command

cd to /opt/IBM/JazzTeamServer/server/conf/rm \$repotools-rm.sh -export
toFile=/tmp/exportRMDB.tar
teamserver.properties=conf/rm/teamserver.properties

The export can take several hours as depends on amount of data it needs
to be exported. You can check the status of the export command in the
export log in the file system. Once the export is completed you will see
a message like this in the export log

2020-09-12 17:57:19,833 Repo Tools 2020-09-12 17:57:19,834
java.version=1.8.0_191 2020-09-12 17:57:19,834
java.runtime.version=8.0.5.25 - pxa6480sr5fp25-20181030_01(SR5 FP25)
2020-09-12 17:57:19,837 Provisioning using
"./conf/rm/provision_profiles". 2020-09-12 17:57:19,862 repotools-rm
-export teamserver.properties=conf/rm/teamserver.properties
toFile=/tmp/exportRM.tar 2020-09-12 17:57:19,863 Global patch active at
/opt/IBM/JazzTeamServer/server/patch/CLM_server_patch_6.0.6.1-iFix003-CALM6061M-I20190718-0352.zip:
"CLM_server_patch_6.0.6.1-CALM6061M-I20190718-0352.zip"

2020-09-12 17:57:19,880 To submit questions about issues, go to the
Jazz.net forum at <https://jazz.net/forum>. To find more information
about a message, see the online product documentation. 2020-09-12
17:57:19,881 CRJAZ1363I Loading the configuration from
"<file:conf/rm/teamserver.properties>". 2020-09-12 17:57:23,337
CRJAZ1778I This server is configured as an application. 2020-09-12
17:57:23,529 CRJAZ1365I The server is attempting to connect to the
following database: "conf/rm/derby/repositoryDB" 2020-09-12 17:57:23,932
CRJAZ1364I The connection to the following database was successful: Db
Product Name: Apache Derby Db Product Version: 10.10.2.0 - (1582446) Db
URL: jdbc:derby:conf/rm/derby/repositoryDB;create=true Jdbc Driver Name:
Apache Derby Embedded JDBC Driver Jdbc Driver Version: 10.10.2.0 -
(1582446) SchemaPrefix:

2020-09-12 17:57:27,369 CRJAZ2558I Setting the local server rename state
to false and the openServerDescriptionServiceTemporarily state to false.
2020-09-12 17:57:27,392 CRJAZ1970I The application is configured with:
Public URI: "<https://>\<\>/rm" Jazz Team Server location:
"<https://>\<\>/jts/" 2020-09-12 17:57:27,511 CRJAZ2523I Setting the
global server rename state to false and the validation state to false.
2020-09-12 17:57:28,858 CRJAZ8190I: The full-text index should point to
an absolute directory, but is currently set to
'conf/rm/indices/artifactindex'. The location of the full-text index
will resolve to
'/opt/IBM/JazzTeamServer/server/conf/rm/indices/artifactindex/\_8GsW0K_MEemqyLEbJf8Kng'.
2020-09-12 17:57:29,913 CRJAZ2105I Checking for a running server...
2020-09-12 17:57:29,966 The user "ADMIN" has logged in to the database
"conf/rm/derby/repositoryDB". 2020-09-12 17:57:29,971 Exporting the data
from the database "conf/rm/derby/repositoryDB" to the file
"/tmp/exportRMDB.tar". 2020-09-12 17:57:29,971 Using encoding "UTF-8"
for TAR file headers. 2020-09-12 17:57:42,273 2020-09-12 17:57:42,275
Exporting all the items present in the repository in offline mode.
2020-09-12 17:57:42,275 2020-09-12 17:57:42,399 Exporting
com.ibm.team.repository/ChangeEvent. 2020-09-12 17:57:42,589 Exported 93
ChangeEvent items in 189 ms. .... ..... ...... 2020-09-12 18:16:45,345
Marker : 1602 items, 1602 item states exported in 684ms. 2020-09-12
18:16:45,345 com.ibm.team.globalconfiguration 2020-09-12 18:16:45,345
UriPair : 10 items, 10 item states exported in 10ms. 2020-09-12
18:16:45,345 GlobalConfiguration : 4 items, 4 item states exported in
6ms. 2020-09-12 18:16:45,345 com.ibm.team.reports 2020-09-12
18:16:45,345 ReportQueryDescriptor : 0 items, 0 item states exported in
0ms. 2020-09-12 18:16:45,345 StorageNode : 293 items, 293 item states
exported in 165ms. 2020-09-12 18:16:45,345 FolderDescriptor : 0 items, 0
item states exported in 0ms. 2020-09-12 18:16:45,345 ReportDescriptor :
0 items, 0 item states exported in 0ms. 2020-09-12 18:16:45,345
2020-09-12 18:16:45,345 Export completed successfully. 2020-09-12
18:16:45,345 The user "ADMIN" has logged out of the database
"conf/rm/derby/repositoryDB".

Please note: Before running a export increase JVM heap size in the
repotools-rm.sh command. Eg (to be added) Ensure, all applications are
down until a import process is completed!

## DB migration : Preparing teamserver.properties for import to run

1\. Make a backup of existing teamserver.properties which contain a DB
connections to Derby

2\. Edit teamserver.properties file, comment out the Derby lines and add
the following (eg)

\#com.ibm.team.repository.db.jdbc.location=conf/rm/derby/repositoryDB
\#com.ibm.team.repository.db.vendor=DERBY
com.ibm.team.repository.db.repoLockId=\_7-DYMK_MEemqyLEbJf8Kng
com.ibm.team.repository.db.timezone=America/New_York
com.ibm.team.repository.db.vendor = ORACLE
com.ibm.team.repository.db.jdbc.location=thin\\RM_DB_USER/{password}@//localhost\\1521/vision1.fyre.ibm.com
com.ibm.team.repository.db.jdbc.password=PWDforRM_DB_USER

3\. Save teamserver.properties file

4\. Run the repotool command import eg

Cd to /opt/IBM/JazzTeamServer/server/conf/rm Run repotools-rm.sh -import
fromFile=/tmp/exportRMDB.tar
teamserver.properties=conf/rm/teamserver.properties

The repotool command will read /tmp/exportRMDB.tar file and will import
into Oracle database. The import command could take longer then an
export because during import we write data into database

2020-09-13 01:50:03,084 Repo Tools 2020-09-13 01:50:03,084
java.version=1.8.0_191 2020-09-13 01:50:03,084
java.runtime.version=8.0.5.25 - pxa6480sr5fp25-20181030_01(SR5 FP25)
2020-09-13 01:50:03,088 Provisioning using
"./conf/rm/provision_profiles". 2020-09-13 01:50:03,103 repotools-rm
-import fromFile=/tmp/exportRMDB.tar
teamserver.properties=conf/rm/teamserver.properties 2020-09-13
01:50:03,105 Global patch active at
/opt/IBM/JazzTeamServer/server/patch/CLM_server_patch_6.0.6.1-iFix003-CALM6061M-I20190718-0352.zip:
"CLM_server_patch_6.0.6.1-CALM6061M-I20190718-0352.zip"

2020-09-13 01:50:03,123 To submit questions about issues, go to the
Jazz.net forum at <https://jazz.net/forum>. To find more information
about a message, see the online product documentation. 2020-09-13
01:50:03,123 CRJAZ1363I Loading the configuration from
"<file:conf/rm/teamserver.properties>". 2020-09-13 01:50:06,189
CRJAZ1778I This server is configured as an application. 2020-09-13
01:50:06,368 CRJAZ1365I The server is attempting to connect to the
following database: "thin:xxxxxxxx@//\<\>:1521/\<\>" 2020-09-13
01:50:06,727 CRJAZ3002I The connection to the following database was
successful: Db Product Name: Oracle Db Product Version: Oracle Database
12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production With the
Partitioning, OLAP, Advanced Analytics and Real Application Testing
options Db URL: jdbc:oracle:thin:xxxxxxxx@//\<\>:1521/\<\> Jdbc Driver
Name: Oracle JDBC driver Jdbc Driver Version: 12.2.0.1.0 SchemaName:
RM_DB_USER

2020-09-13 01:50:07,928 CRJAZ2558I Setting the local server rename state
to false and the openServerDescriptionServiceTemporarily state to false.
2020-09-13 01:50:07,945 CRJAZ1970I The application is configured with:
Public URI: "<https://>\<\>/rm" Jazz Team Server location:
"<https://>\<\>/jts/" 2020-09-13 01:50:08,221 CRJAZ2523I Setting the
global server rename state to false and the validation state to false.
2020-09-13 01:50:08,475 CRJAZ2105I Checking for a running server...
2020-09-13 01:50:08,524 Creating the tables for the database
"thin:xxxxxxxx@//\<\>:1521/\<\>" without indices. 2020-09-13
01:50:26,808 CRJAZ1970I The application is configured with: Public URI:
"<https://>\<\>/rm" Jazz Team Server location: "<https://>\<\>/jts/"
2020-09-13 01:50:27,456 CRJAZ8190I: The full-text index should point to
an absolute directory, but is currently set to
'conf/rm/indices/artifactindex'. The location of the full-text index
will resolve to
'/opt/IBM/JazzTeamServer/server/conf/rm/indices/artifactindex/\_\_bHWQfWEEeqNNc3NAFxjqQ'.
2020-09-13 01:50:28,789 The user "ADMIN" has logged in to the database
"thin:xxxxxxxx@//\<\>:1521/\<\>". 2020-09-13 01:50:28,939 The user
"ADMIN" has logged out of the database "thin:xxxxxxxx@//\<\>:1521/\<\>".
2020-09-13 01:50:28,956 CRJZS5650I Indices directory is
/opt/IBM/JazzTeamServer/server/conf/rm/indices 2020-09-13 01:50:28,957
The database tables were created successfully. 2020-09-13 01:50:29,557
CRJAZ1365I The server is attempting to connect to the following
database: "thin:xxxxxxxx@//\<\>:1521/\<\>" 2020-09-13 01:50:29,595
CRJAZ3002I The connection to the following database was successful: Db
Product Name: Oracle Db Product Version: Oracle Database 12c Enterprise
Edition Release 12.1.0.2.0 - 64bit Production With the Partitioning,
OLAP, Advanced Analytics and Real Application Testing options Db URL:
jdbc:oracle:thin:xxxxxxxx@//\<\>:1521/\<\> Jdbc Driver Name: Oracle JDBC
driver Jdbc Driver Version: 12.2.0.1.0 SchemaName: RM_DB_USER

2020-09-13 01:50:33,410 CRJAZ1970I The application is configured with:
Public URI: "<https://>\<\>/rm" Jazz Team Server location:
"<https://>\<\>/jts/" 2020-09-13 01:50:34,569 The user "ADMIN" has
logged in to the database "thin:xxxxxxxx@//\<\>:1521/\<\>". 2020-09-13
01:50:34,569 Importing the data from the file "/tmp/exportRM.tar" into
the database "thin:xxxxxxxx@//\<\>:1521/\<\>". 2020-09-13 01:50:34,569
Using encoding "UTF-8" for TAR file headers. 2020-09-13 01:50:34,576
Reading the TAR file /tmp/exportRM.tar... 2020-09-13 01:50:35,296
Finished reading the TAR file "/tmp/exportRMDB.tar" in 722 ms.
2020-09-13 01:50:35,297 Using deserializer caching options to improve
migration performance. 2020-09-13 01:50:35,297 Configured to update
database stats every 1800000ms. 2020-09-13 01:50:35,297 Importing
contents from /tmp/exportRMDB.tar into the repository. 2020-09-13
01:50:36,077 Migrating data exported from the following model versions
2020-09-13 01:50:36,077 Namespace URI = com.ibm.team.repository.auth,
Version = 4 ... .... .... .... 2020-09-13 04:18:36,579 Marker : 1602
items, 1602 item states imported. 2020-09-13 04:18:36,579
com.ibm.team.globalconfiguration 2020-09-13 04:18:36,579 UriPair : 10
items, 10 item states imported. 2020-09-13 04:18:36,579
GlobalConfiguration : 4 items, 4 item states imported. 2020-09-13
04:18:36,579 com.ibm.team.reports 2020-09-13 04:18:36,579 StorageNode :
293 items, 293 item states imported. 2020-09-13 04:18:36,579 2020-09-13
04:18:36,579 Migration completed successfully. 2020-09-13 04:18:36,580
The user "ADMIN" has logged out of the database
"thin:xxxxxxxx@//\<\>:1521/\<\>".

## Validation and Release application for usage

Assuming, import log shows all green, its time to bring up all ELM
application. Remember on start up, JTS starts up first and then followed
by all ELM applications. The plain text password that was included in
the import process in teamserver.properties file, will be encrypted on a
server start-up.

Once the RM application is up and running you may want to check RM admin
page to ensure all diagnostic tests are passed including DB connections
to Oracle.

1\. Get a count of the number of objects in the DB
"<https://>\<\>:\<\>/rm/repodebug/repository/itemCount"

2\. Save item count into a html page for validation.

This can be compared with 1:1 mapping from the item count that was taken
out of Derby database. The item must match from Derby to Oracle.

Based on our experience, repotool import process took about 2 hours and
30 minutes, to insert 10GB DNG data into Oracle. This can be different
for each deployment as it depends on a data shape.

As part of validation, we would compare Export / import logs with item
state count page(before and after migration). The log should shows 1:1
mappings across

For example: Change and ChangeSet are identical across export / import
and item states.

2020-09-12 17:57:42,589 Exported 83 ChangeEvent items \<**`===`**
**Exported change event numbers out of repotool export command**
2020-09-13 04:15:42,112 Imported 83 ChangeEvent items
\<=======**Imported change event numbers into database**

2020-09-12 18:01:27,335 Exported 14314 ChangeSet items \<**`===`**
**ChangeSet numbers of export log out using repotool command**
2020-09-13 04:15:42,112 Imported 14314 ChangeSet items \<**`===`**
**ChangeSet numbers of import log into DB using of repotool command**

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
