META:TOPICINFO{author="sbagot" date="1432663745" format="1.1"
reprev="1.23" version="1.23"}
META:TOPICPARENT{name="WhyDoMyETLsTakeSoLongToRun"}

# Long-running ETLs with error(s) [long-running-etls-with-errors]

DKGRAY Authors: Main.GeraldMitchell, Main.StephanieBagot Build basis:
CLM 4.x, 5.x; and supported versions of Insight, RRDI, Requisite Pro,
ClearQuest ENDCOLOR

TOC{title="Page contents"}

This situation is to help determine both cause and resolution where ETL
(Extract, Transform, Load) processes take significantly longed than
expected to run and there is an error present.

## Why do my ETLs take so long to run?

This situation is to help discover the possibilities in correcting ETLs
in the situation where the ETLs seem to be taking what is considered a
longer time than expected to run. This specific topic will cover
instances when an ***error does occur***.

Keep in mind that many errors and failures are not fatal: the jobs may
run or trigger a different result as a consequence of the failure.

If no error has been found or occurred, navigate to the [Long Running
ETL without an
Error](https://jazz.net/wiki/bin/view/Deployment/LongRunningETLNoError)
page.

## Initial Assessment

After you have completed the [Initial
Troubleshooting](https://jazz.net/wiki/bin/view/Deployment/InitialTroubleshootingInvestigation),
and the [Initial
Assessment](https://jazz.net/wiki/bin/edit/Deployment/WhyDoMyETLsTakeSoLongToRun)
ETL specific questions, you have identified an error which you have
determined to be the root cause of the long running ETL. While typically
an error would stop the ETLs from continuing, in some cases, the ETLs
will attempt to continue after the error until completion, thus
resulting in the ETL running for much longer than expected.

## Possible causes and solutions

### There is too much data collected by the job

-   Delivery of data into the data warehouse is slow when projects
    contain more data than can be delivered by the ETL within the time
    limit imposed by HTTP. The HTTP connection used by the JDBC driver
    for delivering data can even be interrupted due to HTTP timeout.
    This can be seen when the JDBC driver records a
    "java.io.IOException: Premature EOF" exception and some of the ETL
    builds fail. This may be intermittent due to network conditions, CLM
    usage, and other environment and system states, as well as the data
    contents. It is possible to reduce the data delivered by customizing
    the ETL process to deliver raw data directly to a temporary table
    and then to separately transform that data into the target table.
    This requires the creation of a temporary table with the correct
    privileges, configuring the application server, customizing the ETL
    process, and executing the ETL job. See the [technote
    1455870](http://www-01.ibm.com/support/docview.wss?uid=swg21455870)
    for an example of Insight and Requisite Pro, though the general
    principal applies to all applications and data warehousing. The HTTP
    connection is governed by a timeout default that can be adjusted for
    the sender and receiver in the HTTP and application server such that
    no HTTP timeout occurs and there is not JDBC driver interruption.
-   The communication timeout issues may also be related to the LPTA
    timeout especially if the CLM servers on in an enterprise topology
    or using proxies. This is most obvious in the application server
    standard out logs where an error such as SECJ0371W: Validation of
    the LTPA token failed because the token expired can be seen. The
    LPTA may be tweaked in the web and application server settings. For
    example, in WebSphere Application Server 7.0 or higher has a LTPA
    Timeout setting that can be accessed the console's Global security
    \> Administrative authentication \> LTPA panel. The LTPA Timeout
    value for forwarded credentials between servers field can be
    adjusted to 240 or higher to yield better results for RQM. See
    [Technote
    1454016](http://www-01.ibm.com/support/docview.wss?uid=swg21454016)
    for more information.
-   If there are ETL error logs relating to connection resets or other
    networking impediments and the database logs show system resource
    errors, the database may need tuned or start to hit system
    limitations. As an example, when CLM Reporting Jobs are executed for
    a very large repository data set (more than 500000 records) on a
    32-bit environment, the jobs may fail after a few hours due to
    limited system resources such as seen in [Technote
    1503427](http://www-01.ibm.com/support/docview.wss?uid=swg21503427).

### Too many other jobs are running and causing errors or failures

-   There are jobs being run which are not necessary. Jobs that are
    duplicated or run too often can slow performance. It is best to only
    run jobs right before they are needed to get the latest information.
    It is also best to run with deltas when possible.
    -   Example: The ANALYZE_TABLE command is already run by the ETL
        jobs, so it is redundant to have it run twice. The ANALYZE_TABLE
        command can be disabled through a new parameter in the Data
        Warehouse connection page named: Automatically update the
        database statistics. Source: [Technote
        1590790](http://www-01.ibm.com/support/docview.wss?uid=swg21590790)

### Something in the data is causing failure

-   It could be that some numbers were hitting a value threshold and the
    error threshold has been disabled. If the error limit has not been
    hit, the job will not fail but the logging will have been impacted
    and the performance might degrade. With no error threshold, the
    errors would continue to occur indefinitely. Depending on the impact
    of the numbers to their usage, these errors may cause a performance
    degradation.
    -   Example: High value numbers (greater than 99,999,999) or numbers
        with a precision greater than in the repository used to cause
        issues with the data warehouse. See [technote
        1551425](http://www-01.ibm.com/support/docview.wss?uid=swg21551425).
        If the repository contains high numbers, they can be ignored
        during the ETL process and not loaded into the data warehouse.
        This means those numeric values will not be available for the
        metrics reporting. Disable the error threshold for the ETL jobs.
        The ETL logs need to be checked thoroughly and periodically to
        make sure no other types of non-fatal errors are ignored. To
        enable the error threshold for the Requirements ETL jobs: as a
        JazzAdmins user access the JTS admin URL, choose "Jazz Team
        Server - Server Administration" and then the "Advanced
        Properties" section. Change the "Requirements Job Threshold"
        property value to from -1 (disabled) to a reasonable number and
        restart the server.

### Something with a job is causing failure

-   The user id the job is using is not allowed
    -   Correct user id permissions
        -    The user ids need permissions in all applications for which
            the ETL will touch, including the JTS.
        -    Assure that the user ids are assigned the correct licenses.
        -    Make sure to assign the data collection user with both the
            "JazzAdmins" repository permission and the "Data Collector"
            license.
    -    Check for the user id to have the permission appropriate to the
        project areas used in each connected application.
        -    Make sure that the user id does not have special characters
            in the id, such as - (dash).
        -   The user ids spelling and password need to be validated.
        -   For example, using a corporate policy for some directory
            services require that the password expires every 90 days,
            and that automated ids be named a specific structure related
            to its purpose. If the directory service administrator audit
            revealed an irregularity, it is possible the id has been
            removed, frozen or locked out.
        -   Remove the LDAP for the User ID (see [Technote
            1609143](http://www-01.ibm.com/support/docview.wss?uid=swg21609143))
            For the Common ETL job there are sometimes errors that are
            intermittent that will cause a failure and possibly be
            missed. When the data collection jobs are run, all jobs
            succeed except for the Common jobs. Common ETL jobs fail
            with an error: CRRRE1404E: The user or password is invalid
            The problem could be due to JTS losing connection to the
            LDAP server at that time, so that change and configuration
            management (CCM) is not able to authenticate the LDAP user
            ID used to run the ETL tasks. If a proxy server is in place,
            it could be due to a failing connection between CCM and JTS
            through the proxy server. An internal functional ID can be
            used to run the ETL Data Collection jobs instead of a real
            LDAP ID. This will result in not using the LDAP server and
            save the time in connection and any validations related to
            the LDAP.
            1.  Navigate to jts/admin \> Server \> Consumers. Create and
                register a new consumers key. Set the etl_user as the
                function user. 2. Navigate to jts/admin \> Reports \>
                Datawarehouse Connection. Enter the consumer key and
                secret for the connection properties. Change the XDC
                Authentication Type from "Form" to "JTS". 3. Navigate to
                jts/admin \> Reports \> Data Collection Jobs. Enter the
                newly created Consumer Key and secret. Note that as seen
                in [ technote
                1591743](http://www-01.ibm.com/support/docview.wss?uid=swg21591743).
                changing the authentication type from LDAP to the
                internal authentication for the Data Collection User
                results in the Data Collection Jobs possibly having
                issues; manually reconfigure the Data Collection User in
                each application.
-   RTC Loop jobs may have unreported failures [Technote
    1515487](http://www-01.ibm.com/support/docview.wss?uid=swg21515487)
    In IBM Rational Insight, running published ETLs against RTC with
    multiple databases reports job succeeded and the Loop jobs will
    report success, but the ETL job logs may contain errors errors if a
    failure occurs with parts of the job.
-   Data collection job variables need to be reviewed and corrected
    -    Disabled jobs need to result in a passed
    -    Failure to have disabled jobs result in a pass will result in a
        full load and wipe out the current data, resulting in a long
        standing full load operation every run, instead of a delta.
    -    Example: a XDC for Requisite Pro disables a build node result
        variable. The disable does not return in a valid response. This
        resulted in a failure and so caused a full ETL load to occur,
        for every run. The full run instead of the delta run takes
        magnitudes more time and also blocks other ETLs dependent on
        that data to run.
-   Data collection jobs need to be run in a specific order
    -    Data collections for older applications (such as Requisite Pro
        or ClearQuest) are recommended to run before the newer CLM
        applications (JTS, RQM)
-   ETLs on specific data shouldn't be attempted at the same time.
    -   The ETL is data dependent and so should be treated as a queue.
        Only one ETL should be scheduled at a time.
-   Run a full data collection job to gather all new data from your
    repository. **NOTE: This may take significantly longer than the
    typical data collection job run (which is only incremental).**

### Check the integrations with other projects

Sometimes data and jobs that are integrated with other applications can
have conflicts with timing, become queued in deadlock, or have other
issues. Assure that all of the jobs and data are necessary for the
functionality desired and that any custom ETL work has been vetted for
timing and logic against the other ETLs.

#### Insight ETL Hangs

There is a known issue with Insight ETLs hanging on Oracle databases.
For more information, see [Technote 1638341: ETL hangs when delivering
data to an Oracle data
warehouse](http://www-01.ibm.com/support/docview.wss?uid=swg21638341).

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
-   <http://pic.dhe.ibm.com/infocenter/rentrpt/v1r1m1/topic/com.ibm.rational.raer.integration.doc/topics/t_integrate_data_source_rtc_etl.html>

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="ConsumerKey.jpg" attachment="ConsumerKey.jpg"
attr="h" comment="Consumer Key" date="1361897461" path="ConsumerKey.jpg"
size="13197" user="sbagot" version="1"}
META:FILEATTACHMENT{name="DataCollectionJobs.jpg"
attachment="DataCollectionJobs.jpg" attr="h" comment="Data Collection
Job Screenshot" date="1361897493" path="DataCollectionJobs.jpg"
size="76076" user="sbagot" version="1"}
META:FILEATTACHMENT{name="DataCollectionJobStatus.jpg"
attachment="DataCollectionJobStatus.jpg" attr="h" comment="Data
Collection Job Status Screenshot" date="1361897517"
path="DataCollectionJobStatus.jpg" size="124286" user="sbagot"
version="1"}
