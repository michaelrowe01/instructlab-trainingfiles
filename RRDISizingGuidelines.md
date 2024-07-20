META:TOPICINFO{author="gcovell" date="1396451436" format="1.1"
version="1.12"}
META:TOPICPARENT{name="PerformanceDatasheetsAndSizingGuidelines"}

# RRDI 2.0.x sizing guidelines [rrdi-2.0.x-sizing-guidelines]

DKGRAY Authors: Main.RosaNaranjo Build basis: CLM 3.x, 4.x, RRDI 2.x
ENDCOLOR

TOC{title="Page contents"}

Sizing a deployment of CLM is a frequent concern in deployment planning.
But, what about sizing the Rational Reporting for Development
Intelligence (RRDI) deployment? The following items are the ones to
consider when thinking about an RRDI deployment sizing.

-   The recommended report server configuration; CPU, memory, disk
    space, and JVM settings
-   The recommended size of the content store database

## General

The data warehouse is a core component of CLM reporting. CLM ETL jobs
extract data from the JTS and CLM applications and load them into the
data warehouse. Both the BIRT- and Cognos-based reports pull data from
the data warehouse when executed. The content store database is mostly
scaled with the number of reports, not necessarily with the number of
users.

### RRDI 2.0 Sizing Considerations

-   A CLM environment with 2500 concurrent users doesn't necessary
    equate to 2500 users running Cognos reports at the same time. Figure
    out how many of the 2500 CLM users are expected to run a Cognos
    report or a viewlet containing Cognos reports concurrently. This
    will allow for a proper sizing.
-   The Cognos team has a general rule of thumb, using a factor of 10,
    when it comes to sizing: 1000 total system users --\> 100
    authenticated users --\> 10 concurrent users. This is definitely not
    the case for CLM, where users are expected to frequently access the
    CCM, QM and RM applications throughout the day. Validate whether
    this assumption is correct: 2500 total CLM users --\> 250
    authenticated report users --\> 25 concurrent report users. Who
    knows, the investigation may result in 2500 total CLM users --\>
    2500 authenticated report users --\> 250 concurrent report users.

Here is an example rough sizing for 250 concurrent report users:

Assumptions:

-   Each user runs a viewlet containing 6 Cognos reports.
-   Each report server has 2 CPUs with 4 cores each = 8 CPU cores.
-   Each report server has 16GB of memory.
-   Each report server has 64-bit OS.
-   Each report takes up 512MB of memory to run.

Rough Sizing:

1.  On each report server, set aside 4GB for the OS and processes
    (including WAS and the JVM that runs the IBM Cognos Web
    application). This leaves 12GB for the `BIBusTKServerMain`
    processes, which are spawned by the Cognos BI server to run reports.
2.  On a report server with 8 CPU cores, the maximum number of
    `BIBusTKServerMain` processes that are supported is 8 x 2 = 16. If
    each `BIBusTKServerMain` process takes up 512MB, 16 of them running
    in parallel would consume 512MB x 16 = 8GB. This is under 12GB, so
    we are good here.
3.  Each `BIBusTKServerMain` process is multi-threaded and is designed
    to run 4 reports in parallel. In theory, a report server with 16
    `BIBusTKServerMain` processes are therefore capable of running 16 x
    4 = 64 reports in parallel. In practice, this may not be observed.
    It all depends on the complexity and size of the report and whether
    report output are cached. In addition, `BIBusTKServerMain` processes
    in current RRDI and Insight are 32-bit and has a memory constraint
    of 2GB.
4.  250 CLM users running a viewlet with 6 Cognos reports concurrently =
    250 x 6 = 1500 concurrent report executions. This means the system
    needs a total of 1500 / 64 = 24 report servers.

When configuring the report server, review the JVM initial and maximum
heap size. If the report server has 64-bit OS and more than 8GB of
memory, the initial and maximum heap size can both be set to 1024MB. It
is strongly recommended that the report server is installed on a machine
with 64-bit OS and 64-bit WebSphere Application Server.

#### Content Store database sizing guidelines

See [published
guidelines](http://pic.dhe.ibm.com/infocenter/cbi/v10r1m0/topic/com.ibm.swg.im.cognos.crn_arch.10.1.0.doc/crn_arch_id2709ADGplnnfrastrct.html#ADGplnnfrastrct)
available in the Cognos BI infocenter.

##### Related topics: [Deployment planning](DeploymentPlanning) [related-topics-deployment-planning]

##### Additional contributors: Main.KelvinLow, Main.DangRen [additional-contributors-main.kelvinlow-main.dangren]

META:TOPICMOVED{by="rnaranjo" date="1370979428"
from="Deployment.DatawarehouseSizingGuidelines"
to="Deployment.RRDISizingGuidelines"}
