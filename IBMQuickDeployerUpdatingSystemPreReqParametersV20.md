META:TOPICINFO{author="ktessier" date="1513021528" format="1.1"
version="1.12"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRun"}

# IBM Quick Deployer updating Rational_QD_SystemPre-Requisite_60x\* component parameters DKGRAY [ibm-quick-deployer-updating-rational_qd_systempre-requisite_60x-component-parameters-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

Before you run the UrbanCode Deploy **Install Applications** application
process, you must set the default LDAP, user credentials, and database
parameters. You can set these parameters when you run the
[installer](IBMQuickDeployerInstallingIntoUCD) by entering the values in
the ldap.properties, userCreds.properties, and database.properties
files, which are included in the Quick Deployer package. Quick Deployer
stores the LDAP, user, and database parameter values in the
Rational_QD_SystemPre-Requisite_60x component. This topic describes how
to permanently store an updated set of these parameter values in the
Rational_QD_SystemPre-Requisite_60x component by running the installer
again and specifying the COMPONENT_ONLY argument. The COMPONENT_ONLY
argument directs the installer to update the
Rational_QD_SystemPre-Requisite_60x component but not perform any of the
other installation tasks.

Alternatively, you can set the parameters by running the following
application processes:

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

To run the above application processes, you must have an environment.
For details on creating an environment, see [UCD environment
construction](IBMQuickDeployerEnvironmentConstruction). When you run
these application processes, they generate the following properties
files, which capture the settings on the target environment:

-   /IBMQD/UCDComponents/AutomationPrep/DatabaseParameters/DBParameter.properties
-   /IBMQD/UCDComponents/AutomationPrep/DatabaseParameters/oracleParameter.properties
-   /IBMQD/UCDComponents/AutomationPrep/UserParameters/userCreds.properties
-   /IBMQD/UCDComponents/AutomationPrep/CustomLDAP/Custom_LDAPSecurity.properties

You can copy these properties files from a VM in the target environment
to the directory where you run the installer, make any additional
changes to them, edit the qd.properties file to point to them, and then
run the installer with the COMPONENT_ONLY argument.

## Update UCD Rational_QD_SystemPre-Requisite_60x component

1.  Edit the parameter values in one or more of the ldap.properties,
    userCreds.properties, database.properties, and qd.properties files.
    **Note**: Check each of the properties files to ensure that they
    contain the desired settings so that you do not inadvertently update
    settings by using an old version of a properties file. For example,
    after the first time that you run the installer to install the Quick
    Deployer application into IBM UrbanCode Deploy, you might change
    some parameters by running one or more of the application processes
    listed above. When you run the installer again, as shown below, it
    updates those application processes based on the settings in the
    properties files. A scenario where you might inadvertently introduce
    unwanted changes to an application process is as follows: When you
    run the installer the first time, you decide not to provide a link
    in the qd.properties file to the ldap.properties file. Instead,
    after the installer completes successfully, you provide the default
    LDAP paramters by running the **Change Default LDAP Parameters**
    application process. Later, you decide to run the installer again,
    as shown below, after changing one setting in the qd.properties
    file. Because you did not provide a link to the ldap.properties file
    in the qd.properties file the first time that you ran the installer,
    you must do so now, and the ldap.properties file must contain the
    same settings that you previously specified when you ran the
    **Change Default LDAP Parameters** application process. Otherwise,
    the installer removes your parameter settings from the **Change
    Default LDAP Parameters** application process.
2.  Run the [installer](IBMQuickDeployerInstallingIntoUCD) and specify
    the COMPONENT_ONLY argument, which directs the installer to update
    the Rational_QD_SystemPre-Requisite_60x component but not perform
    any of the other installation tasks. For example:

C:\qd\>java -jar install.jar C:\qd.properties COMPONENT_ONLY Publishing
new component. Publishing component Rational_QD_SystemPre-Requisite_604
version 20170609-1121. Success Component version creation successful.
Created and published Rational_QD_SystemPre-Requisite_604 20170609-1121.

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:TOPICMOVED{by="ktessier" date="1513021528"
from="Deployment.IBMQuickDeployerUpdatingSystemPreReqParameters"
to="Deployment.IBMQuickDeployerUpdatingSystemPreReqParametersV20"}
