META:TOPICINFO{author="sbagot" date="1432664522" format="1.1"
version="1.33"} META:TOPICPARENT{name="PerformanceTroubleshooting"}

# Why is the Rational Team Concert client slow? [why-is-the-rational-team-concert-client-slow]

DKGRAY Authors: PerformanceTroubleshootingTeam Build basis: RTC 4.0.1
ENDCOLOR

TOC{title="Page contents"}

This page includes information that will help you determine why your IBM
Rational Team Concert client is slow or not responding and help you
understand which components contribute the most to the problem.

## Initial assessment

### Symptoms

-   When you use the Rational Team Concert Eclipse client, the response
    times are long, or the tool becomes unresponsive.

### Impact/scope

-   What specific operations are slow?
-   Does the operation eventually complete, or is the tool indefinitely
    unresponsive (hung)?
-   Does it affect only one, or multiple client installations?
    -   Where are the installations that are affected by the problem
        compared to those that perform acceptably?
-   Does it affect the Client for Eclipse IDE, or the Client for Eclipse
    IDE - Extension Install?
    -   Does it happen only if the Client for Eclipse IDE - Extension
        Install - is installed in an Installation Manager package group
        that contains other products? If so, which products are
        shell-sharing? BR(You can see this by launching the shortcut
        **IBM Installation Manager \> View Installed Packages**)
    -   Does it happen only when there are third-party plug-ins
        installed on the client for Eclipse IDE? BR (You can gather the
        list of installed plug-ins by launching the **Client for Eclipse
        IDE \> Help \> about \> Installation Details \> Configuration**.
        Then press Copy to clipboard and paste into a text file).
    -   Does it happen in only one specific Eclipse workspace?
-   Does it affect the Client for Microsoft Visual Studio IDE?
-   Does it affect the Rational Team Concert Windows shell integration?
-   Does it affect the SCM Command Line Interfaces (CLI)?

### Environmental changes

-   What sort of things might have changed in the environment (outside
    the products)?
    -   Think broadly about hardware, software, network, client.

## Recommended data-gathering and subsequent analysis steps

### Client for Eclipse IDE: Slow response

