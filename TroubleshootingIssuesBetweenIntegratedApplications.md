META:TOPICINFO{author="sbagot" date="1432735994" format="1.1"
version="1.4"} META:TOPICPARENT{name="IntegrationsTroubleshooting"}

# Troubleshooting issues between integrated applications [troubleshooting-issues-between-integrated-applications]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: The
Rational solution for Collaborative Lifecycle Management (CLM) 4.x
ENDCOLOR

TOC{title="Page contents"}

This page provides some initial troubleshooting steps necessary to help
diagnose issues encountered when using integrated applications.

## Initial investigation and analysis

Before you begin, ensure that you have properly setup the integration
for both integrated products per the instructions documented in the IBM
Rational Collaborative Lifecycle Management (CLM) Knowledge Center. See:
Overview of CLM integrations.

### Double check the basics

-    Can the linked application resolve the hostnames of the Jazz
    servers (in an enterprise topology, for instance, if IBM Rational
    Quality Manager (RQM) and Jazz Team Server (JTS) have different
    hostnames), can it resolve all of the Jazz topology names? Check
    this with nslookup. Then check in the other direction, can the Jazz
    servers find your application?

<!-- -->

-    Can they ping the Jazz servers and can the Jazz server ping them?

<!-- -->

-    Are the timestamps between the servers synchronized? Timestamps are
    part of the oAuth dance and having a mismatch will break it.

<!-- -->

-    Is a Pop Up Blocker blocker enabled, preventing popups?

<!-- -->

-    Is a network Proxy preventing access?

<!-- -->

-    Is browser security impacting the situation? If it is seeing
    internal servers as Internet, try them as trusted or intranet. Has a
    shield icon appeared beside the URL indicating a security issue?

<!-- -->

-    Are all applications on https or is it a mix of http and https?
    That can result in the browser blocking mixed content. See for
    example Why is the Select Requirement Collection from DOORS dialog
    appearing blank in Rational Quality Manager?

<!-- -->

-    Are the URLs entered for rootservices documents correct? For Jazz
    applications, they follow a standard of GET failed with http code
    401 and invalid_consumer_key when adding a service link type in
    Rational DOORS

<!-- -->

-    Clear the jazz proxy cache - Go to
    <https://host:9443/ccm/proxy/logout> (replace host/ccm with correct
    hostname/port/context root). It should give a blank page. This
    clears the session to the remote application. Then the next attempt
    to access it will ask for a login.

### Data Matters

Is the issue specific to a particular artifact or collection? Are there
non alpha numeric characters that might be breaking it? If this is the
case, it is likely a defect and should be addressed by Rational Support
or logged on jazz.net.

### Logs

Take a look in the Jazz application log (ccm.log for Rational Team
Concert (RTC), qm.log for RQM, rm.log for Rational Requirements Composer
(RRC) or DOORS Next Generation (NG), dm.log for Design Manager). Check
if the other application has a log.

### Enable HTTP tracing

Tracing tools such as Firebug (an addon for Mozilla Firefox), Microsoft
Internet Explorer Developer Tools (from Internet Explorer 9 onwards, as
we need network tracing) or Google Chrome Developer Tools can help.
Mozille Firefox Install the Firebug addon from getfirebug.com Microsoft
Internet Explorer 9+ Developer tools can be started by clicking F12 or
from the Tools menu Google Chrome Developer tools can be started from
the Tools menu

Regardless of the browser or tool, what you are mostly interested in is
the Network tracing. At their most basic, OSLC integrations are sending
and receiving HTTP GET, PUT, or POST requests. If something is failing,
it is likely one of those you want to trace. Is there an error code in
there you are not seeing in the logs? Is there something different in a
request which works and one which fails?

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.MaeveOReilly [additional-contributors-main.maeveoreilly]
