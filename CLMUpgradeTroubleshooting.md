META:TOPICINFO{author="d3v3r1tt" date="1424460046" format="1.1"
reprev="1.9" version="1.9"}
META:TOPICPARENT{name="UpgradeTroubleshooting"}

# CLM upgrade troubleshooting [clm-upgrade-troubleshooting]

DKGRAY Authors: Main.StephanieBagot,
[UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam) Build basis:
CLM 3.x and later ENDCOLOR

TOC{title="Page contents"}

This page is the starting point for information and techniques to help
diagnose and troubleshoot upgrade issues when upgrading the Rational
Collaborative Lifecycle Management (CLM) family of products (Rational
Team Concert, Rational Requirements Composer, and Rational Quality
Manager).

## Before upgrading

**Before you start the upgrade process, verify the integrity of the
database by runing the
[-verify](http://www.ibm.com/support/knowledgecenter/SSYMRC_5.0.2/com.ibm.jazz.install.doc/topics/r_repotools_verify.html)
repotools command.**

**Planning to upgrade to version 5? See the [RRC 4.x to 5.x migration
tips and
tricks](https://jazz.net/wiki/bin/view/Deployment/RM4to5MigrationTipsTricksProblemsAndSolutions)
article for known issues**

-   Check the [Known issues](KnownIssues) for awareness of issues in the
    current version as a prerequisite for the upgrade
-   Ensure that your current environment meets all the requirements by
    checking the [Environment checklist](EnvironmentCheckList)
-   Perform the upgrade in a test environment prior to upgrading your
    production environment
-   [Backup the necessary configurations and files prior to your
    upgrade](BackupBeforeUpgrade)
-   Go through the [Upgrade
    Insider](https://jazz.net/wiki/bin/view/Deployment/UpgradeInsider)
    page of the deployment wiki for further information about your
    upgrade
-   Contact IBM Support and open up a proactive PMR with your upgrade
    plan and environment specifics. This will ensure Support is aware of
    the upgrade and can plan accordingly to become familiar with your
    environment and plan, resulting in faster response times.
-   [Update your Database Statistics](RunStatistics)

## Performing the upgrade

Below are the steps necessary to complete a successful upgrade. Each
item below discusses common issues seen at that particular step within
the upgrade process.

-   [Run the upgrade script](CLMUpgradeScripts) or alternatively
    [Running the upgrade manually](RunningTheUpgradeManually)
    -   [Update configuration files (CCM, Quality Management, Jazz Team
        Server)](UpdateConfigurationFiles)
    -   [Add database tables (CCM, Quality Management, Jazz Team
        Server)](AddDatabaseTables)
    -   [Upgrade the data warehouse schema (Jazz Team
        Server)](UpgradeDwSchema)
    -   RRC (RDNG) Migration in 5.x - see [RRC 4.x to 5.x migration tips
        and
        tricks](https://jazz.net/wiki/bin/view/Deployment/RM4to5MigrationTipsTricksProblemsAndSolutions)
        or [known
        issues](https://jazz.net/wiki/bin/view/Deployment/RRCMigrationKnownIssues)
-   [Start the applications](StartTheApplications)
-   [Licenses](Licenses)
-   [Migrating the Requirements Management
    application](MigratingRequirementsManagementApplication)
-   [Redeploying predefined templates](RedeployingPredefinedTemplates)

## Upgrade Verification

The following are some items to consider while completing a verification
of data after an upgrade:

### Admin Verification

-   Verify there are no errors in the upgrade logs
-   [Verify the configuration
    files](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.install.doc/topics/t_update_prepare_config.html&scope=null)
-   [Verify server logs and
    URLs](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.install.doc/topics/t_update_prepare_config.html&scope=null)
-   [Verify users, licenses and link
    artifacts](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.install.doc/topics/c_verify_users_licenses_links.html&scope=null)
-   Verify there are no diagnostic errors on any application
-   Verify you are able to navigate between linked project areas
-   Verify there are no errors in process configuration (particularly
    for customized project areas)

Consider you or your users completing an [Upgrade
Verification](https://jazz.net/wiki/bin/view/Deployment/UpgradeVerification)
to ensure the upgrade was successful (not all steps may apply in each
environment).

Consider running an [Online
Verify](https://jazz.net/wiki/bin/view/Main/L3DevTool) which will check
the consistency of the data.

### User Validation:

-   Access work items, saving, creating new work items (verify no
    information is missing)
-   View plans (verify no information is missing)
-   View Dashboards; ensure all are working with no errors
-   Load Reports
-   Access Source Control (checkin, checkout, deliver)

## Issues during user verification testing after upgrade

If your upgrade was successful, but your users report the following:

-   Various functions are not working as expected, or not working the
    same as the pre-upgrade version
-   Some data, such as item statuses, are corrupted after the upgrade
-   Full text queries fail
-   Dashboard issues

Navigate to [Common issues that occur after the
upgrade](AfterTheUpgrade) for information on troubleshooting and
debugging.

## Where do I go from here? If you are unable to resolve your issue using the available online resources, open a service request with IBM Rational Support. Refer to [Additional troubleshooting resources](DataCollectionandSupportResources) for further details.

##### Related topics: None [related-topics-none]

##### External links: \* None [external-links-none]

##### Additional contributors: Main.StephanieBagot, Main.SusanWu, Main.MichaelAfshar, Main.WilliamChen, Main.BrettBohnn, Main.DianeEveritt [additional-contributors-main.stephaniebagot-main.susanwu-main.michaelafshar-main.williamchen-main.brettbohnn-main.dianeeveritt]
