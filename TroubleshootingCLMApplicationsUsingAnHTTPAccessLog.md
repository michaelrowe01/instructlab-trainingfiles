META:TOPICINFO{author="bsilverm" date="1493668691" format="1.1"
version="1.9"} META:TOPICPARENT{name="DeploymentTroubleshooting"}

# Troubleshooting CLM Applications Using an HTTP Access Log DKGRAY Authors: Main.ErikMats, Main.BenjaminSilverman [troubleshooting-clm-applications-using-an-http-access-log-dkgray-authors-main.erikmats-main.benjaminsilverman]

Build basis: CLM 4.0.x ENDCOLOR

TOC{title="Page contents"}

This page discusses how to use an HTTP access log for troubleshooting
CLM applications. Strategies, scripts and examples are given.

## HTTP Access Log

Reverse proxies and application servers can often be configured to
provide an access log, which is simply a list of all invocations managed
by that server. Each log line is placed in the log at the time the
request finishes.

Unlike other logs which generally only contain warnings and errors, an
access log contains detailed information on timing and successful
invocations, generally including most cross-server communication.

### Data in an HTTP Access Log?

A typical access log lists:

-   Who made the request - usually by IP
-   Timestamp of the request
-   HTTP Method of the request (POST/GET/PUT/DELETE ...)
-   path of the request
-   Status returned by the application server/proxy (200, 404, 302, 500,
    400, 403 ...)
-   Size of data returned by the proxy
-   Duration of the request, often in microseconds.

For example, this log example shows:

9.1.2.3 - - \[25/Sep/2015:03:41:52 +0100\] "POST
/jts/auth/j_security_check HTTP/1.1" 302 0
(mod_was_ap22_http.c/-2/handler) clm.example.com:9445 242789

-   The machine at IP 9.1.2.3 made a POST request for
    /jts/auth/j_security_check at 03:41:52.
-   The application server/proxy took 0.243 seconds to return a status
    302, returning a body of 0 bytes.
-   The invocation was handled by clm.example.com:9445, which must be
    where JTS resides.

9.52.3.24 - - \[25/Aug/2015:03:41:57 +0100\] "GET
/ccm/web/com.ibm.team.process.web/ui/internal/images/manage-proj_co.gif
HTTP/1.1" 200 1435 (mod_was_ap22_http.c/-2/handler) clm.example.com:9444
2578

-   The machine at IP 9.52.3.24 made a request for a .gif image at
    03:41:57.
-   It took 0.0003 seconds to return the image which was 1435 bytes in
    size.
-   The invocation was handled by clm.example.com:9444, which must be
    where CCM runs.

### What is usually NOT included in an HTTP Access Log?

User names or other authentication data is generally not included.

The full path including server names is generally not included.

The duration is often not included, but can then be deduced from the
order of entries. See below.

Size of data uploaded or in headers.

Cross-server communication that does not go via the reverse proxy. For
example, single sign-on data for distributed WebSphere servers.

### When to use an HTTP Access log for troubleshooting

Once you know you have a problem to solve, an access log can help answer
important questions, such as:

-   WHAT/WHERE is the problem

<!-- -->

-   WHEN does the problem occur

<!-- -->

-   What is the EXTENT of the problem

## Examples

### Using an access log to rule out a server-side performance problem in a CLM application

If you know the URL or timestamp, a simple grep can give you all
durations for a given operation.

### What happens at the end of a timeout?

You can search around the end of a long-running operation, to see what
else happens at that same time.

### How long does it take to get an error?

Does an error 500 always occur at certain durations? Nice round regular
numbers often indicate timeouts. The exact number may give an important
clue what kind of timeout occurred. Changing a timeout from e.g. 900s to
903s can tell you conclusively which timeout occurred.

### What was the last action by the same user before a hang?

Scenario: You may find that the invocation "configurationUpdates" would
sometimes hang. In order to figure out what this corresponds to, you may
identify the IP behind each of these hangs, then search the file
backwards for that IP to see what was the last thing invoked from that
same client. Excerpt from log:

