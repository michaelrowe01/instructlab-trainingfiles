META:TOPICINFO{author="ajurj" date="1554840149" format="1.1"
version="1.1"}
META:TOPICPARENT{name="IoTContinuousEngineeringSolution6061"}

# Installing the Internet of Things Continuous Engineering Solution from the launchpad DKGRAY Authors: Main.AndreeaJurj Build basis: Version 6.0.6.1 [installing-the-internet-of-things-continuous-engineering-solution-from-the-launchpad-dkgray-authors-main.andreeajurj-build-basis-version-6.0.6.1]

ENDCOLOR

TOC{title="Page contents"}

You can install a subset of the Internet of Things (IoT) Continuous
Engineering Solution by using a launchpad available on Jazz.net. This
launchpad provides multiple options for installing the following
applications and components:

-   Jazz Team Server
-   Rational DOORS Next Generation
-   Rational Team Concert
-   Rational Quality Manager
-   Rational Rhapsody Design Manager
-   Rhapsody Model Manager
-   Rational Engineering Lifecycle Manager
-   Jazz Reporting Service
-   Global Configuration Management
-   Link Index Provider
-   Trial license keys for the applications

ICON{warning} **Attention**: Rational DOORS, and Rational Rhapsody are
not part of the launchpad, and must be installed separately if needed.

-   For information about installing Rational DOORS, read the [product
    documentation](http://www.ibm.com/support/knowledgecenter/SSYQBZ_9.6.1/com.ibm.doors.install.doc/topics/c_node_installing.html).
-   For information about installing Rational Rhapsody, read the
    [product
    documentation](http://www.ibm.com/support/knowledgecenter/SSB2MU_8.4.0/com.ibm.rhp.installing.doc/topics/c_node_installing.html).

If you use configuration management capabilities, install the Link Index
Provider and the Global Configuration Management applications. To learn
about the configuration management feature, read about [Getting started
with configuration
management](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.vvc.doc/topics/c_cm_assess.html).

## Evaluation Installation

The evaluation installation option helps you quickly install the
applications on one Jazz Team Server to create an evaluation environment
for the IoT Continuous Engineering Solution.

1.  Download the IoT Continuous Engineering Solution web installer for
    your operating system from
    [Jazz.net](https://jazz.net/downloads/continuous-engineering-solution/releases/6.0.6.1?p=allDownloads). 2.
    Extract the archive, and start the launchpad. Click `launchpad.exe`
    or `launchpad.sh`, depending on your operating system. 3. Click
    **Install the Server**. 4. Click **Evaluation Installation** to
    launch Installation Manager with the following applications
    selected:
    -   Change and Configuration Management (Rational Team Concert)
    -   Design Management for Rational Rhapsody
    -   Rhapsody Model Manager
    -   Jazz Reporting Service (including the Report Builder and
        Lifecycle Query Engine)
    -   Jazz Team Server
    -   Quality Management (Rational Quality Manager)
    -   Rational Engineering Lifecycle Manager
    -   Requirements Management (Rational DOORS Next Generation)
    -   Trial keys for the selected applications **Note**: If you are
        using configuration management, select the installation packages
        for the following applications:
        -   Link Index Provider (offers capabilities for linking across
            project areas and link discovery in global configurations)
        -   Global Configuration Management (provides capabilities for
            assembling and managing streams and baselines that can span
            multiple project areas of the CLM applications) 5. Follow
            the prompts to install the applications and their trial
            licenses. 6. When the installation is complete, return to
            the launchpad and select **Install the Client Tools**. 7.
            Select to install the Rational Rhapsody client. Complete the
            installation of the client in Installation Manager.

## Custom Installation

The launchpad can also be used as a starting point for installing more
complex topologies using the Custom Installation option. This option
allows you to install any of the IoT Continuous Engineering Solution
applications and the Jazz Team Server to a single application server, or
distributed across multiple application servers.

To determine which configuration meets your needs, read about
[Deployment and installation planning for the Rational solution for
CLM](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/c_planning_install.html).

## Jazz Authorization Server

Install the Jazz Authorization Server to enable Jazz Security
Architecture single sign-on (SSO) in your Jazz products. Jazz Security
Architecture SSO is an alternative single sign-on mechanism to Kerberos
SSO, IBM WebSphere Application Server SSO, or Apache Tomcat SSO. For
more information, read the [CLM
documentation](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/c_jsasso_jas_user_management.html).

## Installing samples

To install the Money that Matters sample, and to set up your
environment, read these articles:

-   [Installing the Money that Matters
    sample](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/t_install_sample_project.html)
-   [Configuring the Money that Matters sample
    environment](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/t_config_sample_proj.html)

ICON{warning} **Restriction**: The **Money that Matters** lifecycle
scenario is designed to work with IBM Rational Software Architect Design
Management Server, RED **not** with Rational Rhapsody Design
ManagerENDCOLOR. If Rational Rhapsody Design Manager is registered with
the Jazz Team Server during the **Register Applications** step, then
Rational Rhapsody Design Manager is automatically contributed, and the
Money that Matters sample creation fails. Using the web interface, clear
the Design Manager selection from the list of applications that
contribute to the sample.

To learn how to install a Rational Rhapsody sample on the Design
Management Server, read the [product
documentation](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/t_sample_project.html).

##### Related topics: \* [Installation overview](IoTContinuousEngineeringSolutionInstallationRoadmap6061) [related-topics-installation-overview]

-   [Installation
    requirements](IoTContinuousEngineeringSolutionInstallationRequirements6061)
-   [Installing with Installation
    Manager](IoTContinuousEngineeringSolutionInstallingApplications6061)

##### External links: [external-links]

-   [Downloading IoT Continuous Engineering
    Solution](https://jazz.net/downloads/continuous-engineering-solution/)
