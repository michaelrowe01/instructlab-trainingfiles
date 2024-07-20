META:TOPICINFO{author="din" date="1704469015" format="1.1"
version="1.2"}
META:TOPICPARENT{name="AutomatedScriptsForDeployingCLMOnWAS"}

# Deploying web applications on one server by using the clm_deploy.py script [deploying-web-applications-on-one-server-by-using-the-clm_deploy.py-script]

DKGRAY Authors: Main.MichaelAfshar Build basis: The Rational solution
for Collaborative Lifecycle Management (CLM) 4.0 and later, up to and
including ELM 7.0.2. ENDCOLOR

TOC{title="Page contents"}

`Note: Support removed for IBM !WebSphere Application Server (Traditional WAS) starting with ELM version 7.0.3. Use !WebSphere Liberty, either embedded and installed with ELM applications, or separately installed`

This Jython script deploys CLM web applications on a single WebSphere
Application Server.

## Before you begin

Ensure WebSphere Application Server and Jazz Team Server and CLM web
applications are installed prior to running `clm_deploy.py`.

## About this task

The clm_deploy.py Jython script performs the following tasks:

-   Installs the following CLM applications, if available in the webapps
    directory, in a single WebSphere Application Server:
    -   jts.war
    -   ccm.war
    -   qm.war
    -   rm.war
    -   admin.war
    -   converter.war
    -   clmhelp.war

**Note:** The web archive applications must have a .war extension.

## Procedure

1.  To deploy web applications, open a command window and change the
    directory to `WASInstallDir/AppServer/profiles/profile_name/bin`. If
    you have more than one profile under the profiles directory, select
    the profile that you want to be used for the CLM installation.
2.  Run the following command substituting \_WAS*username* with the
    WebSphere Application Server admin username, \_WAS*password* with
    the admin user password, path to the script with the location of the
    script, for example, `C:/JazzTeamServer/server/was/clm_deploy.py`
    (notice the forward slash on Windows platform), *nodeName* with the
    WebSphere Application Server node name, *serverName* with the
    WebSphere Application Server server name, and
    `JazzInstallDir/server/tomcat/webapps` with the path to the CLM
    application war files. To avoid problems, do not use spaces in the
    path. You can use double quotation marks for paths with spaces.

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
-f path to the script/clm_deploy.py nodeName serverName
JazzInstallDir/server/tomcat/webapps/

Windows

**Note:** You must use forward slashes for the path to the webapps
directory. For example,
C:/Progra\~1/IBM/JazzTeamServer/server/tomcat/webapps/

wsadmin.bat -language jython -user WAS_username -password WAS_password
-f path to the script/clm_deploy.py nodeName serverName
JazzInstallDir/server/tomcat/webapps/

After deploying the applications, log in to the WebSphere Integration
Solutions Console to start the applications.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