9.23.22.11 - - \[26/Sep/2015:12:59:41 +0100\] "GET
/jts/service/com.ibm.team.repository.service.internal.IServerConfigurationRestService/serviceConfiguration?implementationClassName=com.ibm.team.repository.service.jts.internal.mailer.MailerService
HTTP/1.1" 200 1411 4678 ... 9.23.22.11 - - \[26/Sep/2015:12:59:45
+0100\] "POST
/jts/service/com.ibm.team.repository.service.internal.IServerConfigurationRestService/configurationValidation
HTTP/1.1" 200 260 5874 9.23.22.11 - - \[26/Sep/2015:12:59:47 +0100\]
"POST
/jts/service/com.ibm.team.repository.service.internal.IServerConfigurationRestService/configurationUpdates
HTTP/1.1" 500 536 600053138

This shows that saving e-mail options on JTS failed after 10 minutes
(600053138 microseconds) with a status 500. You can see this because the
log shows that the last page that was loaded before the
configurationUpdate invocation, is the e-mail settings page. You can
generally use Firebug traces on your web browser to test which page
corresponds to each URL.

### Do all invocations fail?

Once you know a path that yields a certain error, you can grep for that
path and see whether the error is consistent for one client, for all
clients, and so forth.

### What else fails?

You may notice a certain function fails with a timeout. It may make
sense to search for other errors in the same timeframe.

### Was the server even involved in a problem?

Example: A user reported as perceived slowness in a CLM application when
creating a link to another application. Studying the access logs you can
check: a/ whether the CLM server or client ever contacted the other
server and whether that server responded in a timely fashion. b/ Whether
that server was waiting for an invocation to the CLM server. This can
help rule out an entire server in a root cause investigation.

## Variations and Challenges

### No duration in access log

If no duration is listed in the access log, entries before and after the
interesting ones can help answer how long an operation took.

In this example, the second line occurs approximately 15 minutes out of
order, returning a status 500.

The more other entries that occur in order, the more likely this
particular entry matches the surrounding timing exactly.

We know for sure that the invocation occurred at 06:40:45. You can tell
for sure that it returned AFTER 06:56:20 (timestamp of the line before),
so it must have taken *at least 935s*. Given that the following lines
occur in order, it is *unlikely* that the operation took much more than
935s. Unfortunately if there is no duration in the file we cannot get
much more exact than this.

9.1.15.132 - - \[25/Sep/2015:06:56:20 +0100\] "POST
/ccm/service/com.ibm.team.build.internal.common.ITeamBuildRequestService
HTTP/1.1" 200 804 9.1.54.136 - - \[25/Sep/2015:06:40:45 +0100\] "POST
/ccm/service/com.ibm.team.filesystem.common.IFilesystemService HTTP/1.1"
500 607 9.1.128.28 - - \[25/Sep/2015:06:56:20 +0100\] "POST
/ccm/service/com.ibm.team.build.internal.common.ITeamBuildService
HTTP/1.1" 200 1714 9.1.128.28 - - \[25/Sep/2015:06:56:20 +0100\] "POST
/ccm/service/com.ibm.team.repository.common.service.IQueryService
HTTP/1.1" 200 422 9.1.128.28 - - \[25/Sep/2015:06:56:20 +0100\] "POST
/ccm/service/com.ibm.team.build.internal.common.ITeamBuildRequestService
HTTP/1.1" 200 782

### Identifying application server IP addresses from an access log

You can use the strings /jts/proxy, /ccm/proxy and so forth to identify
the IP of each application server in a distributed environment. This is
crucial for cross-server communications issues.

9.5.4.3 - - \[25/Aug/2015:03:41:53 +0100\] "GET
/jts/discovery?type=http3A2F2Fjazz.net2Fxmlns2Ffoundation2F1.02FLicenseInfoExpiration&scope=includeExternal
HTTP/1.1" 200 319 18740 9.23.2.42 - - \[25/Aug/2015:03:41:53 +0100\]
"GET
/ccm/proxy?uri=https3A2F2Fwww.example.com2Fjts2Fdiscovery3Ftype3Dhttp253A252F252Fjazz.net252Fns252Fui252Fentry2523JazzTeamServerHome
HTTP/1.1" 200 330 33211

