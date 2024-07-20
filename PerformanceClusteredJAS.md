META:TOPICINFO{author="sahilkmansuri" date="1700822297" format="1.1"
version="1.20"}
META:TOPICPARENT{name="PerformanceDatasheetsAndSizingGuidelines"}

# Setting up a cluster of Jazz Authorization Servers DKGRAY Authors: Main.VaughnRokosz, Main.HongyanHuo Build basis: 6.0.2 [setting-up-a-cluster-of-jazz-authorization-servers-dkgray-authors-main.vaughnrokosz-main.hongyanhuo-build-basis-6.0.2]

ENDCOLOR

TOC{title="Page contents"}

This article shows you how to set up a cluster of Jazz Authorization
Servers.

The [Jazz Authorization server](https://jazz.net/library/article/75)
allows for single sign-on across your Jazz applications. Users can log
in once, and then move between Jazz applications like Rational Team
Concert or Rational Quality Manager without being prompted for
credentials.

If you have an active Jazz deployment, you can reduce the risk of
outages by clustering your Jazz Authorization Server. If you only have
one JAS instance, then no one can log in if that instance is down. But
if you have a cluster, login requests can automatically fail over to
other JAS instances.

## An overview of the approach

The diagram below illustrates the approach to clustering. You start by
setting up several Jazz Authorization Servers (JAS), and configuring
each one to use a common LDAP server. You additionally must configure
each JAS to use a common database server (by default, JAS stores
information locally in a Derby database, so for a cluster, you need to
be able to share information between JAS instances via a common database
server). Finally, you set up a network dispatcher to distribute requests
across your JAS instances. In this article, we'll use the IBM HTTP
Server (IHS) as the network dispatcher.

After you've got your JAS cluster running, you can configure your Jazz
servers to use it (although there are some limitations if you have an
existing non-clustered JAS already set up in your environment).

This article focuses on clustering only JAS. You can also set up your
LDAP or database server in high availability mode. Please refer to the
documentation for your specific LDAP or database product if you are
interested in doing that.

## Installing the Jazz Authorization Server

Your first step is to install the Jazz Authorization Server on at least
two separate systems.

You can download the Jazz Authorization Server from jazz.net (release
6.0 and later). You install it using Installation Manager.

Configure each JAS instance to use a [common LDAP server by following
the instructions in the knowledge
center](https://www.ibm.com/support/knowledgecenter/SSCP65_6.0.1/com.ibm.jazz.install.doc/topics/t_jsasso_jas_user_mgmt.html).

After you've completed the installation, move on to the next step:
configuring persistence.

## Configuring persistence for the Jazz Authorization Server

When you first install the Jazz Authorization server, it comes
configured to use a local Derby database for storing information. That
won't work in a clustered environment, since that information won't be
available to all the instances. In order to cluster JAS instances, you
need to set up a database server which can be shared by all JAS
instances. The basic steps are:

-   Create database tables on a database server which all JAS instances
    can access
-   Update the JAS configuration file (appConfig.xml) to use the
    database server

Out of the box, the Authorization Server is bundled with Derby. We do
not support customizations to the embedded derby and it is not
sufficient to use for clustering your application.

The following sections will show how to do that for both Oracle and Db2,
and will provide sample SQL scripts that can create the necessary
tables. But note that you will need to customize these scripts for your
own environment.

You can find some general information on [using Db2 for persistent OAuth
services](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/cwlp_oauth_db2.html)
in the Liberty documentation. However, some of those instructions are
incorrect; we've provided corrections here where needed.

### Note: TokenString Size Specification.

In all the .sql scripts (provided against Db2/Oracle/MS SQL), the size
of the TokenString provided in the Script needs individual assistance.
The reason for this custom requirement, is that the size of the
TokenString, is not just dependent on how many Jazz groups that a user
is a Member. In a corporate LDAP, it would be very difficult to know
what is the maximum number of LDAP groups a user.

More the user associations with different LDAP groups, bigger can be the
size of the TokenString being generated. Hence, we cannot deduce the
optimal size for this column in the script. However, after experiencing
this issue with clients using different Enterprise DB vendors, after
consulting with Liberty development team, we have been able to get to an
understanding, that this size could grow even upto 30K.

If users have, lesser number Group associations, the default limit of
Varchar(2048) might Suffice. But if this association is more, one could
extend the default size by changing upto Varchar(4000) In Oracle.
However, the same type in Db2 could extend upto 20K, and for MS SQL, one
would need the type to be changed to NVARCHAR(MAX).

Different databases have different upper limits for this Attribute type.
Mentioned below are alternatives for each of the DB Vendors, when the
default limit of 2048 becomes insufficient:

**Oracle :** TOKENSTRING CLOB DEFAULT {} NOT NULL

**IBM Db2:** TOKENSTRING VARCHAR(20000) NOT NULL

**MS SQL:** TOKENSTRING NVARCHAR(MAX) NOT NULL

### Oracle

To configure JAS to use Oracle, start by creating the required tables in
your Oracle database. You can use the sample
[createOauthOracle.sql](https://jazz.net/wiki/pub/Deployment/PerformanceClusteredJAS/createOauthOracle.sql)
as a starting point. You will need to customize this sample for your
environment (e.g. your passwords, paths, tablespaces).

createOauthOracle.sql creates two tablespaces: OAUTH and OAUTH_TMP, and
creates the tables in the OAUTH tablespace. If you have an existing
tablespace that you want to use, you can change the "CREATE TABLE"
statements to use your existing tablespace. If you want to create new
tablespaces, then you should edit the DATAFILE and TEMPFILE clauses to
point at the directory that you want to use for the tablespace.

The Jazz Authorization server expects to find a user named
OAUTHDBSCHEMA, and it expects to find tables in a schema named
OAUTHDBSCHEMA. You will need to create the OAUTHDBSCHEMA user in Oracle.
Customize the "CREATE USER" statement to specify a password for the
OAUTHDBSCHEMA user. When you create the OAUTHDBSCHEMA user, you should
also associate that user with the tablespace you plan to use for the
Oauth tables.

After you finish customizing createOauthOracle.sql, you can log into
your Oracle server and run the SQL script from sqlplus:

To start sqlplus: sqlplus '/ as sysdba'

At the sqlplus prompt, run the SQL command by entering:
@createOauthOracle.sql

Note that the SQL for Oracle differs slightly from the SQL for Db2. \*
The Db2 BIGINT data type is replaced with Oracle's NUMBER(19,0) \*
DEFAULT keyword on CLOB fields must come before NOT NULL \* Oracle uses
additional clauses (TABLESPACE OAUTH STORAGE(INITIAL 50K)) for table
creation \* GRANT clauses in Oracle do not use the USER keyword \*
Enabling a Jazz server to use JAS requires that the DISPLAYNAME field
support NULLs (so, NOT NULL keywords removed from that field)

After you create the tables, you must then configure all JAS instances
to use the tables. You do this by creating a data source definition in
the
[appConfig.xml](https://jazz.net/wiki/pub/Deployment/PerformanceClusteredJAS/appConfigOracle.xml)
file (that file will be in the configuration folder on your JAS server).
You can refer to the attached appConfig.xml file for an example. You
will need to customize this to work with your specific Oracle server,
but the section that defines a data source for Oracle is:

Notes:

-   You need to copy the Oracle JBDC driver (ojdbc6.jar) from your
    Oracle server to the lib/global folder on your JAS server. On Unix,
    that folder would be
    /opt/IBM/JazzAuthServer/wlp/usr/shared/config/lib/global, if you
    install JAS using the defaults.
-   In the "dataSource" record,
    -   For "password", using the password you specified when creating
        the OAUTHDBSCHEMA user in Oracle
    -   For databaseName, use the Oracle SID for your database. The
        sample uses the default value assigned by Oracle - ORCL. Your
        value may be different.
    -   Set the portNumber field to the port on which your Oracle
        instance is running. The Oracle default is 1521; your value may
        be different.
    -   For serverName, enter the host name of the Oracle server.

You'll also need to update the "oauthProvider" record in appConfig.xml
so that it specifies the Oracle data source (rather than the default
Derby data source). The "databaseStore" record should specify the name
of the Oracle data source - in this example, "OAUTH2ORA".

client01

### Db2

To configure JAS to use Db2, start by creating the required tables in
your Db2 database. You can use the sample
[createOauthTablesDB2.sql](https://jazz.net/wiki/pub/Deployment/PerformanceClusteredJAS/createOauthTablesDB2.sql)
as a starting point. You will need to customize this sample for your
environment.

The script will create a database called "oauth2db", and then create
tables in the schema "OAuthDBSchema". You can use a different database
name if you wish, but you must use the schema "OAuthDBSchema". The
tables require a buffer pool that has a page size of at least 8K. The
SQL script creates the necessary buffer pool and table spaces - but you
can skip this if your buffer pools use page sizes of 8K or greater
already.

After you create the tables, you must then configure all JAS instances
to use the tables. You do this by creating a data source definition in
the
[appConfig.xml](https://jazz.net/wiki/pub/Deployment/PerformanceClusteredJAS/appConfigDB2.xml)
file (that file will be in the configuration folder on your JAS server).
You can refer to the attached appConfigDB2.xml file for an example. You
will need to customize this to work with your specific Db2 server, but
the section that defines a data source for Db2 is:

Notes:

-   You need to copy the Db2 JBDC drivers (db2jcc4.jar,
    db2jcc_license_cu.jar) from your Db2 server to the lib/global folder
    on your JAS server. On Unix, that folder would be
    /opt/IBM/JazzAuthServer/wlp/usr/shared/config/lib/global, if you
    install JAS using the defaults.
-   In the "dataSource" record,
    -   For "user", provide the name of a Db2 user to be used for
        connecting to the database
    -   For "password", using the password for the Db2 specified above
    -   For databaseName, use the name of the database you created
        previously ("OAUTH2DB" if you used the sample script)
    -   Set the portNumber field to the port on which your Db2 instance
        is running. The default is 50000; your value may be different.
    -   For serverName, enter the host name of the Db2 server.

You'll also need to update the "oauthProvider" record in appConfig.xml
so that it specifies the Db2 data source (rather than the default Derby
data source). The "databaseStore" record should specify the name of the
Db2 data source - in this example, "OAUTH2DBDS".

client01

### Microsoft SQL Server

**Note:** It is applicable up to and including 7.0.2

To configure JAS to use Microsoft SQL Server, start by creating the
required tables in your SQL Server database. You can use the sample
[createOauthMSSQL.sql](https://jazz.net/wiki/pub/Deployment/PerformanceClusteredJAS/createOauthMSSQLv2.sql)
as a starting point. You will need to customize this sample for your
environment.

The script will create a database called "oauth2db", and then create
tables in the schema "OAuthDBSchema". You can use a different database
name if you wish, but you must use the schema "OAuthDBSchema". The
tables require a buffer pool that has a page size of at least 8K. The
SQL script creates the necessary buffer pool and table spaces - but you
can skip this if your buffer pools use page sizes of 8K or greater
already.

client01

You'll also need to update the "oauthProvider" record in appConfig.xml
so that it specifies the MS SQL Server data source (rather than the
default Derby data source). The "databaseStore" record should specify
the name of the SQL Server data source - in this example, "OAUTH2DBDS".

Notes:

-   You need to copy the Microsoft SQL Server JBDC drivers
    (sqljdbc41.jar) from your MS SQL server to the lib/global folder on
    your JAS server. On Unix, that folder would be
    /opt/IBM/JazzAuthServer/wlp/usr/shared/config/lib/global, if you
    install JAS using the defaults.
-   As per MS
    [Documentation](https://technet.microsoft.com/en-us/library/ms186939(v=sql.110).aspx)
    The maximum number of characters allowed by sql server is 4,000 or
    we can use MAX which supports 2GB storage in size.
-   In the "dataSource" record,
    -   For "user", provide the name of a MS SQL Server user to be used
        for connecting to the database
    -   For "password", using the password for the SQL Server specified
        above
    -   For databaseName, use the name of the database you created
        previously ("OAUTH2DB" if you used the sample script)
    -   Set the portNumber field to the port on which your MS SQL Server
        instance is running. The default is 1433; your value may be
        different.
    -   For serverName, enter the host name of the Microsoft SQL Server.

## Setting up dispatching using IBM HTTP Server

The Jazz Authorization Server is really just a Websphere Liberty server.
The method of using IHS with Liberty can be found in the Liberty
Infocenter - see [Configuring a web server plug-in for
Liberty](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_webserver_plugin.html?cp=SSAW57_8.5.5).
You can follow the basic steps there to create a plugin for Liberty
using the Websphere Customization Toolbox (WCT). Once you have a basic
plugin, you can customize it to dispatch traffic across your JAS
instances.

The additional steps involved to get IHS to dispatch traffic across
multiple JAS instances are:

-   Add a clone id value to the server.xml file for each JAS server
-   Modify the "ServerCluster" section in the plug-in.xml file on the
    IHS server, to route traffic to the available JAS servers
-   Configure the SSL truststores and keystores on IHS and the JAS
    instances

### Updating server.xml on each JAS instance

Add a line similar to the following to the server.xml file on each JAS
instance:

Assign each JAS server a different id (e.g. cloneid00001, cloneid00002),
which guarantees that each id is unique in the cluster. This is used by
IHS to implement session affinity.

See the attached
[server.xml](https://jazz.net/wiki/pub/Deployment/PerformanceClusteredJAS/server.xml)
for an example.

### Updating the Websphere plugin for dispatching

Once you've created a basic WebSphere plugin XML file, you can manually
update it to route traffic across your JAS instances. You need to make
the following changes: \* Add "VirtualHost" entries for the JAS SSL and
non-SSL ports (9280 and 9643 if you are using the defaults) \* Modify
the "ServerCluster" entry to group each of your JAS instances together
into a single cluster \* Update the URI group to include the JAS URIs
that the cluster will handle

The attached
[plugin-cfg.xml](https://jazz.net/wiki/pub/Deployment/PerformanceClusteredJAS/plugin-cfg.xml)
file can be used as an template - you'll need to modify this for your
own deployment. In this example, there is a server cluster called
"server1_Cluster", and this routes traffic to two JAS instances - one
called vtrjas2.rtp.raleigh.ibm.com, and one called
vtrjas3.rtp.raleigh.ibm.com). Both JAS instances are configured with the
default ports (9643 for SSL traffic, and 9280 for non-SSL traffic).

The uri group for JAS should look like this:

If you are using the default names for ServerCluster, UriGroup, and
VirtualHostGroup, the route for the cluster should look like this:

The virtual host group would be something like this. The JAS ports
(9643, 9280) must appear here, along with any other ports on which IHS
is listening.

Finally, the server cluster entry would be similar to the entry below.
You'll need to adjust this based on the number of JAS instances you
have, which clone ids you assigned to each instance, and what your JAS
ports are. Make sure the attribute **CloneID** is present for each
**Server** element - its value is the same with the cloneId specified in
the server.xml for each JAS instance accordingly. You may manually add
this attribute or change value for it. Please note that in the sample
code below, we are using a keystore called "ihskeys.kdb" for the
plugins, the creation and configuration of this keystore will be covered
in the section [Configuring SSL keystores for JAS/IHS
communication](#Configuring_SSL_keystores_for_JA).

### Configuring SSL keystores for JAS/IHS communication

To allow the IHS and JAS instances to communicate over SSL, you'll need
to set up trust and key stores on IHS and JAS, and then exchange
certificates. There are several useful references in the documentation:

-   [Configuring security
    certificates](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Ft_jsasso_jas_cli_certif_conf.html)
-   [Installing a security
    certificate](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Ft_jsasso_jas_cli_certif_conf.html)
-   [Enabling SSL communication in
    Liberty](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Ft_jsasso_jas_cli_certif_conf.html)
-   [Liberty - SSL configuration
    attributes](https://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_ssl.html)
-   [Liberty:
    Keystores](https://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_sec_keystores.html)

For our test configuration, we generated new key and trust stores using
self-signed certificates. The steps we followed are below for Linux; you
may need to adjust these slightly if you already have key stores, or if
you want to use a signed certificate, or if you are working on Windows.

**Step 1: Create a new key store for the IHS server**

On the IHS machine, cd to /bin, e.g. /opt/IBM/HTTPServer/bin, and run
the following commands

./gskcmd -keydb -create -db ihskeys.kdb -pw xxxxx -expire 3650 -stash
-type cms ./gskcmd -cert -create -db ihskeys.kdb -label default -expire
3650 -size 2048 -dn "CN=xxxxx" -default_cert yes -pw xxxxx

, where **dn** denotes the Distinguished Name for the IHS server, use a
fully qualified name for CN. For example -dn
"CN=yourhostname.yourdomain.com".

**Step 2: Create key and trust stores on all JAS instances; export the
public key**

The commands below should be executed on each JAS instance in the
cluster. Take a note for the values of **alias**, **keystore**,
**storepass**, and \*storetype\*; these will be applied to the
appConfig.xml configuration file for JAS.

keytool -genkeypair -alias default -keystore jas.p12 -storepass xxxxx
-validity 3650 -keyalg RSA -keysize 2048 -storetype PKCS12 keytool
-export -alias default -keystore jas.p12 -storetype pkcs12 -file
jas1pub.arm -storepass xxxxx keytool -import -alias default -keystore
jastrust.p12 -storepass xxxxx -file jas1pub.arm -storetype PKCS12

Copy the exported key to your IHS server. Use a unique file name in the
-file option on each JAS server. Here, we use a file "jas1pub.arm" for
the JAS instance JAS1.

**Step 3: Add the public key to the IHS key store**

Start the ikeyman tool and open your IHS keystore. Select "Signer
Certificates", and then select "Add..." for each of the JAS public keys
exported in step 2.

**Step 4: Export the IHS certificate**

On your IHS server, start the ikeyman tool. Open your IHS keystore.
Select "Personal certificates", then "Extract Certificate..." ; save the
certificate as "ihscert.arm".

**Step 5: Import the IHS certificate into the JAS key stores**

Copy ihscert.arm (generated in step 4) to each of your JAS instances.
Then, import the certificate into the trust store by running the
following command:

keytool -import -alias ihsdefault -keystore jastrust.p12 -storepass
xxxxx -trustcacerts -file ihscert.arm -storetype PKCS12

**Step 6: Update appConfig.xml on the JAS instances to use the key and
trust stores**

Update appConfig.xml with a section similar to this:

, where serverKayAlias is the value of **alias** you used in Step 2
above. Make sure the location to the keyStores (in the example above,
"jas.p12" and "jastrust.p12") are using absolute directory path, or they
have to exist in the same directory of appConfig.xml.

You can refer to the attached appConfig.xml sample file as well.

After the configurations are completed and servers restarted, the
clustered JAS can be accessed from
[https://your_IHS_server:your_IHS_port/a_uri](https://your_IHS_server:your_IHS_port/a_uri),
for instance you can verify that the JAS server is online via
<https://your_IHS_server/jazzop/form/login>

## Configuring Jazz servers to use a JAS cluster

Once you have configured an IHS to serve as a network dispatcher for JAS
instances, you can configure your Jazz servers to use the JAS cluster.
Use the host name for the IHS server when prompted for the host name of
the JAS server. Jazz servers will then direct login requests to your
IHS, and your IHS will redirect the requests to one of your JAS
instances.

If you are installing a Jazz server for the first time and you have
already set up your JAS cluster, you should select the option "Enable
Jazz Security Architecture SSO" in Installation Manager.

Then, when running Jazz setup, you'll be prompted to enter the host name
for the Jazz Authorization Server. Enter the name of your IHS server
here.

If you have an existing Jazz server that is not already JAS-enabled, you
can [follow the steps in the
Infocenter](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.2/com.ibm.jazz.install.doc/topics/r_repotools_migrateToJsaSso.html)
to enable it.

## Scalability and high availability testing

We tested a clustered JAS system to understand its scalability limits.
We used a single IBM HTTP Server with two Jazz Authorization servers,
and used a DB2 server to store the JAS configuration databases. The IHS
and JAS servers were virtual machines running Linux Red hat 6, and each
system had 4 virtual CPUs and 8G of RAM. The database server was a
physical system with 24 logical processors and 32G of RAM. We had basic
tuning done on the IHS server.

This cluster was able to process 220 logins per second. This is roughly
equivalent to a user population of 200,000 logging in over 15 minutes.
This is an extreme simulation of what might happen if everyone in an
organization arrived at work at around the same time, and logged into
their Jazz systems immediately. The JAS cluster can easily handle this
extreme load, and in fact, the limit we found was due to a configuration
error on one of the JAS instances (we had not increased the ulimit
settings for open files).

We also ran a failover simulation at scale. We placed the JAS cluster
under constant login load, and then took down one of the JAS instances.
As expected, IHS detected the failure and routed traffic to the other
JAS node. There was one brief failure in the client simulation at this
point - there was a login operation in progress when the JAS instance
was shut down, and this interrupted operation resulted in an HTTP 500
error at the client. But the workload immediately recovered. When the
failed JAS system was brought back up, IHS detected this and began to
route traffic across both JAS instances.

## Limitations

The approach described in this article applies only when setting up a
new Jazz Authorization server. If you have already set up a Jazz
Authorization server and you've set up a Jazz deployment to use it, you
can't create a cluster.

There are two reasons for this:

-   If you have an existing Jazz Authorization Server, it will most
    likely have been configured to use the default Derby database. You
    can't easily transfer the configuration data to a shared database
    server. JAS clustering requires a way to share configuration data
    amongst cluster nodes.
-   Once you have configured a Jazz deployment to use a particular Jazz
    Authorization Server, you can't change it to use a new Jazz
    Authorization Server. So, you are not able to set up a new JAS
    cluster and reconfigure your existing Jazz deployment.

## Tuning

There are a few tuning options available for the Jazz Authorization
server. These may be useful if you see poor login performance in the CLM
applications, or if you see signs of performance issues on the Jazz
Authorization Server (high web container counts, error messages).

If you are using the SCIM feature for JAS, you will need to add the
following line to server.xml (see maxSearchResults to a value greater
than the number of users in your LDAP repository). Symptoms: You will
see errors during jts setup, and you'll also see errors on JAS in
messages.log.

For larger concurrent user loads, you may need to increase the size of
the database connection pool (the default is 50). Add the following line
to server.xml:

To debug possible performance issues related to database access, you can
enable timed operation monitoring on JAS. Add the following line to the
featureManager section in server.xml. This will generate a report of the
top 10 SQL calls to messages.log (and it will also generate a message
when SQL calls take longer than expected).

timedOperations-1.0

You can control the frequency of the reporting by adding the following
line to server.xml (reportFrequency is in hours):

If you see messages in the JAS messages.log file related to the number
of expired tokens, you can adjust some tuning parameters in
appConfig.xml to reduce the number of entries in the OAUTH20CACHE table.
The symptom is a message like this:

\[3/31/17 12:59:12:282 EDT\] 00007e46
om.ibm.ws.security.oauth20.plugins.db.CachedDBOidcTokenStore W 109496
expired tokens to delete. Consider increasing OAuth provider cleanup
interval

You can increase the frequency at which expired tokens are removed by
adding this to the databaseStore entry in appConfig.xml:

You can adjust the lifetime of the cached access tokens by changing
accessTokenLifetime and authorizationGrantLifetime (in the oauthProvider
section of appConfig.xml). By default, the accessTokenLifetime is 2
hours, and the authorizationGrantLifetime is 7 days. You can reduce
authorizationGrantLifetime to 1 day.

You may be able to improve performance by adjusting the isolation level
of the JDBC driver. You can do this by adding the following entry to the
dataSource section of appConfig.xml:

isolationLevel="TRANSACTION_READ_COMMITTED"

##### Additional notes: [additional-notes]

-   The scripts for creating tables are for example only. You should
    change them according to your usage and environment. For example, if
    the TOKENSTRING value of 2048 is too small, you can increase that by
    using a datatype of TOKENSTRING NVARCHAR(MAX) NOT NULL,.
-   Please review the Interactive Installation Guide for specific
    details on setting up the Authorization Server for the version of
    the product you are installing.
-   [WebSphere Liberty: Configuring Persistent OAUTH
    Services](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_oauth_sql.html)

##### Related topics: [related-topics]

-   [Websphere plugin and session
    affinity](http://www-01.ibm.com/support/docview.wss?uid=swg27020055&aid=1)
-   [Jazz server authentication
    explained](https://jazz.net/library/article/75)
-   [Liberty: Timed operations and JDBC
    calls](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_timeop.html)
-   [OAuth configuration parameters in
    Liberty](https://www.ibm.com/support/knowledgecenter/en/SSAW57_8.0.0/com.ibm.websphere.nd.doc/info/ae/ae/cwbs_oauthdefineprovider.html)
-   [Tuning options for
    Liberty](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_tun.html)

##### Additional contributors: Main.KrishnaKanthNaik, Main.ShubjitNaik [additional-contributors-main.krishnakanthnaik-main.shubjitnaik]

META:FILEATTACHMENT{name="Overview.png" attachment="Overview.png"
attr="" comment="" date="1467985966" path="Overview.png" size="12379"
user="vrokosz" version="1"}
META:FILEATTACHMENT{name="appConfigOracle.xml"
attachment="appConfigOracle.xml" attr="" comment="" date="1467990099"
path="appConfigOracle.xml" size="6402" user="vrokosz" version="1"}
META:FILEATTACHMENT{name="createOauthOracle.sql"
attachment="createOauthOracle.sql" attr="" comment="" date="1467990113"
path="createOauthOracle.sql" size="2521" user="vrokosz" version="1"}
META:FILEATTACHMENT{name="createOauthTablesDB2.sql"
attachment="createOauthTablesDB2.sql" attr="" comment=""
date="1467999798" path="createOauthTablesDB2.sql" size="2155"
user="vrokosz" version="1"} META:FILEATTACHMENT{name="appConfigDB2.xml"
attachment="appConfigDB2.xml" attr="" comment="" date="1467999861"
path="appConfigDB2.xml" size="6378" user="vrokosz" version="1"}
META:FILEATTACHMENT{name="server.xml" attachment="server.xml" attr=""
comment="" date="1468006036" path="server.xml" size="1753"
user="vrokosz" version="1"} META:FILEATTACHMENT{name="plugin-cfg.xml"
attachment="plugin-cfg.xml" attr="" comment="" date="1468328658"
path="plugin-cfg.xml" size="3403" user="hhuo" version="2"}
META:FILEATTACHMENT{name="IMsso.png" attachment="IMsso.png" attr=""
comment="" date="1468076242" path="IMsso.png" size="227155"
user="vrokosz" version="1"} META:FILEATTACHMENT{name="jtsSetup.png"
attachment="jtsSetup.png" attr="" comment="" date="1468076254"
path="jtsSetup.png" size="68298" user="vrokosz" version="1"}
META:FILEATTACHMENT{name="IHSSigner.png" attachment="IHSSigner.png"
attr="" comment="" date="1468256751" path="IHSSigner.png" size="19105"
user="vrokosz" version="1"} META:FILEATTACHMENT{name="IHSCert.png"
attachment="IHSCert.png" attr="" comment="" date="1468257989"
path="IHSCert.png" size="157657" user="vrokosz" version="1"}
META:FILEATTACHMENT{name="createOauthMSSQLv2.sql"
attachment="createOauthMSSQLv2.sql" attr="" comment="" date="1567768357"
path="createOauthMSSQLv2.sql" size="2120" user="shubjit" version="1"}
META:FILEATTACHMENT{name="createOauthMSSQL.sql"
attachment="createOauthMSSQL.sql" attr="" comment="Updated
NVARCHAR(2048) to NVARCHAR(MAX)" date="1567768719"
path="createOauthMSSQL.sql" size="2120" user="shubjit" version="1"}
