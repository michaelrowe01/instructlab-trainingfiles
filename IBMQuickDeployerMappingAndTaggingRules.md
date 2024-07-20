META:TOPICINFO{author="ktessier" date="1502126059" format="1.1"
version="1.6"} META:TOPICPARENT{name="IBMQuickDeployer"}

# IBM Quick Deployer mapping and tagging rules [ibm-quick-deployer-mapping-and-tagging-rules]

DKGRAY INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

IBM UrbanCode Deploy (UCD) supports a **mapping system** and a **tagging
system**. IBM Quick Deployer (QD) makes use of these to ensure it only
installs and executes the required scripting and middleware on the
individual servers in the environment.

The [installer](IBMQuickDeployerInstallingIntoUCD) loads the required
components and creates the necessary agent tags.

Mapping and tagging brings flexibility, which allows the user to create
environments with more servers and different application distributions
than the 4 node CLM topology described in the [UCD
Environment](IBMQuickDeployerEnvironmentConstruction) topic. **Tagging
rules** are required to manage this flexibility and to ensure that when
you run the **Install Applications** process to deploy your system you
do not waste time and resources. In the early stage of execution QD will
test the tagging rules and fail if they are not met. This topic explains
these rules.

## Mapping rules

In a QD environment, there are three types of server. Each requires a
different set of mapped components.

-   Database (DB)
    -   Rational_QD_Database_60x
    -   Rational_QD_SystemPre-Requisite_60x
-   Reverse proxy (IHS)
    -   Rational_QD_ApplicationServer_60x
    -   Rational_QD_InstallationManager_60x
    -   Rational_QD_SystemPre-Requisite_60x
-   Application (WAS & "app")
    -   Rational_QD_Application_60x
    -   Rational_QD_ApplicationServer_60x
    -   Rational_QD_InstallationManager_60x
    -   Rational_QD_SystemPre-Requisite_60x

## Tagging rules:

-    QD supports a fixed set of tags **\[WAS, IHS, DB, JTS, CCM, QM, RM,
    RS, DCC, RELM, LDX, GC, LQE, DM\]**.
-    QD supports the following application tags **\[JTS, CCM, QM, RM,
    RS, DCC, RELM, LDX, GC, LQE, DM\]**.
-    There can be only one instance of any application tag in the QD
    environment.
-    The environment must contain one and only one **IHS** tagged agent
    and it cannot contain any other tags.
-    The environment must contain one and only one **DB** tagged agent
    and it cannot contain any other tags.
-    The environment must contain at least one **WAS** tagged agent.
-    The **WAS** tag must be present on any agent containing an
    **application tag**.
-    There must be at least one **application tag** on every **WAS**
    agent in the environment.
-    There must be a **JTS** tag on one of the **WAS** agents in the
    environment.
-    If the **LDX** tag is present it must be on the same agent as the
    **JTS** tag.
-    If **Configuration Management** is going to be enabled then the
    environment must contain the **GC** and **LDX** application tags.

## Example environment

Here is an example of a 3 server environment that meets the mapping and
tagging rules

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="TR_3v13.png" attachment="TR_3v13.png" attr="h"
comment="" date="1498847000" path="TR_3v13.png" size="29119"
user="ktessier" version="1"} META:TOPICMOVED{by="ktessier"
date="1501273243"
from="Deployment.IBMQuickDeployerMappingAndTaggingRulesV20"
to="Deployment.IBMQuickDeployerMappingAndTaggingRules"}
