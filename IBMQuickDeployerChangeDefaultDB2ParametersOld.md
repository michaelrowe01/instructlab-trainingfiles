META:TOPICINFO{author="ktessier" date="1501278327" format="1.1"
reprev="1.21" version="1.21"}
META:TOPICPARENT{name="IBMQuickDeployerSetupAndRunOld"}

# IBM Quick Deployer change default DB2 database parameters DKGRAY [ibm-quick-deployer-change-default-db2-database-parameters-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

The values contained in the default database parameters are used to
configure the connections between the installed CLM applications and
their individual databases. If you are going to use the Quick Deployer
installed DB2 database then there is no need to change them prior to
running the UCD application **Install Applications** process. However,
you should have your database administrator review the configuration to
make sure it conforms to internal security and reliability policies. If
you are going to use an existing DB2 database instance then you need to
ensure that the default database parameters are updated to match the
configuration used by your database instance. To do this follow the
instructions in this topic.

## Change default database parameters 1. Open application **Rational_QD_60x**, click **Environments**, then click the **Request Process** icon for the target environment. 1. In the Process field, select **Change Default DB2 Parameters**.

1\. If you fixed the component versions on the process you will not be
prompted to choose versions. If offered to choose the component
versions, then select Latest Available.

1\. Modify the process property default values to match your database.
The DB2 databases are created using this command **db2 CREATE DATABASE
\${app}DBName \$create{app}DBOption** which is populated using these
property values: eg db2 CREATE DATABASE **\$jtsDBName
\$createjtsDBOption** The properties are as follows \*
**createjtsDBOption** : command options for creating the jts database
*Default* : "ON '/db2fs' DBPATH ON '/db2fs' USING CODESET UTF-8
TERRITORY EN PAGESIZE 16384" \* **jtsDBName** : name of the jts database
*Default* : jtsDB \* **createdwDBOption** : command options for creating
the datawarehouse database *Default* : "ON '/db2fs' DBPATH ON '/db2fs'
USING CODESET UTF-8 TERRITORY EN PAGESIZE 16384" \* **dwDBName** : name
of the datawarehouse database *Default* : dwDB \* **createccmDBOption**
: command options for creating the ccm database *Default* : "ON '/db2fs'
DBPATH ON '/db2fs' USING CODESET UTF-8 TERRITORY EN PAGESIZE 16384" \*
**ccmDBName** : name of the ccm database *Default* : ccmDB \*
**createqmDBOption** : command options for creating the qm database
*Default* : "ON '/db2fs' DBPATH ON '/db2fs' USING CODESET UTF-8
TERRITORY EN PAGESIZE 16384" \* **qmDBName** : name of the qm database
*Default* : qmDB \* **creatermDBOption** : command options for creating
the rm database *Default* : "ON '/db2fs' DBPATH ON '/db2fs' USING
CODESET UTF-8 TERRITORY EN PAGESIZE 16384" \* **rmDBName** : name of the
rm database *Default* : rmDB \* **creategcDBOption** : command options
for creating the gc database *Default* : "ON '/db2fs' DBPATH ON '/db2fs'
USING CODESET UTF-8 TERRITORY EN PAGESIZE 16384" \* **gcDBName** : name
of the gc database *Default* : gcDB \* **createdccDBOption** : command
options for creating the dcc database *Default* : "ON '/db2fs' DBPATH ON
'/db2fs' USING CODESET UTF-8 TERRITORY EN PAGESIZE 16384" \*
**dccDBName** : name of the dcc database *Default* : dccDB \*
**createrelmDBOption** : command options for creating the relm database
*Default* : "ON '/db2fs' DBPATH ON '/db2fs' USING CODESET UTF-8
TERRITORY EN PAGESIZE 16384" \* **relmDBName** : name of the relm
database *Default* : relmDB \* **createlqeDBOption** : command options
for creating the lqe database *Default* : "ON '/db2fs' DBPATH ON
'/db2fs' USING CODESET UTF-8 TERRITORY EN PAGESIZE 32768" \*
**lqeDBName** : name of the lqe database *Default* : lqeDB \*
**createldxDBOption** : command options for creating the ldx database
*Default* : "ON '/db2fs' DBPATH ON '/db2fs' USING CODESET UTF-8
TERRITORY EN PAGESIZE 32768" \* **ldxDBName** : name of the ldx database
*Default* : ldxDB \* **DB2InstancePort** : database connection port
*Default* : 50001

1\. Click on **Submit** and wait for the process to run to completion

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="CDDP1.png" attachment="CDDP1.png" attr="h"
comment="run process" date="1443704420" path="CDDP1.png" size="53560"
user="kenneth" version="1"} META:FILEATTACHMENT{name="CDDP2.png"
attachment="CDDP2.png" attr="h" comment="select Latest Available"
date="1443704442" path="CDDP2.png" size="38984" user="kenneth"
version="1"} META:FILEATTACHMENT{name="CDDP3.png" attachment="CDDP3.png"
attr="h" comment="wait for completion" date="1443704478"
path="CDDP3.png" size="18973" user="kenneth" version="1"}
META:FILEATTACHMENT{name="change-db-parameters.png"
attachment="change-db-parameters.png" attr="h" comment="Clicking Request
Process for environment" date="1481398507"
path="change-db-parameters.png" size="14756" user="ktessier"
version="1"} META:FILEATTACHMENT{name="change-db2-parameters.png"
attachment="change-db2-parameters.png" attr="h" comment="Selecting
Change Default DB2 Parameters" date="1481398544"
path="change-db2-parameters.png" size="51708" user="ktessier"
version="1"} META:TOPICMOVED{by="ktessier" date="1501277518"
from="Deployment.IBMQuickDeployerChangeDefaultDB2Parameters"
to="Deployment.IBMQuickDeployerChangeDefaultDB2ParametersOld"}
