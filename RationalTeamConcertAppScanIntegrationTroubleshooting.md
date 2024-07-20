META:TOPICINFO{author="sbagot" date="1432745003" format="1.1"
version="1.6"}
META:TOPICPARENT{name="IntegrationsTroubleshootingRTCandRationalAppScan"}

# How do I troubleshoot issues that occur when using AppScan with RTC? [how-do-i-troubleshoot-issues-that-occur-when-using-appscan-with-rtc]

DKGRAY Authors: Main.AbrahamSweiss Build basis: IBM Rational Team
Concert 4.0.x and later ENDCOLOR

TOC{title="Page contents"}

This page provides information to help troubleshoot issues encountered
when using IBM Rational AppScan with IBM Rational Team Concert (RTC).

## INITIAL ASSESSMENT

### Prerequisites

-   Ensure that the integration is configured correctly (see:
    RationalTeamConcertIntegrationsAppScan).
-   If the issue appears to be related to RTC, then you can take AppScan
    out of the picture by connecting directly to the jts/admin page.
    Doing this will help validate whether or not RTC is configured
    correctly.
-   If the issue is reproducible by connecting directly to RTC, then the
    issue would lie in RTC and may not be related to AppScan.
-   If the issue is not reproducible, then the issue will most likely
    lie in AppScan.

## Recommended data gathering and subsequent analysis steps

The majority of issues reported with this integration have historically
been related to the LDAP configuration, thus the investigation will
primarily focus in that area.

Collect the log and trace output detailed in the AppScan section of
MustGather: Integration issues when using Rational Team Concert

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: None [additional-contributors-none]
