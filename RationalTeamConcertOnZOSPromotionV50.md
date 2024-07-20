META:TOPICINFO{author="rucielulu" date="1413960306" format="1.1"
reprev="1.7" version="1.7"}
META:TOPICPARENT{name="PerformanceDatasheetsAndSizingGuidelines"}

# Enterprise Extensions promotion improvements in Rational Team Concert version 5.0 on z/OS DKGRAY Authors: [Lu Lu](Main.LuLu) Last updated: June 2, 2014 Build basis: Rational Team Concert v5.0 on z/OS [enterprise-extensions-promotion-improvements-in-rational-team-concert-version-5.0-on-zos-dkgray-authors-lu-lu-last-updated-june-2-2014-build-basis-rational-team-concert-v5.0-on-zos]

ENDCOLOR

TOC{title="Page contents"}

## Introduction

STARTSECTION{"Intro"} This report provides performance data for the
Enterprise Extensions promotion feature enhancements that were
introduced in version 5.0. The tests compare performance between
Rational Team Concert version 5.0 sprint 4 and version 4.0.6.

The objectives of our tests are to ensure that there is no regression
and to verify the performance improvements of the promotion feature.

In our scenario, we measured how long it takes for the 'finalize build
maps' process to complete with the 'publish build map links' option
selected in v5.0 sprint 4 and v4.0.6 promotion definitions.
ENDSECTION{"Intro"}'Finalize Build Maps' activity is one step that takes
about 60 of the whole promotion time, so improvement of 'Finalize Build
Maps' activity enhances promotion greatly.

## Disclaimer

INCLUDE{"PerformanceDatasheetDisclaimer"}

## Findings

In this scenario, we compared 'finalize build maps' activity during v5.0
sprint 4 and v4.0.6 promotions with the 'publish build map links' option
selected.

\* The performance time for the 'finalize build maps' activity changed
from 3 minutes 30 seconds for v4.0.6 down to 49.5 seconds in v5.0. An
improvement of 70 percent.

## Topology

The tests are executed in a single tier topology infrastructure like the
one in the following diagram:

The Jazz Team Server was set up based on WebSphere and DB2 on Linux for
System z. The build machine with the Rational Build Agent was on z/OS.

Test Environment

Jazz Team Server Operating System and version: Linux for System z (SUSE
Linux Enterprise Server 10 (s390x)) System Resource : 10 GB storage, 4
CPs (20000 mips, CPU type: 2097.710, CPU model: E12) CLM: 5.0 Sprint4
(CALM-I20131211-0734), 4 GB heap size DB2: 9.7.0.5 WAS: 8.5.5.1

Build Forge Agent Operating System and version: z/OS 01.12.00 System
Resource: 6 GB storage, 4 CPs (20000 mips, CPU type: 2097.710, CPU
model: E12) Build System Toolkit: 5.0 Sprint4 (RTC-I20131211-0354)

## Methodology

Monitor tools - NMON is used for the Jazz Team Server and RMF on z/OS
was used for Rational Build Agent.

The sample project used in this test was Mortgage\*100, which is 100
duplicates of the [Mortgage sample
application](https://jazz.net/wiki/bin/view/Main/ZOSBuildSamplesV4) .

Test Data

Sample Project Mortgage\*100

Assets 600 COBOL programs 400 Copybooks 200 BMS3 others

Total Assets 1203

In the repository, source code is stored in one stream with one single
component that includes five zComponent projects.

Each test scenario is executed twice for comparison.

### Test Scenarios

Test Scenario Description

Full Dependency Build and Promotion 1) Request full dependency build; 2)
Select 'publish build map links'; 3) Request promotion build to compare
'finalize build maps' activity;

## Results

### Run duration

These data tables show the run duration comparing 'finalize build maps'
activity during promotion between Rational Team Concert Enterprise
Extensions version 5.0 sprint 4 and 4.0.6.

From the test results of build time, we find that 'finalize build maps'
activity in promotion is improved by approximately 70 percent, as
'Finalize Build Maps' activity is one step that takes about 60 of the
whole promotion time, we find that promotion is improved by
approximately 40 percent.

### Build Activities

These data tables display the detailed build activities run time. In
version 5.0 Sprint4, 'Finalize build maps' activity has significantly
improved. The activity charts show that 'Finalize build maps' process
improved about 70 percent.

### CPU and Memory for Jazz Team Server

This graph shows CPU and memory utilization for server, data is
collected by NMON tool.

### CPU and Memory for Build Agent

This graph shows CPU utilization and DASD RATE data for Build Forge
Agent on z/OS system, data is collected by RMF tool.

## Appendix A - Key Tuning Parameters \#AppendixA

Product Version Highlights for configurations under test

IBM WebSphere Application Server 8.5.5.1 JVM settings:

\* GC policy and arguments, max and init heap sizes:

-Xmn512m -Xgcpolicy:gencon -Xcompressedrefs
-Xgc:preferredHeapBase=0x100000000 -Xmx4g -Xms4g OS configuration:

\* hard nofile 120000 \* soft nofile 120000 Refer to
<http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m4/topic/com.ibm.jazz.install.doc/topics/c_special_considerations_linux.html>
for details

DB2 DB2 Enterprise Server 9.7.0.5 Tablespace is stored on the same
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

META:FILEATTACHMENT{name="finalize_build_maps.jpg"
attachment="finalize_build_maps.jpg" attr="h" comment="finalize build
maps" date="1399531771" path="finalize_build_maps.jpg" size="122861"
user="rucielulu" version="1"} META:FILEATTACHMENT{name="cpuMemoryV5.jpg"
attachment="cpuMemoryV5.jpg" attr="h" comment="cpu and memory of v5.0
sprint4" date="1399532818" path="cpuMemoryV5.jpg" size="89816"
user="rucielulu" version="1"}
META:FILEATTACHMENT{name="cpuMemoryV406.jpg"
attachment="cpuMemoryV406.jpg" attr="h" comment="cpu and memory of
v4.0.6" date="1399533086" path="cpuMemoryV406.jpg" size="80898"
user="rucielulu" version="1"} META:FILEATTACHMENT{name="bfaV5.jpg"
attachment="bfaV5.jpg" attr="h" comment="" date="1399533239"
path="bfaV5.jpg" size="78345" user="rucielulu" version="1"}
META:FILEATTACHMENT{name="bfaV406.jpg" attachment="bfaV406.jpg" attr="h"
comment="" date="1399533274" path="bfaV406.jpg" size="85048"
user="rucielulu" version="1"}
META:FILEATTACHMENT{name="singleTierRTCEETests.png"
attachment="singleTierRTCEETests.png" attr="h" comment=""
date="1400496242" path="singleTierRTCEETests.png" size="64395"
user="rucielulu" version="1"} META:FILEATTACHMENT{name="duration.jpg"
attachment="duration.jpg" attr="h" comment="" date="1400496576"
path="duration.jpg" size="70488" user="rucielulu" version="1"}
