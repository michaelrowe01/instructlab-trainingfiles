META:TOPICINFO{author="rwatts" date="1552322902" format="1.1"
version="1.6"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Leveraging Database Partitioning in RQM for Data Growth DKGRAY Authors: Richard Watts, Prabhat Gupta, Gary Johnston, Vishwanath Ramaswamy Build basis: Rational Quality Manager, 6.0.6.1 [leveraging-database-partitioning-in-rqm-for-data-growth-dkgray-authors-richard-watts-prabhat-gupta-gary-johnston-vishwanath-ramaswamy-build-basis-rational-quality-manager-6.0.6.1]

ENDCOLOR

TOC{title="Page contents"}

Starting in 6.0.6.1, we introduced a new feature for customers using
Rational Quality Manager with configuration management called database
partitioning. This is not a product feature but the necessary
configuration steps to enable table partitioning in your enterprise
database.

**Note:** Database partitioning is an **enterprise feature**, which
means you need to determine if the version/license of your enterprise
database supports this feature before you attempt to turn it on. All
three enterprise databases we support, have a version that supports
table partitioning. The best resource to determine the features your
enterprise database supports is your database administrator.

## What is partitioning?

Partitioning is the division of a logical table (or database) into
distinct independent parts. It is normally done for manageability, data
scale, availability or load balancing. In our case, we are partitioning
tables for data scale. Meaning, we partition the table to keep the same
levels of performance as data grows.

In this case, we are partitioning the version table based on item type.
Future releases will include recommendations for other high growth
tables, but we decided to focus on one for our initial release of this
feature.

## When should I consider partitioning

There are two ways to determine how much data you have in your version
table. We provide a managed bean, Project Metrics MBean that you can
enable and monitor for data growth. In addition, we provide vendor
specific queries that can be run to check the number of rows in the
version table. These queries can be run from the repodebug User
Interface in Rational Quality Manager. Either of these approaches will
tell you the size of the version table, which is the key factor on when
to consider enabling table partitioning.

When considering whether to enable partitioning, you need to evaluate
the size of the version table. As the size of the table grows beyond
2GB, it is recommended by database vendors that you consider data growth
strategies for your table. In our case, **25 million rows** in the
version table is approximately 4.5 gb and you should consider
partitioning your version table. Database Administrators should be aware
that enabling database partitioning does incur an approximate 20
increase in table index size.

Below are techniques for determining the size of your version table.

### Project Metrics MBean

How to enable the mbean

The specific attribute

### Repodebug Queries

**Microsoft SQL Server**

SELECT COUNT(1) FROM REPOSITORY.VERSION;

**Oracle DB**

SELECT COUNT(1) FROM REPOSITORY.VERSION;

**DB2 LUW**

SELECT COUNT(1) FROM REPOSITORY.VERSION;

**DB2z**

SELECT COUNT(1) FROM RPSTR_VRSN;

**DB2i**

SELECT COUNT(1) FROM \_REPOSITORY.VERSION;

Where **SchemaPrefix** can be obtained from QMs teamserver property :
com.ibm.team.repository.db.schemaPrefix **Example:**
teamserver.properties for QM have -\>
com.ibm.team.repository.db.schemaPrefix=QMX So the SQL would look like
-\> SELECT COUNT(1) FROM \*QMX_REPOSITORY.VERSION\*;

## How to enable partitioning

Enabling table partitioning is done while the system is shut down using
a repotools command.

repotools-qm.sh -partitioning \[teamserver.properties=tspFile\]
\[logfile=logFile\] enable \[noPrompt\]

## How to disable partitioning

Disabling table partitioning is done the same way. The system is shut
down and a repotools command is executed to disable the table partition.

repotools-qm.sh -partitioning \[teamserver.properties=tspFile\]
\[logfile=logFile\] disable \[noPrompt\]

##### Related topics [related-topics]

[Deployment web home](DeploymentWebHome),

[Project Metrics
MBean](https://jazz.net/wiki/bin/view/Deployment/ProjectMetricsCollectorTask )
[repotools-qm -partitioning
command](https://www-03preprod.ibm.com/support/knowledgecenter/en/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/r_repotools_partitioning.html)

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Michael Afshar, Susan Yeshin, Chris Austin [additional-contributors-michael-afshar-susan-yeshin-chris-austin]
