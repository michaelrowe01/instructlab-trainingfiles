META:TOPICINFO{author="gcovell" date="1401323717" format="1.1"
version="1.20"}
META:TOPICPARENT{name="PerformanceDatasheetsAndSizingGuidelines"}

# Collaborative Lifecycle Management performance report: RRC 4.0.4 release [collaborative-lifecycle-management-performance-report-rrc-4.0.4-release]

DKGRAY Authors: Main.GustafSvensson Last updated: Aug. 29, 2013 Build
basis: Rational Requirements Composer 4.0.4 ENDCOLOR

TOC{title="Page contents"}

## Introduction

This report compares the performance of an unclustered Rational
Requirements Composer version 4.0.4 deployment to the previous 4.0.3
release. The test objective is achieved in three steps:

-   Run version 4.0.3 with standard 1-hour test using 400 concurrent
    users.
-   Run version 4.0.4 with standard 1-hour test using 400 concurrent
    users.
-   The test is run three time for each version and the resulting six
    tests are compared with each other. Three tests per version is used
    to get a more accurate picture since there are variations expected
    between runs.

### Disclaimer [disclaimer]

INCLUDE{"PerformanceDatasheetDisclaimerSomeBrowserSimulation"}

## Findings

### Performance goals

-   Verify that there are no performance regressions between current
    release and prior release with 400 concurrent users using the
    workload described below.

### Findings

-   RPT report shows similar response times for 4.0.4 and 4.0.3.
    -   In 4.0.4 many actions are slightly faster than in 4.0.3.
-   Comparing nmon data for both 4.0.4 and 4.0.3 show similar CPU,
    memory and disk utilization on application servers and database
    server.

## Topology

