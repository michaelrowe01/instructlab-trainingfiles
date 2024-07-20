META:TOPICINFO{author="rucielulu" date="1435642800" format="1.1"
reprev="1.19" version="1.19"}
META:TOPICPARENT{name="PerformanceDatasheetsAndSizingGuidelines"}

# RTCEE for Application Development for z/OS Performance Testing DKGRAY Authors: [Jorge Diaz](Main.JorgeAlbertoDiaz) Build basis: RTC 4.x, RTC 5.x, RTC 6.x [rtcee-for-application-development-for-zos-performance-testing-dkgray-authors-jorge-diaz-build-basis-rtc-4.x-rtc-5.x-rtc-6.x]

ENDCOLOR

TOC{title="Page contents"}

This topic provides general information regarding the different
performance tests for Rational Team Concert [Enterprise
Extensions](https://jazz.net/products/rational-team-concert/features/enterprise)
for the System Z platform.

## Introduction: Platform vs. Features Testing

There are two different sets of tests and two testing aspects to
consider when talking about RTC and the System Z platform:

-   System Z as deployment platform: this is **core RTC** testing,
    therefore no system Z development practices nor RTCEE features are
    considered in this type of tests; but the RTC server is deployed on
    system Z. For example, when talking about deployments following the
    the **E5** and **E6** topologies captured in the [Original Standard
    Deployment Topologies](https://jazz.net/library/article/820) article
    on [Jazz.net](https://jazz.net). This is the case of reports like
    [Rational Team Concert 4.x sizing report for
    z/OS](https://jazz.net/library/article/816). This article **won't**
    cover information on this type of testing as the focus is to provide
    information around RTCEE features performance testing.

<!-- -->

-   Developing for System Z: The RTC [Enterprise
    Extensions](https://jazz.net/products/rational-team-concert/features/enterprise)
    features provide capabilities that leverage and provides support for
    the development for the mainframe. Specific performance tests are
    run for this type of features to assure they are performant; **this
    is the focus of the information in this wiki page**.

Therefore, the following information and topics in this page are focused
on describing the performance tests of RTC EE, where we can
differentiate:

1.  **RTCEE Benchmark Testing**: these are well defined specific
    Rational Team Concert Enterprise Extensions features tests. The data
    gathered will allow to assure the performance of these capabilities,
    and compare releases performance. Given how these tests are run in
    the development cycle they also allow the identification of
    potential issues/bugs.
2.  **Regression Tests**: this category of tests includes the ones like
    regression tests, the testing of new EE features or new EE
    configuration options, or special cases like changes in the
    technology.

The information in this page will cover detailed information on how
RTCEE performance tests are run and what they cover, as well as links to
relevant information when applicable. Following a description of the
main building blocks that are needed to understand the tests is
provided: (1) the topologies in which the tests are run; (2) the data
that is used in the tests; and (3) the different scenarios that are
defined for testing different usages of the features.

## Typical Testing Topologies

Specific RTCEE performance tests are typically executed in a Single Tier
Topology infrastructure like the one in the following diagram:

INCLUDE{RTCEETestingTopologies}

**Note:** specific RTCEE performance tests may be executed following
different topologies. In such situations, it will be detailed in the
relevant tests reports.

## Test Data

INCLUDE{"RTCEEPerfTestsData" section="Intro"}

In order to produce relevant volumes of information, the test data is
replicated several times and used in the tests. Detailed information
about the data used will be provided in the specific information pages
for each test.

## Test Scenarios and Reports

A set of scenarios that are executed as part of the **RTCEE Benchmark
Tests** are defined. While these are standard scenarios that are run,
additional scenarios may be defined for execution of specifically
designed tests.

### Enterprise Dependency Build Scenario

INCLUDE{"RTCEEDepBuildTests" section="Intro"}

Detailed information about this scenario and test reports can be found
[here](RTCEEDepBuildTests).

### Enterprise Extensions Features Scenario

INCLUDE{"RTCEEBenchmarkTests" section="Intro"}

Detailed information about this scenario and test reports can be found
[here](RTCEEBenchmarkTests).

### SCM Command Line Scenario

INCLUDE{"RTCEECLITests" section="Intro"}

Detailed information about this scenario and test reports can be found
[here](RTCEECLITests).

### ISPF Client Scenario

INCLUDE{"RTCEEISPFTests" section="Intro"}

Detailed information about this scenario and test reports can be found
[here](RTCEEISPFTests).

### Concurrent Builds Scenario

INCLUDE{"RTCEEConcBuildTests" section="Intro"}

Detailed information about this scenario and test reports can be found
[here](RTCEEConcBuildTests).

### Customized Regression Tests Scenarios

INCLUDE{"RTCEEBenchmarkIncBuildTests" section="Intro"}

Detailed information about this scenario and test reports can be found
[here](RTCEEBenchmarkIncBuildTests).

### EE Workload Scenario (Additional Scenario)

INCLUDE{"RTCEEWorkloadTests" section="Intro"}

Detailed information about this scenario and test reports can be found
[here](RTCEEWorkloadTests).

## Test Reports Analysis Guidelines

The information presented previously in this wiki page describes the
type of performance tests regularly executed for RTCEE features, and the
different assets used on them. This subsection, as a wrap-up of the
information, will describe data that you can expect to find in the RTCEE
performance tests reports.

### What system information is provided?

In the different reports you will find information about the specifies
of the system used and the software versions used as well. In the
different test reports you will usually find:

-   Specifics of the topology, if anything that needs to be pointed out
-   Particular software versions of the components used: WebSphere
    Application Server version, Database version and CLM version used in
    the test
-   Resources assigned to the system and the components: processing
    units assigned to the systems, MIPS estimation, memory assigned to
    the system and as JVM heap

### What is tracked?

The following table outlines the resources that are tracked and the
units in which results are reported:

-   RTC and DB Server LPAR

\| **CPU** \| Percentage of processing usage. The actual RTC server
process is monitored. \| \| **Memory** \| Measured in Kilobytes. Whole
system memory consumption is monitored. \|

-   Build Machine LPAR

\| **CPU** \| Percentage of processing usage. Whole system memory
consumption is monitored. Being a dedicated LPAR is assumed that system
CPU and Build Agent CPU for builds are comparable. \| \| **Memory** \|
Response times and rate are measured. \|

The following is an example of a resources graphic and the information
presented. Axis meaning will vary depending on information tracked:

##### Related topics: [related-topics]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: [additional-contributors]

META:FILEATTACHMENT{name="graphic.png" attachment="graphic.png" attr="h"
comment="" date="1386610471" path="graphic.png" size="72874"
user="jdiaz" version="1"}
