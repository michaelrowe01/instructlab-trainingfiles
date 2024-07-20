META:TOPICINFO{author="sahilkmansuri" date="1700821816" format="1.1"
version="1.10"} META:TOPICPARENT{name="PerformanceTroubleshooting"}

# Engineering Lifecycle Management Performance Troubleshooting Basics and Data Collection DKGRAY Author: [Isabel Murakami](Main.IsabelMurakami) Build basis: CLM 4.x - ELM 7.x [engineering-lifecycle-management-performance-troubleshooting-basics-and-data-collection-dkgray-author-isabel-murakami-build-basis-clm-4.x---elm-7.x]

ENDCOLOR

TOC{title="Page contents"}

This page was initially written for Rational Team Concert. In
Engineering Lifecycle Management 7.x, DOORS Next adopted the same
architecture as the other applications (RTC-\>Engineering Workflow
Manger, and RQM-\>Engineering Test Manager), so this article is now in
use for all 3 main applications. There is general applicability to the
other Java-based applications also.

When an user says, "The system is too slow" or "ELM is down", what do
they really mean? How do you quantify the user perception of slow? Maybe
the user was expecting that a plan with 500 Work Items would be
displayed within nearly the same amount of time it takes to open a small
one with 50 Work Items. Or maybe just part of a network was down,
affecting all users from a single region.

The only way to understand **what is** working, **what is not** working,
and **how long** it is taking, is by collecting all the data needed to
measure how long each kind of access normally takes under normal usage
and, also, under high usage. Therefore, when the user says, "It is
slow", you can compare and confirm (or not) how much it is slow.

Here is a guide for the Engineering Lifecycle Management (ELM)
Administrator of the main points to understand about your ELM install
and usage, as well as the tools that can be used to collect data
**before**, **during**, and **after** the slowness period.

## Performance Troubleshooting Basics

### Keys to Understanding Performance Issues

-   Performance is relative to the user We need to know the expected
    time under normal conditions and the actual time when experiencing
    slowness
-   The business need of the tool What is used more? SCM, Reports,
    planning
-   Performance issues can occur because of many factors

1.  **Where** is the performance degradation occurring?
    1.  Only one user or all users? (for example, certain users located
        in a certain building)
    2.  Is the performance degradation across the whole server?
2.  **When** is the performance degradation occurring? (all the time,
    under light load, under heavy load)
3.  **What** exactly is slow? SCM, load plans, builds, Reports,
    Dashboards? Or only certain components? (for example, it is slow
    loading plans, but work items are fine)
4.  Are there any hangs, crashes, Out-of-Memory (OOM), high CPU?

### Server versus Client side

When answering the question "where", normally we can detect if the
slowness has been caused by a Server side issue (all users affected) or
a Client side issue (some users affected). For example, all users
connecting via VPN are being affected (the others are working fine), or
a single user is not being able to access the application when using
Visual Studio (configuration problem on a single machine).

***Figure 1: Server versus Client performance indicators***

### Characterizing the Performance Problem

#### The Duration (How long is it taking?)

Collect information on several data points, taking note of the exact
date and time, as well as the amount of time it takes to complete the
task or activity. Why? To be able to compare the expected time versus
the actual time during the slowness, and understand what is slow.

-   Prepare a \#Test using tasks related to the slowest performance
    activity for the user (build, a specific query, saving Work Item
    (WI)). Always use the same tasks.
    -   Choose a big Project Area (PA)
    -   Choose a Plan view with several WIs
    -   Choose a word for a quick search
    -   Prepare a Query to run, for instance Open WIs on a selected PA
    -   Check-in & deliver of a sample Project Area
    -   Sample Build

#### Performance issues at the Server and Client side:

-   Gather a screenshot of the following page from the web UI. Ensure
    you gather a screenshot for each application (jts, ccm, qm/jazz,
    rm):

<https://://admin#action=com.ibm.team.repository.admin.activeServices>
<https://://service/com.ibm.team.repository.service.internal.counters.ICounterContentService>
<https://://admin#action=com.ibm.team.repository.admin.serverStatus>
<https://://admin#action=com.ibm.team.repository.admin.serverDiagnostics>
<https://://service/admin?internal=true#action=com.ibm.team.repository.admin.statistics>

-   How many users are on the system at the time of the slowness? It is
    difficult to answer this question specifically, however, using PMI
    monitoring on WebSphere, we can see how many requests on WebSphere
    are currently being processed.

