META:TOPICINFO{author="sbagot" date="1432746048" format="1.1"
version="1.13"} META:TOPICPARENT{name="CLMUpgradeTroubleshooting"}

# Upgrading the data warehouse [upgrading-the-data-warehouse]

DKGRAY Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam)
Build basis: CLM 3.x and later ENDCOLOR

TOC{title="Page contents"}

This page discusses the Datawarehouse upgrade process which is part of
the Jazz Team Server upgrade script.

## Current data warehouse configuration

The data warehouse schema was a feature initially added to CLM 3.0.1 and
is used for reporting. If you were running any Jazz based products prior
to 3.0.1, and upgraded to 3.0.1, you may be running the data mart if you
did not migrate to the data warehouse. If this is the case, you can skip
this step.

To validate if you are running the data mart or data warehouse, log-in
to the Server Administration page and click **Reports**. Under the
Configuration section click **Data Warehouse Connection** and check the
**Data Warehouse Provider** attribute. If it is set to **Remote**, you
are likely have a Data Warehouse schema setup. If it is set to
**Local**, you are still using data mart or you did not configure a data
warehouse (this configuration is only available in applications at
version 3.0.1.x and higher).

If you are running the data mart, you can skip this step of the upgrade.
If you are running the data warehouse, you can continue this step of the
upgrade.

### Data mart vs data warehouse

A data mart is a storage facility for read-only, historical and
aggregated data. Through the use of an industry standard "star schema",
rather than a more normalized table structure, the data mart is
optimized for efficient queries and quick response times. Reports access
the data that is stored in this data mart. Data mart is not a separated
database from the JTS repository database, but a snapshot only. Prior to
CLM 3.0.1, the Jazz Team Server provides a data mart, as well as an
extensible mechanism for gathering information to store in the data mart
at periodic times. Out of the box, data collection jobs are provided
that aggregate and store various data about work items, source control,
and builds.

A data warehouse is a relational database that is designed for query and
analysis rather than for transaction processing. It contains historical
data derived from transaction data, but it can include data from other
sources. It separates analysis workload from transaction workload and
enables an organization to consolidate data from several sources.
Starting from CLM 3.0.1, users can take advantage of data warehouse
schema feature to separate report data from the JTS repository database.
This feature provide users more control on managing the process of
gathering report data and delivering to business users.

## Data Warehouse upgrade process

During the step in the upgrade, the data warehouse database will undergo
the following changes:

-   Upgrade the Core Schema
-   Grant Core Schema Read Access
-   Populate Date Dimension
-   Upgrade Calm Schema
-   Grant Calm Schema Read Access

### Troubleshooting the Data Warehouse upgrade process

For information on Troubleshooting the Data Warehouse Upgrade Process,
navigate to [Troubleshooting the data
warehouse](https://jazz.net/wiki/bin/edit/Deployment/UpgradeDWSchemaKnownIssues).

### Known Issues

For information on known issues to occur during the data warehouse
upgrade process, navigate to [Known
Issues](https://jazz.net/wiki/bin/edit/Deployment/UpgradeDWSchemaKnownIssues).

## Can I choose not to upgrade my data warehouse?

Yes, but before DW upgrade is completed, all the reports are likely to
fail or display stale data due to failing ETL jobs, meaning, no new data
is gathered for reporting.

### Upgrading the data warehouse manually

If you choose not to upgrade the Data Warehouse when you upgrade the
JTS, it can be upgraded later. Run the following JTS repotools
upgradeWarehouse command:

Windows: cd JazzInstallDir\server repotools-jts.bat -upgradeWarehouse
teamserver.properties=conf\jts\teamserver.properties

UNIX: cd JazzInstallDir/server ./repotools-jts.js -upgradeWarehouse
teamserver.properties=conf/jts/teamserver.properties

|  |
|----|
| **Note:** Jazz Team Server must be upgraded successfully before you can proceed with the data warehouse upgrade. |

### Obtaining DDL scripts for the DW upgrade

Some deployments require the DDL scripts which are run during the
upgrade process so that the data warehouse can be upgraded manually.
This feature will be made available from CLM 4.0.3. [Check here for
detailed instructions in CLM version
4.0.3](https://jazz.net/wiki/bin/view/Main/GenerateDDLScriptsForTheDataWarehouseCreationAndUpgrade)

##### Related topics: [related-topics]

\* [Data Warehouse Snapshot
Schemas](https://jazz.net/wiki/bin/view/Main/DataWarehouseSnapshotSchemas20)
\* [Data Warehouse
Concepts](https://jazz.net/wiki/bin/view/Main/DataWarehouseConcepts) \*
For more troubleshooting topics, refer to [Upgrade
Troubleshooting](UpgradeTroubleshooting).

##### External links: [external-links]

-   None

##### Additional contributors: Main.SusanWu [additional-contributors-main.susanwu]
