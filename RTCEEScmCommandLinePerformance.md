META:TOPICINFO{author="rucielulu" date="1449827895" format="1.1"
version="1.6"} META:TOPICPARENT{name="RTCEECLITests"}

# Rational Team Concert For z/OS SCM Command Line Performance DKGRAY Authors: Main.SuHui Date: Dec 11, 2015 Build basis: Rational Team Concert for z/OS version 4.0.3, 5.0, 5.0.2, 6.0, 601 [rational-team-concert-for-zos-scm-command-line-performance-dkgray-authors-main.suhui-date-dec-11-2015-build-basis-rational-team-concert-for-zos-version-4.0.3-5.0-5.0.2-6.0-601]

ENDCOLOR

TOC{title="Page contents"}

## Introduction

This report compares the performance of RTC for z/OS SCM command line
include zload and zimport. The zimport command will import z/OS PDS
members into RTC source control. And zload command will load a
repository workspace onto the z/OS system.

Based on our test for every release from version 4.0.3 to 6.0.1, the
performance of zload and zimport command stay stable without notable
performance regression or improvement. This report only include data of
4.0.3, 5.0, 5.0.2, 6.0 and 6.0.1 to demonstrate the performance.

The performance data provided is obtained by benchmark test of each
release.

## Disclaimer

INCLUDE{"PerformanceDatasheetDisclaimer"}

## Findings

Based on our test data, performance of the zload and zimport SCM
commands stay stable from version 4.0.3 and 6.0. There are no notable
performance regressions or improvements between releases.

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
5.0 GA, 4 GB heap size DB2: 9.7.0.5 (from 4.0.3 GA to 4.0.6 GA),
10.1.0.0(from 5.0 GA to 6.0.1 GA) WAS: 8.0.0.3 (from 4.0.3 GA to 4.0.5
GA), 8.5.5.1 (from 4.0.6 GA to 6.0.1 GA)

Build Forge Agent Operating System & Version: z/OS 01.12.00 System
Resource: 6 GB Storage, 4 CPs (20000 mips, CPU type : 2097.710, CPU
model: E12) Build System Toolkit: from 4.0.3 GA to 6.0.1 GA

## Methodology

Run duration of the commands are compared by getting test start date and
time.

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

The commands are executed twice against each version.

### Test Scenario Description

Test Scenario Description

SCM command line 1. run the zload command to load a repository workspace
containing source code of the sample project onto the z/OS system2. run
the zimport command to import the loaded PDS to a new created repository
workspace

## Results

### Run duration

The charts below show the command run duration of version 4.0.3, 5.0,
5.0.2, 6.0 and 6.0.1. The commands are run twice against each release
and the average time is taken for comparison. The run durations for both
zload and zimport command are comparable between releases.

#### zload

#### zimport

## Appendix A - Key Tuning Parameters \#AppendixC

Product Version Highlights for configurations under test

IBM WebSphere Application Server 8.0.0.3 (4.0.3GA to 4.0.5GA), 8.5.5.1
(4.0.6GA to 6.0GA) JVM settings:

\* GC policy and arguments, max and init heap sizes:

-Xmn512m -Xgcpolicy:gencon -Xcompressedrefs
-Xgc:preferredHeapBase=0x100000000 -Xmx4g -Xms4g OS configuration:

\* hard nofile 120000 \* soft nofile 120000 Refer to
<http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m4/topic/com.ibm.jazz.install.doc/topics/c_special_considerations_linux.html>
for details

DB2 DB2 Enterprise Server 9.7.0.5 (4.0.3GA to 4.0.6GA), 10.1.0.0 (5.0GA
to 6.0 GA) Tablespace is stored on the same machine as IBM WebSphere
Application Server

License Server Same as CLM version Hosted locally by JTS server

Network

Shared subnet within test lab

#### About the authors [about-the-authors]

Main.SuHui

--------------------

##### Questions and comments: [questions-and-comments]

-   What other performance information would you like to see here?
-   Do you have performance scenarios to share?
-   Do you have scenarios that are not addressed in documentation?
-   Where are you having problems in performance?

COMMENT{type="below" target="PerformanceDatasheetReaderComments"
button="Submit"}

INCLUDE{"PerformanceDatasheetReaderComments"}

META:FILEATTACHMENT{name="zload.gif" attachment="zload.gif" attr="h"
comment="" date="1435809003" path="zload.gif" size="26288"
user="bjsuhui" version="2"} META:FILEATTACHMENT{name="zimport.gif"
attachment="zimport.gif" attr="h" comment="" date="1435808978"
path="zimport.gif" size="27711" user="bjsuhui" version="2"}
