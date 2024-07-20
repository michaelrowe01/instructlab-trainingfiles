META:TOPICINFO{author="yisu" date="1681745822" format="1.1" reprev="1.7"
version="1.7"} META:TOPICPARENT{name="DeploymentMigratingAndEvolving"}

# Migrating Your Jazz Authorization Server From Derby To An Enterprise Database DKGRAY Authors: Main.DavidNoecker, Main.MirkoHartwig Build basis: Jazz Authorization Server 6.0.x+ [migrating-your-jazz-authorization-server-from-derby-to-an-enterprise-database-dkgray-authors-main.davidnoecker-main.mirkohartwig-build-basis-jazz-authorization-server-6.0.x]

ENDCOLOR

TOC{title="Page contents"}

## How to migrate your database from Derby to another COTS (Common Off The Shelf) database

### Procedure for preparing for, then migrating the applications to use the new database vendor

Additional background details to follow. For now, this procedure has
been tested internally and at multiple client sites. Also see:
[Documentation on Jazz Authorization Server DB configuration missing in
Knowledge
Centre](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/463705)
which will address how to setup Jazz Authorisation Server.

A non-clustered JAS installation may want to use an enterprise database.
The enterprise DB setup instructions are in the clustered JAS wiki topic
because a clustered JAS absolutely requires an enterprise database. A
non-clustered deployment may consider using one for various reasons
(e.g. ability to manage using existing IT staff/infrastructure), but the
requirements for the JAS DB are not extensive (it hardly grows at all;
performance is not critical; etc.).

1\. On JTS export JTS \*.json file with

./repotools-jts.sh -prepareJsaSsoMigration adminUserId= adminPassword=
repositoryURL=<https://%5Bpublic-url%5D>:\[port\]/jts
toFile=JTS_output.json

2\. Repeat on all other Applications, such as CCM, for example:

./repotools-ccm.sh -prepareJsaSsoMigration adminUserId= adminPassword=
repositoryURL=<https://%5Bpublic-url%5D>:\[port\]/ccm
toFile=CCM_output.json

Attention: please check twice when you create \*.json files for all
existing applications (use the corresponding repotools-xxx.sh for each
application)

3\. Stop JAS, base on your DB choice, follow the "Setting up a Jazz
Authorization Server DB instruction under the following Database Setup
pages:

Db2:
<https://www.ibm.com/docs/en/elms/elm/7.0.2?topic=database-setting-up-db2>
Oracle:
<https://www.ibm.com/docs/en/elms/elm/7.0.2?topic=database-setting-up-oracle>
SQL Server DB:
<https://www.ibm.com/docs/en/elms/elm/7.0.2?topic=database-setting-up-sql-server>

4\. Start JAS and test your configuration as described in this link:
<https://www.ibm.com/docs/en/elm/7.0.3?topic=server-deploying-starting-jazz-authorization>

5\. Stop all applications JTS, CCM, RM, QM etc.. This step is necessary
as if the applications are running you can not execute the migration
command.

6\. Migrate created \*.json files starting with JTS using

./repotools-jts.sh -migrateToJsaSso
authServerUrl`https://[jas-url]:9643/oidc/endpoint/jazzop authServerUserId`
authServerPassword= jtsSsoDataFile=JTS_output.json 7. Then migrate all
other application using as example fo CCM:

./repotools-ccm.sh -migrateToJsaSso
authServerUrl`https://[jas-url]:9643/oidc/endpoint/jazzop authServerUserId`
authServerPassword= jtsSsoDataFile=JTS_output.json
appSsoDataFile=CCM_output.json

8\. After migration, startup all Application beginning with JTS

9\. Test availability of all Application after startup

Attention: please be aware that LDX/LQE/JRS may not be available so
please try to unregister and reregister these applications after your
Test step 9.)

##### Related topics: [Deploying and starting Jazz Authorization Server](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.install.doc/topics/c_jsasso_jas_deploy_start.html&scope=null), [Setting up a cluster of Jazz Authorization Servers](PerformanceClusteredJAS) [related-topics-deploying-and-starting-jazz-authorization-server-setting-up-a-cluster-of-jazz-authorization-servers]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.ShubjitNaik, Main.PaulEllis, Main.TobiasBurkhardt [additional-contributors-main.shubjitnaik-main.paulellis-main.tobiasburkhardt]
