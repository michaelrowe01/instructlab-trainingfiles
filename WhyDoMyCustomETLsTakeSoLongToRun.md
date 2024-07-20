META:TOPICINFO{author="sbagot" date="1432663850" format="1.1"
version="1.14"} META:TOPICPARENT{name="WhyDoMyETLsTakeSoLongToRun"}

# Why do my custom ETLs take so long to run? [why-do-my-custom-etls-take-so-long-to-run]

DKGRAY Authors: Main.GeraldMitchell, Main.StephanieBagot Build basis:
CLM 4.x, 5.x ENDCOLOR

TOC{title="Page contents"}

This situation is to help determine causes where custom ETLs (Extract,
Transform, Load) take significantly longer to run than expected.

## Why do my custom ETLs take so long to run?

This situation is to help discovering ways to troubleshoot Custom ETLs
in the situation where they seem to run longer than expected. This
specific topic will cover instances when ***no error occurs***. If an
error has occurred, navigate to the [Long Running ETL with
Error](https://jazz.net/wiki/bin/view/Deployment/LongRunningETLError)
page.

## Initial assessment

After you have completed the [Initial
Troubleshooting](https://jazz.net/wiki/bin/view/Deployment/InitialTroubleshootingInvestigation),
and the [Initial
Assessment](https://jazz.net/wiki/bin/view/Deployment/WhyDoMyETLsTakeSoLongToRun)
ETL specific questions, you have been unable to identify any errors or
other unexpected behaviour which is causing the long running ETL. This
page will help to point you to where to investigate next.

## Possible causes and solutions

1\. Running the latest ETLs will take advantage of any performance
increases available in a later version. As an example, significant
improvements were made to the performance of the general ETL processes
between 3.x and 4.x including the processes running the custom ETLs.
Future updates may also improve performance.

2\. Using integrations such as Requisite Pro or ClearQuest, the order
can have a significant impact on the amount of data loaded (or loaded
twice). The order of the Data Collection Jobs should be set to gather
the information for the integrations before the CLM application ETLs so
that the links are retained, and that any custom ETLs come after the
data used by that ETL has been processed by its dependencies. This step
will need to be completed by the administrator/creator of the custom
ETLs. Since this is a custom ETL, we cannot provide any information on
ensuring the configuration is 'correct' as we do not know the details.

3\. Design the queries such that they run against the data warehouse
instead of against the LIVE application database.

Also, any causes and solutions for the Out Of The Box ETL that are long
running are relevant to Custom ETLs as well. For more information, see
the following pages: **[Yes, I found an error which could be causing the
Long Running
ETL](https://jazz.net/wiki/bin/view/Deployment/LongRunningETLError)** OR
**[No, I have not found any error causing the Long Running
ETL](https://jazz.net/wiki/bin/view/Deployment/LongRunningETLNoError)**

### Custom ETL strategy

Considering the strategy of the ETL is important to the speed.

#### Example from RQM 3.0.1.3

The following example is from RQM 3.0.1.3 but is applicable to any
creation or modification of an ETL XDC. The default XDC for RQM prior to
3.0.1.3 caused the ETLs to iterate over each project on the server one
by one, thus retrieving resources individually for each project. With
the newer XDC file, the ETL will retrieve resources of all projects
areas in one pass. The results of this change is that there are not
iterations to the driver, and so it removes the overhead of the
iteration. Because there is a driver associated with a retrieval that
requires an initialization, there is an initialization overhead for
every round-trip to the application server. Every driver would have an
initial start up overhead. There is also another overhead cost either an
additional overhead per use or the same initial start up overhead. This
depends on the native nature of the driver and the driver design. For
all resources of one project, this overhead could add up quickly for
each project. In addition, creating the connection has networking
overhead as well. The new ETL strategy was to minimize the server
round-trips and therefore saves this initialization time. For many
projects, this could save up to hours for every delta or full ETL run.
The disadvantage of having a comprehensive single resource load strategy
is that in case of an error during the load, the subsequent reload after
the error correction would require much more data than you would for a
project by project approach where you would be able to pick up from the
project that has failed. In addition the affect of each pull to the
database is not as controllable and the amount of data in a single pull
is not as compacted, which for very large ETLs may cause a bandwidth
related issue. Source: [Release notes for reporting improvements in RQM
3.0.1.3](https://jazz.net/downloads/rational-quality-manager/releases/3.0.1.3?p=news#reporting)

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
