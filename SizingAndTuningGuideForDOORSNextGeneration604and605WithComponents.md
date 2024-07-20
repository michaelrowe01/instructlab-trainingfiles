META:TOPICINFO{author="rnaranjo" date="1574276258" format="1.1"
version="1.27"}
META:TOPICPARENT{name="PerformanceDatasheetsAndSizingGuidelines"}

# Sizing and Tuning Guide for Rational DOORS Next Generation 6.0.4 and 6.0.5 with Components using Global Configuration Management DKGRAY Authors: Main.SkyeBischoff [sizing-and-tuning-guide-for-rational-doors-next-generation-6.0.4-and-6.0.5-with-components-using-global-configuration-management-dkgray-authors-main.skyebischoff]

Build basis: IBM Rational DOORS Next Generation 6.0.4 iFix002 and 6.0.5
ENDCOLOR

TOC{title="Page contents"}

## Introduction

The 6.0.3 release of IBM Rational DOORS Next Generation (DNG) included
the new Component feature. Components are smaller encapsulated
"projects" with their own artifacts, configurations, streams and
baselines. Components serve to encapsulate
modules/artifacts/configurations for end users and reduce user
configuration for administrators. Using components in a DNG deployment
can considerably change the performance profile of a given deployment.
When used properly components will reduce clutter and improve
performance for daily activities.

This article will focus on sizing and tuning of the 6.0.4 and 6.0.5
release of DNG including the new Component feature. We'll talk briefly
about DNG Component performance in 6.0.3, because there have been a few
new configuration changes and performance differences since the 6.0.3
release. But the focus will stay on DNG 6.0.4 and 6.0.5 as these
releases were our target for broad scenario coverage, complex data
generation, and full scalability testing to demonstrate scalability of a
deployment (where scalability refers to the maximum throughput/user load
which can be achieved for a given repository size without significant
response degradation).

### Standard disclaimer

The information in this document is distributed AS IS. The use of this
information or the implementation of any of these techniques is a
customer responsibility and depends on the customer's ability to
evaluate and integrate them into the customer's operational environment.
While each item may have been reviewed by IBM for accuracy in a specific
situation, there is no guarantee the same or similar results will be
obtained elsewhere. Customers attempting to adapt these techniques to
their own environments do so at their own risk. Any pointers in this
publication to external Web sites are provided for convenience only and
do not in any manner serve as an endorsement of these Web sites. Any
performance data contained in this document was determined in a
controlled environment, and therefore, the results may be obtained in
other operating environments may vary significantly. Users of this
document should verify the applicable data for their specific
environment.

Performance is based on measurements and projections using standard IBM
benchmarks in a controlled environment. The actual throughput or
performance any user will experience will vary depending upon many
factors, including considerations such as the number of other
applications running in the customer environment, the I/O configuration,
the storage configuration, and the workload processed. Therefore, no
assurance can be given an individual user will achieve results similar
to those stated here.

This testing was done as a way to compare and characterize the
differences in performance between different configurations of the 6.0.4
and 6.0.5 product. The results shown here should thus be looked at as a
comparison of the contrasting performance between different
configurations, and not as an absolute benchmark of performance.

### Use of Global Configuration Management

As mentioned in the [topology section](#TestTopology) all our component
based testing used the Global Configuration Management application (GC).
Specifically our 500 component data shape used 30 global configurations
each containing 10 DNG components. Our remaining 200 components remained
outside the Global Configuration using only local configurations. The
importance of the GC in our testing played two parts. First we wanted to
test a more complicated change management solution using the GC
application and ensure performance was similar to our results with local
DNG configurations. Second we wanted to test shared queries across DNG
components. Using the GC application allowed us to create folders and
queries where artifacts could be linked across ten different components,
while viewing the query from a single GC configuration. Most of our
previous performance testing articles do not make use of the GC
application, so its important to consider GC usage when reviewing this
article.

### Importance of 6.0.4 iFix002

During development of 6.0.4 there was a critical problem found and fixed
shortly before the products GA. Unfortunately this specific fix caused a
cascade of complex and serious performance degradation in DNG for both
normal operations, CM operations and component usage. Consequently the
performance team worked closely with the development team to test and
eliminate all performance regressions caused by this issue. The
culmination of this work is in 6.0.4 iFix002 (and later iFix). Likewise
6.0.5 contains all of these fixes. If you are using 6.0.4 we highly
recommend you upgrade DNG and your other CLM applications to at least
iFix002 for best performance. All 6.0.4 data discussed in this article
is based off iFix002.

\#HardwareImpact

## How hardware configurations impact scalability

We conducted a series of tests with different hardware configurations,
to assess the impact of memory and disk drives on scalability. The
overall hardware conclusions from using general DNG are still true when
using DNG Components. As a general rule, the system can support more
users, artifacts, and components as the amount of RAM on the DNG server
increases. The number of supported users can also be increased if the
disk I/O speed is increased (e.g. by using SSD drives instead of regular
hard disks). The reason for this concerns the index files used by the
DNG server to provide fast access to artifact data. The DNG server will
cache this index in memory if possible, which is why increasing the
amount of RAM can improve performance. The amount of RAM available to
cache the DNG index is roughly the total amount of RAM minus the maximum
size of the JVM heap. If the disk size of the DNG index (in
server/conf/rm/indices) is less than that number, then the DNG index
will be cached in memory, which will allow for the fastest read access
to DNG data. The DNG index will be accessed from the file system when
there isn't enough memory to cache the index completely (but also on
write operations). This is why disk I/O matters, and why SSD drives
(when combined with enough RAM) provides the best performance and scale.

