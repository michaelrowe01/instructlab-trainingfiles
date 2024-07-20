META:TOPICINFO{author="johna_5fowen" date="1454684229" format="1.1"
reprev="1.14" version="1.14"}
META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Deployment example: IBM Hursley DevOps environment DKGRAY Authors: JohnOwen Build basis: None [deployment-example-ibm-hursley-devops-environment-dkgray-authors-johnowen-build-basis-none]

ENDCOLOR

TOC{title="Page contents"}

This article describes the architecture, topology, and specification of
the Jazz service offering provided by the DevOps Infrastructure (DOI)
organization, based in Hursley, England. Part of IBM Software Group, DOI
provides this service to the UK development community and its
distributed worldwide teams.

**Definition:** *Jazz repository* is the name that DOI has given to the
Jazz Team Server and the applications (Rational Team Concert, Rational
Quality Manager) hosted on it. Sometimes, this is referred to as a *Jazz
family* or *Jazz instance*. Technically speaking, the repository refers
to the name of the server portion of the URL. For example, the Jazz
applications accessed via the following URLs are part of the Jazz
repository **jazz987**:

<https://jazz987.hursley.ibm.com:9443/jazz/web>
<https://jazz987.hursley.ibm.com:9443/qm/web>

## Architecture overview

***Figure 1. Hursley Jazz service - High-level architecture***

Figure 1 shows the high-level architecture of the service and includes
the following components:

