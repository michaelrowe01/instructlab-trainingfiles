META:TOPICINFO{author="rucielulu" date="1450248116" format="1.1"
reprev="1.12" version="1.12"}
META:TOPICPARENT{name="RTCEEBenchmarkTests"}

# Rational Team Concert For z/OS Features Performance Comparison Between Releases [rational-team-concert-for-zos-features-performance-comparison-between-releases]

DKGRAY Authors: [Lu Lu](Main.rucielulu), Zhang Wei, Main.SuHui Date: Nov
24th, 2014 Build basis: Rational Team Concert for z/OS from 4.0.2,
4.0.3, 4.0.4, 4.0.5, 4.0.6, 5.0, 5.0.1, 5.0.2, 6.0, 6.0.1 ENDCOLOR

TOC{title="Page contents"}

## Introduction

This report compares the performance of RTC for z/OS features(Package,
Deploy and Promotion) between releases since v4.0.2 until v6.0.1.
Generally constant performance improvements are made into releases of
RTC for z/OS. The objective of this report is to present the
improvements.

The performance data provided is obtained by benchmark test of each
release.

## Disclaimer

INCLUDE{"PerformanceDatasheetDisclaimer"}

## Findings

Based on following feature test data, we can get following summaries of
RTC EE features from 4.0.2 to 6.0: 1. Performance of 'Promotion' feature
has improved significantly (80). 2. Performance of 'Deploy' feature has
improved about 16.9. 3. Performance of 'Package' feature is stable.

From 4.0.2 to 6.0.1, the overall performance improvement of the
Promotion feature is about 80:

\*. From 4.0.3 to 4.0.4, promotion time has improved by 7 ('Generating
list of binaries to promote' activity is the most notable improvement of
50 than 4.0.3). \*. From 4.0.5 to 4.0.6, promotion time has improved by
75('Finalize build maps' activity is a remarkable great improvement of
96 than 4.0.5). \*. From 5.0.2 to 6.0.1, promotion time has improved by
23 to 37('Generating list of binaries to promote' and 'Finalize build
maps' are the improved activities).

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

## Results

### Run duration

Below charts show run duration comparing between 4.0.2 until 6.0.1 of
each EE feature, and each feature of EE are run twice against each
release and the average time is taken for comparison.

Package: From below 'Package' feature runtime chart, each release has
simliar runtime duration, no big improvement in this feature, but this
feature is stable.

Deploy: From below 'Deploy' feature runtime chart, it improved about
16.9 from v4.0.2 to v5.0.1 for MortgageApplication x1000.

Note - For v5.0, there was one regression issue but had been fixed
quickly.

Promotion: From below 'Promotion' feature runtime chart, this feature is
continous improved release by release, it has been improved 80. For the
release by release comparison, it improved by 75 from 4.0.5 to 4.0.6 and
23 to 37 from 5.0.2 to 6.0.1.

Below 'Promotion - Single Changes' runtime chart is a special scenario
desinged from v4.0.4 release, which shows peformance improvement of
'promotion with change set' feature.

### Build Activities

Display all feature test results in one comparison table is too large,
so seperate into 3 comparison tables and link to other page.

For EE feature test results, they are divided into following 3
comparison tables, please navigate to linked page for detailed results.

'Package' Comparison Results [here](RTCEEFeaturesPackageComparison)
'Deploy' Comparison Results [here](RTCEEFeaturesDeployComparison)
'Promotion(Full Promotion and Single Changeset)' Comparison Results
[here](RTCEEFeaturesPromotionComarison)

## Appendix A - Key Tuning Parameters \#AppendixA

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

Main.Lu Lu

--------------------

##### Questions and comments: [questions-and-comments]

-   What other performance information would you like to see here?
-   Do you have performance scenarios to share?
-   Do you have scenarios that are not addressed in documentation?
-   Where are you having problems in performance?

COMMENT{type="below" target="PerformanceDatasheetReaderComments"
button="Submit"}

INCLUDE{"PerformanceDatasheetReaderComments"}

META:FILEATTACHMENT{name="promotionRuntime2.jpg"
attachment="promotionRuntime2.jpg" attr="h" comment="promotionRuntime2"
date="1411354927" path="promotionRuntime2.jpg" size="95951"
user="rucielulu" version="1"}
META:FILEATTACHMENT{name="deployRuntime.gif"
attachment="deployRuntime.gif" attr="h" comment="" date="1450247573"
path="deployRuntime.gif" size="17531" user="rucielulu" version="3"}
META:FILEATTACHMENT{name="packageRuntime.gif"
attachment="packageRuntime.gif" attr="h" comment="" date="1450248115"
path="packageRuntime.gif" size="18307" user="rucielulu" version="3"}
META:FILEATTACHMENT{name="promotionRuntime.gif"
attachment="promotionRuntime.gif" attr="h" comment="" date="1450247407"
path="promotionRuntime.gif" size="16888" user="rucielulu" version="3"}
META:FILEATTACHMENT{name="promotionRuntime2.gif"
attachment="promotionRuntime2.gif" attr="h" comment="" date="1450247209"
path="promotionRuntime2.gif" size="17912" user="rucielulu" version="3"}
