META:TOPICINFO{author="sbeard" date="1458827674" format="1.1"
reprev="1.1" version="1.1"}
META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Systematic approach to performance and availability monitoring and management DKGRAY Authors: Main.StevenBeard Build basis: CLM and SSE all versions [systematic-approach-to-performance-and-availability-monitoring-and-management-dkgray-authors-main.stevenbeard-build-basis-clm-and-sse-all-versions]

ENDCOLOR

TOC{title="Page contents"}

This page is intended to provide an overall systematic approach to
monitoring and managing performance and availability issues. It will:

-   Initially outline the general approach DETECTING and issue, DECIDING
    what to DO and approaches to DOING something to rectify the
    underlying root cause
-   How to initially DETECT availability and performance issues
-   How to systematically working from the symptoms to the root cause of
    performance or availability issues and identify the failure scenario
-   Outline performance and availability scenarios with symptoms, root
    cause, recommended DECISION on what to DO and how to DO it

## General approach

-   ***DETECT that there is an performance issue or outage.*** It is
    critical that the Development Environment Team DETECTS that there
    has been an outage or a performance issue is building up as quickly
    as possible. This should be fully automated and automatically notify
    the whole Development Environment Team team straight away. It is
    critical to the confidence in the Development Environment Service
    that when the users raise a failure incident, the administrative
    team can say, Yes we know about the failure and we are already
    dealing with it or even better the administrative team have already
    proactively communicated that there has been a failure and they are
    working to resolve it. On the other hand a response of, what failure
    we did not know there was a problem?, can be catastrophic!

***Recommendation:*** You should investigate whether your Development
Environment Team can be automatically notified of application failures
via SMS or email.

-   ***DECIDE what to do.*** This is often where the most time is wasted
    when recovering from a performance issue or outage. It is critical
    that ALL the perceived failure scenarios are documented and what the
    standard procedure are for recovery in the SLA. It is human nature
    that Administrators will believe, if you give me just another hour,
    I can work out what the problem is and fix it, when the better
    approach for a first-time failure is to just restart the single
    point of failure or environment and then try and diagnose what the
    root cause of the problem is when the users can get on with their
    development. Generally, the best approach is to just restart the
    environment for a first-time failure, but on the second or third
    failure with the same symptoms take a little more time to try and
    diagnose the root cause. Also there should be a clear point in time
    when you should failover to the DR site rather than trying to
    resolve HA failure scenarios in the primary data center.

***Recommendation:*** Define target Maximum Time to Recovery (MTTR) for
any single or multiple HA scenarios of 1-2 hours. At this point after
the failure there should always be a review meeting to decide to fail
over to the DR data center OR in exceptional situations exactly how much
additional time should be allowed to recover before the next review
meeting. Too often we see customers trying to diagnose and fix their
production development environment for too long, when it would have made
more sense to failover to their disaster recovery site earlier and get
the development teams working again sooner.

-   ***Do something to fix the problem.*** Where possible this should be
    fully automated or at least have detailed manual procedures defined
    that have been well tested.

## DETECTING availability issues

Before we try and identify the root cause of an outage, we must be able
to DETECT that there has been an outage!

HOW TO ADD

## DETECTING performance issues

Before we try and identify the root cause of a performance issue, we
should DETECT that there is a performance issue to start with!

Most performance issues can be DETECTED by systematic environment
systems monitoring.

HOW TO ADD

## Systematically working from the symptoms to the root cause of performance or availability issues

## Performance and availability scenarios with symptoms, root cause, recommended DECISION on what to DO and how to DO it

| Scenario | Symptoms | Root cause | DECISIONS on what to DO | How to DO |
|:---|:---|:---|:---|:---|
| Incremental growth in usage leading to gradual performance issues | Systems monitoring trends gradually going-up and users starting to complain about slower performance | Deployment topology needs to be scaled-up | If existing systems resources already at comfortable maximum then scale-up topology | LINK: Scale-up topology |
| \^ | \^ | OR In sufficient systems resources | OTHERWISE increase appropriate systems resources | LINK: Scale-up systems resources |
| Network latency issues for specific sites |  |  |  |  |
| Failure of a single server or tier of environment |  |  |  |  |
| Failure of common IT service |  |  |  |  |
| Fundamental failure of primary data center |  |  |  |  |
| User operations known to ALWAYS have high demands |  |  |  |  |
| User operations known to SOMETIMES have high demands |  |  |  |  |
| Potential IBM product defect |  |  |  |  |

tactical resolution vs permanent fix - consider

## Develop a pragmatic approach to assessing actual user performance for each of the development tools

Acceptable performance can be very subjective leading to users,
teams/projects and organizations having a perception of performance
problems when none exist or they are poorly understood.

Understanding the symptoms and hopefully getting to the root cause of
performance issues can be very hard, so a critical first step is to
DECIDE whether there is or is not a performance issue to start with!

***Recommendation:*** Establish a small set of benchmark manual
performance tests that can be used to initially assess performance when
a user raises a performance service request/incident. A small number of
manually timed (users wrist watch) performance tests for common
operations (login, create WI, run a standard query, open dashboard etc.)
are an excellent way of assessing the current performance from a users
workstation when they raise a performance service request/incident.

It is critical that the manual tests are consistent and run against the
same RTC, RQM and RDNG project and data so that the results can be
consistently compared. For each test you should DECIDE an acceptable
range of performance so that they can DECIDE whether the user has a
performance issue and its magnitude.

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: None [additional-contributors-none]

-   [decisiontree.tiff](ATTACHURL/decisiontree.tiff): decisiontree.tiff

META:FILEATTACHMENT{name="decisiontree.tiff"
attachment="decisiontree.tiff" attr="" comment="" date="1458824368"
path="decisiontree.tiff" size="366236" user="sbeard" version="1"}
