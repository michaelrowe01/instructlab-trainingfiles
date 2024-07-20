META:TOPICINFO{author="sbeard" date="1422035663" format="1.1"
version="1.18"} META:TOPICPARENT{name="DeploymentAdminstering"}

# Configuring and tuning IBM HTTP Server (IHS) [configuring-and-tuning-ibm-http-server-ihs]

DKGRAY Authors: Main.HongyanHuo, Main.GrantCovell Build basis: CLM 3.x,
CLM 4.x ENDCOLOR

TOC{title="Page contents"}

This article explains some of the strategies for configuring and tuning
IHS.

## Introduction

IHS is based on the Apache HTTP Server. In the [CLM standard
topologies](https://jazz.net/library/article/820), IHS also functions as
reverse proxy server. A reverse proxy server provides a layer of
indirection for backend application servers, and can provide load
balancing at the http server tier to other application servers.

This article introduces some monitoring and tuning techniques.
Generally, tuning is not always necessary as the default IHS settings
are designed to handle reasonable load. However symptoms of poor
performance include IHS crashing and CPU thrashing.

|  |
|----|
| Diagnosing and troubleshooting IHS server problems may be out-of-scope for most Jazz administrators. These tasks may be better performed by Web server administrators. Do not make changes to IHS configurations without making backups first. Do not make changes to IHS configurations without consulting your Web server administrators. |

## The IHS directives and what they mean

The tunable IHS directives live in the `httpd.conf` in the `\config`
directory. Always backup the `httpd.conf` file before making a change
(rename it to `httpd.conf.bak` for example). After making changes, you
will need to restart IHS for changes to take effect. All numeric values
must be positive, non-zero integers.

### **Multi-Processing Module (aka MPM)** directives

`MaxClients` is a key factor that defines how much load IHS can serve.
`MaxClients` is not the same as maximum number of users served.
`MaxClients` is a soft limit to control the simultaneous connections or
threads. Changing this value doesn't mean IHS will deny new or
additional user requests. Requests over this value will be put in queue
until there are available threads.

-   `MaxClients` is recommended to be set lower than 2000 for a single
    IHS server. Monitor the number of **bsy** threads (see "section IHS
    error logs" below) to determine the peak of the simutanous
    connections based on your typical load, and then add 25 as a secure
    factor to set the value of MaxClients.

<!-- -->

-   Note that on Windows there is no `MaxClients` directive and that
    `ThreadsPerChild` is used instead.

`ServerLimit`, `ThreadsPerChild`, `ThreadsLimit` along with `MaxClients`
affect the capability of IHS in handling loads. To tune these, start
with `ThreadsPerChild` and consider platform, plugin, SSL and caching. A
higher `ThreadsPerChild` can benefit the WebSphere plugin, but the
trade-off compensates CPU for SSL.

-   `ThreadsPerChild` default is 25.

<!-- -->

-   `ThreadsLimit` should equal `ThreadsPerChild`.

<!-- -->

-   `ServerLimit` should be equal to `MaxClients` divided by
    `ThreadsPerChild` rounded to nearest integer. Ideally, change
    `MaxClients` so that it equals `ServerLimit` multiplied by
    `ThreadsPerChild` without any fractions. If `ServerLimit` multiplied
    by 25 is greater than the amount of available RAM, lower
    `MaxClients` and readjust `ServerLimit`.

`StartServers`, `MaxSpareThreads`, `MinSpareThreads` determine how IHS
reacts when load varies.

-   `MinSpareThreads` should not exceed the value of 25 or 10 of
    `MaxClients`.

<!-- -->

-   `MaxSpareThreads` can be increased in step with `MaxClients`.

<!-- -->

-   `StartServers` is best to leave at default of 1.

`MaxRequestsPerChild` can remain at the default of 0.

### Other considerations

Modules that are not in use should be unloaded to reduce IHS memory
footprint.

\|Optimizing KeepAlive, KeepAliveTimeOut and MaxKeepAliveRequests can be
very helpful to improve the performance as well. Plugin parameters may
also be taken into account for fine-tuning, if the WebSphere web server
plugin modules are configured.\|

|  |
|----|
| Note that the tuning highly depends on the actual server environment and the load. Use the suggested values above as a starting point and follow the tuning practices to adjust them. Please refer to the documents in the section 'External link' for more details. |

## IHS server settings

### System resources

On a linux system be sure that there are enough user processes allowed.
You may need to increase the `max user processes` setting using this
command:

ulimit -u 65536

Also decrease the stack size. 512 MB is sufficient for CLM apps: \#add
this line into the envvar file under folder /conf ulimit -s 512

## Tools and tips

### IHS error logs

Ordinarilly, IHS logging is enabled by default. In test systems, you may
wish to disable the access_log to save disk space. To do this comment
out the following in the httpd.conf file

CustomLog logs/access_log common

However, for production environment, consider the options for
effectively managing log files
<http://httpd.apache.org/docs/2.2/logs.html>.

IHS error logs live in the `/logs` directory. The frequency they are
written to is controlled by the `mpmstats` module which is automatically
enabled in IHS version 8.x. To obtain more accurate statistics, set the
`ReportInterval` to a small value. For instance, set it to 60 (seconds).

Sample output of `mpmstats`:

\[Mon Jun 04 14:32:00 2012\] \[notice\] mpmstats: rdy 88 bsy 187 rd 0 wr
5 ka 160 log 0 dns 0 cls 22

In the above example `bsy 187` indicates the busy threads and should be
less than the MaxClients value.

Monitoring the log files closely by watching for **\[alert\]**,
**\[warn\]** and **\[error\]** messages can give you hints on what goes
wrong, for example:

\[Thu May 10 15:10:34 2012\] \[alert\] (11)Resource temporarily
unavailable: apr_thread_create: unable to create worker thread

The above message shows that IHS hits a resource limit and cannot create
more threads. If the MPM modules are configured correctly (see section
"The IHS directives and what they mean" above), it may be often remedied
by reducing MaxClients or increasing the maximum user processes on the
system. This link provides handful information for IHS trouble-shooting:
<http://publib.boulder.ibm.com/httpserv/ihsdiag/errorlog.html>

### Server status

Runtime monitoring is possible through the IHS server-status page,
located at `http://your_server_name/server-status`

Enable the IHS server-status page by adding an `allow` directive to the
corresponding section of the `httpd.conf`.

Apache.org makes a sample page available at
<http://www.apache.org/server-status>.

### Useful commands on Linux

Watch open IHS processes with this command:

ps -ylC httpd

Sort by process size:

ps -ylC httpd --sort:rss

Sort by parent process:

ps -ylC httpd --sort:ppid

Check an individual process with child threads

pstree -cp

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

\* IBM article [Using IBM HTTP Server 6.1 and later diagnostic
capabilities with
WebSphere](http://publib.boulder.ibm.com/httpserv/ihsdiag/WebSphere61.html)
\* IBM article on tuning IHS: [IHS performance
tuning](http://publib.boulder.ibm.com/httpserv/ihsdiag/ihs_performance.html)
\* IBM technote: [Tuning IHS to maximize the number of client
connections to WebSphere Application
Server](http://www-304.ibm.com/support/docview.wss?uid=swg21167658) \*
IBM IHS Q&A: [IHS Questions and
Answers](http://publib.boulder.ibm.com/httpserv/ihsdiag/questions.html#IHSV8)
\* IBM Infocenter [IHS v8
Infocenter](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/index.jsp?topic=2Fcom.ibm.websphere.ihs.doc2Finfo2Fihs2Fihs2Fwelcome_ihs.html)
\* Apache.org article: [Apache
tuning](http://httpd.apache.org/docs/current/misc/perf-tuning.html) \*
IBM developerWorks article: [Proxy server versus the HTTP plug-in:
Choosing the best WebSphere Application Server workload management
option](http://www.ibm.com/developerworks/websphere/techjournal/1010_pape/1010_pape.html)

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="ihsdefaults.jpg" attachment="ihsdefaults.jpg"
attr="h" comment="IHS defaults" date="1375132066" path="ihsdefaults.jpg"
size="39798" user="gcovell" version="1"}
META:FILEATTACHMENT{name="mpmstats.jpg" attachment="mpmstats.jpg"
attr="h" comment="" date="1375198155" path="mpmstats.jpg" size="11428"
user="gcovell" version="1"} META:FILEATTACHMENT{name="serverstatus.jpg"
attachment="serverstatus.jpg" attr="h" comment="" date="1375199715"
path="serverstatus.jpg" size="75297" user="gcovell" version="1"}
META:FILEATTACHMENT{name="mod_status.jpg" attachment="mod_status.jpg"
attr="h" comment="mod_status" date="1375201107" path="mod_status.jpg"
size="28813" user="gcovell" version="1"}
META:FILEATTACHMENT{name="ps.jpg" attachment="ps.jpg" attr="h"
comment="process" date="1375202108" path="ps.jpg" size="63947"
user="gcovell" version="1"} META:TOPICMOVED{by="sbeard"
date="1385831914" from="Deployment.TuningIBMHTTPServer"
to="Deployment.ConfiguringAndTuningIBMHTTPServer"}
