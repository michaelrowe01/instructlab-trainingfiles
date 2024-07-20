META:TOPICINFO{author="michaelrowe" date="1699640800" format="1.1"
version="1.37"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# High availability principles DKGRAY Authors: Main.GrantCovell, Main.StevenBeard, Main.StephaneLeroy, Main.ScottRich Build basis: None [high-availability-principles-dkgray-authors-main.grantcovell-main.stevenbeard-main.stephaneleroy-main.scottrich-build-basis-none]

ENDCOLOR

TOC{title="Page contents"}

High availability (HA) and disaster recovery (DR) are both related
aspects of [Wikipedia: Business continuity
planning](http://en.wikipedia.org/wiki/Business_continuity_planning).

***Availability is a measure of the time that a server or process
functions normally for general usage, as well as a measure of the amount
of time that the recovery process requires after a component failure.
High availability is system design and implementation that achieves
system and data availability almost all of the time, 24 hours a day, 7
days a week, and 365 days a year. High availability does not equate to
100 availability. To achieve 100 availability is not a cost-effective
reality for the large majority of implementations today; rather, it is a
goal - [IBM High Availability Solution for IBM FileNet P8
Systems](http://www.redbooks.ibm.com/redbooks/pdfs/sg247700.pdf).***
***High availability is a system design approach and associated service
implementation that ensures a prearranged level of operational
performance will be met during a contractual measurement period -
[Wikipedia: High
availability](http://en.wikipedia.org/wiki/High_availability).***

As Rational development environments become larger and support larger
user communities, HA of these environments is becoming increasingly
essential within most organizations. Development is increasingly
considered a core business function by many organizations and as such
poor availability of the Rational development environment used to
support it can have large business cost and capability implications.

The related [Disaster Recovery](DisasterRecovery) topic focuses upon a
major failure of the primary data center requiring failover to a
secondary disaster recover data center or fundamental rebuild of the
primary data center.

This topic outlines the different principles of HA that you should
consider when designing a Rational development environment. It is
critical that HA is considered from the outset of designing your
environment because the design itself will constrain the HA solution. HA
that is developed as an afterthought may result in significant rework of
the environment or result in a suboptimal solution. However, the first
thing to consider is what are your organizations **real** requirements
for HA based on your business and technical needs and requirements for
the environment itself.

\#AvailabilityNumberOfNines

## Availability - "number of nines"

Availability is usually expressed as a percentage of up-time. The notion
of "number of nines" relates to increasingly higher levels of
availability, where a greater number of nines signifies a greater
percentage of HA or up-time. For example, "Five nines" equates to an
up-time of 99.999.

The following table shows the downtime per year, month and week allowed
for a particular percentage availability assuming that the environment
is required 24x7x365(6) days a year.

***Percentage availability table***

\#MeasuringAvailability

## Measuring availability

Availability is measured in percentage of time. If an environment is
available 99 of the time for normal business operation, the environments
availability is 99. This availability percentage translates to the
average of the specific amount of downtime per day, per month or per
year.

To truly measure the availability of an environment, we must first
differentiate the planned outages and the unplanned outages. Planned
outages take place when the operations staff takes a server offline to
perform backups, upgrades, maintenance, and other scheduled events.
Unplanned outages occur due to unforeseen events, such as power loss, a
hardware or software failure, user operator errors, security breaches,
or natural disasters.

Availability is usually only measure for supported business operating
hours for an environment. Some organizations only support Rational
development environments for core business hours, such as 08:00 - 19:00
Monday to Friday. Increasingly due to geographically distributed
development and development outside of core business hours, environments
are often supported for extended hours, sometimes approaching
24x7x365(6). However, it is always good practice to have regular
scheduled outage windows for back-up and maintenance. Further, it is
critical that administrative staff for all tiers of the Rational
development environment are available on site or on call for supported
hours to ensure that any HA/DR solutions perform correctly and to
support unforeseen failures!

It is important that you establish a way to measuring your environments
availability to be able to assess whether you are meeting or exceeding
your required availability.

\#MeanTimetoRecovery

## Mean Time to Recovery (MTTR)

MTTR is the average time that an environment will take to recover from
all or specific failure scenarios. Sometimes an organization will focus
on only HA scenarios within the primary data center and exclude DR
scenarios.

##### Related topics: [Disaster recovery](DisasterRecovery), [Approaches to implementing high availability and disaster recovery for Rational Jazz environments](ApproachesToImplementingHAAndDR) [related-topics-disaster-recovery-approaches-to-implementing-high-availability-and-disaster-recovery-for-rational-jazz-environments]

##### External links: [external-links]

-   [IBM High Availability Solution for IBM FileNet P8
    Systems](http://www.redbooks.ibm.com/redbooks/pdfs/sg247700.pdf) -
    some of the descriptions on this page are strongly derived from this
    IBM Redbook.
-   [Deploying Rational Team Concert on WebSphere Application Server for
    high availability using idle
    standby](http://www.ibm.com/support/docview.wss?rs=3488&uid=swg21390906)

##### Additional contributors: Main.HariVetsa, Main.MattLavin [additional-contributors-main.harivetsa-main.mattlavin]

META:FILEATTACHMENT{name="nines.jpg" attachment="nines.jpg" attr="h"
comment="" date="1367712401" path="nines.jpg" size="95092"
user="gcovell" version="1"} META:FILEATTACHMENT{name="ha_expense.jpg"
attachment="ha_expense.jpg" attr="h" comment="" date="1367712620"
path="ha_expense.jpg" size="38073" user="gcovell" version="1"}
