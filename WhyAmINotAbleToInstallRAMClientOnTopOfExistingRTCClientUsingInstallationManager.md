META:TOPICINFO{author="sbagot" date="1432744914" format="1.1"
version="1.15"} META:TOPICPARENT{name="IntegrationsTroubleshooting"}

# Why can't I install the Rational Asset Manager client on top of existing package group by using IBM Installation Manager? [why-cant-i-install-the-rational-asset-manager-client-on-top-of-existing-package-group-by-using-ibm-installation-manager]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: Rational
Team Concert 4.0.x, Rational Asset Manager 7.5.1.2, Rational Software
Architect 8.5.x, Rational Software Architect for WebSphere 8.5.x,
Rational Application Developer for WebSphere 8.5.x ENDCOLOR

TOC{title="Page contents"}

This document describes what to do to install the IBM Rational Asset
Manager 7.5.1.x client on top of an existing IBM Installation Manager
package group containing, for example, IBM Rational Team Concert client,
IBM Rational Software Architect for WebSphere, or IBM Rational
Application Developer for WebSphere 8.5.x.

## Initial assessment

### Symptoms

\* When you install Rational Asset Manager 7.5.1.2 in the same package
group where you previously installed IBM Rational Team Concert 4.0.x or
Rational Software Architect for WebSphere 8.5.x, the installation fails
with the following error:

In plain text: Installation failed. Error during "complete" phase:
CRIMA1082E: The bundle "com.ibm.ut.help.common_2.11.3.v20130228_1957"
cannot be installed in this Eclipse configuration because it is not
equivalent to the bundle "com.ibm.ut.help.common_2.7.2.v20121004_1540"
that is already installed.

\* When you install Rational Team Concert 4.0.x or Rational Software
Architect for WebSphere 8.5.x in the same package group where you
previously installed Rational Asset Manager 7.5.1.2, the installation
fails with the following error:

In plain text: Installation failed. Error during "complete" phase:
CRIMA1082E: The bundle "com.ibm.ut.help.common_2.7.2.v20121004_1540"
cannot be installed in this Eclipse configuration because it is not
equivalent to the bundle "com.ibm.ut.help.common_2.11.3.v20130228_1957"
that is already installed.

### Impact/scope

-   This is affecting all the users who are trying to install Rational
    Asset Manager 7.5.1.2 on top of an existing package.

## Data gathering and subsequent analysis steps

### IBM Installation Manager logs

1 Start IBM Installation Manager. 1 Collect the installation logs by
clicking **Help \> Export data for Problem Analysis**. 1 Save the
resulting .zip file to a temporary folder. 1 Extract the files. 1 Check
what exact products are installed by opening this file: `installed.xml`.
1 Look for installation errors by opening this file: `logs\index.xml`. 1
Compare the date and times of the installation logs with the
installation history: `histories\index.xml`. This helps in establishing
the phase during which the installation errors occurred.

## Possible causes

-   [WI 88849 : RAM client 7.5.1.2 Installation Manager offering package
    fails to shell share with other eclipse based
    packages](https://jazz.net/jazz02/web/projects/Rational20Asset20Manager#action=com.ibm.team.workitem.viewWorkItem&id=88849)

### Installation errors

-   When you install two Eclipse-based products in the same Installation
    Manager package goup, the Equinox P2 reconciler process runs. If it
    finds plugin versions that will invalidate the Eclipse
    configuration, the installation procedure stops.

## Possible solutions

\* Install Rational Asset Manager by using the Eclipse **Help \> Install
New Software...** mechanism into your existing IBM Installation Manager
package as follows: 1 Get the URL of your Rational Asset Manager server
Eclipse update site from the **Help icon** and choose **Extensions**.

The Extension page says the Rational Asset Manager Eclipse is based on
version 3.4 although it is compatible with Eclipse 3.6.2 and above (see
[Work item 88588:Extension page still says RAM's Eclipse client is based
on
3.4](https://jazz.net/jazz02/web/projects/Rational20Asset20Manager#action=com.ibm.team.workitem.viewWorkItem&id=88588)
for further details). 1 Point to your Rational Asset Manager 7.5.1.2
server Eclipse **Update Site** (for example:
`http://host:port/ram/RCPUpdateSite/`)

Select all the options you see in the above screenshot even the Rational
Team Concert 3.0 client integration plugin as it is valid for version
3.0 and above.

\* Install Rational Team Concert into your Rational Asset Manager
7.5.1.2 client using the eclipse **Help \> Install New Software...**
mechanism as follows: 1 Download the Client for Eclipse IDE
(**RTC-Client-p2Repo-4.0.x.zip**) you can get from the **[RTC
downloads](https://jazz.net/downloads/rational-team-concert/)** as shown
below:

1 Point to P2 installer .zip you downloaded as shown below:

##### Related topics: [related-topics]

\* Still need help troubleshooting your integrations issue? Refer to
[Integrations Troubleshooting](IntegrationsTroubleshooting) for
additional topics.

##### External links: [external-links]

-   [Rational Team Concert
    downloads](https://jazz.net/downloads/rational-team-concert/)

##### Additional contributors: Main.FrancoisPanaget [additional-contributors-main.francoispanaget]

META:FILEATTACHMENT{name="RAM7512OnTopOfRSA851Error.jpg"
attachment="RAM7512OnTopOfRSA851Error.jpg" attr="h" comment="Error when
installing RAM 7512 to existing RSA 8.5.x or RTC 4.0.x package group"
date="1369927130" path="RAM7512OnTopOfRSA851Error.jpg" size="100089"
user="fpanaget" version="1"}
META:FILEATTACHMENT{name="RTC402OnTopOfRAM7.5.1.2.jpg"
attachment="RTC402OnTopOfRAM7.5.1.2.jpg" attr="h" comment="Error when
installing RTC 4.0.x to existing RAM 7512 package group"
date="1369929080" path="RTC402OnTopOfRAM7.5.1.2.jpg" size="95133"
user="fpanaget" version="1"}
META:FILEATTACHMENT{name="RTCClientForEclipseP2Install.jpg"
attachment="RTCClientForEclipseP2Install.jpg" attr="h" comment="RTC
Client For EclipseIDE installation with P2 repository" date="1369991507"
path="RTCClientForEclipseP2Install.jpg" size="213329" user="fpanaget"
version="1"}
META:FILEATTACHMENT{name="RTCClientForEclipseIDEDownload.jpg"
attachment="RTCClientForEclipseIDEDownload.jpg" attr="h" comment="Client
For Eclipse IDE repository download" date="1369992112"
path="RTCClientForEclipseIDEDownload.jpg" size="272399" user="fpanaget"
version="1"} META:FILEATTACHMENT{name="RamExtensionEclipsePlugin.jpg"
attachment="RamExtensionEclipsePlugin.jpg" attr="h" comment="RAM
extensions Eclipse Plug-in URL page" date="1369994191"
path="RamExtensionEclipsePlugin.jpg" size="169592" user="fpanaget"
version="1"} META:FILEATTACHMENT{name="RamExtension.jpg"
attachment="RamExtension.jpg" attr="h" comment="How to get the RAM
Extensions' page" date="1369994374" path="RamExtension.jpg" size="32441"
user="fpanaget" version="1"}
META:FILEATTACHMENT{name="RAMClientInstallFromUpateSite.jpg"
attachment="RAMClientInstallFromUpateSite.jpg" attr="h" comment="RAM
client plugins installation from udpate site" date="1370000948"
path="RAMClientInstallFromUpateSite.jpg" size="293714" user="fpanaget"
version="1"}
