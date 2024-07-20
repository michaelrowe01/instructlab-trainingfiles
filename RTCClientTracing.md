META:TOPICINFO{author="sbeard" date="1368532224" format="1.1"
version="1.18"} META:TOPICPARENT{name="RTCClientPerformance"}

# How to enable additional tracing in the Rational Team Concert client for Eclipse IDE [how-to-enable-additional-tracing-in-the-rational-team-concert-client-for-eclipse-ide]

DKGRAY Authors: PerformanceTroubleshootingTeam Build basis: Rational
Team Concert 4.0.x ENDCOLOR

TOC{title="Page contents"}

It is possible to activate built-in traces in the RTC Eclipse Client.
These traces may provide additional information about issues that are
hard to reproduce in a different environment, including performance
information.

## How to enable additional tracing

To add traces to an Eclipse-based application, you must create a file
containing trace strings, and then relaunch the application with a
specific command line.

### How to find out what trace options are available

To find out what trace strings are available, you can proceed as
follows:

1 Open the Java Perspective: **Window \> Open Perspective \> Java** 1
Click on **Run \> Run Configurations...** 1 Click on **Eclipse
Application** 1 Press the **New** button (it is the first icon on the
top-left) 1 Click on **Tracing** 1 Select the plug-ins you want to
trace. The RTC Plug-in names start with *com.ibm.team*. In some cases,
you might need to trace Eclipse plug-ins, for example
*org.eclipse.core.jobs* or *org.eclipse.core.resources*. 1 Click on
**Run**. A second instance of Eclipse starts, with the traces enabled. 1
In the original instance, do: **Window \> Show View \> Console**. Look
at the startup messages. You will see something like: Debug options:
<file://.metadata/.plugins/org.eclipse.pde.core/New_configuration/.options>
loaded 1 Open the *.options* file with a text editor.

### Example of .options file with Trace strings

1 Save the generated *.options* file **in the RTC Client for Eclipse
installation directory**. This file contains specific trace strings for
the plug-ins you want to trace. 1 For example, these trace strings are
appropriate for the Eclipse Client (*rcp* stands for Rich Client
Application):
com.ibm.team.filesystem.rcp.core/trace.componentsyncmodel.contexts=true
com.ibm.team.filesystem.rcp.core/trace.activeworkspaces=true
com.ibm.team.filesystem.rcp.core/trace.componentsyncmodel.refresh=true
With these traces you will get results like the following while checking
in and delivery source files: ... BEGIN: LocalChangeSource.update (Thu
Feb 28 17:20:33 CET 2013) END: LocalChangeSource.update (1 ms) BEGIN:
ComponentSyncContext.refresh full true (context CCMProject1 Default
Component CCMProject1 Stream Workspace-CCMProject1 Stream type 2 repo:
<https://ibm-oprsurvfat7.ams.nl.ibm.com:9443/ccm/,user1,1,480>) (Thu Feb
28 17:20:33 CET 2013) BEGIN: CompareToNode.computeItemsAndChildren
elements size 1 (Thu Feb 28 17:20:33 CET 2013) BEGIN:
ItemManager.fetchCompleteItem
<com.ibm.team.repository.common.model.impl.ContributorHandleImpl@171f171f>
(stateId: , itemId: \[UUID \_cdenUIAAEeKeWtSjJ9gfOQ\], origin:
<com.ibm.team.repository.client.internal.TeamRepository@2a652a65>,
immutable: true) (Thu Feb 28 17:20:33 CET 2013) END:
ItemManager.fetchCompleteItem DEFAULT Proxy of
<com.ibm.team.repository.common.model.impl.ContributorImpl@15b215b2>
(stateId: \[UUID \_63Y9V4AGEeKa-d3d_MzpVw\], itemId: \[UUID
\_cdenUIAAEeKeWtSjJ9gfOQ\], origin:
<com.ibm.team.repository.client.internal.TeamRepository@2a652a65>,
immutable: true) (contextId: \[UUID \_8lNyYNwSEd2pIJ5QVwgQGg\],
modified: 2013-02-26 12:23:18.311, workingCopy: ) (mergePredecessor:
null, workingCopyPredecessor: , workingCopyMergePredecessor: ,
predecessor: \[UUID \_63XvMoAGEeKa-d3d_MzpVw\]) (emailAddress:
<user1@example.com>, userId: user1, name: user1 user1, archived: false)
(2 ms) ....

