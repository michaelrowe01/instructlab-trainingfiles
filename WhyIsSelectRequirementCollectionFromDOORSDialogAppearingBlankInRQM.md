META:TOPICINFO{author="sbagot" date="1432736472" format="1.1"
reprev="1.5" version="1.5"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandDOORS"}

# Why is the Select Requirement Collection from DOORS dialog appearing blank in Rational Quality Manager? [why-is-the-select-requirement-collection-from-doors-dialog-appearing-blank-in-rational-quality-manager]

DKGRAY Authors: Main.MaeveOReilly Build basis: CLM 4.x and DOORS 9.4 and
later as supported ENDCOLOR

TOC{title="Page contents"}

This topic provides information to help troubleshoot an issue where the
Select Requirement Collection from IBM Rational DOORS is appearing blank
in Rational Quality Manager (RQM).

## Initial assessment

-   Has this ever worked?
-   Have there been browser updates recently?
-   Is RQM on http or https? Is DOORS Web Access on http or https?

----+++ Symptoms

The **Select Requirement Collection** dialog is blank.

----+++ Impact

The impact can vary. It may not be all browsers or all users, as they
have different versions and security settings.

## Possible causes and solutions

Modern browsers have adopted an approach of blocking mixed content by
default. Mixed content is where an application on HTTPS wants to display
content from an application on HTTP. Part of it is encrypted, part of it
is not. The browser wants to protect the user from this situation and
will block the unencrypted (HTTP) content which results in blank
dialogs.

The best and **recommended solution is to run both on HTTPS**. Failing
that, run both on HTTP.

If that is not feasible, on a browser level it is possible to force the
browser to accept mixed content.

### Chrome

A shield icon will appear beside the URL. Click on this and allow it to
run unsafe scripts.

### Microsoft Internet Explorer

A message appears at the bottom of the browser. Click **Show all
content**.

### Mozilla Firefox

A shield icon appears on the top left beside the address. Clicking on
this shield does not currently help. It is necessary to go the Firefox
configuration by typing **<about:config>** in the address bar. Locate
the parameter **security.mixed_content.block_active_content** and set it
to false. It will then stop blocking the mixed content. Be aware that it
will stop blocking it for all websites, not just RQM and DOORS.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]

META:FILEATTACHMENT{name="IEwithHttpHttps.jpg"
attachment="IEwithHttpHttps.jpg" attr="h" comment="" date="1386010897"
path="IEwithHttpHttps.jpg" size="50184" user="dmmckinn" version="1"}
META:FILEATTACHMENT{name="FireFoxwithHttpHttps.jpg"
attachment="FireFoxwithHttpHttps.jpg" attr="h" comment=""
date="1386010914" path="FireFoxwithHttpHttps.jpg" size="105636"
user="dmmckinn" version="1"}
META:FILEATTACHMENT{name="ChromeHttpsHttp.jpg"
attachment="ChromeHttpsHttp.jpg" attr="h" comment="" date="1386011687"
path="ChromeHttpsHttp.jpg" size="50541" user="dmmckinn" version="1"}
