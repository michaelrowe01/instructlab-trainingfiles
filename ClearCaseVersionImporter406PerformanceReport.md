# ClearCase Version Importer performance report: Rational Team Concert 4.0.6 release

 Authors: [Masa Koinuma](Main.MasabumiKoinuma), [Cunxia
Sun](Main.CunxiaSun) 

Last Updated: March 6, 2014 

Build basis: Rational Team Concert 4.0.6


The ClearCase Version Importer is a new feature of Rational Team Concert
4.0.5. It can migrate all the versions in any branches in Rational
ClearCase in a single operation, and the version branching is also
replicated in Rational Team Concert source control. This document
provides performance data that you can refer to.

The performance result gives you an idea about how long it takes to
import files and folders using the ClearCase Version Importer, although
this example is not a benchmark. Your performance also varies with the
speed of the server host, database type, and the client host that you
use.

The performance report of 4.0.5 release is available at [ClearCase
Version Importer Performance Report in Rational Team Concert
4.0.5](/library/article/1368). This document also provides some
considerations to migrate the data efficiently.

For more information about the ClearCase Version Importer, see
[Migrating data with the ClearCase Version
Importer](https://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.team.connector.scm.cc.doc/topics/c_version_importer_intro.html).

## Topology

In this test environment, all software is installed and configured on a
single host, except for the Rational ClearCase Servers. The ClearCase
Version Importer commands are run on the same host as well. The
following table shows the single server topology variables.

| Metadata Variable | Value |
|:---|:---|
| Operating System | Windows 7 64bit |
| CPU | Intel Core i7-2600 CPU @ 3.4GHz (8-core) |
| Memory | 8GB |
| Network | 100Mbps Ethernet |
| Database Management System | DB2 10.1 |
| Application Server | Tomcat 7 (3GB max heap) |
| License Management System | Trial |
| User Management System | Tomcat |
| Rational ClearCase Client Version | 8.0.1.2 |
| Other technologies | None |

The Rational ClearCase servers are hosted on Solaris Sparc machines. All
the machines are located on the same local network.

## Methodology

The export command of the ClearCase Version Importer runs against the
VOB sub-folders that are listed in the result table, and the duration of
the command is measured.

Then, the intermediate data is imported to a new component of a new
stream on the local CCM server, and the duration of the command is
measured. The user mapping is not configured.

## Results

**Note:** The table shows an average time to import or export the files
per version. The time varies by test case because there are several
other factors that contribute to the duration (such as cleartext pool
cache or the number of files and directories in single Rational Team
Concert component).

### Single view migration

\| **Folder Name** \| **\# of Elements (Folders/Symbolic Links/Files)**
\|\| **\# of File versions** \| **Export Duration (in seconds)** \|\|
**Average Export time per version in seconds** \| **Import Duration (in
seconds)** \|\| **Average Import time per version in seconds** \|

|  |  |  |  |  |  |  |  |  |  |
|----|----|----|----|----|----|----|----|----|----|
| \atria\lib\tbs | 85 | (0/3/82) | 10,709 | 1h00m | (3,616s) | 0.34 | 32m | (1,920s) | 0.18 |
| \applets\ucc | 3,277 | (589/40/2,598) | 120,161 | 10h06m | (36,360s) | 0.30 | 7h38m | (27,480s) | 0.23 |
| \Java\Windows | 16,230 | (2,282/1/13,947) | 27,920 | 11h06m | (39,960s) | 1.43 | 54m | (3,240s) | 0.12 |
| \Java\HPUX | 18,340 | (1,925/89/16,326) | 32,722 | 14h24m | (51,840) | 1.58 | 1h26m | (5,160s) | 0.16 |
| \design | 31,922 | (3,880/341/27,701) | 110,649 | 110h51m | (399,060s) | 3.6 | 14h54m | (53,640s) | 0.48 |

### Multiple view migration

\| **Folder Name** \| **\# of views** \| **\# of Elements
(Folders/Symbolic Links/Files)** \|\| **\# of File versions** \|
**Export Duration** \| **Average Export time per version in seconds** \|
**Import Duration** \| **Average Import time per version in seconds** \|

|               |     |       |                  |         |        |      |        |      |
|---------------|-----|-------|------------------|---------|--------|------|--------|------|
| \nucor\client | 1   | 4,769 | (651/25/4093)    | 158,063 | 22h20m | 0.51 | 11h05m | 0.25 |
| \nucor\client | 3   | 6,126 | (1,953/75/4,098) | 156,525 | 36h07m | 0.83 | 17h51m | 0.41 |

#### For more information [for-more-information]

## References

-   [ClearCase Version Importer Performance Report in Rational Team
    Concert 4.0.5](/library/article/1368)
-   [Migrating data with the ClearCase Version
    Importer](https://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.team.connector.scm.cc.doc/topics/c_version_importer_intro.html)
-   [Rational Team Concert and Rational ClearCase integration
    cookbook](RationalTeamConcertAndRationalClearCaseIntegrationCookbook)

#### About the authors 

[Masa Koinuma](Main.MasabumiKoinuma) is a team lead of Rational
ClearCase, ClearQuest and Jazz Integrations.

[Cunxia Sun](Main.CunxiaSun) is a quality engineer of Rational
ClearCase, ClearQuest and Jazz Integrations.

--------------------

##### Questions and comments:

-   What other performance information would you like to see here?
-   Do you have performance scenarios to share?
-   Do you have scenarios that are not addressed in documentation?
-   Where are you having problems in performance?
