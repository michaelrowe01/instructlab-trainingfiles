META:TOPICINFO{author="websmith" date="1656093642" format="1.1"
version="1.9"} META:TOPICPARENT{name="DeploymentAdminstering"}

# Workitem Attachment Migration Utility [workitem-attachment-migration-utility]

DKGRAY Authors: Main.SharoonShettykuriyala, Main.TimFeeney Build basis:
6.0.6, 6.0.6.1, 7.0, 7.0.1, 7.0.2 A support case must be opened to
download the utility. ENDCOLOR

TOC{title="Page contents"}

**REDDisclaimer: The Attachment Migration Utility is provided on request
from IBM support. Please open a case to obtain a link to the
download.ENDCOLOR**

Note: The attachment context is stored in the Full Text Index (Lucene).
Reindexing the full text index may restore missing downloads if the
indexing was interrupted while an attachment is moved. The Attachment
Migration Utility can also restore the context (Project Area
association) for attachments.

## Overview

In release 7.0, EWM updated the default access control context for
attachments to be the same as the work item access control to which it
is uploaded. The Attachments Migration Utility is a stand-alone Java
application used to analyze and update attachments in a repository. The
utility is provided to help customers migrate existing attachments to
the new access control model. It will find all work items that do not
have the same access control as the work item linked and update the
access context accordingly.

The utility should be run first in a test environment with a clone of
the production EWM repository. This will allow you to gauge the time it
would take to run the utility in production and to verify that the
commands yield expected results. The utility was developed mainly with
the intent to run as part of an upgrade to 7.x, however, it can also be
run on a 7.x system after upgrade as well.

To download the utility, go to the Attachments section at the bottom of
this page. Download the 'readme.txt' file and the .jar file related to
the version of your ELM system.

## Features

The utility lists all the attachments in the repository that are:

-   linked to multiple work items, with an option to remove multiple
    links (so that an attachment would be owned by one work item only)
-   linked to a work item but are project owned, with an option to
    update the context to that of the work item
-   not linked to any work item, with an option to link to a specified
    work item
-   linked to a deleted work item, with an option to remove the link to
    the deleted work item

The analysis can be scoped to a specific project or all attachments in
the repository.

Using the argument -h or -help provides a detailed help message on the
various supported arguments and commands the utility supports.

The utility displays the size of individual orphaned attachments (not
linked to any work item) as well as the total size for all orphaned
attachments. This information can be used to remove these orphaned
attachments since attachments (especially large ones) are often a large
contributor to EWM repository size.

## Examples

### Help

\$ /bin/java.exe -jar AttachmentMigrationUtility.jar -uri`:/> -u` -pw=
-c=analyzeAndUpdateAttachments -h

Attachments Migrator 1.0 **`============================`** The
Attachments Migrator Utility is a stand-alone Java application used to
analyze attachments in a repository and allow to change the access
context of the attachments to that of the work item it is linked to. It
supports the following commands:

Command: analyzeAndUpdateAttachments Description: Fetch all attachments
in a repository and update based on arguments. List all the
attachments: - which are linked to multiple work items, option to remove
the multiple links. - linked to a work item but are project owned,
option to update the context to that of the work item. - not linked to
any work item, option to link to the specified work item. - have any
attachments linked to a deleted work item, option to remove the link to
the deleted work item.

Argument Reference **`==============`**

Note: Argument values containing whitespace must be enclosed in double
quote characters.

-h, -help Prints this help message.

-uri, -serverUri= The fully qualified URL of IBM Engineering Workflow
Management in the following format: <https://:/> Note: The fully
qualified URL is case sensitive.

-u, -userName= The username for a valid user for the server.

-pw, -password= The password for the username for the server.

-update Update the access context of attachments that are project owned
with the access context of the work item it is associated with, update
the project of the attachment if different than the work item.

-rmDelWILink Remove link to deleted work items from the attachments.

-rmMultiWILinks Remove multiple work links from the attachment.

-addWorkItemId The work item id to associate attachments that are not
associated with any work item.

