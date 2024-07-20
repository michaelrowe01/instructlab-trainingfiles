META:TOPICINFO{author="ktessier" date="1513021176" format="1.1"
version="1.19"} META:TOPICPARENT{name="IBMQuickDeployer"}

# IBM Quick Deployer system requirements DKGRAY [ibm-quick-deployer-system-requirements-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

Review all requirements before you install and run IBM Quick Deployer.
Also review the references to the appropriate product-specific websites.

## Systems needed

-   Review the [CLM 6.0.4 system requirements](CLMSystemRequirements604)
    and the [CLM sizing strategy](CLMSizingStrategy60).
-   Plan your topology by using the [Recommended Application Lifecycle
    Management (ALM) deployment topologies
    6.x](RecommendedALMDeploymentTopologies6).

## IBM UrbanCode Deploy server

-   Current release of [IBM UrbanCode
    Deploy](http://www-03.ibm.com/software/products/en/ucdep) is
    installed (tested with version 6.2.1.0.ifix01767250).
-   User with UrbanCode Deploy admin privileges to import and configure
    the IBM Quick Deployer application.
-   An admin authentication token to import the Quick Deployer
    application into UrbanCode Deploy. You can create a token from the
    UrbanCode Deploy **Settings** menu.
-   Customer can create/import templates, manage blueprints, or manually
    construct UrbanCode Deploy environments from available agents:
    -   Template import via cloud system integration
    -   Manual template definition
    -   Manual environment definition

## Media server or local media

You must provide the installers for the IBM Rational solution for
Collaborative Lifecycle Management (CLM) or IoT Continuous Engineering
(CE) solution and necessary middleware. See [IBM Quicker Deployer
installation media](IBMQuickDeployerInstallationMedia) for details.

-   You are responsible for obtaining and processing all required
    installation media.
-   Installation media can be maintained on an FTP server or installed
    on each of the target VMs (local). For Linux only, the local path
    can be a network mount.

## Tivoli LDAP server

Access to a configured instance of Tivoli Directory Server.

## General authentication and account information

-   Able to provide passwords for IBM DB2 or Oracle, LDAP, and WebSphere
    Application Server to UrbanCode Deploy process.
-   Provide connection information for customer provisioned DB2 or
    Oracle server, if used. If you use the DB2 or Oracle server that
    Quick Deployer installs, this connection information is not needed.
-   Provide connection information for customer provisioned LDAP server.
-   Provide connection information for the customer maintained media
    server.
-   Provide an OS User account. Quick Deployer uses this User account to
    install some middleware and CLM or CE applications.

## Target VMs

-   Customer provisioned VMs that meet the [CLM 6.0.4 system
    requirements](CLMSystemRequirements604) and the [CLM sizing
    strategy](CLMSizingStrategy60).
-   Customer provisioned VMs that support snapshots. Because Quick
    Deployer is not restartable, and does not support uninstall
    operations, you should create snapshots before you use Quick
    Deployer to deploy applications on the target VMs.
-   The operating system of all VMs in deployment must be the same. QD
    does not support mixed OS deployments.
-   Each VM must be a member of the same domain, and the fully qualified
    domain name of each VM must contain only lowercase characters.
-   All servers must be set to the same time zone.
-   Python 2.7.5+ is installed and is included in the system path.
    **Note**: Python 3.x is not supported. Also note that for windows,
    later python releases may have issues with identifying the correct
    platform, so we have tested with python 2.7.5 and in a limited way,
    with python 2.7.9.
-   The UrbanCode Deploy specified version of Java is installed and is
    included in the system path. Ensure that the JAVA_HOME environment
    variable is set.
-   When an LDAP property contains a comma-separated list of values,
    there cannot be any spaces in or between the values.
-   After all other prerequisites have been met, the UrbanCode Deploy
    agent should be installed and running on each VM. See the
    *Installing agents* topic in the [IBM UrbanCode Deploy Knowledge
    Center](https://www.ibm.com/support/knowledgecenter/SS4GSP) for
    details.
-   Quick Deployer will create folder IBMQD in the root folder if it
    does not exist, and Quick Deployer requires the following contiguous
    space on each target VM to run the installation and configuration.
    See individual product sizing guides for any additional space that
    might be required.
    -   IBM HTTPS Server - 20 GB
    -   WebSphere Server - 50 GB
    -   IBM DB2 - 60 GB
    -   Oracle - 40 GB

### Linux-specific requirements

-   Each VM should be configured so that the command *hostname -f*
    returns the fully qualified domain name.
-   RHEL 6.9+ (64-bit) is installed. **Please note** that RHEL 6.x
    support is deprecated for Quick Deployer 2.0 and will be removed in
    the next release, being replaced with RHEL 7.x.
-   The following packages are installed:
    -   xorg-x11-server-Xvfb
    -   expect
    -   DM requires a number of specific RH packages - [Rational
        Rhapsody Design Manager 6.0.4 system
        requirements](https://jazz.net/wiki/bin/view/Deployment/CLMSystemRequirements604).
-   UrbanCode Deploy agent is installed as root.
-   Ensure that Secure Copy Protocol (SCP) can be used to copy a file
    from the IHS server to all the WAS servers, If not, then the script
    that runs SCP might fail without an error.
-   Ensure that files created by the root user are readable by others,
    such as, the OS user.
-   Ensure that the /IBMQD folder is writable and readable by the OS
    user if created by you. If created by the application, then Quick
    Deployer expects that folders created by the root user are
    accessible by the OS user as described in the previous requirement.
-   Quick Deployer expects the /home folder permission to be at
    least 755. Otherwise, the DB2 or Oracle create instance process
    fails.
-   The OS user requires sudo privileges. Make sure that the OS user is
    granted **some commands** privileges with **NOPASSWD**. To grant
    these privileges, edit the sudoers file with a tool such as visudo
    and add the following line to the end of the file to ensure that the
    OS user settings are not overriden:
    -   On RH7 add this line where clmadmin is the OS user:
        -   clmadmin ALL=(ALL) NOPASSWD:
            /usr/bin/mkdir,/usr/bin/touch,/usr/bin/sh,/usr/bin/chmod,/usr/bin/echo
    -   On RH6 add this line where clmadmin is the OS user:
        -   clmadmin ALL=(ALL) NOPASSWD:
            /bin/mkdir,/bin/touch,/bin/sh,/bin/chmod,/bin/echo
-   Scripts are able to enable SSH and use it to move certificate files
    between the WebSphere Application Server and IBM HTTP Server
    servers.

### Windows-specific requirements

-   Windows Server 2012 R2 Standard (64-bit) is installed.
-   Ensure that the Windows Management Instrumentation Command-line
    interface (WMIC) is enabled. The WMIC is included with Windows
    Server 2012.
-   Ensure that the OS User account (a local user that will be used to
    install the applications) exists.
-   Ensure that remote desktop access is granted to the OS User account
    (for example, clmadmin). Login to remote desktop access as the OS
    User before you run any Quick Deployer scripts to ensure that the
    account is setup correctly by Windows.
-   Ensure the local security policy is amended so that log on as a
    service is enabled for the OS User account.
-   Ensure that the C:\IBMQD folder is writable and readable by the
    administrator if it is created by you. If C:\IBMQD is created by the
    application, Quick Deployer expects that folders created by the
    Administrator are accessible by the OS User.
-   Ensure that the C:\etc folder is created manually before running any
    scripts.
-   UrbanCode Deploy agent is installed using the Administrator account
    and is running as the Administrator user.

## Database server

-   Customer-supplied DB2 or Oracle server requires the installation of
    an UrbanCode Deploy agent so scripts can be run as root user (on
    Linux) or administrator (on Windows).
-   Additional Oracle requirements: \* Review [Supported Oracle Linux 7
    and Red Hat Enterprise Linux 7 Distributions for
    x86-64](http://docs.oracle.com/database/121/LADBI/pre_install.htm#LADBI80757)
    or [Supported Oracle Linux 6 and Red Hat Enterprise Linux 6
    Distributions for
    x86-64](http://docs.oracle.com/database/121/LADBI/pre_install.htm#LADBI7534).
    \* Review [How to Complete Preinstallation Tasks
    Manually](http://docs.oracle.com/database/121/LADBI/app_manual.htm#LADBI7864).
    \* To use an existing database server, the instance must have been
    created on that server. The UrbanCode Deploy deployment creates
    users only on the defined database instance. In addition, set the
    values for the **processes** and **open_cursors** parameters to
    1,000. For example: alter system set processes=1000 scope=spfile;
    alter system set open_cursors = 10000 scope=both; \* All Oracle
    database users must have the same passwords that are defined in the
    userCreds.property file.

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:TOPICMOVED{by="ktessier" date="1513021176"
from="Deployment.IBMQuickDeployerSystemRequirements"
to="Deployment.IBMQuickDeployerSystemRequirementsV20"}
