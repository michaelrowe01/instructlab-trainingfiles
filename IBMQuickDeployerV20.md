META:TOPICINFO{author="ktessier" date="1513021177" format="1.1"
reprev="1.12" version="1.12"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# IBM Quick Deployer DKGRAY [ibm-quick-deployer-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

IBM Quick Deployer automates installing and deploying IBM Jazz
solutions: Collaborative Lifecycle Management (CLM) and IoT Continuous
Engineering (CE) on Red Hat Linux 6.9+ or Windows Server 2012 R2
Standard by using IBM UrbanCode Deploy. Currently the operating system
of all VMs in a deployment must be the same. You can use IBM Quick
Deployer to deploy CLM 6.0, CLM 6.0.x and CE 6.0.x on user-supplied VMs,
either locally or in the cloud. The automation can also install and
configure middleware, including IBM WebSphere Application Server, IBM
HTTP Server, and IBM DB2 database server or Oracle database server. IBM
Quick Deployer supports the standard Jazz deployment topologies;
however, because it uses an UrbanCode Deploy tagging mechanism, you can
distribute applications across multiple servers and many different
topologies are possible. Currently only new installations are supported
and only one instance of each Jazz application is supported per
topology. Upgrade support is being considered for future releases.

IBM Quick Deployer is developed and used internally by the CLM DevOps
pipeline team. IBM Quick Deployer provides a flexible mechanism for
building topologies and easily switching between deployment platforms.
IBM Quick Deployer is available as an unsupported utility that can be
downloaded from Jazz.net, so you can now use the same automation to
deploy and configure new installations in your own environment. IBM
Quick Deployer removes the need to understand all the middleware and
application configuration details, eliminates human error, conforms to
recommended topologies, and provides a repeatable process.

## IBM Quick Deployer overview

-   IBM UrbanCode Deploy-based new installation and configuration
    package for CLM and CE (no upgrade support)
-   Support for installing iFix releases for CLM, Design Management and
    IBM Rhapsody Design Management applications
-   Used internally as part of the CLM continuous test pipeline
-   UrbanCode Deploy-type tagging allows you to control which
    applications are deployed and where
-   Eliminates dependence on preinstalled middleware images
-   Installs WebSphere Application Server
-   Installs IBM HTTP Server (reverse proxy)
-   Installs a DB2 or Oracle database server or connects to an existing
    DB2 or Oracle database server
-   Connects to a provided LDAP server
-   Delivered as an unsupported Jazz.net download

## New in QD v2.0

-   Support for Windows deployments. You can now use Quick Deployer to
    deploy CLM or CE applications and supporting middleware, on Linux
    (Red Hat Linux 6.9+) or Windows (Windows Server 2012 R2 Standard)
    platforms. Note: the operating system of all VMs in a deployment
    must be the same.
-   An installer that automates many of the setup tasks that had to be
    completed manually in previous releases. The installer uses several
    properties files where you specify the details, such as user
    credentials and database parameters, of your installation.

## System requirements

-   [System requirements](IBMQuickDeployerSystemRequirementsV20)

## Limitations and known issues

-   [Limitations and known
    issues](IBMQuickDeployerLimitationsKnownIssues)

## Package content

-   [Package content](IBMQuickDeployerPackageContent)

## Application setup and run

To configure and run the Quick Deployer, see [IBM Quick Deployer setup
and run](IBMQuickDeployerSetupAndRunV20)

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:TOPICMOVED{by="ktessier" date="1513018558"
from="Deployment.IBMQuickDeployer" to="Deployment.IBMQuickDeployerV20"}