-deleteAttachmentsNoWI, delAttachmentsNoWI Deletes the attachments which
has no work item associated with it.

-l, -log= \[Optional\] Logs information to the specified log file
(relative file name or absolute file path). Note: The log file is
rotated (deleted) on every execution of the tool.

-p, -project= \[Optional\] Analysis is done only for the specified
project

Example usage: /bin/java.exe -jar AttachmentMigrationUtility.jar -uri=
-u= -pw= -c`analyzeAndUpdateAttachments -l`

### Analyze attachments

\$ /bin/java.exe -jar AttachmentMigrationUtility.jar -uri`:/> -u` -pw=
-c=analyzeAndUpdateAttachments Requested commands are:
\[analyzeAndUpdateAttachments\]. analyzeAndUpdateAttachments started.
Contacting <https://://> User has logged in to <https://://> 0 \[main\]
INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachments linked to multiple work items: 1 1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 1 - license_en.html linked to work item 2253 in project BH
Scrum 1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 1 - license_en.html linked to work item 2254 in project BH
Scrum 1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
analyzeAndUpdateAttachments completed.

\$ /bin/java.exe -jar AttachmentMigrationUtility.jar -uri`:/> -u` -pw=
-c=analyzeAndUpdateAttachments Requested commands are:
\[analyzeAndUpdateAttachments\]. analyzeAndUpdateAttachments started.
Contacting <https://://>... User has logged in to <https://://>

