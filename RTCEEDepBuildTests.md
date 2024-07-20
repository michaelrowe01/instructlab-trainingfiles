META:TOPICINFO{author="rucielulu" date="1435808490" format="1.1"
version="1.7"} META:TOPICPARENT{name="RTCSystemZPerformanceTesting"}

# RTCEE Performance Testing: Dependency Build Scenario DKGRAY Authors: [Jorge Diaz](Main.JorgeAlbertoDiaz) Build basis: RTC 4.x [rtcee-performance-testing-dependency-build-scenario-dkgray-authors-jorge-diaz-build-basis-rtc-4.x]

ENDCOLOR

TOC{title="Page contents"}

STARTSECTION{"Intro"} This scenario tests the performance of the
enterprise Dependency Based Build focused on a single user executing a
team build. The tests are executed against two sets of data:
MortgageApplicationx100 and MortgageApplicationx1000 on z/OS, and
"Maillistx100" and "Maillistx1000" on IBMi platform. Unless otherwise
specified, the following options are commonly used in the tests
executing this scenario:

-   Leave the publish build maps option cleared

ENDSECTION{"Intro"}

## Scenario for RTCz Detailed Description

The following is a detailed description of the individual steps that are
executed in the emulation of this scenario to measure performance data.

Test Steps Description

1\. Perform an initial full build of all the programs included in the
test data set2. Change one COBOL file and execute the build3. Change one
COPY file and execute the build4. Change all COPY books and rebuild 5.
Change all COBOL files and rebuild After a first complete build of all
the programs, different changes are performed and a rebuild requested.
These requests will rebuild the changed programs and impacted ones. The
COBOL file changed in these tests is
"MortgageApplication-JKECMORT\zOSsrc\COBOL\JKECMORT.cbl" The COPY file
changed in these tests is
"MortgageApplication-Common\zOSsrc\COPYBOOK\JKEMTCOM.cpy". Modifying
this copy will impact four COBOL files: "JKEMLIST.cbl", "JKECSMRT.cbl",
"JKECMORT.cbl" and "JKECMAIN.cbl". Finally, all the copybooks are
modified and a build requested making all impacted programs to be built.

**Note regarding modified files during tests:** when a replicated data
set is used (e.g. Mortgagex100), every replication of the cobol and
copybooks files referred here are modified.

## Scenario for RTCi Detailed Description

The following is a detailed description of the individual steps that are
executed in the emulation of this scenario to measure performance data.

Test Steps Description

1\. Perform an initial full build of all the programs included in the
test data set2. Change one RPG file and execute the build 3. Change all
RPG files and rebuild After a first complete build of all the programs,
different changes are performed and an incremental build is requested.
These requests will rebuild the changed programs and impacted ones.

**Note regarding modified files during tests:** when a replicated data
set is used (e.g. Mortgagex100), every replication of the cobol and
copybooks files referred here are modified.

## Test Topologies

The following topologies are being used for the execution of this
scenario in order to test the performance and gather relevant data.

INCLUDE{"RTCEETestingTopologies" section="SingleTierZ"}
INCLUDE{"RTCEETestingTopologies" section="SingleTierI"}

## Test Reports

Please refer to the below links for the reports related to this
scenario.

1.1. [Rational Team Concert For ZOS Performance Comparison Between
Releases](RationalTeamConcertForZOSPerformanceComparisonBetweenReleases)

1.2. [Rational Team Concert For IBMi Performance Comparison Between
Releases](RationalTeamConcertForIBMiPerformanceComparisonBetweenReleases)

This report provide a release by release comparison of the initial full
dependency build performance.

2.1. [Rational Team Concert For z/OS Incremental Build Performance
Comparison Between Releases
]( RTCEEIncrementalBuildComparisonBetweenReleases)

2.2. [Rational Team Concert For IBMi Incremental Build Performance
Comparison Between Releases
]( RTCEEIncrementalBuildComparisonBetweenReleasesForIBMi)

This report provide a release by release comparison of the incremental
dependency build performance. The builds are requested after different
changes are performed.

##### Related topics: [related-topics]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: [additional-contributors]
