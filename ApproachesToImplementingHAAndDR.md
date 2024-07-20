# Approaches to implementing high availability and disaster recovery for Jazz environments 

Authors: Main.TimFeeney, Main.RichRakich 
Build basis: ELM 7.x 

***Please note: as announced with CLM v4.0.6: IBM will be simplifying
the approach to High Availability (HA) for the Rational CLM/Jazz
platform. Customers and IBM are increasingly using other technologies,
such as cloud and virtualization strategies, that provide a solution
which adapts to business demands for both availability and scale in a
cost-effective manner. IBM will be removing support for WebSphere
Application Server based application clustering from the CLM/Jazz
platform for version 5.0. Many of the customers who have evaluated
WebSphere Application Clustering decided that it was too expensive and
complex for the benefits provided for Jazz applications and exceeded
their required availability.***

This set of topic pages provides guidance on potential ways to implement
HA and Disaster Recovery (DR) for Jazz environments using capabilities
of the platforms and middleware you have chosen to deploy your Rational
Jazz environment on. Often this enables you to reuse existing
procedures, configurations and technologies that already use for other
IT systems. There are numerous different approaches, technologies and
implementation options, so this set of topic pages will focus on the
most commonly available and used approaches and technologies. The
implementation options are usually constrained by your organizations
existing approach to using these technologies for HA and DR, so in many
situations we will only provide general guidelines and best practice to
point your infrastructure administrators in the right direction.
Therefore, for many of implementation options we will not provide
detailed installation and configuration guides. Also you should rely
upon the documentation, guidance and best practice, services and support
of middleware vendors to install and configure the respective
middleware.

