META:TOPICINFO{author="rucielulu" date="1450245683" format="1.1"
version="1.12"} META:TOPICPARENT{name="RTCEEPerfTestsData"}

# Rational Team Concert For z/OS Incremental Build Performance Comparison Between Releases [rational-team-concert-for-zos-incremental-build-performance-comparison-between-releases]

DKGRAY Authors: Main.SuHui Main.LuLu Date: Nov 24th, 2014 Build basis:
Rational Team Concert for z/OS 4.0.2, 4.0.3, 4.0.4, 4.0.5, 4.0.6, 5.0,
5.0.1, 5.0.2, 6.0, 6.0.1 ENDCOLOR

TOC{title="Page contents"}

## Introduction

This report compares the incremental build performance of RTC for z/OS
between releases since v4.0.2 until v6.0.1. Generally constant
performance improvements are made into releases of RTC for z/OS. The
objective of this report is to present the improvements.

The performance data provided is obtained by benchmark test of each
release. The report includes build duration and links to the detailed
build activities.

## Disclaimer

INCLUDE{"PerformanceDatasheetDisclaimer"}

## Findings

Based on the test data, incremental build performance of the RTC for
z/OS has improved significantly from 4.0.2 to 6.0.1.

-   From **4.0.2 to 5.0.2**, the overall improvement of the build time
    is about **30 to 50** depending on different test scenarios.
-   From **5.0.2 to 6.0**, the time of incremental build with large
    change set improved more than **20**. "Collecting buildable files"
    and "Updating dependency data" activities during build preprocessing
    are the main improved activities.
-   From **6.0 to 6.0.1**, "Updating Dependency data" activity is
    improved 120 and 'Compile' activity is improved 6.

Constant performance enhancements have been made into release 4.0.3,
4.0.5, 4.0.6, 5.0, 6.0 and 6.0.1 to improve the build preprocessing
speed.

## Topology

The tests are executed in a Single Tier Topology infrastructure like the
one in the following diagram: INCLUDE{"RTCEETestingTopologies"
section="SingleTierZ"}

The RTC server was set up based on WebSphere and DB2 on Linux for System
z. The build machine with Rational Build Agent was on zOS.

Test Environment

RTC Server Operating System & Version: Linux for System z (SUSE Linux
Enterprise Server 10 (s390x)) System Resource : 10 GB Storage, 4 CPs
(20000 mips, CPU type : 2097.710, CPU model: E12) CLM: from 4.0.2 GA to
6.0.1 GA, 4 GB heap size DB2: 9.7.0.5 (from 4.0.2 GA to 4.0.6 GA),
10.1.0.0(5.0 GA to 6.0.1 GA) WAS: 8.0.0.3 (from 4.0.2 GA to 4.0.5 GA),
8.5.5.1 (from 4.0.6 GA to 6.0.1 GA)

Build Forge Agent Operating System & Version: z/OS 01.12.00 System
Resource: 6 GB Storage, 4 CPs (20000 mips, CPU type : 2097.710, CPU
model: E12) Build System Toolkit: from 4.0.2 GA to 6.0.1 GA

## Methodology

Build time and individual activity time are compared by getting test
start date and time.

The sample projects for the test are:

