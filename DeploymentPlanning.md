META:TOPICINFO{author="tfeeney" date="1696875576" format="1.1"
version="1.64"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Deployment planning: Where to start? [deployment-planning-where-to-start]

DKGRAY Authors: Main.StevenBeard Build basis: None ENDCOLOR

TOC{title="Page contents"}

Rational deployment has two distinct aspects:

-   **Technical deployment** of Rational products and solutions that
    includes [planning and design](DeploymentPlanningAndDesign);
    [installing, upgrading, and
    migrating](DeploymentInstallingUpgradingAndMigrating);
    [integrating](DeploymentIntegrating); [configuring and
    tuning](DeploymentAdminstering); [monitoring](DeploymentMonitoring);
    and [troubleshooting](DeploymentTroubleshooting). Technical
    deployment results in a Rational development environment that is
    flexible, scalable, available, resilient, secure, and supportable.

<!-- -->

-   **Organizational deployment,** which includes technical deployment,
    but also includes the business change, adoption, development best
    practices, enablement, and the whole Rational field engagement
    needed to improve an organization's development capability.

This topic outlines several key planning and design considerations for
designing a Rational development environment. These considerations focus
on the environment and non-functional options that typically effect how
successful your deployment and ultimate adoption will be.

## Introduction and approach

One of the questions that customers most frequently ask is:

***How should we deploy an enterprise Rational environment that is:
flexible, scalable, performant, available, resilient, secure and
supportable etc.?***

Quite rightly, you balk at an answer that only points you to the system
requirements or gives you a myriad of permutations along with an it
depends answer. \*You want stronger guidance\*

While no recipes or approaches guarantee success, this topic and section
outline the general approach for planning and designing a Rational
development environment that meets your requirements. Subsequent topic
sections cover specific design considerations.

\#RationalDeploymentWayForward

## Rational deployment way forward

-   Focus on a few recommended deployment topologies: the guidance and
    best practice captured in this wiki
-   Focus development and testing, particularly system and performance
    testing, on the recommended topologies
-   Reduce permutations that are of little or no business or technical
    value to customers
-   Focus Rational Field engagement and best practices on the
    recommended topologies via presales, services, and support
    engagements
-   Provide one repository for all additional deployment guidance and
    best practices for customers, partners, and Rational staff: this
    Deployment wiki!

***Vision: Improve your time to value by providing more prescriptive
guidance and simplifying the deployment of Rational solutions***

\#DesignPlanDeployMonitorAndManage

## Plan and design, deploy, monitor and manage for flexibility, scalability, and performance

1 Design and plan the deployment of your Rational development
environment against your potential usage model, functional and
non-functional requirements, constraints, etc. 1 Build flexibility and
scalability into the design and deployment 1 Monitor user and automated
usage against Rational application and system performance 1 Manage your
environment to meet your changing requirements, constraints, and needs
while maintaining adequate performance

The following sections outline key considerations for designing and
planning a development environment against this basic approach.

\#ProperlyConsiderAndDocument

## Properly consider and document the real non-functional requirements for your development environment

The following list includes some of the most critical non-functional
requirements you must understand and document for a development
environment:

-   **Capacity, performance, and monitoring:** Consider common user
    operations as a bench marks of required performance as well as
    automated monitoring
-   **[High availability:](HighAvailability)** What is the real
    availability you need to support your operational systems?
    -   Almost no organizations need their software development
        environments to be 100 available!
-   **[Disaster recovery:](DisasterRecovery)** What is a reasonable
    recovery time and how much data can you afford to lose?
-   **Security:** What corporate, industry, compliance or government
    security standards to you need to adhere to?
-   **Audit and control:** What are your organization, industry, or
    regulatory requirements?
-   **Compliance:** What industry or regulatory standards to you need to
    comply with?

\#DevelopAUsageModel

## Develop a usage model for your Rational development environment

Consider short, medium, and long-term. Understand the potential capacity
and scalability requirements from the outset so that you can design in
flexibility to meet your changing needs.

At a minimum, this model should include this information:

-   Your development roles
-   Numbers of staff per role
-   Staff locations and numbers per role
-   Expected usage or process per role

Further, try to estimate the amount of SCM data the environment will
need to support, both initially from migrating for previous SCM tools
and the rate of growth of data over time.

\#DesignAnEnvironmentThatCouldScale

## Estimate your potential usage, but design an environment that can scale to support at least twice the usage

Estimate your potential usage based on a potential usage model.

Use IBM Techline (available through your IBM representative) and the
local Rational Field Team to help you size your environment. IBM
Techline provides this assistance:

-   IBM server sizing for IBM software and for selected software vendors
-   Solution design, configuration, validation and assistance.

Build as much flexibility, scalability, and performance into your design
by using these methods:

-   [Application server virtualization](PrinciplesOfGoodVirtualization)
-   Separation of Jazz applications onto separate virtual or physical
    servers: [use an enterprise standard
    topology](StandardTopologiesOverview)
-   Database clustering; for example, Oracle RAC and DB2 HADR
-   A [reverse proxy server](UnderstandingReverseProxy) that you can use
    to refactor your environment in the future

\#ConsiderUsingVirtualization

## Consider using virtualization for flexibility and scalability

Virtualize the application tier, including your [reverse proxy
server](UnderstandingReverseProxy). Database tier flexibility and
scalability is best served by database clustering.

Well-managed virtualized servers permit modifying CPU, RAM, and disk
image sizes with much greater ease than physical servers.

A virtualized infrastructure can support certain levels of [high
availability and disaster recovery](ApproachesToImplementingHAAndDR):

-   Monitor the application, application server, and virtual server, and
    automatically restart if unresponsive
-   Cope with single hardware failure; for example, VMware HA and
    PowerHA
-   Failover between data centers; for example, VMware vSphere/vMotion,
    Platespin.

[Principles of good virtualization](PrinciplesOfGoodVirtualization):

-   Manage and monitor virtualization
-   Ensure that CPU, memory, and network resources are dedicated and
    uncapped
-   Do not overcommit a virtualization environment

\#ReuseCommonManagedITInfrastructureServices

## Reuse common managed IT infrastructure services

The infrastructure services you reuse might include the following
services:

-   Central database service
-   Virtualization or cloud environment
-   Backup, high-availability, and disaster-recovery services
-   Authentication and licensing
-   Complete hosting or Platform-as-a-Service offering

Make sure that the Service-Level Agreement (SLA) meets your
requirements:

-   Typically an SLA is an operational SLA, so it is more than
    sufficient for a development environment
-   Usually, it has a higher quality of service than an individual team
    can support

Separate infrastructure from tools and methods administration if
possible.

\#StartByMakingTheMajorDecisions

## Start by making major decisions about platform, operating systems (OS), and middleware

Where possible, choose the middleware and editions that meet your
ultimate requirements:

-   Reduce the need for major migrations as you scale-up the environment
-   Reduce the amount of time you spend re-learning how to tune new
    middleware or editions

Where possible, choose a platform, OS, and middleware that you already
have experience with. Standardize on the same platform, OS, middleware,
editions, and versions for the whole of your Rational environment, where
possible.

Choose a [deployment topology](StandardTopologiesOverview) that meets
your requirements and that can scale to meet your needs. It is easier to
scale-down an enterprise topology/environment than scale-up an
evaluation topology.

\#PlanForMultipleInstances

## Plan for multiple instances of specific application servers

Plan for multiple application instances if you think you are going to
scale to need them:

-   Split teams/projects across multiple instances along organizational
    boundaries or due to low dependency
-   Typically Rational Team Concert and occasionally Rational Quality
    Manager require multiple instances
-   Rule of thumb: A typical instance of the Change and Configuration
    Management (CCM) application can support 350-400 concurrent users

Each instance requires a separate context root; for example, two
instances of the CCM application might be ccm1 and ccm2.

Cross-instance working is supported by Open Services for Lifecycle
Collaboration (OSLC) work item linking and distributed SCM.

For more details, see [Planning for multiple Jazz application server
instances](PlanForMultipleJazzAppInstances).

\#YouCantManageOrImprove

## Management and improvement are impossible without monitoring

Understand what systems monitoring methods you already perform within
your organization and reuse them if appropriate. Monitoring methods
might include homegrown tools, 3rd-party packages, or Tivoli monitoring.

A well-managed development environment is monitored. Identify a handful
of measures and start capturing them on a regular schedule, either
manually or automatically. Consider measuring all of the following
information:

-   **Database:** Uptime, database size, log size, index age, time to
    make backups, size of backups, threads, sockets, and query
    statistics
-   **Application server, web server:** Uptime, CPU, JVM size, threads,
    connections, and memory usage
-   **Licenses:** Number and type used
-   **Network:** Latency, bandwidth, pings, tracert, and packet loss

For more guidance and best practices, see the [Monitoring
section](DeploymentMonitoring) of the Deployment wiki.

\#ManageYourEnvironment

## Manage your environment to meet your changing requirements, constraints, and needs while maintaining adequate performance

Actual usage will always differ from the potential usage model you
originally captured for an environment:

-   Maintain a living usage model to understand how to an environment is
    used
-   Use the system, user, and usage monitoring to inform the living
    usage model
-   Review your design constraints and architectural decisions, and
    design against the current and new future usage

To avoid an under-performing environment, use the flexibility you built
in to scale the environment.

Measure and review whether other non-functional requirements and targets
are being met; for example, HA/DR, audit/control and compliance:

\* All non-functional requirements must have specific and measurable
targets \* The Rational environment must perform, is not a requirement

\#IncludeAReverseProxy

## Include a reverse proxy

A reverse proxy provides a web server, on a single host, that forwards
requests to the Jazz applications.

The benefit of using a reverse proxy is the ability to mask the
complexity or changes to the underlying deployment from your end users.
You can start with a simpler topology and refactor to a more complex
topology later as needed. For more information, see the [understanding
reverse proxy](UnderstandingReverseProxy) topic.

You can refactor the physical topology and still maintain links:

-   Enhance or replace hardware: scale hardware vertically
-   Split Jazz applications onto separate hardware: scale hardware
    horizontally
-   Scale hardware horizontally and vertically

\#HardwareAndSoftwareRequirements

## Hardware and software requirements

Before you begin the installation, verify that your hardware and
software meet the minimum requirements. A 64-bit operating system and a
minimum of 8 GB of server memory provide the best environment for
running Jazz Team Server. For a complete list of system requirements for
the Rational solution for CLM, the Rational solution for SSE, and their
related products, see [Installing, upgrading, and
migrating](DeploymentInstallingUpgradingAndMigrating) section.

\#DeploymentWorkshopsAndReviews

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
and refine Day 2 agenda, and wrap-up Day 1.

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
post-sales. A more detailed sample agenda can be found at [Deployment
Workshops and Reviews in Detail](DeploymentWorkshopsAndReviewsDetail).

##### Related topics: [Principles of good virtualization](PrinciplesOfGoodVirtualization), [Standard deployment topologies overview](StandardTopologiesOverview), [Planning for multiple Jazz application server instances](PlanForMultipleJazzAppInstances), [Understanding reverse proxy](UnderstandingReverseProxy), [High availability principles](HighAvailability), [Disaster recovery principles](DisasterRecovery), [Approaches to implementing high availability and disaster recovery for Jazz](ApproachesToImplementingHAAndDR), [Typical Deployment Planning Workshop Questions](DeploymentPlanningTypicalQuestions) [related-topics-principles-of-good-virtualization-standard-deployment-topologies-overview-planning-for-multiple-jazz-application-server-instances-understanding-reverse-proxy-high-availability-principles-disaster-recovery-principles-approaches-to-implementing-high-availability-and-disaster-recovery-for-jazz-typical-deployment-planning-workshop-questions]

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="proxyblackbox.png"
attachment="proxyblackbox.png" attr="h" comment="" date="1368981966"
path="proxyblackbox.png" size="95698" user="sbeard" version="2"}
META:FILEATTACHMENT{name="monitor.png" attachment="monitor.png" attr="h"
comment="" date="1394676697" path="monitor.png" size="124808"
user="sbeard" version="1"} META:FILEATTACHMENT{name="ccms.png"
attachment="ccms.png" attr="h" comment="" date="1394676713"
path="ccms.png" size="69150" user="sbeard" version="1"}
META:FILEATTACHMENT{name="requirements.png"
attachment="requirements.png" attr="h" comment="" date="1394676729"
path="requirements.png" size="36791" user="sbeard" version="1"}
META:FILEATTACHMENT{name="scalability.png" attachment="scalability.png"
attr="h" comment="" date="1394676745" path="scalability.png"
size="124676" user="sbeard" version="1"}
META:FILEATTACHMENT{name="reuse.png" attachment="reuse.png" attr="h"
comment="" date="1394676760" path="reuse.png" size="127840"
user="sbeard" version="1"}
