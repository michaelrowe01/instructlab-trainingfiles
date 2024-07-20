META:TOPICINFO{author="sbagot" date="1385142927" format="1.1"
reprev="1.1" version="1.1"}
META:TOPICPARENT{name="WhyDoMyETLsTakeSoLongToRun"}

# Why do my ETLs take so long to run? DKGRAY Authors: Main.GeraldMitchell, Main.StephanieBagot Build basis: CLM 4.x ENDCOLOR [why-do-my-etls-take-so-long-to-run-dkgray-authors-main.geraldmitchell-main.stephaniebagot-build-basis-clm-4.x-endcolor]

TOC{title="Page contents"}

This situation is to help assess and analyze data to assist in the
investigation and debugging of long running Java and Insight ETLs
(Extract, Transform and Load) with IBM Rational Collaborative Lifecycle
Management (CLM) applications.

## Initial assessment

After you have completed the [Initial
troubleshooting](https://jazz.net/wiki/bin/view/Deployment/InitialTroubleshootingInvestigation),
the first item to identify the cause for long running ETLs is to monitor
the ETL progress and determine which of the ETLs are taking too long to
complete. Keep in mind that 'too long' is relative to the user's
perception. This could be affected by your system resources or other
environmental impacts, which might cause longer running ETLs. Your ETLs
might simply be running 'too long' due to limitations in your
environment or configuration.

Some questions to help analyze this information are as follows:

### Symptoms

\* How did you discover that the ETL is running too long? \* Which
applications are the ETL involved with? \* Is the ETL eventually
completing? \* If the ETL completes, is the data there and as expected?
This can be tested by running any report and validating that the data is
as expected. The report parameters should also show all the associated
team areas, timelines, etc.

### Impact / scope

-   Does it effect multiple ETLs?
-   Are the ETL problems across all applications?

### Timing (when?)

-   When did the long running ETLs start to occur, or did it always take
    long to run?
-   Is the long running ETL continuous or repeatable or intermittent?
-   If the ETL is run manually, does it complete in sufficient time?

### Environmental changes

-   Have the data collection jobs been changed?
-   Have any projects been archived, deleted or renamed?
-   Have any applications or reporting solutions been added or removed?
-   Has the data warehouse changed? (Such as location, JDBC connection
    information)
-   Have the ETLs been changed or customized?

## Recommended analysis steps

### All ETLs (Out-of-the-box (OOTB) ETLs)

This topic is described further for OOTB ETLs in [Why do my out of the
box ETLs take so long to
load?](https://jazz.net/wiki/bin/view/Deployment/WhyDoMyOutOfTheBoxETLsTakeSoLongToRUN)

### Custom ETLs

This topic is described further for custom ETLs in [Why do my custom
ETLs take so long to
load?](https://jazz.net/wiki/bin/view/Deployment/WhyDoMyCustomETLsTakeSoLongToRun)

### Reporting specific logs

-   Review the ETL logs and look for the information on the data
    collection jobs. Check the application log files (qm-etl.log,
    jts-etl.log, ccm-etl.log, jazz-etl.log) in the following log
    directory: /logs/\*-etl.log See [How do I read the ETL log
    files](https://jazz.net/wiki/bin/view/Deployment/HowToReadETLLogFile)
    for more information.
-   Data manager logs in the reporting tool
    -   The default location of the data manager logs are at
        ***/cognos/datamanager/log***
    -   Check the log named Build_job_type.log, to see whether there are
        failures or how many records have been delivered.
-   Data log load: ***/cognos/datamanager/data***
-   Review the XML data configuration (.xdc). Make sure that the
    correct/current version catalog is used.
-   The mustgather information for Rational Insight is available from
    [Technote 1409882 - Data Collection: Rational Custom Report
    MustGather
    List](http://www.ibm.com/support/docview.wss?uid=swg21409882). This
    information may also be valuable if you are trying to analyze the
    ETLs and are using Insight.
    -   Rational Insight ETL logs for mustgather:
        -   The default location of the Rational Insight JDBC logs and
            Rational Insight Data Manager logs are at C:/Documents and
            Settings//logs
        -   You can change the default location by modifying the
            register of the jdbclogpath parameter in the registry:
            HKEY_LOCAL_MACHINE/SOFTWARE/ODBC/ODBCINST.INI/IBM Rational
            insight XML ODBC Driver
        -   Rational Insight Data Manager logs are located at
            /cognos/datamanager/log
        -   Rational Insight Data Manager logs for rejected data are
            located in /cognos/datamanager/data

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
-   <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/topic/com.ibm.rational.reporting.admin.doc/topics/t_running_the_data_collection_jobs.html>
-   <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/topic/com.ibm.rational.reporting.admin.doc/topics/c_data_collection.html>

##### Additional contributors: None [additional-contributors-none]

##### Questions and comments: [questions-and-comments]

COMMENT{type="below" target="WhyDoMyETLsTakeSoLongToRunComments"
button="Submit"}

INCLUDE{"WhyDoMyETLsTakeSoLongToRunComments"}
