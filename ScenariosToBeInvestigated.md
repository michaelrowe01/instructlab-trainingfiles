META:TOPICINFO{author="tfeeney" date="1588773294" format="1.1"
version="1.7"} META:TOPICPARENT{name="CLMExpensiveScenarios"} e

# CLM Scenarios to Investigate as Potentially ExpensiveRED(DRAFT)ENDCOLOR DKGRAY Authors: Main.TimFeeney Build basis: The Rational solution for Collaborative Lifecycle Management (CLM) and the Rational solution for systems and software engineering (SSE) v6.0.1. [clm-scenarios-to-investigate-as-potentially-expensivereddraftendcolor-dkgray-authors-main.timfeeney-build-basis-the-rational-solution-for-collaborative-lifecycle-management-clm-and-the-rational-solution-for-systems-and-software-engineering-sse-v6.0.1.]

ENDCOLOR

TOC{title="Page contents"}

This page captures CLM scenarios that may potentially be expensive but
need further investigation to characterize and confirm. See the parent
topic containing the
[known](https://jazz.net/wiki/bin/edit/Deployment/CLMExpensiveScenarios)
list.

REDNote: The information herein is a work in progress and is continually
being reviewed/refinedENDCOLOR

|  |  |  |  |  |
|----|----|----|----|----|
| BLUE **Table 1: Summary of CLM Scenarios to Investigate** ENDCOLOR |  |  |  |  |
| **Product** | **Scenario** | **Scenario ID** | **Best Practice** | **Investigate** |
| [Rational DOORS Next Generation (DRAFT)](#Rational_DOORS_Next_Generation) | [Comparing local configurations with large number of artifacts](#Comparing_local_configurations_w) | DNG_Compare_Configuration | link | [106102](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=106102) |
|  |  |  |  |  |
| [Rational Team Concert (DRAFT)](#Rational_Team_Concert) | [Concurrently loading a large number of large configurations](#Concurrently_loading_a_large_num) | RTC_Load_Workspace | link | [389280](https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.viewWorkItem&id=389280) |
| \^ | [Import of large CSV files](#Import_of_large_CSV_files) | RTC_CSV_Import | link | [389357](https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.viewWorkItem&id=389357) |
| \^ | [Export of large number of work items to CSV file](#Export_of_large_number_of_work_i) | RTC_Workitem_Export | link | [389359](https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.viewWorkItem&id=389359) |
| \^ | [Large bulk edits of work items](#Large_bulk_edits_of_work_items) | RTC_WI_Bulk_Edit | link | [389361](https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.viewWorkItem&id=389361) |
|  |  |  |  |  |
| [Rational Quality Manager (DRAFT)](#Rational_Quality_Manager) | [Comparing local configurations with large number of artifacts](#Comparing_local_configuratio_AN1) | RQM_Compare_Configuration | link | [151178](https://jazz.net/jazz02/web/projects/Rational20Quality20Manager#action=com.ibm.team.workitem.viewWorkItem&id=151178) |
|  |  |  |  |  |
| [Jazz Reporting Services (all reporting technologies) (DRAFT)](Jazz_Reporting_Services_all_repo) |  |  |  |  |
|  |  |  |  |  |
| [Global Configuration (DRAFT)](#Global_Configuration) |  |  |  |  |

## Rational DOORS Next Generation

### Comparing local configurations with large number of artifacts

RED This scenario needs further analysis to confirm it can be expensive
and to characterize further. See [work item
106102](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=106102)
ENDCOLOR

## Rational Rhapsody Design Manager

### Importing or moving a large model to DM

When you import a large model, or move a large model (in
actively-managed mode) to DM, the server could potentially become
unresponsive, especially when others are working in that same stream. DM
notifies users that an import is occurring.

### Scenarios that load a large model

Some scenarios require loading a model in its entirety; if the model is
large, it can impact server memory and processing. Such scenarios
include:

-   Generating code from a model
-   Exporting a model (using Save as)
-   Creating a table layout in Rhapsody with too broad a scope

Use smaller related models to reduce the system demands; this is also a
best practice.

### OSLC integration to DNG/DOORS Rhapsody DM can manage OSLC links between model elements and requirements artifacts in related DOORS and DNG projects. When doing so, DM retrieves all available requirements from the projects and all defined links from the DM server. The integration synchronizes to find new requirements/links. If the requirements project is large, the link management can be resource-intensive.

To reduce resource demands, use a filtered view (e.g. collection,
module) to narrow the amount of requirements to retrieve.

## Rational Team Concert

### Concurrently loading a large number of large configurations

This may occur with many continuous builds doing many concurrent loads
of large configurations (those approaching the file/folder limit as
described in [RTC
Limits](https://jazz.net/wiki/bin/view/Deployment/EnvelopesRangesAndLimits#RTC)).

RED This scenario needs further analysis to confirm it can be expensive
and to characterize further. See [work item
389280](https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.viewWorkItem&id=389280).
ENDCOLOR

### Import of large CSV files

Similar to an import of a Microsoft Project plan, an import of a large
CSV file can keep the server busy and drive memory usage. However,
unlike the plan import, CSV file imports occur more frequently and are
often part of a round trip update.

RED Further investigation to better characterize a 'large' CSV file
import and the load generated when importing one is tracked by [work
item
389357](https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.viewWorkItem&id=389357).
ENDCOLOR

#### Best Practices for Import of large CSV files [best-practices-for-import-of-large-csv-files]

For more than 1000 work items, it is best to wait for off hours or until
the server is lightly loaded.

### Export of large number of work items to CSV file

Exporting a large number of work items primarily impacts memory on the
server.

RED Further investigation to better characterize a 'large' number of
work items and the load generated when exporting them is tracked by
[work item
389359](https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.viewWorkItem&id=389359).
ENDCOLOR

### Large bulk edits of work items Performance and load driven by this scenario is a function of the number of work items and number of attributes changed as each work item is changed and saved one at a time.

RED This scenario needs further analysis to confirm it can be expensive
and to characterize further. See [work item
389361](https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.viewWorkItem&id=389361).
ENDCOLOR

### Slow running scenarios

#### Synchronizing attributes after a large amount of change in attributes for a work item [synchronizing-attributes-after-a-large-amount-of-change-in-attributes-for-a-work-item]

There are two ways for [synchronizing work item
attributes](http://www-01.ibm.com/support/docview.wss?uid=swg21372230).
First, using the RTC Eclipse client, run a query and select a set of
work items then right click the type column and select Synchronize
Attributes. This process would only affect the selected work items and
response time is not a concern unless the client selected thousands of
work items. The second method is to trigger the sync from the process
configuration editor by the "check attributes usages in repository"
action. This process could take a long time as it sync all work items
created with all work item types within the same project area. If there
are thousands of work items in the project area with a large number of
attributes changes, it can take some time to complete (a warning is
presented to the user).

#### Loading a work item with a large amount of customized attributes [loading-a-work-item-with-a-large-amount-of-customized-attributes]

When there are over 100 custom attributes in a work item type, loading
of a work item of that type can be slow from the client perspective but
isn't known to drive server load.

## Rational Quality Manager

### Comparing local configurations with large number of artifacts

RED This scenario needs further analysis to confirm it can be expensive
and to characterize further. See [work item
151178](https://jazz.net/jazz02/web/projects/Rational20Quality20Manager#action=com.ibm.team.workitem.viewWorkItem&id=151178).
ENDCOLOR

## Jazz Reporting Services (all reporting technologies)

## Global Configuration

-------

##### Related topics: [related-topics]

##### External links: [external-links]

META:TOPICMOVED{by="tfeeney" date="1462956549"
from="Deployment.OperationsToBeInvestigated"
to="Deployment.ScenariosToBeInvestigated"}
