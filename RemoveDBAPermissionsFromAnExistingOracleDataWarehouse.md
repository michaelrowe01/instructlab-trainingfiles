META:TOPICINFO{author="dcoffin" date="1553710894" format="1.1"
reprev="1.1" version="1.1"}
META:TOPICPARENT{name="ConfiguringAndTuningOracle"}

# Removing DBA permissions from an existing Oracle data warehouse [removing-dba-permissions-from-an-existing-oracle-data-warehouse]

DKGRAY Authors: Main.DarrenCoffin Build basis: CLM version 6.x and later
ENDCOLOR

TOC{title="Page contents"}

You can remove Database Administrator (DBA) permissions from an existing
Oracle data warehouse which was initially set up with a DBA user. This
is achieved by using the repository tools command.

## Modifying existing Oracle data warehouse

1\. Stop the Jazz Team Server, if it is running.

2\. To generate the scripts go to JTS_Install_Dir/server and run the
following command. Replace user ID and user password with your etlDbUser
user ID and password. The etlDbUser should be a new user that will not
have admin access, instead of the current user that is already
configured for the data warehouse:repotools-jts
-generateWarehouseDDLScripts
additionalOptions="noAdmin;etlDbUser:;defaultPsswd:" The
`additionalOptions` parameters include:

-   `noAdmin` (required): Indicates that the generated scripts can be
    run without DBA privileges.
-   `etlDbUser` (required): The user ID of a database user that is used
    to connect to the data warehouse and run the ETL jobs from CLM. This
    user should not have DBA privileges and does not need to already
    exist.
-   `defaultPsswd` (optional): The password to be assigned to all
    automatically created data warehouse users. This value is optional.
    However, if a default password is not specified, then individual
    passwords must be set instead.
-   `cfgPsswd` (optional): The password to be assigned to the
    automatically created data warehouse user. This value must be
    provided if a default password is not specified.
-   `calmPsswd` (optional): The password to be assigned to the
    automatically created data warehouse user. This value must be
    provided if a default password is not specified.
-   `dwPsswd` (optional): The password to be assigned to the
    automatically created data warehouse user. This value must be
    provided if a default password is not specified.
-   `odsPsswd` (optional): The password to be assigned to the
    automatically created data warehouse user. This value must be
    provided if a default password is not specified.
-   `assetPsswd` (optional): The password to be assigned to the
    automatically created data warehouse user. This value must be
    provided if a default password is not specified.
-   `schkPsswd` (optional): The password to be assigned to the
    automatically created data warehouse user. This value must be
    provided if a default password is not specified.

The command produces the following script files in the
repotools-jts_generateWarehouseDDLScripts.out/oracle directory. Not all
of them will be used in these instructions:

-   1-setupCoreSpace.sql
-   2-createCoreSchema.sql (not used; core schema already exists in an
    existing data warehouse)
-   3-grantCoreSchemaReadAccess.sql
-   4-populateDateDimension.sql (not used; date dimensions are already
    populated in an existing data warehouse)
-   5-setupCalmSpace.sql
-   6-createCalmSchema.sql (not used; calm schema already exists in an
    existing data warehouse)
-   7-grantCalmSchemaReadAccess.sql
-   additionalSteps.sql

|  |
|----|
| **Note:** If you have more than one Oracle database in your environment, in order for the scripts to locate the correct database you must create an environment variable called ORACLE_SID and set its value to your database name before you try running the scripts on your Oracle server. For example, `SET ORACLE_SID=CLMDB` |

|  |
|----|
| **Note:** You will encounter some error messages about partitions already existing and about user name conflicts. You might also encounter some error messages about a missing RPTUSER. These error messages can safely be ignored. |

3\. Open SQL Plus and run the following scripts in this order. DBA
privileges required:

-   1-setupCoreSpace.sql
-   5-setupCalmSpace.sql

4\. If the etlDBUser does not already exist, do these steps to create
it. DBA privileges required:

1.  Open additionalSteps.sql for editing.
2.  Replace the password with an actual password.
3.  Save and close the additionalSteps.sql file.
4.  Run the additionalSteps.sql script in SQL Plus. The script will
    create a non-DBA user with the required permissions for running the
    ETL jobs from CLM.

5\. In SQL Plus run these scripts in this order. DBA privileges not
required.

-   3-grantCoreSchemaReadAccess.sql
-   7-grantCalmSchemaReadAccess

6\. Start the Jazz Team Server and log into
<https://hostname.example.com:9443/jts/setup>.

7\. Skip through the steps until the **Configure Data Warehouse** page
and edit the JDBC location, replacing the old user name with the new
etlDbUser name which does not have DBA permissions.

8\. Change the JDBC password to the password that was set for the
etlDbUser.

9\. Click **Test Connection** and ensure you can make a connection to
your database with the etlDbUser.

10\. Complete the rest of the set up wizard, stopping at the **Configure
Data Warehouse Database** pages for any other applications registered
with the JTS, repeating steps 8 and 9 for each of them.

##### Related topics: [related-topics]

-    [Create Oracle data warehouse without DBA
    permissions](CreateOracleDataWarehouseWithoutDBAPermissions) -
    Explains how to create a brand new Oracle data warehouse without DBA
    permissions. Also has instructions for how to upgrade an Oracle data
    warehouse without DBA permissions.

##### External links: \* [IBM Knowledge Center CLM 6.0.6.1 repotools -generateWarehouseDDLScripts Reference](https://www.ibm.com/support/knowledgecenter/en/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/r_repotools_gen_dw_ddlScripts.html) [external-links-ibm-knowledge-center-clm-6.0.6.1-repotools--generatewarehouseddlscripts-reference]

-   [IBM Knowledge Center CLM 6.0.6.1 repotools
    -generateWarehouseUpgradeScripts
    Reference](https://www.ibm.com/support/knowledgecenter/en/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/r_repotools_gen_dw_upgradescripts.html)
