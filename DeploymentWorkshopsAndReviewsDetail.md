META:TOPICINFO{author="michaelrowe" date="1699535694" format="1.1"
version="1.5"} META:TOPICPARENT{name="DeploymentPlanning"}

# Deployment Workshops and Reviews in Detail DKGRAY Authors: Main.TimFeeney, Main.GrantCovell, Main.StevenBeard, Main.MikeDelargy Build basis: N/A [deployment-workshops-and-reviews-in-detail-dkgray-authors-main.timfeeney-main.grantcovell-main.stevenbeard-main.mikedelargy-build-basis-na]

ENDCOLOR

TOC{title="Page contents"}

## Deployment workshops and reviews

A typical 2 day deployment workshop or review for an enterprise scale
Rational development environment:

***Day 1***

**09:00 - 09:30:** Give introductions and present the scope and agenda.
**09:30 - 10:00:** Present and discuss the key considerations for
designing a Rational development environment. **10:00 - 11:30:**
Understand general requirements, constraints, and usage for the
environment. **11:30 12:30:** Review the current development environment
(Rational or third party).

**12:30 13:00:** Lunch

**13:00 14:30:** Understand the current infrastructure services and
preferred middleware/platforms. Make key platform, OS, and middleware
decisions. **14:30 16:30:** Discuss deployment topology options based on
the preferred technology and common services. **16:30 17:00:** Review
and refine Day 2 agenda, and wrap-up Day 1.

***Day 2***

**9:00 - 10:00:** Review of Day 1

Hold sessions to discuss and agree on the approach to and design for
these tasks:

-   Capacity planning, performance, and monitoring
-   High-availability and disaster-recovery
-   Security
-   Audit and control
-   Compliance
-   Administration, configuring, and tuning

**16:30 17:00:** Overall wrap-up and discuss next steps

\* Determine who is going to document the detailed deployment design,
and by when.

IBM Rational software supports deployment workshops and reviews pre- and
post-sales.

## Sample Agenda

**\[CLIENT\] Technical Deployment Review Workshop** **\[Location\]**
**\[Date(s)\]**

This workshop focuses on technical rather than organizational
deployment:

-   Technical deployment of Rational products and solutions which
    includes: planning, designing, installing, configuring, integrating,
    upgrading and administering Rational development environments that
    are: flexible, scalable, performance, available, resilient, secure
    and supportable.
-   Organizational deployment which includes technical deployment, but
    also includes the business change, adoption, best practices,
    enablement and the whole Rational field engagement need to improve
    an organizations development capability.

However, technical deployment needs to be mindful of the requirements
and constraints imposed by organizational deployment.

The workshop would start by reviewing the existing deployment at
\[CLIENT\] and by understanding the business and technical requirements,
and constraints that the environment must support now and in the future
as they roll it out to more development teams.

This workshop is conducted as a face-to-face in person meeting, and will
investigate all relevant aspects of technical deployment in a structured
way. For each aspect we will:

-   Clarify the requirement and constraints
-   Understand \[CLIENT\]'s preferred approach and technology
-   Understand what has been deployed to date and what challenges or
    issues \[CLIENT\] has
-   Discuss options and make key recommendations to meet \[CLIENT\]'s
    requirements, constraints and needs.

**Note**: Times in this agenda are based upon local time \[EST\].

**Note**: Topics and links listed are examples of material that will be
discussed. There may be other topics that will be discussed which arent
listed here. Similarly not all topics listed here may in actuality be
discussed. Frequent checkpoints during the actual workshop will refine
and adjust the agenda and required topics as necessary.

**Location**: \[CLIENT\] or IBM location

**Attendees**: \[CLIENT\]

|      |                             |
|------|-----------------------------|
| Name | Role                        |
|      | (Executive Sponsor)         |
|      | (Program/Project Architect) |
|      | (Tools Administrator)       |
|      | (DBA)                       |
|      | (IT Administrator)          |
|      | (Business Owner)            |
|      | role                        |

IBM

|      |             |
|------|-------------|
| Name | Role        |
|      | Facilitator |
|      | Facilitator |
|      | role        |
|      | role        |
|      | role        |

Agenda Day 1, \[Date\]: Understand current situation, future strategy
and plans

