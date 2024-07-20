META:TOPICINFO{author="lekandrade" date="1694626450" format="1.1"
version="1.36"}
META:TOPICPARENT{name="DOORSToDNGMigrationAndIntegration"}

# Rational DOORS 9 to Rational DOORS Next Generation migration sizing guide DKGRAY Authors: Main.PaulEllis, Main.ErikCraig, Main.PaulClunie, Main.BenSilverman [rational-doors-9-to-rational-doors-next-generation-migration-sizing-guide-dkgray-authors-main.paulellis-main.erikcraig-main.paulclunie-main.bensilverman]

Build basis: Rational DOORS 9.6.1.3+, Rational DOORS Next Generation
6.0.1, 6.0.2, 6.0.3 ENDCOLOR

TOC{title="Page contents"}

Updated April 2018: This paper contains many important pieces of
information for older releases. I advise people to start with [ Rational
DOORS Next Generation: Organizing requirements for best
performance](https://jazz.net/wiki/bin/view/Deployment/DNGPerformanceAndData)
for the latest and comprehensive explanation of how we advise all DOORS
Next Generation to setup their data.

The purpose of this page is to collate information from other sections
of the deployment wiki and aggregate those with new guidance for DOORS 9
migration packages and Rational DOORS Next Generation(RDNG) sizing.
There are important new updates since the RDNG 6.0.2 release. This
document was updated on May 4th, 2016 to reflect these.

DOORS 9 does not publish sizing recommendations for module and project
size in the same way as [DOORS Next Generation's sizing
guides](https://jazz.net/wiki/bin/view/Deployment/PerformanceDatasheetsAndSizingGuidelines).
However, it is imperative when evaluating a migration from DOORS 9 to
DOORS Next Generation that your DOORS 9 data is analyzed and modified
accordingly before attempting imports into RDNG.

In order to understand the context of your migration you should avail of
the [Migration Metrics
utility](https://jazz.net/wiki/bin/view/Deployment/CalculatingYourRequirementsMetrics#Using_Migration_Metrics_with_Rat)
built into DOORS 9.6.1.3 and later. Also see the online help topic for
[Migrating data to Rational DOORS Next
Generation](http://www.ibm.com/support/knowledgecenter/SSYQBZ_9.6.1/com.ibm.doors.administering.doc/topics/t_migrate_dng.html?lang=en-us)

Also ensure that you are comfortable with the detailed guidance advice
from the [Migrate data from Rational DOORS to Rational DOORS Next
Generation](http://www.ibm.com/developerworks/rational/library/rational-migrate-doors-data-to-doors-next-generation-trs/index.html)
developerWorks article before proceeding.

Once you have an understanding of your current data shape within DOORS 9
you can more easily map this to how you wish to structure your modules
and projects within RDNG.

You can follow the progress on the latest ifix under development
[here](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.dashboard.viewDashboard&team=Jazz20Collaborative20ALM20Maintenance&tab=_41).

## Sizing recommendations for Rational DOORS Next Generation

The most helpful information when evaluating whether your data will
migrate easily across to RDNG is to compare the output from the
Migration Metrics tool and correlate module and project sizings with our
[published advice on Rational DOORS Next Generation Sizing in
6.x](https://jazz.net/wiki/bin/view/Deployment/SizingAndTuningGuideForRationalDOORSNextGenerationVersion602#Appendix_C_Test_data_shape_and_v).

The key metrics from these guides in relation to migration are below. In
[Rational Requirements Composer Project Sizing
Recommendations](https://jazz.net/wiki/bin/view/Deployment/RationalRequirementsComposerProjectSizing)
we explicitly stated our recommendations, but that document was written
for Rational Requirements Composer 4.x . Since then our recommendations
have been more implicit via the [performance datasheets and
guidelines](https://jazz.net/wiki/bin/view/Deployment/PerformanceDatasheetsAndSizingGuidelines).
The sections below once again try to simplify the detailed information
within the datasheets for rule-of-thumb guidance.

### Recommended folder, module, project and instance sizes

RDNG 6.0.x (Windows)

RDNG 6.0 / 6.0.1

RDNG 6.0.2+ (mapped I/O)

Total Number of Folders / Modules

10,000\*

10,000\*

10,000\*

Artifacts per Project

85,000 - 150,000

85,000 - 150,000

85,000 - 150,000

Artifacts per instance

2 - 2.5 million

2 - 2.5 million

4 - 5 million

\#MemorymappedIO

#### Memory mapped I/O since DNG 6.0.2

There is an important change to the way in which DNG references the data
in the Jena indices since the 6.0.2 release. This change is by default
with Linux, but those that run their DNG system on Windows require
manual steps to enact these changes. [Setting Memory Mapped I/O on
Windows 64 bits
systems](https://jazz.net/wiki/bin/view/Deployment/ConfiguringAndTuningDNG#Memory_Mapped_I_O_in_DNG_6_0_2)
documents how to do this, but also the subsequent sections reflect on
the decisions and considerations that need to accompany turning this on.

**Why turn it on?** As the table shows, the scalability increases when
the indices are read outside of the Java Virtual Machine heap space. The
performance is also improved when heavier workloads are in operation. It
is particularly important if you are experiencing heavy garbage
collection with long pause times, leading to potential garbage
collection storms (almost constant collection) where you can free up the
Java heap.

#### Additional Guidance:

**10,000 (10k) artifacts per module and folder** BRThis helps to improve
readability. As a best practice start with creating a folder structure
in the project and avoid adding too many artifacts directly in the root
folder. There are other artifact types that need consideration, number
of links within project and cross project that could increase as well
(based on the above project, module and folder size limits). It must be
noted that attempts to import beyond 10k will require a different set of
resources to the standard implementation. It will be increasingly
difficult to work effectively with a module above this size, even if the
import is successful. See below for further details on considerations
for larger modules.

**85,000 - 150,000 artifacts per project** BRArtifacts per project
should generally not exceed 85,000 and these include folders, modules,
module artifacts and collections. In case there are a high number of
images, tables which in turn increase size of artifacts, consider a
lower artifact number per project. If the installation is appropriately
sized then these maximum numbers could potentially increase to 100k
-150k. However, as general guidance the 85k project sizing is a better
target for planning where possible.

**2 - 5 million artifacts per instance/repository** BRA comfortable
overall size of a repository depends on many different aspects of both
the data, hardware and number of users concurrently using the system. In
the [Recommended hardware settings](#RecommendedHardwareSettings) below
you can see how you would need to scale your hardware for each load.
Further, more detailed guidance is given in [the performance report for
RDNG
6.x](https://jazz.net/wiki/bin/view/Deployment/PerformanceDatasheetsAndSizingGuidelines).

-   The guidance though for Rational DOORS Next Generation 6.0 and 6.0.1
    on Linux is that you will start to see negative performance once you
    exceed **2 - 2.5 million artifacts**.
-   The guidance though for Rational DOORS Next Generation 6.0.2 and
    6.0.3 on Windows, by default, is that you will start to see negative
    performance once you exceed **2 - 2.5 million artifacts** per
    instance/repository

BRThere are a couple of important changes within RDNG 6.0.2. The
aforementioned [Jena change](#MemorymappedIO) will assist both Windows
and Linux, but more crucially, it was possible to switch the way Jena
indices are managed by the operating system in 6.0.2 which affords the
maximum size of the instance to approximately double from RDNG 6.0.1.

-   The guidance though for Rational DOORS Next Generation 6.0.2 with
    memory mapped I/O is that you will start to see negative performance
    once you exceed **4 - 5 million artifacts**.

### Recommended hardware settings

\#RecommendedHardwareSettings The simplest approach for sizing is to
match your pattern with this diagram which demonstrates hardware
scalability in terms of the number of requirements (y axis) and number
of concurrent users for each specification.

The [Tested
Hardware](https://jazz.net/wiki/bin/view/Deployment/SizingAndTuningGuideForRationalDOORSNextGenerationVersion60#Appendix_B_Tested_hardware_and_s)
section of the [Sizing and Tuning Guide for Rational DOORS Next
Generation version
6.0.2](https://jazz.net/wiki/bin/view/Deployment/SizingAndTuningGuideForRationalDOORSNextGenerationVersion602)
shows the hardware recommended for the data shapes we tested against.

The [System
Requirements](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=675C72E0F28D11E4989B60FF8B09BCE8&osPlatforms=AIX|IBM20i|Linux|Mac20OS|Windows|z/OS&duComponentIds=D003|S002|S004&mandatoryCapIds=30|9|24|35|13|132|42|19|16|26|40&optionalCapIds=133|66|135|7|5|12|19|137|27|4&cm_mc_uid=55870443158614815313554&cm_mc_sid_50200000=1488193444)
no longer quote a minimum specifications for CPU and RAM, preferring to
use the workload definitions within the Sizing guides. Smaller systems
should extrapolate down according to the above graphic. 1 user & a large
import of data from DOORS 9 is still going to need ample hardware for
the size of data and not sized for 1 user. If DNG is one of the elements
of your CLM solution, then please also consider [our Proof Of Concept
sizing for CLM
6.x](https://jazz.net/wiki/bin/view/Deployment/ProofOfConceptSizingIn6x).

Please note that this information is specific to 6.0.3 and that changes
to the maximum number or artifacts in the database, with all other
variables are subject to change in future releases.

## Sizing limitations for the size of the migration package created in DOORS 9

In Rational DOORS Next Generation(RDNG) 6.0.1, there are recommended
limits on the size of the migration package which are dependent on the
machine resources of the importing RDNG server.

As for numbers of DOORS objects in a single migration package, we have
some benchmark figures for a realistic set of modules of varying sizes
and object hierarchies. This provides a good guide to the maximum amount
of data that can be handled in a single migration import.

The machine specification in use for the export of the DOORS 9 and
import into RDNG 6.0.1. Based on the figures within the section
[Recommended hardware settings](#RecommendedHardwareSettings) above, :

-   Windows Server 2012
-   32GB RAM
-   2 x vCPU
-   Java heap values set at: Xmx 16G, Xms 16G, Xmn 4G

The following example was generated using DOORS v9.6.1.4 and RDNG
v6.0.1:

**NEW: The table below has been expanded to include figures from
importing the same package using RDNG v6.0.2 and v6.0.4. Note the size
of the indices is reduced and the time to import is significantly
improved. The 6.0.1 numbers have been kept for comparison and evaluation
of whether upgrading to the latest release would benefit your size of
implementation. It is important to note thate the figures were not
produced using consistent setups as there were changes in the underlying
infrastructure between versions.**

Total number of objects / Modules

Number of Links

Number of OLEs and Size(MB)

Size of package / uncompressed

Duration of DOORS 9 Export

Duration of DNG Import 6.0.1

Duration of DNG Import 6.0.2

Duration of DNG Import 6.0.4

RDNG Indices Size **6.0.1**

RDNG Indices Size 6.0.2

RDNG Indices Size 6.0.4

11114 / 21

8000

800 / 11MB

14.2MB / 136MB

4 mins, 6 secs

67 mins

52 mins

32 mins

733 MB

\<733 MB

805MB

26676 / 43

2000

1920 / 26.4MB

35MB / 397MB

11 mins, 40 secs

3 hours, 16 mins

2 hours, 21 mins

1 hour, 11 mins

2.16GB

1.67GB

2.54GB

60018 / 106

50,000

4320 / 59.5MB

78.3MB / 809MB

30 mins, 31 secs

10 hours, 4 mins

5 hours, 32 mins

3 hours, 54 mins

4.22GB

3.95GB

6.6GB

120,036 / 212

100,000

8640 / 118.9MB

156MB / 1.58GB

1 hour, 22 mins

25 hours, 9 mins

12 hours, 27 mins

9 hours, 13 mins

8.01GB

7.8GB

15.0GB

 

The table shows that as the size of the imports grow, the hardware
specification becomes increasingly inadequate. The final time of 25
hours in RDNG 6.0.1 would be greatly improved with additional resources.
There are considerable improvements with 6.0.2, but even the 15 hour
figure could be drastically improved with more resources.

Notes: \* Using the specification above, files above approximately 2Gb
uncompressed typically fail to upload into RDNG. \* Larger ReqIF/migiz
packages will require larger Java heap sizes and therefore memory. \*
There will be significant disk activity during an import for the
application server and the database server \* In DNG 6.0.3 there is a
new server parameter:

-   Server Administration -\> Advanced Properties -\> RM Client
    Component -\> com.ibm.rdm.web.config.WebConfig
-   Maximum size for ReqIF and Migration files (MB) 150
-   Maximum size for uploaded files (MB) 50

## Considerations before exporting DOORS data to RDNG

This section is no longer required as of RDNG 6.0.4, where the migration
import is significantly improved. The main guidance for approaching this
migration is comprehensively discussed within [Migrate data from
Rational DOORS to Rational DOORS Next
Generation](http://www.ibm.com/developerworks/rational/library/rational-migrate-doors-data-to-doors-next-generation-trs/index.html?cm_mc_uid=36410414050514450077320&cm_mc_sid_50200000=1460365063)
developerWorks article.

If after assessing which data sets need to be exported you are facing
sizes in excess of those discussed in this article then you should
strongly consider performing the data manipulation prior to exporting
from DOORS and well before attempting an import. [Considerations for
larger imports](#ConsiderationForLargerImports) above explains the
additional resources required to accept a large package, so postponing
the manipulation to post-export is nonsensical.

The following procedure is how you would potentially split DOORS 9.x
modules into smaller components, prior to migration. The example below
is for a 50k object module within DOORS 9.

1 Run the DXL from technote [How to keep links when restoring a DOORS
module archive](http://www.ibm.com/support/docview.wss?uid=swg21625169)
to get all the links in to attributes in the main module 2 Move
artifacts to several/new target modules (Tools -\> Functions -\> Copy
Object), perhaps 5 modules would be ideal so that each module has 10k
artifacts. 3 Use "Link by Attribute" to re-establish the incoming and
outgoing links to/from each module

This information is provided as an example method for reconfiguring data
without losing links, which would usually make this action prohibitive.
Please contact DOORS Support for further assistance with implementing
the technote, although also please note the Disclaimer.

## Considerations for larger imports.

\#ConsiderationForLargerImports

What is considered a large import can be subjective, but in terms of
this article it is any migration which attempts over 10k artifacts in a
single migration or ReqIF package. The recommended limit of 10k
artifacts per module are still respected, but as with the examples
above, there are multiple modules destined for a project of
approximately 100k artifacts.

-    Increase the log file of the database server. Empirically, our
    expertise resides with DB2, therefore the following settings are
    recommended for change in order to unblock the bottleneck of the
    database server.

db2 connect to RM6 db2 update db cfg for RM6 using LOGPRIMARY 120 db2
update db cfg for RM6 using LOGFILSIZ 16384

-    Ensure the hard disks in use are optimal. Solid State Disks(SSD)
    are recommended for the RM indices location and the database
    server's log file area. Standard 10k rpm as disk speed is generally
    insufficient for the read/write access required on very heavily used
    directories. Use hdparm tT to track disk speed. The Timing cached
    reads per second are crucial.

<!-- -->

-    More memory. As the packages grow larger, as will the amount of RAM
    required.
-    Java Heap space available. Consider increasing your Xmx, Xms and
    Xmn relative to your package size. You should actively monitor your
    Java garbage collection and allocate more resources accordingly.
-    CPU. The machine used for the above numbers is significantly below
    that recommended for larger data sets, as extrapolated from relative
    size prescribed within the [published advice on Rational DOORS Next
    Generation Sizing in
    6.x](https://jazz.net/wiki/bin/view/Deployment/SizingAndTuningGuideForRationalDOORSNextGenerationVersion602#Appendix_C_Test_data_shape_and_v).
-    Run regular updates on the database statistics after each large
    migration. See, [Keeping database statistics
    up-to-date](https://jazz.net/wiki/bin/view/Deployment/SizingAndTuningGuideForRationalDOORSNextGenerationVersion602#Keeping_database_statistics_up_t),
    for instructions for your database server.
-    Finally, note that long running sessions can fall foul of web
    server timeouts. Please note [Tuning Jazz systems to support
    performance
    testing](https://jazz.net/wiki/bin/view/Deployment/TuningForPerformanceTesting#Tuning_systems_for_long_runs)
    for guidance if a single operation import exceeds 6 hours.
-    The final point to note is that large migrations will benefit, as
    will upgrades, from collocation of the database and the application
    server. This is not recommended as a standard topology so would be
    typically a solution for migrations. If the level of data transfer
    merits collocation for Business As Usual, then

## Considerations for concurrent import of ReqIF/migiz

The ReqIF import is limited to the \# of threads specified in /rm/admin
-\> Advanced Properties -\> ReqIF.importThreadPoolSize. The default is
1, meaning you can do one import at a time. I'd advise against importing
multiple in to the same project area at the same time. Larger imports
can be resource intensive, consuming a good amount of memory in the JVM
and periods of high CPU usage during indexing. This is something to keep
an eye on if you're going to do more than 1 import at the same time.
Otherwise, smaller imports should be safer to try concurrently, but keep
an eye on resource utilization. You may need to temporarily increase
your JVM heap size or add more CPU's while doing multiple imports.

##### Related topics: [Calculating your requirements metrics](https://jazz.net/wiki/bin/view/Deployment/CalculatingYourRequirementsMetrics), [Collaborative Lifecycle Management performance report: RDNG 6.0](https://jazz.net/wiki/bin/view/Deployment/CollaborativeLifecycleManagementPerformanceReportRDNG60Release), [Sizing and tuning guide for Rational DOORS Next Generation 6.0](https://jazz.net/wiki/bin/view/Deployment/SizingAndTuningGuideForRationalDOORSNextGenerationVersion60) [related-topics-calculating-your-requirements-metrics-collaborative-lifecycle-management-performance-report-rdng-6.0-sizing-and-tuning-guide-for-rational-doors-next-generation-6.0]

##### External links: [Migrate data from Rational DOORS to Rational DOORS Next Generation](http://www.ibm.com/developerworks/rational/library/rational-migrate-doors-data-to-doors-next-generation-trs/index.html) [external-links-migrate-data-from-rational-doors-to-rational-doors-next-generation]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.KouroshManeshni, Main.TimHards, Main.VaughnRokosz, Main.KnutRadloff, Main.PaulYoung [additional-contributors-main.kouroshmaneshni-main.timhards-main.vaughnrokosz-main.knutradloff-main.paulyoung]

META:FILEATTACHMENT{name="Screen_Shot_2017-03-14_at_09.55.42.png"
attachment="Screen_Shot_2017-03-14_at_09.55.42.png" attr=""
comment="latest scaling graph" date="1489485410"
path="Screen_Shot_2017-03-14_at_09.55.42.png" size="73517"
user="paulellis" version="1"}
