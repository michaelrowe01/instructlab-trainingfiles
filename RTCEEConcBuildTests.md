META:TOPICINFO{author="rucielulu" date="1435808643" format="1.1"
version="1.5"} META:TOPICPARENT{name="RTCSystemZPerformanceTesting"}

# RTCEE Performance Testing: Concurrent Builds Scenario DKGRAY Authors: [Jorge Diaz](Main.JorgeAlbertoDiaz) Build basis: RTC 4.x 5.x 6.x [rtcee-performance-testing-concurrent-builds-scenario-dkgray-authors-jorge-diaz-build-basis-rtc-4.x-5.x-6.x]

ENDCOLOR

TOC{title="Page contents"}

STARTSECTION{"Intro"} The scenario targets the concurrent execution
builds. To accomplish that, team builds and personal builds are executed
concurrently in different steps of the scenario.

ENDSECTION{"Intro"}

## Scenario Detailed Description

Following the detail of the different steps that are performed for
testing this scenario on both z/OS and IBMi:

Test Steps of RTCz Description

1\. Perform two(2) enterprise dependency builds concurrently with
Mortgageapplicationx2502. Change a COBOL file in each repository
workspace3. Request five(5) personal builds concurrently After a first
complete build of all the programs ran in two team builds concurrently,
different sets of changes and personal builds are performed.

Test Steps of RTCi Description

1\. Perform two(2) enterprise dependency builds concurrently with
Maillist X2502. Change one RPG file in each repository workspace3.
Request five(5) personal builds concurrently After a first complete
build of all the programs ran in two team builds concurrently, different
sets of changes and personal builds are performed.

## Test Topologies

The following topologies are being used for the execution of this
scenario in order to test the performance and gather relevant data.

INCLUDE{"RTCEETestingTopologies" section="SingleTierZ"}
INCLUDE{"RTCEETestingTopologies" section="SingleTierI"}

## Test Reports

Please refer to the link below for test report related to current
scenario.

\* Below report compares the concurrent build performance of RTC for
z/OS. [Rational Team Concert For z/OS Concurrent Build
Performance](RTCEEConcurrentBuildComparisonBetweenReleases) \* Below
report compares the concurrent build performance of RTC for IBMi.
[Rational Team Concert For IBMi Concurrent Build
Performance](RTCEEConcurrentBuildComparisonBetweenReleasesForIBMi)

##### Related topics: [related-topics]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: [Lu Lu](Main.LuLu) [additional-contributors-lu-lu]