#### Client side

-   Metronome output and test performance during the \#Test Steps
    execution
-   Collect HTTPWatch output during the \#Test steps execution

### Understanding the Environment

1.  Operating system of the user and server (RHEL, SUSE, Windows)
2.  Database vendor
3.  Application Server (Tomcat or WebSphere)
4.  Client type (web or eclipse) and Client version, Web Browser
    (Firefox, Internet Explorer, Chrome) and Browser version
5.  System Specifications: RAM, Heap Size, CPU, Virtualized or Physical
    machine?
6.  Network Information:
    1.  Where is the DB located relative to the Application Server?
    2.  Where are the users located relative to the Application Server?
    3.  Is there a firewall, loadbalancer, proxy?
    4.  How and When are the Maintenance tasks executed? (backup,
        reindex, update statistics, automatic tasks to clean up
        temporary folders)
7.  Has a server rename occurred?
8.  Is your server using IPv6? Are your clients using IPv6?
9.  Which applications/products/APIs are accessing this Jazz Team Server
    (JTS) or DB Repository? Requirements Management (RM), Quality
    Management (QM), Change and Configuration Management (CCM), Jazz
    Reporting Service (rb), BuildForge, TaskTop, custom applications?
10. What else is running on these environment, sharing the hardware
    resources?
11. Physical driver location (Indices location) NFS, local/shared paths

### Understanding the Size and Usage

1.  How many active users? (JTS/Admin active users)
2.  Are all the users in the same timezone as the Server?
3.  How many concurrent users? (PMI settings on WebSphere Application
    Server (WAS))
4.  What are the days and times with more usage?
5.  How many Project Areas?
6.  What is the size of the biggest Project Area? And the smallest one?
7.  What does the user use the most? Reporting, Planning, SCM?
8.  Regarding Check-in&Delivery, What is the size of the biggest stream
    to be delivered?
9.  What is the size of your DB repository?
10. The number of Builds, how many build engines, how much source code
    is involved? Where is the build being executed (network, version)?

## Data Collection

### Collect the Configuration

#### Client side

-   Parameters used to start Eclipse

#### Server side

-   JVM parameters used for each application
-   (WAS) Webcontainer thread pool size for each application : Servers
    -\> Server Types -\> WebSphere application server -\> \[Server
    Name\] -\> Thread Pools -\> WebContainer.
-   (WAS) Asynch or Synch mode: Check if the property
    com.ibm.ws.webcontainer.channelwritetype does exist on Servers -\>
    Server Types -\> WebSphere application server -\> \[Server Name\]
    -\> Container Settings -\> Web Container Settings -\> Web Container
    -\> Custom Properties.
-   Value of "Maximum Record Count" defined on the Advanced Property for
    the BIRT Reports
-   DB connection parameters for each application:

<https://://admin#action=com.ibm.team.repository.admin.configureDatabaseConnection>

-   IHS/plug-in configuration files

### Prepare the Data Collection

#### Client side