-   Mortgage Application \*100 which is 100 duplicates of the [Mortgage
    sample
    application](https://jazz.net/wiki/bin/view/Main/ZOSBuildSamplesV4)
-   Mortgage Application \*1000 which is 1000 duplicates of the
    [Mortgage sample
    application](https://jazz.net/wiki/bin/view/Main/ZOSBuildSamplesV4)

Test Data

Sample Project Mortgage\*100 Mortgage\*1000

Assets 600 COBOL programs 400 Copybooks 200 BMS3 others

6000 COBOL programs 4000 Copybooks 2000 BMS3 others

Total Assets 1203

12003

In the repository the source code is stored in one stream with one
single component which includes 5 zComponent Projects.

Enterprise builds are executed twice against each version.

### Test Scenario Description

After a complete build of all the programs, different changes are
performed and a rebuild requested. These requests will rebuild the
changed programs and impacted ones.

Test Scenario Description

Incremental Build 1. Change a copybook
(MortgageApplication-Common\zOSsrc\COPYBOOK\A00MTCOM.cpy) and request
build2. Change a COBOL file
(MortgageApplication-EPSCMORT\zOSsrc\COBOL\A00CMORT.cbl) and request
build3. Change all copybooks and request build3. Change all COBOL files
and request build

## Results

### Run duration & Build Activities

The charts below show the run duration comparison from 4.0.2 until
6.0.1. Builds are run twice against each release and the average time is
taken for comparison. From **4.0.2 to 5.0.2**, the overall improvement
of the build time is from about **30 to 50**. From **5.0.2 to 6.0**, the
time of incremental build with large change set improved more than
**20**. Links to the individual pages are provided for the detailed
build activities.

#### Change a copybook file and execute build

Detailed build activities comparison for this test scenario "Change a
copybook file and execute build" can be found
[here](RTCEEIncrementalBuildActivitiesOneCopybook).

#### Change a COBOL file and execute build

Detailed build activities comparison for this test scenario "Change a
COBOL file and execute build" can be found
[here](RTCEEIncrementalBuildActivitiesOneCobol).

#### Change all copybook files and execute build

Detailed build activities comparison for this test scenario "Change all
copybook files and execute build" can be found
[here](RTCEEIncrementalBuildActivitiesAllCopybook).

#### Change all COBOL files and execute build

This test scenario is designed and executed from 4.0.6 release.

Detailed build activities comparison for this test scenario "Change all
COBOL files and execute build" can be found
[here](RTCEEIncrementalBuildActivitiesAllCobol).

## Appendix A - Key Tuning Parameters \#AppendixC

Product Version Highlights for configurations under test

IBM WebSphere Application Server 8.0.0.3 (4.0.2GA to 4.0.5GA), 8.5.5.1
(4.0.6GA to 6.0.1GA) JVM settings:

\* GC policy and arguments, max and init heap sizes:

-Xmn512m -Xgcpolicy:gencon -Xcompressedrefs
-Xgc:preferredHeapBase=0x100000000 -Xmx4g -Xms4g OS configuration:

\* hard nofile 120000 \* soft nofile 120000 Refer to
<http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m4/topic/com.ibm.jazz.install.doc/topics/c_special_considerations_linux.html>
for details

DB2 DB2 Enterprise Server 9.7.0.5 (4.0.2GA to 4.0.6GA), 10.1.0.0 (5.0GA
to 6.0.1GA) Tablespace is stored on the same machine as IBM WebSphere
Application Server

License Server Same as CLM version Hosted locally by JTS server

Network

Shared subnet within test lab

#### About the authors [about-the-authors]

Main.SuHui Main.LuLu

--------------------

##### Questions and comments: [questions-and-comments]

-   What other performance information would you like to see here?
-   Do you have performance scenarios to share?
-   Do you have scenarios that are not addressed in documentation?
-   Where are you having problems in performance?

COMMENT{type="below" target="PerformanceDatasheetReaderComments"
button="Submit"}

INCLUDE{"PerformanceDatasheetReaderComments"}

META:FILEATTACHMENT{name="onecopybook.gif" attachment="onecopybook.gif"
attr="h" comment="" date="1449823328" path="onecopybook.gif"
size="17903" user="rucielulu" version="4"}
META:FILEATTACHMENT{name="onecobol.gif" attachment="onecobol.gif"
attr="h" comment="" date="1449823452" path="onecobol.gif" size="16848"
user="rucielulu" version="4"} META:FILEATTACHMENT{name="allcopybook.gif"
attachment="allcopybook.gif" attr="h" comment="" date="1449823576"
path="allcopybook.gif" size="16965" user="rucielulu" version="4"}
META:FILEATTACHMENT{name="allcobol.gif" attachment="allcobol.gif"
attr="h" comment="" date="1449823673" path="allcobol.gif" size="16000"
user="rucielulu" version="4"}
