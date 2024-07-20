META:TOPICINFO{author="sbagot" date="1432736221" format="1.1"
version="1.10"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandDOORS"}

# Why can't I create a link from a Rational DOORS object to an artifact in Rational Team Concert or Rational Quality Manager? [why-cant-i-create-a-link-from-a-rational-doors-object-to-an-artifact-in-rational-team-concert-or-rational-quality-manager]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: The
Rational solution for Collaborative Lifecycle Management (CLM) 4.x,
Rational DOORS 9.3 and later ENDCOLOR

TOC{title="Page contents"}

This page covers the basics and the pitfalls when trying to create an
Open Services for Lifecycle Collaboration (OSLC) link from IBM Rational
DOORS to Rational Quality Manager (RQM) or Rational Team Concert (RTC).
This configuration uses backlinks, which means when you create a link in
Rational DOORS, it writes to the artifact in RTC or RQM. The same
happens if you create a link in RTC or RQM, that must write to Rational
DOORS. As the link information is stored in both tools, write access to
both tools is required.

## Initial assessment

### Symptoms

-   A link from RTC or RQM is not created. The effect is, when looking
    at a work item or test case, the related Rational DOORS requirement
    is not seen and no hover over is possible.
-   A backlink from Rational DOORS to RTC or RQM is not created. In this
    case, the link is there in RTC or RQM and the users in those tools
    can see the related requirement. However, the users in Rational
    DOORS have no knowledge that the link exists. For example, they may
    not see that the Rational DOORS requirement is linked to an RTC work
    item or RQM test case.

### Impact/scope/timing

This may impact all users. Or it may be specific to a user or data set.

## Data gathering and subsequent analysis steps

Note if there is any error given.

Check to see if the link is created in either tool.

Check if the link can be created from another object in Rational DOORS.

Check if the link can be created to another artifact in RQM or RTC.

See if it works in the other direction - from RQM or RTC to Rational
DOORS.

See if it works from Rational DOORS Web Access in Microsoft Internet
Explorer.

As a *last step*, Fiddler can be useful to capture the http calls.
Fiddler can be used from Rational DOORS version 9.5.0.1 onwards.

To configure Fiddler, set two system environment variables:

<proxy=8888@127.0.0.1>

proxy_type=HTTP

If RQM or RTC are running in https mode, under **Tools-Fiddler Options**
set it to `Decrypt HTTPS Traffic`. Then look for the GET/POST/PUT
requests and any errors or anomalies.

## Possible causes and solutions

### Defects

There are some defects, particularly in early versions. See:

[ **Using Rational Team Concert integration crashes Rational DOORS when
Japanese Microsoft Office IME is used**
](http://www.ibm.com/support/docview.wss?uid=swg21607173)

[ **CRCRW5065I error creating a link from Rational DOORS Web Access to
Rational Team Concert**
](http://www.ibm.com/support/docview.wss?uid=swg21620565)

### Data

If the issue is specific to a Rational DOORS object or RQM/RTC artifact,
check for characters in the title or description that might break it.
For example, square brackets are known to break linking from DOORS to
RQM in Rational DOORS 9.5.0.1 and earlier.

### Permissions Make sure that the user has write access to the object in Rational DOORS and the artifact in RQM or RTC. In Rational DOORS, the user must be able create an external link. In RQM or RTC, the user must be able create a link of the type selected (for example: implemented by; validated by). Permissions issues could also be temporary due to to locking. See:

[ **Creating a collaboration link from Rational DOORS to Rational Team
Concert results in "The object could not be created" error**
](http://www.ibm.com/support/docview.wss?uid=swg21515748)

### Internet Explorer

Ensure the Rational DOORS client can find the Jazz server in **Microsoft
Internet Explorer**. The Rational DOORS client only runs on Windows;
therefore, Internet Explorer is always installed. Rational DOORS is
hardcoded to use Internet Explorer DLLs to load content from OSLC
providers. As a result, Internet Explorer must work. If, for example,
you want to link Rational DOORS and RTC, it must be possible to login to
RTC from Internet Explorer. This is irrespective of whether Internet
Explorer is the user's default or preferred browser. For Rational DOORS
to work with RTC, Internet Explorer must be able find RTC because if it
cannot, neither can Rational DOORS. It is also important to take note of
any security messages and don't allow IE to block anything.

[ **Creating link to Rational DOORS in RTC results in "Navigation to the
webpage was cancelled" error**
](http://www.ibm.com/support/docview.wss?uid=swg21625320)

[ **Submitting an Implementation Request from Rational DOORS to Rational
Team Concert results in error "HTTP Status 404 error"**
](http://www.ibm.com/support/docview.wss?uid=swg21642961)

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: \* [ **Integrate Rational Quality Manager with Rational DOORS using Open Services Lifecycle Collaboration** ](http://jazz.net/library/article/1020/) [external-links-integrate-rational-quality-manager-with-rational-doors-using-open-services-lifecycle-collaboration]

-   [ **Configure DOORS and Rational Team Concert for globally
    distributed workers**
    ](http://www.ibm.com/developerworks/rational/library/doors-rational-team-concert-globally-distributed-workers/)
-   [ **Configuring Rational DOORS and Rational Team Concert to
    integrate with one another**
    ](http://jazz.net/library/LearnItem.jsp?href=content/articles/rtc/3.0/configuring-doors-and-rtc-to-integrate/index.html)
-   [ **Integrating the Requirements Management application and Rational
    DOORS**
    ](http://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.5/com.ibm.rational.rrm.help.doc/topics/t_config_doors.html)
-   [ **How to increase the Rational DOORS Web Access logging levels**
    ](http://www.ibm.com/support/docview.wss?uid=swg21456938)
-   [ **How to enable logging for DWA Interoperation server**
    ](http://www.ibm.com/support/docview.wss?uid=swg21397464)
-   [ **Fiddler** ](http://fiddler2.com/get-fiddler)
-   [IBM](http://www.ibm.com)

##### Additional contributors: Main.MaeveOReilly [additional-contributors-main.maeveoreilly]