-   Activate
    [metronome](https://jazz.net/wiki/bin/view/Deployment/JazzMetronomeToolKeepsUsHonest)
    on Eclipse Client
-   (Firefox) Download and Install
    [Firebug](http://getfirebug.com/downloads)
-   (Firefox) Download and Install
    [NetExport](http://www.softwareishard.com/blog/netexport/)
-   (Firefox and Internet Explorer) Download and Install
    [HttpWatch](https://www.httpwatch.com/download/)

#### Server side

-   Prepare a \#TestConnection : Ping and traceroute application x
    database.
-   Enable PMI collection data [Tuning WebSphere servers for Rational
    Team Concert performance](https://jazz.net/library/article/1430)
-   Monitoring and Tuning -\> Performance Monitoring Infrastructure
    (PMI) -\> \[Server Name\] -\> Enable Performance Monitoring
    Infrastructure (PMI)
-   Performance Monitoring Infrastructure (PMI) \> server1 \> Custom
    monitoring level:

Threads Enable ActiveCount PoolSize Servlet Session manager Enable
ActiveCount and LiveCount

-   (WAS) Enable the verbose log by adding -verbose:gc on your JVM or by
    following [Enabling verbose garbage collection (verboseGC) in
    WebSphere Application
    Server](http://www-01.ibm.com/support/docview.wss?uid=swg21114927)
-   (Tomcat) Enable the Garbage collection through the following JVM
    Options for CATALINA_OPTS:

-verbose:gc -Xloggc:\$CATALINA_HOME/logs/gc.log or
Xloggc:CATALINA_HOME/logs/gc.log -XX:+PrintHeapAtGC (only if more
details about the memory consumed is needed, extra output generated)
-XX:+PrintGCDetails -XX:+PrintGCTimeStamps
-XX:-HeapDumpOnOutOfMemoryError

##### WAIT

1.  Register at [WAIT](https://wait.ibm.com) and read the WAIT manual
2.  Download the script on each application machine (jts/ccm/qm/rm)

#### Out-of-Memory (OOM)

-   (WAS) Read [MustGather: Out of Memory errors with WebSphere
    Application Server on AIX, Linux, or
    Windows](http://www.ibm.com/support/docview.wss?uid=swg21138587) and
    choose the better way to collect data. If needed, download and
    install IBM Support Assistant Data collector on the machines facing
    the OOM (jts/ccm/qm/rm)

### Data Collection during Slow Performance

#### Server side

-   Engage Database support team for locks, contentions, abnormal DB
    behavior.
-   Execute the \#TestConnection - ping/traceroute from app database
-   Collect WAIT Data

./waitDataCollector.sh --sleep 30 --iters 10 --javacoreDir \[PID\]

##### Hang, Crash or High CPU

-   Windows Capture screen shots showing the Task Manager (CPU sorted).
    Also, from the Task Manager/Resource Monitor button, take screen
    shots of all tabs, expanding the sections.

#### Server and Client side, if System is Accessible:

-   Execute the \#Test steps prepared at the Characterizing the
    performance problem
    -   Gather a screenshot of the following page from the web UI.
        Ensure you gather a screenshot for each application (jts, ccm,
        qm/jazz, rm):

<https://://admin#action=com.ibm.team.repository.admin.activeServices>
<https://://service/com.ibm.team.repository.service.internal.counters.ICounterContentService>
<https://://admin#action=com.ibm.team.repository.admin.serverStatus>
<https://://admin#action=com.ibm.team.repository.admin.serverDiagnostics>
<https://://service/admin?internal=true#action=com.ibm.team.repository.admin.statistics>

-   How many users are on the system at the time of the slowness? It is
    difficult to answer this specific question, however using PMI
    monitoring on WebSphere, we can see how many requests on WebSphere
    are currently being processed.

#### Client side

-   Metronome output and test performance during the \#Test Steps
    execution
-   Collect HTTPWatch output during the \#Test steps execution

### Data Collection after Slow Performance

#### Server side

-   ISALite (run on all machines: jts/ccm/qm/rm)
-   IHS and plugin logs: http_plugin.log, access_log, error.log
-   Statistics: Ensure you gather a screenshot for each application
    (jts, ccm, qm/jazz, rm).:

<https:////service/admin?internal=true#action=com.ibm.team.repository.admin.statistics>

#### Out-of-Memory (OOM)

-   Heapdump and core files created
-   If we have a core file, execute JExtract included with JRE in
    server/jre/bin

\#jextract.exe

#### Client side

-   Eclipse Client log

##### Related topics: [Initial Troubleshooting Investigation](InitialTroubleshootingInvestigation), [How to start a troubleshooting assessment](HowToStartATroubleshootingAssessment), [Performance troubleshooting](PerformanceTroubleshooting), [Browser performance](BrowserPerformance) [related-topics-initial-troubleshooting-investigation-how-to-start-a-troubleshooting-assessment-performance-troubleshooting-browser-performance]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)
-   [Support must gather for performance hang or high cpu
    issues](https://www.ibm.com/support/pages/mustgather-performance-hang-or-high-cpu-issues-elm-applications?)

##### Additional contributors: Main.DianeEveritt [additional-contributors-main.dianeeveritt]

##### Questions and comments: [questions-and-comments]

COMMENT{type="below"
target="RTCTroubleshootingBasicsandDataCollectionComments"
button="Submit"}

META:FILEATTACHMENT{name="serverVSclient.PNG"
attachment="serverVSclient.PNG" attr="h" comment="Server versus client
side performance troubleshooting indicators" date="1423251663"
path="serverVSclient.PNG" size="194559" user="d3v3r1tt" version="1"}
