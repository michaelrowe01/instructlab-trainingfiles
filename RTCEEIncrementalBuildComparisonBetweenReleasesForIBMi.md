META:TOPICINFO{author="bjsuhui" date="1450335163" format="1.1"
version="1.5"} META:TOPICPARENT{name="RTCEEDepBuildTests"}

# Rational Team Concert For IBMi Incremental Build Performance Comparison Between Releases [rational-team-concert-for-ibmi-incremental-build-performance-comparison-between-releases]

DKGRAY Authors: Main.LuLu Main.SuHui Date: June 29, 2015 Build basis:
Rational Team Concert for IBMi 5.0.2, 6.0, 6.0.1 ENDCOLOR

TOC{title="Page contents"}

## Introduction

This report compares the incremental build performance of RTC for IBMi
between releases since v5.0.2 until v6.0.1. Generally constant
performance improvements are made into releases of RTC for IBMi. The
objective of this report is to present the improvements.

The performance data provided is obtained by benchmark test of each
release. The report includes build duration and links to the detailed
build activities.

## Disclaimer

INCLUDE{"PerformanceDatasheetDisclaimer"}

## Findings

Based on the test data, incremental build performance of the RTC for
IBMi has improved significantly from 5.0.2 to 6.0.

From **5.0.2 to 6.0**, "Collecting buildable files" activities during
build preprocessing is the main improved activities based on the new
buildmap mechanism.

From **6.0 to 6.0.1**, "Collecting buildable files" activities has an
improvement of about **60** for incremental build with all the RPG files
changed. "Updating dependency data" has an improvement of **more than
60**, which is a result of performance improvement of source code data
scan.

## Topology

The tests are executed in a Single Tier Topology infrastructure like the
one in the following diagram: INCLUDE{"RTCEETestingTopologies"
section="SingleTierI"}

The RTC server was set up based on WebSphere and DB2 on IBMi. The build
machine with Rational Build Agent was on IBMi.

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

-   Mortgage Application \*100
-   Mortgage Application \*1000

Test Data

Sample Project Maillist \*100 Maillist \*1000

Assets 500 RPGLE 200 SRVPGM 100 PGMSRC 4 DSPF 4 LF 2 PF 6 CLLE 1 \* CLP

5000 RPGLE 2000 SRVPGM 1000 PGMSRC 4 DSPF 4 LF 2 PF 6 CLLE 1 \* CLP

Total Assets 817 buildable file

8017 buildable file

In the repository the source code is stored in one stream with one
single component.

Enterprise builds are executed twice against each version.

### Test Scenario Description

After a complete build of all the programs, different changes are
performed and a rebuild requested. These requests will rebuild the
changed programs and impacted ones.

Test Scenario Description

Incremental Build 1. Change one RPG file and request build2. Change all
RPG files and request build

## Results

**Note : since 6.0.1 benchmark , we have replaced our IBMi performance
testing LPARs and new performance baselines are created. 6.0 benchmark
have been re-run to compare on identical hardware.**

### Run duration & Build Activities

The charts below show the run duration comparison from 5.0.2 to 6.0, and
from 6.0 to 6.0.1. Builds are run twice against each release and the
average time is taken for comparison. From **5.0.2 to 6.0**, the
'preprocessing' of the build time is improved greatly when changing all
buildable files, 'collecting buildable file' activity is improved almost
97, total build time under this scenario is improved almost 68.

From **6.0 to 6.0.1**, "Collecting buildable files" activities has an
improvement of about **60** for incremental build with all the RPG files
changed. "Updating dependency data" has an improvement of **more than
60**.

Links to the individual pages are provided for the detailed build
activities.

#### Change one RPG file and execute build

Detailed build activities comparison for this test scenario "Change one
RPG file and execute build" can be found
[here](RTCEEIncrementalBuildActivitiesOneRPG).

#### Change all RPG files and execute build

Detailed build activities comparison for this test scenario "Change all
RPG files and execute build" can be found
[here](RTCEEIncrementalBuildActivitiesAllRPG).

## Appendix A - Key Tuning Parameters \#AppendixC

Product Version Highlights for configurations under test

IBM WebSphere Application Server 8.5.5.3 (5.0.2GA to 6.0GA),
8.5.5.7(from 6.0GA to 6.0.1 GA) JVM settings:

\* GC policy and arguments, max and init heap sizes:

-Xmn768m -Xgcpolicy:gencon -Xcompressedrefs
-Xgc:preferredHeapBase=0x200000000 -Xmx6g -Xms6g

DB2 DB2 for IBMi v7.1 Tablespace is stored on the same machine as IBM
WebSphere Application Server

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

META:FILEATTACHMENT{name="oneRPG.jpg" attachment="oneRPG.jpg" attr="h"
comment="" date="1435573089" path="oneRPG.jpg" size="66845"
user="rucielulu" version="1"} META:FILEATTACHMENT{name="allRPGs.jpg"
attachment="allRPGs.jpg" attr="h" comment="" date="1435573183"
path="allRPGs.jpg" size="62475" user="rucielulu" version="1"}
META:FILEATTACHMENT{name="allRPGs_2.png" attachment="allRPGs_2.png"
attr="h" comment="" date="1450322725" path="allRPGs_2.png" size="19424"
user="bjsuhui" version="1"} META:FILEATTACHMENT{name="oneRPG_2.png"
attachment="oneRPG_2.png" attr="h" comment="" date="1450322755"
path="oneRPG_2.png" size="16796" user="bjsuhui" version="1"}
