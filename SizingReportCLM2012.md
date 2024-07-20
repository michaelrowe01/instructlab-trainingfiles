META:TOPICINFO{author="gcovell" date="1386457741" format="1.1"
version="1.3"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Collaborative Lifecycle Management 2012 Sizing Report (Standard Topology E1) [collaborative-lifecycle-management-2012-sizing-report-standard-topology-e1]

DKGRAY Authors: Main.VaughnRokosz, Main.SkyeBischoff,
Main.DavidChadwick, Main.TimFeeney Last updated: June 13, 2012 Build
basis: CLM 2012, Rational Team Concert 4.0, Rational Quality Manager
4.0, Rational Requirements Composer 4.0 ENDCOLOR

TOC{title="Page contents"}

|  |
|----|
| This article originally appeared at <https://jazz.net/library/article/814> |

The [CLM 2011 Sizing guide](https://jazz.net/library/article/641)
presented the results of our performance testing for the CLM 3.0.1
release. Now that CLM 4.0 is available, its time to update the sizing
guide with the results of our testing against 4.0.

There are a couple of things worth calling out specifically for 4.0.
First, we are focusing our performance testing around standard
topologies; These [standard topologies](StandardTopologiesOverview)
represent frequently chosen deployment patterns. Our performance testing
becomes more relevant when it aligns with the common patterns of
deployment in use by our clients. Secondly, the CLM 4.0 release now
supports high availability through clustering. The impact of clustering
on performance is something which well be investigating in more detail
later this year, so expect to see follow-up articles on that work later.

In this article, well focus on comparing the performance of the 4.0
release to the 3.0.1 release. This involved repeating our 3.0.1 tests
against identical hardware and topologies, with the same data and
workloads. The good news is that 4.0 is as good or better than 3.0.1. We
remain confident that we can support over 2000 active users in an
enterprise environment.

## CLM Test Environment

Our in-house IBM Jazz environment was the workload model used to
generate an Rational Team Concert (RTC) test workload. At the time of
this writing, the CLM 2012 performance test environment generates load
levels of over 2000 active developers operating within 10 active streams
(over 200 or more active users per stream). During the course of a
typical scalability run, users across all roles generate over 3600 work
items per hour (86,000 work items over 24 hours). Builds are simulated
by loading source code from the RTC server at a rate equivalent to 95
builds per hour (over 2300 builds over 24 hours). In addition, quality
professional users run production-like test scenarios for up to 200
active users and analyst users run requirements definition and
management scenarios for up to 100 active users.

With the full CLM solution configured, there are additional scenarios
that check traceability and links between assets in different
repositories and answer key questions assessing test coverage and
requirements impacted by defects. All of these scenarios require reading
data from the data warehouse or multiple live data repositories. These
scenarios are also factored into the CLM performance workload as is the
expectation that dashboards may (and usually will) contain viewlets with
data from different repositories.

## Workload Characterization Summary

The CLM workload is broken down by the various user roles occurring
across the lifecycle of a software development project. The roles
defined -- developers, quality professionals, and analysts -- mirror the
designed role-based licensing and user workflows that implement project
tasks using the CLM platform. Within each role, various representative
user workflows or tasks were broken out as a percentage of overall work
done. Our 4.0 testing used the same workloads as we defined previously
for the 3.0.1 release. More details on the exact breakdown for workloads
can be found later in this document.

There are really two distinct dimensions to the test environment sizing:
number of assets and the number and roles of users actively interacting
with those assets. As your user community grows in size, number of
hosted projects, and length of time using the CLM platform, the
supporting hardware resources need to grow too in order to support your
expanding user community. By testing this extreme workload size on a
very large asset base, we will show you how well the CLM 2012 platform
scales. Note that the user sizing relates to the actual number of active
users, which is a small fraction of the total number of registered
users.

Our 4.0 tests focused on a distributed server setup which is aligned
with our [standard topology
E1](https://jazz.net/wiki/bin/view/Deployment/RecommendedCLMDeploymentTopologies#CLM_E1_Enterprise_Distributed_Li),
with one exception: we have used AIX as the operating system instead of
Linux. The E1 topology represents a whole division or even an enterprise
using the CLM solution as the platform for their software development
shop. While there is no limit or constraint on the number of separate
servers put in place by an enterprise (since there is no longer a server
license fee), the scalability of a single CLM platform, consisting of a
single Jazz Team Server (JTS) and linked Change and Configuration
Management (CCM), Quality Management (QM), and Requirements Management
(RM) applications, can be expanded to handle most software development
shops or project sizes. Our measurements do not in any way reflect a
hard limit to the size of the user community supported by a single JTS
but are merely representative of a fairly large enterprise customer. By
engaging software size modeling specialist in our Techline organization,
larger configurations can be derived that will handle much larger user
communities on a single JTS.

With the 4.0 release, we recommend 64-bit servers only. We no longer
recommend the use of 32-bit servers.

TABLE{ tablewidth="90" cellpadding="4" cellspacing="3" }

|  |  |  |  |  |
|----|----|----|----|----|
| **Distributed server solution** *RRC, RQM, RTC and JTS are on different servers with shared JTS, dual-tier database* | **Deployment** | **RTC Developer** | **RQM Quality Manager** | **RRC Analyst** |
| Large-Scale Enterprise Configuration | CLM | 2000+ active users1 million artifacts60 GB database | 1000 active users 500K artifacts 15 GB database | 200 active users 200K artifacts |
| Mid-Scale Enterprise Configuration | CLM | 700 active users 1 million artifacts 60 GB database | 500 active users 500K artifacts 15 GB database | 100 active users 100K artifacts |

Customers may confidently choose a lower cost single application server
configuration with the option of moving one or more of the CLM
applications to additional servers as the team grows. This implies that
you start with (or add) a front-end web server that forwards different
application roots to different application servers, that is, utilize a
[reverse proxy
server](http://publib.boulder.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.install.doc/topics/c_reverse_proxy.htm).
Alternatively, you could start with a single application server using
four hostname aliases for the various Public URIs for each application
(RM, CCM, QM and JTS), that is, configure virtual hosts for the
applications. With a little planning, you can adjust your hardware
configurations while keeping the Public URIs stable, which is currently
a requirement with the CLM 2012 applications. However, for enterprise
deployments, we recommend that you start with a distributed topology.

## CLM Reference Configurations and Test Results

Our 4.0 testing focused on the [standard enterprise topology
E1](https://jazz.net/wiki/bin/view/Deployment/RecommendedCLMDeploymentTopologies#CLM_E1_Enterprise_Distributed_Li)
with a few minor differences to allow for comparison to our 3.0.1
results. Our 4.0 test environment did not include a proxy, and used AIX
instead of Linux on most server nodes. The table below shows test
results complete with hardware specifications, utilization and response
time numbers. These results can be used as a starting point for
scalability expectations of these products or the entire CLM 2012
solution. If further scalability advice is needed, have your IBM sales
team contact the Techline team to give specific advice based on your
workload and hardware constraints.

TABLE{ tablewidth="90" cellpadding="4" cellspacing="3" }

| Users/Data Volume | Role | Manufacturer | Model | HW Architecture | Number of processors | Processor Speed | Memory (GB) | Total Average CPU Usage | Total Average Memory Usage (GB) | Average Page Response Time (sec) |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| 700 RTC, 500 RQM, 100 RRC - RTC 1Mil, RQM 200k, RRC100k | CLM - RTC Server | IBM | 8203-E4A | Power6 | 4 | 4 Ghz | 16 GB | 40 | 8 | 3.6 sec |
|  | CLM - RQM Server | IBM | 8203-E4A | Power6 | 4 | 4 Ghz | 16 GB | 40 | 8 |  |
|  | CLM - RRC Server | IBM | 8840 | Intel Xeon | 2 | 3.4 Ghz | 8 GB | 20 | 7 |  |
|  | CLM - JTS Server | IBM | 8203-E4A | Power6 | 4 | 4 Ghz | 16 GB | 50 | 8 |  |
|  | CLM - DB Server | IBM | 8840-MC1 | Intel Xeon | 2 | 2.8 Ghz | 8 GB | 50 | 8 |  |

The average response time for 4.0 is slightly better than 3.0.1 (3.6 sec
vs. 3.8 sec for 3.0.1). Over the duration of the test (30 min), 350 MB
of data was uploaded to the server, and 1.6 GB of data was downloaded.

## CLM Hardware Sizing Recommendations

Our standard test topologies (such as the [distributed enterprise E1
topology](RecommendedCLMDeploymentTopologies#CLM_E1_Enterprise_Distributed_Li))
is constructed out of the following kinds of servers:

TABLE{ tablewidth="90" cellpadding="4" cellspacing="3" } \| **Server
building blocks in standard test topologies** \|\|

|  |  |
|----|----|
| Web tier (IBM HTTP Server, Load balancers) | IBM x3250 - Dual CPU Intel Xeon 3060 2.4 GHz or higher 64-bit, 8 GB RAM |
| CLM server | IBM x3550 - Dual 4 core CPUs, 64-bit, 16GB or higher for each server |
| Database server | IBM x3650 - Dual 4 core CPUs, 64-bit, 32GB or higher |
| Disk | High Performance SAS Disk (15K), RAID, SAN or NAS direct connected disk subsystem |

## Tomcat and WebSphere Application Server (WAS) Configurations

While the Jazz Server is pre-configured with Tomcat out of the box,
which is good for evaluation and smaller departmental deployments, we
recommend using WebSphere Application Server (WAS) for large-scale and
enterprise deployments. Tomcat does include simple, file-based user
realm for non-LDAP setups, and provides minimal support for Single
Sign-On (SSO). The SSO experience is limited to one host (i.e. all
applications deployed in the same (virtual) host). There are external
SSO solutions available, but we have not yet confirmed these were
supported by Jazz deployments in Tomcat.

WebSphere Application Server (WAS) does provide flexibility for creating
multiple profiles, has built-in configurable [reverse
proxy](http://publib.boulder.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.install.doc/topics/c_reverse_proxy.html),
and provides full support for Single Sign-On (SSO) whether the
applications are all in one server, or distributed amongst multiple
machines for better scalability; WAS also offers an out of the box
administration user interface for installing; stopping and (re)starting
applications, configuring Java virtual machine properties, security,
etc. Customers have told us that they are taking advantage of the
ability to create instantaneous WAS instances to enable deployment of a
new Jazz server which utilizes their existing security configuration.
WAS also provides more flexible LDAP support and role-to-group mapping
and monitoring with Tivoli ITCAM integration. Additionally, high
availability through clustering is only supported for WAS.

For more information on the benefits of WebSphere, please go to the
following link:
<http://www-01.ibm.com/software/webservers/appserv/was/features/>

## Network Connectivity

There are two aspects to network connectivity: connectivity amongst the
Jazz application and database servers within the CLM environment and
connectivity between the CLM servers and the end users.

The recommendation for network connectivity in dual-tier configurations
of the CLM environment is to minimize latency between the application
server and database server (no more than 1 - 2 ms) and to have the
servers located on the same subnet. When using external storage
solutions, the recommendation is to minimize connectivity latencies,
with the optimal configuration being via Fibre (optical).

As far as network connectivity with the end users of the CLM platform,
there are conditions of slow WAN performance and high volume build or
SCM usage that can be vastly improved by implementing a content caching
proxy server scheme. This configuration is described in the content
caching proxy server article on jazz.net.

## Disks

There are several considerations when choosing disk subsystems including
continuing availability in the event of a disk crash, preventing
repository data loss, and raw throughput and low latency of disk
operations. In our configurations for the CLM 2012 testing, we chose a
RAID 1E (mirrored disk) configuration providing complete data redundancy
and continued operation in the event of a single disk failure. This
configuration is not cost prohibitive for customers without large SAN or
NAS solutions available but still provides reasonable operational
characteristics. For larger configuration, use of a NAS solution with
direct fibre channel connectivity is recommended but not required.
Please review the [IBM NAS
solutions](http://www-03.ibm.com/systems/storage/network/n5000/appliance/)
when making your decision as they provide both NAS and DAS connectivity.

For your database server, be sure to review the recommendations from
your database vendor when considering how to map the CLM database tables
to storage devices. For example, [this developerWorks
article](http://www.ibm.com/developerworks/data/bestpractices/databasestorage/)
describes best practices for DB2 database storage.

## Artifact Sizing Guidelines

Here is a listing of recommendations on artifact sizing that will ensure
optimal performance of the repository when the data sizes increase
significantly.

**Repository**: There are no limits to the number of projects, users, or
iteration structures in the server.

**Projects**: There are no limits to size of projects or number of
contained assets.

**Work Items**: There is no upper limit to the amount of work items in
the repository.

**Plans**: You can have as many plans as needed in the repository and
they can also be deleted.

**Test Assets**: You can have as many test plans, suites, cases,
scripts, execution records, environments, results, and schedules
(automations) as you want in a project.

**Requirements Assets**: You can have as many requirements of any type,
collections, link types, and links among your assets as you want in a
project.

**Reports**: The bulk of the data warehouse size is a function of the
number of work items. The only performance limitation we've seen is
based on the number of streams that are selected as part of the "Stream
Size" reports. This is configurable, and we recommend that you only
configure your integration streams to be collected. By default, no
streams are configured and you can use the "Administer SCM Snapshot"
page when you are logged-in as the administrator in the web user
interface

**Build**: There is no limit on the amount of build results as such, but
there are guidelines on the size of the build results and the pruning
schedule. We suggest that when you get into the enterprise scale and
have 100s of build results a day, ensure that continuous builds are
being pruned (e.g., check the pruning option in the build definition
editor). In addition, instead of uploading gigabytes of build results,
what we do is keep the larger content on the build machines and create
links from the build results to the location to find the build results.
This avoids putting too much transient data into the repository.

**Source Control**: We recommend 100K files and folders in a single
component and if you have more files to split them into multiple
components. We encourage individual users to keep less than 300 change
sets suspended. While there is no limitation, there is a tendency for a
large suspended set to slow down operations involving the suspended set
(suspend, resume, and discard) as well as add some additional cost when
refreshing or changing collaborations. We have tested the user
experience of working with a large number of components in workspaces
and streams. There are no known issues with having hundreds of
components in a stream or workspace, and we have tested the user
experience with 500 components in collaboration.

**Dashboards**: Configuration data in dashboards can hold 32KB. This
affects viewlets such as static HTML, Headlines, and Bookmarks etc. that
can be edited directly by users, and of course any newly written
viewlets using the dashboard mementos to store data for viewlets.

## Workload Details for Scalability Testing

The following tables are the detailed description of the workload used
to test the scalability of the CLM 2012 solution.

### Purpose and Content

This workload creates a realistic dynamic user load. It contains
standalone requirements management, change and configuration management
and quality management as well as combined scenarios involving
integrations and reporting across each of the applications. Users
periodically log off and on, and then randomly choose a new use case.
This creates a dynamic user load, with behaviors similar to live
servers.

At a high level, the workload simulates 479 RQM users, 513 RTC users
using work items, and 123 RRC users. There are an additional 185
simulated RTC users that perform source code and build operations.

A more detailed breakdown of the workload is below.

### Scenario Details

TABLE{ tablewidth="90" cellpadding="4" cellspacing="3" }

| Product | User Role | Percentage total | Scenario Details |
|:---|:---|:---|:---|
| RQM | QE Manager | 4 | Browse Test Plans, Test cases: user browses assets by: View Test Plans, then configure View Builder for name search; clicks next a few times (server size paging feature), then open test plan found, review various sections, then close. Search for test case by name, opens test case found, review various sections, then close. |
|  | Test Lead | 4 | Test Script Review: Search for test script by name, open it, reviews it, then closes. |
|  |  | 2 | Test Case Creation: create test case by: opening the Create Test Case page, enters data for a new test case, and then saves the test case. |
|  |  | 4 | Test Plan Editing: list all test plans; from query result, open a test plan for editing, add a test case to the test plan, a few other sections of the test plan are edited and then the test plan is saved. |
|  | Tester | 12 | Test Execution: user selects "test execution records" by name, then selects TER from for execution, starts execution, enters pass/fail verdict, reviews results, sets points then saves. |
|  |  | 6 | Test Execution Record Browsing: user browses TERs by: name, then selects the TER and opens the most recent results. |
|  |  | 2 | Test Script Editing: user selects Test Script by name. test script then opened for editing, modified and then saved. |
|  | Integrations | 1 | Test Plan Requirements Collection links to new RTC Task: user logs in, creates a test plan, goes to the requirement collection section, and links a new RTC task. |
|  |  | 1 | Test Case links to new RRC Requirement: user logs in, creates a test case, goes to the requirement links section, and links a new RRC requirement. |
|  |  | 1 | Test Case links to RTC Development Item: user logs in, creates a test case, goes to the development links section, and links a new RTC defect. |
|  |  | 1 | Test Script links to new RTC Task: user logs in, creates a test script, adds one step to the test case, and links a new RTC task. |
|  |  | 1 | Test Plan links to RRC Requirements Collection: users logs in, creates a test plan, goes to the requirement collections section, and links a new RRC requirement collection. |
|  |  | 1 | Test Plan links to RTC Development Release Plan: users logs in, creates a test plan, goes to the development plan section, and links a development plan. |
|  |  | 23 | Query Defects: user logs in, views the shared queries, runs a query, and views one defect. |
| RRC | Analyst | 1 | Add Comments: Open requirement with 100 comments and raises a comment to 8 people in the team. |
|  |  | 1 | Create Requirement: Create a requirement with a table, image and RichText. Also edit an artifact with 100 enumerated attributes and modify one of them. |
|  |  | 1 | Create Requirement: Create a requirement with a table, image and RichText. Also edit an artifact with 100 enumerated attributes and modify one of them. |
|  |  | 1 | Filter Query: Execute a query with 100 results and Open 3 levels of nested folder. |
|  |  | 1 | Search String: Search for a string returning 30 matched items. |
|  |  | 1 | Review Approve: user logs in. opens the review panel, adds 20 reviewers and 10 artifacts, saves the review, starts the review, opens the existing review, abstains the first artifact, approves the second artifact, and disproves the remaining. |
|  |  | 1 | Show Tree: Open folder with artifacts with links and perform a on Show tree in the grid. |
|  |  | 1 | View Collections: View collections with 100 artifacts from the collections folders. |
|  | Integrations | 1 | Individual Artifacts linked to RQM Test Case: user logs in, creates an artifact, and links a new RQM test case. |
|  |  | 1 | Individual Artifacts linked to RTC Story: user logs in, creates an artifact, and links a new RTC story. |
|  |  | 1 | Requirements Collection links to RTC Development Release Plan: user logs in, creates a requirement collection, and links an existing RTC dev release plan. |
|  |  | 1 | Requirements Collection links to RQM Quality Plan: user logs in, creates a requirement collection, and links a new RQM quality plan. |

### RTC Build and SCM Details

TABLE{ tablewidth="90" cellpadding="4" cellspacing="3" }

| User Role | Approximate Number of Simulated Users | Workload Details | Role Details |
|:---|:---|:---|:---|
| Developer/SCM | 175 | 4 Daemons as fast as possible; 1 Agent machine | File change sets, accept and deliver change sets, accept changes, refresh pending changes, check history, deliver baseline changes, and other SCM related activities. |
| Build Project Manager | 10 | 10 Virtual users/threads @ 2 builds per hour; 1 Agent machine | Ant build that is run standalone without the Jazz Build Engine. Each build has a separate build definition/engine. Notifies jazz of build start, loads workspace, publishes links, pretends build is compiling, publishes artifacts, pretends build is testing, and notifies jazz of build completion. |

##### Related topics: [related-topics]

-   [Deployment planning](Deployment.DeploymentPlanning)
-   [Deployment planning and
    design](Deployment.DeploymentPlanningAndDesign)

##### External Links: [external-links]

##### Additional contributors: Main.GrantCovell [additional-contributors-main.grantcovell]
