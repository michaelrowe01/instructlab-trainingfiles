META:TOPICINFO{author="sbagot" date="1432735698" format="1.1"
version="1.11"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandClearQuest"}

# Troubleshooting Guide: Rational ClearQuest Synchronizer DKGRAY Authors: Main.IntegrationsTroubleshootingTeam [troubleshooting-guide-rational-clearquest-synchronizer-dkgray-authors-main.integrationstroubleshootingteam]

Build basis: Rational ClearQuest Synchronizer 7.x and later, as
supported by Rational Team Concert (RTC) 4.x and later ENDCOLOR

TOC{title="Page contents"}

## Introduction

This guide will provide links to resources you can use to troubleshoot
issues with the IBM Rational ClearQuest (CQ) Synchronizer (previously
known as ClearQuest Connector). Below are categories for most types of
problems and this diagram shows the basic components of the integration.
This diagram also shows the logs for each component. In general, you
will need to consult the logs when issues arise. Later in the Guide,
there is information on how to control the logging levels.

## 1. Configuration

Configuration issues occur if you have not met the prerequisites or
something has changed in the system which can include: user accounts,
permissions, licenses, schema changes, and hook code. Use this checklist
to identify areas that you may need to re-configure if you are setting
it up for the first time, or areas you need to check for changes if the
Sychronizer was formerly working: Configuration checklist

Verify the external repository connection Open a Web browser and enter
the CQ Gateway URL as entered in the External Repository Connection Info
field. If correct, this should display the CQ Connector Gateway status
page. If this is not displayed, verify that the CQ Gateway has been
started or that the URL is correct.

## 2. Synchronization Rules

Synchronization Rules map fields between the external object (for
example, CQ record) and a Jazz item (for example, work item) and
describes the transformations.

There are many guidelines and examples for creating these in the IBM
Rational Collaborative Lifecycle Management Knowledge Center. Here is an
article with additional instructions:
<https://jazz.net/wiki/bin/view/Main/WritingSyncRules>. Typically, when
you save synchronization rules, you will see errors or messages to help
troubleshoot any problems. Also, consult the IBM Rational Team Concert
(RTC) logs for errors.

Simplify new synchronization rules: To ensure synchronization is not
failing due to field mapping errors, you may want to simplify your
synchronization rules as much as possible. To do this, map only the
fields which are required fields in CQ or Rational Team Concert. Once
synchronization works with these fields, you may add more field mappings
to your synchronization rules, testing synchronization along the way.

## 3. Outgoing Sync - RTC WIs --\> CQ records

Verify the Jazz Server can reach the CQ Gateway by opening a
synchronization rule in the RTC Client. If you see the error
`CRRTC4690E: The "External type" filed could not be populated. Name: BAD RULE`,
then the Jazz server can not reach the gateway.

Gateway logs can provide more details. For example, the log could show
it contacting CQ but records are not making it in to CQ. In this case,
you will need to review the CQ logs. Or CQ tracing may be needed. Search
for ClearQuest Web "MustGather" technotes for information on the
location of the logs for your ClearQuest version and consult the CQ
logs. Typically, this includes CQ hooks tracing.

## 4. Inbound - CQ records --\> RTC WIs

In this case, CQ records fail to make it into RTC. To troubleshoot,
consult the CQ Gateway log and the RTC or Rational Quality Manager (RQM)
log.

## 5. Conflicts

Conflicts can occur when two users make nearly simultaneous changes to a
ClearQuest record and its corresponding work item. Sometimes, you may
manually resolve the conflict by selecting the appropriate value.

Check Synchronization status in the RTC Client.

Messages in the RTC Client can provide steps for how to resolve
conflicts.

##### Related topics: [Deployment web home](DeploymentWebHome), Rational Team Concert and Rational ClearQuest integration cookbook [related-topics-deployment-web-home-rational-team-concert-and-rational-clearquest-integration-cookbook]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.AntoinetteIacobo [additional-contributors-main.antoinetteiacobo]

META:FILEATTACHMENT{name="cq-synchronizer-troubleshooting-diagram.jpg"
attachment="cq-synchronizer-troubleshooting-diagram.jpg" attr="h"
comment="" date="1406831509"
path="cq-synchronizer-troubleshooting-diagram.jpg" size="37011"
user="dmmckinn" version="1"}
