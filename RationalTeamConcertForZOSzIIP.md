META:TOPICINFO{author="jdiaz" date="1410775838" format="1.1"
version="1.8"}
META:TOPICPARENT{name="PerformanceDatasheetsAndSizingGuidelines"}

# Rational Team Concert Enterprise Extension zIIP Offload Performance in 5.0 [rational-team-concert-enterprise-extension-ziip-offload-performance-in-5.0]

DKGRAY Authors: [Lu Lu](Main.LuLu) Last updated: June 2, 2014 Build
basis: Rational Team Concert on zOS 5.0 ENDCOLOR

TOC{title="Page contents"}

## Introduction

STARTSECTION{"Intro"} This report provides the offload percentage of a
Java workload in RTC EE when using a System z Integrated Information
Processor (zIIP).

A zIIP processor can help to offload application workload (Java
application) from z/OS greatly.

The objective of this testing was to understand the offload percentage
of a Java workload in RTC EE by zIIP processor. ENDSECTION{"Intro"}
Note: We strongly recommend to run with a zIIP or zAAP on the build
machine in order to offload the java workload and make it less
expensive.

## Disclaimer

INCLUDE{"PerformanceDatasheetDisclaimer"}

## Findings

In this scenario, we compared the CPU utilization between 1 general CP
and 1 general CP with 1 zIIP processor to find the offload percentage of
a Java workload in RTC EE on the build machine when using zIIP
processor.

\* It was found that about 80 - 90 of the workload was offloaded to the
zIIP processor and CPU utilization of the general CP was consistently
below 5 when using a zIIP processor.

The IBM System z Integrated Information Processor (zIIP) is available on
all IBM zEnterprise (zEnterprise), System z12, System z10, and System z9
servers. It is designed to increase general computing capacity and to
lower overall total cost of computing for select data and transaction
processing workloads for business intelligence (BI), ERP and CRM, and
select network encryption workloads on the mainframe.

## Topology

The tests are executed in a Single Tier Topology infrastructure like the
one in the following diagram:

The RTC server was set up based on WebSphere and DB2 on Linux for System
z. The build machine with Rational Build Agent was on zOS.

Test Environment

RTC Server Operating System & Version: Linux for System z (SUSE Linux
Enterprise Server 10 (s390x)) System Resource : 10 GB Storage, 4 CPs
(20000 mips, CPU type : 2097.710, CPU model: E12) CLM: 5.0 Sprint4
(CALM-I20131211-0734), 4 GB heap size DB2: 9.7.0.5 WAS: 8.5.5.1

Build Forge Agent Operating System & Version: z/OS 01.12.00 System
Resource: 6 GB Storage, 4 CPs (20000 mips, CPU type : 2097.710, CPU
model: E12) Build System Toolkit: 5.0 Sprint4 (RTC-I20131211-0354)

## Methodology

Monitor tools - NMON was used for RTC server and RMF on zOS was used for
Rational Build Agent.

The sample project for the test was Mortgage\*1000 which is 1000
duplicates of the [Mortgage sample
application](https://jazz.net/wiki/bin/view/Main/ZOSBuildSamplesV4) .

Test Data

Sample Project Mortgage\*1000

Assets 6000 COBOL programs 4000 Copybooks 2000 BMS3 others

Total Assets 12003

In the repository, source code is stored in one stream with one single
component which includes 5 zComponent Projects.

Each test scenario is executed twice for comparison.

### Test Scenarios

Test Scenario Description

Full Dependency Build 1. Run 2 times of full dependency build with 1
general CP;2. Run 2 times of full dependency build with 1 general CP and
1 zIIP

## Results

### Run duration

These tables show the run duration comparison between 1 general CP and 1
general CP + 1 zIIP with the test start and completion time.

Based on the build time results it was found that a Full Dependency
build takes a little less time when using a zIIP, saving about 10 build
time.

### CPU and Memory for Build Agent

This graph shows CPU utilization for Build Forge Agent on ZOS machine,
data is collected by RMF tool.

About 80 - 90 of the java workload has been offloaded by zIIP processor.

With one general CP:

With one general CP & one zIIP:

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

## Appendix A - Reference materials \#AppendixA

Refer to following links for zIIP processor material:

\-
<http://www-03.ibm.com/systems/z/hardware/features/ziip/capability.html> -
<http://www-03.ibm.com/systems/z/hardware/features/ziip/index.html>

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

META:FILEATTACHMENT{name="1GCP.jpg" attachment="1GCP.jpg" attr="h"
comment="CPU Usage with 1 general CP" date="1399362627" path="1GCP.jpg"
size="71007" user="rucielulu" version="1"}
META:FILEATTACHMENT{name="1GCP\_\_1_zIIP.jpg"
attachment="1GCP\_\_1_zIIP.jpg" attr="h" comment="CPU Usage with 1
general CP & 1 zIIP" date="1399362877" path="1GCP\_\_1_zIIP.jpg"
size="76899" user="rucielulu" version="1"}
META:FILEATTACHMENT{name="singleTierRTCEETests.png"
attachment="singleTierRTCEETests.png" attr="h"
comment="singleTierRTCEETests" date="1399364168"
path="singleTierRTCEETests.png" size="64395" user="rucielulu"
version="1"} META:FILEATTACHMENT{name="zIIP_testing_result.jpg"
attachment="zIIP_testing_result.jpg" attr="h" comment="buildtime"
date="1399366937" path="zIIP_testing_result.jpg" size="77032"
user="rucielulu" version="1"}
