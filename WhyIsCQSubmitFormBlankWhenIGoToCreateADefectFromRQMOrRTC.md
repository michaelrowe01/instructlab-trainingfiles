META:TOPICINFO{author="atiacobo" date="1440106619" format="1.1"
reprev="1.4" version="1.4"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandClearQuest"}

# Why is the ClearQuest Submit form blank when I go to create a defect from RQM or RTC? DKGRAY Authors: Main.IntegrationsTroubleshootingTeam [why-is-the-clearquest-submit-form-blank-when-i-go-to-create-a-defect-from-rqm-or-rtc-dkgray-authors-main.integrationstroubleshootingteam]

Build basis: Rational ClearQuest, Rational Quality Manager, Rational
Team Concert ENDCOLOR

TOC{title="Page contents"}

This topic page provides information to help you troubleshoot an issue
where the ClearQuest Submit form is blank when you create a defect from
Rational Quality Manager (RQM) or Rational Team Concert (RTC)?

## Possible causes

-   There has been some change that has affected the integration's
    configuration. For example, the CQ database is no longer available
    for the dbset.
-   Browser configuration and security setting changes
-   Server Security changes
-   Defects

## Solution

\* Review the configuration setup information under Section II Parts B
and C Configuring ClearQuest Web (CQWeb) server for CLM integrations in
technote 1433074 **How to configure ClearQuest Web for Collaborative
Lifecycle Management integrations** to ensure that all the steps have
been followed. \* Review changes to the integration configuration, e.g.
a server rename on the CLM side and the changes were not made on the CQ
side; the dbset is no longer registered on the CQWeb Server; the CQ
database schema was upgraded and the CQWeb was not restarted, etc. \*
Check changes to the browser settings, e.g. ensure pop-up blockers are
still disabled; the CLM Server URL is still added to the browser's list
of Trusted Sites or Exceptions; try clearing the browser cache. \* If
using mixed protocols (e.g. CLM uses https and CQ uses http), see
technote 1652291 **RQM ClearQuest OSLC/Bridge Integration: New Defect
window is empty** \* You may be impacted by security changes in CQ
related to mixed protocols. See technote 1614955 **Defect submit form is
blank or says this content cannot be displayed in a frame** for details.
For certain browser versions or server versions, it is not possible to
configure around these security changes. If you are using mixed
protocols, you may be required to configure CQWeb to use https and
implement a CLM server rename. \* You may be impacted by a defect in
CQWeb. See technote 1660756 **ClearQuest Bridge is not working with
Microsoft Internet Explorer 9 (IE9)**

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.AntoinetteIacobo [additional-contributors-main.antoinetteiacobo]
