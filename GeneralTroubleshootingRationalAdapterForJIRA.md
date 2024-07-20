META:TOPICINFO{author="dmmckinn" date="1424884353" format="1.1"
version="1.3"}
META:TOPICPARENT{name="IntegrationsTroubleshootingRationalAdapterForJIRA"}

# General Troubleshooting Rational Adapter for JIRA [general-troubleshooting-rational-adapter-for-jira]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: Rational
Adapter for JIRA Standard Edition v1.1, Rational Collaborative Lifecycle
Management version 4.0, 4.0.1, 4.0.2, 4.0.3 ENDCOLOR

TOC{title="Page contents"}

This page provides general troubleshooting information for IBM Rational
Adapter for JIRA Standard Edition v1.1.

### Turning on Logging

The administrator needs to add a file in {JIRA-install-root}/conf called
'oslc_log4j.properties'.

For example:

On Microsoft Windows: c:\Program Files
(x86)\Atlassian\JIRA\conf\oslc_log4j.properties

On Linux: /opt/Atlassian/JIRA/conf/oslc_log4j.properties

Information on how to enable logging can be found at: Using JIRA logging
with the JIRA adapter

### Using the IBM Support Assistant Lite (ISALite) utility to collect diagnostic information

-   ISALite can be used to collect information about your JIRA Adapter
    environment.
-   It is bundled with JIRA adapter plugin and can be found in
    {JIRA-adapter-install-directory}/support/ directory.
-   Steps to run ISALite and collect the output can be found at:
    -   Gathering diagnostic information for the JIRA adapter

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   Troubleshooting the JIRA adapter
-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.KotTontranakwong [additional-contributors-main.kottontranakwong]

##### Questions and comments: [questions-and-comments]

COMMENT{type="below"
target="GeneralTroubleshootingRationalAdapterForHPALMComments"
button="Submit"}

INCLUDE{"GeneralTroubleshootingRationalAdapterForHPALMComments"}
