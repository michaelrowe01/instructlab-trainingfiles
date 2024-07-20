META:TOPICINFO{author="sahilkmansuri" date="1711002186" format="1.1"
version="1.79"} META:TOPICPARENT{name="DeploymentTroubleshooting"}

# Performance troubleshooting DKGRAY Authors: PerformanceTroubleshootingTeam [performance-troubleshooting-dkgray-authors-performancetroubleshootingteam]

Build basis: ELM 7.x and later ENDCOLOR

TOC{title="Page contents"}

This page is the starting point for information and techniques to help
diagnose performance issues when using the IBM Rational Collaborative
Lifecycle Management (CLM) family of products (Rational Team Concert,
Rational Requirements Composer, and Rational Quality Manager).

## How to use this performance troubleshooting guide

The situations listed below are divided into two groups: situations
likely to be encountered by administrators, and situations likely to be
encountered by users of the CLM products.

If you are new to troubleshooting, see [How to start a troubleshooting
assessment](HowToStartATroubleshootingAssessment), and [Data Collection
Basics](RTCTroubleshootingBasicsandDataCollection). Also, take the time
to review [Common Jazz hardware configuration and performance impact
overview](CommonJazzHWConfigPerfImpact) and [Must Gather for Performance
problems in CLM](MustgatherPerformanceProblemsInCLM).

### Administrator situations

-   [Oracle Must
    Gather](https://jazz.net/wiki/bin/view/Deployment/OracleMustGather)
    will guide you on how to see problematic queries and the information
    IBM will need to process these
-   [DB2 Must
    Gather](https://jazz.net/wiki/bin/view/Deployment/Db2MustGather):
    similar to [Oracle Must
    Gather](https://jazz.net/wiki/bin/view/Deployment/OracleMustGather),
    it will guide you on how to collect information for problematic
    queries on IBM DB2 Servers

<!-- -->

-   [Why do I get out-of-memory (OOM) errors in the log
    files?](OomIntheLog)
-    [Preventing Out-of-memory errors in Lifecycle Query
    Engine](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.3/com.ibm.team.jp.lqe2.doc/topics/c_lqe_outofmemoryerrors.html)
-   [Why do my ETLs take so long to run?](WhyDoMyETLsTakeSoLongToRun)
-   [Why is my CPU spiking?](WhyIsMyCPUSpiking)
-   [How do I determine if my server has enough
    memory?](HowToDetermineServerMemory)
-   [How do I determine if my network has a
    problem?](HowDoIDetermineIfMyNetworkHasAProblem)
-   [Troubleshooting problems in virtualized
    environments](VirtualizationTroubleshooting)
-   [Why do some pages take two minutes to
    load?](WhyDoSomePagesTakeTwoMinutesToLoad)

### User situations

-   [Why is browser performance slow?](BrowserPerformance)
-   [Why does my Rational Team Concert plan take so long to
    load?](RTCPlanLoading)
-   [Why is the Rational Team Concert client
    slow?](RTCClientPerformance)
-   [Why does my Rational Team Concert query take so long to return
    results?](WhyDoesMyQueryTakeSoLong)
-   [My builds are slow: how can I speed them up?](RTCSlowBuilds)
-   [Why does it take so long to log in?](WhyIsMyAuthenticationSlow)
-   [Troubleshooting CLM Applications Using an HTTP Access
    Log](https://jazz.net/wiki/bin/view/Deployment/TroubleshootingCLMApplicationsUsingAnHTTPAccessLog)

### Where do I go from here? If you are unable to resolve your issue using online resources, open a service request with IBM Enterprise Software Support. For details, see [Troubleshooting resources](DataCollectionandSupportResources).

##### Additional contributors: Main.DeniseMcKinnon, Main.MichaelAfshar, Main.MikeDelargy, Main.StephanieBagot [additional-contributors-main.denisemckinnon-main.michaelafshar-main.mikedelargy-main.stephaniebagot]
