META:TOPICINFO{author="sbagot" date="1432746250" format="1.1"
version="1.8"} META:TOPICPARENT{name="CLMUpgradeTroubleshooting"}

# Running the upgrade manually [running-the-upgrade-manually]

DKGRAY Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam)
Build basis: CLM 4.x and later ENDCOLOR

TOC{title="Page contents"}

This page will discuss issues that arise when completing the upgrade
process manually instead of running the upgrade scripts.

## Upgrade steps

|  |
|----|
| It is strongly recommended that you complete the CLM upgrade by using the Interactive Upgrade Guide and the upgrade scripts. |

## Manually running the upgrade

If you decide to bypass using the upgrade script, you will be running
the repotools commands manually. The upgrade script runs the following
commands: repotools- -migration\_\_updateConfigurationFiles repotools-
-addTables

As well as performs the following file merges:

-   Updates the teamserver.proprties files based on the information from
    the previous version
-   With the RM application, the old version friendsconfig.rdf file is
    merged, which contains the list of servers set up for
    cross-repository integration with the new version
-   In a Tomcat environment, merges the content of server.xml and
    web.xml files with the new version and copies the old version
    tomcat-users.xml file
-   The JTS upgrade script will also upgrade the Data Warehouse

### Updating the configuration files

Navigate to [Updating the Configuration
Files](https://jazz.net/wiki/bin/view/Deployment/UpdateConfigurationFiles)
for information on known issues which may occur at this step.

### Adding the database tables

Navigate to [Adding the Database Tables](AddDatabaseTables) for
information on known issues which may occur at this step.

### Upgrading the data warehouse

Navigate to [Upgrading the DW Schema](UpgradeDwSchema) for information
known issues which may occur at this step.

##### Related topics: [related-topics]

\* For more upgrade troubleshooting topics, refer to [Upgrade
Troubleshooting](UpgradeTroubleshooting).

##### External links: \* None [external-links-none]

##### Additional contributors: Main.StephanieBagot [additional-contributors-main.stephaniebagot]
