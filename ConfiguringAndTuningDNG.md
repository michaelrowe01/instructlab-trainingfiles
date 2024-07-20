META:TOPICINFO{author="snehaagarwal0312" date="1701064890" format="1.1"
version="1.42"} META:TOPICPARENT{name="DeploymentAdminstering"}

# Tips for Configuring and tuning DOORS Next Generation DKGRAY Authors: Main.PaulEllis, Main.ErikCraig, Main.BenjaminSilverman, Main.SkyeBischoff Build basis: DOORS Next Generation(DNG) 5.x, DOORS Next Generation 6.x, 7.x. [tips-for-configuring-and-tuning-doors-next-generation-dkgray-authors-main.paulellis-main.erikcraig-main.benjaminsilverman-main.skyebischoff-build-basis-doors-next-generationdng-5.x-doors-next-generation-6.x-7.x.]

ENDCOLOR

TOC{title="Page contents"}

The purpose of this page is to offer additional guidance on specific
performance tuning and configuration settings with DOORS Next Generation
6.x only. DOORS Next moved away from a Jena file system, to a relational
database in 7.x, for the majority of index-related data. This document
is therefore not classed as being relevant to the DOORS Next 7.x
release, although aspects (Java settings) will still be useful. Instead
refer to:

-   [DOORS Next 7.0.2 ifix 8 supplement performance
    report](https://jazz.net/wiki/bin/view/Deployment/PerformanceDoorsNext702iFix8)
-   [DOORS Next 7.x performance
    report](https://jazz.net/wiki/bin/view/Deployment/RequirementsManagement70Performance)

In DOORS Next 7.x we have changed the underlying data store to a
relational database The level of explanation here and the general
applicability is less than the standard performance reports and official
sizing and tuning guides referenced below.

The main guides for 6.x reference are:

-   [Sizing and tuning guide for Rational DOORS Next Generation 6.0.5:
    with Components using Global Configuration
    Management](https://jazz.net/wiki/bin/view/Deployment/SizingAndTuningGuideForDOORSNextGeneration604and605WithComponents)
-   [Performance test results for Rational DOORS Next Generation 6.0.6
    ifix3 with
    Components](https://jazz.net/wiki/bin/view/Deployment/PerformanceResultsForDNG606ifix3)

If you are evaluating the upgrade to DOORS Next 7.x, then wee recommend
DOORS Next 7.x customers refer to:

-   [Understanding DOORS Next sizings in ELM 6.x to estimate timings
    when upgrading to DOORS Next
    7.x](https://jazz.net/wiki/bin/view/Deployment/UnderstandingDOORSNextSizingsin6X)

This document has also been updated to give more context on the
memory-mapped I/O (MMIO) issue experienced by customers using Windows
64-bits servers (May 2021).

## Tuning the Java Virtual Machine

[Wikipedia
quote](https://en.wikipedia.org/wiki/Java_virtual_machine#Generational_heap)
"The Java virtual machine heap is the area of memory used by the JVM for
dynamic memory allocation". IBM advises that the initial heap for DNG is
set to be [one third of the overall
JVM](https://jazz.net/wiki/bin/view/Deployment/SizingAndTuningGuideForRationalDOORSNextGenerationVersion602#JVM_nursery_sizing_1_3_of_max_JV).

If 6.0.6.1 users have selected the option to use the [Guava Cache In
Jena](https://www.ibm.com/support/pages/node/6454531) via the admin UI,
or in teamserver.properties, then this recommendation is then to use 1/4
(one quarter) and not 1/3). This setting is independent of direct vs
memory mapped below.

It should also be noted that the DOORS Next Generation nursery
recommendation of 1/3 Xmx comes from a time when max heaps were lower,
typically, 8G. As heaps grow, the 1/3 value should not be applied. A max
nursery of 8G should be sufficient regardless of max heap sizes. As
always, analyzing verbose gc logs with GCMV is the best way to make JVM
tuning decision.

However, there are several use cases where altering the JVM heap sizes
either temporarily, or due to growing pains is appropriate. The
following advice is listed to address the considerations available to
administrators since DNG 6.0.2.

#### Additional Java Settings

Check that the following JVM parameters have been set:

-Dcom.ibm.team.jfs.rdf.internal.jena.enableExtendedCaching=true.

This option reduces the load on Jena by caching information about
components. The default is false, but we recommend that you enable this.

-Dcom.ibm.team.jfs.rdf.internal.jena.QueryFilterNodeCacheSpec=softValues,maximumSize=10000000,recordStats,concurrencyLevel=10.

This option controls the size of a cache which is used to reduce the
load on Jena. For large systems with millions of artifacts, use a
maximumSize of 10 million - the default is 1 million. If you are using
configuration management, you can use a maximumSize based on the total
number of versions.

-Dcom.ibm.team.repository.service.internal.vvc.activityStopsPrepopulation=false.

The DNG server will pre-populate caches during startup, but by default,
the pre-population is stopped when users log into the system. Set this
parameter to false to allow the pre-population to run to completion.

### Memory Mapped I/O in DNG 6.0.2+

[Jena
Memory-mapped_file](https://en.wikipedia.org/wiki/Memory-mapped_file) is
a new optional memory mode which allows for a different way of managing
the DNG indices. Prior to DNG 6.0.2 direct I/O mode was the default mode
on Linux and Windows. DNG 6.0.2, 6.0.3 and 6.0.4 default to direct mode
for Windows. Since DNG 6.0.5, mapped mode is the default for Windows
servers as well as Linux servers. The two modes differ in how they
access the JVM nursery, resulting in different performance for the
overall system in memory consumption and garbage collection.

Here is a brief comparison between the two modes:

#### Jena behavior using Direct I/O Mode:

-   As a query processes, the indices are copied to the JVM nursery
    causing large chunky disk accesses.
-   These are short-lived and is part of the reason why we recommend the
    1/3rd nursery space for DNG.
-   This then results in more Garbage Collection work.

<!-- -->

-   Direct mode requires a very large Java heap and considerable
    additional OS memory to load the indices in the System File Cache.
-   We do not recommend using direct mode in a production system. This
    will reduce the amount of artifacts/concurrent users that the
    repository can support

#### Jena behavior using Memory Mapped I/O Mode:

-   Jena is able to directly access the address of the blocks on disk
-   In the best case this is cached by filesystem/operating system
-   Reduces memory access outside of the JVM heap
-   We recommend reducing to 1/4 nursery space for DNG.
-   Mapped mode requires a moderate-large Java heap and less additional
    OS memory to load the indices in the System File Cache.
-   Some Windows configurations on Virtual Machines will have slower
    Jena writes due to a virtualized IO issue with memory mapped I/O.

#### Memory Mapped I/O on Windows 64 bits systems

Note 1: In May 2021, IBM issued the technote [IBM Engineering Lifecycle
Query Engine performance is very poor for query and indexing on Windows
servers](https://www.ibm.com/support/pages/node/6450437). This details
the underlying issue that we had been experiencing on Windows 64 bits
systems, which is then even more likely to be encountered when using
Memory Mapped I/O. As stated in the technote, this impacts both
virtualised Windows and bare-metal servers in both direct and mapped
mode.

Note 2 : If you are running with memory-mapped I/O and are experiencing
hangs similar to this please follow the guidance in [IBM Engineering
Lifecycle Query Engine performance is very poor for query and indexing
on Windows servers](https://www.ibm.com/support/pages/node/6450437) and
contact IBM Support.

Since CLM 6.0.5 we have defaulted both Linux and Windows to memory
mapped mode.

There are two settings in the Advanced Properties (rm/admin) that need
to be changed from **direct** or **infer**, to **mapped**. If you do
need to use **direct**, note that the scalability referenced in the
Sizing Guides will not be achievable.

Jena TDB Default File Access Mode Jena TDB File Access Mode

The same properties can be set by adjusting teamserver.properties in
/server/conf/rm to include the following:

com.ibm.team.jfs.jena.tdb.file-mode-default=mapped
com.ibm.team.jfs.jena.tdb.file-mode=mapped

**Note:** If done this way, the server must be restarted or done with
the server offline for the changes to take effect

**NOTE**: There is also a index.properties file located in several
folders under \server\conf\rm\indices directory. If the existing
index.properties file has an entry for jenaFileMode, it should be set to
equal what your desired filemode should be, for example,
jenaFileMode=mapped or jenaFileMode=direct.

If Jena File Access Mode is enabled, you should see a message like this
in the rm.log, during the startup sequence:

2019-10-23 18:16:40,483 \[ Default Executor-thread-93\] INFO
com.ibm.team.jfs - CRJZS5597I JFS Indices use mapped I/O via the
operating system

#### Considerations when using Mapped I/O on Windows

One of the main considerations of using memory mapped I/O is that the
possibility of contention in the 32 bits space within Windows increases,
as detailed in [Native Out of Memory
Exceptions](https://jazz.net/wiki/bin/view/Deployment/AttemptingToUseRTCOnWindowsOperatingSystemLeadsIntoNativeOutOfMemory)
(**Note:** Linux does not have this issue).

It is therefore essential to switch **-Xcompressedrefs** to
**-Xnocompressedrefs**.

We recommend in the [Native Out of Memory
Exceptions](https://jazz.net/wiki/bin/view/Deployment/AttemptingToUseRTCOnWindowsOperatingSystemLeadsIntoNativeOutOfMemory)
article the

"IBM Java team recommends that when you use -Xnocompressedrefs you
should be doubling current Java Virtual Machine(JVM) heap allocation."

This recommendation does **not** apply in this context. The usage of the
nursery heap will actually go down when using memory-mapped I/O, with a
larger demand on native memory. Therefore, it is recommended to use the
existing JVM heap sizes initially and [monitor your way to your optimum
setting](https://jazz.net/wiki/bin/view/Deployment/ProofOfConceptSizingIn6x#Monitor_your_way_to_good_Java_he).

### Lifecycle Query Engine(LQE) and Link Index Provider (LDX)

DOORS Next Generation is not the only implementation with underlying
Jena indices. Lifecycle Query Engine(LQE) and Link Index Provider (LDX)
also use this technology, therefore it is important to understand [IBM
Engineering Lifecycle Query Engine performance is very poor for query
and indexing on Windows
servers](https://www.ibm.com/support/pages/node/6450437).

[Initial indexing is slower than expected when LQE/LDX is running on a
virtualized Microsoft Windows
server](https://www.ibm.com/support/pages/initial-indexing-slower-expected-when-lqeldx-running-virtualized-microsoft-windows-server)
details how to switch to using direct mode for the purposes of running
the reindex. For optimal use during run time, it is still advised to use
mapped mode.

### Large heap sizes, greater than 24GB (Java 6)/57GB Java 7+

Similar to using mapped I/O, as described above, you would need to
switch from compressedrefs to nocompressedrefs when a heap size of more
than 57GB is required. This is due to greater heap space usage that
could be prevented.

## Disk speed's impact on performance

Large imports or deletes of data are predominately write heavy. This is
due to having to index the data that is being imported at the same time
as importing it into the system. You will see large I/O usage when you
import in both the database's area (data files and temp spaces), as well
as the indices directory of DNG. If you are using a browser on the
server for the import, then this is not advisable as the browser will
also add to I/O contention and of course have its own CPU and RAM
consumption.

The discussion on large imports is discussed in further detail within
the [DOORS to DNG Migration
Guide](https://jazz.net/wiki/bin/view/Deployment/DOORSToDNGMigrationSizingGuide).
The impact on even memory mapped I/O, described in the previous
sections, is when the data **is not** actually in memory on some level.
In these instances, slower disk = slower queries (and indexing time).
This is an important point, as we have seen customers who have increased
the RAM and vCPUs available, but overlook their [Achilles'
heel](https://en.wikipedia.org/wiki/Achilles'_heel) of disk speed.

Mapped I/O would be fast, even on say a 5400rpm disk. However, only if
it was all able to be in memory (and all had been accessed at least
once), hence populating the caches. This would particularly impact non
functional testing and evaluations, if you do not run multiple runs of
tests and do not allow the server to fully initialize.

There is a more comprehensive discussion of [RAM, CPU and disk
speed](https://jazz.net/wiki/bin/view/Deployment/ProofOfConceptSizingIn6x#Considerations_for_RAM_CPU_and_d)
within the [Proof of Concept Sizing in CLM
6.x](https://jazz.net/wiki/bin/view/Deployment/ProofOfConceptSizingIn6x).
The advice there is not specific to DNG and is part of a different
discussion. It is worth noting though that there are [additional disk
speed considerations for large imports of data into
DNG](https://jazz.net/wiki/bin/view/Deployment/DOORSToDNGMigrationSizingGuide#Considerations_for_larger_import),
both at the application and database levels.

## Tuning repotools commands for upgrade and reindex

The majority of this article is based around ensuring that a typically
running system is optimally tuned for performance. This typically means
that you need to optimize the read/write speed of your indices and
balance this against your RAM and heap requirements.

When you need to reindex, or upgrade, then there are not the same
concerns of other running programs and you can utilize more of your
available resources. The latest Interactive Upgrade Guide quotes that
you can use 8GB RAM for your Xmx value within the repotools-rm file
(.bat on Windows, .sh on Linux). We recommend that you can expand this
to half RAM for these operations, so as to minimize the duration of the
upgrade or reindex operations.

## What else?

[Upgrade Must Read pertinent
information](https://jazz.net/wiki/bin/view/Deployment/UpgradeMustReadList#Additional_pertinent_information)
is the best place to check out the known issues outside of this
document. At the time of writing, there is particular database advice
for Oracle and SQL Server on top of the general advice of [ Appendix E:
Application Server Tuning
](https://jazz.net/wiki/bin/view/Deployment/PerformanceResultsForDNG606ifix3#Appendix_F_Database_Server_Tunin)
in the 6.0.6 ifix 3 "Performance test results for Rational DOORS Next
Generation 6.0.6 ifix3 with Components".

Here are some known issues:

-   [DNG 6.x: SQL Server errors when optimization
    applied](http://www-01.ibm.com/support/docview.wss?uid=swg21980867)
-   [DNG 6.x: Oracle and SQL upgrade performance
    considerations](http://www-01.ibm.com/support/docview.wss?uid=swg21975746)
-   [After upgrading to 6.0, the Requirements Management server is slow
    or times out](https://jazz.net/library/article/1516#00111)

##### Related topics: [Sizing And Tuning Guide DNG 602](https://jazz.net/wiki/bin/view/Deployment/SizingAndTuningGuideForRationalDOORSNextGenerationVersion602), [Configuring and tuning the Java Virtual Machine (JVM)](ConfiguringAndTuningTheJVM) [related-topics-sizing-and-tuning-guide-dng-602-configuring-and-tuning-the-java-virtual-machine-jvm]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.IanGreen, Main.RosaNaranjo, Main.KnutRadloff, Main.MattHolt [additional-contributors-main.iangreen-main.rosanaranjo-main.knutradloff-main.mattholt]
