META:TOPICINFO{author="ktessier" date="1501856896" format="1.1"
version="1.11"} META:TOPICPARENT{name="IBMQuickDeployerOld"}

# IBM Quick Deployer setup and run (using setup script) DKGRAY [ibm-quick-deployer-setup-and-run-using-setup-script-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

The following setup procedure explains how to install, configure, and
run **IBM Quick Deployer** to deploy CLM and CE systems. The setup
information should help you with these tasks:

-   Size your system
-   Import the IBM UrbanCode Deploy application and its components
-   Import the IBM Quick Deployer scripts used by the UrbanCode Deploy
    components
-   Understand which middleware is required and get IBM Quick Deployer
    to install it
-   Configure the UrbanCode Deploy application and component processes
    to match your environment (such as user names, passwords, LDAP
    settings)
-   Optionally configure the UrbanCode Deploy application to use an
    existing IBM DB2 or Oracle database instance
-   Configure UrbanCode Deploy environments to represent the desired
    application topology
-   Run the **Install Applications** process to deploy the system

## Installation, configuration and run outline

1.  Review the [System
    requirements](IBMQuickDeployerSystemRequirementsOld).
2.  Review the [Limitations and known
    issues](IBMQuickDeployerLimitationsKnownIssuesOld).
3.  Download and extract the IBM Quick Deployer package from the
    compressed file. The package includes - [Package
    content](IBMQuickDeployerPackageContent)
    -   Application JSON file
    -   Component version .zip files
    -   Component version extract, add and update scripts
    -   Application setup scripts
    -   License files
4.  You must obtain and license the following middleware and product
    installation bits:
    -   IBM WebSphere Application Server
    -   IBM HTTP Server
    -   IBM DB2 database server or Oracle server
    -   (one of) Collaborative Lifecycle Management 6.0 or 6.0.x or
        Continuous Engineering Solution 6.0.x
5.  Deploy the latest version of IBM UrbanCode Deploy.
6.  Install the IBM Quick Deployer application into IBM UrbanCode Deploy
    by [running the setup script](IBMQuickDeployerInstallingIntoUCDOld).
7.  Update the permissions granted to the [Team Member
    role](IBMQuickDeployerSetupAndRunV13ScriptUpdatePermissions).
8.  Configure and expose the installation bits on a shared NFS media
    server or add them to each target VM - [Installation
    media](IBMQuickDeployerInstallationMediaOld)
9.  Set fixed component versions on application processes - [Set fixed
    component versions](IBMQuickDeployerSetFixedComponentVersions)
10. Optionally, enable [Configuration Management
    capabilities](IBMQuickDeployerSetupAndRunV13ScriptEnableCMOld).
11. Configure [NTP system clock default
    values](IBMQuickDeployerSetupAndRunV13ScriptSetNTPDefaultsOld).
12. Optionally, [enable installation of iFix
    releases](IBMQuickDeployerSetupAndRunV13ScriptEnableIFixesOld).
13. Set up and [secure the Admin user name and
    password](IBMQuickDeployerSecuringUserPasswords#Securing_admin_password).
14. Create an application environment - [Environment
    construction](IBMQuickDeployerEnvironmentConstruction)
    -   Create an UrbanCode Deploy resource
    -   Create an UrbanCode Deploy environment
    -   Add agents to the environment
    -   Map components to the agents
    -   Tag agents with middleware and application designators
15. Follow this step to save a permanent set of LDAP, User and DB
    parameters for future use
    -   Update and capture the LDAP, User and DB parameters and save
        them in a new version of the Rational_QD_SystemPre-Requisite_60x
        component using this process - [Updating the
        Rational_QD_SystemPre-Requisite_60x\*
        component](IBMQuickDeployerUpdatingSystemPreReqParametersOld)
16. Alternatively follow these steps to individually update the LDAP,
    User and DB parameters for use in a single installation
    -   Optionally update default values used by the **Change Default
        LDAP Parameters** process - [Modify the Change Default LDAP
        Parameters default
        values](IBMQuickDeployerModifyChangeDefaultLDAPParametersDefaults)
    -   Run the **Change Default LDAP Parameters** process - [Change the
        default LDAP
        parameters](IBMQuickDeployerChangeDefaultLDAPParametersOld)
    -   Optionally update default values used by the **Change Default
        User Parameters** process - [Modify the Change Default User
        Parameters default
        values](IBMQuickDeployerModifyChangeDefaultUserParametersDefaults)
    -   Optionally secure the user passwords - [Securing user
        passwords](IBMQuickDeployerSecuringUserPasswords)
    -   Run the **Change Default User Parameters** process - [Change the
        default user
        parameters](IBMQuickDeployerChangeDefaultUserParametersOld)
    -   Optionally modify the **Install Applications** process to use an
        existing IBM DB2 or Oracle database server - [Modify the Install
        Applications process to use an existing
        database](IBMQuickDeployerModifyInstallApplicationsProcessToUseAnExistingDatabase)
    -   Optionally run the **Change Default DB2 Parameters** process -
        [Change the default DB2 database
        parameters](IBMQuickDeployerChangeDefaultDB2ParametersOld)
    -   Optionally run the **Change Default Oracle Parameters**
        process - [Change the default Oracle database
        parameters](IBMQuickDeployerChangeDefaultOracleParametersOld)
    -   If you are going to use the Quick Deployer installed DB2
        database then you should have your database administrator review
        the configuration to make sure it conforms to internal security
        and reliability policies.
17. Run the **Install Applications** process - [Run the Install
    Application
    process](IBMQuickDeployerRunInstallApplicationsProcessOld)
18. Below are the default WebSphere Application Server settings that are
    updated by Quick Deployer. Consult the IBM Knowledge Center for
    WebSphere Application Server to determine if these settings are
    sufficient for your environment.
    -   JVM maximum and minimum heap size:
        -   2g if total RAM is less than 4GB
        -   4g if total RAM is between 4GB-6GB
        -   6g if total RAM is between 6GB-7.5GB
        -   75 of total RAM if total RAM is greater than 7.5GB
    -   The WebContainer Thread pool maximum and minimum sizes are set
        to 200
    -   Session Management
        -   Added a new custom Property:
            InvalidateOnUnauthorizedSessionRequestException=true
        -   Unchecked the Enable Cookies option
19. Configure a license server - [License key
    management](IBMQuickDeployerLicenseKeyManagement)
20. Set up an NTP system clock after installation - [Configuring the NTP
    system clock](IBMQuickDeployerConfiguringTheNTPSystemClock)
21. Suppress Data Collection Component (dcc) Administration page menus
    that are not required - [Suppressing dcc admin
    menus](IBMQuickDeployerSuppressingDccAdminMenus)
22. Optionally, [update component
    artifacts](IBMQuickDeployerUpdatingComponentArtifactsOld)
23. [IBM Quick Deployer CLM iFix Support
    Portal](IBMQuickDeployerIFixSupportOld)

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}
