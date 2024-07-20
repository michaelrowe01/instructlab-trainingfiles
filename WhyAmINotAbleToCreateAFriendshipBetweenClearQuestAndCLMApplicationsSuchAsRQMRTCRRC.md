META:TOPICINFO{author="sbagot" date="1432735640" format="1.1"
version="1.19"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandClearQuest"}

# Why can't I create a friendship between Rational ClearQuest and CLM applications, such as Rational Quality Manager, Rational Team Concert, and Rational Requirements Composer? [why-cant-i-create-a-friendship-between-rational-clearquest-and-clm-applications-such-as-rational-quality-manager-rational-team-concert-and-rational-requirements-composer]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: The
Rational solution for Collaborative Lifecycle Management (CLM) 4.x,
Rational ClearQuest 7.1.2.x ENDCOLOR

TOC{title="Page contents"}

This page covers things to check if errors occur when you create the
friendship and project association between IBM Rational ClearQuest (CQ)
and the Jazz products for Open Services for Lifecycle Collaboration
(OSLC) based integrations, such as Rational Team Concert (RTC) or
Rational Quality Manager (RQM).

## Initial assessment

### Symptoms

-   You are following the instructions to create a friendship between
    the Rational Collaborative Lifecycle Management (CLM) applications
    and Rational ClearQuest (CQ) and are getting errors.

There are two parts to the setup, establishing an OSLC relationship
between the CLM application and CQ Web (application-wide settings) and
associating a CLM project area with a CQ connection (for example: a
specific instance of a schema and user database; in CQ terms, a dbset).

### Impact/scope

-   The friendship is done as an initial setup. Project area
    associations with CQ artifact containers can be made as these
    projects are created.

### Before you begin

When creating a friendship between Jazz and CQ, there are specific
requirements that must be adhered to or the setup can fail. These are
listed in the setup instructions in the information centers, yet
frequently are the cause when errors occur:

1\. Browser pop-ups are not enabled.

-   If browser pop-ups are not enabled, the integration will fail.
    Explore your browser's Help on the topic of pop-ups since there can
    be more than one type of configuration.

**Note**: If you began the setup configuration process and at some later
point discovered popups were disabled, clear your browser cache and
begin the process again. Bogus information might have been stored, and
some browsers may not display any subsequent message or the message may
be unclear. Similarly, if you discover that you have tried to enter the
wrong administrative user name or password (for example: you entered the
CQ user for Jazz or the Jazz admin for CQ), clear the cache and start
again.

2\. Stable URLs for CQ Web and Jazz.

-   You must use the Jazz public URL.
-   You should be using public host names rather than aliases or
    proxies. Note that although URLs may resolve, they may not be the
    stable URL.
-   Any attempt to change the CQ Web URL at some point after the
    integration is setup and data is created will require a server
    rename operation.
-   There are specific requirements for matching http/https between the
    servers depending on your CQ version. The integration will fail if
    the requirements are not met, so this is an important check. See [A
    new security feature in CQ Web may restrict HTML content from
    displaying
    correctly](http://www.ibm.com/support/docview.wss?uid=swg21588252)
    and other technotes linked within this topic for complete details.

3\. Ensure clocks of all hosts are synchronized.

-   They can be no more than a few minutes apart or the integration will
    fail.
-   While the Jazz Team Server (JTS) has a setting to configure a
    Network Time Protocol (NTP) server, CQ does not. You must check that
    these are synchronized manually.

4\. Connectivity

-   Ensure that you can browse to CQ Web by using a browser installed on
    the Jazz Server using the stable URL. Similarly, ensure you can
    browse to the CLM application by using a browser installed on CQ
    Web.

5\. Correct configuration entries.

-   The discovery URL format must be followed exactly as described in
    the information center. You should be clear on exactly which Jazz
    instance, CQ Web, and dbset you are configuring. The format is:
    `https:///cqweb/oslc/repo//discovery`, where is the name of your CQ
    Web server and is the name of your CQ schema repository.

<!-- -->

-   Use the following URL to view the connection profiles (dbset names)
    on the CQ Web Server: `http:///cqweb/oslc/repo` The resulting XML
    file will list all the possible dbsets registered on the CQ Web
    Server under the tag `Repository` and then the
    `ServiceProviderCatalog` title tag, for example: `7.0.0`. These
    strings are case sensitive.

6\. Other considerations

-   Are you using load balancing with CQ Web?

Make sure that every CQ Web is using a consistent configuration for the
Jazz Server. Refer to [ ClearQuest Web server in a load-balanced
deployment should not be used as an OSLC
provider](http://www.ibm.com/support/docview.wss?uid=swg21579391) and [
Configuring OSLC Cross-Server Communication links in a load balanced
ClearQuest Web environment for additional configuration
details](http://www.ibm.com/support/docview.wss?uid=swg21579499)

## Possible errors and causes:

-   Failed to read matching artifact container catalog resource:

Unable to load URL:
/qm/proxy?uri=<http://Mycqweb/oslc/repo/&dojo.preventCache> =xxxx Status
500 Variation: Unable to load URL:
/qm/proxy?uri=<http://Mycqweb/oslc/repo/> Status 500 Cause: the clocks
between ClearQuest and the Jazz Server are not synchronized.

-   Failed to read friends resource:

Unable to load URL:
/jazz/proxy?uri=[https://xxxx:xxxx/jazz/friends](https://xxxx:xxxx/jazz/friends),
Status: 0 Cause: the user is accessing the Jazz server with an URL that
does not start with what is specified in the Public URI Root.

##### Related topics: None [related-topics-none]

##### External links: \* None [external-links-none]

##### Additional contributors: Main.AntoinetteIacobo [additional-contributors-main.antoinetteiacobo]

META:TOPICMOVED{by="lziosi" date="1367569240"
from="Deployment.WhyCantISetupMyOSLCIntegration"
to="Deployment.WhyAmINotAbleToCreateAFriendshipBetweenClearQuestAndCLMApplicationsSuchAsRQMRTCRRC"}
