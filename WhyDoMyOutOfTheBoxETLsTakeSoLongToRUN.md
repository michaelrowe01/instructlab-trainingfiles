META:TOPICINFO{author="sbagot" date="1432663941" format="1.1"
version="1.13"} META:TOPICPARENT{name="WhyDoMyETLsTakeSoLongToRun"}

# Why do my out of box ETLs take so long to run? DKGRAY Authors: Main.GeraldMitchell, Main.StephanieBagot Build basis: CLM 4.x, 5.x [why-do-my-out-of-box-etls-take-so-long-to-run-dkgray-authors-main.geraldmitchell-main.stephaniebagot-build-basis-clm-4.x-5.x]

ENDCOLOR

TOC{title="Page contents"}

This situation is to help determine causes where out of box ETLs
(Extract, Transform, Load) take significantly longer to run than
expected.

## What is my ETL doing?

See the parent topic [Why do my ETLs Take so Long to
Run?](https://jazz.net/wiki/bin/view/Deployment/WhyDoMyETLsTakeSoLongToRun)
for an explanation of ETL activity.

## Initial Assessment

See the parent topic [Why do my ETLs Take so Long to
Run?](https://jazz.net/wiki/bin/view/Deployment/WhyDoMyETLsTakeSoLongToRun)
for an exaplanation of how to do initial assessment on ETLs.

## Recommended analysis steps

### Determine that the ETL jobs have successfully completed. Jobs can be started from JTS but each application server, including the JTS, will only display the status of the local jobs. To see the status of a specific data collection job, you must use the Administration page of the application, select the Reports page, and choose the Data Collection Job Status link. The status of the data collection jobs is shown in the order in which they are run. The Data Collection Job Status page under the Server Administration (JTS, CCM, and QM applications) can be accessed directly using

<https://://admin#action=com.ibm.team.reportsManagement.etlStatus>

Errors may be indicated by a Failed status on the Data Collection job
Status page

### Determine that the user ID's are correct

-   Assure that the correct ids are used to run the ETLs and that those
    ids have the correct and enabled licenses. \* The Jazz Reporting
    should be configured as a Consumer (Inbound) for each application
    (JTS, CCM, and QM) with a username. Out of box, this username is
    identified as etl_user. \* The consumer Key should also be listed as
    the consumer key on the Data Collection Jobs page (screenshot
    above).
    -   This user should have the Data Collector Client Access License
        assigned.

### Disabled jobs Look for Jobs that have been disabled. This can be done on the Data Collection Jobs page under the Server Administration (JTS, CCM, and QM applications)

<https://://admin#action=jazz.viewPage&id=com.ibm.team.reports.reportsManagementPage>
The screenshot below shows that all Data Collection Jobs for the JTS
have been enabled.

### Review the Log files

View the ETL logs and look for the information on the Data collection
jobs. Check the application log files (qm-etl.log, jts-etl.log,
ccm-etl.log, jazz-etl.log) in the following log directory:
/logs/\*-etl.log See [How do I read the ETL
Logs](https://jazz.net/wiki/bin/view/Deployment/HowToReadETLLogFile) for
more information.

### Advanced analysis

----++++ Debugging using the ETL SELECT statements ETL steps often
contain SQL SELECT statements. The result set from these steps can be
useful for problem determination as well as the length of time a certain
transaction should take. Keep in mind that with ETL, the SQL Statements
will only encompass the 'Extract' phase. When you run the SELECT
statements manually, this will only show the transactional time and
should not be used as a baseline for how long the ETL should take as the
data will still transform and load into the Data Warehouse database. See
[Technote
1116474](http://www-01.ibm.com/support/docview.wss?uid=swg21116474) for
more information. ----++++ Reviewing the Active Services When the ETL is
running, you can check the Active Services page on the JTS to determine
the exact service which is being run, and for how long. This will
provide more information than the Data Collection Job Status page.
**NOTE:** When an ETL job is started manually, the name of the service
will differ than if the ETL job is started automatically through the
nightly service. Below is a screenshot of the Active Services when
running the ETL jobs manually:

## Possible causes and solutions

After reviewing the above information on assessment and analysis, you
may or may not have found an error which correlates to the long running
ETL. If so, navigate to the following pages: **[Yes, I found an error
which could be causing the Long Running
ETL](https://jazz.net/wiki/bin/view/Deployment/LongRunningETLError)** OR
**[No, I have not found any error causing the Long Running
ETL](https://jazz.net/wiki/bin/view/Deployment/LongRunningETLNoError)**

##### Related topics: [related-topics]

-   Still need help troubleshooting your performance issue? Refer to
    [Performance Troubleshooting](PerformanceTroubleshooting) for
    additional topics.
-   [How to read ETL log files](HowToReadETLLogFile)
-   [Why do my OOB ETLs take so long to
    run?](WhyDoMyOutOfTheBoxETLsTakeSoLongToRUN)
-   [Why do my custom ETLs take so long to
    run?](WhyDoMyCustomETLsTakeSoLongToRun)
-   [Long-running ETLs with error(s)](LongRunningETLError)
-   [Long-running ETLs without error(s)](LongRunningETLNoError)

##### External links: [external-links]

-   <http://en.wikipedia.org/wiki/Extract,_transform,_load>
-   <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/topic/com.ibm.rational.reporting.admin.doc/topics/t_running_the_data_collection_jobs.html>
-   <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/topic/com.ibm.rational.reporting.admin.doc/topics/c_data_collection.html>

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="ConsumerKey.jpg" attachment="ConsumerKey.jpg"
attr="h" comment="Consumer Key" date="1362595859" path="ConsumerKey.jpg"
size="13197" user="sbagot" version="1"}
META:FILEATTACHMENT{name="DataCollectionJobs.jpg"
attachment="DataCollectionJobs.jpg" attr="h" comment="Data Collection
Job" date="1362595877" path="DataCollectionJobs.jpg" size="76076"
user="sbagot" version="1"}
META:FILEATTACHMENT{name="DataCollectionJobStatus.jpg"
attachment="DataCollectionJobStatus.jpg" attr="h" comment="Job Status"
date="1362595892" path="DataCollectionJobStatus.jpg" size="124286"
user="sbagot" version="1"}
META:FILEATTACHMENT{name="ActiveService_Manual.jpg"
attachment="ActiveService_Manual.jpg" attr="h" comment="Active
Services - Manual run of ETL" date="1365527060"
path="ActiveService_Manual.jpg" size="43899" user="sbagot" version="1"}
