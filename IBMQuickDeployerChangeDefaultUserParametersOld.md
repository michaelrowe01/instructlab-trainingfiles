META:TOPICINFO{author="ktessier" date="1501278328" format="1.1"
reprev="1.19" version="1.19"}
META:TOPICPARENT{name="IBMQuickDeployerSetupAndRunOld"}

# IBM Quick Deployer change default user parameters DKGRAY [ibm-quick-deployer-change-default-user-parameters-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

Prior to running the UCD **Install Applications** application process
you must run the **Change Default User Parameters** application process.
Running the **Change Default User Parameters** application process
allows you to change the default user / password combinations to match
your system. Once you know the user / password combinations for your
system you can permanently change the default values by following the
instruction in the [Modify Change Default User Parameters
Defaults](IBMQuickDeployerModifyChangeDefaultUserParametersDefaults)
wiki page.

## Change default user parameters 1. Open application **Rational_QD_60x** and run process **Change Default User Parameters** on the target environment.

1\. If you fixed the component versions on the process you will not be
prompted to choose versions. If offered to choose the component
versions, then select Latest Available. 1. Modify the process property
default values to match your System. DB2 username restrictions / rules
are highlighted below, make sure you follow these rules when specifying
all of the DB2 user names:

Must be lowercase letters (a-z), numbers (0-9), and the underscore
character(\_) Must not start with a number or underscore Cannot be
longer than eight characters Cannot begin with IBM, SYS, SQL, or a
number Cannot be USERS, ADMINS, GUESTS, PUBLIC or LOCAL

A full up to date set of restrictions can be found at [DB2 Version
10.5 - Installing DB2 Servers (page 42 for user ID
restrictions)](http://public.dhe.ibm.com/ps/products/db2/info/vr105/pdf/en_US/DB2InstallingServers-db2ise1051.pdf)
The properties are as follows \* **mediaUser** : user that accesses an
http media server *Default* : not used \* **mediaPassword** : password
for mediaUser *Default* : not used \* **IHSServerKeyStorePassword** : -
password for the IHS certificate keystore *Default* : ihspassword \*
**DB2InstanceUser** : this is the DB2 instance user (several databases
are stored in an instance) *Default* : db2inst1 \*
**DB2InstancePassword** : password for DB2InstanceUser *Default* :
db2password \* **DB2InstanceUserGroup** : group to contain the
DB2InstanceUser (will be created) *Default* : db2iadm1 \* **DB2DASUser**
: this is the DB2 administration server user (refer to DB2InstanceUser
rules) *Default* : dasusr1 \* **DB2DASUserGroup** : group to contain the
DB2DASUser (will be created) *Default* : dasadm1 \* **DB2FenceUser** :
this is the DB2 fenced user (refer to DB2InstanceUser rules) *Default* :
db2fenc1 \* **DB2FenceUserGroup** : group to contain the DB2FenceUser
(will be created) *Default* : db2fadm1 \* **OSUserName** : user used to
install and run IM, WAS, IHS & jazzApps *Default* : osusername \*
**OSUserGroup** : group to contain the OSUserName *Default* :
osusergroup \* **OSUserPassword** : password for OSUserName *Default* :
osuserpassword

1\. Click on **Submit** and wait for the process to run to completion

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="CDUP1.png" attachment="CDUP1.png" attr="h"
comment="run process" date="1443707333" path="CDUP1.png" size="47435"
user="kenneth" version="1"} META:FILEATTACHMENT{name="CDUP2.png"
attachment="CDUP2.png" attr="h" comment="select Latest Available"
date="1443707351" path="CDUP2.png" size="39127" user="kenneth"
version="1"} META:FILEATTACHMENT{name="CDUP3.png" attachment="CDUP3.png"
attr="h" comment="wait for completion" date="1443707370"
path="CDUP3.png" size="26687" user="kenneth" version="1"}
META:FILEATTACHMENT{name="CDUP1a.png" attachment="CDUP1a.png" attr="h"
comment="run process" date="1462363471" path="CDUP1a.png" size="51470"
user="kenneth" version="1"} META:TOPICMOVED{by="ktessier"
date="1501274876"
from="Deployment.IBMQuickDeployerChangeDefaultUserParameters"
to="Deployment.IBMQuickDeployerChangeDefaultUserParametersOld"}
