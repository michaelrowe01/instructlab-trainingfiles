META:TOPICINFO{author="ktessier" date="1501278328" format="1.1"
reprev="1.6" version="1.6"}
META:TOPICPARENT{name="IBMQuickDeployerSetupAndRunOld"}

# IBM Quick Deployer change default Oracle database parameters DKGRAY [ibm-quick-deployer-change-default-oracle-database-parameters-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

The values contained in the default database parameters are used to
configure the connections between the installed CLM applications and
their individual databases. If you are going to use the Quick Deployer
installed Oracle database then there is no need to change them prior to
running the UCD application **Install Applications** process. However,
you should have your database administrator review the configuration to
make sure it conforms to internal security and reliability policies. If
you are going to use an existing Oracle database server, then you need
to ensure that the **instance** is created and the default database
parameters are updated to match the configuration used by your database
instance. To do this follow the instructions in this topic.

## Change default database parameters 1. Open application **Rational_QD_60x**, click **Environments**, then click the **Request Process** icon for the target environment. 1. In the Process field, select **Change Default Oracle Parameters**.

1\. If you fixed the component versions on the process you will not be
prompted to choose versions. If offered to choose the component
versions, then select Latest Available.

1\. Modify the process property default values to match your database.
The Oracle user table space are created using this command **CREATE
BIGFILE TABLESPACE \$TSName DATAFILE '\${TS_path}/\${appName}.dbf'
\$createTSOption** which is populated using these property values: eg
CREATE BIGFILE TABLESPACE **\$oraclejtsTableSpace DATAFILE
\$oracleDBStorage_Home/jts.dbf \$oraclejtsCreateTS** The Oracle user
temporary table space are created using this command **CREATE TEMPORARY
TABLESPACE \$TEMPTSName TEMPFILE '\${TS_path}/\${appName}temp.dbf'
\$createTEMPTSOption** which is populated using these property values:
eg CREATE TEMPORARY TABLESPACE **\$oraclejtsTempTableSpace TEMPFILE
\$oracleDBStorage_Home/jtstemp.dbf \$oraclejtsCreateTempTS** The Oracle
users are created using this command **CREATE USER \$DBUser IDENTIFIED
BY \$DBUsersPassword DEFAULT TABLESPACE \$TSName QUOTA UNLIMITED ON
\$TSName TEMPORARY TABLESPACE \$TEMPTSName** which is populated using
these property values: eg CREATE USER \$oraclejtsUser IDENTIFIED BY
\$oracleDBUsersPassword DEFAULT TABLESPACE \$oraclejtsTableSpace QUOTA
UNLIMITED ON \$oraclejtsTableSpace TEMPORARY TABLESPACE
\$oraclejtsTempTableSpace\* Grant oracle user this command **GRANT
\$UserGrantOption TO \$DBUser** which is populated using these property
values: eg GRANT \$oraclejtsGrantOption TO **\$UserGrantOption** The
properties are as follows \* **oracleDBStorage_Home** : oracle database
storage location *Default*:\${p:LINUX_UCD_ROOT}/database/dbstorage \*
**oracleInstanceName** : oracle instance name, the instance must already
existed *Default*:CLMINST \* **oraclePort** : oracle port *Default*:1521
\* **oraclejtsTableSpace** : jts table space name *Default* : jtsTS \*
**oraclejtsCreateTS** : command option for creating jts table space
*Default* : "SIZE 1G AUTOEXTEND ON EXTENT MANAGEMENT LOCAL AUTOALLOCATE"
\* **oraclejtsTempTableSpace** : jts temporary table space name
*Default* : jtsTStemp \* **oraclejtsCreateTempTS** : command option for
creating jts temporary table space *Default* : "SIZE 20M AUTOEXTEND ON
EXTENT MANAGEMENT LOCAL UNIFORM SIZE 1M" \* **oraclejtsUser** : jts user
name *Default* : jtsUSER \* **oraclejtsGrantOption** : command option
for granting jts user option *Default* : "CREATE PROCEDURE, CREATE
SESSION, CREATE TABLE, CREATE VIEW" \* **oracleccmTableSpace** : ccm
table space name *Default* : ccmTS \* **oracleccmCreateTS** : command
option for creating ccm table space *Default* : "SIZE 1G AUTOEXTEND ON
EXTENT MANAGEMENT LOCAL AUTOALLOCATE" \* **oracleccmTempTableSpace** :
ccm temporary table space name *Default* : ccmTStemp \*
**oracleccmCreateTempTS** : command option for creating ccm temporary
table space *Default* : "SIZE 20M AUTOEXTEND ON EXTENT MANAGEMENT LOCAL
UNIFORM SIZE 1M" \* **oracleccmUser** : ccm user name *Default* :
ccmUSER \* **oracleccmGrantOption** : command option for granting ccm
user option *Default* : "CREATE PROCEDURE, CREATE SESSION, CREATE TABLE,
CREATE VIEW" \* **oracleqmTableSpace** : qm table space name *Default* :
qmTS \* **oracleqmCreateTS** : command option for creating qm table
space *Default* : "SIZE 1G AUTOEXTEND ON EXTENT MANAGEMENT LOCAL
AUTOALLOCATE" \* **oracleqmTempTableSpace** : qm temporary table space
name *Default* : qmTStemp \* **oracleqmCreateTempTS** : command option
for creating qm temporary table space *Default* : "SIZE 20M AUTOEXTEND
ON EXTENT MANAGEMENT LOCAL UNIFORM SIZE 1M" \* **oracleqmUser** : qm
user name *Default* : qmUSER \* **oracleqmGrantOption** : command option
for granting qm user option *Default* : "CREATE PROCEDURE, CREATE
SESSION, CREATE TABLE, CREATE VIEW" \* **oraclermTableSpace** : rm table
space name *Default* : rmTS \* **oraclermCreateTS** : command option for
creating rm table space *Default* : "SIZE 1G AUTOEXTEND ON EXTENT
MANAGEMENT LOCAL AUTOALLOCATE" \* **oraclermTempTableSpace** : rm
temporary table space name *Default* : rmTStemp \*
**oraclermCreateTempTS** : command option for creating rm temporary
table space *Default* : "SIZE 20M AUTOEXTEND ON EXTENT MANAGEMENT LOCAL
UNIFORM SIZE 1M" \* **oraclermUser** : rm user name *Default* : rmUSER
\* **oraclermGrantOption** : command option for granting rm user option
*Default* : "CREATE PROCEDURE, CREATE SESSION, CREATE TABLE, CREATE
VIEW" \* **oraclegcTableSpace** : gc table space name *Default* : gcTS
\* **oraclegcCreateTS** : command option for creating gc table space
*Default* : "SIZE 1G AUTOEXTEND ON EXTENT MANAGEMENT LOCAL AUTOALLOCATE"
\* **oraclegcTempTableSpace** : gc temporary table space name *Default*
: gcTStemp \* **oraclegcCreateTempTS** : command option for creating gc
temporary table space *Default* : "SIZE 20M AUTOEXTEND ON EXTENT
MANAGEMENT LOCAL UNIFORM SIZE 1M" \* **oraclegcUser** : gc user name
*Default* : gcUSER \* **oraclegcGrantOption** : command option for
granting gc user option *Default* : "CREATE PROCEDURE, CREATE SESSION,
CREATE TABLE, CREATE VIEW" \* **oracledccTableSpace** : dcc table space
name *Default* : dccTS \* **oracledccCreateTS** : command option for
creating dcc table space *Default* : "SIZE 1G AUTOEXTEND ON EXTENT
MANAGEMENT LOCAL AUTOALLOCATE" \* **oracledccTempTableSpace** : dcc
temporary table space name *Default* : dccTStemp \*
**oracledccCreateTempTS** : command option for creating dcc temporary
table space *Default* : "SIZE 20M AUTOEXTEND ON EXTENT MANAGEMENT LOCAL
UNIFORM SIZE 1M" \* **oracledccUser** : dcc user name *Default* :
dccUSER \* **oracledccGrantOption** : command option for granting dcc
user option *Default* : "CREATE PROCEDURE, CREATE SESSION, CREATE TABLE,
CREATE VIEW" \* **oraclerelmTableSpace** : relm table space name
*Default* : relmTS \* **oraclerelmCreateTS** : command option for
creating relm table space *Default* : "SIZE 1G AUTOEXTEND ON EXTENT
MANAGEMENT LOCAL AUTOALLOCATE" \* **oraclerelmTempTableSpace** : relm
temporary table space name *Default* : relmTStemp \*
**oraclerelmCreateTempTS** : command option for creating relm temporary
table space *Default* : "SIZE 20M AUTOEXTEND ON EXTENT MANAGEMENT LOCAL
UNIFORM SIZE 1M" \* **oraclerelmUser** : relm user name *Default* :
relmUSER \* **oraclerelmGrantOption** : command option for granting relm
user option *Default* : "CREATE PROCEDURE, CREATE SESSION, CREATE TABLE,
CREATE VIEW" \* **oraclelqeTableSpace** : lqe table space name *Default*
: lqeTS \* **oraclelqeCreateTS** : command option for creating lqe table
space *Default* : "SIZE 1G AUTOEXTEND ON EXTENT MANAGEMENT LOCAL
AUTOALLOCATE" \* **oraclelqeTempTableSpace** : lqe temporary table space
name *Default* : lqeTStemp \* **oraclelqeCreateTempTS** : command option
for creating lqe temporary table space *Default* : "SIZE 20M AUTOEXTEND
ON EXTENT MANAGEMENT LOCAL UNIFORM SIZE 1M" \* **oraclelqeUser** : lqe
user name *Default* : lqeUSER \* **oraclelqeGrantOption** : command
option for granting lqe user option *Default* : "CREATE PROCEDURE,
CREATE SESSION, CREATE TABLE, CREATE VIEW" \* **oracleldxTableSpace** :
ldx table space name *Default* : ldxTS \* **oracleldxCreateTS** :
command option for creating ldx table space *Default* : "SIZE 1G
AUTOEXTEND ON EXTENT MANAGEMENT LOCAL AUTOALLOCATE" \*
**oracleldxTempTableSpace** : ldx temporary table space name *Default* :
ldxTStemp \* **oracleldxCreateTempTS** : command option for creating ldx
temporary table space *Default* : "SIZE 20M AUTOEXTEND ON EXTENT
MANAGEMENT LOCAL UNIFORM SIZE 1M" \* **oracleldxUser** : ldx user name
*Default* : ldxUSER \* **oracleldxGrantOption** : command option for
granting ldx user option *Default* : "CREATE PROCEDURE, CREATE SESSION,
CREATE TABLE, CREATE VIEW" \* **oracledmTableSpace** : dmtable space
name *Default* : dmTS \* **oracledmCreateTS** : command option for
creating dm table space *Default* : "SIZE 1G AUTOEXTEND ON EXTENT
MANAGEMENT LOCAL AUTOALLOCATE" \* **oracledmTempTableSpace** : dm
temporary table space name *Default* : dmTStemp \*
**oracledmCreateTempTS** : command option for creating dm temporary
table space *Default* : "SIZE 20M AUTOEXTEND ON EXTENT MANAGEMENT LOCAL
UNIFORM SIZE 1M" \* **oracledmUser** : dm user name *Default* : dmUSER
\* **oracledmGrantOption** : command option for granting dm user option
*Default* : "CREATE PROCEDURE, CREATE SESSION, CREATE TABLE, CREATE
VIEW" \* **oracledwTableSpace** : dwtable space name *Default* : dwTS \*
**oracledwCreateTS** : command option for creating dw table space
*Default* : "SIZE 1G AUTOEXTEND ON EXTENT MANAGEMENT LOCAL AUTOALLOCATE"
\* **oracledwTempTableSpace** : dw temporary table space name *Default*
: dwTStemp \* **oracledwCreateTempTS** : command option for creating dm
temporary table space *Default* : "SIZE 20M AUTOEXTEND ON EXTENT
MANAGEMENT LOCAL UNIFORM SIZE 1M" \* **oracledmUser** : dw user name
*Default* : dwUSER \* **oracledwGrantOption** : command option for
granting dm user option *Default* : "DBA"

