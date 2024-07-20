META:TOPICINFO{author="tomp" date="1513129357" format="1.1"
version="1.6"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRun"}

# IBM Quick Deployer run Install Applications process DKGRAY [ibm-quick-deployer-run-install-applications-process-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

This topic leads you through running the **Install Applications**
process to install IBM Rational solution for Collaborative Lifecycle
Management (CLM) or IoT Continuous Engineering (CE) solution
applications onto your server system.

## Prepare the target system

Before you run the UrbanCode Deploy **Install Applications** application
process, you must set the default LDAP, user, and database parameters.
You can set these parameters when you run the
[installer](IBMQuickDeployerInstallingIntoUCD) by entering the values in
the ldap.properties, userCreds.properties, and database.properties
files, which are included in the Quick Deployer package. Alternatively,
you can set the parameters by running the following application
processes:

-   **Change Default LDAP Parameters** application process - [Change the
    default LDAP
    parameters](IBMQuickDeployerChangeDefaultLDAPParameters)
-   **Change Default User Parameters** application process - [Change the
    default user
    parameters](IBMQuickDeployerChangeDefaultUserParameters)
-   **Change Default DB2 Database Parameters** application process -
    [Change default DB2 database
    parameters](IBMQuickDeployerChangeDefaultDB2Parameters)
-   **Change Default Oracle Database Parameters** application process -
    [Change default Oracle database
    parameters](IBMQuickDeployerChangeDefaultOracleParameters)
-   **Change Default SQL Server Database Parameters** application
    process - [Change default SQL Server database
    parameters](IBMQuickDeployerChangeDefaultSQLServerParameters)

Quick Deployer stores the LDAP, user, and database parameter values in
the Rational_QD_SystemPre-Requisite_60x component. To permanently store
an updated set of these parameter values in the
Rational_QD_SystemPre-Requisite_60x component, see [IBM Quick Deployer
updating Rational_QD_SystemPre-Requisite_60x\* component
parameters](IBMQuickDeployerUpdatingSystemPreReqParameters).

## Install the applications

1\. This process cannot be restarted; therefore, create a snapshot of
the target VMs before proceeding. 1. Open application
**Rational_QD_60x** and click **Run Process** against the target
environment.

1\. When the **Run Process** window opens: a. Select process **Install
Applications**. a. Set **Admin user name** and **Admin user password**
to the credentials of the administrator account defined on the LDAP
Server. a. Set **enableIFIX** to **TRUE** if you want to install a fix
pack. a. Set **RUN_JTS_SCRIPTED_SETUP** to **Y** if you want Jazz Team
Server setup to be run by the automation. a. Set **IMPORT_LDAP_USERS**
to **Y** if you want the users defined on the LDAP server to be imported
into Jazz Team Server by the automation. (RUN_JTS_SCRIPTED_SETUP must be
set to Y) a. Set **MTM_SAMPLE** to **Y** if you want the Money That
Matters (MTM) sample deployed by the automation. (RUN_JTS_SCRIPTED_SETUP
must be set to Y) a. Set **AppServer** to **was** or **liberty** a. Set
**EnableCM** to **TRUE** if you want to activate **Configuration
Management**. If you set this to **TRUE**, you must also enter a value
for **CMActivationKey**. a. Set **EnableNTPclock** to **TRUE** to
connect to the clock specified during configuration. If you set this to
**TRUE**, you must also enter a value for \*NTPclock". a. If you use a
prefix to LDAP user names to form the distinguished name (DN), set
**Prefix_LDAP**. a. Set **DBVendor** to **db2**, **oracle**, or
**sqlserver**. a. Set **appMediaRoot** to match the version of CLM or CE
you wish to install. a. If **enableIFIX** is **TRUE**, set
**CLMiFixVersion** to match the CLM version and fix pack that you want
to install. Make sure that the appMediaRoot version and the iFixVersion
match. a. If **enableIFIX** is **TRUE**, set **DMiFixVersion** and / or
**DMMSiFixVersion** to match the DM version and fix pack that you want
to install. Make sure that the appMediaRoot version and the iFixVersions
match. If you select DM, and DMMS fix packs make sure that you specify
the same version for the **DMiFixVersion** and **DMMSiFixVersion** fix
packs. a. If **AppServer** is **was** then set **wasJavaSDKVersion** to
**bundled6**, **7.1** or **bundled8** a. If **DBVendor** is **oracle**
then set **oracleVersion** to **12.1** or **12.2**

1\. Wait for the process to complete

## Post install

If the process was successful, you can access the Jazz applications by
using the fully qualified domain name of the IHS server on port 9443
followed by the context root and page name of the application. For
example:

<https://:9443/jts/admin> <https://:9443/ccm/admin>
<https://:9443/ccm/web> <https://:9443/qm/admin> ...

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="run-request.png" attachment="run-request.png"
attr="h" comment="" date="1512139955" path="run-request.png"
size="49693" user="ktessier" version="1"}
META:FILEATTACHMENT{name="run-install2v21.png"
attachment="run-install2v21.png" attr="h" comment="" date="1512139977"
path="run-install2v21.png" size="58122" user="ktessier" version="1"}
META:FILEATTACHMENT{name="run-log2.png" attachment="run-log2.png"
attr="h" comment="" date="1512140001" path="run-log2.png" size="55492"
user="ktessier" version="1"} META:TOPICMOVED{by="ktessier"
date="1513020408"
from="Deployment.IBMQuickDeployerRunInstallApplicationsProcessV21"
to="Deployment.IBMQuickDeployerRunInstallApplicationsProcess"}