-   You should start by investigating whether the performance issue is
    caused by the client-server interaction.
    -   You can use [Jazz
        Metronome](http://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.5/com.ibm.team.concert.doc/topics/t_metronome.html)
        to measure the response times between the Rational Team Concert
        client and the Jazz Team Server. See [The Jazz Metronome Tool
        Keeps us
        honest](https://jazz.net/blog/index.php/2008/02/01/the-jazz-metronome-tool-keeps-us-honest/)
        for more information.

<!-- -->

-   If you know that the web client is performing the same actions much
    faster than the Eclipse client, investigate the client itself in
    more detail. The following data-gathering techniques are listed in
    order of increasing complexity.
    -   The Eclipse workspace log, located in:
        `workspace\.metadata\.log` can offer a starting point for the
        investigation of local client issues. Verify if the times of any
        listed exceptions match the time of occurrence of the observed
        performance issue. The names of the Java packages involved in
        the exceptions provide an indication of the components involved.
    -   Many operations run as background jobs in Eclipse (for example:
        validation, indexing). You can get an idea of what background
        jobs are running by launching:
        -   **Window \> Show View \> Progress**
        -   Click on the triangle pointing towards the bottom, on the
            toolbar of the Progress View.
        -   Select **Preferences \> Show System and sleeping
            operations**. The Progress View will show you what
            background jobs might be using CPU cycles and slowing down
            the progress of User Interface thread that runs the user
            requested operations.
    -   In some cases, based on the nature of the initial errors you see
        in the `workspace\.metadata\.log`, or the list of background
        jobs in the Progress View, [enable additional
        tracing](RTCClientTracing) in the Client for Eclipse IDE.
    -   If you need to investigate the performance of the Client for
        Eclipse IDE down to the level of measuring the execution times
        of individual method calls, you can use various techniques to
        [profile](profileRationalTeamConcertClientForEclipse) the Client
        for Eclipse IDE.
    -   In case the Client for Eclipse IDE is installed together with
        other products or plug-ins, extend the tracing or profiling
        options listed in the above links to include operations
        initiated by such other products or plug-ins. However, profiling
        and tracing are resource-intensive operations, so you should
        have a specific idea of what needs to be traced or profiled to
        reduce the amount of data that needs to be collected and
        analyzed.

### Client for Eclipse IDE: Hangs

-   If the Client for Eclipse IDE is unresponsive (hanging): you must
    gather at least three **JavaCores** at some time interval (depending
    on the total duration of the slow operation, the interval could
    range from a few seconds to one or more minutes). 1 To generate the
    JavaCores:
    -   UNIX or Linux: 1 Find the process ID of the Client for Eclipse
        IDE, by running `ps -ef |grep javaw` 1 Execute the command
        `kill -3 pid` where pid is the process ID identified above
    -   Windows: the first two methods described in the technote
        [MustGather: Java Application
        Hangs](http://www.ibm.com/support/docview.wss?uid=swg21391829)
        are applicable to the case of the Client for Eclipse IDE. 1 Once
        you have gathered the JavaCores, you can analyze them with the
        [IBM Support
        Assistant](http://www.ibm.com/software/support/isa/workbench.html),
        by adding the IBM Thread and Monitor Dump Analyzer for Java
        (TMDA). Alternatively, you can use
        [WAIT](https://wait.ibm.com/).

### Client for Microsoft Visual Studio IDE

-   If the issue occurs in the Client for Microsoft Visual Studio IDE,
    you can use this technote to gather more information: [How to turn
    on Rational Team Concert trace log from Visual
    Studio](http://www.ibm.com/support/docview.wss?uid=swg21445903)

### Rational Team Concert Windows shell integration for Microsoft Windows Explorer

-   If the issue occurs in the [Rational Team Concert Windows shell
    integration for Windows
    Explorer](http://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.5/com.ibm.team.scm.doc/topics/t_scm_shell_intro.html),
    configure logging as follows: 1 Open Microsoft Windows Explorer 1
    Open the **Rational Team Concert Shell Control Panel** 1 Select
    **Manage Preferences \>Other Preferences** in the Control Panel 1
    Set the **Trace Level** to **Info** or **Verbose**. See the
    following image: 1 For the location of the log files, from the
    Rational Team Concert Shell Control Panel, click on Help and select:
    **Open Log File**, **Save Log Files**, as in the following
    screenshot:

### Command line interfaces (CLIs)

-   You can use [metronome for the CLI](SCMCommandLineMetronome) to
    enable tripcount and timing statistics for the command line
    interface.
-   You can [set CLI properties for
    logging](http://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.5/com.ibm.team.scm.doc/topics/r_scm_cli_preferences_properties.html).
    See also: [How to enable CLI
    logging](https://jazz.net/wiki/bin/view/Main/SCMCommandLineBugReporting).

## Possible causes and solutions

The following recommendations are generally applicable:

### Start a new Eclipse workspace

If the issue occurs in only one Eclipse workspace, it may be ideal to
create a new workspace. Over time, the metadata, for example log and
history files, accumulates in the workspace .metadata directory and
negatively impacts performance. After a new workspace is created, you
should import all of your projects into the new workspace. Note that
preferences may be workspace-specific and may be reset to their default
values.

### System performance

The Rational Team Concert client needs fast access to the disk(s) where
the installation is located and where the Eclipse .metadata folder and
the projects are stored. This applies also to the Sandbox that you use
with the Windows shell integration. Anything that slows this down (disk
fragmentation, access to a remote disk, Antivirus) can affect
performance.

-   Defragment the disk where the installation, the Eclipse workspaces,
    the projects, and the sandbox are stored.
-   Make sure that the installation and the Eclipse workspaces are
    stored locally (not on a remote disk).
-   Antivirus software processes that provide real-time protection or
    monitoring scan files each time that they are loaded into system
    memory. This scanning activity can negatively impact the performance
    of any product function that loads large amounts of data into system
    memory. Examples of product functions that might be negatively
    impacted by real-time scanning are startup and (automatic) build.
    Verify if the Antivirus has significant impact, by testing the same
    functions with real-time scanning of the Eclipse workspace or of the
    sandbox switched off.

##### Related topics: [related-topics]

-   [How to enable additional tracing in the RTC Client for Eclipse
    IDE](RTCClientTracing)
-   [How to profile the RTC Client for Eclipse
    IDE](profileRationalTeamConcertClientForEclipse)
-   [SCM CommandLine Metronome](SCMCommandLineMetronome)
-   [Performance Troubleshooting](PerformanceTroubleshooting)

##### External links: [external-links]

-   Jazz Metronome: Measuring server response times:
    <http://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.5/com.ibm.team.concert.doc/topics/t_metronome.html>
-   The Jazz Metronome Tool Keeps us honest:
    <https://jazz.net/blog/index.php/2008/02/01/the-jazz-metronome-tool-keeps-us-honest/>
-   MustGather: Java Application Hangs:
    <http://www.ibm.com/support/docview.wss?uid=swg21391829>
-   How to turn on Rational Team Concert trace log from Visual Studio:
    <http://www.ibm.com/support/docview.wss?uid=swg21445903>
-   IBM Support Assistant:
    <http://www.ibm.com/software/support/isa/workbench.html>
-   WAIT: <https://wait.ibm.com/>
-   Rational Team Concert Shell:
    <http://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.5/com.ibm.team.scm.doc/topics/t_scm_shell_intro.html>
-   Performance of SCM CLI - A Study:
    <https://jazz.net/wiki/bin/view/Main/SCMCLIPerformanceStudy>
-   Getting started with the Jazz SCM command line in Rational Team
    Concert: <https://jazz.net/library/article/620>
-   How to contact IBM Support:
    <http://www.ibm.com/software/rational/support/contact.html>
-   How to send data to IBM Support:
    <http://www.ecurep.ibm.com/app/upload>

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="WinExplorerIntegration_4.0.1small.jpg"
attachment="WinExplorerIntegration_4.0.1small.jpg" attr="h" comment=""
date="1365174738" path="WinExplorerIntegration_4.0.1small.jpg"
size="50589" user="lziosi" version="1"}
META:FILEATTACHMENT{name="WinExplorerIntegrationFiles_4.0.1.jpg"
attachment="WinExplorerIntegrationFiles_4.0.1.jpg" attr="h" comment=""
date="1365174475" path="WinExplorerIntegrationFiles_4.0.1.jpg"
size="129793" user="lziosi" version="1"}
META:FILEATTACHMENT{name="WinExplorerIntegration_4.0.1.jpg"
attachment="WinExplorerIntegration_4.0.1.jpg" attr="h" comment=""
date="1365174362" path="WinExplorerIntegration_4.0.1.jpg" size="88337"
user="lziosi" version="1"}
META:FILEATTACHMENT{name="WinExplorerIntegrationFiles_4.0.1small.jpg"
attachment="WinExplorerIntegrationFiles_4.0.1small.jpg" attr="h"
comment="" date="1365174639"
path="WinExplorerIntegrationFiles_4.0.1small.jpg" size="34503"
user="lziosi" version="1"}
