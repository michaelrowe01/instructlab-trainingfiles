META:TOPICINFO{author="ktessier" date="1501856896" format="1.1"
version="1.41"} META:TOPICPARENT{name="IBMQuickDeployerOld"}

# IBM Quick Deployer setup and run DKGRAY [ibm-quick-deployer-setup-and-run-dkgray]

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
    existing IBM DB2 instance
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
    -   Tag create scripts
    -   License files
4.  You must obtain and license the following middleware and product
    installation bits through standard IBM mechanisms:
    -   IBM WebSphere Application Server
    -   IBM HTTP Server
    -   IBM DB2 database server
    -   (one of) Collaborative Lifecycle Management 6.0 or 6.0.x or
        Continuous Engineering Solution 6.0.x
5.  Configure and expose the installation bits on a shared NFS media
    server or add them to each target VM - [Installation
    media](IBMQuickDeployerInstallationMediaOld)
6.  Deploy the latest version of IBM UrbanCode Deploy.
7.  Install and configure an UrbanCode Deploy application - [Application
    setup](IBMQuickDeployerApplicationSetup)
    -   Create the **Rational QD CLM** team on the UrbanCode Deploy
        server and add an admin user
    -   Create the **Team Member** role
    -   Add the **Rational QD CLM** team to any existing UrbanCode
        Deploy agents
    -   Import and configure the application from the supplied JSON file
8.  Load the component code - [Component version
    setup](IBMQuickDeployerComponentVersionSetup)
9.  Set fixed component versions on application processes - [Set fixed
    component versions](IBMQuickDeployerSetFixedComponentVersions)
10. Create agent tags - [Create agent
    tags](IBMQuickDeployerCreateAgentTags)
11. Overview of how Quick Deployer uses UrbanCode Deploy component
    mapping and agent tagging - [Mapping and tagging rules for Quick
    Deployer](IBMQuickDeployerMappingAndTaggingRulesOld)
12. Create an application environment - [Environment
    construction](IBMQuickDeployerEnvironmentConstruction)
    -   Create an UrbanCode Deploy resource
    -   Create an UrbanCode Deploy environment
    -   Add agents to the environment
    -   Map components to the agents
    -   Tag agents with middleware and application designators
13. Follow this step to save a permanent set of LDAP, User and DB
    parameters for future use
    -   Update and capture the LDAP, User and DB parameters and save
        them in a new version of the Rational_QD_SystemPre-Requisite_60x
        component using this process - [Updating the
        Rational_QD_SystemPre-Requisite_60x\*
        component](IBMQuickDeployerUpdatingSystemPreReqParametersOld)
14. Alternatively follow these steps to individually update the LDAP,
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
15. Run the **Install Applications** process - [Run the Install
    Application
    process](IBMQuickDeployerRunInstallApplicationsProcessOld)
16. Below are the default WebSphere Application Server settings that are
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
17. Configure a license server - [License key
    management](IBMQuickDeployerLicenseKeyManagement)
18. Set up an NTP system clock after installation - [Configuring the NTP
    system clock](IBMQuickDeployerConfiguringTheNTPSystemClock)
19. Suppress Data Collection Component (dcc) Administration page menus
    that are not required - [Suppressing dcc admin
    menus](IBMQuickDeployerSuppressingDccAdminMenus)
20. Optionally, [update component
    artifacts](IBMQuickDeployerUpdatingComponentArtifactsOld)
21. [IBM Quick Deployer CLM iFix Support
    Portal](IBMQuickDeployerIFixSupportOld)

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="addagents.png" attachment="addagents.png"
attr="h" comment="" date="1443625069" path="addagents.png" size="65417"
user="tomp" version="1"} META:FILEATTACHMENT{name="Snap3.png"
attachment="Snap3.png" attr="h" comment="" date="1443625618"
path="Snap3.png" size="49138" user="tomp" version="1"}
META:TOPICMOVED{by="ktessier" date="1501278327"
from="Deployment.IBMQuickDeployerSetupAndRun"
to="Deployment.IBMQuickDeployerSetupAndRunOld"}
