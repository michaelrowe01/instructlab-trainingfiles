META:TOPICINFO{author="paulellis" date="1381159390" format="1.1"
reprev="1.4" version="1.4"}
META:TOPICPARENT{name="UpgradingRequirementsComposerFrom2To3"}

# Perform a trial RRC2 to RRC3 migration [perform-a-trial-rrc2-to-rrc3-migration]

DKGRAY Authors: Main.ShirleyHui Build basis: CLM 2011, Rational Team
Concert 3.0.1, Rational Requirements Composer 3.0.1ENDCOLOR

TOC{title="Page contents"}

This article describes tips for planning your RRC2 to RRC3 migration by
performing a trial upgrade.

Refer to [Upgrade Reference for CLM
2011](https://jazz.net/library/article/698) for overall guidance on
upgrading.

We highly recommend that you perform a trial upgrade in a test
environment before upgrading your production environment.

However, we also recognize that performing a trial upgrade may be a
complex, time-consuming task. One of the most important steps to
preparing for the upgrade - understanding how your type system will look
in RRC3 - can be accomplished without upgrading your entire repository.

We recommend that you independently migrate one or two projects whose
type systems are representative of your team's usage. This step will
take a little extra time to setup, but it will save time overall.

In this smaller environment, you may also review the migration logs and
directories, run the upgrade report tool, and become familiar with the
delta and error annotations. The files will be smaller and more
manageable, for one project. You may find issues that can be reported to
Support, or determine that some modifications to RRC2 data will be
necessary. It is also easier and faster to re-test the migration, if
necessary. The turn around time will be faster with only one project in
the repository.

After you are comfortable with the upgrade of the sample project,
proceed with the trial upgrade of the entire repository. The upgraded
sample repository cannot be used in a production environment. The sample
project exported from RRC2 will not have all revisions of artifacts and
some other data is not exported via the project archive.

## Extract and migrate a single project to evaluate the type system

-   From your current RRC2 client, download a project archive of a
    representative project
-   Install RRC2 on a test machine
-   Import the project archive into the test RRC2 repository. If you
    have a few projects, repeat for additional projects.
-   Install RRC3 on a test machine.
    -   This can be the same machine you just installed RRC2. You cannot
        run RRC2 and RRC3 simultaneously, only one server can run at a
        time.
    -   This can use the simplest configuration with Tomcat and Derby.
    -   If you wish, you can setup the environment to mirror your
        production environment and reuse the environment to run the
        trial upgrade. However, this often involves multiple machines.
        With Tomcat and Derby, you will likely be able to use one
        machine, without overloading it.

<!-- -->

-   From the RRC2 test server, export the test repository. Copy the tar
    file to the RRC3 test server.
-   From the RRC3 test server, perform the offline migration using the
    upgrade scripts.
-   Continue with the online migration step.
-   Examine the migration results and review the type system in RRC3
    from 'Manage Project Properties' UI dialog
-   Review the [type system
    information](UnderstandingTheDataTransformations#SectionA).
    -   You may want to redo the migration to try some of the
        suggestions. You can restore from backup and try again.

<!-- -->

-   Review the [Results of the
    Migration](UpgradingRRCReviewTheMigrationResults).

IMPORTANT: Take a backup after offline migration. For example,

-   from the InstallDir/server directory, run "repotools-jts.bat -export
    toFile=afterOffline.tar"
-   if you need to re-do the online migration, run "repotools-jts.bat
    -import fromFile=afterOffline.tar"
-   if the network fails, or other major system failure, like a power
    outage, you have to restart from backup

Note: If you change the RRC2 data, you will need to start with a new
RRC3 install

This exercise is for test purposes only - the upgraded RRC3 test
repository will not have all data from your RRC2 repository.

## Run a Trial Upgrade

Open the [Info
Center](http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/index.jsp) and
search for 'Staging a test environment for the upgrade process'.

We recommend running a trial upgrade of your repository in a test
environment before upgrading your production environment.

-   This will give you an idea of how long it will take in production
-   Expose any issues in the test environment, not while users are
    trying to work.
-   Possibly repair or reorganize some data in RRC2 before the upgrade
-   Some additional things to consider:
    -   Archive old projects before performing the upgrade
    -   [Reduce the RRC2 export time](#SectionR1)

After running the trial upgrade and reviewing the results, some actions
may be required on the RRC2 data. Perform those actions and repeat the
trial until you are satisfied with results. When you are satisfied,
perform upgrade on production data, taking care to take backups at every
major step.

\#SectionR1

## Reduce the RRC2 export time

There are 3 ways to reduce the RRC2 export time:

-   We found that you will have a significant performance improvement if
    you run the repotools -export from the same machine where the
    database is installed. This requires installing RRC2 or Jazz
    Foundation 1.0.0.2 iFix 8 on the same machine as the DB server.
    However, many customers are prohibited from installing other
    software on the DB server.
-   Disable inclusion of indices in the tar file. They are not needed
    for migration.
    -   Add to the existing teamserver.properties:
        com.ibm.team.jfs.enable.index.migration=false to disable
        inclusion of indices in tar file
-   Use an enhancement to repotools -export which allows us to skip
    storage areas that contain data that will never be used in RRC 3.x.
    -   This feature is available in Jazz Foundation 1.0.0.2 iFix 8.
    -   This version of Jazz Foundation was released after the latest
        release of RRC 2.x. It is not available in any RRC 2.x. However,
        this is not a problem. You only need JFS to run the repotools
        -export.

How to install

-   Install JFS 1.0.0.2 iFix8 (either on DB machine or another machine)
-   Copy the RRC2ServerInstallDir/server/conf directory (contains
    conf/jazz and conf/rdm) to the JFS install directory
-   Copy the update sites directories from the
    RRC2ServerInstallDir/server directory to the JFS install directory
-   Configure teamserver.properties to point to the database being used
    by RRC2. (may already be correct from copying it above)
-   Add to the existing teamserver.properties:

com.ibm.team.jfs.exportFilterHistoryInStorageAreas=com.ibm.rdm.project-resources,com.ibm.rdm.attributegroups,com.ibm.rdm.savedfilters

to ignore these storage areas

-   Also add com.ibm.team.jfs.enable.index.migration=false to disable
    inclusion of indices in tar file
-   Shutdown the RRC 2.x server (if you haven't already done so)
-   Run the repotools -export from the JFS installation.

##### Related topics: [Limitations](UpgradingRequirementsComposerFrom2To3#SectionR1), [Understanding the data transformations](UnderstandingTheDataTransformations), [Running a trial migration](UpgradingRRCRunningaTrialMigration), [Perform backups before offline and online migration steps](UpgradingRequirementsComposerFrom2To3#SectionR4), [Online migration error handling](UpgradingRequirementsComposerFrom2To3#SectionR5), [Review the migration results](UpgradingRRCReviewTheMigrationResults) [related-topics-limitations-understanding-the-data-transformations-running-a-trial-migration-perform-backups-before-offline-and-online-migration-steps-online-migration-error-handling-review-the-migration-results]

##### External links: [external-links]

-   [Upgrade Reference for CLM
    2011](https://jazz.net/library/article/698)

##### Additional contributors: Main.PaulEllis [additional-contributors-main.paulellis]

META:TOPICMOVED{by="paulellis" date="1380817034"
from="Deployment.UpgradingRRCRunningatrialmigration"
to="Deployment.UpgradingRRCRunningaTrialMigration"}
