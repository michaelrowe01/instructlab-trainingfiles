META:TOPICINFO{author="sbagot" date="1432735115" format="1.1"
version="1.4"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandClearQuest"}

# Why is my ClearQuest Import failing with error CRRTC0290E? [why-is-my-clearquest-import-failing-with-error-crrtc0290e]

DKGRAY Authors: Main.IntegrationsTroubleshootingTeam Build basis: IBM
Rational Team Concert 4.x and later, Rational ClearQuest 7.0.1 or later
(as identified as supported version) ENDCOLOR

TOC{title="Page contents"}

## Initial Assessment

### Symptoms

You are about to import ClearQuest records with the ClearQuest import
Wizard from an archive into a Project Area based on a custom process
template. The records are not imported but the following error appears:
"Could not create work item from bug : CRRTC0290E: The work item cannot
be saved because the work item's type is not configured correctly at the
project level".

### Impact / Scope

This issue is affecting all ClearQuest Imports that are not mapped
correctly to a corresponding work item type in the target project area
when using the ClearQuest Import Wizard

## Data gathering and subsequent analysis steps

-   The exported process from the Project Area
-   The zipped file that contains the ClearQuest records
-   The mapping file used for the import

## Possible Solutions

\* Make sure that the record type of the exported ClearQuest record is
part of the xml The tag is called Every xml file with a ClearQuest
record has the following tag

has to be replaced with a record type like Defect

-   Make sure that the record type from the xml file is mapped to a
    corresponding Workitem type in the process used for the Project
    Area.

\* Make sure that the id is correct. The mapping rule looks like:
targetId="com.ibm.team.workitem.attribute.workitemtype"\>

has to be replaced with a record type like Defect. has to be replaced
with the correct id from the process the target Project Area is based
on. To find the id:

1.  Open the target Project Area in RTC Eclipse client
2.  On the tab Process Configuration expand Project Configuration -
    Configuration Data - Work Items - Types and Attributes
3.  Select the target work item type and check the ID.

Still need help troubleshooting your integrations issue? Refer to
ClearQuest Import Wizard Limitations and known Problems

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: \* ClearQuest Knowledge Center Topic: Migrating Rational ClearQuest records to Work Items [external-links-clearquest-knowledge-center-topic-migrating-rational-clearquest-records-to-work-items]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.ElisabethCarbone [additional-contributors-main.elisabethcarbone]

META:FILEATTACHMENT{name="workitem_id.jpg" attachment="workitem_id.jpg"
attr="h" comment="" date="1402321156" path="workitem_id.jpg"
size="122869" user="dmmckinn" version="1"}
