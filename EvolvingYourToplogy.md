META:TOPICINFO{author="rrakich" date="1704729545" format="1.1"
version="1.8"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Evolving your topology [evolving-your-topology]

DKGRAY Authors: Main.PaulEllis, Main.ShubjitNaik, Main.RichRakich Build
basis: Products, editions, or versions that apply to the content. If no
build basis applies to this content, set the build basis to None.
ENDCOLOR

TOC{title="Page contents"}

## Introduction

It is typical for a project to download the Jazz software from jazz.net
and then install this in a proof of concept scenario, in order to
demonstrate the applications to potential users/management/stakeholders.
In some circumstances, those new projects using the proof of concept
will start adding production data. You soon have a key system using
completely under-powered hardware in an environment, which was never
intended or planned, for production use.

The above pattern is just one scenario where you would want to move
Collaborative Lifecycle Management (CLM) or Systems and Software
Engineering (SSE) collocated applications to a new topology. It is also
quite conceivable that you started off with just one project and are now
on your way to many, many more! If you are, then you will need to evolve
your topology.

The [Deployment Planning and Design](DeploymentPlanningAndDesign)
section of this wiki explains the different types of topology. BR The
base example that this article will use is the [CLM V1 Evaluation single
server](AlternativeCLMDeploymentTopologies#CLM_V1_Evaluation_Single_server)
topology and how to evolve from this.

An assumption of these evolutions is that in moving your applications
and/or Jazz Team Server from one location to another, there was some
planning performed when URIs were defined. It is most common that a
[reverse proxy](InstallProxyServers) was setup for this. Ultimately, if
you also need to change your URI, then you will need to take advantage
of [Server Rename](ServerRename).

## How do I separate a Jazz Team Server from an application?

Once you register an application with a JTS, it is not possible to
change that association by re-registering with a new JTS. It is only
possible to change the location of the Jazz Team Server. The version of
the JTS must always be at the same version as your highest application.
For example, if you have EWM 7.0.2; ETM 7.0.2; and DN 7.0.3, your JTS
must be at least version 7.0.3.

The assumption here is that you will move the Jazz Team Server (JTS)
from the incumbent server onto its own hardware/Virtual machine as you
evolve from the [CLM V1 Evaluation single
server](AlternativeCLMDeploymentTopologies#CLM_V1_Evaluation_Single_server)
topology to a [recommended CLM deployment
topology](RecommendedCLMDeploymentTopologies) or a [recommended SSE
deployment topology](RecommendedSSEDeploymentTopologies). These
instructions also account for a [reverse proxy](InstallProxyServers).

**Backup everything so that you are sure that you can restore your
original deployment should anything untoward occur during this
procedure.**

-   Stop the current application server for your apps and JTS (assuming
    EWM for this example)
-   Install JTS with a new application server instance into a new
    install directory
-   Copy the JTS applications configuration details from old server to
    the new copy the teamserver\*.properties for /jts.
-   Copy indices install_dir/server/conf/jts/indices to the new
    application server install, if not it has to be created again on the
    new server with repotool-jts
-   Configure the new application server to use other ports than the
    first one. Make sure the new JTS application server listens on a
    different port number.
-   Update the [reverse proxy](InstallProxyServers) so that the JTS URL
    points to the new JTS application server
-   [Undeploy](#SectionA1) JTS from the original application server so
    that it will only run the EWM server
-   Start the new JTS application server
-   Start the old application server which now serves only the EWM
    application (and the other application servers).
-   Test that everything is working correctly, specially links from jts
    to ccm and back from ccm to jts
-   Stop both application servers, make backup so that it can be
    reverted to this two server configuration at any time.

BR

You will have to make sure that you either get / create a personal
certificate from/on the new JTS server or get one from a Certificate
Authority (CA) and then import that certificate into the key that is
referenced in the *httpd.conf* file. You will have to do this with your
other applications servers too, if you move those. This is not just a
step for the JTS, any relocated application will also need a certificate
regenerated.

For more information on configuring certificates and reverse proxy,
please refer to the specific [section](InstallProxyServers) within this
wiki that is dedicated to this.

\#SectionA1

## How do I undeploy an application or Jazz Team Server using IBM Installation Manager?

[How do I manually disable and undeploy an application](#SectionA2)
below describes how you can achieve this manually if you did not use
Installation Manager to install your Jazz solution.

If you used IBM Installation Manager, then you can follow the steps here
to modify your installation to remove an application, or the Jazz Team
Server itself.

-   Start Installation Manager
-   Select **Uninstall**
-   Select the **Jazz Team Server** box next to the instance that you
    wish to uninstall.
    -   Also select **Trial keys for Engineering Lifecycle Management
        Products**, although you will be reminded/prompted if you forget
        this step.
-   Press the **Next \>** button
-   Confirm that the Backup Location corresponds to the location where
    your Jazz installation resides, if you have multiple instances of
    Jazz installed.
-   In the *Uninstall Packages* page, ensure all of the above selections
    are confirmed and then press the **Uninstall \>** button

\#SectionA2

## How do I manually disable and undeploy an application?

This answer is taken from the
[forum](https://jazz.net/forum/questions/131449/how-can-i-disable-rrc-and-rqm-applications-on-tomcat?redirect=2Fforum2Fquestions2F1314492Fhow-can-i-disable-rrc-and-rqm-applications-on-tomcat)
and applies to Tomcat.BR

-   First unregister the applications from JTS
    -   Access
        [https://server:port/jts/admin#action=com.ibm.team.repository.admin.registeredApplications](https://server:port/jts/admin#action=com.ibm.team.repository.admin.registeredApplications)
    -   Delete the applications that you wish to disable
-   Move the application's files
    -   Stop the server
    -   Move the relevant files and folders out of the application
        server profile apps directory based on the specific application
        you wish to disable.
    -   The applications' files and folders are listed below in the
        table: \| **Application** \| **Files** \| **Folders** \| \| **RM
        Application** \| rm.war \| rm \| \| **QM Application** \| qm.war
        \| qm \| \| **CCM Application** \| ccm.war \| ccm \|
-   Clear out the work and application server cache directories
-   Re-start the Server

##### Related topics: [Standard deployment topologies overview](StandardTopologiesOverview), [Server Rename](ServerRename), [Reverse Proxy](InstallProxyServers) [related-topics-standard-deployment-topologies-overview-server-rename-reverse-proxy]

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]