0 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachments with out the same access context as the work item: 1 1
\[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 4 - capture-20200309-1114 (1).png linked to work item 98 in
project JKE Banking (Change Management) 1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachments linked to no work items: 3 1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 5 - Screen Shot 2020-04-15 at 3.02.57 PM.png in project
All_Presentation with size 475.4 KB 2 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 6 - Screen Shot 2020-04-10 at 3.08.50 PM.png in project BH
Scrum with size 95.1 KB 2 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 8 - Screen Shot 2020-04-15 at 3.02.57 PM.png in project BH
Scrum with size 475.4 KB 2 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Total attachments size: 1.0 MB 2 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
analyzeAndUpdateAttachments completed.

\$ /bin/java.exe -jar AttachmentMigrationUtility.jar -uri`:/> -u` -pw=
-c=analyzeAndUpdateAttachments Requested commands are:
\[analyzeAndUpdateAttachments\]. analyzeAndUpdateAttachments started.
Contacting <https://://>... User has logged in to <https://://> 0
\[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachments linked to no work items: 2 1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 3 - landscape-2090495_960_720.jpg in project dbp-scrum with
size 99.7 KB 1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 4 - Screen Shot 2018-08-07 at 5.25.53 PM.png in project Sai
Scrum with size 64.6 KB 1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Total attachments size: 164.4 KB 1 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
analyzeAndUpdateAttachments completed.

### Delete attachments that have no associated work item

\$ /bin/java.exe -jar AttachmentMigrationUtility.jar -uri`:/> -u` -pw=
-c=analyzeAndUpdateAttachments -deleteAttachmentsNoWI Requested commands
are: \[analyzeAndUpdateAttachments\]. analyzeAndUpdateAttachments
started. Contacting <https://://>... User has logged in to <https://://>

0 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Deleting attachment 3 - landscape-2090495_960_720.jpg Delete Attachments
1291 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Deleting attachment 4 - Screen Shot 2018-08-07 at 5.25.53 PM.png Delete
Attachments Exception: CRJAZ6053E To complete the 'Save Attachment'
task, you need these permissions: 'You don't have permission to perform
the following actions: Delete attachment (delete)'
analyzeAndUpdateAttachments completed.

If the user does not have permissions to delete the attachment for that
project then the appropriate error is thrown.

### Update the access context of attachments that are project owned

This will change the access context of the work item that are project
owned to that of the work item; it will update the project of the
attachment if different than the work item.

\$ /bin/java.exe -jar AttachmentMigrationUtility.jar -uri`:/> -u` -pw=
-c=analyzeAndUpdateAttachments -update Requested commands are:
\[analyzeAndUpdateAttachments\]. analyzeAndUpdateAttachments started.
Contacting <https://://>... User has logged in to <https://://> 0
\[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Updating context for attachment 4 - capture-20200309-1114 (1).png to
context of work item 98. 2925 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
2925 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachments linked to no work items: 3 2925 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
2926 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 5 - Screen Shot 2020-04-15 at 3.02.57 PM.png in project
All_Presentation with size 475.4 KB 2926 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 6 - Screen Shot 2020-04-10 at 3.08.50 PM.png in project BH
Scrum with size 95.1 KB 2926 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 8 - Screen Shot 2020-04-15 at 3.02.57 PM.png in project BH
Scrum with size 475.4 KB 2926 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Total attachments size: 1.0 MB 2927 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
analyzeAndUpdateAttachments completed.

### Remove multiple work links from the attachment

\$ /bin/java.exe -jar AttachmentMigrationUtility.jar -uri`:/> -u` -pw=
-c=analyzeAndUpdateAttachments -rmMultiWILinks Requested commands are:
\[analyzeAndUpdateAttachments\]. analyzeAndUpdateAttachments started.
Contacting <https://://>... User has logged in to <https://://> 0
\[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Multiple work item links to attachment 1 - license_en.html ... retaining
link to work item 2253. 1039 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Deleting link: sourceRef 2254: Formal item for CR 92269 - Project A
targetRef: 1: license_en.html. analyzeAndUpdateAttachments completed.

### Associate attachments with no work item association to a specific work item

\$ /bin/java.exe -jar AttachmentMigrationUtility.jar -uri`:/> -u` -pw=
-c`analyzeAndUpdateAttachments -addWorkItemId` Requested commands are:
\[analyzeAndUpdateAttachments\]. analyzeAndUpdateAttachments started.
Contacting <https://://>... User has logged in to <https://://> 0
\[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Linking attachment 5 - Screen Shot 2020-04-15 at 3.02.57 PM.png to work
item 17571. 351 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Linking attachment 6 - Screen Shot 2020-04-10 at 3.08.50 PM.png to work
item 17571. 841 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Linking attachment 8 - Screen Shot 2020-04-15 at 3.02.57 PM.png to work
item 17571. 1594 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
1594 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachments with out the same access context as the work item: 2 1594
\[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
1594 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 6 - Screen Shot 2020-04-10 at 3.08.50 PM.png linked to work
item 17571 in project BH Scrum 1594 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 8 - Screen Shot 2020-04-15 at 3.02.57 PM.png linked to work
item 17571 in project BH Scrum 1594 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
1594 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
1594 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachments in different project than the work item: 2 1595 \[main\]
INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
----------------------------------------------------------------------
1595 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 6 - Screen Shot 2020-04-10 at 3.08.50 PM.png linked to work
item 17571 in project BH Scrum 1595 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
Attachment 8 - Screen Shot 2020-04-15 at 3.02.57 PM.png linked to work
item 17571 in project BH Scrum 1595 \[main\] INFO
com.ibm.team.tap.tools.attachmentsMigrator.AttachmentMigrationUtility -
-----------------------------------------------------------------------
analyzeAndUpdateAttachments completed.

A support case must be opened to access the utility. --
Main.LarrySmith - 2022-03-31

Removed references to out of scope versions. -- Main.LarrySmith -
2022-06-24

## Related topics: [related-topics]

See this
[blog](https://trfeeney.wordpress.com/2019/10/08/follow-up-to-help-my-rtc-database-is-getting-big)
to learn more on how database space can be reclaimed once the unwanted
attachments are deleted from the system.

META:FILEATTACHMENT{name="readme7.0.txt" attachment="readme7.0.txt"
attr="" comment="readme for the Attachment Migration Utility (applicable
to all versions)" date="1585934125" path="readme7.0.txt" size="2387"
user="tfeeney" version="1"}
