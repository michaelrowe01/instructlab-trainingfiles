META:TOPICINFO{author="din" date="1704469158" format="1.1"
version="1.2"}
META:TOPICPARENT{name="AutomatedScriptsForDeployingCLMOnWAS"}

# Deploying web applications in a distributed environment by using the clm_deploy_distributed.py script [deploying-web-applications-in-a-distributed-environment-by-using-the-clm_deploy_distributed.py-script]

DKGRAY Authors: Main.MichaelAfshar Build basis: The Rational solution
for Collaborative Lifecycle Management (CLM) 4.0 and later, up to and
including ELM 7.0.2. ENDCOLOR

TOC{title="Page contents"}

`Note: Support removed for IBM !WebSphere Application Server (Traditional WAS) starting with ELM version 7.0.3. Use !WebSphere Liberty, either embedded and installed with ELM applications, or separately installed`

This Jython script deploys CLM web applications on multiple WebSphere
Application Servers in a distributed environment.

## Before you begin

Ensure WebSphere Application Servers and Jazz Team Server and CLM web
applications are installed prior to running `clm_deploy_distributed.py`.

## About this task

The `clm_deploy_distributed.py` Jython script performs the following
tasks:

-   Installs the following CLM applications, if included in your command
    argument as a comma-separated list:
    -   jts.war
    -   ccm.war
    -   qm.war
    -   rm.war
    -   admin.war
    -   converter.war
    -   clmhelp.war

**Note:** The web archive applications must have a .war extension.

## Procedure

1.  To deploy CLM applications on multiple WebSphere Application server,
    open a command window and change the directory to
    `WASInstallDir/AppServer/profiles/profile_name/bin`. If you have
    more than one profile under the profiles directory, select the
    profile that you want to be used for the CLM installation.
2.  Run the following command substituting \_WAS*username* with the
    WebSphere Application Server admin username, \_WAS*password* with
    the admin user password, path to the script with the location of the
    script, for example,
    `C:/JazzTeamServer/server/was/clm_deploy_distributed.py` (notice the
    forward slash on Windows platform), *nodeName* with the WebSphere
    Application Server node name, *serverName* with the WebSphere
    Application Server server name, and
    `JazzInstallDir/server/tomcat/webapps` with the path to the CLM
    application war files. To avoid problems, do not use spaces in the
    path. You can use double quotation marks for paths with spaces. List
    the name of applications to be installed separated by a comma
    without spaces.

**Remember:** If you used IBM Installation Manager to install the CLM
applications and during the installation cleared the check box for
**Install Tomcat 7 with JTS web application**, by default, the web
application files (.war) are copied into the
`JazzInstallDir/server/webapps` directory. If during installation you
selected **Install Tomcat 7 with JTS web application**, the web
application files (.war) are copied into the
`JazzInstallDir/server/tomcat/webapps` directory.

UNIX

./wsadmin.sh -language jython -user WAS_username -password WAS_password
-f path to the script/clm_deploy_distributed.py nodeName serverName
JazzInstallDir/server/tomcat/webapps/ jts,qm,ccm

Windows

**Note:** You must use forward slashes for the path to the webapps
directory. For example,
C:/Progra\~1/IBM/JazzTeamServer/server/tomcat/webapps/

wsadmin.bat -language jython -user WAS_username -password WAS_password
-f path to the script/clm_deploy_distributed.py nodeName serverName
JazzInstallDir/server/tomcat/webapps/ jts,qm,ccm

##### Related topics: [related-topics]

##### External links: [external-links]

##### Additional contributors: [additional-contributors]
