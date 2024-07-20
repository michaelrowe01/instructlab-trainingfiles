META:TOPICINFO{author="rucielulu" date="1449827663" format="1.1"
reprev="1.4" version="1.4"} META:TOPICPARENT{name="RTCEEConcBuildTests"}

# Rational Team Concert For z/OS Concurrent Build Performance DKGRAY Authors: Main.SuHui Main.LuLu [rational-team-concert-for-zos-concurrent-build-performance-dkgray-authors-main.suhui-main.lulu]

Date: Dec 11, 2015 Build basis: Rational Team Concert for z/OS version
4.0.3, 5.0.1, 5.0.2, 6.0, 6.0.1 ENDCOLOR

TOC{title="Page contents"}

## Introduction

This report compares the concurrent build performance of RTC for z/OS
between release 4.0.3, 5.0.1, 5.0.2, 6.0 and 6.0.1. The test include
both concurrent team build and concurrent personal build.

Based on the test data, there is an improvement of the concurrent build
run duration, which is due to the constant performance improvements of
the dependency build feature. For more information about the dependency
build performance improvements, read the [Rational Team Concert For z/OS
Performance Comparison Between
Releases](RationalTeamConcertForZOSPerformanceComparisonBetweenReleases).

The performance data provided is obtained by benchmark test of each
release. This report only includes the build run duration information.

## Disclaimer

INCLUDE{"PerformanceDatasheetDisclaimer"}

## Findings

Based on the test data, concurrent build performance of the RTC for z/OS
has improved from 4.0.3 to 6.0.1.

From **4.0.3 to 6.0.1**, the overall improvement of the build time is
more than **36** for concurrent team build.

## Topology

The tests are executed in a Single Tier Topology infrastructure like the
one in the following diagram: INCLUDE{"RTCEETestingTopologies"
section="SingleTierZ"}

The RTC server was set up based on WebSphere and DB2 on Linux for System
z. The build machine with Rational Build Agent was on zOS.

Test Environment

RTC Server Operating System & Version: Linux for System z (SUSE Linux
Enterprise Server 10 (s390x)) System Resource : 10 GB Storage, 4 CPs
(20000 mips, CPU type : 2097.710, CPU model: E12) CLM: from 4.0.3 GA to
5.0.1 GA, 4 GB heap size DB2: 9.7.0.5 (from 4.0.3 GA to 4.0.6 GA),
10.1.0.0(from 5.0 GA to 6.0.1 GA) WAS: 8.0.0.3 (from 4.0.3 GA to 4.0.5
GA), 8.5.5.1 (from 4.0.6 GA to 6.0.1 GA)

Build Forge Agent Operating System & Version: z/OS 01.12.00 System
Resource: 6 GB Storage, 4 CPs (20000 mips, CPU type : 2097.710, CPU
model: E12) Build System Toolkit: from 4.0.3 GA to 6.0.1 GA

## Methodology

Build durations are compared by getting test start date and time.

The sample projects for the test are:

-   Mortgage Application \*250 which is 250 duplicates of the [Mortgage
    sample
    application](https://jazz.net/wiki/bin/view/Main/ZOSBuildSamplesV4)

Test Data

Sample Project Mortgage\*250

Assets 1500 COBOL programs 1000 Copybooks 500 BMS3 others

Total Assets 3003

In the repository the source code is stored in one stream with one
single component which includes 5 zComponent Projects.

Every test is executed twice against each version.

### Test Scenario Description

Test Scenario Description

Concurrent Build 1. Perform two team build concurrently2. After the team
builds are completed, created five repository workspaces, change a COBOL
file (MortgageApplication-EPSCMORT\zOSsrc\COBOL\A00CMORT.cbl) in each of
the repository workspace3. Request five personal builds concurrently

## Results

### Run duration

The charts below show the build run duration comparison between 4.0.3,
5.0.1, 5.0.2, 6.0, 6.0.1. Tests are run twice against each release and
the average time is taken for comparison.

From **4.0.3 to 6.0.1**, the overall improvement of the build time is
more than **36** for concurrent team build.

The data in the charts are the average time of the concurrent builds.

#### Concurrent team build

In this test scenario, two team builds are requested concurrently.

#### Concurrent personal build In this test scenario, five personal build are requested concurrently after one COBOL file is changed.

## Appendix A - Key Tuning Parameters \#AppendixC

Product Version Highlights for configurations under test

IBM WebSphere Application Server 8.0.0.3 (4.0.3GA to 4.0.5GA), 8.5.5.1
(4.0.6GA to 6.0.1GA) JVM settings:

\* GC policy and arguments, max and init heap sizes:

-Xmn512m -Xgcpolicy:gencon -Xcompressedrefs
-Xgc:preferredHeapBase=0x100000000 -Xmx4g -Xms4g OS configuration:

\* hard nofile 120000 \* soft nofile 120000 Refer to
<http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m4/topic/com.ibm.jazz.install.doc/topics/c_special_considerations_linux.html>
for details

DB2 DB2 Enterprise Server 9.7.0.5 (4.0.3GA to 4.0.6GA), 10.1.0.0 (5.0GA
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

META:FILEATTACHMENT{name="concurrentteambuild.gif"
attachment="concurrentteambuild.gif" attr="h" comment=""
date="1449827591" path="concurrentteambuild.gif" size="19503"
user="rucielulu" version="3"}
META:FILEATTACHMENT{name="concurrentpersonalbuild.gif"
attachment="concurrentpersonalbuild.gif" attr="h" comment=""
date="1449827663" path="concurrentpersonalbuild.gif" size="20882"
user="rucielulu" version="3"}
