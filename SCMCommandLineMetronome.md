META:TOPICINFO{author="sbeard" date="1368542832" format="1.1"
version="1.7"} META:TOPICPARENT{name="RTCClientPerformance"}

# SCM command line metronome [scm-command-line-metronome]

DKGRAY Authors: PerformanceTroubleshootingTeam Build basis: RTC 4.0.x
ENDCOLOR

TOC{title="Page contents"}

To measure the execution time of the SCM command line application, you
can activate debug options on the command line.

## Preparing

1 Create a file called ".options" containing this text:
com.ibm.team.filesystem.cli.core/debug=true
com.ibm.team.filesystem.cli.core/debug/trips=true 1 Save the file in the
directory where you installed the scm command line, for example:
C:\IBM\TeamConcert401\scmtools\eclipse

### Tracing

1 Launch the command scm -debug .options \[scm commands and options\] 1
Example: C:\IBM\TeamConcert401\scmtools\eclipse\>scm -debug .options
list projectareas -r <https://ibm-oprsurvfat7.ams.nl.ibm.com:9443/ccm/>
Start VM: C:\IBM\TeamConcert401\jdk\jre/bin/java.exe ..... Debug
options: <file:/C:/IBM/TeamConcert401/scmtools/eclipse/options.txt>
loaded Time to load bundles: 3 Starting application: 377 (1000)
"CCMProject1" Service Trip Statistics: Interface/method Calls Time
IRepositoryRemoteService 1 24ms fetchOrRefreshItems 1 24ms
IQueryService........... 1 19ms queryItems 1 19ms -- Total time in
service calls: 43ms

##### Related topics: [related-topics]

-   [Why is the RTC Client slow?](RTCClientPerformance)
-   [Performance Troubleshooting](PerformanceTroubleshooting)

##### External links: [external-links]

-   None

##### Additional contributors: Main.LaraZiosi [additional-contributors-main.laraziosi]

##### Questions and comments: [questions-and-comments]

COMMENT{type="below" target="SCMCommandLineMetronomeComments"
button="Submit"}

INCLUDE{"SCMCommandLineMetronomeComments"}
