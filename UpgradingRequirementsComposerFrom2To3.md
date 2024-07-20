META:TOPICINFO{author="paulellis" date="1383732153" format="1.1"
version="1.3"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Advanced Upgrade observations: IBM Rational Requirements Composer 2.x to 3.x [advanced-upgrade-observations-ibm-rational-requirements-composer-2.x-to-3.x]

DKGRAY Authors: Main.ShirleyHui Build basis: CLM 2011, Rational Team
Concert 3.0.1, Rational Requirements Composer 3.0.1ENDCOLOR

TOC{title="Page contents"}

This article describes details specific to migrating from Rational
Requirement Composer (RRC)2 to RRC3, also known as CLM 2011.BR Refer to
[Upgrade Reference for CLM 2011](https://jazz.net/library/article/698)
for overall guidance on upgrading.BR This article is also relevant to
those who wish to migrate to RRC 4.x/CLM 2012 and beyond, as the
migration to 3.x is a first step in the two-step process of migrating
from RRC 2.x.BR

## Recommendations

-   Migrate using the most recent version of 3.0.1.x in order to have
    the most up to date fixes in migration code. Currently this is
    version RRC 3.0.1.6.
-   Validate the data after migrating to 3.0.1.6 and BEFORE proceeding
    with an upgrade to 4.x or newer versions.

Please use the following sections to understand the data migration, and
to plan and execute your migration.

-   [Limitations](#SectionR1)
-   [Understanding the data
    transformations](UnderstandingTheDataTransformations)
-   [Running a trial migration](UpgradingRRCRunningaTrialMigration)
-   [Perform backups before offline and online migration
    steps](#SectionR4)
-   [Online migration error handling](#SectionR5)
-   [Review the migration
    results](UpgradingRRCReviewTheMigrationResults)

\#SectionR1

### Limitations

-   The migration occurs for the entire RRC2 repository. Partial or
    project-by-project migration is not supported.BR
-   Migration of RRC2 project archives is not supported.BR
-   All URI references using the rich-client based protocol
    (rpc://protocol) will be broken after migration.BR
-   This protocol is not supported in RRC3.BR

\#SectionR4

### Perform backups

Migration cannot be resumed or restarted if an error is encountered. You
must restart the migration at the previous step from backup. Perform a
backup of the Jazz Team Server and database (this includes the database
and the InstallDir/server/conf directory) before:BR

-   Running the upgrade\rm_upgrade.bat script (offline migration step)
-   Starting the online migration

\#SectionR5

### Online migration error handling

The online migration phase must run uninterrupted from start to
finish.BR

Fatal error conditions:

-   Loss of connectivity to JTS.
-   Insufficient disk space.
-   General environment failures, such as power failure or other network
    issues.BR

If you encounter any of these fatal errors, resolve the environment
issues, restore the Jazz Team Server server from backup and run the
online migration again.

### Unexpected migration error

When the online migration is complete, it will report whether it was
successful.BR

If it reports that the migration failed, locate the
'migration-errors.log' in InstallDir/conf/rdm/migration/systime-tmp
directory. *systime* is a 13 digit number based on the time the
migration ran.BR

Review the errors for conditions related to the environment (network,
JTS error). If possible, correct the condition, restore from backup, and
run the online migration again.BR

If there are no environment failures, contact IBM Support.BR

### Errors in individual resources

The online migration will be successful even if there are errors in
individual resources. These errors are not considered fatal. You will be
able to access the repository to validate the migration.

We highly recommend that you perform a trial upgrade in a test
environment before upgrading your production environment. Errors in
individual resources should be investigated to determine if the
migration code can be corrected. Often, the resource was corrupted in
RRC2 and is no longer in use in your project.

##### Related topics: [Limitations](#SectionR1), [Understanding the data transformations](UnderstandingTheDataTransformations), [Running a trial migration](UpgradingRRCRunningaTrialMigration), [Perform backups before offline and online migration steps](#SectionR4), [Online migration error handling](#SectionR5), [Review the migration results](UpgradingRRCReviewTheMigrationResults) [related-topics-limitations-understanding-the-data-transformations-running-a-trial-migration-perform-backups-before-offline-and-online-migration-steps-online-migration-error-handling-review-the-migration-results]

##### External links: [external-links]

-   [Upgrade Reference for CLM
    2011](https://jazz.net/library/article/698)

##### Additional contributors: Main.PaulEllis [additional-contributors-main.paulellis]

META:FILEATTACHMENT{name="migrationWithErrors.JPG"
attachment="migrationWithErrors.JPG" attr="" comment=""
date="1380818164" path="migrationWithErrors.JPG" size="58859"
user="paulellis" version="1"}
