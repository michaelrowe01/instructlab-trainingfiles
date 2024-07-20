META:TOPICINFO{author="din" date="1704469262" format="1.1"
version="1.5"}
META:TOPICPARENT{name="AutomatedScriptsForDeployingCLMOnWAS"}

# Setting up WebSphere Application Server by using the clm_was_config.py script [setting-up-websphere-application-server-by-using-the-clm_was_config.py-script]

DKGRAY Authors: Main.MichaelAfshar Build basis: The Rational solution
for Collaborative Lifecycle Management (CLM) 4.0 and later, up to and
including ELM 7.0.2. ENDCOLOR

TOC{title="Page contents"}

`Note: Support removed for IBM !WebSphere Application Server (Traditional WAS) starting with ELM version 7.0.3. Use !WebSphere Liberty, either embedded and installed with ELM applications, or separately installed`

With this Jython script, you can automate common administration tasks
and configure security in WebSphere Application Server.

## Before you begin

Make sure WebSphere Application Server is installed, a profile is
created, and the server is started prior to running `clm_was_config.py`.

## About this task

**Important:** The 4 GB memory used in the heap size settings and the
JVM arguments is for a system with minimum of 8 GB of physical memory.

When increasing the Java heap size, ensure that enough unused physical
memory is available on the machine to cover the increase. If sufficient
physical memory is not available, either install additional memory or
take into account the effect on overall performance that occurs.

It is also important to have more physical memory than is required by
all of the processes on the machine combined to prevent paging or
swapping. Paging reduces the performance of the system and affects the
performance of the Java memory management system.

The `clm_was_config.py` Jython script performs the following tasks:

-   Clears the Use Java 2 security to restrict application access to
    local resources check box.
-   Selects the Enable application security check box.
-   Selects the Enable administrative security check box.
-   Selects the Use available authentication data when an unprotected
    URI is accessed check box.
-   Sets the Initial Java Virtual Machine heap size to 4096.
-   Sets the Maximum Java Virtual Machine heap size to 4096.
-   Sets the recommended JVM arguments:

AIX

-Xmx4g -Xms4g -Xmn512m -Xgcpolicy:gencon -Xnocompressedrefs

Solaris and Mac OS X

**Note:** Mac OS X is unsupported.

-Xmx4g -Xms4g -Xmn512m -XX:MaxPermSize=768M
-XX:ReservedCodeCacheSize=512M -XX:CodeCacheMinimumFreeSpace=2M

Windows and Linux

-Xmx4g -Xms4g -Xmn512m -Xgcpolicy:gencon -Xcompressedrefs
-Xgc:preferredHeapBase=0x100000000

-   Adds the following custom properties:
    -   Name: JAZZ_HOME Value: Path to the JazzInstallDir/server/conf
        directory.
    -   Name: java.awt.headless Value: true
    -   Name:
        org.eclipse.emf.ecore.plugin.EcorePlugin.doNotLoadResourcesPlugin
        Value: true
    -   **For releases before ELM 7.0.1 SR1 / 7.0.2 SR1:**
    -   Name: log4j.configuration Value: Path to the
        startup_log4j.properties file.
    -   **For releases 7.0.1 SR1 / 7.0.2 SR1 and beyond:**
    -   Name: log4j2.configuration Value: Path to the startup_log4j2.xml
        file.

**Note:** If you are using Oracle or SQL Server database, you must
manually add the JDBC location in the Integrated Solutions Console. For
more information, see [Setting up WebSphere Application
Server](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m4/topic/com.ibm.jazz.install.doc/topics/t_s_server_installation_setup_WAS.html)
in the information center.

## Procedure

1.  To set up WebSphere Application Server, open a command window and
    change the directory to
    `WASInstallDir/AppServer/profiles/profile_name/bin`. If you have
    more than one profile under the profiles directory, select the
    profile that you want to be used for the CLM installation.
2.  Enter the following command substituting \_WAS*username* with the
    WebSphere Application Server admin username, \_WAS*password* with
    the admin user password, path to the script with the location of the
    script, for example,
    `C:/JazzTeamServer/server/was/clm_was_config.py` (notice the forward
    slash on Windows platform), and `JazzInstallDir/server/conf` with
    the path to the Jazz Team Server installation configuration
    directory. To avoid problems, do not use spaces in the path. You can
    use double quotation marks for paths with spaces.

UNIX

./wsadmin.sh -language jython -user WAS_username -password WAS_password
-f Path to the script/clm_was_config.py JazzInstallDir/server/conf

Windows

**Note:** You must use forward slashes for the path to the installation
configuration and the script directories. For example,
`C:/Progra~1/IBM/JazzTeamServer/server/conf`

wsadmin.bat -language jython -user WAS_username -password WAS_password
-f Path to the script/clm_was_config.py JazzInstallDir/server/conf

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]

META:TOPICMOVED{by="paulellis" date="1385730159"
from="Deployment.SetupWASJyton" to="Deployment.SetupWASJython"}