Note: the *com.ibm.team.filesystem.cli* strings relate to the Command
Line Interfaces client. See [SCM Command Line Interfaces
Metronome](https://jazz.net/wiki/bin/view/Main/SCMCommandLineMetronome)
for more information.

### Launch the RTC Client for Eclipse with the traces enabled

1 Launch the following command **from the RTC Client Installation
directory** (so that the *.options* file can be found by the JVM): BR
Windows: eclipsec.exe -product com.ibm.team.concert.product -debug \>
trace.txt 2\>&1 Linux: ./jdk/jre/bin/java -Xms100m -Xmx512m
-Dosgi.requiredJavaVersion=1.5 -Dosgi.bundlefile.limit=100 -jar
./plugins/org.eclipse.equinox.launcher_1.1.1.R36x_v20101122_1400.jar
-showsplash -debug -product com.ibm.team.concert.product \> trace.txt
2\>&1 1 Note: The above command line for Linux is derived from the
contents of the *eclipse.ini* file contained in the Rational Team
Concert Client for Eclipse IDE v4.0.1. It is subject to change in higher
releases or if you install on an existing Eclipse, with a different JVM,
shell-sharing with other products etc. An easy way to construct the
command line appropriate for your installation is as follows: 1 Launch
the product normally 1 From a command prompt, execute "ps -ef \|grep
javaw" (to see the command line of all "javaw" processes. There may be
more than one, and you have to identify the one that refers to Rational
Team Concert Client for Eclipse IDE) 1 Make note of the command line
used to launch RTC Client for Eclipse IDE 1 Replace "javaw" with "java"
1 Add "-debug -product com.ibm.team.concert.product \> trace.txt 2\>&1"
at the end of the command 1 Note: If you installed the Rational Team
Concert for Eclipse IDE - Extension Install - on Rational Application
Developer, see [How to trace Rational Application Developer for
WebSphere
Software](http://www-01.ibm.com/support/docview.wss?uid=swg21327307) 1
The resulting trace will be found in the file *trace.txt*, located in
the RTC Client Installation directory, after the run completes.

##### Related topics: [related-topics]

-   [Why is the Rational Team Concert client slow?
    ](RTCClientPerformance)
-   [SCM command line interfaces
    metronome](https://jazz.net/wiki/bin/view/Main/SCMCommandLineMetronome)
-   [Performance troubleshooting](PerformanceTroubleshooting)

##### External links: [external-links]

-   How to trace Rational Application Developer for WebSphere Software:
    <http://www-01.ibm.com/support/docview.wss?uid=swg21327307>
-   How to contact IBM support:
    <http://www-01.ibm.com/software/rational/support/contact.html>
-   How to send data to IBM support:
    <http://www.ecurep.ibm.com/app/upload>

##### Additional contributors: None [additional-contributors-none]

##### ! Questions and comments: [questions-and-comments]

COMMENT{type="below" target="RTCClientTracingComments" button="Submit"}

INCLUDE{"RTCClientTracingComments"}

META:FILEATTACHMENT{name="Tracing1.jpg" attachment="Tracing1.jpg"
attr="" comment="" date="1361991352" path="Tracing1.jpg" size="117377"
user="lziosi" version="1"} META:FILEATTACHMENT{name="Tracing2.jpg"
attachment="Tracing2.jpg" attr="" comment="" date="1361991318"
path="Tracing2.jpg" size="141732" user="lziosi" version="1"}
