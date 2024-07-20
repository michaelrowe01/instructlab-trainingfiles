META:TOPICINFO{author="tfeeney" date="1707761971" format="1.1"
version="1.26"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Best Practices for Configuring LQE For Performance and Scalability DKGRAY Authors: KeithWells Build basis: Lifecycle Query Engine 6.0.6.x, 7.x through 7.0.2 [best-practices-for-configuring-lqe-for-performance-and-scalability-dkgray-authors-keithwells-build-basis-lifecycle-query-engine-6.0.6.x-7.x-through-7.0.2]

ENDCOLOR

TOC{title="Page contents"}

For 7.0.3 release, the content of this page has been moved to
<https://www.ibm.com/docs/en/elm/7.0.3?topic=performance-configuring-lqe-ldx-improving-scalability>

## **Hardware Recommendations**

-   *It is recommended* LQE be deployed on a dedicated computer with
    adequate CPU, memory and hard drive capacity.
-   *It is recommended*, for best performance, LQE be deployed as a
    stand-alone application on a web server.
-   When deploying LQE on virtual machine images, ensure the physical
    system has sufficient CPU capacity, RAM and disk IO.

### RAM

The LQE application makes use of two kinds of memory: Heap memory and
Native memory. Heap memory is allocated via the JVM properties and is
used by LQE for various heap allocations. Native memory is allocated on
demand by the Operating System and is used by LQE to load the index into
the memory. The amount of RAM needed on a system, for efficient
functioning of LQE, should be calculated based on the heap and native
memory projections.

1\. The JVM heap size for LQE should be 4GB or greater. For dataset
sizes \[sum of the sizes of all of the indices folders on the hard
drive\] greater than 16GB, the heap size should be 25 of dataset size
For example if the estimated size of dataset on the disk is 20 GB, heap
allocation should be 5GB (25 of 20GB).

**Note:** historyTdB and historyText should not be included in the
calculation. Due to the specific of history, you can ignore the size of
it at all for the calculation of the memory needed.

2\. In addition to JVM heap allocation, there should be sufficient free
memory available to load the dataset into memory. For example, if the
estimated indexed dataset is 16 GB on the disk, there should be at least
16 GB of free memory available in addition to 4 GB of JVM heap
allocation. In this case, the total memory reserved for LQE should be
at-least 20 GB.

3\. Examples:

-   Estimated dataset size on disk = 12 GB   Total reserved memory for
    LQE = 4GB heap + 12 GB native = 16GB
-   Estimated dataset size on disk = 20GB   Total reserved memory for
    LQE = 25 of 20GB heap + 20 GB native = 25GB

These memory settings are the same for both reindexing (no matter if
direct io mode is used or not) and normal usage of LQE.

Reserved memory for LQE should be in addition to memory required by the
operating system and other processes.

-   **Estimating the size of the dataset:**

As discussed above, determining the amount of RAM to be allocated for
LQE on a system requires estimating the size of the dataset. The size of
the dataset is dependent on the amount of the data indexed by LQE. For
example if a RTC WorkItems TRS was indexed by LQE, the indexTdb folder
may take anywhere from 1.5GB to 3GB space on the disk depending on the
amount of content in each work item. The textIndex folder may take
between 500 MB and 1GB on the disk. Thus the total size of the dataset
(size of indexTdb + size of shapeTdb + size of versionTdb + size of
textIndex + size of shapeText) could range from 2GB to 4GB on the disk.

-   **Configuring JVM Heap:**
    -   The JVM minimum heap size should be set to 1GB using the -Xms1G
        JVM property
    -   The JVM maximum heap size can be configured by using the -Xmx
        JVM property. For example, if the estimated heap size (as
        determined based on the guidance above) is 4GB, it can be
        configured as: -Xmx4G
    -   *It is recommended* the heap nursery size be set to 1/5 of the
        max heap. For example, the recommended nursery size for -Xmx5G
        would be 1/5 of 5GB or -Xmn1G.
    -   You might need extra heap memory to support high query loads.

### CPU

*It is recommended* LQE be deployed on servers with CPUs which have
clock speeds greater than 2 GHz. CPUs with higher clock speeds increases
indexing performance and speeds up query execution times.

*It is recommended* LQE be deployed on servers with multi-core CPUs to
increase the capacity for concurrent query executions.

### Storage *It is recommended* LQE be deployed on servers with Solid State Drives (SSD) drives. Solid State Drives offer significant improvement for disk read and write operations. This results in improved indexing and query execution performance; in fact, Solid State Drives can increase indexing performance by a factor of 2 times.

### Network

*It is recommended* that LQE be deployed with other data providers on
the same network. Indexing performance is improved with a faster network
because LQE and data providers can respond to requests quicker. Query
performance is improved with a faster network because Access Control
Point (ACP) checks are faster.

## **Operating System Recommendations**

*It is recommended* LQE be deployed on a Linux-based system. Although
LQE works fine on a Windows-based system, Linux-based systems provide
slightly better performance. On Linux systems, the Linux kernel version
should preferably be above the 3.x level.

## **Server Deployment Recommendations**

### **WebSphere Liberty Settings**

Change the lazy Load setting in server.xml file which can be found in
server/liberty/servers/clm folder.

From

`webContainer deferServletLoad="true"`

To

`webContainer deferServletLoad="false"`

### Server Settings

On the server where LQE will be deployed, it is recommended to increase
the maximum number of threads for request processing. This would
increase the number of simultaneous requests which can be handled by the
server (and LQE). On Tomcat, increase the default number of threads from
200 to 250, but keep in mind this applies to LQE and if other web
applications are installed on this server, then consider increasing this
value higher.

On the server where LQE will be deployed, it is recommended to increase
the queue size for the maximum number of incoming requests. Increasing
this value will allow more incoming requests to be queued before they
are rejected by the server. On Tomcat, increase the default number of
requests from 100 to 250, but keep in mind this applies to LQE and if
other web applications are installed on this server, then consider
increasing this value higher.

## LQE Recommendations

### Indexing Performance

Indexing performance depends an several factors: CPU processing
capability, hard drive read/write speeds, and network latency. LQE is a
highly concurrent web application and optimally uses multi-core CPUs for
parallel processing. Since the index is written to a hard drive, the
hard drive should be optimally capable of fast read/write speeds. And
when LQE indexes a data provider, there should be optimum networking
capability for LQE and the data provider to send and receive http
messages.

For best indexing performance, it is recommended

-   LQE be deployed on servers with CPUs which have clock speeds greater
    than 2 GHz. Faster CPUs increases indexing performance.

<!-- -->

-   LQE be deployed on servers with multi-core CPUs to increase the
    capacity for concurrent processing.

<!-- -->

-   LQE be deployed on servers with Solid State Drives (SSD) drives when
    possible to increase indexing performance. (Solid State Drives can
    increase indexing performance by a factor of 2 times).

<!-- -->

-   LQE be deployed with other data providers on the same network
    subsystems for faster indexing performance.

<!-- -->

-   to increase the number of threads for first time and incremental
    indexing to achieve higher throughputs. See this article for more
    information about setting the number of threads for Indexing:
    <https://www.ibm.com/support/knowledgecenter/en/SSYMRC_7.0.2/com.ibm.team.jp.lqe2.doc/topics/t_configuring_trs_providers.html>.

### Query Performance/Scalability

Query performance also depends on many factors: CPU processing
capability, RAM capacity, hard drive read/write speeds, network latency,
indexed dataset size, data complexity, and query optimization.

-   Increased CPU capacity increases query execution performance.
-   Increased RAM capacity improves in-memory computations and prevents
    potential memory constraints
-   Solid State Drives reduce read and write times.
-   Reduced network latency improves ACP check response times.
-   Indexed dataset size makes a huge difference, usually due to the
    increased number of nodes to traverse in queries.
-   All queries should be optimized by reducing the result set earlier
    in the query structure. Query response times should target less than
    100 milliseconds (ms) for optimum scaling in larger datasets. The
    query can be restructured for optimum efficiency by understanding
    the data structures.

For query performance, it is recommended

-   LQE be deployed on servers with CPUs which have clock speeds greater
    than 2 GHz. Faster CPUs increases query execution performance.

<!-- -->

-   to increase RAM capacity to the expected dataset size \* 1.25 to
    improve query performance (see examples above).

<!-- -->

-   LQE be deployed on servers with Solid State Drives (SSD) drives when
    possible to increase read performance for query execution.

<!-- -->

-   LQE be deployed with other data providers on the same network
    subsystems to improve ACP check response times.

<!-- -->

-   to always optimize queries to run faster than 100 ms. Queries can be
    written in many ways and depends on understanding the data
    structure, dataset size, and data complexity to narrow the results
    in an efficient way.

<!-- -->

-   to adjust HTTP Connection and Socket Timeouts in the LQE admin UI
    based upon the response times for your optimized queries. You can
    update these values in the **Advanced Properties** page.

### Recommended Defaults for LQE primary and secondary logs for DB2

Due to the parallel processing that Lifecycle Query Engine component
does with data, the database at a given collection will be very active.
The following examples are just for guidelines. Adjust these settings
accordingly depending on your data load initially and over time.

The database must have the MAXAPPLS increased to allow for concurrent
connections in Lifecycle Query Engine to process data if it is not set
to AUTOMATIC. Increase the value to 300.

db2 update db cfg for LQE using maxappls 300 db2 update db cfg for LQE
using locklist 20000 db2 update db cfg for LQE using LOGFILSIZ 20000 db2
update db cfg for LQE using logprimary 25 db2 update db cfg for LQE
using logsecond100

A request has been submitted to add this information to the Interactive
Upgrade Guide. Refer to WI 410156 for further details.

### Backing up LQE

Backup: The free disk space requirement for the backup folder is (twice
the size of each tdb) + 300k (100k per tdb). The reason for requiring at
least two times the size of the LQE indices for the backup operation is
because the backup process copies the indexes and the LQE
metadata+selections+selects from the Relational Database to the backup
location on the disk. The indices can be compressed to reduce the size

When the compress backup option is selected, then a second size check is
done after the backup folder will be created. That second size check
requires you have enough free disk space equal to the size of the backup
folder. Note that LQE backups are not useful if the backup is older than
the rebase period of QM or RM's TRS feeds, which at most should be 30
days. So there's no need to keep LQE backups that are more than a month
old.

Compaction: It is recommended to schedule your compactions to run prior
to the backups.

The free disk space requirement for the compaction is the total size of
each tdb. This potentially can fail due to the same disk space check.
This size check is done against the location of the index folders, which
in this case is the same partition as the backup location.

If you are seeing the error in the logs:

2019-01-01 00:48:00,907 \[lqe.BackupScheduler0-task-thread-0\] ERROR
bm.team.integration.lqe.lib.backup.impl.BackupTask - CRLQE0475E A fatal
error occurred during backup. Next Steps: I would suggest the following
steps.

1\. Ensure you have sufficient space in the backup area, for twice the
size of the index directory.

2\. If you need to troubleshoot further, edit the
conf/lqe/log4j.properties Change the backup logging to debug level
instead of trace. Add logging for the compaction.

log4j.logger.com.ibm.team.integration.lqe.lib.backup.BackupScheduler=debug
log4j.logger.com.ibm.team.jis.lqe.compaction.CompactionScheduler=debug
log4j.logger.com.ibm.team.jis.lqe.compaction.CompactionTask=debug
log4j.logger.com.ibm.team.jis.lqe.compaction.CompactionUtils=trace

Reload the log4j from the LQE UI.

3\. Run compaction. Capture the lqe.log(s) when it finishes.

4\. Run a backup.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: \* KrzysztofKazmierczyk [additional-contributors-krzysztofkazmierczyk]

META:TOPICMOVED{by="rnaranjo" date="1481744467"
from="Deployment.LifecycleQueryEngineBestPractises"
to="Deployment.LifecycleQueryEngineBestPractices"}