1\. Click on **Submit** and wait for the process to run to completion

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="change-db-parameters.png"
attachment="change-db-parameters.png" attr="h" comment="Clicking Request
Process for environment" date="1481398778"
path="change-db-parameters.png" size="14756" user="ktessier"
version="1"} META:FILEATTACHMENT{name="CDDP2.png" attachment="CDDP2.png"
attr="h" comment="" date="1481398879" path="CDDP2.png" size="38984"
user="ktessier" version="1"} META:FILEATTACHMENT{name="CDDP3.png"
attachment="CDDP3.png" attr="h" comment="" date="1481398975"
path="CDDP3.png" size="18973" user="ktessier" version="1"}
META:FILEATTACHMENT{name="change-oracle-parameters.png"
attachment="change-oracle-parameters.png" attr="h" comment=""
date="1481751091" path="change-oracle-parameters.png" size="51542"
user="ktessier" version="1"}
META:FILEATTACHMENT{name="change-oracle-parameters1.png"
attachment="change-oracle-parameters1.png" attr="h" comment=""
date="1481751248" path="change-oracle-parameters1.png" size="51542"
user="ktessier" version="1"} META:TOPICMOVED{by="ktessier"
date="1501276170"
from="Deployment.IBMQuickDeployerChangeDefaultOracleParameters"
to="Deployment.IBMQuickDeployerChangeDefaultOracleParametersOld"}
