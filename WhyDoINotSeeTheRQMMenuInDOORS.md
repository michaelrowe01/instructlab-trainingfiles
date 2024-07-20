META:TOPICINFO{author="sbagot" date="1432736268" format="1.1"
version="1.6"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandDOORS"}

# Why can't I see the RQM menu in DOORS? [why-cant-i-see-the-rqm-menu-in-doors]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: CLM 4.x,
DOORS 9.4 and later as supported ENDCOLOR

TOC{title="Page contents"}

This page covers what to do if you cannot see the IBM Rational Quality
Manager (RQM) menu in IBM Rational DOORS. This is relating to the OSLC
based integration from DOORS 9.4 on-wards. It does not cover the legacy
RQMI interface of DOORS 9.3 and earlier.

## Initial assessment

Has the menu ever been there?

### Symptoms

The RQM menu is missing in Rational DOORS.

### Impact

This impacts all users.

## Possible causes and solutions

-   The RQM menu is only present if the OSLC QM provider, in this case
    Rational Quality Manager, is version 2.0 or higher. It is not there
    for version 1.0 providers. A defect in earlier versions of DOORS may
    have defaulted it to 1.0, but it can be manually set to 2.0. In the
    Remote Services tab of DOORS Database Properties, ensure the OSLC
    version for RQM is set to 2.0. Then open the module again.

<!-- -->

-   In DOORS 9.5, the creation of the collaboration links has been seen
    to not set the OSLC version. How exactly this can happen is
    currently unknown. It can be resolved by recreating the Quality
    Manager collaboration links in File-OSLC-Remote Services. The
    collaboration links are the bottom part of the dialog - typically
    'validated by' for Quality Manager links.

<!-- -->

-   Technote 1611316 [RQM menu does not appear in DOORS and RQM
    integration](http://www.ibm.com/support/docview.wss?uid=swg21611316)

### Defects

PM81110: [Auto-detect option for OSLC Version in Register Server dialog
defaults to 1.0 while registering a Remote
Service](http://www.ibm.com/support/docview.wss?uid=swg1PM81110)

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: \* [Integrate Rational Quality Manager with Rational DOORS using Open Services Lifecycle Collaboration](https://jazz.net/library/article/1020/) [external-links-integrate-rational-quality-manager-with-rational-doors-using-open-services-lifecycle-collaboration]

-   [How to increase the Rational DOORS Web Access logging
    levels](http://www.ibm.com/support/docview.wss?uid=swg21456938)
-   [How to enable logging for DWA Interoperation
    server](http://www.ibm.com/support/docview.wss?uid=swg21397464)
-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.MaeveOReilly [additional-contributors-main.maeveoreilly]
