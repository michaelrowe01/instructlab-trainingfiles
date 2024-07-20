META:TOPICINFO{author="rucielulu" date="1435807201" format="1.1"
reprev="1.3" version="1.3"}
META:TOPICPARENT{name="RTCSystemZPerformanceTesting"} This section
describes the testing topologies used for performance tests focused on
RTCEE features for Application Development for z/OS.
STARTSECTION{"SingleTierZ"}

#### Single Tier Topology: zLinux [single-tier-topology-zlinux]

ENDSECTION{"SingleTierZ"} From the diagram, we can differentiate:

-   Server components are installed in a zLinux LPAR where CLM server
    and database server are deployed. In spite that the tests are
    focused on RTC Enterprise Extensions capabilities, the software
    installation includes the full CLM solution.
-   A z/OS LPAR in the same system Z holds the installation of the RTC
    build components (Build Agent and Build Toolkit), and the RTC ISPF
    client.
-   Both LPARs are dedicated to the CLM components described.

This section describes the testing topologies used for performance tests
focused on RTCEE features for Application Development for IBMi.
STARTSECTION{"SingleTierI"}

#### Single Tier Topology: IBMi [single-tier-topology-ibmi]

ENDSECTION{"SingleTierI"} From the diagram, we can differentiate:

-   Server components are installed in a IBMi LPAR where CLM server are
    deployed and DB2 server is used. In spite that the tests are focused
    on RTC Enterprise Extensions capabilities, the software installation
    includes the full CLM solution.
-   A IBMi LPAR in the same IBMi system holds the installation of the
    RTC build components (Build Agent and Build Toolkit).
-   Both LPARs are dedicated to the CLM components described.

STARTSECTION{"DualTierZ"}

#### Dual Tier Topology: z/OS [dual-tier-topology-zos]

ENDSECTION{"DualTierZ"}

From the diagram, we can differentiate:

-   RTC Server components are installed in a z/OS LPAR.
-   A z/OS LPAR in the same system Z holds the installation of both the
    DB2 database and the RTC build components (Build Agent and Build
    Toolkit).
-   Both LPARs are dedicated to the CLM components described during the
    testing

META:FILEATTACHMENT{name="singleTierRTCEETests.png"
attachment="singleTierRTCEETests.png" attr="h" comment=""
date="1385735325" moveby="jdiaz"
movedto="Deployment.RTCEETestingTopologies.singleTierRTCEETests.png"
movedwhen="1409561524"
movefrom="Deployment.RTCSystemZPerformanceTesting.singleTierRTCEETests.png"
path="singleTierRTCEETests.png" size="64395" user="jdiaz" version="1"}
META:FILEATTACHMENT{name="dualTierRTCEETests.png"
attachment="dualTierRTCEETests.png" attr="h" comment=""
date="1409569647" path="dualTierRTCEETests.png" size="39462"
user="jdiaz" version="1"}
META:FILEATTACHMENT{name="singleTierRTCEETests_IBMi.jpg"
attachment="singleTierRTCEETests_IBMi.jpg" attr="h" comment=""
date="1435807201" path="singleTierRTCEETests_IBMi.jpg" size="78036"
user="rucielulu" version="1"}
