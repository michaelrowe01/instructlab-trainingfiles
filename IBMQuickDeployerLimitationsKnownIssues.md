META:TOPICINFO{author="tomp" date="1513104527" format="1.1"
version="1.6"} META:TOPICPARENT{name="IBMQuickDeployer"}

# IBM Quick Deployer limitations and known issues DKGRAY [ibm-quick-deployer-limitations-and-known-issues-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

## Current limitations

-   The operating system of all VMs in a deployment must be the same. QD
    does not support mixed OS deployments.
-   UrbanCode Deploy agent must run as the root user on Linux and the
    Administrator user on Windows so all QD scripts will run in this
    context
-   LDAP support limited to Tivoli Directory Server
-   In general, the process cannot be restarted (should always create a
    snapshot of the VMs before running any UrbanCode Deploy process)
-   Only one environment can be connected to a database server;
    otherwise, name conflicts and UrbanCode Deploy process concurrency
    issues can occur
-   Will not support multiple instances of any application
-   The context root of the CLM or CE application's URL cannot be
    changed from the default
-   All CLM and CE application tags are expected to match the context
    root of their URL
-   For Windows deployments, if you select **local** as the installation
    media type, the local path cannot be a mapped network drive.
-   Python 2.7.5+ must be installed and included in the system path on
    the target VMs. Python 3.x is not supported.
-   If you use Oracle 12.1, you must use the 12.1.0.1 ojdbc7.jar. If you
    use the 12.1.0.2 ojdbc7.jar, you receive an error message when you
    run the repotools -createTables command. For additional information,
    see [repotools -createTables command fails with ORA-01000 on Oracle
    12](http://www-01.ibm.com/support/docview.wss?uid=swg21990430).
-   Quick Deployer supports deployment of environments that include the
    IBM WebSphere Liberty server only if those environments consist of
    CLM/CE 6.0.5 or later applications.

## Known issues

-   In CLM 6.0 scripted JTS Setup fails intermittently when attempting
    to register TRS providers with LQE. If this happens then JTS Setup
    will need to be completed from the web UI at ../jts/admin.
-   You must set the default user and LDAP parameters before you run the
    **Install Applications** process. You can do this by entering values
    in the userCreds.properties and ldap.properties files before you run
    the [installer](IBMQuickDeployerInstallingIntoUCD). Alternatively,
    you can run the Change Default User Parameters and Change Default
    LDAP Parameters processes.
-   DB2 user name restrictions are not enforced by the Change Default
    User Parameters process
-   If the Windows response time is slow, the Oracle installation might
    fail. The default total wait time is 60 minutes; after that, it
    exits with a failure. You can increase the number of tries or the
    interval wait time in function **post_windows_install** of the file
    Database/InstallOracle/install_oracle.py.
-   The Rational Requirements Management (RM) Converter application,
    which renders the read-only view of RM graphical artifacts, is
    installed but not configured. An issue was discovered when the
    Converter application was deployed on RHEL 7+. Therefore, the
    converter.war file will be present on the server but will not be
    configured in the WebSphere Application Server (WAS) server or the
    WAS Liberty server. See tech note [Requirements Management (RM)
    Converter application configuration and troubleshooting
    guide](https://jazz.net/library/article/1089) for detailed
    configuration instructions.

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:TOPICMOVED{by="ktessier" date="1513020155"
from="Deployment.IBMQuickDeployerLimitationsKnownIssuesV21"
to="Deployment.IBMQuickDeployerLimitationsKnownIssues"}
