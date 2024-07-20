META:TOPICINFO{author="sbagot" date="1403543885" format="1.1"
reprev="1.1" version="1.1"} META:TOPICPARENT{name="UpgradeDwSchema"}

# Upgrading the data warehouse [upgrading-the-data-warehouse]

DKGRAY Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam)
Build basis: CLM 3.x and later ENDCOLOR

TOC{title="Page contents"}

This page discusses known issues and troubleshooting the Datawarehouse
upgrade process.

|  |
|----|
| **Note:** Jazz Team Server must be upgraded successfully before you can proceed with the data warehouse upgrade. |

## Troubleshooting the Data Warehouse upgrade process

Since the upgrade scripts for the Data Warehouse will change the
database, the most common issues that can occur during the upgrade are
related to the database. If this section of the upgrade script fails,
review the following log, located in the ../server folder of the CLM
application installation directory, for more information.

repotools-jts_upgradeWarehouse.log

## Known Issues

### CRJAZ0265E: The database resource or the virtual storage is not available.

**Version:** Upgrade to 4.x **Error During Upgrade:** CRJAZ0265E: The
database resource or the virtual storage is not available. SQLSTATE:
57011 **Cause:** This specific message is a result of running out of
space in the transaction logs. **Resolution:** Run the following SQL
statements to increase the log size. Note that the default size of the
first is 8, and the second is 16. db2 update db cfg for DWDB using
logprimary 20 db2 update db cfg for DWDB using logsecond 30

### Data Collection Jobs Failing

**Version:** Data warehouse upgrade to 4.x **Error During Upgrade:**
Data collection jobs are failing, and in the log file the following
error occurs: CRRRE1420E: Can not redirect to the OAuthentication
identify URL **Cause:** The data collection jobs need to go through a
'migration' **Resolution:** Run the full data collection jobs for all
once When you look at the status, for example, if you run a Full data
collection job for common under JTS/reports, you would see two entries,
**Common Migration** and **Common** **NOTE:** The full data collection
jobs may take some time to run in your deployment as they are different
than the daily jobs which only gather changed data.

##### Related topics: [related-topics]

\* [Data Warehouse Snapshot
Schemas](https://jazz.net/wiki/bin/view/Main/DataWarehouseSnapshotSchemas20)
\* [Data Warehouse
Concepts](https://jazz.net/wiki/bin/view/Main/DataWarehouseConcepts) \*
For more troubleshooting topics, refer to [Upgrade
Troubleshooting](UpgradeTroubleshooting).

##### External links: [external-links]

-   None

##### Additional contributors: Main.StephanieBagot [additional-contributors-main.stephaniebagot]

##### Questions and comments: [questions-and-comments]

COMMENT{type="below" target="UpgradeDwSchemaComments" button="Submit"}

INCLUDE{"UpgradeDwSchemaComments"}
