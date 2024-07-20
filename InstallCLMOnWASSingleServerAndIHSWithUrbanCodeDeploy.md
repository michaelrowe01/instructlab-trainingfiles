META:TOPICINFO{author="lziosi" date="1414776543" format="1.1"
reprev="1.7" version="1.7"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Install CLM on WebSphere Application Server single server and IBM HTTP Server with IBM UrbanCode Deploy DKGRAY Authors: Main.LaraZiosi Build basis: IBM Collaborative Lifecycle Management 5.0.0, IBM UrbanCode Deploy 6.1.0.3, IBM WebSphere Application Server 8.5.5.2 [install-clm-on-websphere-application-server-single-server-and-ibm-http-server-with-ibm-urbancode-deploy-dkgray-authors-main.laraziosi-build-basis-ibm-collaborative-lifecycle-management-5.0.0-ibm-urbancode-deploy-6.1.0.3-ibm-websphere-application-server-8.5.5.2]

ENDCOLOR

TOC{title="Page contents"}

This article shows an examplar IBM UrbanCode Deploy process that can be
used to automate the installation and setup of IBM Collaborative
Lifecycle Management on a single server. The process also automates the
installation and configuration of IBM WebSphere Application Server, and
of a reverse proxy based on IBM HTTP Server.

## Introduction

### Topology

There are three machines in this topology:

-   VM1: contains the installation of IBM UrbanCode Depoy server and one
    agent used for version imports
-   VM2: contains the installation of IBM WebSphere Application Server,
    IBM Collaborative Lifecycle Management and one agent
-   VM3: contains the installation of IBM HTTP Server and one agent

All machines run the Linux Operating System. The agents can run as root
or as a normal user. This will determine how Installation Manager and
all the products will be installed. UrbanCode Deploy impersonation using
su or sudo is not supported by this process design.

### Prerequisites

IBM UrbanCode Deploy processes can only be imported on exactly the same
server version and plug-ins. The attached Application process was
developed on this configuration:

-   IBM UrbanCode Deploy 6.1.0.3
-   [Installation Manager Plug-in
    2](https://hub.jazz.net/project/ucplugin/UrbanCode20Deploy20Plug-in20for20IBM20Installation20Manager/overview)
-   [IBM WebSphere - Application Deployment Plug-in
    73](https://developer.ibm.com/urbancode/plugin/ibm-websphere-application-deployment-2/ibm-websphere-application-deployment/)

The following additional products were used:

-   [IBM Installation Manager
    1.8.0](http://www-01.ibm.com/support/docview.wss?uid=swg24037640)
-   IBM WebSphere Application Server 8.5.5.2
-   IBM CLM 5.0.0
-   Oracle 11g

It is assumed that the machines VM2 and VM3 can access the repositories
where the Installation Manager repositories are located. The repository
locations need to be specified as Component Environment properties as
described below.

It is assumed that the machines have proper ulimits set before launching
the installation process. See: [Planning to install on UNIX and Linux
systems](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.0/com.ibm.jazz.install.doc/topics/c_special_considerations_linux.html?cp=SSYMRC_5.0.0⟨=en).

### How to use this process

To use this process, proceed as follows:

1 Make sure that you have installed the exact versions of the plugins
named above 1 From the Application page in UrbanCode Deploy, import the
Application JSON file 1 Add two agents to the Application Environment 1
Add the following components to the agent on VM2:

-   InstallationManagerComponent
-   CLMPackageComponent
-   WASPackageComponent
-   OracleDriver
-   WASProfile
-   WASCompleteConfigForCLM
-   JTSSetup 1 Add the following components to the agent on VM3:
-   InstallationManagerComponent
-   IHSPackageComponent 1 Unzip the attached workspace.zip so to create
    the directory /workspace If you want to change this path, you will
    have to adjust it in the Configuration tab of each component. 1
    Download the [IBM Installation Manager
    1.8.0](http://www-01.ibm.com/support/docview.wss?uid=swg24037640)
    installer and copy it to:
    /workspace/InstallationManager/1.8.0/agent.installer.linux.gtk.x86_1.8.0.20140902_1503.zip
    1 Download the Oracle JDBC Driver `ojdbc6.jar` and copy it to:
    /workspace/OracleDriver/1.0/ojdbc6.jar 1 Create a custom Jython
    script to configure Websphere Application Server to use an LDAP
    registry (standalone or as part of a Federated Repository) and copy
    it to: /workspace/WAS_LDAP_Configuration/1.0/LDAPConfig.py 1 Record
    a JTS setup on a preconfigured sample installation, using the
    command: repotools-jts.sh -setup
    repositoryURL`https://hostname.example.com:9443/jts adminUserId`
    adminPassword= responseFile JTSSetup.properties See for more
    information: [Repository tools command to configure the
    server](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.1/com.ibm.jazz.install.doc/topics/r_repotools_setup.html?lang=en)
    1 Place the resulting property file in:
    /workspace/JTSSetup/Oracle/JTSSetup.properties 1 Review the
    Installation Manager response files in the folders: 1
    /workspace/CLMComponent/5.0.0 1 /workspace/IHSComponent/8.5.5.2 1
    /workspace/WASComponent/8.5.5.2 1 Import versions of all the
    components 1 Set up the following Environment variables:

LDAP.password

LDAPJazzAdmins

LDAPJazzDWAdmins

LDAPJazzGuests

LDAPJazzProjectAdmins

LDAPJazzUsers

OraclePassword

WASNodeName WASNode01

WASPassword

WASUser wasadmin

WASProfileName AppSrv01

WASServerName server1

and the following Component Environment properties, that refer to the
Installation Manager Repositories from which to install CLM, WebSphere
Application Server and IBM HTTPS Server.

At this point, you are ready to execute these two application processes
in order:

1 InstallAll 1 ConfigureWASforCLMAndDoJTSSetup

## Process design principles

### Root and user installations

This process assumes that identity of the user that runs the UrbanCode
Deploy Agent indicates the wish to install IBM Installation Manager and
all the products as that user. This process therefore supports only
**root** installation (using the command `installc`) or **user**
installation (using the command `userinstc`) of IBM Installation
Manager. Installation Manager **group** installation is not supported.
For these reasons, UrbanCode Deploy impersonation is not supported by
this process (additionally, the Application Deployment plugin does not
support impersonation).

The process defines the default installation directories of all products
at runtime, based on whether the agent runs as root or as user.

### Automating WebSphere Discovery and Topology Discovery

The Plugin WebSphere - Application Deployment offers two steps, called
**WebSphere Discovery** and **WebSphere Topology Discovery**. They are
designed to be used interactively, rather than from a process. Their
behavior is described in this Knowledge Center page: [Importing
resources from WebSphere Application
Server](http://www-01.ibm.com/support/knowledgecenter/SS4GSP_6.0.1/com.ibm.udeploy.doc/topics/resources_import_was.html).

One key feature of this plugn is that it relies on configuring Resource
Roles, described here: [Application Deployment for WebSphere plug-in -
Roles](https://developer.ibm.com/urbancode/plugindoc/ibmucd/application-deployment-websphere-plug/73-528720/roles/).
In the normal interactive usage, you would manually invoke the discovery
of the topology of a WebSphere Cell, which would create a number of
Resources in the Resource Tree, for all Nodes, Clusters, Servers. Then
you would manually place components in the correct scope, and by virtue
of the Resource Role, those components would inherit all the parameters
required to connect to WebSphere Application Server from that scope.

When you attempt to automate this task, you cannot manually place the
Components on the Resources, since the Resources do not yet exist (they
will be discovered will running the process). This issue can be solved
by dynamically creating new Resources of type Component in the correct
location in the Resource Tree and then invoking the execution of an
Application process that invokes processes of those Components. A
disadvantage of this approach is that the versions of those dynamically
mapped Components are not visible to the user that invokes the process,
as they are selected at runtime.

## Detailed process design

### Process to install Install Installation Manager

The Component process to install Installation Manager looks as follows:

The script contained in the step Install Installation Manager as root or
user contains:

chmod u+x -R \* user=\${p:agent/USER} if \[ "\$user" == "root" \]; then
./installc -log InstallationManagerInstallation.log -acceptLicense more
InstallationManagerInstallation.log else ./userinstc -log
InstallationManagerInstallation.log -acceptLicense more
InstallationManagerInstallation.log fi

The chmod command is required because the unzip step does not preserve
the execute bit of the files contained in the archive. The predefined
variable `agent/USER` is used to determine whether to install as root or
as normal user.

A switch command based on the value of the same variable is also used to
set two properties on the agent, as follows:

Type of user Variable name Variable value

root IMCLPath /opt/IBM/InstallationManager/eclipse/tools/imcl

user IMCLPath
\${p:agent/HOME}/IBM/InstallationManager/eclipse/tools/imcl

The Uninstall process contains only one shell step with this code:

if \[ "\${p:agent/USER}" == "root" \]; then cd
/var/ibm/InstallationManager/uninstall ./uninstallc else cd
\${p:agent/HOME}/var/ibm/InstallationManager/uninstall ./uninstallc rm
-rf \${p:agent/HOME}/var rm -rf \${p:agent/HOME}/etc rm -rf
\${p:agent/HOME}/IBM fi

### Process to install a product

The processes to install the products are all similar, so only the
example processes for CLM are shown below.

The installation directories of the products are different, based on
whether Installation Manager is installed as root or normal user.

These installation directories are required by multiple components (for
example, when configuring WebSphere Application Server for CLM, you need
to know the CLM installation location).

It is therefore interesting to store these installation directories as
Environment variables.

The process that creates an Environment variable does not get access to
its value in subsequent steps, because a new version of the Environment
is created when a property is added, and that version of the environment
is not available to the yet to the currently running process.

Therefore the process is split in two: the first Component process sets
the Environment variables, and the second Component process actually
installs the product using those variables.

Process to prepare variables for installing CLM:

Process to Install CLM:

Step to Execute Response File to install CLM:

The Step to Execute Response File to install CLM takes the following
Response File variables:

sharedLocation=\${p:agent/sharedLocation},clmRepositoryLocation=\${p:environment/clmRepositoryLocation},clmInstallLocation=\${p:environment/clmInstallLocation}

These variables must be declared in the Response File that you use,
according to the Installation Manager Knoweldge center topic: [Response
File
variables](https://www-01.ibm.com/support/knowledgecenter/SSDV2W_1.8.0/com.ibm.silentinstall12.doc/topics/r_silent_install_variable.html?lang=en)

The uninstall process just runs a different response file, which
contains the uninstall command for the profile that was previously
installed.

### Application Process to configure WebSphere Application Server for CLM

The Application process to configure WebSphere Application Server for
CLM is shown below:

### Process to create the WebSphere Application Server profile

The process to create the WebSphere Application Server profile contains
a shell step that runs `manageprofiles.sh`.

The step to invoke manageprofile.sh to create a WAS profile looks as
follows:

The code of the step is as follows:

./manageprofiles.sh -create -templatePath
\${p:WASTemplateDir}/\${p:WASTemplateType} -profileName
\${p:WASProfileName} -profilePath
\${p:WASProfilePath}/\${p:WASProfileName} -enableAdminSecurity true
-adminUserName \${p:WASUser} -adminPassword \${p:WASPassword} -nodeName
\${p:environment/WASNodeName} -serverName
\${p:environment/WASServerName} -defaultPorts

Although the Application Deployment plugin has a plugin to start
WebSphere Application Server, we cannot easily use that step yet,
because we have not yet performed the Discovery and Topology Discovery.
Therefore the step to start WAS uses the known variable
`environment/serverName` to start the server with the command
`startServer.sh`.

The step to start WAS without using the Application Deployment plugin is
shown below:

### Component process to Discover the WAS Cell

The following Component process shows how to Discover the WAS Cell:

The idea behind this process is to invoke the **WebSphere Discovery**
step so that it creates a Resource representing the WebSphere Cell. In
order to do so, the parent of the current resource is retrieved and its
path is stored in a variable (`parent.resource.path`). The current
resource being a Component, its parent is generally the Agent.

Then the WebSPhere Discovery step is invoked with the following
parameters (so that it will create the WebSphere Cell Resource just
under the parent of the current resource):

Path Override
\${p:environment/WASProfilePath}/\${p:environment/WASProfileName}/bin/wsadmin.sh

Profile Path resource

\${p:environment/WASProfilePath}/\${p:environment/WASProfileName}

Resource \${p:Populate_parent.resource.path/parent.resource.path}
(hidden)

This image shows the details of the WebSphere Discovery step:

The process then verifies that the newly created resource has the
`WebSphereCell` role. (See: [Application Deployment for WebSphere
plug-in -
Roles](https://developer.ibm.com/urbancode/plugindoc/ibmucd/application-deployment-websphere-plug/73-528720/roles/)
for more information).

Finally, it constructs the path of the newly created Resource and it
stores it in an environment variable, as it will be needed in future
steps.

### Component process to Configure the WAS Profile for CLM

The following Component process shows how to Configure the WAS Profile
for CLM:

This process is special because it dynamically places components on the
resources discovered by the **WebSphere Discovery** and **WebSphere
Topology Discovery** steps.

The **WebSphere Topology Discovery** step will find that there is a Node
inside the Cell and a Server inside the Node, and it will create
Resources that have the same names and hierarchy. It is important to
execute the steps of Application Deployment plugin from inside these
resources, so that all the variables contained in their Resource Roles
are available.

In order to add new Components to the Resource tree, you can use the
step called **Create Resource**, and specify the Component name for both
the Resource Name and the Resource Role, as shown below:

Once the Components are dynamically placed in the Resource tree,
Application processes that deploy those components (or operational
processes) can be invoked, using the step shown below:

Highlighed in yellow is the field which contains the versions of the
Components that the Application process will deploy. Note that when you
launch the process, you will not be prompted to select versions for
these dyanmically added components. You need to make sure that the
versions listed inside these steps are the ones you intend to deploy.

These Application processes are used for the following purposes:

1 To configure LDAP in WebSphere Application Server, using a custom
Jython script. You can easily record such a script while you manually
configure LDAP using the Administrative Console. 1 To run the `wsadmin`
scripts supplied with CLM: `clm_was_config.py` and `clm_deploy.py`,
described here: [Automatically deploying the Collaborative Lifecycle
Management applications on WebSphere Application
Server](https://jazz.net/wiki/bin/view/Deployment/AutomatedScriptsForDeployingCLMOnWAS).
The second script contains commented method calls to configure WAS JVM
properties specific to various databases. There is a part of the process
that uncomments these calls for the desired Database and substitutes the
location where the corresponding JDBC driver has been installed. 1 To
Map the security roles of the CLM applications (`jts`, `qm`, `ccm`) to
the LDAP groups.

### Process to run JTS setup

The process to run JTS setup is actually very simple, as it is based on
leveraging the [Repository Tools command-line
reference](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.1/com.ibm.jazz.install.doc/topics/c_repotools_overview.html?lang=en).

It replaces any environment specific values in the `JTSSetup.properties`
file, then it invokes the following command to actually run the setup:

./repotools-jts.sh -setup includeLifeCycleProjectStep=true
repositoryURL=[https://\${p:agent/Hostname](https://$%7Bp:agent/Hostname)}:9443/jts
adminUserId=\${p:environment/LDAP.user}
adminPassword=\${p:environment/LDAP.password}
parametersFile=JTSSetup.properties

## References

##### Related topics: [Installing, upgrading, and migrating](DeploymentInstallingUpgradingAndMigrating), [Deployment web home](DeploymentWebHome) [related-topics-installing-upgrading-and-migrating-deployment-web-home]

##### External links: [external-links]

-   [IBM UrbanCode](https://developer.ibm.com/urbancode/)
-   [WebSphere Topology Auto-Discovery \[Video
    Training](https://developer.ibm.com/urbancode/docs/websphere-topology-auto-discovery-video-training/)\]

##### Additional contributors: Main.FrancoisPanaget, Natarajan Thirumeni [additional-contributors-main.francoispanaget-natarajan-thirumeni]

META:FILEATTACHMENT{name="CompEnvProps.jpg"
attachment="CompEnvProps.jpg" attr="h" comment="Component Environment
Properties" date="1414440931" path="CompEnvProps.jpg" size="155536"
user="lziosi" version="1"}
META:FILEATTACHMENT{name="InstallInstallationManager.jpg"
attachment="InstallInstallationManager.jpg" attr="h" comment="Component
process to Install Installation Manager" date="1414488235"
path="InstallInstallationManager.jpg" size="162766" user="lziosi"
version="1"}
META:FILEATTACHMENT{name="PrepareVariablesForInstallingCLM.jpg"
attachment="PrepareVariablesForInstallingCLM.jpg" attr="h"
comment="Prepare variables for installing CLM" date="1414489689"
path="PrepareVariablesForInstallingCLM.jpg" size="80714" user="lziosi"
version="1"} META:FILEATTACHMENT{name="InstallCLMProcess.jpg"
attachment="InstallCLMProcess.jpg" attr="h" comment="Process to Install
CLM" date="1414489801" path="InstallCLMProcess.jpg" size="41207"
user="lziosi" version="1"}
META:FILEATTACHMENT{name="ExecuteResponseFile.jpg"
attachment="ExecuteResponseFile.jpg" attr="h" comment="Step to Execute
Response File to install CLM" date="1414489887"
path="ExecuteResponseFile.jpg" size="121663" user="lziosi" version="1"}
META:FILEATTACHMENT{name="CreateWASProfile.jpg"
attachment="CreateWASProfile.jpg" attr="h" comment="Process to create
and start the WAS profile" date="1414491269" path="CreateWASProfile.jpg"
size="35483" user="lziosi" version="1"}
META:FILEATTACHMENT{name="ManageprofileStep.jpg"
attachment="ManageprofileStep.jpg" attr="h" comment="Step to invoke
manageprofile.sh to create a WAS profile" date="1414491312"
path="ManageprofileStep.jpg" size="166110" user="lziosi" version="1"}
META:FILEATTACHMENT{name="StepToStartWAS.jpg"
attachment="StepToStartWAS.jpg" attr="h" comment="Step to start WAS
without using the Application Deployment plugin" date="1414491723"
path="StepToStartWAS.jpg" size="77927" user="lziosi" version="1"}
META:FILEATTACHMENT{name="Applicationprocess.jpg"
attachment="Applicationprocess.jpg" attr="h" comment="Application
process to configure WAS for CLM" date="1414516440"
path="Applicationprocess.jpg" size="93819" user="lziosi" version="1"}
META:FILEATTACHMENT{name="ConfigureWASProfileForCLM.jpg"
attachment="ConfigureWASProfileForCLM.jpg" attr="h" comment="Component
process to Configure the WAS Profile for CLM" date="1414516759"
path="ConfigureWASProfileForCLM.jpg" size="225761" user="lziosi"
version="1"} META:FILEATTACHMENT{name="DiscoverWASCell.jpg"
attachment="DiscoverWASCell.jpg" attr="h" comment="Component process to
Discover the WAS Cell" date="1414517050" path="DiscoverWASCell.jpg"
size="90680" user="lziosi" version="1"}
META:FILEATTACHMENT{name="WebSphereDiscoveryStep.jpg"
attachment="WebSphereDiscoveryStep.jpg" attr="h" comment="WebSphere
Discovery Step" date="1414518308" path="WebSphereDiscoveryStep.jpg"
size="104799" user="lziosi" version="1"}
META:FILEATTACHMENT{name="CreateComponentResource.jpg"
attachment="CreateComponentResource.jpg" attr="h" comment="Creat
Component Resource" date="1414530638" path="CreateComponentResource.jpg"
size="119800" user="lziosi" version="1"}
META:FILEATTACHMENT{name="RunApplicationProcessFromComponentProcess.jpg"
attachment="RunApplicationProcessFromComponentProcess.jpg" attr="h"
comment="Run Application Process from Component Process"
date="1414530677" path="RunApplicationProcessFromComponentProcess.jpg"
size="126562" user="lziosi" version="1"}
META:FILEATTACHMENT{name="RunJTSSetup.jpg" attachment="RunJTSSetup.jpg"
attr="h" comment="Run JTS Setup" date="1414534505"
path="RunJTSSetup.jpg" size="69155" user="lziosi" version="1"}
META:FILEATTACHMENT{name="ExecuteJTSSetupStep.jpg"
attachment="ExecuteJTSSetupStep.jpg" attr="h" comment="Execute JTS Setup
step" date="1414534550" path="ExecuteJTSSetupStep.jpg" size="129559"
user="lziosi" version="1"}
