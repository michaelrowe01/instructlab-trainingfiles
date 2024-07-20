META:TOPICINFO{author="paulellis" date="1678200735" format="1.1"
version="1.23"} META:TOPICPARENT{name="DeploymentMigratingAndEvolving"}

# Moving an Engineering Workflow Management (EWM) SCM component to a new EWM SCM server DKGRAY Authors: Main.ArunSriramaiah Main.PaulEllis Main.SheejaVijayan [moving-an-engineering-workflow-management-ewm-scm-component-to-a-new-ewm-scm-server-dkgray-authors-main.arunsriramaiah-main.paulellis-main.sheejavijayan]

Build basis: Engineering Workflow Management 6.0.6.1, 7.0.x ENDCOLOR

TOC{title="Page contents"}

This article relates to Engineering Workflow Management (EWM) Source
Control Management (SCM) components. EWM was formerly known as Rational
Team Concert.The products were renamed during the ELM 6.0.6.1/7.0
timeframe. For more information, see [Renaming the IBM Continuous
Engineering
Portfolio](https://jazz.net/blog/index.php/2019/04/23/renaming-the-ibm-continuous-engineering-portfolio)

Newly introduced in the ELM 6.0.6.1 release, there are now tworepotool
commandsto refactor your components across different server
repositories.

**Note:**

**1.** This method of moving Components, is meant for 1-time import of
components only. Once a component is imported into the destination
repository, the next import of the same import with newer baselines will
not be accepted during the import.

**2.** In case distributed SCM is enabled in the source repository
(during the export of the component), this needs to be enabled in the
destination repository too.

## Introduction New capabilities were introduced in the 6.0.6.1 release of EWM. This document explains about the uses of these new capabilities and their importance.

**Component Export\Import**

The repotools-ccm command for the CCM server now supports

-   Exporting a component and the contained SCM information into an
    export file.
-   Importing a component and the contained SCM information from an
    export file.

These new capabilities can be used to migrate a component from one
server to another with history references without the need to use
distributed SCM.

The scmExportComponent command exports the contents of source-control
management (SCM) components to a .tar file. The scmImportComponent
command imports the contents of an exported .tar file. The EWM SCM CLI
functions that are described here must be run by a user with
administrative privileges.

This section outlines the process of migrating an ELM SCM component to a
new server. It provides step-by-step instructions.

**Supported Use Cases**

The new capabilities supports the following use cases:

\* Populating a new server with an EWM SCM components content and
history \* Migrating SCM data to another server. \* Database reduction:
migrate SCM content to a new server and remove it from the original
server to rebalance database sizes \* Refactoring: Separate the SCM data
to a different server due to product closure or geographical
repositioning \* Creating a pre-production Jazz environment with real
data \* Setting up a second CCM server only for SCM/Build

**Important considerations**

-   The initial replication can be very long-running. You can run in non
    business hours (resource-intensive activity).
-   Issues running export\import commands with derby database, It will
    support derby in a network mode.
-   This document was tested by using DB2 11 enterprise database.
-   This document is applicable to all supported databases see link [CLM
    6061 System
    Requirements](https://jazz.net/wiki/bin/view/Deployment/CLMSystemRequirements6061)
    to system requirements and works when you export from one database
    vendor to another.

## Part 1 - Export the component (Server-A)

The scmExportComponent command exports the contents of a database,
scoped to a set of SCM components, to a .tar file.

The exported .tar file only contains data that is only a part of the
specified SCM components and is not a full database export. You can
import the .tar file onto a different server.

[ Use the scmExportComponent command
](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/r_scmExportComponent.html)
to export the contents of SCM components to a .tar file.

Before you import components, ensure that they do not exist on the
server already. All components in the archive are imported together. The
following data is included in an exported component archive:

\* Component \* Contained baselines \* History \* Change sets \* Files
and folders that are modified by change-sets in the component, and the
content that is associated with these files. \* Version identifiers,
item permissions, and custom attributes for any files and folders that
are part of the export. \* Contributor information for all users who
create or modify any exported item.

The following data is not included in an exported component archive:

-   The current state of the component in the workspace or stream, and
    the history of operations done in a stream or workspace. Before you
    export, create baselines to record the current state of any notable
    streams or workspaces.
-   Snapshots are not included, but the individual baselines under the
    component are included.
-   Baseline hierarchies are not included, but the individual baselines
    that make up the hierarchy under the component are included.

**UseCase**

Repository tools command to export SCM components

[ Use the scmExportComponent command
](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/r_scmExportComponent.html)

The export command requires a component UUID. To determine the UUID of
the component use the EWM web browser or use the EWM SCM Command Line
command.

Use "command prompt" for Windows operating systems. For multiple
operating systems or for operating systems other than Windows, use
"command line."

**Example**

Open a command prompt and enter the following command:

cd C:\Program Files\IBM\JazzTeamServer\server\\

**repotools-ccm.bat -scmExportComponent
components=\_iIfDAEKSEd2A5aJWEO8dbA,\_pN8RYPi-Ed2J16MAqQXG5g
toFile=exportComponents.tar**

Open a command prompt and enter the following command: cd
/opt/IBM/JazzTeamServer/server/

**./repotools-ccm.sh -scmExportComponent
components`_iIfDAEKSEd2A5aJWEO8dbA,_pN8RYPi-Ed2J16MAqQXG5g toFile`./exportComponents.tar**

The command can also be used for multiple components. Example:

BR

**Export Command Output:**

BR

## Additional fix in 7.0 & prechecklist for Import command

-   Component import with new contributors does not work with OIDC SSO,
    fixed in EWM 7.0 version.

If scm component import contains new contributors and the server is
configured to use OIDC single sign on, then the import will fail while
attempting to create the contributors in the JTS

<https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.viewWorkItem&id=489373>

-   Component import with new contributors does not work if the JTS is
    offline ( Ensure that JTS is online) , fixed in EWM 7.0 version.

When performing an offline component import, if we have new contributors
then we will fail to make calls to the JTS to create the users and
import will fail.

<https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.viewWorkItem&id=489374>

**Note: Check latest ifix for the 6061 version, if it's back-ported.**

## Part 2 - Import the component (Server-B)

\*Use the scmImportComponent command to import the contents of an
exported source-control management (SCM) component .tar file into a
database.

[Repository tools command to import SCM
components](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/r_scmImportComponent.html)

All data in the previously exported SCM component .tar file is imported
together. Components being imported must not previously exist on the
server.

-   Imported components are initially owned by the default Admin user
    and are in an archived state. An administrator must unarchive the
    component and set the owner to an appropriate process area or
    contributor before users can access it.
-   Imported files and folders with permissions set to a context that
    does not exist on the server are reassigned to the Admin user. When
    you import components onto a new server, the permission context
    (that is, project area) might not exist.
-   Custom attributes are controlled by the project area that owns the
    component.
-   Custom attributes of the component that is imported to a new server
    are retained. But users cannot set new attributes unless they are
    configured in the project area that owns the component.

**Command Example: EWM 6061**

Open a command prompt and enter the following command:

cd C:\Program Files\IBM\JazzTeamServer\server\\

**repotools-ccm.bat -scmImportComponent fromFile=exportComponents.tar**

Open a command prompt and enter the following command:

cd /opt/IBM/JazzTeamServer/server/

**./repotools-ccm.sh -scmImportComponent
fromFile=./exportComponents.tar**

**Import Command Output:**

BR

**Command Examples for: EWM 70, 701, 702 and 703**

The scmImportComponent behaviour has changed from 7.0 (seedefect 489374)
where the 'importContributors' option has been introduced.

This option needs to be used when the archive file has new contributor
records. Contributor information has to be imported first before other
information like components, baselines, changesets, etc. Because while
importing component or change-set information, owner info needs to be
set, and running the import command with the 'importContributors' option
first makes new owner info available in the server later on.

In short, when the archive file has new contributors information then
the import command should be run twice, once with the
'importContributors' option first and again without the
'importContributors' option.

**New usage: : EWM 70, 701, 702 and 703**

\*./repotools-ccm.sh-scmImportComponent
fromFile`"exportComponents.tar" importContributors repositoryURL=https:/// adminUserId=* adminPassword`

**./repotools-ccm.sh-scmImportComponent
fromFile`"/root/exportComponents.tar" repositoryURL=https:/// adminUserId`
adminPassword=**

Note: The output of the scmImportComponent command with the
'importContributors' option which shows that the
component/baselines/changesets are imported (but shows the time taken is
0ms which basically means they are skipped from getting imported) and a
work item should be raised to fix the output message.

<https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.viewWorkItem&id=544008>

## Part 3 - Set the migrated component into the project Scope in Server-B

Imported components are initially owned by the default Admin user and
are in an archived state. An administrator must unarchive the component
and set the owner to an appropriate process area or contributor before
users can access it.

1\) Explicitly list archived components by using the SCM list components
command.

Lists the components that are associated with a workspace, stream, or
repository.

[list
components](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.team.scm.doc/topics/list_components.html&scope=null)

Example: **code** is a component that is migrated from Server-A to
Server-B

C:\IBM\RTCEE42\scmtools\eclipse\>

**scm.exe list components -r <https://RTC6061:9443/ccm> -u Admin -j
--visibility archived**

BR

**Note:** In some cases it is seen that this command does not return any
results. You can retrieve the required value under the ITEM_ID of the
component - using the repodebug utility and query the SCM.COMPONENT
table, and look for the component name in the NAME_COL column.

2\) Change the visibility scope of the component

