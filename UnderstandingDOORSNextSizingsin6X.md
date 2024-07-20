META:TOPICINFO{author="sahilkmansuri" date="1700821243" format="1.1"
version="1.51"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Understanding DOORS Next sizings in ELM 6.x to estimate timings when upgrading to DOORS Next 7.x DKGRAY Authors: Main.IanGreen, Main.PaulEllis, Main.VaughnRokosz Build basis: Engineering Lifecycle Management - DOORS Next 6.x migrating to DOORS Next 7.x [understanding-doors-next-sizings-in-elm-6.x-to-estimate-timings-when-upgrading-to-doors-next-7.x-dkgray-authors-main.iangreen-main.paulellis-main.vaughnrokosz-build-basis-engineering-lifecycle-management---doors-next-6.x-migrating-to-doors-next-7.x]

ENDCOLOR

TOC{title="Page contents"}

This article is intended to help contextualize your database size
relative to IBM's upgrade process testing. It is recommended to make a
note of how much storage the database is using for the DOORS Next
database both before and after the upgrade.

The article also discusses what tuning is required for your data size,
with the assumption of the database administrator (DBA) as a key
component in interpreting the advice.

Note: After upgrade, DOORS Next will demand much more resources on the
database server and less from the application server due to this
re-platforming. DBAs must re-size bufferpools, SGA/PGA sizes to cope
with the new workloads, and may also need to amend CPU/RAM resources.

Note: Ensure there is sufficient space for log files, database temporary
tables relative to the size of your installation. If you are unsure how
to calculate this after reading this and [Troubleshooting
Upgrades](https://jazz.net/wiki/bin/view/Deployment/TroubleshootingDOORSNextUpgrades)
then please contact IBM Support.

### Gathering pre-upgrade repository size

In this wiki and jazz.net articles, whenever repository size in DOORS
Next is discussed, it is in terms of the total number of artifacts. The
[7.0 performance: IBM Engineering Requirements Management DOORS
Next](https://jazz.net/wiki/bin/view/Deployment/RequirementsManagement70Performance)
details performance expectations post-upgrade, again using the number of
artifacts value.

You must take these measurements on the DOORS Next version 6 repository
before the upgrade. Execute the following SQL statement and make a note
of the results in case you need to share them with IBM. If you run this
SQL, it is important to supply IBM Support with all the values, as each
value can effect the duration of your upgrade.

**Note** These SQL queries are not applicable to a 7x DOORS Next
repository. Use the queries under the Post-upgrade calculations section
below, after upgrading to 7.x.

\- Oracle

SELECT 'concepts' AS metric, COUNT(DISTINCT CONCEPT) AS value FROM
VVCMODEL_VERSION UNION ALL SELECT 'versions' AS metric, COUNT(DISTINCT
VERSION) AS value FROM VVCMODEL_VERSION UNION ALL SELECT 'configs' AS
metric, COUNT(**) AS value FROM VVCMODEL_CONFIGURATION UNION ALL SELECT
'changesets' AS metric, COUNT(**) AS value FROM VVCMODEL_CHANGE_SET
UNION ALL SELECT 'version mappings' AS metric, COUNT(**) AS value FROM
VVCMODEL_VERSION UNION ALL SELECT 'resources' AS metric, COUNT(**) AS
value FROM RESOURCE_RESOURCE UNION ALL SELECT 'resource revisions' AS
metric, COUNT(**) AS value FROM RESOURCE_RESOURCE res INNER JOIN
REPOSITORY_ITEM_STATES states ON states.ITEM_UUID = res.ITEM_ID UNION
ALL SELECT 'item states' AS metric, COUNT(**) AS value FROM
REPOSITORY_ITEM_STATES

\- DB2

SELECT 'concepts' AS metric, COUNT(DISTINCT CONCEPT) AS value FROM
VVCMODEL.VERSION UNION ALL SELECT 'versions' AS metric, COUNT(DISTINCT
VERSION) AS value FROM VVCMODEL.VERSION UNION ALL SELECT 'configs' AS
metric, COUNT(**) AS value FROM VVCMODEL.CONFIGURATION UNION ALL SELECT
'changesets' AS metric, COUNT(**) AS value FROM VVCMODEL.CHANGE_SET
UNION ALL SELECT 'version mappings' AS metric, COUNT(**) AS value FROM
VVCMODEL.VERSION UNION ALL SELECT 'resources' AS metric, COUNT(**) AS
value FROM RESOURCE.RESOURCE UNION ALL SELECT 'resource revisions' AS
metric, COUNT(**) AS value FROM RESOURCE.RESOURCE res INNER JOIN
REPOSITORY.ITEM_STATES states ON states.ITEM_UUID = res.ITEM_ID UNION
ALL SELECT 'item states' AS metric, COUNT(**) AS value FROM
REPOSITORY.ITEM_STATES

### How to interpret your values

Until ELM 7.0, the key value to determine the size of your database has
been the number of artifacts in your repository. In the [7.0 Performance
datasheet for DOORS
Next](https://jazz.net/wiki/bin/view/Deployment/RequirementsManagement70Performance#Data_limits_in_7_0)
performance during usage is still measured in these terms.

In terms of upgrade, the resource revisions metric and the other metrics
above will be of more help than the raw number of artifacts in your
repository. The resource revisions number is important as it indicates
the number of revisions that the upgrade will need to process. There are
also other shapes that could determine the overall size. Your Staging
environment upgrade is the most reliable indicator of expected upgrade
time.

#### Sample data points from upgrades

\#SQLMetricExamples

TABLE{ tableborder="2" cellpadding="2" cellspacing="2" cellborder="2"
headeralign="center" dataalign="right" disableallsort="on"
tablewidth="40" }

|                        |                      |            |            |
|------------------------|----------------------|------------|------------|
|                        | 2.3M IBM Test Server | Client A   | Client B   |
| Repository size        | 2,300,000            | 1,897,515  | 256,615    |
| Concepts               | 7,884,586            | 3,414,563  | 1,241,340  |
| Versions               | 8,176,219            | 6,107,958  | 2,893,997  |
| Configs                | 46,935               | 275        | 5297       |
| Changesets             | 605,539              | 1,797,783  | 646,033    |
| Version Mappings       | 8,792,972            | 10,077,175 | 4,675,924  |
| Resources              | 10,904,741           | 10,668,439 | 11,057,361 |
| Resource Revisions     | 12,673,763           | 19,021,273 | 17,800,441 |
| Item States            | 22,280,080           | 31,239,827 | 23,930,331 |
| AddTables upgrade time | 10 hours             | 17.5 hours | 7 hours    |

Notes:

-   This information is database agnostic.
-   The hardware between the examples were different.
-   This table shows how different measurements can impact the overall
    upgrade time.
-   As stated in [Migration tuning of the repotools
    JVM](#MigrationTuning), the JVM heap size was set to 16GB,
    REPOTOOLS_MX_SIZE=16384

The hardware required to achieve the initial 2.3M time, based on that
data shape is available in the

#### DB Server for IBM testing

2 x Intel Xeon E5-2640, 2.5GHz (ten-core):

-   40 logical processors (hyperthreaded)
-   64 GB RAM
-   RAID 10 - 15K SAS, disk x14
-   Red Hat Enterprise Linux Server 7.6

#### RM Server for IBM testing

2 x 2.5GHz (six-core):

-   24 logical processors (hyperthreaded)
-   32 GB RAM
-   RAID 5 - SAS, disk x4
-   Red Hat Enterprise Linux Server 7.6
-   WebSphere Liberty, 24GB Heap

### Understanding data shape deviations

#### Large composite changesets

During our upgrade validations, we check to ensure consistency of the
changesets that have been delivered. Clients that have used large
composite deliveries of changesets may require additional temp dbspace
during the upgrade.

Run the following two queries to understand your data shape. The second
query relies on the output of the first, so replace the ? (question
mark) in the 2nd query with the output of the first.

Run the following queries in the DOORS Next 6.x/7.x environment:

DB: Oracle

SELECT JZ_PARENT_ID, COUNT(JZ_PARENT_ID) FROM
VVCMODEL_CHANGE_SET_MERGED_FRM GROUP BY JZ_PARENT_ID ORDER BY
COUNT(JZ_PARENT_ID) DESC;

SELECT CHANGE_SET_ITEM_ID, TARGET_STREAM_ITEM_ID FROM
VVCMODEL_DELIVERED_CHANGE WHERE CHANGE_SET_ITEM_ID = ?;

If your results return multiple entries in excess of 1,000, then you
should follow the instructions below for [Oracle
optimizations](#OracleOptimizations).

DB: DB2

SELECT JZ_PARENT_ID, COUNT(JZ_PARENT_ID) FROM
VVCMODEL.CHANGE_SET_MERGED_FROM GROUP BY JZ_PARENT_ID ORDER BY
COUNT(JZ_PARENT_ID) DESC;

SELECT CHANGE_SET_ITEM_ID, TARGET_STREAM_ITEM_ID FROM
VVCMODEL.DELIVERED_CHANGE WHERE CHANGE_SET_ITEM_ID = ?;

### Monitoring your upgrade

There is an extensive section in this
[wiki](TroubleshootingDOORSNextUpgrades#NMon_and_other_monitoring_tools)
on how to monitor your system during this upgrade, with specific areas
to focus on when running your Staging upgrades. Planning your ELM
upgrade to version 7.x also contains additional information which may be
required when contacting IBM Support. A list of must-gather information
is at the bottom of this article.

### Migration tuning of the repotools JVM

\#MigrationTuning

In terms of the DOORS Next repository, you should only need to amend the
following setting in the repotools-rm file from 1500MB to the values
below. This is consistent with the Interactive Upgrade Guide. It is only
anticipated that you would require 32GB if your repository is on a very
large scale. It is not recommended to increase past 32GB and certainly
not recommended to create enormous heaps to speed up the upgrade. We
found no evidence that larger heap sizes improved performance, beyond
32GB.

We also recommend that you set a file to record the verbose garbage
collection information. For more information on setting the verbosegc
log, see the WebSphere help document [Writing Verbose GC to a Specified
Log -Xverbosegclog in AIX, Linux and
Windows](https://www.ibm.com/support/pages/writing-verbose-gc-specified-log-xverbosegclog-aix-linux-and-windows)

Windows example to increase it to 16G and set verbose GC logging:

set REPOTOOLS_MX_SIZE=16384 set VMARGS=VMARGS -verbose:gc
-Xverbosegclog:c:\temp\verbosegc.log -XX:NumberOfGCLogFiles=100
-XX:GCLogFileSize=20M

Linux example to increase it to 16G and set verbose GC logging:

export REPOTOOLS_MX_SIZE=16384 export VMARGS="\$VMARGS -verbose:gc
-Xverbosegclog:/tmp/verbosegc.log -XX:NumberOfGCLogFiles=100
-XX:GCLogFileSize=20M

## Post-upgrade calculations

It is expected that the post-upgraded DOORS Next database will require
approximately 60 -100 more than the storage required for the existing
DOORS Next 6.x. You must ensure that the database is suitably configured
for this growth.

\- Oracle

SELECT 'resource types' AS metric, COUNT(**) AS value FROM
DNGMIGRATION_DB_RESOURCE_TYPE UNION ALL SELECT 'upgrade mappings' AS
metric, COUNT(**) AS value FROM DNGMIGRATION_DB_UPGRADE_MAPPNG UNION ALL
SELECT 'mappings' AS metric, COUNT(**) AS value FROM REPOSITORY_VERSION
UNION ALL SELECT 'r.versions' AS metric, COUNT(DISTINCT STATE_ID) AS
value FROM REPOSITORY_VERSION UNION ALL SELECT 'item states' AS metric,
COUNT(**) AS value FROM REPOSITORY_ITEM_STATES

\- DB2

SELECT 'resource types' AS metric, COUNT(**) AS value FROM
DNGMIGRATION.DB_RESOURCE_TYPE UNION ALL SELECT 'upgrade mappings' AS
metric, COUNT(**) AS value FROM DNGMIGRATION.DB_UPGRADE_MAPPING UNION
ALL SELECT 'mappings' AS metric, COUNT(**) AS value FROM
REPOSITORY.VERSION UNION ALL SELECT 'r.versions' AS metric,
COUNT(DISTINCT STATE_ID) AS value FROM REPOSITORY.VERSION UNION ALL
SELECT 'item states' AS metric, COUNT(**) AS value FROM
REPOSITORY.ITEM_STATES

## Tuning the database

This next section details a base set of considerations which apply where
database servers are typically installed within the context of ELM-only.

The most significant advice we can give for tuning databases for upgrade
is already listed in the [Interactive Upgrade
Guide](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.2/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html),
which is to ensure that the database statistics are up-to-date, for
example:

Oracle: EXEC DBMS_STATS.GATHER_DATABASE_STATS

DB2: DB2 REORGCHK UPDATE STATISTICS ON TABLE ALL

### Database tuning and guidance

When database servers are part of large database farms, many of these
considerations will be redundant. However, it is recommended to discuss
with your database administrator (DBA) to determine what values are
appropriate within the context of your enterprise setup. This section is
not expected to be copied verbatim. These values are specific to the
machine size in use and are not appropriate for any database server
which is smaller, where you will need to extrapolate relative values.

#### DB2

When the IBM Performance Engineering team ran the DB2 upgrade of DOORS
Next for 7.x, there were some tuning actions performed to the database.
This section of the article is a guide for DBAs and not prescriptive,
but advisory. We are therefore only covering the DB2 settings that were
altered in order to improve performance.

First, we forced DB2 to maximize all the available RAM to the DOORS Next
DB Memory as well as its bufferpool size, e.g.:

First, run these three commands as db2admin user prior to the upgrade,
to understand your configurations and settings for the current
database(s) (replacing to the actual database name):

\$ db2 connect to \$ db2pd -dbptnmem \$ db2 get db cfg for

We recommend that you unset the automatic flag so that STMM
(self-tuning) does not reduce the settings inadvertently during
migration. We have seen anecdotal evidence that upgrade times can be
reduced by up to 40 when this is unset.

Your sizes could vary depending on the size of the database and the
actual RAM available on the system.

Note:

-   We recommend that your BUFFERPOOL during upgrade is 10 of the
    overall RM database size.
-   That the BUFFERPOOL is 70 of DATABASE_MEMORY,

For example: 500GB RM database -\> 50GB BUFFERPOOL (3276800 16KB pages)
-\> 70GB DATABASE_MEMORY (18350080 4KB pages).

db2 "ALTER BUFFERPOOL IBMDEFAULTBP SIZE 3276800" db2 "update db cfg for
RMDB using DATABASE_MEMORY 18350080"

See the [Db2 documentation for calculating memory
sizes](https://www.ibm.com/docs/en/db2/11.5?topic=parameters-database-memory-database-shared-memory-size).
If your DBA requires further guidance, contact IBM Db2 Support.

Then we secured the minimums for the following:

db2 update db cfg using stmt_conc off immediate db2 update db cfg using
APPLHEAPSZ 10000 automatic db2 update db cfg using LOGFILSIZ 65536 db2
update db cfg using SORTHEAP 28615 db2 update db cfg using
SHEAPTHRES_SHR 143077 db2 update db cfg using PCKCACHESZ 32184 db2
update db cfg using STMTHEAP 8000 automatic db2 update db cfg using
AUTO_REORG off

Finally, we altered inline length for LOB data:

alter table REPOSITORY.ITEM_STATES alter column ITEM_VALUE set inline
length 2048; alter table REPOSITORY.CONTENT_STORAGE alter column
CONTENT_BYTES set inline length 4096; reorg table REPOSITORY.ITEM_STATES
allow read access longlobdata; reorg table REPOSITORY.CONTENT_STORAGE
allow read access longlobdata;

LOBs during upgrade: LOBs don't use the buffer pool, so that means more
I/O is required for their processing. If you are monitoring I/O on the
database server, they this can be run later...but it will increase I/O.
If Db2 is running very high-performing disks, then these inline steps
are not necessary.

There is more information on these values and how they would be set for
production performance in the [Db2
Tuning](https://jazz.net/wiki/bin/view/Deployment/RequirementsManagement70Performance#DB2_tuning)
portion of the [7.0 Performance
report](https://jazz.net/wiki/bin/view/Deployment/RequirementsManagement70Performance).

#### Oracle

This section of the article is a guide for DBAs and not prescriptive,
but advisory. We are therefore only covering the Oracle settings that
were altered in order to improve performance.

Oracle memory management settings:

automatic memory management memory_max_target=50000M scope=spfile;
memory_target=50000M scope=spfile; sga_max_size=0 scope=spfile;
sga_target=0 scope=spfile; pga_aggregate_limit=0 scope=spfile;
pga_aggregate_target=0 scope=spfile;

\#OracleOptimizations It is also important that you ensure that you have
sufficient TEMP tablespaces, which have the ability to auto-extend if
necessary. Failure to do so will result in a compromised upgrade and
likely to require a rollback and re-attempt at the upgrade. Error
messages encountered with Oracle servers can be found in
[Troubleshooting DOORS Next Upgrades](TroubleshootingDOORSNextUpgrades).

We recommend turning the following optimizer parameters to false as they
make changes to execution plans dynamically, reacting to data that it
sees. These settings can lead to upgrade unpredictability since the
order in which Oracle processes the data, for example, change sets, will
matter. This skews our data, so it is hard for the optimizer to make
good decisions. There are two optimizer flags that can make execution
plans more stable. Caution: these are system-wide parameters and will
impact all the rest of the SQL during the upgrade.

In Oracle 12.1, you would set

-    OPTIMIZER_ADAPTIVE_FEATURES=FALSE
-    \_optimizer_use_feedback=FALSE
-    "\_complex_view_merging"=FALSE

<https://community.oracle.com/tech/developers/discussion/228122/optimizer>

In Oracle 12.2 and Oracle 19c, you would set

-    OPTIMIZER_ADAPTIVE_PLANS to FALSE,
-    OPTIMIZER_ADAPTIVE_STATISTICS to FALSE
-    \_optimizer_use_feedback=FALSE
-    "\_complex_view_merging"=FALSE

Note, "\_complex_view_merging" is a hidden parameter, so the double
quotes are required. We recommend that this setting is reset after the
upgrade:

-   alter system reset "\_complex_view_merging"

\| Note: If you are unable to apply these settings to your Oracle
installation then you will need to control the amount of temp dbspace
used during the Phase 3 - Finalisation phase by reducing the amount of
threads that run at this time. See: [Setting the Foundation threads to
reduce temp dbspace
consumption](TroubleshootingDOORSNextUpgrades#TEMP_dbspace).

There is more information on these values and how they would be set for
production performance in the [Oracle
Tuning](https://jazz.net/wiki/bin/view/Deployment/RequirementsManagement70Performance#Oracle_tuning)
portion of the [7.0 Performance
report](https://jazz.net/wiki/bin/view/Deployment/RequirementsManagement70Performance).

### Considerations for larger imports.

\#ConsiderationForLargerImports

What is considered a large import can be subjective, but in terms of
this article it is any migration of data in this manner where new tables
are being populated in the database from a Jena data store should treat
this as a large import. It is common to increase the number of
transaction logs to accommodate such an operation.

-    Increase the log file of the database server. Empirically, our
    expertise resides with DB2, therefore the following settings are
    recommended for change in order to unblock the bottleneck of the
    database server.

db2 connect to RM7 db2 update db cfg for RM7 using LOGPRIMARY 120 db2
update db cfg for RM7 using LOGSECOND -1 db2 update db cfg for RM7 using
LOGFILSIZ 16384

It is important to ensure that your Oracle archive logs are appropriate
for a very large transaction that occurs as part of the DNG upgrade to
avoid an Oracle DB archive logging full filesystem. See [Troubleshooting
DOORS Next Upgrades](TroubleshootingDOORSNextUpgrades) for more on error
SQLSTATE: 64000, SQLCODE: 257 which relates to this topic.

#### Undo tablespace

For large upgrades, and/or where the data may be unusual due to import
scripts, OSLC, or any other non-GUI usage then it is recommended that
the undo tablespace is monitored and set to autoextend where possible.
Read [Undo tablespace
errors](https://jazz.net/wiki/bin/view/Deployment/TroubleshootingDOORSNextUpgrades#Undo_tablespace)
for more details.

#### Ensure the hard disks in use are optimal.

Solid State Disks(SSD) are recommended for the RM indices location and
the database server's log file area. Standard 10k rpm as disk speed is
generally insufficient for the read/write access required on very
heavily used directories. Use hdparm tT to track disk speed. The Timing
cached reads per second are crucial.

Typically with database servers, the IOPS (I/O per second) is a
significant indicator of performance. We recommend that your DBA refer
to our article on [Disk
Benchmarking](https://jazz.net/wiki/bin/view/Deployment/DiskBenchmarking).
This article covers tools that can benchmark the performance of storage
systems, and includes some sample results from the IBM labs. The typical
methods to calculate the IOPS of the DB server are these benchmarks:

-   [Calibrate_io](https://jazz.net/wiki/bin/view/Deployment/DiskBenchmarking#Disk_benchmarking_with_calibrate)
    (Oracle)
-   [SLOB](https://jazz.net/wiki/bin/view/Deployment/DiskBenchmarking#Disk_benchmarking_with_SLOB)
    (Oracle)
-   [Sysbench](https://jazz.net/wiki/bin/view/Deployment/DiskBenchmarking#Disk_benchmarking_with_sysbench)
    (OS)

### Considerations for Staging comparisons (Must gather)

\#MustGather

It is important to size any run in a Staging environment appropriately.
The ideal is to use comparable hardware, as well as the same software
settings in the application (repotools-rm) and database (as discussed
above) to know how long the upgrade will take. If it is not possible to
do so, then you should understand the characteristics of your deployment
by assessing [ What to monitor during the
upgrade](https://jazz.net/wiki/bin/view/Deployment/TroubleshootingDOORSNextUpgrades#What_to_monitor_during_the_upgra)

##### Related topics: [7.0 performance: IBM Engineering Requirements Management DOORS Next](https://jazz.net/wiki/bin/view/Deployment/RequirementsManagement70Performance), [Planning your ELM upgrade to version 7.0](https://www.ibm.com/support/pages/node/6156021), [Oracle 12c Tuning Guide](https://docs.oracle.com/database/121/TGSQL/toc.htm) [related-topics-7.0-performance-ibm-engineering-requirements-management-doors-next-planning-your-elm-upgrade-to-version-7.0-oracle-12c-tuning-guide]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.HongyanHuo, Main.MarkGoossen, Main.TimFeeney, Main.WillChatham [additional-contributors-main.hongyanhuo-main.markgoossen-main.timfeeney-main.willchatham]
