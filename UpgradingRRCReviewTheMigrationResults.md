META:TOPICINFO{author="paulellis" date="1380897402" format="1.1"
reprev="1.3" version="1.3"}
META:TOPICPARENT{name="UpgradingRequirementsComposerFrom2To3"}

# Reviewing the RRC3 migration results [reviewing-the-rrc3-migration-results]

DKGRAY Authors: Main.ShirleyHui Build basis: CLM 2011, Rational Team
Concert 3.0.1, Rational Requirements Composer 3.0.1ENDCOLOR

TOC{title="Page contents"}

This article describes how to access and review the results of the RRC3
migration.

Refer to [Upgrade Reference for CLM
2011](https://jazz.net/library/article/698) for overall guidance on
upgrading.

To review the results of the upgrade, run the [RRC Upgrade report tool
](#SectionA1)and review the [contents of the upgrade
directory](#SectionA2).

\#SectionA1

## Upgrade Report Tool

The upgrade report tool is available in versions 3.0.1.4 and higher in
InstallDir/conf/rdm/tools.BR

Command line:BR

upgrade-reports.bat -helpBR

upgrade-reports.sh -helpBR

upgrade-reports.bat *command* {-help}BR

upgrade-reports.sh *command* {-help}BR

commands: makeResourceReport, makeErrorReport, makeDeltaReport,
makeErrorArchiveBR

**makeResourceReport** BR

Generates resource-centric reports:

-   resource-urls.csv - a list of the resource urls for artifacts with
    errors.

Note: this does not include internal resources, such as links or
comments, that do not have a front side url.

Each artifact listed may have multiple revisions with errors - consult
the file resource-report-errs.csv. The entry in this list is the URL
that will display the artifact in a browser, if the artifact is
accessible. You may use this URL in RRC2 to determine if the current
revision of this artifact was accessible and not corrupted. The entry
also includes the number of revisions of this artifact that are
reporting an error.

-   resource-report-errs.csv - one report for all error annotations.
-   resource-report.\_projectAreaId.csv - one for each project area,
    with delta annotations for each resource, including the resources
    that were reported in the errors report.BR

Each row represents a version of each resource, noting the value of all
annotations on that resource version noted during the upgrade. There may
be multiple versions of a particular resource, one row per version.

**makeErrorReport**

Generates an error-centric report, error-report.txt, which contains an
entry for each error found during the upgrade.

**makeDeltaReport**

Generates a delta annotation-centric report, delta-report.txt, which
contains an entry for each delta annotation noted during the upgrade.

**makeErrorArchive**

Generates an archive of all recorded data for resources that encountered
errors during the upgrade. The archive will be found in
InstallDir/rdm/migration/systime-tmp/systime-tmp.jar. This archive may
be used to communicate with Support about non-critical resource errors.

\#SectionA2

## Upgrade Results

### Location of the upgrade results directory

This directory will be found in the InstallDir/rdm/migration/systime-tmp
directory. systime is a 13 digit number.

### Navigating the upgrade directory

This directory contains:

-   migration-errors.log - If the upgrade has a critical failure, this
    file contains information about the failure
-   resource-errors.log - This file contains information about
    non-critical errors for individual resources
-   migration-metrics.rdf and resources-metrics.csv - Statistics from
    the migration
-   Folders representing different kinds of resources (for example,
    "Resources", "Folders", "Links", "Comments") contain files related
    to those resources.
-   When you run the upgrade report tool, output files are written to
    this directory.

**To find the original RRC2 xhtml content for a resource that reported
an error:**

-   Find the resource id in the entry in resource-errors.log, in the
    form 'rrc' followed by an ID.
-   Note the revision ID. For example, Resource:
    https://server:9443/jts/storage/com.ibm.rdm.resources/rrc308?revision=\_v1wbhmagEeCeW9etSZqfCw
-   Change to the Resources/rrcID directory.

In the directory, there will be files with unique id names, with no
extension, one file for each version of the resource.

For example: \_v1wbhmagEeCeW9etSZqfCw

This file contains the original RRC2 xhtml content for a version of this
resource.

**To find the resource delta file for a resource:**

-   To access the resource delta file for resource, find the resource
    id, in the form 'rrc' followed by an ID.

Change to the Resources/rrcID directory. In the directory, there will be
files with unique id names, with a .rdf extension, one file for each
version of the resource.

For example: \_v1wbhmagEeCeW9etSZqfCw

This is the resource delta file for this version of the resource.

## Review Results Checklist

-   Run InstallDir/rdm/tools/upgrade-report.bat makeResourceReport'
-   Review output files in the upgrade results directory.
-   Get the list of artifacts with migration errors from
    resource-urls.csv
-   Determine if each artifact is accessible in RRC2 and RRC3 by opening
    the URL. It will look something like,
    https://server:9443/rdm/resources/rrc346. The RRC2 UI may report it
    cannot open the artifact or encountered an error opening the
    artifact.
-   Eliminate artifacts that are no longer used in RRC2 - this may
    include artifacts that were corrupted in 2.x, or deleted. If the
    artifact is no longer used, you may ignore this error.
-   Some artifacts may not be accessible in RRC3 and some may be
    displayed but cannot display their contents. Separate the artifacts
    into two lists.
-   Using the resource-errors.log and the resource-report-errs.csv file,
    evaluate the errors for remaining artifacts.
-   The resource-report-errs.csv report contains a column
    'contentRepaired', which indicates whether a special repair
    transform was attempted on the resource content, and whether the
    repair succeeded or not. If it says 'Content repaired', the resource
    content was preserved but the original formatting needed to be
    removed. Other annotations indicate that the content could not be
    repaired.
-   If the artifact is active and required, contact IBM Support to
    submit a defect.

##### Related topics: [Limitations](UpgradingRequirementsComposerFrom2To3#SectionR1), [Understanding the data transformations](UnderstandingTheDataTransformations), [Running a trial migration](UpgradingRRCRunningaTrialMigration), [Perform backups before offline and online migration steps](UpgradingRequirementsComposerFrom2To3#SectionR4), [Online migration error handling](UpgradingRequirementsComposerFrom2To3#SectionR5), [Review the migration results](UpgradingRRCReviewTheMigrationResults) [related-topics-limitations-understanding-the-data-transformations-running-a-trial-migration-perform-backups-before-offline-and-online-migration-steps-online-migration-error-handling-review-the-migration-results]

##### External links: [external-links]

-   [Upgrade Reference for CLM
    2011](https://jazz.net/library/article/698)

##### Additional contributors: Main.PaulEllis [additional-contributors-main.paulellis]
