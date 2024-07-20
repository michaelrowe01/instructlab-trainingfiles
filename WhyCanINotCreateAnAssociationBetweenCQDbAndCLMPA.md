META:TOPICINFO{author="atiacobo" date="1440108587" format="1.1"
reprev="1.1" version="1.1"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandClearQuest"}

# Why can I not create an association between a ClearQuest database and a CLM Project Area (RQM, RTC, RRC)? DKGRAY Authors: Main.IntegrationsTroubleshootingTeam Build basis: None. [why-can-i-not-create-an-association-between-a-clearquest-database-and-a-clm-project-area-rqm-rtc-rrc-dkgray-authors-main.integrationstroubleshootingteam-build-basis-none.]

ENDCOLOR

TOC{title="Page contents"}

Review the troubleshooting topic "Why can't I create a friendship
between Rational ClearQuest and CLM applications, such as Rational
Quality Manager, Rational Team Concert, and Rational Requirements
Composer?" to make sure basic requirements for the integration are met.

Is the database missing from the list? See the above topic, item 5 for
the query you can run to navigate to the registered data. You will need
to investigate further with the ClearQuest administrator as to why it is
not available for the connection.

Use a browser debugging tool such as Firebug to detect an errors or
messages that may not show up in the UI. Typically, there is a response
here to a call that will reveal more information on the failure which
you can use to search for known issues.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.AntoinetteIacobo [additional-contributors-main.antoinetteiacobo]