### Performance Summary Comparing 6.0.4 vs 6.0.5

The table below summarizes the page attempts, overall average response
time of all pages, standard deviation and maximum response time. All of
these results were gathered after the [initial server
caching](#ServerCaching). In general both 6.0.4 and 6.0.5 performed well
with our 300 user test against our 500 component, 1.35 million
repository. As noted in the chart both 6.0.4 and 6.0.5 had average
response times under 1 second making your typical scenario feel
responsive and resulting in a healthy user experience. 6.0.5 did have
improvements which resulted in overall lower average response times,
lower maximum responses times, and ultimately a smaller deviation or
spread between the slowest and fastest responses.

This table compares the average page and page element responses between
6.0.4 and 6.0.5. Here you can clearly see the blue line for 6.0.5 is
consistently lower than 6.0.4 with a smaller spread between average
response times. But again both product versions showed healthy response
times throughout the two hour run. Its also important to note repeated
product runs across both versions showed very similar results with no
more than 5 different between repeat runs.

This table compares the top 10 slowest pages between 6.0.4 and 6.0.5.
Here we can see scenarios with potential to be slow in production
environments and scenarios which have improved between releases. Our
notable slow scenarios are "Search Module for 1.3" and "Open Module".
Our improvements from 6.0.4 to 6.0.5 are Open Module, Show Artifact
Folder with Links, Show Artifacts For component and Show Modules for
Component.

"Open Module " has been a frequent target for improvement in the product
and this testing showed notable improvement moving from 4.6 to 1.9
seconds on average. "Show Artifact Folder with Links" is a new scenario
where a folder is open and viewed with artifacts linked across ten
different components; this shared query showed healthy improvement
moving from 2.2 to 1.1 seconds on average.

Initial project access or "Show Artifacts and Show Modules" has been a
frequent target for query improvements and showed improvement; but it
should be noted a portion of the improvement to these two scenarios and
"Select Configuration" also results from script caching changes due to
some product and scenario design changes.

Last we have our slow scenario "Search Module for 1.3". This scenario is
notably slower than the rest at an average of 14.1 and 13.0 seconds
between releases. This scenario highlights a current problem with having
too many components and artifacts inside of the same project. While many
queries will accept folder or component context, there are still a
handful of product queries which only accept the project scope. "Search
Module for 1.3" is a full text search intended to search the module for
the key text "1.3". Unfortunately full text searches are limited to
project scope in DNG, so users will find these scenarios notably slower
if a project contains too many components or artifacts. For our testing
we intentionally loaded a single project with all 500 components to
exacerbate performance in scenarios similar this, with the goal of
improvement performance as much as possible when limitations like this
were observed. We would like to improve full text search in monolithic
DNG projects with a large number of components, but for now the scenario
can feel a bit sluggish.

### Scalability Comparison of Component Population vs Think Time in 6.0.3

During our 6.0.3 performance testing of DNG components we had the
opportunity to test scalability across a different set of component
population levels and compare different think times. The component data
we populated used approximately the same [data shape](#DataShape) as our
6.0.4 and 6.0.5 testing with all components part of one single large
project. The only exception was the 6.0.3 data shape had only
approximately 1 million artifacts and all components beyond 300 were
populated with templates containing no artifacts. We did this
intentionally so the artifact count would not increase as we scaled
between 300, 500 and 1000 components in a single project.

We tested each component level with user think times of 30, 60 and 120
seconds. Changing the user think time was our preferred method of
adjusting the throughput while testing with the same 300 concurrent
users. Changing the throughput allowed a better understanding of the
scalability at each component level. For CLM performance testing a 30
second think time is considered aggressive for your average scenario. 60
to 90 seconds is considered a normal throughput. And 120 seconds is
considered slower.

Looking at our results at 120 second think times both 500 and 300
component populations performed very well, with average page response
times under one second. 1000 components did not run well and showed 10
second+ response times which users would find to be a poor experience.

Our results at 60 second think times only the 300 component population
performed well, maintaining response times under one second. 500 and
1000 components exceeded 20 and 30 second+ response times resulting in
an experience where the server felt very unresponsive.

Finally our results at 30 second think times none of the population
levels performed well. 300 components was able to run at 10 second+
response times but again users would not find using the server to be a
pleasant experience. 500 and 1000 components exceeded 30 and 40 second+
response times resulting in an experience where the server felt very
unresponsive and quite a bit of the server traffic was returning as
unavailable.

Given these results and our observations we advise the following in
relation to project size and component population:

-   For the best performance a single project shouldn't contain over 300
    components. 300 component populations consistently showed good
    performance across different workloads and think times in our
    testing. It was only during the most aggressive 30 second think
    times a 300 component repository would not perform well.
-   If you have large physical hardware systems and they are very well
    tuned 500 components can perform acceptably in a single project.
    6.0.3 testing showed very good response times at 120 second think
    times, and our 6.0.4 and 6.0.5 testing has shown with product
    improvements 500 components can perform well at 90 second think
    times.
-   If you start approaching a very high component count in a single
    project such as 1000 components, performance is not ideal. Running
    300 users none of our think times including the slower 120 second
    ran well. We ran one additional run not included in the chart using
    1000 components, 200 users and a 120 second think time and this was
    finally able to achieve a 1.2 average response time resulting in
    acceptable performance.

### Deployment Recommendations and Summary

Based off the data we've gathered for DNG and GC with Components we've
learned a number of different things about scalability. Below are some
guidelines to consider when deploying a new DNG server or planning the
growth of current servers. Please keep in mind these guidelines will not
be true for all data. But most servers will benefit from considering
these issues when planning data distribution and design.

-   High component counts in a single project does cause the server to
    slow down overall, and for best performance a single project
    shouldn't contain over 300 components.
-   Component usage allows a single project to perform well with
    approximately 1 million artifacts, but some scenarios will still run
    slow like full text searches. Consequently it is best to separate
    projects out logically and keep your project's overall artifact
    count lower.
-   DNG Components are still limited by Jena's overall index size so an
    entire server should not exceed 2million artifacts. If a server
    could reach these counts then projects should be split to separate
    DNG servers to keep each server's overall artifact count lower.
-   If users are heavily using change management and frequently create
    new streams, they should ensure components are broken into separate
    logical projects. Overuse of components and streams in a single
    project can result in very dense data resulting in performance
    degradation.
-   In any project a single folder/query/module with over 10k artifacts
    can cause user scenario saturation and performance issues. To avoid
    this folders, queries and modules should be split logically to avoid
    over saturation.
-   Make sure your server hardware aligns with your environments size
    and usage. Not having enough memory, CPUs, or physical disks can
    greatly degrade a DNG servers performance.

With these recommendations in mind remember performance is a factor of
both repository design and user scenario usage along with artifact,
project, component and stream counts. The metrics and advice we found in
this article are only a subset of possible DNG performance scenarios.
Larger environments with better encapsulation and distribution may
perform better than what we've outlined here. While smaller environments
with dense data and large queries may run startling slow. Keep in mind
the above examples can have lower/higher thresholds if another competing
factor is changing the system behavior. Always remember an overloaded
portion of any application can degrade performance for the whole system.
This is true for Jazz applications as much as any other application.

\#TestTopology

## Appendix A: Topology

The topology used in our testing is based on the [standard (E1)
Enterprise - Distributed / Linux / DB2
topology](https://jazz.net/wiki/bin/view/Deployment/RecommendedCLMDeploymentTopologies5#CLM_E1_Enterprise_Distributed_Li)

Key:

-   RM Server: Rational DOORS Next Generation Server
-   JTS: Jazz Team Server
-   GC: Global Configuration Server

## Appendix B: Tested hardware and software configurations

All of the hardware tested was 64 bit and supported hyperthreading. The
following table shows the server hardware configurations used for all
the tests and repository sizes.

TABLE{ tableborder="2" cellpadding="2" cellspacing="2" cellborder="2"
headeralign="center" dataalign="center" disableallsort="on"
tablewidth="90" }

| Roll | Server | Number of machines | Machine type | Processor/machine | Total processor cores/machines | Memory/machine | Storage | Network interface | OS and version |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| Proxy Server | IBM HTTP Server and WebSphere Plugin | 1 | IBM System x3550 M4 | 2 x Intel Xeon E5-2640 2.5GHz (six-core) | 24 | 16 GB | RAID 5 279GB SAS Disk x 4 | Gigabit Ethernet | Red Hat Enterprise Linux Server 6.9 (Santiago) |
| RM server | WebSphere Application Server 8.5.5.11 | 1 | IBM System x3550 M4 | 2 x Intel Xeon E5-2640 2.5GHz (six-core) | 24 | 64 GB | RAID 5 279GB SAS Disk x 4 | Gigabit Ethernet | Red Hat Enterprise Linux Server 6.9 (Santiago) |
| Jazz Team Server and Global Configuration Server | WebSphere Application Server 8.5.5.11 | 1 | IBM System x3550 M4 | 2 x Intel Xeon E5-2640 2.5GHz (six-core) | 24 | 32 GB | RAID 5 279GB SAS Disk x 4 | Gigabit Ethernet | Red Hat Enterprise Linux Server 6.9 (Santiago) |
| Database | IBM DB2 enterprise version 11.1.0 | 1 | IBM System x3650 M4 | 2 x Intel Xeon E5-2640 2.5GHz (six-core) | 24 | 64 GB | RAID 10 279GB SAS Disk x 16 | Gigabit Ethernet | Red Hat Enterprise Linux Server 6.9 (Santiago) |

\#DataShape

## Appendix C: Test data shape and volume

The 6.0.4 and 6.0.5 tests used repositories containing 1.35 million
artifacts. All data is contained inside 500 components which are
contained inside a single project. Two types of components were used
"Medium Components with Modules" and "Small Components with Only
Artifacts". Using the two component types allowed us to deploy and test
our target module counts, and then fill in the rest of the server with
smaller components not containing any of the bulkier modules. The
artifacts, modules, comments, links, and other objects were evenly
distributed among each component. The project contained the total data
as shown in the following table.

TABLE{ tableborder="2" cellpadding="2" cellspacing="2" cellborder="2"
headeralign="center" dataalign="center" disableallsort="on"
tablewidth="30" }

| Artifact Type                   | Number       |
|:--------------------------------|:-------------|
| Projects                        | 1            |
| Components                      | 500          |
| Large modules (3,000 artifacts) | 100          |
| Medium modules (500 artifacts)  | 500          |
| Module artifacts                | 550,000      |
| Non-module artifacts            | 800,000      |
| Total Artifacts                 | 1.35 million |
| Links                           | 6.2 million  |
| Folders                         | 29,000       |
| Streams                         | 500          |
| Baselines                       | 500          |
| GC Configurations               | 30           |
| JFS-rdfindex Size               | 102 Gb       |
| JFS-textindex Size              | 28 Gb        |
| Total Jena Index Size           | 130 Gb       |

## Appendix D: Workload characterization

IBM Rational Performance Tester was used to simulate the workload. A
Rational Performance Tester script was created for each use case. The
scripts are organized by pages; each page represents a user action.
Users were distributed into many user groups and each user group
repeatedly runs one script (use case). The RM team used the user load
stages in Rational Performance Tester to capture the performance
metrics.

Before each test the DNG, Jazz and database data was restored to our
baseline for performance testing. Next the server is started and primed
with 300 users caching components and modules. Finally we start our 300
simulated users ramping one user on every 10 seconds resulting in all
users being loaded after 50 minutes. We allow the server to settle for
15 minutes. And last we gather 60 minutes of performance data with 300
users running their use case scenarios against our DNG server. During
that time, tests were run with a 90 second think time between operations
for each user (with a small random distribution to avoid user bunching).

This table shows the use cases and the number of users who were
repeatedly running each script:

TABLE{ tableborder="2" cellpadding="2" cellspacing="2" cellborder="2"
headeralign="center" dataalign="center" disableallsort="on"
tablewidth="60" }

| Use case |  Description |  Of Users |  Number of users |
|:---|:---|:---|:---|
| Link DNG Artifacts | Create a new artifact link to a different component in the current GC configuration | 5 | 15 users |
| View DNG Artifacts with Links | Open folder with artifacts, linked spanning multiple DNG components in the current GC configuration | 15 | 45 users |
| Create DNG Artifact | Create a new artifact | 10 | 30 users |
| Browse DNG Component Switch Menu | Open the configuration switch menu, perform a \* search and browse all DNG components | 5 | 15 users |
| Browse GC Configuration Switch Menu | Open the configuration switch menu and search for a GC configuration | 5 | 15 users |
| Browse GC Configurations and Streams | Open the GC project, open single GC configuration, and browse the GC streams | 5 | 15 users |
| View DNG Components | Open DNG web and view the components for a large project | 5 | 15 users |
| Manage DNG Components and Configurations | Open RM component management window, search for a component and browse to the components streams | 5 | 15 users |
| Scroll DNG Module | Open medium module and scroll through 20 pages of artifacts | 15 | 45 users |
| Search DNG Module View | Open medium module and perform a full text search for specific text | 15 | 45 users |
| Create DNG Module/Artifact Comment | Open medium module, open an artifact and add a new comment | 15 | 45 users |

\#ServerCaching

### Initial Server Caching

Caching plays a large part in DNG in regards to performance when using a
large number of components, modules and configurations. Each
configuration and component has its own subset of data to cache with the
server. This means you'll see increased usage of server memory and CPU
activity as more components are loaded and accessed. After a server has
been restarted performance can slow for the first users of a newly
loaded component. Our tests utilized the worst case scenario with 300
users each accessing a different component. We prime the server for each
new user and component over 3-6 hours. This is important to note because
sever performance can be affected negatively after restart if too many
users are immediately using too many different components. Again our
testing indicates 300 different components could be loaded and used over
a full work day, but there are limits to how many can be immediately
loaded by the server.

Another important consideration for caching is avoiding bloating a
single project with too many components. Our testing distinctly showed
after a server restart component initial access response times increase
as too many components bloat a single project. Testing a project with
100 components showed initial component load times take between 10-20
seconds. Testing a project with 500 components showed initial component
load times between 60-120 seconds. This increase in time is caused by
broad query accesses spanning a single project required to cache and
initialize the component and configuration for its first use since the
server has been restarted. We are tracking potential improvements in
this area, but in 6.0.4 and 6.0.5 for optimal performance it's ideal to
avoid bloating a single project with too many components. Our testing
showed keeping a single project under 100 components is ideal. While the
results here show having 500 components in a single project is possible,
this configuration also highlights long sub-optimal component load times
which may not be ideal in a production environment.

Finally for caching we should shortly discuss the [Jena file access
mode](#JenaAccess ) and its importance to initial server caching. As
noted in the [Jena file access mode](#JenaAccess ) section there are two
options "direct" and "mapped". Mapped has a number of benefits to DNG,
but one distinct benefit to projects with a large number of components.
With the "direct" mode we had to prime the DNG server for approximately
6 hours before our 300 components were ready for our 300 user
performance run. On the other hand the "mapped" mode required 3 hours
before our 300 components were ready for the same user run. So using the
Jena mapped mode results in notably better initial component caching
after a server restart for a project with a large number of components.
Again we want to improve the performance of initial component loading
but using Jena's mapped mode does help.

\#FailureMode

### A note on failure modes

What we see in all cases is the response times slowly increase as the
user load increases up to a point - and at that point, there is a
sudden, sharp increase in response times. At the same time, the CPU
utilization on the DNG server increases to 100. This is the classic
symptom of lock contention in Java. As the load increases, the simulated
users start to ask for exclusive access to the same data, and this
causes a queue to form. The bottleneck forms around access to the DNG
index information. We have observed the user load at which this issue
happens is not consistent, and so there is a margin of error on the user
estimates of +/- 50-100 users.

This failure mode is in part a consequence of the performance simulation
itself, which issues a stream of requests against the server at a steady
rate, without pause. Our simulated users never take breaks for coffee,
or go to meetings, or go to lunch! This represents a worst case
scenario, where the server can never catch up. In production usage, it
would be common for bursts of operations to be followed by slow periods,
during which the server can catch up.

## Appendix E: Application Server Tuning

### Java Virtual Memory Heap Tuning

When allocating your DNG application server's minimum (Xms) and maximum
(Xmx) Java Virtual memory heap you want to allocate the appropriate
amount for your anticipated server load. For medium deployments this
target is often 16Gb, while Large deployments often target a 24Gb heap.
For our very large DNG Component based server we used 27Gb which is the
maximum you can use when enabling "compressed references". We used the
maximum heap because our large repository was able to make good use out
of the maximum memory size. During performance runs garbage collection
would reduce our heap down to roughly 30 to 40 of max and then
progressively our performance run would consume most of the heap before
collection again. Memory contention was always the highest during the
initial caching period of our server, when all of the components,
configurations, and modules were being progressively cached.

For configuring your nursery (Xmn) you want to allocate between 20 to 30
of the total heap (Xmx) to the nursery. The nursery is a section of JVM
memory used to efficiently manage short-lived objects, such as those
associated with handling an incoming HTTP request. As the number of
concurrent DNG users grows, there is more demand on the nursery to
process the incoming transactions. If the nursery is too small, memory
for those objects will be copied into sections of JVM memory which have
more management overhead. By allocating more memory to the nursery, you
can improve performance at higher load levels by ensuring short-lived
objects stay in the nursery. Optimal nursery size can vary by max user
load and amount of different content accessed over time. For our testing
increasing the nursery size beyond \~5Gb did not show any performance
gains (which was 18 of our total heap size).

To set memory add the generic JVM arguments: -Xmx27g -Xms27g -Xmn4915m

### Java Garbage Collection Tuning

DNG testing with components showed the ideal garbage collection policy
to be gencon. CLM testing across the Jazz products has show gencon to
perform efficient garbage collection in most situations. For DNG with
Components gencon is still the proper GC choice.

To enable gencon add the generic JVM arguments: -Xgcpolicy:gencon
-Xgc:preferredHeapBase=0x100000000

### Java Compressed References

DNG testing with components showed enabling compressed references
(Xcompressedrefs) to be ideal. This does cap your maximum application
server heap at 27Gb but a heap this large should be enough for almost
any configuration. Disabling compressed references results in extremely
high java heap consumption requiring you to double your heap size (or
more) for the same performance. So in order to net performance gains
with compressed references disabled you essentially have to have a heap
more than 54Gb. Likewise juggling such a large heap has other operating
system costs, and eats up memory Jena would otherwise use for file
system caching, so its extremely unlikely disabling compressed
references will ever net a performance gain.

To enable compressed references add the generic JVM argument:
-Xcompressedrefs

### Java Argument Summary

Including all of the above memory tuning our JVM and GC policy were
setup as follows:

Initial Heap Size: 27648 Maximum Heap Size: 27648

Generic JVM Arguments: -Xmx27g -Xms27g -Xmn4915m -Xgcpolicy:gencon
-Xcompressedrefs -Xgc:preferredHeapBase=0x100000000
-XX:MaxDirectMemorySize=1G

### Jena Index and File System Cache Memory Consumption

In addition to the application server memory, you have a small overhead
of system memory and file system cache consumption with part of the Jena
index loaded. Jena index consumption of system memory for file system
caching is one of the more complicated aspects to understand in DNG.
Essentially the Jena index is a series of large files on disk and the
operating system will load the most active portions into the file system
cache as part of "inactive" memory. Its very important your deployment
have extra memory available unused by the application server heap and
operating system in order to cache Jena on the side. Having extra memory
for Jena caching can greatly reduce disk activity and memory contention.
Without extra memory Jena will be forced to dynamically load from disk
more frequently and actively load in and out of memory resulting in an
overall system slowdown, reduced user load and reduced throughput. For
our component testing our DNG server had 64Gb of memory: 27Gb for our
application heap, 2Gb for our Linux operating system, and 35Gb for our
Jena index. Note our total index size was 130Gb and would have benefited
some from having more memory (particularly during post restart caching).
128Gb of memory would be ideal for a system with a 100Gb+ index.

The key point is DNG caches Jena in the operating system outside of the
application server heap. Ideally you want your DNG server to have enough
system memory for (Application Server) + (Operating System) + (50-100 of
your Jena Index size) \<= (total system memory). The closer to 100 your
Jena index can load into the system file cache, the less likely your DNG
server will suffer from disk/memory contention.

### Tuning the Configuration Management Cache

Some information about streams and baselines is cached in memory. The
cache size can be changed to improve the performance for higher user
loads (with the tradeoff being additional memory usage). You control the
cache settings through JVM startup parameters (e.g. through the -D flag
or by using custom JVM properties).

The cache stores information which DNG associates with each
configuration (where a configuration is a stream, baseline, or change
set). For best performance, set the cache size to the number of
concurrent users. This supports the worst-case scenario where all active
users are working in separate configurations. The default value for this
cache is 200. Assume each active entry in the cache will consume 2M of
RAM.

To set as a JVM startup parameter:

-Dcom.ibm.rdm.configcache.expiration 60 -Dcom.ibm.rdm.configcache.size
2000

For additional tuning guidance for the configuration cache, refer to
this technote [Tuning the configuration cache for IBM Rational DOORS
Next
Generation](http://www-01.ibm.com/support/docview.wss?uid=swg21995500)

### Tuning the New Pre_Populate Feature in 6.0.4

DNG 6.0.4 includes a new feature which is enabled by default called
"pre_populate". This overrides the previous default updatePolicy in DNG
of "on_demand". Pre_populate loads configurations data into the cache
after the DNG server restarts. By loading configuration data into the
server dynamically after restart, initial access of components, modules,
and other assets can be notably faster (after pre_populate has
finished). With a DNG server using components and Global Configuration
we generally did not see any performance gains when using pre_populate
in comparison to the past setting on_demand. Our observations are likely
biased since our testing only used Global Configurations and no local
configurations. If your users are primarily using DNG based local
configurations I recommend using the new 6.0.4 default "pre_populate".
If your users are primarily using GC based configurations I recommend
using the previous 6.0.3 setting "on_demand".

For best performance, you can set the noOfConfigsToPreload to match the
number configurations in your deployment. This would support the worst
case scenario where all configurations are loaded on your server during
the day. If you set noOfConfigsToPreload higher than the default 100,
you will consume more application server heap memory when your server is
first booted.

To set as a JVM startup parameter:

-Dcom.ibm.team.repository.service.internal.vvc.cache.updatePolicy
on_demand
-Dcom.ibm.team.repository.service.internal.vvc.noOfConfigsToPreload 100
-Dcom.ibm.team.repository.service.internal.vvc.noOfConfigsToCache 2000
-Dcom.ibm.team.repository.service.internal.vvc.ConfigurationIdCache.noOfConfigsToCache
2000

\#JenaAccess

### Jena TDB Default File Access Mode

Jena has two primary file access modes we use "direct" and "mapped".
Full Details on direct vs mapped I/O can be read here:
<https://jazz.net/wiki/bin/view/Deployment/ConfiguringAndTuningDNG> Our
DNG testing with or without components traditionally uses "mapped" as
mapped is almost always superior with lower heap usage, smaller nursery
requirements, and faster Jena access.

On Windows, "direct" mode is the default. We have had issues with using
mapped mode on Windows virtual machines, where the sync() system call
(used to flush dirty pages from memory to disk) becomes slow. We did not
successfully isolate the issue, however. If you are running DNG on
Windows virtual machines, you may consider experimenting with mapped
mode. Mapped mode works functionally on Windows, but you should monitor
performance. The sync() issue would manifest as indexing backlogs or
response time spikes.

To set the Jena File Access Mode access rm/admin and go to advanced
properties: Jena TDB Default File Access Mode - mapped Jena TDB File
Access Mode - mapped

There is also a index.properties file located in several folders under
\server\conf\rm\indices directory. If the existing index.properties file
has an entry for jenaFileMode, it should be set to equal what your
desired filemode should be, for example, jenaFileMode=mapped or
jenaFileMode=direct.

If Jena File Access Mode - Mapped is enabled, you should see a message
like this in the rm.log, during the startup sequence:

2019-10-23 18:16:40,483 \[ Default Executor-thread-93\] INFO
com.ibm.team.jfs - CRJZS5597I JFS Indices use mapped I/O via the
operating system

### Available TCP/IP ports

The default number of TCP/IP ports available on AIX and Linux operating
systems is too low and must be increased. Windows operating systems have
a higher default limit, but the limit might still be too low for large
concurrent user loads. Use the following instructions to increase the
port range.

-   On AIX and Linux systems, set the limit as follows: ulimit -n 65000
-   On Windows 2003 Server, follow these steps:
    -   Open the registry.
    -   Navigate to
        HKEY_LOCAL_MACHINE/SYSTEM/CurrentControlSet/Services/Tcpip/Parameters
        and create a dWord named MaxUserPort. Set its value to 65000.
    -   Restart the computer.
-   On Windows 2008 Server, follow the instructions in this [Microsoft
    support article](http://support.microsoft.com/kb/929851) to change
    the dynamic port range. For the start port setting, use 2000. Set
    the number of ports to 63535.

### Thread pool size

The WebSphere Application Server thread pool size must be increased from
the default of 50 to 75 percent of the expected user load. For example,
if you have 400 concurrent users, the thread pool maximum should be set
to 300.

### More suggestions

In a 3-server topology, where Jazz Team Server and the DNG server are on
separate hardware, adjust two settings in the fronting.properties file
for loads higher than 200 concurrent users.

-   Ensure com.ibm.rdm.fronting.server.connection.route.max equals the
    number of users
-   Ensure com.ibm.rdm.fronting.server.connection.max is twice the value
    of number of users

When you use a proxy or reverse proxy server, you might need to increase
the maximum allowed connections on the proxy server, depending on the
concurrent user load. For more information, see [Tuning IBM HTTP Server
to maximize the number of client connections to WebSphere Application
Server](http://www-01.ibm.com/support/docview.wss?uid=swg21167658) .

## Appendix F: Database Server Tuning

### Keeping Database Statistics Up-To-Date

Information about streams, baselines, and changesets is stored in tables
in the database. The DNG server will query these tables when users work
in a DNG project which is enabled for configuration management. For best
performance, be sure the database statistics are kept up to date as the
size of the repository grows. This is especially critical when you are
first adopting configuration management. Some of the tables will start
out empty, and then grow as users work with streams, baselines, and
change sets. Keeping the database statistics updated ensures the queries
against those tables will be properly optimized.

Databases generally manage statistics automatically; for example, in a
scheduled overnight operation. However, to ensure the database is fully
optimized, you can manually run the statistics as follows. DB2 DB2
REORGCHK UPDATE STATISTICS ON TABLE ALL

Oracle EXEC DBMS_STATS.GATHER_DATABASE_STATS

See also [Slow server performance and CRRRW7556E on IBM Rational DOORS
Next Generation version
6.0.x](http://www-01.ibm.com/support/docview.wss?uid=swg21975746) for
further information on keeping databases tuned for configuration
management, if you are experiencing performance issues.

### Database Server Hardware

For a database server, the team used an IBM System x3650 M4 with 2 x
Intel Xeon E5-2640 2.5 GHz (six-core) and 64G of total RAM. The total
number of processor cores/machines was 24. In the tests, one server was
used for both the Jazz Team Server and RM databases. The database server
was used for the testing was IBM DB2 enterprise version 11.1.0. The same
hardware and database settings were used for all of the performance
tests, irrespective of the repository size.

In our tests, performance bottlenecks always formed first on the DNG
server, due to the interactions around the disk-based indices. The
database server was not the limited factor. However, the 6.0.x release
does use the database server more heavily for storing version
information, so we expect a higher end database server with fast disks)
will improve performance as the number of versions and configurations
increases.

### Hard Disk Capacity and Configuration

The database servers should use the RAID 10 configuration with the RAID
controller configured with "write back cache." The team observed
performance degradation in some use cases when using "write-through"
caching. Use a high capacity and high performing hard disk (10K RPM or
better).

TABLE{ tableborder="2" cellpadding="2" cellspacing="2" cellborder="2"
headeralign="center" dataalign="center" disableallsort="on"
tablewidth="60" }

| Repository | Combined disk usage of Jazz Team Server and RM databases | Hard Disk Size |
|:---|:---|:---|
| Up to 500,000 artifacts | \~100 GB | 300 GB |
| Up to 1 million artifacts | \~150 GB | 400 GB |
| Up to 2 million artifacts | \~300 GB | 700 GB |

## Appendix G: Proxy Server Configuration (for repositories of all sizes)

The team used the same server hardware to test repositories of all
sizes. In general, the proxy server does not slow the performance of the
RM server.

### IHS Tuning

For the IHS systems used during the tests, in the server pool regulation
section (worker.c) of httpd.conf file, these parameters were configured:

TABLE{ tableborder="2" cellpadding="2" cellspacing="2" cellborder="2"
headeralign="center" dataalign="center" disableallsort="on"
tablewidth="30" }

| Parameter           | Value |
|:--------------------|:-----:|
| ThreadLimit         |  25   |
| ServerLimit         |  100  |
| StartServers        |   2   |
| MaxClients          | 2500  |
| SpareThreads        |  25   |
| MaxSpareThreads     |  500  |
| ThreadsPerChild     |  25   |
| MaxRequestsPerChild |   0   |

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]

META:FILEATTACHMENT{name="DNGComponentEnvironment.jpg"
attachment="DNGComponentEnvironment.jpg" attr="" comment="DNG Component
Testing Topolgy" date="1512480792" path="DNGComponentEnvironment.jpg"
size="56709" user="sbischo" version="1"}
META:FILEATTACHMENT{name="604vs605PageSummary.jpg"
attachment="604vs605PageSummary.jpg" attr="" comment="Page Summary"
date="1519282497" path="604vs605PageSummary.jpg" size="50326"
user="sbischo" version="1"}
META:FILEATTACHMENT{name="604vs605ResponseTimeSummary.jpg"
attachment="604vs605ResponseTimeSummary.jpg" attr="" comment="Response
Time Summary" date="1519282518" path="604vs605ResponseTimeSummary.jpg"
size="142471" user="sbischo" version="1"}
META:FILEATTACHMENT{name="604vs605Top10.jpg"
attachment="604vs605Top10.jpg" attr="" comment="Top 10 Summary"
date="1519282536" path="604vs605Top10.jpg" size="95181" user="sbischo"
version="1"}
META:FILEATTACHMENT{name="603ComponentPopulationVsThinkTime.jpg"
attachment="603ComponentPopulationVsThinkTime.jpg" attr=""
comment="Component Population vs Think Time" date="1519367314"
path="603ComponentPopulationVsThinkTime.jpg" size="66073" user="sbischo"
version="1"} META:TOPICMOVED{by="sbischo" date="1519408959"
from="Deployment.SizingAndTuningGuideForRationalDOORSNextGenerationVersion604WithComponents"
to="Deployment.SizingAndTuningGuideForDOORSNextGeneration604and605WithComponents"}
