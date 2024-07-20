META:TOPICINFO{author="tfeeney" date="1595448186" format="1.1"
reprev="1.2" version="1.2"} META:TOPICPARENT{name="MBeansUsage"}

# Collecting basic health check metrics using JMX MBeans DKGRAY Authors: Main.TimFeeney Build basis: 6.0.6.1 and later [collecting-basic-health-check-metrics-using-jmx-mbeans-dkgray-authors-main.timfeeney-build-basis-6.0.6.1-and-later]

ENDCOLOR

TOC{title="Page contents"}

The ELM application provides a basic [health check
widget](PerformanceHealthCheckWidget) you can add to a dashboard. In
addition, there a few different MBeans you can monitor related to base
application health.

### Server Information MBean

The bean provides some health information for the server running the
application. Of most interest are:

-   ***dbConnectionStatus*** - indicates if the status of the
    application's connection to the database
-   ***dbPingTime*** - a measure of the latency between the application
    and database

A working and low latency connection to the database are essential to
the application providing a good quality of service. Monitor these
attributes to detect if the connection fails or the latency degrades
appreciably over time.

### Repotools Verify Information MBean

This bean provides the results of an online verify that checks the
integrity of an application's production database. There are several
verifiers that execute, for each, the attributes to watch are

-   ***componentId*** - identifies the validator being run
-   ***statusCode*** - indicates the result of the particular verifier
-   ***severity*** - provides an assessment of the severity of
    verification results, eg. OK, WARNING, ERROR and others.

This is a resource intensive scenario so should be run infrequently and
during off hours. Monitor the results to detect any reported errors to
further investigate, with IBM Support, as needed.

### Diagnostics MBean

Server diagnostics can be run regularly to analyze many aspects of the
server so as to quickly identify problems. There are several tests that
execute, for each, the attributes to watch are

-   ***testId*** - the test that ran
-   ***status*** - the overall status of the test execution
-   ***statusDesc*** - short description of the test results
-   ***detailStatusDesc*** - more information about the test results

Monitor the results to detect any reported errors to further
investigate, with IBM Support, as needed. Use of this bean is also
described in [CLM Monitoring](https://jazz.net/library/article/91590).

### LogEvents MBean

This bean tracks error and warning messages captured in the application
log file. Key errors to watch for are documented in [Monitoring error
messages](MonitoringLoggedErrorMessages). Occurrence of these messages
should be investigated, with IBM Support, as needed.

Some useful attributes include

-   ***errorId*** - the ID of the error
-   ***errorTitle*** - title of the error
-   ***errorDetails*** - additional details for the error
-   ***userId*** - the user involved in the request that resulted in the
    error

Some clients have log parsing enabled in their application monitoring
environment. These likely provide a more robust capability than what
this MBean provides.