The topology under test is based on [Standard Topology (E1) Enterprise -
Distributed / Linux /
DB2.](https://jazz.net/library/article/820#Enterprise_Distributed_Linux__DB2)

The specifications of machines under test are listed in the table below.
Server tuning details listed in [**Appendix A**](#AppendixA)

Function Number of Machines Machine Type CPU / Machine Total \# of CPU
Cores/Machine Memory/Machine Disk Disk capacity Network interface OS and
Version

IBM HTTP Server and WebSphere Plugin 1 IBM System x3250 M4 1 x Intel
Xeon E3-1240 3.4GHz (quad-core) 8 16GB RAID 1 -- SAS Disk x 2 279GB
Gigabit Ethernet Red Hat Enterprise Linux Server release 6.3 (Santiago)

JTS Server 1 IBM System x3550 M4 2 x Intel Xeon E5-2640 2.5GHz
(six-core) 24 32GB RAID 5 -- SAS Disk x 4 279GB Gigabit Ethernet Red Hat
Enterprise Linux Server release 6.3 (Santiago)

RRC Server 1 IBM System x3550 M4 2 x Intel Xeon E5-2640 2.5GHz
(six-core) 24 32GB RAID 5 -- SAS Disk x 4 279GB Gigabit Ethernet Red Hat
Enterprise Linux Server release 6.3 (Santiago)

Database Server 1 IBM System x3650 M4 2 x Intel Xeon E5-2640 2.5GHz
(six-core) 24 64GB RAID 10 -- SAS Disk x 16 279GB Gigabit Ethernet Red
Hat Enterprise Linux Server release 6.3 (Santiago)

RPT Workbench 1 VM image 2 x Intel Xeon X7550 CPU (1-Core 2.0GHz 64-bit)
2 6GB SCSI 80GB Gigabit Ethernet Microsoft Windows Server 2003 R2
Standard Edition SP2

RPT Agent 1 xSeries 345 4 x Intel Xeon X3480 CPU (1-Core 3.20GHz 32-bit)
4 3GB SCSI 70GB Gigabit Ethernet Microsoft Windows Server 2003
Enterprise Edition SP2

RPT Agent 1 xSeries 345 4 x Intel Xeon X3480 CPU (1-Core 3.20GHz 32-bit)
4 3GB RAID 1 - SCSI Disk x 2 70GB Gigabit Ethernet Microsoft Windows
Server 2003 Enterprise Edition SP2

RPT Agent 1 Lenovo 9196A49 1 x Intel Xeon E6750 CPU (2-Core 2.66GHz
32-bit) 2 2GB SATA 230GB Gigabit Ethernet Microsoft Windows Server 2003
Enterprise Edition SP2

Network switches N/A Cisco 2960G-24TC-L N/A N/A N/A N/A N/A Gigabit
Ethernet 24 Ethernet 10/100/1000 ports

N/A: Not applicable.

### Network connectivity

All server machines and test clients are located on the same subnet. The
LAN has 1000 Mbps of maximum bandwidth and less than 0.3ms latency in
ping.

### Data volume and shape

The artifacts were distributed between 40 small projects, 10 medium
projects and one large project for a total of 200,589 artifacts.

The repository contained the following data:

-   141 modules
-   14,500 module artifacts
-   3,203 folders
-   434 collections
-   274 reviews
-   40,798 comments
-   520 public tags
-   110 private tags
-   15,350 terms
-   22,778 links
-   360 views

<!-- -->

-   Database size = 20 GB
-   JTS index size = 9 GB

The large project contained the following data:

-   11 modules
-   1,160 folders
-   78,842 requirement artifacts
-   106 collections
-   64 reviews
-   16,897 comments
-   300 public tags
-   50 private tags
-   9,006 terms
-   15,594 links
-   200 views

## Methodology

Rational Performance Tester was used to simulate the workload created
using the web client. Each user completed a random use case from a set
of available use cases. A Rational Performance Tester script is created
for each use case. The scripts are organized by pages and each page
represents a user action.

Based on real customer use, the test scenario provides a ratio of 70
reads and 30 writes. The users completed use cases at a rate of 30 pages
per hour per user. Each performance test runs for 60 minutes after all
of the users are activated in the system.

### Test cases and workload characterization

\#TestCases

Use case Description of Total Workload

Login Connect to the server using server credentials. None

[Create a collection](#CreateCollection) Create collections with 10
artifacts. 6

[Filter a query](#FilterQuery) Run a query that has100 results and open
3 levels of nested folders. 8

[Open nested folders](#OpenNested) Create review and complete review
process. 4

[Manage folders](#ManageFolders) Create a folder, move it to a new
location, and then delete the folder. 1

[Query by ID](#QueryBy) Search for a specific ID in the repository. 8

[View collections](#ViewCollections) View collections that contain 100
artifacts from the collections folders. 13

[Check suspect links](#CheckSuspect) Open an artifact that has suspect
links. 6

[Add comments to an artifact](#AddComments) Open a requirement that has
100 comments and creates a comment addressed to 8 people on the team. 8

[Open the project dashboard](#OpenProject) Open the project and
dashboard for the first time. 7

[Create a multi-value artifact](#CreateMulti) Create a multi-value
artifact and then add a multi-value attribute. 2

[Create an artifact](#CreateArtifact) Create a requirement that contains
a table, an image and rich text. Edit an artifact that has 100
enumerated attributes and modify an attribute. 2

[Show artifacts in a Tree view](#ShowArtifacts) Open a folder that
contains artifacts with links and show the data in a tree view. 8

[Open graphical artifacts](#OpenGraphical) Open business process
diagrams, use cases, parts, images, sketches and story boards. 5

[Create and edit a storyboard](#CreateEdit) Create and edit a
storyboard. 4

[Display the hover information for a collection](#DisplayHover) Open a
collection that contains 100 artifacts and hover over the Artifacts
page. 4

[Query by String](#QueryString) Search for a string that returns 30
matched items. 10

[Create a PDF report](#CreateReport) Generate a 50-artifact PDF report.
2

[Create a Microsoft Word report](#CreateWord) Generate a 100-artifact
Microsoft Word report. 2

#### Response time comparison

The median response time provided more even results than the average
response time. The nature of the high variance between tests where some
tasks at time takes a longer time to run, such as when the server is
under heavy load, makes the average response time less predictive. Both
the median and average values are included in the following tables and
charts for comparison.

In the repository that contained 200,000 artifacts with 400 concurrent
users, no obvious regression was shown when comparing response times
between runs.

The numbers in the following charts include all of the pages for all of
the scripts that ran.

## Results

**Garbage collection**

Verbose garbage collection is enable to create the GC logs. The GC logs
shows very little variation between runs. There is also no discernible
difference between versions . Below is one example of the output from
the GC log for each application.

**RM**

**JTS**

\#CreateCollection Create a collection

[Back to Test Cases & workload characterization](#TestCases)

\#FilterQuery Filter a query

[Back to Test Cases & workload characterization](#TestCases)

\#OpenNested Open nested folders

[Back to Test Cases & workload characterization](#TestCases)

\#ManageFolders Manage folders

[Back to Test Cases & workload characterization](#TestCases)

\#QueryBy Query by ID

[Back to Test Cases & workload characterization](#TestCases)

\#ViewCollections View collections

[Back to Test Cases & workload characterization](#TestCases)

\#CheckSuspect Check suspect links

[Back to Test Cases & workload characterization](#TestCases)

\#AddComments Add comments to an artifact

[Back to Test Cases & workload characterization](#TestCases)

\#OpenProject Open the project dashboard

[Back to Test Cases & workload characterization](#TestCases)

\#CreateMulti Create a multi-value artifact

[Back to Test Cases & workload characterization](#TestCases)

\#CreateArtifact Create an artifact

[Back to Test Cases & workload characterization](#TestCases)

\#ShowArtifacts Show artifacts in a Tree view

[Back to Test Cases & workload characterization](#TestCases)

\#OpenGraphical Open graphical artifacts

[Back to Test Cases & workload characterization](#TestCases)

\#CreateEdit Create and edit a storyboard

[Back to Test Cases & workload characterization](#TestCases)

\#DisplayHover Display the hover information for a collection

[Back to Test Cases & workload characterization](#TestCases)

\#QueryString Query by string

[Back to Test Cases & workload characterization](#TestCases)

\#CreateReport Create a PDF report

[Back to Test Cases & workload characterization](#TestCases)

\#CreateWord Create a Microsoft Word report

[Back to Test Cases & workload characterization](#TestCases)

## Appendix A

\#AppendixA

Product Version Highlights for configurations under test

IBM HTTP Server for WebSphere Application Server 8.5.0.1 IBM HTTP Server
functions as a reverse proxy server implemented via Web server plug-in
for WebSphere Application Server. Configuration details can be found
from the [CLM
infocenter](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Ft_config_reverse_proxy_ihs.html).

**HTTP server (httpd.conf)**:

-   MaxClients: increase value for high-volume loads [(adjust value
    based on user
    load)](http://publib.boulder.ibm.com/httpserv/ihsdiag/ihs_performance.html)
-   ThreadsPerChild = 50

**Web server plugin-in (plugin-cfg.xml)**:

-   ServerIOTimeout="900"

**OS Configuration**:

\* max user processes = unlimited

IBM WebSphere Application Server Network Deployment 8.5.0.1 JVM
settings:

-   GC policy and arguments, max and init heap sizes:

-XX:MaxDirectMemorySize=1g -Xgcpolicy:gencon -Xmx4g -Xms4g -Xmn512m
-Xcompressedrefs -Xgc:preferredHeapBase=0x100000000

**Thread pools:**

-   Maximum WebContainer = Minimum WebContainer = 500

**OS Configuration:**

System wide resources for the app server process owner:

-   max user processes = unlimited
-   open files = 65536

DB2 DB2 10.1

LDAP server

License server

Hosted locally by JTS server

RPT workbench 8.2.1.5 Defaults

RPT agents 8.2.1.5 Defaults

Network

Shared subnet within test lab

#### For more information [for-more-information]

-   [Collaborative Lifecycle Management 2012 Sizing Report (Standard
    Topology E1)](SizingReportCLM2012)

#### About the authors [about-the-authors]

Main.GustafSvensson

--------------------

##### Questions and comments: [questions-and-comments]

-   What other performance information would you like to see here?
-   Do you have performance scenarios to share?
-   Do you have scenarios that are not addressed in documentation?
-   Where are you having problems in performance?

COMMENT{type="below" target="PerformanceDatasheetReaderComments"
button="Submit"}

INCLUDE{"PerformanceDatasheetReaderComments"}

META:FILEATTACHMENT{name="image014.png" attachment="image014.png"
attr="h" comment="" date="1378494644" path="image014.png" size="87648"
user="gsven" version="2"} META:FILEATTACHMENT{name="image015.png"
attachment="image015.png" attr="h" comment="" date="1378494667"
path="image015.png" size="42456" user="gsven" version="2"}
META:FILEATTACHMENT{name="image016-2.png" attachment="image016-2.png"
attr="h" comment="" date="1378242431" path="image016-2.png" size="76183"
user="gcovell" version="1"} META:FILEATTACHMENT{name="image018.png"
attachment="image018.png" attr="h" comment="" date="1378494687"
path="image018.png" size="41708" user="gsven" version="2"}
META:FILEATTACHMENT{name="image019.png" attachment="image019.png"
attr="h" comment="" date="1378494707" path="image019.png" size="54824"
user="gsven" version="2"} META:FILEATTACHMENT{name="image020.png"
attachment="image020.png" attr="h" comment="" date="1378495072"
path="image020.png" size="76844" user="gsven" version="2"}
META:FILEATTACHMENT{name="image021.png" attachment="image021.png"
attr="h" comment="" date="1378495095" path="image021.png" size="74475"
user="gsven" version="2"} META:FILEATTACHMENT{name="image022.png"
attachment="image022.png" attr="h" comment="" date="1378495122"
path="image022.png" size="44685" user="gsven" version="2"}
META:FILEATTACHMENT{name="image023.png" attachment="image023.png"
attr="h" comment="" date="1378495136" path="image023.png" size="70726"
user="gsven" version="2"} META:FILEATTACHMENT{name="image024.png"
attachment="image024.png" attr="h" comment="" date="1378495154"
path="image024.png" size="107444" user="gsven" version="2"}
META:FILEATTACHMENT{name="image025.png" attachment="image025.png"
attr="h" comment="" date="1378495172" path="image025.png" size="60645"
user="gsven" version="2"} META:FILEATTACHMENT{name="image026.png"
attachment="image026.png" attr="h" comment="" date="1378495193"
path="image026.png" size="131159" user="gsven" version="2"}
META:FILEATTACHMENT{name="image027.png" attachment="image027.png"
attr="h" comment="" date="1378495301" path="image027.png" size="79889"
user="gsven" version="2"} META:FILEATTACHMENT{name="image028.png"
attachment="image028.png" attr="h" comment="" date="1378495280"
path="image028.png" size="57459" user="gsven" version="2"}
META:FILEATTACHMENT{name="image031.png" attachment="image031.png"
attr="h" comment="" date="1378495220" path="image031.png" size="105846"
user="gsven" version="2"} META:FILEATTACHMENT{name="image029.png"
attachment="image029.png" attr="h" comment="" date="1378495263"
path="image029.png" size="42163" user="gsven" version="2"}
META:FILEATTACHMENT{name="image030.png" attachment="image030.png"
attr="h" comment="" date="1378495246" path="image030.png" size="82132"
user="gsven" version="2"} META:FILEATTACHMENT{name="o_image007.png"
attachment="o_image007.png" attr="h" comment="" date="1378243030"
path="o_image007.png" size="60621" user="gcovell" version="1"}
META:FILEATTACHMENT{name="o_image009.png" attachment="o_image009.png"
attr="h" comment="" date="1378243050" path="o_image009.png" size="63285"
user="gcovell" version="1"} META:FILEATTACHMENT{name="jts403run1png.png"
attachment="jts403run1png.png" attr="h" comment="" date="1378243065"
path="jts403run1png.png" size="168633" user="gcovell" version="1"}
META:FILEATTACHMENT{name="RMrun1.png" attachment="RMrun1.png" attr="h"
comment="" date="1378243081" path="RMrun1.png" size="178077"
user="gcovell" version="1"}
META:FILEATTACHMENT{name="ServerOverview.png"
attachment="ServerOverview.png" attr="h" comment="" date="1378243094"
path="ServerOverview.png" size="13029" user="gcovell" version="1"}
META:FILEATTACHMENT{name="p_image017.log" attachment="p_image017.log"
attr="h" comment="" date="1378243171" path="p_image017.log" size="58758"
user="gcovell" version="1"} META:FILEATTACHMENT{name="image007.png"
attachment="image007.png" attr="h" comment="" date="1378494515"
path="image007.png" size="58884" user="gsven" version="2"}
META:FILEATTACHMENT{name="image011.png" attachment="image011.png"
attr="h" comment="" date="1378494541" path="image011.png" size="60332"
user="gsven" version="2"} META:FILEATTACHMENT{name="image016.png"
attachment="image016.png" attr="h" comment="" date="1378495722"
path="image016.png" size="76332" user="gsven" version="1"}
META:FILEATTACHMENT{name="image017.png" attachment="image017.png"
attr="h" comment="" date="1378495740" path="image017.png" size="58749"
user="gsven" version="1"}
