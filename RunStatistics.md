META:TOPICINFO{author="sbagot" date="1432745849" format="1.1"
version="1.2"} META:TOPICPARENT{name="CLMUpgradeTroubleshooting"}

# Run Database Statistics [run-database-statistics]

Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam) Build
basis: CLM 4.x, 5.x ENDCOLOR

TOC{title="Page contents"}

This topic discusses running the database statistics prior to an
upgrade.

## Database Statistics

The upgrade documentation suggests that prior to any upgrade, you should
update the database statistics for your CLM Deployment. Otherwise, the
upgrade process may take significantly longer.

The following tables must contain up-to-date database statistics:
REPOSITORY.ITEM_STATES REPOSITORY.ITEM_CURRENTS REPOSITORY.ITEM_TYPES
LINKS.AUDITABLE_LINK

## Running the Database Statistics

Work with your DBA to run the database statistics.

## Common Issues

Below are some known issues which arise during the update configuration
files step in the upgrade process

### DB2: Runstats fails

**Version:** Upgrade to 4.x using DB2 **Error During Upgrade:** The
default runstats, db2 runstats on table REPOSITORY.ITEM_STATES, command
fails, it results in an error related to the
INDEX-Dcom.ibm.team.repotools.rcp.allowInvalidBundles=true" is not
properly formatted. **Resolution:** Have your DBA run the following
command: db2 runstats on table REPOSITORY.ITEM_STATES on all columns and
sampled detailed indexes all allow write access

##### Related topics: [related-topics]

\* For more upgrade troubleshooting topics, refer to [Upgrade
Troubleshooting](UpgradeTroubleshooting).

##### External links: [external-links]

-   None

##### Additional contributors: Main.SusanWu [additional-contributors-main.susanwu]
