META:TOPICINFO{author="ktessier" date="1513021850" format="1.1"
reprev="1.17" version="1.17"} META:TOPICPARENT{name="IBMQuickDeployer"}

# IBM Quick Deployer setup and run DKGRAY [ibm-quick-deployer-setup-and-run-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

The following setup procedure explains how to install, configure, and
run **IBM Quick Deployer** to deploy CLM/CE systems. The setup
information should help you with these tasks:

-   Size your system and plan your topology.
-   Understand what middleware is required and assemble all the
    installation bits for IBM Quick Deployer to install.
-   Edit the configuration files (e.g ldap, user, database properties)
    in the Quick Deployer package to customize your Quick Deployer
    install.
-   Import the IBM Quick Deployer application and its components into
    UCD.
-   Create the Quick Deployer environment to represent the desired
    application topology you want to install.
-   Run the **Install Applications** process to deploy the CLM/CE
    system.

## Plan

1.  Define your desired topology. See [Recommended Application Lifecycle
    Management (ALM) deployment topologies
    6.x](https://jazz.net/wiki/bin/view/Deployment/RecommendedALMDeploymentTopologies6)
    for details.
2.  Review the [System
    requirements](IBMQuickDeployerSystemRequirementsV20).
3.  Review the [Limitations and known
    issues](IBMQuickDeployerLimitationsKnownIssues).

## Prepare

1.  Ensure that you have an IBM UrbanCode Deploy server set up and that
    you have created the necessary accounts with the required
    permissions.
2.  Ensure that you have set up the target VMs to match your desired
    topology.
3.  Obtain and license the following middleware and product installation
    bits:
    -   IBM WebSphere Application Server
    -   IBM HTTP Server
    -   IBM DB2 database server or Oracle server
    -   (one of) Collaborative Lifecycle Management 6.0 or 6.0.x or
        Continuous Engineering Solution 6.0.x
    -   IBM Installation Manager
4.  Configure and expose the installation bits on a media server, or add
    them to each target VM - [Installation
    media](IBMQuickDeployerInstallationMedia).
5.  Ensure you have the required accounts and passwords for your LDAP
    server.

## Install the Quick Deployer application into UrbanCode Deploy 1. Download and extract the IBM Quick Deployer package from the compressed file into a location where you can run Java. The package includes - [Package content](IBMQuickDeployerPackageContent).

1.  Install the IBM Quick Deployer application into IBM UrbanCode Deploy
    by [customizing your properties files and then running the
    install.jar file](IBMQuickDeployerInstallingIntoUCD).

## Optional configuration tasks

-   Update the permissions granted to the [Team Member
    role](IBMQuickDeployerSetupAndRunV13ScriptUpdatePermissions).
-   Set fixed component versions on application processes - [Set fixed
    component versions](IBMQuickDeployerSetFixedComponentVersions).
-   [Enable installation of iFix
    releases](IBMQuickDeployerSetupAndRunV20ScriptEnableIFixes). See
    also [IBM Quick Deployer CLM iFix Support
    Portal](IBMQuickDeployerIFixSupport).
-   Secure the administrator and user passwords. [Securing user
    passwords](IBMQuickDeployerSecuringUserPasswords).

## Create an UrbanCode Deploy application environment

-   To connect your target VMs to the UCD server and tell Quick Deployer
    what to install on each machine you now [create an application
    environment](IBMQuickDeployerEnvironmentConstruction).

## Install the CLM or CE applications

-   Run the **Install Applications** process - [Run the Install
    Application process](IBMQuickDeployerRunInstallApplicationsProcess).

## Post-installation tasks

1.  Review and adjust WebSphere Application Server settings. See
    [WebSphere Application Server Knowledge
    Center](https://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5).
    These are the default settings that are updated by Quick Deployer:
    -   JVM maximum and minimum heap size:
        -   2g if total RAM is less than 4GB
        -   4g if total RAM is between 4GB-6GB
        -   6g if total RAM is between 6GB-7.5GB
        -   75 of total RAM if total RAM is greater than 7.5GB
    -   The WebContainer Thread pool maximum and minimum sizes are set
        to 200.
    -   Session Management
        -   Added a new custom Property:
            InvalidateOnUnauthorizedSessionRequestException=true.
        -   Unchecked the Enable Cookies option.
2.  Configure a license server - [License key
    management](IBMQuickDeployerLicenseKeyManagement).
3.  Optionally, set up an NTP system clock after installation -
    [Configuring the NTP system
    clock](IBMQuickDeployerConfiguringTheNTPSystemClock).
4.  Optionally, [update component
    artifacts](IBMQuickDeployerUpdatingComponentArtifacts).

## Maintenance tasks

When you run the installer, you can set the database parameters, LDAP
parameters, and user credentials. However, you might want to change some
of these settings after the installation is complete. To make such
changes, perform these tasks:

-   Update default values used by the **Change Default LDAP Parameters**
    process: [Modify the Change Default LDAP Parameters default
    values](IBMQuickDeployerModifyChangeDefaultLDAPParametersDefaults).
-   Run the **Change Default LDAP Parameters** process: [Change the
    default LDAP
    parameters](IBMQuickDeployerChangeDefaultLDAPParameters).
-   Update default values used by the **Change Default User Parameters**
    process: [Modify the Change Default User Parameters default
    values](IBMQuickDeployerModifyChangeDefaultUserParametersDefaults).
-   Run the **Change Default User Parameters** process: [Change the
    default user
    parameters](IBMQuickDeployerChangeDefaultUserParameters).
-   Modify the **Install Applications** process to use an existing IBM
    DB2 or Oracle database server: [Modify the Install Applications
    process to use an existing
    database](IBMQuickDeployerModifyInstallApplicationsProcessToUseAnExistingDatabaseV20).
-   Run the **Change Default DB2 Parameters** process: [Change the
    default DB2 database
    parameters](IBMQuickDeployerChangeDefaultDB2Parameters).
-   Run the **Change Default Oracle Parameters** process: [Change the
    default Oracle database
    parameters](IBMQuickDeployerChangeDefaultOracleParameters).
-   If you are going to use the Quick Deployer installed DB2 database,
    then you should have your database administrator review the
    configuration to make sure it conforms to internal security and
    reliability policies.
-   To save a permanent set of LDAP, user and database parameters for
    future use, update the parameters and save them in a new version of
    the Rational_QD_SystemPre-Requisite_60x component by using this
    process: [Updating the Rational_QD_SystemPre-Requisite_60x\*
    component](IBMQuickDeployerUpdatingSystemPreReqParametersV20).

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:TOPICMOVED{by="ktessier" date="1513020807"
from="Deployment.IBMQuickDeployerSetupAndRun"
to="Deployment.IBMQuickDeployerSetupAndRunV20"}
