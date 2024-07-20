META:TOPICINFO{author="sbagot" date="1432663588" format="1.1"
version="1.44"} META:TOPICPARENT{name="PerformanceTroubleshooting"}

# Why do my ETLs take so long to run? DKGRAY Authors: Main.GeraldMitchell, Main.StephanieBagot Build basis: CLM 4.x, 5.x [why-do-my-etls-take-so-long-to-run-dkgray-authors-main.geraldmitchell-main.stephaniebagot-build-basis-clm-4.x-5.x]

ENDCOLOR

TOC{title="Page contents"}

This situation is to help determine both cause and resolution where ETL
(Extract, Transform, Load) processes take significantly longer than
expected to run.

## Introduction to ETLs

In order to understand how running ETLs can cause performance issues
across the server, you should first understand what the ETL is doing.

First, the ETL (Extract, Transform, Load) jobs are initiated as a
scheduled task, run by the following service as
***com.ibm.team.datawarehouse.service.internal.SnapshotRunnerTask***.
The ETLs are run in a certain sequence, detailed in the article [Running
the
ETLs](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.1/com.ibm.rational.reporting.admin.doc/topics/t_running_the_data_collection_jobs.html?cp=SSYMRC_5.0.1⟨=en).

After the task is initiated, the ETL will extract the data from the
application database, transform it, and load it into the operational
data store (ODS) tables within the data warehouse database. While the
ETL is active, network latency, database configuration, and JDBC
connections can contribute to long running ETLs or performance issues.
If the application servers and database servers are located remotely,
the loading process is affected.

There are two types of ETLs which run on the server - Full Data
Collection Job and an Incremental, or Delta, data collection Job. On the
Data Collection Jobs page, each are denoted by two different icons under
Action. Hover over the icon for a description. The Full Data Collection
Jobs occur during the initial run of the data collection jobs. These
jobs take significantly longer because it is gathering all data.
Subsequent job runs are done using an incremental or 'delta' run where
only changed data from the last job is collected. These jobs are much
faster.

Once all the application ETLs have run, the JTS Star ETL is run, which
will again extract, transform and load the data, this time from the ODS
and stored in Jazz Team Server. Again, network latency, database
configuration, and JDBC connections can contribute to performance
degradation at this step.

Both sets of ETLs require system resources to run the tasks and extract
and load the data on both the server hosting the Collaborative Lifecycle
Management (CLM) application and the database server.

**Note:** The [Data Collection Component
(DCC)](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.rational.dcc.doc/topics/c_dcc_intro.html)
is available as of CLM 5.0 and higher. Deploying DCC on another system
will alleviate many of the known performance constraints described below
when you are using the traditional Java ETL's. If you are running the
out of the box CLM ETL's, it is strongly recommended you use DCC in
place of the Java ETL's. If you are using Rational Insight to execute
the out of the box CLM ETL's, it is also recommended to use the
Insight/DCC integration scripts to [invoke the CLM DCC ETL's from your
Insight Data Manager
ETL](http://www-01.ibm.com/support/knowledgecenter/SSRL5J_1.1.1.6/com.ibm.rational.dcc.doc/topics/t_postinstall_insight.html).
A video is also available on [this
page](https://www.youtube.com/watch?v=37KgyonMjZE)

## Initial assessment and analysis

For information on how to assess and analyze information related to long
running ETLs, review the [Initial Assessment and
Analysis](https://jazz.net/wiki/bin/view/Deployment/ETLAssessmentAndAnalysis)
page.

## Known issues

### Migrating from the data mart to the data warehouse

Despite improvements to ETL and server performance, the migration
between the data mart and data warehouse is still expected to be long
running. If you previously used the data mart, the first ETL run into
the data warehouse will automatically migrate the data over from the
data mart, which is typically a longer run time than if you were to run
a full data collection job. This is due to many factors including the
time it takes to gather the records, and move them between databases
(where network or database latency may come into play).

### Older CLM versions

CLM versions prior to 4.0.1 might have run full collection for each
build. Improvements have been made to ensure that delta builds are being
run (ensuring that only changes between the last build and the current
are captured) as well as overall ETL performance. Ensure you are running
on the latest version of CLM to take advantage of these enhancements.

### Database statistics

After an ETL is run, the database statistics are updated for the tables.
In some environments, the database statistics would cause extremely slow
running ETLs and is indicated in the ETL log where total time for each
build is not the sum of each of the times above (See [How do I read the
ETL Log
Files](https://jazz.net/wiki/bin/view/Deployment/HowToReadETLLogFile)
for more information). If your database administrator (DBA) is running
UPDATE STATS by default, you can turn it off from the Jazz Team Server.
**Note:** We do not recommend turning this off by default because over
time the database statistics it will increase performance due to the
indexing that is completed. To turn this feature off, navigate to your
Jazz Team Server Data Warehouse Connections page:
<https://:/jts/admin#action=com.ibm.team.reportsManagement.configureDataWarehouseConnection>
and change "Automatically update the database statistics" to false.

### Historical Data

The RICALM.REQUEST_BASELINE table will contain information necessary for
reporting. There may be large amounts of historical data, causing the
table to contain more information which may no longer be needed and be
larger in size. It may be advantageous to remove some of the historical
data if it is no longer needed. **DO NOT PROCEED with removing the
historical data without being under the advisement of support.**

### Oracle Data Guard

When running Oracle Data Guard, performance may be slow due to the
functions of Data Guard. It may be advantageous to investigate turning
Oracle Data Guard off. **DO NOT PROCEED with turning Oracle Data Guard
off without first consulting your Database Administrator.**

### Datawarehouse Indices

There are certain indices on the RICALM.REQUEST_BASELINE table which may
be contributing to performance degradation during updates. It may be
possible to remove these indices. **DO NOT PROCEED with removing the
indices without being under the advisement of support.**

## Possible causes and solutions

After reviewing the above information on assessment and analysis, you
might find an error that correlates to the long running ETL. Navigate to
one of the following pages:

-   [Yes, I found an error that could be causing the long running
    ETL](https://jazz.net/wiki/bin/view/Deployment/LongRunningETLError)
-   [No, I have not found any error causing the long running
    ETL](https://jazz.net/wiki/bin/view/Deployment/LongRunningETLNoError)

##### Related topics: [related-topics]

-   Still need help troubleshooting your performance issue? Refer to
    [Performance Troubleshooting](PerformanceTroubleshooting) for
    additional topics.
-   [Why Do my OOB ETLs take so long to
    run?](WhyDoMyOutOfTheBoxETLsTakeSoLongToRUN)
-   [Why do my custom ETLs take so long to
    run?](WhyDoMyCustomETLsTakeSoLongToRun)
-   [How to read ETL log files](HowToReadETLLogFile)
-   [Long-running ETLs with error](LongRunningETLError)
-   [Long-running ETLs without errors](LongRunningETLNoError)

##### External links: [external-links]

-   <http://en.wikipedia.org/wiki/Extract,_transform,_load>
-   <http://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.5/com.ibm.rational.reporting.admin.doc/topics/t_running_the_data_collection_jobs.html>
-   <http://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.5/com.ibm.rational.reporting.admin.doc/topics/c_data_collection.html>

##### Additional contributors: None [additional-contributors-none]

##### Questions and comments: [questions-and-comments]
