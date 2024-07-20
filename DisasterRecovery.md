META:TOPICINFO{author="sbeard" date="1429600857" format="1.1"
version="1.20"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Disaster recovery principles DKGRAY Authors: Main.StevenBeard, [DanToczala](Main.DavidToczala), Main.RalphSchoon Build basis: None [disaster-recovery-principles-dkgray-authors-main.stevenbeard-dantoczala-main.ralphschoon-build-basis-none]

ENDCOLOR

TOC{title="Page contents"}

High availability (HA) and disaster recovery (DR) are both related
aspects of [Wikipedia: Business continuity
planning](http://en.wikipedia.org/wiki/Business_continuity_planning).

***Disaster recovery is the process, policies and procedures related to
preparing for recovery or continuation of technology infrastructure
critical to an organization after a natural or human-induced disaster -
[Wikipedia: Disaster
recovery.](http://en.wikipedia.org/wiki/Disaster_recovery)***

This topic focuses upon a major failure of the primary data center
requiring failover to a secondary disaster recover data center or
fundamental rebuild of the primary data center.

The related [High availability principles](HighAvailability) focuses on
failure scenarios and recovery within the primary data center.

This topic outlines the different principles of DR that you should
consider when designing a Rational development environment. It is
critical that DR is considered from the outset of designing your
environment because the design itself will constrain the DR solution. DR
that is developed as an afterthought may result in significant rework of
the environment or result in a suboptimal solution. However, the first
thing to consider is what are your organizations **real** requirements
for DR based on your business and technical needs and requirements for
the environment itself.

\#RecoveryPointObjective

## Recovery point objective (RPO)

RPO (measure in time) is the maximum tolerable period of data,
information and/or development effort etc. that can be lost from an
environment due to a DR failure. An RPO of 1 hour means that an
organization can always revert back to a restore point that is never
more than one hour old. This would require that the organization
executes backups or equivalent DR solutions every hour. Practically, a
development environment may have a RPO of one day, which may mean that
data is backed up every night at a specific time. Some organizations
have a requirement that their development environment has an RPO less
than 24 hours, which will usually require advanced approaches to back-up
online.

\#RecoveryTimeObjective

## Recovery time objective (RTO)

RTO (measured in time) is the measure of how long it takes an
organization to restore services through either HA, DR, or any
combination. An RTO of 15 minutes means that an organization can restore
its environment within 15 minutes or less. Practically, most development
environments measure their RTO in hours. As surprising as it may seem,
some organizations measure RTO in days.

\#DRQualityOfService

## DR quality-of-service

Most organizations typically consider four different DR
quality-of-service (QoS) levels for their enterprise:

-   Platinum: RPO = seconds, RTO = under two hours. Delivered by a Tier
    7 infrastructure like GDPS.
-   Gold: RPO = two hours, RTO = six hours. Delivered by a Tier 4/5
    database log mirror/log apply solution.
-   Silver: RPO = 24 hours, RTO = 48 hours. Delivered by a RPiT backup
    capability using a Tier 1-3 approach.
-   Bronze: RPO = 24 hours, RTO = 48 hours. Delivered by nightly backups
    for the purpose of DR using a Tier 1-3 approach.

Most development environments require bronze or silver disaster recover
QoS. If the operational systems the development environment supports are
business critical and may require timely development changes, a gold QoS
maybe required. Only a very few development environment that support
nationally critical operational systems, or massive national or
international banking systems will ever require platinum QoS.

The primary question you should ask is: "How long can my operational
systems go without being able to make a critical development change?"
Further, does this require the whole development environment or just
part?

Secondary questions that might contribute to deciding the QoS level
require include:

-   How much in lost productivity does it cost your organization to have
    the development environment down per hour/day?
-   What are the implications of loosing some of you development data
    depending upon the RPO of your QoS level (quality and/or
    compliance)?
-   Would a limited development environment allow you to make critical
    development changes for operational systems, while you recover the
    development environment more slowly?
-   What is the balance between the cost of your DR solution and the
    resultant cost due to different QoS levels?

\#DRProcessAndProcedures

## DR process and procedures

The following phases are the phases of any DR process. This section
outlines the high-level steps needed for proper DR. A separate
step-by-step DR document should be made available so administrators who
are unfamiliar with Jazz can also perform these operations. The last
subsection highlights the need to exercise these processes on a regular
basis to ensure that DR processes and procedures provide adequate
mitigation of the risks associated with loss of the Jazz systems and
their data.

Some good examples of DR capabilities and processes can be seen in the
Jazz Team Server Backup Details and the RRC Backup and Restore documents
on the Jazz wiki site.

### Notification/activation phase

During this phase, the Jazz administrator becomes aware of a loss of
service. In some scenarios, this is detected electronically, and
automated processes are kicked off. In other scenarios, the notification
is more manual in nature.

After the Jazz administrator is aware of a potential loss of service,
other impacted parties need to be notified immediately. At this point,
the Jazz administrator and a other stakeholders will need to assess and
identify the problem, and the correct DR procedures need to be
identified and executed.

-   Notification procedures

<!-- -->

-   Damage assessment

<!-- -->

-   Plan activation

### Recovery phase

During this phase, recovery assets are put into place and the DR
procedures are completed. Recovery refers to the recovery of service for
the end users and stakeholders of the Jazz infrastructure.

-   Sequence of recovery activities

<!-- -->

-   Recovery procedures

### Reconstitution phase

After service--possibly at a reduced performance or capacity--has been
restored, the original issue must be addressed. After the cause of the
loss of service has been identified and addressed, plans for moving back
to the original production systems must be made and executed. This
resumption of normal operations should occur with as little impact as
possible to the Jazz user community.

-   Primary site recovery

<!-- -->

-   Primary site replacement

\#QuarterlyRecoveryDrills

## Quarterly recovery drills

Several staff members should be trained and practiced in DR procedures.
A regular DR drill enforces the training and verifies that the
infrastructure and procedures are working and up-to-date.

The process to back up the repositories requires that the Jazz server be
shut down in order to ensure that database integrity is maintained. Full
backups, as opposed to incremental backups, should be performed, in
order to ensure database integrity. After the backup is completed, the
Jazz server processes can be restarted.

##### Related topics: [Back up the Rational solution for Collaborative Lifecycle Management](BackupCLM), [High availability principles](HighAvailability), [Approaches to implementing high availability and disaster recovery for Rational Jazz environments](ApproachesToImplementingHAAndDR) [related-topics-back-up-the-rational-solution-for-collaborative-lifecycle-management-high-availability-principles-approaches-to-implementing-high-availability-and-disaster-recovery-for-rational-jazz-environments]

##### External links: \* [Wikipedia: Business continuity planning](http://en.wikipedia.org/wiki/Business_continuity_planning) [external-links-wikipedia-business-continuity-planning]

-   [Wikipedia: Disaster
    recovery.](http://en.wikipedia.org/wiki/Disaster_recovery)
-   [Disaster Recovery
    levels](http://www.ibmsystemsmag.com/mainframe/administrator/backuprecovery/Disaster-Recovery-Levels/)

##### Additional contributors: None [additional-contributors-none]
