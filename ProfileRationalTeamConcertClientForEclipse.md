META:TOPICINFO{author="lziosi" date="1383827665" format="1.1"
version="1.15"} META:TOPICPARENT{name="RTCClientPerformance"}

# How to profile the Rational Team Concert client for Eclipse IDE [how-to-profile-the-rational-team-concert-client-for-eclipse-ide]

DKGRAY Authors: PerformanceTroubleshootingTeam Build basis: RTC 4.0.x
ENDCOLOR

TOC{title="Page contents"}

Profiling allows you to get very detailed timing information about
individual method calls in the Rational Team Concert Client for Eclipse
IDE. Profiling is only recommended if you are trying to address a very
specific performance concern, and typically you will want to supply the
gathered information to IBM support for more investigation. In general,
Profiling produces a very large amount of trace data. It is best to keep
the profiling session as short as possible, and perform only the steps
that are strictly required to reproduce the observed performance issue.

If you are using a standalone installation of the Rational Team Concert
Client for Eclipse IDE, you can use the Eclipse Test & Performance Tools
Platform Project (TPTP) profiling capabilities, which are freely
available.

|  |
|----|
| If the Rational Team Concert Client for Eclipse IDE is installed in the same Installation Manager Package Group with Rational Application Developer or Rational Software Architect (for WebSphere), you have the additional option of using a built-in profiling agent. See the technote [How can you tell what is the exact cause of the slow response of the product?](http://www-01.ibm.com/support/docview.wss?uid=swg21627067). |

## Eclipse Test & Performance Tools Platform Project (TPTP) installation prerequisites

-   The required TPTP software is included in the following products:
    -   Rational Application Developer
    -   Rational Software Architect
    -   Rational Software Architect for WebSphere

<!-- -->

-   Alternatively, you can install a standalone [Eclipse 3.6.2
    (Helios)](http://www.eclipse.org/downloads/packages/release/helios/sr2).
    You will have to add TPTP 7.2.4 as described in: [Install TPTP with
    Update
    Manager](http://wiki.eclipse.org/Install_TPTP_with_Update_Manager).
    Note that Eclipse 3.6.2 is the highest version of Eclipse that
    includes TPTP.

## Launching the Rational Team Concert Client for Eclipse IDE in profiling mode

### Prepare the Rational Team Concert Client for Eclipse IDE for profiling

Prepare the Rational Team Concert Client for Eclipse IDE for profiling
as follows:

1 Open the file *eclipse.ini*, located in the RTC Client for Eclipse IDE
installation directory. 1 Determine what is the location of the JVM used
(found after the -vm argument) 1 Determine the version and the bitness
of the JVM, by launching the command: java -version from the directory
where the JVM is located 1 If the RTC Client JVM version is 32bits, then
you will need to use the 32bits profiler agent, if the RTC Client JVM is
64bits, you will need to use the 64bits profiler agent. 1 The location
of the Java profiler agents (referred to as **Java profilers absolute
path** in the following sections) is as follows:BR For
Windows:\<\>\plugins\org.eclipse.tptp.platform.jvmti.runtime\_\agent_files\For
Linux:
\<\>/plugins/org.eclipse.tptp.platform.jvmti.runtime\_/agent_files/ 1 To
profile the RTC Client for Eclipse IDE with the CPU Profiler in
standalone mode, with filters contained in *filters.txt* and writing the
results into *log.trcxml*, add the following line at the very end of the
*eclipse.ini* file (after the *-vmargs* argument) BR For Windows:
-agentpath:\JPIBootLoader=JPIAgent:server=standalone,file=log.trcxml,filters=filters.txt;CGProf
For Linux the entire library file name must be used. So
*libJPIBootLoader.so* should be used instead of *JPIBootLoader* or
*libJPIBootLoader*:
-agentpath:/libJPIBootLoader.so=JPIAgent:server=standalone,file=log.trcxml,filters=filters.txt;CGProf
1 For example, for a Windows installation of RTC Client for Eclipse 64
bits, you would use:
-agentpath:C:\eclipse-java-helios-SR2-win32-x86_64\eclipse\plugins\org.eclipse.tptp.platform.jvmti.runtime_4.6.3.v201102041710\agent_files\win_em64t\JPIBootLoader=JPIAgent:server=standalone,file=log.trcxml,filters=filters.txt;CGProf
1 Save the *eclipse.ini* file.

### Prepare the filters

Filtering is mandatory in this case: if you do not filter anything the
RTC Client for Eclipse IDE will be unacceptably slow and the resulting
*log.trcxml* file will be multiple Gigabytes just to complete the
startup phase.

1 Create a file called *filters.txt* in the same directory where
*eclipse.ini* is located. 1 Use the following contents to start with:
com.ibm.team.\* \* INCLUDE \* \* EXCLUDE This means that all the methods
of all the classes in packages that start with *com.ibm.team* are
included, and all other methods are excluded. You might be able to
restrict the filters further based on your knowledge of the problem
area, or you might want to include some of the Eclipse packages if they
are relevant to the problem at hand. For the full syntax of the filters,
see [Profiling an application in stand-alone
mode](http://publib.boulder.ibm.com/infocenter/radhelp/v8r5/index.jsp?topic=2Forg.eclipse.tptp.platform.doc.user2Ftasks2Fteprofsa.htm).

### Launch the RTC Client for Eclipse and reproduce the issue

1 Open a command prompt. 1 Change directory to the installation
directory of the Rational Team Concert Client for Eclipse, so that the
file filters.txt is found in the current directory. 1 Launch the RTC
Client for Eclipse from that directory. 1 Reproduce the problem (note
that the execution time will be significantly slower than normal,
depending on how many methods you included in the filters). Make sure to
keep the session as short as possible (do not include unnecessary
operations, or reading the resulting data will be more difficult). 1
Collect the file *log.trcxml* 1 Remember to remove the additional line
from the *eclipse.ini* file.

### Read the profiling data

To read the profiling data, you need to launch one of the products
listed in the Installation prerequisites section above. Then proceed as
follows:

1 Open the Profiling and Logging Perspective: **Window \> Open
Perspective \> Other \> Profiling and Logging** 1 Right click on the
Profiling Monitor view and select: **Import \> Profiling and Logging \>
Profiling file**, as follows: 1 Wait for the file to be imported, then
right-click on it and choose: **Open with \> Execution statistics**. You
will see results like the following: 1 You can drill down to the
individual method level. You can see how many times a method was called
and how much time it took. 1 This data helps in identifying which
specific methods contribute to the performance bottleneck. For the
interpretation of the data, you might want to contact IBM support and
supply the generated file.

##### Related topics: \* [Why is the Rational Team Concert Client slow? ](RTCClientPerformance) [related-topics-why-is-the-rational-team-concert-client-slow]

-   [Performance Troubleshooting](PerformanceTroubleshooting)

##### External links: [external-links]

-   Eclipse 3.6.2:
    <http://www.eclipse.org/downloads/packages/release/helios/sr2>
-   Install TPTP with Update Manager:
    <http://wiki.eclipse.org/Install_TPTP_with_Update_Manager>
-   Profiling an application in stand-alone mode using Rational
    Application Developer or Rational Software Architect for WebSphere:
    <http://publib.boulder.ibm.com/infocenter/radhelp/v8r5/index.jsp?topic=2Forg.eclipse.tptp.platform.doc.user2Ftasks2Fteprofsa.htm>
-   Java Application profiling with TPTP:
    <http://www.eclipse.org/articles/Article-TPTP-Profiling-Tool/tptpProfilingArticle.html>
-   How can you tell what is the exact cause of the slow response of the
    product?:
    <http://www-01.ibm.com/support/docview.wss?uid=swg21627067>
-   How to contact IBM support:
    <http://www-01.ibm.com/software/rational/support/contact.html>
-   How to send data to IBM support:
    <http://www.ecurep.ibm.com/app/upload>

##### Additional contributors: Lara Ziosi [additional-contributors-lara-ziosi]

##### Questions and comments: [questions-and-comments]

COMMENT{type="below"
target="ProfileRationalTeamConcertClientForEclipseComments"
button="Submit"}

INCLUDE{"ProfileRationalTeamConcertClientForEclipseComments"}

META:FILEATTACHMENT{name="ProfilingResults2.jpg"
attachment="ProfilingResults2.jpg" attr="h" comment="" date="1361981034"
path="ProfilingResults2.jpg" size="144790" user="lziosi" version="1"}
META:FILEATTACHMENT{name="ProfilingResults1.jpg"
attachment="ProfilingResults1.jpg" attr="h" comment="" date="1361981003"
path="ProfilingResults1.jpg" size="184569" user="lziosi" version="1"}
META:FILEATTACHMENT{name="ImportProfilingFile.jpg"
attachment="ImportProfilingFile.jpg" attr="h" comment=""
date="1361980980" path="ImportProfilingFile.jpg" size="85030"
user="lziosi" version="1"}