An invocation of /ccm/proxy causes the CCM server (with apparent IP
9.5.4.3) to immediately forward the request to the /jts context.
Studying the timestamps and durations you can also see that one
invocation encloses the other.

### When to delete access logs

Access logs can quickly become quite large. A filled up file system is
no use to anyone. So consider rolling over and archiving logs.

### Multi-threaded access logs

It is likely possible to have multi-threaded access logs. Assumptions
about log file order no longer hold then.

### Logs from multiple reverse proxies logs with the same application servers.

Multiple reverse proxies may be used for load balancing. This poses some
challenges:

-   If you merge both logs, how do you avoid getting the timestamps out
    of order, in particular if the log is missing a duration?
-   "less" or "grep" needs to be applied to both files.

## Reading access logs using "less"

In order to read an access log you may need a text editor/viewer that
can easily display hundreds of megabytes of text. I find "less" (from
Cygwin or Linux) is quite useful. Most important shortcuts:

-   g - beginning of file

<!-- -->

-   G - end of file

<!-- -->

-   / - search forward

<!-- -->

-   ? - search backward

So to find an invocation that I know occurred at 11:42 and ran for some
minutes, I would:

1\. Invoke less access_log

2\. Hit G to go to end of file

3\. Type ? 2015:11:42 to find the LAST invocation with that timestamp.

## Example scripts

### Invocations lasting longer than 10s

For a log file of this format, run grep -E "\[0-9\]{8,}\$" access_log to
find all invocations running longer than 10s. This filters for any row
where the last column is a number with 8 digits or more.

9.23.22.11 - - \[26/Sep/2015:12:59:47 +0100\] "POST
/jts/service/com.ibm.team.repository.service.internal.IServerConfigurationRestService/configurationUpdates
HTTP/1.1" 500 536 600053138

### Isolate timestamp, URL and duration

cut -d ' ' -f 4,7,13 \< access_log \| tr ' ' '\t'

Example output, which can be polished and fed to Excel to create pivot
or scatter graphs: \[25/Aug/2015:03:42:01 /jts/view-history 487891

## How to enable access logs

### IBM HTTP Server

The access log is enabled by default using the **CustomLog** directive
in the httpd.conf. To add time in microseconds or seconds, use **D** or
**T** in the **LogFormat** directive as outlined in [this
article](https://www.ibm.com/developerworks/library/co-websphere-access-feature/#Tip201).

### WebSphere Application Server

To enable access logging for WebSphere Application Server, refer to the
section titled **NCSA Access Logging** in [this
article](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.nd.multiplatform.doc/ae/utrb_httperrlogs.html?lang=en).

### Apache Tomcat The Tomcat server.xml has access logging commented out by default. To change this, open the server.xml under /server/tomcat/conf/ and uncomment the following section at the bottom of the file:

You can also add **T** to the pattern to log the time in seconds. Note
the difference between **t** included above which logs the date/time of
the request and **T** which logs how long the request took to complete
(in seconds). Refer to [this
article](https://tomcat.apache.org/tomcat-7.0-doc/config/valve.html#Access_Logging)
for more details on the Tomcat access logging.

### Websphere Liberty Profile (6.0.1)

Refer to [this
article](http://www-01.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_http_accesslogs.html)
for instructions on modifying the server.xml to include access logging.
An modified server.xml is included in the attachments at the bottom of
this article. Refer to the section in the file titled "HTTP ACCESS
LOGGING" for an example.

### Squid caching proxy

Refer to [this
article](http://www.squid-cache.org/Doc/config/access_log/).

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

<https://jazz.net/wiki/bin/view/Deployment/ContentCachingProxyJazzSCM>

##### External links: [external-links]

META:FILEATTACHMENT{name="server.xml" attachment="server.xml" attr=""
comment="Example Liberty server.xml with access logging enabled"
date="1493668690" path="server.xml" size="2682" user="bsilverm"
version="2"} META:TOPICMOVED{by="erikmats" date="1443559352"
from="Deployment.TroubleshooitngCLMApplicationsUsingAnHTTPAccessLog"
to="Deployment.TroubleshootingCLMApplicationsUsingAnHTTPAccessLog"}
