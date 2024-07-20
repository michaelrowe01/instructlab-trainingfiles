META:TOPICINFO{author="rucielulu" date="1435808505" format="1.1"
version="1.6"} META:TOPICPARENT{name="RTCSystemZPerformanceTesting"}

# RTCEE Performance Testing: Benchmark Scenario Part 2 - Enterprise Extensions features DKGRAY Authors: [Jorge Diaz](Main.JorgeAlbertoDiaz) [Lu Lu](Main.rucielulu) [rtcee-performance-testing-benchmark-scenario-part-2---enterprise-extensions-features-dkgray-authors-jorge-diaz-lu-lu]

Build basis: RTC 4.x, RTC 5.x, RTC 6.x ENDCOLOR

TOC{title="Page contents"}

STARTSECTION{"Intro"} This scenario consists on testing the performance
of the Enterprise Extensions features used in a complete end-to-end
feature testing, from 'Promotion', 'Package', to final 'Deployment'.
ENDSECTION{"Intro"}

## Scenario Detailed Description

The following is a detailed description of the individual steps that are
executed in the emulation of this scenario to measure performance data.

Test Steps Description

Precondition: An initial full enterprise build has been completed
successfully of all programs included in in the test data set. If you
want to get full dependency build test result, please go to this
[link](https://jazz.net/wiki/bin/view/Deployment/RTCEEBenchmarkTests).1.
Package the application2. Run a Deployment3. Request full component
based promotion4. Make a single changeset, request promotion with single
changeset \* 2(do twice) After a first complete build of all the
programs, a component promotion is performed. Once promoted the sources
and binaries, the latter are packaged and finally deployed. The tests
are executed with different sets of the Scalability Test Data to get
information of the system resources consumption with different levels of
load.

## Test Topologies

The following topologies are being used for the execution of this
scenario in order to test the performance and gather relevant data.

INCLUDE{"RTCEETestingTopologies" section="SingleTierZ"}
INCLUDE{"RTCEETestingTopologies" section="SingleTierI"}

## Test Reports

Please refer to the below link for detail test report related to current
scenario. The report provide a release by release comparison of the
Enterprise Extensions Feature(promotion, package, deployment).

[Rational Team Concert For ZOS Feature Performance Comparison Between
Releases](RTCEEFeaturePerformanceComparisonBetweenReleases) [Rational
Team Concert For IBMi Feature Performance Comparison Between
Releases](RTCEEFeaturePerformanceComparisonBetweenReleasesForIBMi)

##### Related topics: [related-topics]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: [additional-contributors]

##### Questions and comments: [questions-and-comments]

-   What other performance information would you like to see here?
-   Do you have performance scenarios to share?
-   Do you have scenarios that are not addressed in documentation?
-   Where are you having problems in performance?

COMMENT{type="below" target="PerformanceDatasheetReaderComments"
button="Submit"}

INCLUDE{"PerformanceDatasheetReaderComments"}

META:FILEATTACHMENT{name="singleTierRTCEETests_IBMi.png"
attachment="singleTierRTCEETests_IBMi.png" attr="h" comment=""
date="1435641650" path="singleTierRTCEETests_IBMi.png" size="78271"
user="rucielulu" version="1"}
