META:TOPICINFO{author="wbchen" date="1559753802" format="1.1"
reprev="1.2" version="1.2"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# QM addTables command can fail on 6.0.6.1 upgrade DKGRAY Authors: Main.WilliamChen Build basis: IBM Rational Quality Manager 6.0.x. [qm-addtables-command-can-fail-on-6.0.6.1-upgrade-dkgray-authors-main.williamchen-build-basis-ibm-rational-quality-manager-6.0.x.]

ENDCOLOR

TOC{title="Page contents"}

This wiki page provides detailed steps to resolve an addTables command
error during 6.0.6.1 upgrade.

This known issue is being tracked via Jazz defect
[482936.](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=482936)
The failure was only observed on two separate instances.

**Important**: Consult an DBA before running queries from steps 2
through 5.

### Step 1 - Check QM addTables log

This example is from DB2 database:

2019-05-14 10:49:13,496 The user "ADMIN" has logged out of the database
"//dbServer:port/instanceName:user=xxxxxxxx;password=xxxxxxxx;".
2019-05-14 10:49:13,496 CRJAZ3138E The total number of rows copied to
the new version table, REPOSITORY.VERSION, does not match the total
number of rows of the older version table(s). 2019-05-14 10:49:13,497
CRJAZ3138E The total number of rows copied to the new version table,
REPOSITORY.VERSION, does not match the total number of rows of the older
version table(s).
com.ibm.team.repository.common.TeamRepositoryException: CRJAZ3138E The
total number of rows copied to the new version table,
REPOSITORY.VERSION, does not match the total number of rows of the older
version table(s).

2019-05-14 10:49:13,498 CRJAZ1791E The migration completed with errors.
The imported database is unstable and should not be used without further
analysis.

### Step 2 - Run these two queries to check if there is a mismatch

select count(\*) from \[qm database
name\].\[EXECUTION\].\[VEXECUTION_RECORD\]

select count(\*) from \[qm database
name\].\[EXECUTION\].\[VEXECUTION_RECORD\] join \[qm database
name\].\[REPOSITORY\].\[ITEM_TYPES\] on \[qm database
name\].\[REPOSITORY\].\[ITEM_TYPES\].\[ITEM_UUID\]= \[qm database
name\].\[EXECUTION\].\[VEXECUTION_RECORD\].\[ITEM_ID\]

Note: Be sure to replace \[qm database name\] with valid QM database
name. The total number of rows should be different if there is a
mismatch.

### Step 3 - Restore QM database

This must be done before proceeding to step 4.

### Step 4 - Run this custom insert command

insert into REPOSITORY.ITEM_TYPES select distinct
REPOSITORY.ITEM_STATES.ITEM_UUID, REPOSITORY.ITEM_STATES.ITEM_TYPE_DBID
from EXECUTION.VEXECUTION_RECORD join REPOSITORY.ITEM_STATES on
ITEM_ID=ITEM_UUID where ITEM_ID not in ( select ITEM_UUID from
REPOSITORY.ITEM_TYPES)

This custom insert command should correct the row count discrepancy.
Please use next step to verify the information.

### Step 5 - Repeat step 2 to confirm there is no mismatch

Run both queries again to confirm there is no mismatch. Then complete
the remaining 6.0.6.1 upgrade steps.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.VidyaMalkarnekar, Main.GlennBardwell [additional-contributors-main.vidyamalkarnekar-main.glennbardwell]
