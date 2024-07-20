META:TOPICINFO{author="sbagot" date="1432736596" format="1.1"
version="1.6"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandDOORS"}

# How to debug CLM integrations with DOORS [how-to-debug-clm-integrations-with-doors]

DKGRAY Authors: Main.MaeveOReilly Build basis: CLM 4.x and later
ENDCOLOR

TOC{title="Page contents"}

This topic provides a general strategy for debugging Open Services for
Lifecycle Collaboration (OSLC) based integrations with IBM Rational
DOORS.

## Double check the basics

-   Can the DOORS Web Access (DWA) server resolve the hostnames of the
    Jazz server (in an enterprise topology, for instance, if IBM
    Rational Quality Manager (RQM) and Jazz Team Server (JTS) have
    different hostnames), can it resolve all of the Jazz topology names?
    Check this with \*nslookup \*. Then check in the other direction,
    can the Jazz server find DWA?
-   Can the DWA servers ping the Jazz servers and vice versa?
-   Are the timestamps between the servers synchronized? Timestamps are
    part of the oAuth dance and having a mismatch can break it.
-   Is a Pop Up Blocker blocking stuff?
-   Is a network Proxy preventing access?
-   Is browser security impacting? If it is seeing internal servers as
    Internet, try them as trusted or intranet.
-   Microsoft Internet Explorer MUST work for accessing any application
    you wish to link to DOORS. If it does not work in Internet Explorer,
    it is unlikely it will work in DOORS.
-   Are the URLs entered for rootservices documents correct? For Jazz
    applications, they follow a standard of /admin page. For example,
    for RQM:

For DOORS, it is **/dwa/public/rootservices**. Here again, we must be
consistent. Match the protocol, hostname and port to the URL seen for an
object, either in DOORS or DWA:

## Check for known issues

Known issues are listed in the Integration Troubleshooting section of
the Deployment wiki.

## Double check the DWA configuration

In particular in versions prior to 9.5.1, ensure the DOORS Database and
DWA have been configured to use the exact same protocol, port, and
hostname. See technote Technote 1612615 for more details.

## Data Matters

Is the issue specific to a particular DOORS module, view, object or a
particular artifact on the Jazz side? Are there non alpha numeric
characters that might be breaking it? If this is the case, it is likely
a defect and should be addressed by Rational Support or logged on
jazz.net.

## Logs

The DWA festival logging is very good in particular for OSLC requests.
Take a look at them for any errors or messages - **DWA Install
Dir/server/festival/logs**.

It is possible to activate more logging by renaming **DWA Install
Dir/server/festival/config/festival-log4j.xml.support** to
**festival-log4j.xml** and restarting DWA.

Broker logging can be activated by renaming **DWA Install
Dir/broker/conf/log4j.properties.support** to **log4j.properties** and
restarting DWA.

Interop level logging is the most detailed and cryptic. It is generally
only useful to Rational support. Activate it by adding additional
parameters to the command starting interop: **-loglevel 8 -l
c:\logfile1.txt** See: [How to enable logging for DWA Interoperation
server](http://www-01.ibm.com/support/docview.wss?uid=swg21397464)

Consider also the Jazz application logs. **ccm.log** for Rational Team
Concert (RTC), **qm.log** for RQM, **rm.log** for Rational Requirements
Composer (RRC) or DOORS Next Generation (NG), dm.log for Design Manager.

## Enable HTTP tracing

First consider where the problem is see: is it in a Jazz application or
in DOORS Web Access (DWA) or in DOORS 9 client? If it starts in a DOORS
9 client, is it reproducible in DOORS Web Access? Moving to a web based
application simplifies debugging.

### A. Issue seen in Jazz Application or DOORS Web Access

http tracing tools such as Firebug (an addon for Mozilla Firefox),
Internet Explorer Developer Tools (from Internet Explorer 9 onwards, as
we need network tracing) or Google Chrome Developer Tools can help.

Mozilla Firefox Install the firebug addon from getfirebug.com Microsoft
Internet Explorer 9+ Developer tools can be started by clicking F12 from
the Tools menu Google Chrome Developer tools can be started from the
Tools menu

Regardless of the browser or tool, what we are mostly interested in is
the Network tracing. At their most basic, OSLC integrations are sending
and receiving HTTP GET, PUT, or POST requests. If something is failing,
it is likely one of those we want to trace. Is there an error code in
there we are not seeing in the logs? Is there something different in a
request which works and one which fails?

Some screenshots from Chrome. A Test Plan creates a Requirements
Collection Link to a view in DOORS. Then the Test Plan is saved. Here we
see GET, PUT, POST operations.

In this instance, they all worked, so all give a 200. If we want to look
in more detail, we double click on the request of interest. For
instance, for the final POST this was a Save of the Test Plan. That
operation writes to the View in DOORS so that DOORS is also aware that
the view is linked to a Test Plan.

### B. Issue is seen in DOORS 9

This is a bit trickier. There is little in the way of out of the box
logging and for the most part, DWA will not be used so its logging does
not help. From 9.5.0.1 however, it is possible to use Fiddler which
works like Firebug and Developer Tools.

Install and start Fiddler get it from: <http://fiddler2.com/>. If either
application is using https (this is the default for Jazz applications
and recommended for DWA), under **Tools-Fiddler Options-HTTPS**, check
**Decrypt HTTPS traffic**.

Create two environment variables (right click on \*My Computer \>
Properties \> Advanced \> Environment Variables\*; or just type
environment variable in the Start menu):

<proxy=8888@127.0.0.1> proxy_type=HTTP

Start the DOORS Client. Now all OSLC requests DOORS makes will go
through the proxy defined here and can be seen in Fiddler which can help
track down the particular one which is failing in the same manner as
Firebug.

Remember to delete the environment variables when you are done or DOORS
will not function correctly if Fiddler is not started.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="public-uri1.jpg" attachment="public-uri1.jpg"
attr="h" comment="Public URI" date="1382631227" path="public-uri1.jpg"
size="29862" user="dmmckinn" version="1"}
META:FILEATTACHMENT{name="public-uri2.jpg" attachment="public-uri2.jpg"
attr="h" comment="Public URI" date="1382631251" path="public-uri2.jpg"
size="45664" user="dmmckinn" version="1"}
META:FILEATTACHMENT{name="Requirements-collect-links.jpg"
attachment="Requirements-collect-links.jpg" attr="h"
comment="Requirements Collections Links" date="1382631303"
path="Requirements-collect-links.jpg" size="72949" user="dmmckinn"
version="1"}
META:FILEATTACHMENT{name="Requirements-collect-link-details.jpg"
attachment="Requirements-collect-link-details.jpg" attr="h"
comment="Requirements Collections Link Details" date="1382631332"
path="Requirements-collect-link-details.jpg" size="239117"
user="dmmckinn" version="1"} META:FILEATTACHMENT{name="EVs.jpg"
attachment="EVs.jpg" attr="h" comment="Environment Variables"
date="1382631355" path="EVs.jpg" size="56176" user="dmmckinn"
version="1"}