This page aims to provide pragmatic and cost-effective approaches to
achieving HA and DR that meet your requirements and needs. There is the
trade-off between costs/complexity of the approach and the level of
availability you can achieve, see [Pragmatic approach to achieving your
required HA and DR](#PragmaticApproach).

Please read to following introductory topics to gain an understanding of
key HA and DR principles:

-   [High availability principles](HighAvailability)
-   [Disaster recovery principles](DisasterRecovery)

## Plan for failure

Despite the best guidance, best practice, planning, deployment and
management, your Jazz development environment will someday fail. When
properly designed,
[implemented](DisasterRecovery#DRProcessAndProcedures) and
[practiced](DisasterRecovery#QuarterlyRecoveryDrills), HA and DR
approaches will help you manage failure and recovery within acceptable
time frames. If HA, DR, and backup procedures and policies are habits,
then downtime is reduced.

You must recommend and implement suitable HA and DR to meet the
customers ***REAL*** requirements and needs:

-   HA is system design and implementation that achieves system and data
    availability most or all of the time
    -   HA usually focuses on availability within the primary datacenter
-   DR leverages technology and automation to ensure business continuity
    in the event of an unanticipated event
    -   DR usually focuses on failover to a secondary datacenter
    -   Backup is the most basic part of DR and should always be a part
        of a DR solution
-   You are likely to achieve higher availability than you target if you
    focus on the right aspects

\#PragmaticApproach

## Pragmatic approach to achieving your required HA and DR

An administration team that is developing a HA and/or DR plan for a
development environment must weigh the need to recover quickly and
completely against the cost to implement the recovery. Also the impact
to the I/O performance of the environment should be considered, as well
as the environment [recovery time objective
(RTO)](DisasterRecovery#RecoveryTimeObjective). In other words, how much
time is available to fully recover the environment with all critical
development operations up and running again? Another important factor to
consider is the environment's [recovery point objective
(RPO)](DisasterRecovery#RecoveryPointObjective): How much data is lost,
or at what actual recovery point-in-time is all data current?

***[The expense of
availability](http://www.redbooks.ibm.com/redbooks/pdfs/sg247700.pdf)***

The above image shows that there is an important balance between the
costs of failure, and the costs of HA and DR.

HA and DR requirements for systems that support business or national
critical capabilities, such as stock-exchanges, government agencies,
hospitals, banks or e-commerce website, are likely to be much higher
that a typical development environment, unless the development
environment needs to have similar available as the system it supports.
Even in this situation the required availability is usually less that
the business or national critical system!

As you design your HA and DR strategy, consider the inconveniences
(costs) if your SCM system goes down for: 1 day, 4 hours, 1 hour, 15
minutes, 15 seconds, etc. In many cases, the costs of ensuring very
small outage windows are not offset by the organization cost to design,
implement and practice HA/DR.

Additional business continuity costs can include:

-   Hardware and software
    -   Additional datacenters, servers, physical components
    -   Additional software, licenses
-   People
    -   Product admins, IT admins, off-site contractors, 3rd-party
    -   Business continuity procedures, planning, training,
        implementation, testing
    -   And after deployment, remember to practice, practice, practice
-   Determining when to actually implement HA and DR
    -   Monitoring: automatic and/or manual
    -   Tools, logging, policies, procedures
    -   And of course, more practice, practice, practice

Only consider and implement a HA and/or DR solution that you are sure
your organization is capable of supporting. If your organization has no
experience with a technology or lack of general administrative maturity
to supporting it, poorly implementing and supporting it may cause more
outages than it is intended to prevent!

Make sure that your organization [measures the actual
availability](HighAvailability#MeasuringAvailability) it achieves.
Document potential and actual failure scenarios within your
organization, and use them to incrementally improve you HA and DR
solution to further meet your needs.

## Typical and realistic requirements for HA and DR for a Rational Jazz environment

Below are listed the key measure of HA and DR and respective realistic
and typical requirements that customer and IBM development environments
have:

-   **[Availability](HighAvailability#AvailabilityNumberOfNines)** -
    Most customers have an availability requirement for their
    development environment in the range of 99.5 - 99.7 for supported
    business operating hours. A few customer have a ***REAL***
    requirement for 99.9 availability, but be very careful not to set
    your requirement higher than needed as the cost of achieving very
    high levels of availability can be prohibitive! Further, many
    customer focus their requirement for HA within their primary
    datacenter and explicitly exclude DR scenarios requiring failover to
    a secondary datacenter or major rebuild of the primary datacenter.
    It is often useful to understand the required availability of
    similar systems within your organization and the level of
    availability supported by [common IT services that you could
    reuse](DeploymentPlanning#ReuseCommonManagedITInfrastructureServices),
    which will help you define a realistically achievable and needed
    requirement for availability.

<!-- -->

-   **[Mean time to recovery
    (MTTR)](HighAvailability#MeanTimetoRecovery)** - Again we often see
    MTTR requirements for recovery focused on HA within the primary
    datacenter, rather than DR scenarios. We see typically see MTTR
    requirements in the range of 2-6 hours for a development environment
    within the primary datacenter.

<!-- -->

-   **[Recovery point objective
    (RPO)](DisasterRecovery#RecoveryPointObjective)** - Most
    organizations base their required RPO on a nightly or once a day
    [offline back-up](BackupCLM). This constrains your achievable RPO to
    24 hours with recovery point in time at the time of the back-up.

<!-- -->

-   **[Recovery time objective
    (RTO)](DisasterRecovery#RecoveryTimeObjective)** - The required RTO
    we see in customers is usually in the range of 4 hours to 2 days.
    However, most organizations realize that in the event of a major
    primary datacenter failure, the development environment will often
    be one of the last systems to be restored.

\#FailureScenarios

## Failure scenarios with general approach to resolving failure and possible platform/middleware implementations

| Failure scenario | General approach to resolving failure | Possible platform/middleware implementations | Possible MTTR for HA and achievable RTO for DR |
|:---|:---|:---|:---|
| **Jazz application failure** | Monitoring scripts detect that the Jazz application is unavailable Scripts try to restart the Jazz application a number of times If the Jazz application does not restart successfully, consider applying the approach to resolving a WAS failure **NOTE: depending on experience, cost and complexity of setting-up the application monitoring and recovery, you could treat a Jazz application failure using the same approach as a single application server failure** | [Jazz application recovery using PowerHA](ImplementingApplicationHAUsingPowerHA#JazzApplicationRecovery) [Jazz application recovery using VMware HA](ImplementingApplicationHAUsingVMwareHA#JazzApplicationRecovery) | 5 - 10 minutes |
| **WAS failure** | Monitoring scripts detect that WAS is unavailable Scripts try to restart WAS a number of times and then the Jazz application(s) If WAS does not restart successfully, consider applying the approach to a single application server failure **NOTE: depending on experience, cost and complexity of setting-up the WAS monitoring and recovery, you could treat a WAS failure using the same approach as a single application server failure** | [WAS recovery using PowerHA](ImplementingApplicationHAUsingPowerHA#WasRecovery) [WAS recovery using VMware HA](ImplementingApplicationHAUsingVMwareHA#WasRecovery) [Example script for a Jazz deployment on WebSphere](ImplementingApplicationRecoveryExampleScript) [Warm standby WebSphere Application Server recovery using WebSphere Network Deployment](WarmStandbyWASRecoveryUsingWASND) | 10 - 15 minutes |
| **Single application server failure** | This could be due to HW, OS or 3rd party SW errors or failures The middleware hypervisor detects the failure and invokes the restart or fail over of the application server | [Single LPAR recovery using PowerHA](ImplementingApplicationHAUsingPowerHA#SingleLPARRecovery) [Single virtual server recovery using VMware HA](ImplementingApplicationHAUsingVMwareHA#SingleVirtualServerRecovery) | 15 - 20 minutes |
| \* Database failure\* | This could be due to the database servers, storage or network connections failing | [Database recovery](DatabaseRecovery) | 15 minutes to 4 hours |
| **Web server tier failure** | A common strategy for HA in the web server tier is the use of a load balancer that feeds a reverse proxy server |  | 15 minutes - 2 hours |
| **Jazz indexes corrupted** | This should never happen due to a Jazz application, WAS or single application server failure The only time this could happen is due to a storage corruption | [Jazz indexes, backup and recovery considerations](JazzIndexesBackupAndRecoveryConsiderations) | 1 - 24 hours |
| **Primary data center or site failure** | A lost or inaccessible site will likely entail loss of ALL Jazz server resources and some data loss This failure might be due to natural (fire, flood, tornado etc.) or human (hacking, malicious damage, stupidity etc.) failure **Note:** often re-establishing a development environment will be less of a priority than re-establishing other business critical systems | DR using PowerHA and database back-up or clustering TBD DR using VMware technologies and database back-up or clustering TDB | 4 hours to 2 days |
| **Network failure** | The local area network (LAN) or wide area network (WAN) is offline Users will notice that all applications (including Jazz applications) are unresponsive Users that are developing in Eclipse workspaces will be able to continue their work on software development assets, but no data will be stored to the Jazz repositories Often, networks may experience significant slowdown, but they are rarely offline If there is a network outage, it impacts all users and will be handled by IT support as a top priority problem. | No special procedures by the Jazz administrators are warranted | 15 minutes to 2 days |
| **Storage failure** | This would be due to server disk, Storage Area Network (SAN) or Network Area Storage (NAS) failure Storage failure can cause loss of data, and users will notice that the Jazz applications and Jazz server seem either unresponsive, or unable to store changes (when information returned to user is from the server cache) Users that are developing in Eclipse workspaces will be able to continue their work on software development assets, but no data will be stored to the Jazz repositories The use of SAN and NAS technologies can help reduce the risk of a single disk failure causing an unplanned outage | [Storage recovery](StorageRecovery) | 15 minutes to 2 days |

*Please note*: If two or more failures occur at the same time, it will
probably take longer to recover than the longest MTTR of all the
individual failures. In a worst case scenarios, you will not be able to
restore all the individual parts of your Rational environment to a
consistent state, resulting in you having to recovering from your [Jazz
back-up](BackupCLM). For this reason it is essential that you always
back-up your environment on a regular basis as the last line of defense
for all HA and DR scenarios.

##### Related topics: [related-topics]

-   [Implementing application HA using
    PowerHA](ImplementingApplicationHAUsingPowerHA)
-   [Implementing application HA using VMware
    HA](ImplementingApplicationHAUsingVMwareHA)

##### External links: [external-links]

-   None

##### Additional contributors: 
- None [additional-contributors-none]
