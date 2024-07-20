META:TOPICINFO{author="dcoffin" date="1606146806" format="1.1"
reprev="1.14" version="1.14"}
META:TOPICPARENT{name="ConfiguringAndTuningOracle"}

# Create Oracle data warehouse without DBA permissions [create-oracle-data-warehouse-without-dba-permissions]

DKGRAY Authors: Main.MichaelAfshar, Main.AlannaZito Build basis: CLM
version 5.x and later ENDCOLOR

TOC{title="Page contents"}

You can create the Oracle data warehouse table spaces without having the
DBA permissions. This is achieved by using repository tools command.

## Creating data warehouse

### Before you begin

Before you create the data warehouse, ensure that Jazz Team Server
database is created and configured. Click **Test Connection** in the
wizard to ensure that you can make a connection to your database.

To create the data warehouse do these steps:

1\. Start Jazz Team Server and log into
<https://hostname.example.com:9443/jts/setup>.

2\. Skip through the steps until the **Configure Data Warehouse** page
and enter the following values:

-   Select Oracle from the Database Vendor list
-   Select JDBC for connection type
-   Enter your JDBC location
-   Enter your JDBC password
-   Enter the database table space folder

3\. Click **Test Connection** and ensure you can make a connection to
your database.

4\. Select the **I do not wish to configure the data warehouse at this
time** check box and then click **Next** to go to the next page. This
action saves the preferences that you entered to the Jazz Team Server
teamserver.properties file.

5\. Stop Jazz Team Server.

6\. To generate the scripts go to JTS_Install_Dir/server and run the
following command. Replace user ID and user password with your etlDbUser
user ID and password:repotools-jts -generateWarehouseDDLScripts
additionalOptions="noAdmin;etlDbUser:;defaultPsswd:" The
`additionalOptions` parameters include:

-   `noAdmin` (required): Indicates that the generated scripts can be
    run without DBA privileges.
-   `etlDbUser` (required): The user ID of the database user that is
    used to connect to the data warehouse and run the ETL jobs from CLM.
    This user does not need to already exist in order to generate the
    scripts and also does not require to have DBA privileges.
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
-   `trsPsswd` (optional, new since 7.0.3): The password to be assigned
    to the automatically created data warehouse user. This value must be
    provided if a default password is not specified.
-   `assetPsswd` (optional, not required in 7.0.3 and later): The
    password to be assigned to the automatically created data warehouse
    user. This value must be provided if a default password is not
    specified.
-   `schkPsswd` (optional, not required in 7.0.3 and later): The
    password to be assigned to the automatically created data warehouse
    user. This value must be provided if a default password is not
    specified.

The command produces the following script files in the
repotools-jts_generateWarehouseDDLScripts.out/oracle directory:

-   1-setupCoreSpace.sql
-   2-createCoreSchema.sql
-   3-grantCoreSchemaReadAccess.sql
-   4-populateDateDimension.sql
-   5-setupCalmSpace.sql
-   6-createCalmSchema.sql
-   7-grantCalmSchemaReadAccess.sql
-   additionalSteps.sql

|  |
|----|
| **Note:** If you have more than one Oracle database in your environment, in order for the script to locate the correct database you must create an environment variable called ORACLE_SID and set its value to your database name. For example, `SET ORACLE_SID=CLMDB` |

|  |
|----|
| **Note:** You might also encounter some error messages about missing RPTUSER. These error messages can safely be ignored. |

7\. Open SQL Plus and run the following scripts in this order. DBA
privileges required:

-   1-setupCoreSpace.sql
-   5-setupCalmSpace.sql

8\. If the etlDBUser does not already exist, do these steps to create
it. DBA privileges required:

1.  Open additionalSteps.sql for editing.
2.  Replace the password with an actual password.
3.  Save and close the additionalSteps.sql file.
4.  Run the additionalSteps.sql script in SQL Plus. The script will
    create a non-DBA user with the required permissions for running the
    ETL jobs from CLM.

9\. In SQL Plus run these scripts in these order. DBA privileges not
required.

-   2-createCoreSchema.sql
-   3-grantCoreSchemaReadAccess.sql
-   4-populateDateDimension.sql
-   6-createCalmSchema.sql
-   7-grantCalmSchemaReadAccess

10\. Start Jazz Team Server.

11\. Return to the jts/setup wizard and on the Configure Data Warehouse
page, clear the **I do not wish to configure the data warehouse at this
time**. Ensure that the user in the connection string (JDBC location) is
the same as the etlDBUser that was specified when generating the
scripts. Test the connection, and complete the set up wizard.

## Upgrading data warehouse

### Before you begin

Make sure the following conditions are met before starting the data
warehouse upgrade: \* The Jazz Team Server teamserver.properties file
has been migrated from the previous version and has the data warehouse
connection details. \* **The data warehouse tables have not been
upgraded.** \* **Note**: Do not make any changes to the connection
details or to database user privileges before generating the scripts and
upgrading the data warehouse. After the upgrade is complete, any
required changes can be made.

### Procedures 1. Go to go to JTS_Install_Dir/server and run the `repotools-jts generateWarehouseUpgradeScripts` command with the `additionalOptions` parameter. For information about the `additionalOptions` parameters, see the section in the beginning of this document.

1.  Optional (If you are upgrading to version 6.0.1, this step is
    required): DBA privilege is required for this step. If the data
    warehouse users have not already been unlocked and assigned
    passwords, run the `additionalSteps.sql` script to unlock them. Note
    that the users will already be unlocked if the data warehouse was
    created using the scripts generated with `noAdmin` parameter.
2.  DBA privilege is required for this step when upgrading to version
    7.0.3 or later for the first time. Otherwise, DBA privilege is not
    required for this step. Run the following scripts in this order:
    -   1-upgradeCoreSchema.sql
    -   2-populateDateDimension.sql
    -   3-upgradeCalmSchema.sql
    -   4-grantCoreSchemaReadAccess.sql
    -   5-grantCalmSchemaReadAccess
3.  Ensure that the connection string for the data warehouse in Jazz
    Team Server and the applications references the same etlDBUser that
    was specified when generating the scripts.

**Note:** It's possible that some of the sql scripts in the above list
may be empty. This is because different things need to be upgraded by
the scripts in different versions of the product, all the script files
get generated even if there is no content in some of them.

##### External links: \* [IBM Knowledge Center CLM 6.0.6.1 repotools -generateWarehouseDDLScripts Reference](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/r_repotools_gen_dw_ddlScripts.html) [external-links-ibm-knowledge-center-clm-6.0.6.1-repotools--generatewarehouseddlscripts-reference]

-   [IBM Knowledge Center CLM 6.0.6.1 repotools
    -generateWarehouseUpgradeScripts
    Reference](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/r_repotools_gen_dw_upgradescripts.html)

##### Additional contributors: Main.RosaNaranjo [additional-contributors-main.rosanaranjo]
