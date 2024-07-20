META:TOPICINFO{author="atiacobo" date="1440106834" format="1.1"
reprev="1.1" version="1.1"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandClearQuest"}

# Why do many ClearQuest record types appear when associating records and some do not even have the OSLC Links Package applied? DKGRAY Authors: Main.IntegrationsTroubleshootingTeam Build basis: None. [why-do-many-clearquest-record-types-appear-when-associating-records-and-some-do-not-even-have-the-oslc-links-package-applied-dkgray-authors-main.integrationstroubleshootingteam-build-basis-none.]

ENDCOLOR

TOC{title="Page contents"}

When you are associating ClearQuest (CQ) change requests to CLM
artifacts, the ClearQuest search menu appears. Sometimes all the record
types in the schema will be available. This can be confusing to users.

In ClearQuest 8.0.0.3, a configuration setting was added in
cqrest.properties to filter the non-OSLC-Package-Enabled record type.
This is a product defect - APAR PM54995. For more information, see
<http://www-01.ibm.com/support/docview.wss?uid=swg1PM54995>.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.AntoinetteIacobo [additional-contributors-main.antoinetteiacobo]
