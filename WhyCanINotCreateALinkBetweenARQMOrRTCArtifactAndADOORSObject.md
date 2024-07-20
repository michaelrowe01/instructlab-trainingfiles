META:TOPICINFO{author="sbagot" date="1432736890" format="1.1"
version="1.10"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandDOORS"}

# Why can't I create an OSLC link between a Rational Quality Manager or Rational Team Concert artifact and a Rational DOORS object? [why-cant-i-create-an-oslc-link-between-a-rational-quality-manager-or-rational-team-concert-artifact-and-a-rational-doors-object]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: CLM 4.x and
later, Rational DOORS 9.3 and later as supported ENDCOLOR

TOC{title="Page contents"}

This page covers debugging problems creating links from IBM Rational
Quality Manager (RQM) and IBM Rational Team Concert (RTC) to IBM
Rational DOORS. While there is some overlap, issues creating links
**from** Rational DOORS to RQM and RTC will be covered separately. The
link model used with Design Management and IBM Rational Requirements
Composer (RRC) is different and hence that is also not covered here,
though again there is overlap.

## Initial assessment

-   What error is seen?
-   Is it failing for all users?
-   Has it ever worked?
-   Is it failing for all possible link types?
-   In which tool is it failing?

### Symptoms

-   A link from RTC or RQM is not created. The effect is, when looking
    at a work item or a test case, the related Rational DOORS
    requirement is not seen and no hover over is possible.
-   A backlink from Rational DOORS to RTC or RQM is not created. In this
    case, the link is there in RTC or RQM and the users in those tools
    can see the related requirement. However the users in Rational DOORS
    have no knowledge the link exists. For example, they may not see the
    Rational DOORS requirement is linked to a RTC work item or RQM test
    case.

### Impact

This may impact all users

## Data gathering and subsequent analysis steps

[Firebug](http://getfirebug.com) can be useful if no error is seen in
the web browser. It can show what requests it is sending to Rational
DOORS Web Access and what responses are arriving back. Of particular
note is usually the Net tab. Extra logging in Rational DOORS Web Access
will show what requests are arriving and responses are being sent. See
[How to increase the Rational DOORS Web Access logging
levels](http://www.ibm.com/support/docview.wss?uid=swg21456938) and
review the request.log and response.log.

## Possible causes and solutions

### No write access to the Rational DOORS module

The Rational DOORS module is open in exclusive edit mode or a relevant
section is locked or the user does not have access to write to the DOORS
module. Creating a backlink requires write access to the module - it
will fail if this is not possible. For further details see: [Saving an
IBM Rational Quality Manager Test Plan linked to a view in IBM Rational
DOORS fails with "An error occurred while saving links from requirements
provider"](http://www.ibm.com/support/docview.wss?uid=swg21612615).

### Rational DOORS Web Access configuration error

It is critical that the settings in festival.xml's published.url.prefix
match exactly what was set in the Rational DOORS database via dbadmin
-dwaHost/dwaProtocol/dwaPort. See [Saving an IBM Rational Quality
Manager Test Plan linked to a view in IBM Rational DOORS fails with "An
error occurred while saving links from requirements
provider"](http://www.ibm.com/support/docview.wss?uid=swg21612615) and
[Clicking Rational DOORS Implements Requirement link fails with HTTP 404
error in Rational Team
Concert](http://www.ibm.com/support/docview.wss?uid=swg21607827).

### Browser security settings In particular on Internet Explorer it is necessary to ensure the browser is displaying all content and not blocking it. Pop-up blockers can also impact. See also [Creating link to Rational DOORS in RTC results in "Navigation to the webpage was cancelled" error](http://www.ibm.com/support/docview.wss?uid=swg21625320).

### Project association not done on database level

The RQM/RTC project is not associated with the Rational DOORS database,
instead it has only been associated with a view. For links which require
access to a requirements collection, such as in RTC plans or RQM test
plans, they will not be able select a collection and the user cannot
proceed. For further details see [How to select a Rational DOORS View in
Rational Team Concert or Rational Quality
Manager](http://www.ibm.com/support/docview.wss?uid=swg21610453) and
[Only the URIs of Rational DOORS Requirements are shown in Rational Team
Concert Requirements Selection
dialog](http://www.ibm.com/support/docview.wss?uid=swg21620604)

### Defects

There are some defects, particularly in early versions. See:

-   ["Not supported" error when when linking a Rational Quality Manager
    artifact to a Rational DOORS
    object](http://www.ibm.com/support/docview.wss?uid=swg21638674)
-   [PM79924: Adding Collaboration Link type for RQM / RTC fails with
    401
    signature_invalid](http://www.ibm.com/support/docview.wss?crawler=1&uid=swg1PM79924)
-   [PM51166: Unable to Create 'Implemented By' links from RTC when the
    module has a view with a Layout column from Analysis
    Wizard](http://www.ibm.com/support/docview.wss?uid=swg1PM51166)
-   [PM79456: Http 500 error trying to associate a DOORS module with a
    Rational Quality Manager
    project](http://www.ibm.com/support/docview.wss?uid=swg21615699)

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: \* Integrate Rational Quality Manager with Rational DOORS using Open Services Lifecycle Collaboration: <https://jazz.net/library/article/1020/> [external-links-integrate-rational-quality-manager-with-rational-doors-using-open-services-lifecycle-collaboration-httpsjazz.netlibraryarticle1020]

-   Configure DOORS and Rational Team Concert for globally distributed
    workers:
    <http://www.ibm.com/developerworks/rational/library/doors-rational-team-concert-globally-distributed-workers/>
-   Configuring Rational DOORS and Rational Team Concert to integrate
    with one another:
    <https://jazz.net/library/LearnItem.jsp?href=content/articles/rtc/3.0/configuring-doors-and-rtc-to-integrate/index.html>
-   Integrating the Requirements Management application and Rational
    DOORS:
    <http://www.ibm.com/support/knowledgecenter/SSR27Q_4.0.6/com.ibm.rational.rrm.help.doc/topics/t_config_doors.html?cp=SSR27Q_4.0.6>
-   How to increase the Rational DOORS Web Access logging levels:
    <http://www.ibm.com/support/docview.wss?uid=swg21456938>
-   How to enable logging for DWA Interoperation server:
    <http://www.ibm.com/support/docview.wss?uid=swg21397464>

<!-- -->

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.MaeveOReilly [additional-contributors-main.maeveoreilly]