For example, : Private or Public, depending on what you want to set as
visibility.

**Note: If the alias is not working, use the components UUID in the
command executions.**

Set the attributes of items.

[set
attributes](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.team.scm.doc2Ftopics2Fset_attributes.html)

C:\IBM\RTCEE42\scmtools\eclipses

**scm.exe set attribute --component \_4_gg0ON8EemgH41uLVD-BQ
--visibility public -r <https://db2:9443/ccm> -u Admin**

Password (Admin @ <https://db2:9443/ccm>): The component property was
set.

BR

3\) Change the owner scope for the component

For Example,..: Project Area or Team Area, depending on what you want to
set as owner).

Note: If the alias is not working, use the components UUID in the
command executions..

Set the attributes of items

[set
attributes](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.team.scm.doc2Ftopics2Fset_attributes.html)

C:\IBM\RTCEE42\scmtools\eclipse\>

**scm.exe set attribute --component \_4_gg0ON8EemgH41uLVD-BQ --ownedby
Demo -r <https://db2:9443/ccm> -u Admin**

Password (Admin @ <https://db2:9443/ccm/>): The component property was
set.

BR

## Post Checklist: 1) Check that the imported component is under project scope. \*Note: Imported component can be listed using the following command. \* C:\IBM\RTCEE42\scmtools\eclipse\>

**scm.exe list components -r <https://db2:9443/ccm> -u Admin -j**

Password (Admin @ <https://db2:9443/ccm>):

BR

2\) Add the component into the stream and verify the following details.

-   Component
-   Contained baselines
-   History
-   Change sets
-   Files and folders that are modified by change-sets in the component,
    and the content that is associated with these files.
-   Version identifiers, item permissions, and custom attributes for any
    files and folders that are part of the export.
-   Contributor information for all users who create or modify any
    exported item.

BR

### Cleaning up and reclaiming space

[Database Growth - Strategies for minimizing the growth of repository
databases](https://jazz.net/wiki/bin/view/Deployment/DatabaseGrowth),
Main.RosaNaranjo describes how to perform the final step.

In Engineering Workflow Management (EWM), the following items contribute
greatly to database growth if not kept in check:

-   Build results
-   Work item attachments
-   Binary content in SCM as versioned content

You can refer the following articles and presentations that are written
on this topic:

\* [Help! My EWM Database is getting
big!](https://trfeeney.wordpress.com/2014/12/09/help-my-rtc-database-is-getting-big/)
\* [Follow-up to Help! My EWM Database is getting
big!](https://trfeeney.wordpress.com/2019/10/08/follow-up-to-help-my-rtc-database-is-getting-big/)
\* [Deleting data in Engineering Workflow Management](DataDeletionRTC)
\* [Reducing the size of the Engineering Workflow Management repository
database](https://jazz.net/library/article/1459) \* [Deleting content in
EWM](https://jazz.net/library/article/1006)

##### Related topics: [Database Growth](DatabaseGrowth), [Deleting data in Engineering Workflow Management](DataDeletionRTC) [related-topics-database-growth-deleting-data-in-engineering-workflow-management]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.PaulEllis, Main.RosaNaranjo [additional-contributors-main.paulellis-main.rosanaranjo]

META:FILEATTACHMENT{name="1SupportedUsecase.png"
attachment="1SupportedUsecase.png" attr="h" comment="1SupportedUsecase"
date="1580906570" path="1SupportedUsecase.png" size="1520882"
user="arusrira" version="1"}
META:FILEATTACHMENT{name="2ExportCommand.png"
attachment="2ExportCommand.png" attr="h" comment="Phase1Export"
date="1580906862" path="2ExportCommand.png" size="542552"
user="arusrira" version="1"}
META:FILEATTACHMENT{name="3ExportOutput.png"
attachment="3ExportOutput.png" attr="h" comment="3ExportOutpout"
date="1580906911" path="3ExportOutput.png" size="230582" user="arusrira"
version="1"} META:FILEATTACHMENT{name="1ImportCommand.png"
attachment="1ImportCommand.png" attr="h" comment="iImportCommand"
date="1580913566" path="1ImportCommand.png" size="260616"
user="arusrira" version="1"}
META:FILEATTACHMENT{name="2ImportOutput.png"
attachment="2ImportOutput.png" attr="h" comment="2ImportOutput"
date="1580913604" path="2ImportOutput.png" size="512550" user="arusrira"
version="1"} META:FILEATTACHMENT{name="ArchivedComp.png"
attachment="ArchivedComp.png" attr="h" comment="ArchivedComp"
date="1580915370" path="ArchivedComp.png" size="157784" user="arusrira"
version="1"} META:FILEATTACHMENT{name="VisblityComp.png"
attachment="VisblityComp.png" attr="h" comment="VisblityComp"
date="1580915403" path="VisblityComp.png" size="77360" user="arusrira"
version="1"} META:FILEATTACHMENT{name="ChangeOwner.png"
attachment="ChangeOwner.png" attr="h" comment="ChangeOwner"
date="1580915895" path="ChangeOwner.png" size="78737" user="arusrira"
version="1"} META:FILEATTACHMENT{name="CompList.png"
attachment="CompList.png" attr="h" comment="CompList." date="1580916237"
path="CompList.png" size="174569" user="arusrira" version="1"}
META:FILEATTACHMENT{name="EclipseClient.png"
attachment="EclipseClient.png" attr="h" comment="EclipseClient"
date="1580916506" path="EclipseClient.png" size="472138" user="arusrira"
version="1"}
