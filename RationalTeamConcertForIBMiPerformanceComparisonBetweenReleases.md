META:TOPICINFO{author="bjsuhui" date="1450343296" format="1.1"
version="1.11"} META:TOPICPARENT{name="RTCEEDepBuildTests"}

# Rational Team Concert For IBMi Performance Comparison Between Releases [rational-team-concert-for-ibmi-performance-comparison-between-releases]

DKGRAY Authors: Main.LuLu Main.SuHui Date: Jun 25th, 2015 Build basis:
Rational Team Concert for IBMi 5.0.2, 6.0, 6.0.1 ENDCOLOR

TOC{title="Page contents"}

## Introduction

This report compares the performance of RTC for IBMi between releases
since v5.0.2 until v6.0.1. Generally constant performance improvements
are made into releases of RTC on IBMi. The objective of this report is
to present the improvements.

The performance data provided is obtained by benchmark test of each
release. Currently the report includes only the build information.

## Disclaimer

INCLUDE{"PerformanceDatasheetDisclaimer"}

## Findings

Based on the test data, build performance of the RTC for IBMi has
improved significantly from 5.0.2 to 6.0, based on the new build map
mechanism.

From **5.0.2 to 6.0**, the big improvement is on 'collecting buildable
file' activity of 'preprocessing' period, after changing all RPG files
of MaillistX100 sample project, 'collecting buildable file' activity
takes **5 minutes** in v6.0 which takes **2 hours and 30 minutes** in
v5.0.2, improved almost **95+**.

From **6.0 to 6.0.1**, 'Updating dependency data' has an improvement of
**more than 60**. This is a result of performance improvement of source
code data scan.

## Topology

The tests are executed in a Single Tier Topology infrastructure like the
one in the following diagram: INCLUDE{"RTCEETestingTopologies"
section="SingleTierI"}

The RTC server was set up based on WebSphere on IBMi. The build machine
with Rational Build Agent was on IBMi.

Test Environment

RTC Server Operating System & Version: IBMi v7.1 System Resource : 4
dedicated processors, 30GB memory CLM: from 5.0.2 GA to 6.0.1 GA, 6 GB
heap size DB2: DB2 for IBMi v7.1 WAS: 8.5.5.3(from 5.0.2 GA to 6.0 GA),
8.5.5.7(from 6.0GA to 6.0.1 GA)

Build Forge Agent Operating System & Version: IBMi v7.1 System Resource:
4 dedicated processors, 30GB memory Build System Toolkit: from 5.0.2 GA
to 6.0.1 GA

## Methodology

Build time and individual activity time are compared by getting test
start date and time.

The sample projects for the test are:

-   Maillist Application \*100
-   Maillist Application \*1000

Test Data

Sample Project Maillist \*100 Maillist \*1000

Assets 500 RPGLE 200 SRVPGM 100 PGMSRC 4 DSPF 4 LF 2 PF 6 CLLE 1 \* CLP

5000 RPGLE 2000 SRVPGM 1000 PGMSRC 4 DSPF 4 LF 2 PF 6 CLLE 1 \* CLP

Total Assets 817 buildable file

8017 buildable file

In the repository the source code is stored in one stream with one
single component.

Enterprise builds are executed twice against each version.

## Results

**Note : since 6.0.1 benchmark , we have replaced our IBMi performance
testing LPARs and new performance baselines are created. 6.0 benchmark
have been re-run to compare on identical hardware.**

### Run duration

The charts below shows the run duration comparison between v5.0.2 and
v6.0, and from v6.0 to v6.0.1. Builds are run twice against each release
and the average time is taken for comparison.

Following table displays build test result with release by release
comparison:

### Build Activities

The chars below display the run times of build activity "Collecting
buildable files" and "Compile" which have gained some improvements
between releases. Builds are run twice against each release and the
average time is taken for comparison.

For the full build activity run time details, please refer to following
tables:

Detailed build activities comparison can be found
[here](RTCiFullBuildActivities).

## Appendix A - Key Tuning Parameters

Product Version Highlights for configurations under test

IBM WebSphere Application Server 8.5.5.3 (5.0.2GA to 6.0GA),
8.5.5.7(from 6.0GA to 6.0.1 GA) JVM settings:

\* GC policy and arguments, max and init heap sizes:

-Xmn768m -Xgcpolicy:gencon -Xcompressedrefs
-Xgc:preferredHeapBase=0x200000000 -Xmx6g -Xms6g

DB2 DB2 Enterprise Server for IBM v7.1 Tablespace is stored on the same
machine as IBM WebSphere Application Server

License Server Same as CLM version Hosted locally by JTS server

Network

Shared subnet within test lab

#### About the authors [about-the-authors]

Main.LuLu

--------------------

##### Questions and comments: [questions-and-comments]

-   What other performance information would you like to see here?
-   Do you have performance scenarios to share?
-   Do you have scenarios that are not addressed in documentation?
-   Where are you having problems in performance?

COMMENT{type="below" target="PerformanceDatasheetReaderComments"
button="Submit"}

INCLUDE{"PerformanceDatasheetReaderComments"}

META:FILEATTACHMENT{name="runtime.png" attachment="runtime.png" attr="h"
comment="build run time" date="1435560760" path="runtime.png"
size="13505" user="rucielulu" version="1"}
META:FILEATTACHMENT{name="compile.jpg" attachment="compile.jpg" attr="h"
comment="" date="1435561387" path="compile.jpg" size="63970"
user="rucielulu" version="1"}
META:FILEATTACHMENT{name="collectingBuildFile.jpg"
attachment="collectingBuildFile.jpg" attr="h" comment=""
date="1435561409" path="collectingBuildFile.jpg" size="56947"
user="rucielulu" version="1"} META:FILEATTACHMENT{name="runtime_2.png"
attachment="runtime_2.png" attr="h" comment="" date="1450255568"
path="runtime_2.png" size="19020" user="bjsuhui" version="2"}
META:FILEATTACHMENT{name="compile_2.png" attachment="compile_2.png"
attr="h" comment="" date="1450255532" path="compile_2.png" size="18044"
user="bjsuhui" version="2"}
META:FILEATTACHMENT{name="collectingBuildFile_2.png"
attachment="collectingBuildFile_2.png" attr="h" comment=""
date="1450255481" path="collectingBuildFile_2.png" size="17703"
user="bjsuhui" version="2"}