-   [Logical partitions
    (LPARs)](http://en.wikipedia.org/wiki/Logical_partition_28virtual_computing_platform29)
    hosting Jazz repositories
-   Rational Reporting for Development Intelligence (RRDI)
-   Proxy
-   Jazz build engines
-   End users
-   Tivoli Storage Manager
-   Tivoli Monitoring

Each component is described in the following sections.

### LPARs hosting Jazz repositories

The service currently hosts approximately 20,000 users on 100 Jazz
repositories hosted on 13 logical partitions (LPARs). Most of these
instances are production repositories. Typically 10 to 15 test
repositories are also provided to allow teams to test new function and
verify plug-ins and process configurations against new releases of Jazz.
The number of LPARs fluctuates as repositories are moved to LPARs hosted
on new hardware. The total number of repositories hosted has fluctuated,
too, as projects reach the end of their lifecycle and are archived, and
as new teams move to Jazz. The Jazz service was originally set up with
Rational Team Concert 1.0. This release didn't support the
compartmentalization requirements available in version 2.0 and later
releases. Therefore, teams were allocated their own repositories. With
the introduction of Rational Quality Manager in version 2.0.1, several
teams also requested Rational Quality Manager repositories, which led to
a further increase in the number of hosted repositories. Starting with
version 3.0.1, Jazz supports multiple applications on the same Jazz Team
Server. Therefore, new requests have resulted in teams being given a
single repository that includes Rational Team Concert, Rational Quality
Manager, and the Requirements Management application (which, since
version 5.0, is Rational Doors Next Generation). The number of users
registered with individual repositories varies from a handful for the
smallest instances to over 2,200 for the largest repositories.

|      |      |      |      |      |      |      |      |      |
|------|------|------|------|------|------|------|------|------|
| 2008 | 2009 | 2010 | 2011 | 2012 | 2013 | 2014 | 2015 | 2016 |
| 27   | 61   | 79   | 98   | 92   | 93   | 88   | 76   | 86   |

***Table 1. Number of of production repositories hosted at the end of
each year (to date in the current year). A further 10 to 15 repositories
are used for test purposes***

|      |      |      |      |      |      |      |      |      |
|------|------|------|------|------|------|------|------|------|
| 2008 | 2009 | 2010 | 2011 | 2012 | 2013 | 2014 | 2015 | 2016 |
| 2    | 6    | 9    | 18   | 24   | 19   | 19   | 17   | 19   |

***Table 1a. Total number of users ('000s) registered to production Jazz
repositories at the end of each year (to date in the current year).
Additional users are registered to the test repositories***

#### LPAR

\* Each logical partition (LPAR) contains between one and 11 Jazz
repositories \* No more than one very large repository, or no more than
two large repositories are hosted on a single LPAR \* IBM Power 6 and
IBM Power 7 hardware \* AIX 6.1 or 7.1 \* Between 128 GB and 256 GB RAM
(256 GB is the benchmark for new LPARs) \* Between 8 and 16 logical CPUs
(16 CPUs is the benchmark for new LPARs) \* Single-tier architecture
with each LPAR hosting the application server, Jazz, and the
accompanying database \* Each repository has an associated IBM DB2
instance, also hosted on the same LPAR. The decision for the database
and application server to co-exist was made at the beginning to reduce
an anticipated performance overhead associated with network
communications between the database and application server. While other
topologies, such as separating the database server from the application
server, were considered, the current model still remains the preferred
option. Although there is overhead with having separate database
instances for each Jazz repository, this setup makes moving repositories
to new LPARs more straightforward. This separation is ideal because
shutting down a Jazz repository and its associated database instance and
moving the repository is completely independent from the usage of any
other repository hosted on the affected LPARs. \* All data (operating
system and application data) is hosted on the storage area network (SAN)

#### Jazz repository

-   Application server: Apache Tomcat
-   Database: DB2 9.7 or DB2 10.1

### Rational Reporting for Development Intelligence (RRDI)

-   RRDI instances are hosted on two separate LPARs
-   Each LPAR contains up to six RRDI instances
-   IBM Power 6 and IBM Power 7 hardware
-   AIX 6.1 or 7.1
-   24 GB RAM
-   4 CPUs
-   Single-tier architecture with each LPAR hosting the application
    server, Jazz, and the accompanying database
-   Each repository has an associated DB2 instance, also hosted on the
    same LPAR
-   All data (operating system and application data) is hosted on the
    storage area network (SAN)
-   RRDI mandates WebSphere Application Server, which is why separate
    LPARs to the ones hosting Jazz repositories were used

### Proxy

The proxy comprises a single load balancer that feeds requests to one of
three proxy servers. These servers direct requests to the respective
Jazz repository. The proxy solution is used by teams running builds from
Jazz build engines hosted in Hursley. Typically, the proxy reduces the
time taken by Rational Team Concert during a source control management (
SCM) fetch operation. The use of proxies is not recommended for
developer use, because, although they derive benefit during SCM
operations such as accepting changes, other operations such as
displaying work items or plans can take up to three times longer because
the proxy won't cache such operations efficiently.

### Jazz build engines

Jazz build engines are hosted on multiple platforms, incorporating
physical and virtual machines, some of which are automatically deployed.

### End users

Software developers and testers who write, update, or build code use
either the Rational Team Concert Eclipse client or an Eclipse client,
such as Rational Developer for System z, that supports the Rational Team
Concert plug-in. Non-coders use the web client to access Jazz.

### Tivoli Storage Manager

Two types of backup are supported: offline, where Jazz is stopped during
the backup, and online, where Jazz remains up during the backup phase,
which does not require a Jazz outage. Key operating system information
and Jazz non-database data (such as work item indexes) are backed up to
Tivoli Storage Manager. The four databases (DW, Jazz Team Server,
Rational Team Concert, and Rational Quality Manager) are backed up to
files that are then also backed up to Tivoli Storage Manager.

The outage associated with offline backups is minimized by restarting
Jazz as soon as the database backup files are created and before the
database files are backed up by Tivoli Storage Manager. Because the
database backup files can account for almost 98 of all files that are
transferred to Tivoli Storage Manager, this sequencing of the backups
can reduce the outage window associated with offline backups by many
hours.

### Tivoli Monitoring

All Jazz LPARs include Tivoli Monitoring agents, which record basic
information such as the following data:

-   Total CPU utilization, which is used to identify trends in total
    usage of the LPAR. This information is useful for capacity planning
    purposes and for identifying any anomalies that might affect Jazz
    performance.
-   CPU utilization for each Jazz Java process
-   Total RAM utilization for the LPAR, which is useful for capacity
    planning
-   RAM utilization for each Jazz Java process
-   Network throughput, which provides the ability to assess and rectify
    slowdowns in key processes, such as Tivoli Storage Manager backups
-   File system status indicators

Other information is also monitored, including DB2 performance. The team
uses this data to assess Jazz performance and identify where maintenance
or improvements are required.

Some Jazz repositories also monitor the response times associated with
sample builds. This information provides a user perspective of Jazz
performance.

### Storage area network (SAN)

All data (operating system, file system, and database) is hosted on the
SAN. Two key factors led to choosing this option. First, when the Jazz
service was first established with the release of Rational Team Concert
1.0 in 2008, there was uncertainty about how much data would be created.
The SAN provides a solution with the ability to increase capacity as
Jazz repositories grow. Today, 17 TB of data are hosted on the SAN. The
second factor was to host the operating system on the SAN in addition to
all the data. This method provided an easier way to transfer LPARs to
new hardware.

|      |      |      |      |      |      |      |      |      |
|------|------|------|------|------|------|------|------|------|
| 2008 | 2009 | 2010 | 2011 | 2012 | 2013 | 2014 | 2015 | 2016 |
| 0.1  | 0.5  | 1.4  | 4.9  | 9    | 15   | 17   | 30   | 34   |

***Table 2. Total production Jazz data (TB) stored on the SAN at the end
of each year (to date in the current year)***

##### Related topics: [Deployment planning and design](DeploymentPlanningAndDesign) [related-topics-deployment-planning-and-design]

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="Diagram1.jpeg" attachment="Diagram1.jpeg"
attr="h" comment="Hursley Jazz Service - High Level Architecture"
date="1408377351" path="Diagram1.jpeg" size="112068" user="johna_5fowen"
version="1"}
