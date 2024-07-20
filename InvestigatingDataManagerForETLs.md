META:TOPICINFO{author="sbeard" date="1368525168" format="1.1"
version="1.6"} META:TOPICPARENT{name="WhyDoMyETLsTakeSoLongToRun"}

# Investigating data manager for ETLs [investigating-data-manager-for-etls]

DKGRAY Authors: Main.GeraldMitchell Build basis: CLM ENDCOLOR

TOC{title="Page contents"}

This situation is to help discover the possibilities in correcting ETLs
(Extract-Transform-Load) in the situation where the ETLs seem to be
taking what is considered a longer time than expected to run and the
process is controlled by the Data Manager in Insight.

## Recommended analysis steps

#### Reporting tool specific logs

-   Data Manager logs in the reporting tool
    -   The default location of the Data Manager logs are at
        ***/cognos/datamanager/log***
    -   Check the log named Build_job_type.log, to see whether there are
        failure or how many records have been delivered.
-   Data log load: ***/cognos/datamanager/data***
-   Review the XML Data Configuration (.xdc). Make sure that the
    correct/current version catalog is used.
-   The mustgather information for Rational Insight is available from
    [Technote
    1409882](http://www-01.ibm.com/support/docview.wss?uid=swg21409882).
    This information may also be valuable if you are trying to analyze
    the ETLs and are using Insight.
    -   Rational Insight ETL logs for mustgather:
        -   The default location of the Rational Insight JDBC logs and
            Rational Insight Data Manager logs are at C:/Documents and
            Settings//logs
        -   You can change the default location by modifying the
            register of the jdbclogpath parameter in the
            HKEY_LOCAL_MACHINE/SOFTWARE/ODBC/ODBCINST.INI/IBM Rational
            insight XML ODBC Driver registry.
        -   Rational Insight Data Manager logs are located at
            /cognos/datamanager/log
        -   Rational Insight Data Manager logs for rejected data are
            located in /cognos/datamanager/data

## Possible Causes and Solutions

After reviewing the above information on assessment and analysis, you
may or maynot have found an error which correlates to the long running
ETL. If so, navigate to the following pages: **[Yes, I found an error
which could be causing the Long Running
ETL](https://jazz.net/wiki/bin/view/Deployment/LongRunningETLError)** OR
**[No, I have not found any error causing the Long Running
ETL](https://jazz.net/wiki/bin/view/Deployment/LongRunningETLNoError)**

## Keywords to aid searching

performance diagnosis delay wait ETL extract transform load data
collection job star common RTC RQM Insight JTS time delay report long
length slow freeze frozen response XDC error exception disable variable
STAR datamanager custom

##### Related topics: None [related-topics-none]

##### External links: [external-links]

-   <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/topic/com.ibm.rational.reporting.admin.doc/topics/t_running_the_data_collection_jobs.html>
-   <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/topic/com.ibm.rational.reporting.admin.doc/topics/c_data_collection.html>
-   <http://en.wikipedia.org/wiki/Extract,_transform,_load>

##### Additional contributors: None [additional-contributors-none]
