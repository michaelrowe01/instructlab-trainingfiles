META:TOPICINFO{author="sahilkmansuri" date="1700822684" format="1.1"
version="1.13"} META:TOPICPARENT{name="PerformanceTroubleshooting"}

# Mustgather: Performance problems in Engineering Lifecycle Management [mustgather-performance-problems-in-engineering-lifecycle-management]

DKGRAY Authors: Main.ChristianGlockner, Main.PaulEllis,
Main.BenSilverman ENDCOLOR

TOC{title="Page contents"}

When you are facing a performance problem with ELM that you can't
resolve yourself, you can always reach out to IBM Rational Client
Support for help. When you open a case with IBM Support to report a
performance problem, it's vital that you provide meaningful information
from the start. This must gather document lists the information that we
need from you in order to analyze and resolve your performance problem
as swiftly as possible.

This document follows a specific flow to assist with troubleshooting any
type of performance issue. There is a fantastic must-gather,
[Troubleshooting database problems by using built-in serviceability
features of IBM Collaborative Lifecycle
Management](https://www.ibm.com/support/docview.wss?uid=swg22010123),
which must be highlighted before you proceed. Used in conjunction with
this page, this should add a very specific and granular level of detail
to this wider-ranging and Kepner-Tregoe-style document.

## Problem definition

Before determining which information to collect and send to IBM support
to analyze a performance problem it is important to first understand the
nature of the performance problem. To allow IBM support to help you in
the best way possible, please provide answers to the following
questions:

Which specific actions are slow?

Typically performance problems do not necessarily affect a whole system
but rather just a part of it. It is much easier to analyze a performance
problem that is narrowed down to specific actions rather than one
reported too vaguely (the system is slow). If you do find that indeed
all actions are slow, then do state that.

Which specific actions are not slow

During the analysis of any problem it is useful to understand the scope
of the problem, i.e. which functions of a system are affected but also
which are not affected. This will help narrow down the root cause of the
problem. If you find that there are no actions that are performing
satisfactorily, then please state that.

How slow are the specific actions that are slow?

After understanding the scope of the performance problem, we'll need to
understand the scale of it. This is important because it will partly
determine the business impact caused by the performance problem. What
matters here are specific numbers for instance It takes 30 seconds to
open a Work Item rather than It takes a very long time to open a Work
Item. You may not have tools to measure performance, but a stop watch is
good enough for this purpose.

What performance are you expecting from those actions that are slow?

Now we know how long it takes for certain actions to be carried out, we
also need to understand what performance you are expecting from those
actions. For instance, if performance was fine at some point in the past
and it took 5 seconds to open a Work Item, then those 5 seconds might be
a good number to be expecting. Otherwise, if you are just beginning to
use the system and have no reference performance from the past, provide
us with your expectation. Again, be as specific as you can.

When is the slowness observed?

It is very rare that performance problems affect a system all the time.
Most of the time poor performance is observed at specific times, for
instance during busy periods. In order to understand the timing of the
performance problem, you'll need to collect data over a period of time.
Say you're facing slow performance once a day in that case, you should
note the time of the occurrence (and how long it lasts) for several days
before reporting the problem to us. This will be crucial because it
helps us understand if there is any pattern in how and when the problem
arises, which will, in turn, be very useful for the identification of
the root cause. If performance is indeed poor all the time, then please
state that.

When was the slowness observed for the first time?

If your system was performing satisfactorily in the past and only
recently started showing poor performance it is important for us to
understand when the problem started because we can work with you to
determine what has changed that could lead to the degradation in
performance. If you do not have any date and time that you can pinpoint,
often the date and time of the first official report (for instance via a
ticket) is the best information you will have and we'd be happy to have
that information too.

Who experiences the slowness? Who doesn't?

In many organizations, users of a system or an application are globally
dispersed these days, some may be working from the office while others
may be working from home. Additionally, users typically have varying
degrees of permissions within an application. All of these may have an
impact on the perceived performance of the application. It is therefore
important to understand which specific users are actually experiencing
the slowness, but also which specific users are not. If you find that
only a subset of your users are seeing poor performance while there are
others who are not, we'll work with you to determine what these users
have in common and what distinguishes them from the others but generally
you can help us by letting us know any commonalities or distinctions you
can think of, for instance, geographic location.

Is it getting slower? Is it getting faster?

Depending on the nature of the performance problem you may be seeing a
deterioration of performance over time, or perhaps an improvement.
However, it's perfectly possible that performance remains stable at an
unsatisfactory level. Either way, we'd like to understand what trend you
are observing.

Are you seeing high CPU usage?

If you are experiencing a performance problem and observing constant
high CPU usage at the same time, then most likely the high CPU usage is
the cause of the performance problem. In that case the investigation
will aim to identify the root cause of the high CPU usage and we need
specific bits of information from you. See WhyIsMyCPUSpiking.

## Environment description

Once you understand the nature of the performance problem by answering
the questions above, it is time to collect environmental information:

What architecture/topology are you using?

For the analysis of any performance problem, it is critical to
understand the architecture of the system exhibiting poor performance.
Since CLM supports several different deployment topologies it is
important that you tell us which topology you are using. A proven way of
doing that is to provide us with a diagram that details your
environment, including the database server(s), the application
server(s), any proxy server(s) and clients.

Are you using VMware?

Virtualization is so ubiquitous these days, chances are that you are
using it for hosting your applications. If you are, we will need even
more information which you can provide to us by answering the questions
below. Note: If you are using VMware clustering or DRS please answer the
questions with the totals for all hypervisors in the cluster rather than
for just one hypervisor.

How many sockets are installed in the hypervisor and how many cores are
on each socket? Is hyperthreading enabled on the hypervisor? How much
physical memory is installed on the hypervisor? How many VMs are powered
on on the hypervisor? How many vCPUs are allocated in total to all
powered on VMs on the hypervisor? How much memory is allocated in total
to all powered on VMs on the hypervisor? What reservations (if any) are
in place for vCPUs on the VM in question? What reservations (if any) are
in place for memory on the VM in question?

Operating system and middleware stack

CLM gives you various choices for the underlying middleware. For that
reason, we'd like to understand whether you are using IBM WebSphere
Application Server or Apache Tomcat as your application server, but also
which database backend you are using. Finally, we'd also like to know
which operating system you are using, including bitness (32 vs 64). For
all components we need to know which exact version you are using.

Resource allocation and usage

Whether you are using VMware or not, we need to understand how many
resources are allocated to the application, the middleware and the
database. It is therefore important to answer these questions:

How much total memory is allocated to the machine running CLM or the
database server? If you are using a deployment model where the CLM
applications and the database are spread across multiple servers, please
provide this information for each individual server.

What are the settings concerning minimum and maximum Java Virtual
Machine heap size (Xms and Xms) and nursery space (Xmn) for the
application server running CLM? Again, if you have CLM deployed across
multiple machines (or application servers), please provide this
information for each.

If you are running Linux or UNIX, please provide the output of free -m,
if you are running on Windows, please provide a screenshot of Task
Manager's Performance tab.

Usage model

In order for us to understand whether the allocated resources are
sufficient, we need to have a clear understanding of your usage model.
We therefore need more information (the more specific the better) on the
following:

How many registered users do you have in total? How many licenses do you
have for all of the CLM products? How many concurrently logged in users
do you see on average? What are your users doing in the applications? If
possible work with your users to establish what their day-to-day
activities are. Also try to determine if there is a set of activities
that are only performed at certain times (e.g. end-of-quarter reporting,
end-of-iteration check-ins, etc.).

## Information gathering

In order to analyze the performance problem we need certain bits of
information from you. The list below should help you collect the right
information. [Troubleshooting database problems by using built-in
serviceability features of IBM Collaborative Lifecycle
Management](http://www-01.ibm.com/support/docview.wss?uid=swg22010123)
has just been written and provide new options since 6.0.3 for obtaining
key metrics.

Resource utilization We need to understand the amount of resources that
are available and in use on the system in question. To get that
information, we'd prefer to get a graph created using a monitoring
solution of your choice, showing CPU and memory usage over the course of
at least 24 hours. This will allow us to see if there are any obvious
issues with resource utilization on the system.

Application log files

Application log files will allow us to get a better idea of what the
application is doing at the time when you are observing the performance
problem. It is important that the log files you send to us cover at
least one (ideally more than one) instance of it.

Note: In the paths below, JAZZ_HOME refers to the JazzTeamServer
directory (typically C:\Program Files\IBM\JazzTeamServer on Windows or
/opt/IBM/JazzTeamServer on Linux/UNIX).

Additionally, WAS_HOME refers to the directory where WebSphere
Application Server is installed (typically C:\Program
Files\IBM\WebSphere\AppServer on Windows or /opt/IBM/WebSphere/AppServer
on Linux/UNIX), PROFILE_NAME refers to the name of WebSphere Application
Server profile which the CLM applications are installed in (by default
AppSrv01).

If you are using CLM with Tomcat on Windows, please send us a zip file
of the following directories:

JAZZ_HOME\server\logs JAZZ_HOME\server\tomcat\logs

If you are using CLM with Tomcat on Linux or UNIX, please send us a zip
(or tar) file of the following directories:

JAZZ_HOME/server/logs JAZZ_HOME/server/tomcat/logs

If you are using CLM with WebSphere Application Server on Windows,
please send us a zip file of the following directory:

WAS_HOME\profiles\PROFILE_NAME\logs

If you are using CLM with WebSphere Application Server on Linux or UNIX,
please send us a zip (or tar) file of the following directory:

WAS_HOME/profiles/PROFILE_NAME/logs

Javacore files / WAIT data collection

By looking at javacore files, we will be able to determine which code
the application was executing and what it was potentially waiting for
(for instance a lock, a network resource, etc). These javacore files can
be generated in a number of ways, but the preferred way is using the
WAIT Data Collector.

The WAIT Data Collector can be downloaded from <https://wait.ibm.com/>
(free registration required), and is specific to the operating system.

Once you are observing the performance problem, first identify the
process ID (PID) of the java process belonging to either Tomcat or
WebSphere Application Server. This can be done using ps -ef \| grep java
on Linux or UNIX or using Task Manager on Windows (you will need to add
the PID column to the display columns). In the commands below, this PID
is referred to as PID.

Then start the WAIT Data Collector and let it collect 5 javacore files,
30 seconds apart by running the appropriate command below from a DOS
prompt or terminal in the directory where you extracted the WAIT Data
Collector.

Note: In the commands below, JAZZ_HOME refers to the JazzTeamServer
directory (typically C:\Program Files\IBM\JazzTeamServer on Windows or
/opt/IBM/JazzTeamServer on Linux/UNIX).

Additionally, WAS_HOME refers to the directory where WebSphere
Application Server is installed (typically C:\Program
Files\IBM\WebSphere\AppServer on Windows or /opt/IBM/WebSphere/AppServer
on Linux/UNIX), PROFILE_NAME refers to the name of WebSphere Application
Server profile which the CLM applications are installed in (by default
AppSrv01).

If you are using Tomcat on Windows: waitDataCollector.bat PID
JAZZ_HOME\server --sleep 30 --iters 5 If you are using Tomcat on Linux
or UNIX: ./waitDataCollector.sh --sleep 30 --iters 5 PID If you are
using WebSphere Application Server on Windows: waitDataCollector.bat PID
WAS_HOME\profiles\PROFILE_NAME --sleep 30 --iters 5 If you are using
WebSphere Application Server on Linux or UNIX: ./waitDataCollector.sh
--sleep 30 --iters 5 PID

Once data collection is finished, a zip or tar file will be generated
automatically. Please send this file to us for further investigation.

Verbose Garbage Collection

Performance problems may be caused by excessive garbage collection of
the Java Virtual Machine. To rule this in or out, we need to analyze
verbose garbage collection logs. Verbose garbage collection is disabled
by default and therefore needs to be enabled as follows:

If you are using Tomcat:

Open the file JAZZ_HOME/server/server.startup.bat (Windows) or
JAZZ_HOME\server\server.startup (Linux/UNIX) in an editor and locate the
following line:

export JAVA_OPTS

In the line before that line add the following:

JAVA_OPTS="\$JAVA_OPTS -verbose:gc -Xverbosegclog"

After saving the file, restart Tomcat.

After the restart is complete, verbose GC logs will be generated in
JAZZ_HOME\server (Windows) or JAZZ_HOME/server (Linux/UNIX). The logs
will be named verbosegc.YYYYMMDD.HHMMSS.PID.txt (where YYYYMMDD and
HHMMSS are the date and time and PID is the process ID of the java
process).

These verbose GC logs should be provided to us for further analysis.

Note: If you have configured Tomcat to run as a Windows Service, then
the two Java Options -verbose:gc and -Xverbosegclog need to be added to
the Java Options in the Tomcat Service configuration panel.

If you are using WebSphere Application Server:

Open the WebSphere Integrated Solutions Console, log in, and navigate to
Servers \> Server Types \> WebSphere application server \> SERVER_NAME
(where SERVER_NAME is the name of the application server, by default
server1). Expand Java and Process Management and click Process
definition. On the following page click Java Virtual Machine. In the
text field Generic JVM arguments enter the following:

-verbose:gc -Xverbosegclog

Click OK. At the top of the page click “Save. Restart WebSphere
Application Server.

After the restart is complete, verbose GC logs will be generated in
WAS_HOME\profiles\PROFILE_NAME (Windows) or
WAS_HOME/profiles/PROFILE_NAME (Linux/UNIX). The logs will be named
verbosegc.YYYYMMDD.HHMMSS.PID.txt (where YYYYMMDD and HHMMSS are the
date and time and PID is the process ID of the java process). These
verbose GC logs should be provided to us for further analysis.

##### Additional contributors: Main.RosaNaranjo [additional-contributors-main.rosanaranjo]

##### Related topics: [Performance Troubleshooting](PerformanceTroubleshooting), [Deployment troubleshooting home](DeploymentTroubleshooting) [related-topics-performance-troubleshooting-deployment-troubleshooting-home]
