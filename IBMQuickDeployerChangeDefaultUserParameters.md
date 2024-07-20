META:TOPICINFO{author="ktessier" date="1513112163" format="1.1"
version="1.10"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRun"}

# IBM Quick Deployer change default user parameters DKGRAY [ibm-quick-deployer-change-default-user-parameters-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

Before you run the UrbanCode Deploy **Install Applications** application
process, you must set the default user credentials. You can set these
parameters when you run the
[installer](IBMQuickDeployerInstallingIntoUCD) by entering the values in
the userCreds.properties file, which is included in the Quick Deployer
package. Alternatively, you can set the parameters by running the
**Change Default User Parameters** application process.

Once you know the user / password combinations for your system, you can
permanently change the default values by following the instructions in
the [Modify Change Default User Parameters
Defaults](IBMQuickDeployerModifyChangeDefaultUserParametersDefaults)
wiki page.

## Change default user parameters 1. Open application **Rational_QD_60x** and run process **Change Default User Parameters** on the target environment.

1\. If you fixed the component versions on the process you will not be
prompted to choose versions. If offered to choose the component
versions, then select Latest Available. 1. Modify the process property
default values to match your System. DB2 username restrictions / rules
are highlighted below, make sure you follow these rules when specifying
all of the DB2 user names:

-   Windows: Must be uppercase or lowercase letters (A-Za-z), numbers
    (0-9), and the underscore character. Linux: Must be lowercase
    letters (a-z), numbers (0-9), and the underscore character.
-   Must not start with a number or underscore
-   Windows: Cannot be longer than 30 characters. Linux: Cannot be
    longer than eight characters.
-   Cannot begin with IBM, SYS, SQL, or a number
-   Cannot be USERS, ADMINS, GUESTS, PUBLIC or LOCAL

A full up to date set of restrictions can be found in the *Installing
DB2 Servers* topic at [IBM Knowledge Center: DB2 for Linux UNIX and
Windows](https://www.ibm.com/support/knowledgecenter/SSEPGG) The
properties are as follows \* **IHSServerKeyStorePassword** : - password
for the IHS certificate keystore *Default* : ihspassword \*
**DB2InstanceUser** : this is the DB2 instance user (several databases
are stored in an instance) *Default* : db2inst1 (*linux*) db2admin
(*Windows*) \* **DB2InstancePassword** : password for DB2InstanceUser
*Default* : db2password \* **DB2InstanceUserGroup** : group to contain
the DB2InstanceUser (will be created) *Default* : db2iadm1 (*linux*)
DB2ADMNS (*Windows*) \* **DB2DASUser** : this is the DB2 administration
server user (refer to DB2InstanceUser rules) *Default* : dasusr1
(*linux*) db2admin (*Windows*) \* **DB2DASUserGroup** : group to contain
the DB2DASUser (will be created) *Default* : dasadm1 (*linux*) DB2ADMNS
(*Windows*) \* **DB2FenceUser** : this is the DB2 fenced user (refer to
DB2InstanceUser rules) (not required on Windows) *Default* : db2fenc1 \*
**DB2FenceUserGroup** : group to contain the DB2FenceUser (will be
created) (not required on Windows) *Default* : db2fadm1 \*
**OSUserName** : user used to install and run IM, WAS, IHS & jazzApps
*Default* : osusername \* **OSUserGroup** : group to contain the
OSUserName *Default* : osusergroup \* **OSUserPassword** : password for
OSUserName *Default* : osuserpassword \* **oracleOSUserName** : this is
the os user that will run Oracle database *Default* : orauser \*
**oracleOSUserPassword** : the oracle user's password *Default* :
oraclePassword \* **oracleOSUserPrimaryGroup** : the primary group for
the oracle OS user (not required on Windows) *Default* : oinstall \*
**oracleOSUserAdditionalGroup** : the additional group for oracle OS
user (not required on Windows) *Default* : dba \* **oracleALLPassword**
: the password that is to be used for all schemas in the starter
database *Default* : oracleALLPassword \* **oracleSYSPassword** : the
SYS password for the starter database *Default* : oracleSYSPassword \*
**oracleSYSTEMPassword** : the SYSTEM password for the starter database
*Default* : oracleSYSTEMPassword \* **oracleDBSNMPPassword** : the
DBSNMP password for the starter database *Default* :
oracleDBSNMPPassword \* **oraclePDBADMINPassword** : the PDBADMIN
password required for the creation of a Pluggable Database in the
Container Database if a Pluggable database is created *Default* :
oraclePDBADMINPassword \* **oracleDBUsersPassword** : the password for
all database users (e.g. user is jtsUser) *Default* :
oracleDBUsersPassword \* **sqlSAPassword** : SQL Server SA password.
Required only for SQL Server installations *Default* : sqlSAPassword \*
**sqlDBUsersPassword** : the password for all database users (e.g. user
is jtsUser) *Default* : sqlDBUsersPassword

1\. Click on **Submit** and wait for the process to run to completion

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="CDUP3.png" attachment="CDUP3.png" attr="h"
comment="" date="1498842911" path="CDUP3.png" size="26687"
user="ktessier" version="1"} META:FILEATTACHMENT{name="CDUP2.png"
attachment="CDUP2.png" attr="h" comment="" date="1498842925"
path="CDUP2.png" size="39127" user="ktessier" version="1"}
META:FILEATTACHMENT{name="CDUP1a.png" attachment="CDUP1a.png" attr="h"
comment="" date="1498842937" path="CDUP1a.png" size="51470"
user="ktessier" version="1"} META:FILEATTACHMENT{name="CDUP1aV20.png"
attachment="CDUP1aV20.png" attr="h" comment="Running Change Default User
Parameters process" date="1501265387" path="CDUP1aV20.png" size="31221"
user="ktessier" version="1"} META:TOPICMOVED{by="ktessier"
date="1501274968"
from="Deployment.IBMQuickDeployerChangeDefaultUserParametersV20"
to="Deployment.IBMQuickDeployerChangeDefaultUserParameters"}