-   09:00 - 09:30 Introductions, review agreed scope, focus and agenda
    -   Introductions, roles
    -   This agenda document and any specific required scope and focus
        will be reviewed
    -   Finalize topics, times and breaks

<!-- -->

-   09:30 - 10:00 Present and discuss key consideration when designing
    the technical deployment of IBM Rational environments
    -   IBM to present using the [Deployment planning: Where to
        start?](https://jazz.net/wiki/bin/view/Deployment/DeploymentPlanning)
        topic in the [Deployment
        wiki](https://jazz.net/wiki/bin/view/Deployment/WebHome).

<!-- -->

-   10:00 12:00 Review existing technical deployment and understand
    general requirement, constraints and usage; Review current
    development environment
    -   \[CLIENT\] to present with active discussion:
    -   Current \#users, location distribution, roles
    -   Future \#users, location distribution, roles
    -   Required and current Availability requirements
    -   Required Mean Time to Recovery, Recovery Point Objective,
        Recovery Time Objective etc.
    -   Development disciplines that need to be supported
    -   3rd part integration and migration we need to support
    -   Security, audit and compliance requirements
    -   Review future strategy and plans.
    -   \[CLIENT\] to lead discussion and reference the background
        documentation given to IBM Rational

<!-- -->

-   12:00 13:00 Lunch

<!-- -->

-   13:00 14:30 Understand in detail \[CLIENT\]'s existing
    infrastructure services and preferred middleware/platforms review
    and make key platform, OS and middleware decisions/recommendations
    -   Database, platform, virtualization, HA/DR including back-up etc.
    -   \[CLIENT\] to outline their existing infrastructure services
    -   Start confirming topics to be discussed on Day 2 in greater
        depth

\* 14:30 16:00 Discuss deployment topology, technology and platform
options based upon \[CLIENT\]'s preferred approach and technology, and
available common services

-   [Standard deployment topologies
    overview](https://jazz.net/wiki/bin/view/Deployment/StandardTopologiesOverview)
    wiki topic and sub-topic pages will be the guidance and best
    practice this session is based upon:
-   [Collaborative Lifecycle Management architecture
    overview](https://jazz.net/wiki/bin/view/Deployment/CLMArchitectureOverview)
-   [Planning for multiple Jazz application server
    instances](https://jazz.net/wiki/bin/view/Deployment/PlanForMultipleJazzAppInstances)
-   [Principles of good
    virtualization](https://jazz.net/wiki/bin/view/Deployment/PrinciplesOfGoodVirtualization)
-   [Understanding reverse
    proxy](https://jazz.net/wiki/bin/view/Deployment/UnderstandingReverseProxy)
    -   [Proxy server installation landing
        page](https://jazz.net/wiki/bin/view/Deployment/InstallProxyServers)
-   [Using content caching proxies for Jazz Source
    Control](https://jazz.net/wiki/bin/view/Deployment/ContentCachingProxyJazzSCM)
    Improve SCM read performance from remote locations
-   [System Requirements for IBM Rational Collaborative Lifecycle
    Management (CLM)
    6.0.2](https://jazz.net/wiki/bin/view/Deployment/CLMSystemRequirements602)
-   [Jazz licensing
    explained](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=servers-managing-licenses-in-engineering-lifecycle-management-elm)
    Discuss license and license server options for an Enterprise
    development environment \* Continue confirming topics to be
    discussed on Day 2 in greater depth \* 16:00 17:00 Review progress,
    refine Day 2 agenda
-   Review surfaced issues, recommendations and actions
-   Refine Day 2 agenda
-   Adjust topics, timeslots as needed
-   Wrap-up Day 1

Agenda Day 2, \[Date\]: Detailed discussion of decisions to be made;
in-depth topics

-   09:00 10:00 Review and refine Day 2 agenda
    -   Review surfaced issues, recommendations and actions
    -   Refine Day 2 agenda
    -   Adjust topics and timeslots

<!-- -->

-   10:00 12:00 Capacity planning, performance and monitoring
    -   [CLM Sizing
        Strategy](https://jazz.net/wiki/bin/view/Deployment/CLMSizingStrategy)
        wiki topic will be used as the guidance and best practice for
        capacity planning
    -   [Performance
        datasheets](https://jazz.net/wiki/bin/view/Deployment/PerformanceDatasheetsAndSizingGuidelines)
        wiki page and containing topic pages will be used as the
        guidance and best practice for performance
        -   [Improving the performance of Rational Team Concert by using
            the dynamic cache service in WebSphere Application
            Server](https://jazz.net/wiki/bin/view/Deployment/UsingWebSphereDynaCacheWithRTC)
    -   Discuss developing a production development environment wide
        monitoring configuration, which combines user and automated
        usage with CLM Server Monitoring, database, application server
        and systems monitoring information for the production
        development environment to produce a correlated dashboard.
        Ultimately the key monitoring that needs to be combined to
        produce a correlated dashboard includes:
        -   Concurrent user usage via licensing monitoring from the JTS,
            IBM Rational License Key Server or preferably the Rational
            License Key Server Administration and Reporting tool
        -   CLM Server Monitoring
        -   WAS monitoring
        -   Database server monitoring
        -   VMware monitoring
        -   General systems performance monitoring
    -   [Monitoring: Where to
        Start?](https://jazz.net/wiki/bin/view/Deployment/MonitoringWhereToStart)
        Wiki topic and
        [Monitoring](https://jazz.net/wiki/bin/view/Deployment/DeploymentMonitoring)
        section of the wiki will be used as the guidance and best
        practice for monitoring

<!-- -->

-   12:00 13:00 Lunch

<!-- -->

-   13:00 14:00 High availability and disaster recovery
    -   [Approaches to implementing high availability and disaster
        recovery for Rational Jazz
        environments](https://jazz.net/wiki/bin/view/Deployment/ApproachesToImplementingHAAndDR)
        wiki topic and sub-topic pages will be the guidance and best
        practice this session is based upon:
        -   [Strategies for backup of the Rational Collaborative
            Lifecycle Management Solution and
            Environment](https://jazz.net/wiki/bin/view/Deployment/BackupStrategies)
        -   [Understanding how to install manual failover techniques
            with the Jazz
            solution](https://jazz.net/wiki/bin/view/Deployment/JazzManualFailoverTechniques)
        -   [Implementing application recovery: Example script for a
            Jazz deployment on
            WebSphere](https://jazz.net/wiki/bin/view/Deployment/ImplementingApplicationRecoveryExampleScript)

<!-- -->

-   14:00 15:00 Administration, configuring, tuning and over-flow topics
    -   Roles and responsibilities of Rational Tools Administration Team
    -   How to provide an enhanced development environment service
    -   [Implementation planning and deployment
        roadmap](https://jazz.net/wiki/bin/view/Deployment/ImplementationPlanningAndDeploymentRoadmap)
        wiki topic and sub-topic pages will be the guidance and best
        practice this session is based upon:
        -   [Establishing a systems and software engineering ecosystem
            center of
            excellence](https://jazz.net/wiki/bin/view/Deployment/DeploymentEstablishingACenterOfExcellence)
        -   [Accelerating adoption of software tools and
            practices](https://jazz.net/wiki/bin/view/Deployment/DeploymentAcceleratingAdoption)
        -   [Deployment monitoring and
            tracking](https://jazz.net/wiki/bin/view/Deployment/DeploymentMonitoringAndTracking)
    -   [Patch service for CLM
        applications](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.repository.web.admin.doc/topics/c_patch_svc_clm_app_svrs.html)
    -   [Upgrade
        planning](https://jazz.net/wiki/bin/view/Deployment/UpgradePlanning)
    -   [Upgrade best practice based upon IBM
        experience](https://jazz.net/wiki/bin/view/Deployment/UpgradeBestPracticeBasedUponIBMExperience)

<!-- -->

-   15:00 16:00 Review and wrap-up workshop
    -   Review surfaced issues, recommendations and follow-on actions
    -   Review format of final deliverable

Prerequisites, constrains and background for the workshop

1.  \[CLIENT\] to provide existing Rational technical deployment
    planning and design documentation for review prior to the workshop
2.  The local IBM Rational Team will support all activities prior,
    during and after the workshop for business and technical
    understanding and continuity
3.  \[CLIENT\] and IBM Rational will ensure that the right Tools and
    Infrastructure Administrators, Architects and Specialists can fully
    support the workshop sessions.
4.  IBM Rational will produce a short review report with key
    recommendations after the workshop.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
