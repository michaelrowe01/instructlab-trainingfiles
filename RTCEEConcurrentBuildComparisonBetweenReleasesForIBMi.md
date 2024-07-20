META:TOPICINFO{author="bjsuhui" date="1450764583" format="1.1"
version="1.4"} META:TOPICPARENT{name="RTCEEConcBuildTests"}

# Rational Team Concert For IBMi Concurrent Build Performance DKGRAY Authors: Main.LuLu Main.SuHui [rational-team-concert-for-ibmi-concurrent-build-performance-dkgray-authors-main.lulu-main.suhui]

Date: June 30th, 2015 Build basis: Rational Team Concert for IBMi
version 5.0.2, 6.x ENDCOLOR

TOC{title="Page contents"}

## Introduction

This report compares the concurrent build performance of RTC for IBMi
since v5.0.2 until v6.0.1. The test include both concurrent team build
and concurrent personal build.

Based on the test data, there is a little improvement of the concurrent
build run duration, which is due to the constant performance
improvements of the dependency build feature.

The performance data provided is obtained by benchmark test of each
release. This report only includes the build run duration information.

## Disclaimer

INCLUDE{"PerformanceDatasheetDisclaimer"}

## Findings

Based on the test data, concurrent build performance of the RTC for IBMi
has improved from 5.0.2 to 6.0.1.

From **5.0.2 to 6.0**, the overall improvement of the build time is
about **5** for concurrent team build, but no obvious improvement in
concurrent personal build.

From **6.0 to 6.0.1**, the overall improvement of the build time is
about **2** for concurrent team build.

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

Build durations are compared by getting test start date and time.

The sample projects for the test are:

-   Maillist Application \*250

Test Data

Sample Project Maillist \*250

Assets 1250 RPGLE 500 SRVPGM 250 PGMSRC 4 DSPF 4 LF 2 PF 6 CLLE 1 \* CLP

Total Assets 2017

In the repository the source code is stored in one stream with one
single component which includes 5 zComponent Projects.

Every test is executed twice against each version.

### Test Scenario Description

Test Scenario Description

Concurrent Build 1. Perform two team build concurrently2. After the team
builds are completed, created five repository workspaces, change a RPG
file in each of the repository workspace3. Request five personal builds
concurrently

## Results

**Note : since 6.0.1 benchmark , we have replaced our IBMi performance
testing LPARs and new performance baselines are created. 6.0 benchmark
have been re-run to compare on identical hardware.**

### Run duration

The charts below show the build run duration comparison between 5.0.2
and 6.0, and from v6.0 to v6.0.1. Tests are run twice against each
release and the average time is taken for comparison.

From **5.0.2 to 6.0**, the overall improvement of the build time is
about **5** for concurrent team build, but no obvious improvement in
concurrent personal build.

From **6.0 to 6.0.1**, the overall improvement of the build time is
about **2** for concurrent team build.

The data in the charts are the average time of the concurrent builds.

#### Concurrent team build

In this test scenario, two team builds are requested concurrently.

#### Concurrent personal build In this test scenario, five personal build are requested concurrently after one RPG file is changed.

## Appendix A - Key Tuning Parameters \#AppendixC

Product Version Highlights for configurations under test

IBM WebSphere Application Server 8.5.5.3 (5.0.2GA to 6.0GA),
8.5.5.7(from 6.0GA to 6.0.1 GA) JVM settings:

\* GC policy and arguments, max and init heap sizes:

-Xmn768m -Xgcpolicy:gencon -Xcompressedrefs
-Xgc:preferredHeapBase=0x200000000 -Xmx6g -Xms6g

Refer to
<http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m4/topic/com.ibm.jazz.install.doc/topics/c_special_considerations_linux.html>
for details

DB2 DB2 Enterprise Server for IBMi v7.1 Tablespace is stored on the same
machine as IBM WebSphere Application Server

License Server Same as CLM version Hosted locally by JTS server

Network

Shared subnet within test lab

#### About the authors [about-the-authors]

Main.LuLu Main.SuHui

--------------------

##### Questions and comments: [questions-and-comments]

-   What other performance information would you like to see here?
-   Do you have performance scenarios to share?
-   Do you have scenarios that are not addressed in documentation?
-   Where are you having problems in performance?

COMMENT{type="below" target="PerformanceDatasheetReaderComments"
button="Submit"}

INCLUDE{"PerformanceDatasheetReaderComments"}

META:FILEATTACHMENT{name="concurrentPersonalBuild.jpg"
attachment="concurrentPersonalBuild.jpg" attr="h" comment=""
date="1435733020" path="concurrentPersonalBuild.jpg" size="49420"
user="rucielulu" version="1"}
META:FILEATTACHMENT{name="concurrentTeamBuild.jpg"
attachment="concurrentTeamBuild.jpg" attr="h" comment=""
date="1435733087" path="concurrentTeamBuild.jpg" size="49681"
user="rucielulu" version="1"}
META:FILEATTACHMENT{name="concurrentPersonalBuild_2.png"
attachment="concurrentPersonalBuild_2.png" attr="h" comment=""
date="1450693840" path="concurrentPersonalBuild_2.png" size="15592"
user="bjsuhui" version="1"}
META:FILEATTACHMENT{name="concurrentTeamBuild_2.png"
attachment="concurrentTeamBuild_2.png" attr="h" comment=""
date="1450693870" path="concurrentTeamBuild_2.png" size="18195"
user="bjsuhui" version="1"}
