META:TOPICINFO{author="jdiaz" date="1416590346" format="1.1"
version="1.2"} META:TOPICPARENT{name="RTCEEWorkloadTests"}

# RTCEE Performance Testing: EE Workload Scenario Scenario 1 Test Report [rtcee-performance-testing-ee-workload-scenario-scenario-1-test-report]

DKGRAY Authors: [Jorge Diaz](Main.JorgeAlbertoDiaz) Date: Nov 21st, 2014
Build basis: Rational Team Concert 5.0 ENDCOLOR

TOC{title="Page contents"}

## Introduction

This report gathers the result of the execution of the Scenario 1 as
described in [RTCEE Workload
Tests](https://jazz.net/wiki/bin/view/Deployment/RTCEEWorkloadTests)
page.

## Disclaimer

INCLUDE{"PerformanceDatasheetDisclaimer"}

## Findings

-   Size of repository volume don't increases in 8 hours
    exeuction(compare end with start condition).
-   CPU usage of CLM server is \< 60
-   CPU usage of Build System Toolkit & DB2z is \< 60
-   CPU usage of DB2z is smoothly under 6

## Topology

The tests are executed in a Single Tier Topology infrastructure like the
one in the following diagram: INCLUDE{"RTCEETestingTopologies"
section="DualTierZ"}

### Test Topology Parameterization

The following system configuration is used in the execution of this
particular scenario variant:

Test Environment Configuration Model MSU

RTC Server Operating System & Version: z/OS 01.12.00 System Resource :
10 GB Storage, 2 CPs (1000 mips, CPU type : 2097.710) CALM: 5.0 GA, 4 GB
heap size WAS: 8.5.5.1

E12

Build Forge Agent & DB2z Operating System & Version: z/OS 01.12.00
System Resource: 6 GB Storage, 4 CPs (2000 mips, CPU type : 2097.710)
Build System Toolkit: 5.0 GA DB2: 10.1.0.0

E12 513

## Results

-   For 8 hours long run of scenario1, 46 times(iterations) concurrent
    builds have been launched, total 1288 personal builds and 44 team
    builds have been processed successfully.

Start Time End Time Concurrent Request Times Concurrent Users Each Time
Total Personal Builds Num Team Build Request Times Total Team Builds Num

8/16/2014 11:30:50 AM 8/16/2014 7:34:38 PM 46 28 1288 4 40

-   Personal build time/average build time of concurrent builds in 8
    hours test:

Build Definition Build duration of Personal Build

Build Definition 1 - 2 22 seconds - 4 minutes 22 seconds, average 2
minutes

Build Definition 3 - 5 30 seconds - 4 minutes 53 seconds, average 2
minutes 30 seconds

Build Definition 6 - 10 29 seconds - 3 minutes 43 seconds, average 2
minutes 10 seconds

\* No build(both personal and team build) fails in EE workload scenario
1 test.

-   CLM Server monitoring:

<!-- -->

-   Build System Toolkit monitoring:

<!-- -->

-   DB2z monitoring:

\* 140.4 Contributors are simulated in 2nd run - Overall Count Attempted
Tasks For Run = 23990 \* Indice incremental rate:

Indice Directory Name Before execution After execution Incresed Rate

\_Indices 2115620 2242828 6.01

./jfs-rdfhistory 308 424 37.66

./jfs-rdfindex 1986436 2112940 6.37

./jfs-texthistory 52 252 0.00

./jfs-textindex 128816 129404 0.46

#### About the authors [about-the-authors]

Main.JorgeAlbertoDiaz

--------------------

##### Questions and comments: [questions-and-comments]

-   What other performance information would you like to see here?
-   Do you have performance scenarios to share?
-   Do you have scenarios that are not addressed in documentation?
-   Where are you having problems in performance?

COMMENT{type="below" target="PerformanceDatasheetReaderComments"
button="Submit"}

INCLUDE{"PerformanceDatasheetReaderComments"}

META:FILEATTACHMENT{name="avganalysisOfclmserver.jpg"
attachment="avganalysisOfclmserver.jpg" attr="h" comment="Average and
Peak Analysis for the Selected Time Range across all Days of CLM Server"
date="1413966101" moveby="jdiaz"
movedto="Deployment.RTCEEWorkloadTestScenario1Report.avganalysisOfclmserver.jpg"
movedwhen="1416583310"
movefrom="Deployment.RTCEEWorkloadTests.avganalysisOfclmserver.jpg"
path="avganalysisOfclmserver.jpg" size="102821" user="rucielulu"
version="1"} META:FILEATTACHMENT{name="cpudsad_clmserver.jpg"
attachment="cpudsad_clmserver.jpg" attr="h" comment="CPU Usage and DASD
RATE of CLM Server" date="1413966336" moveby="jdiaz"
movedto="Deployment.RTCEEWorkloadTestScenario1Report.cpudsad_clmserver.jpg"
movedwhen="1416583423"
movefrom="Deployment.RTCEEWorkloadTests.cpudsad_clmserver.jpg"
path="cpudsad_clmserver.jpg" size="168435" user="rucielulu" version="1"}
META:FILEATTACHMENT{name="avganalysisOfbst.jpg"
attachment="avganalysisOfbst.jpg" attr="h" comment="Average and Peak
Analysis for the Selected Time Range across all Days of BST"
date="1413966028" moveby="jdiaz"
movedto="Deployment.RTCEEWorkloadTestScenario1Report.avganalysisOfbst.jpg"
movedwhen="1416583495"
movefrom="Deployment.RTCEEWorkloadTests.avganalysisOfbst.jpg"
path="avganalysisOfbst.jpg" size="103020" user="rucielulu" version="1"}
META:FILEATTACHMENT{name="cpudsad_bst.jpg" attachment="cpudsad_bst.jpg"
attr="h" comment="CPU Usage and DASD RATE of BST & DB2z"
date="1413966285" moveby="jdiaz"
movedto="Deployment.RTCEEWorkloadTestScenario1Report.cpudsad_bst.jpg"
movedwhen="1416583544"
movefrom="Deployment.RTCEEWorkloadTests.cpudsad_bst.jpg"
path="cpudsad_bst.jpg" size="160653" user="rucielulu" version="1"}
META:FILEATTACHMENT{name="cpuOfDB2z.jpg" attachment="cpuOfDB2z.jpg"
attr="h" comment="Engine/CPU Utilization of DB2z 10" date="1413966456"
moveby="jdiaz"
movedto="Deployment.RTCEEWorkloadTestScenario1Report.cpuOfDB2z.jpg"
movedwhen="1416583610"
movefrom="Deployment.RTCEEWorkloadTests.cpuOfDB2z.jpg"
path="cpuOfDB2z.jpg" size="96359" user="rucielulu" version="1"}
