META:TOPICINFO{author="ajurj" date="1554840419" format="1.1"
version="1.1"}
META:TOPICPARENT{name="IoTContinuousEngineeringSolution6061"}

# Installing the Internet of Things Continuous Engineering Solution with Installation Manager DKGRAY Authors: Main.AndreeaJurj Build basis: Version 6.0.6.1 [installing-the-internet-of-things-continuous-engineering-solution-with-installation-manager-dkgray-authors-main.andreeajurj-build-basis-version-6.0.6.1]

ENDCOLOR

TOC{title="Page contents"}

## Installing Installation Manager

IBM Installation Manager is a program for installing, updating, and
modifying software packages. It helps you manage the IBM applications,
or packages, that it installs on your computer.

Installation Manager provides tools that help you keep packages up to
date, modify packages, manage the licenses for your packages, and
uninstall packages. Installation Manager includes six wizards for
maintaining packages:

-   The **Install** wizard walks you through the installation process.
    You can install a package by simply accepting the defaults, or you
    can modify the default settings to create a custom installation.
    Before you install, you get a complete summary of your selections
    throughout the wizard. Use the wizard to install one or more
    packages.
-   The **Update** wizard searches for available updates to packages
    that you have installed. An update might be a released fix, a new
    feature, or a new version of the product. Details of the contents of
    the update are provided in the wizard to help you determine whether
    to apply an update.
-   The **Modify** wizard helps you modify certain elements of a package
    that you have already installed. During the first installation of
    the package, you select the features that you want to install.
    Later, if you require other features, you can use the modify
    packages wizard to add them to your package. You can also remove
    features, and add or remove languages.
-   The **Manage Licenses** wizard helps you set up the licenses for
    your packages. Use this wizard to change your trial license to a
    full license, to set up your servers for floating licenses, and to
    select which type of license to use for each package.
-   The **Roll Back** wizard helps you to revert to a previous version
    of a package.
-   The **Uninstall** wizard removes a package from your computer. You
    can uninstall more than one package at a time.

Installation Manager must be installed before you can install your
software packages. Installation Manager is automatically installed in
these circumstances:

-   When you start the installation of your package from the launchpad
-   When you start the installation of your package from a trial site

The latest version of Installation Manager might be required for your
package. Updates are discovered automatically if you have not cleared
the **Search service repositories for updates** check box on the
Installation Manager preference page.

To install Installation Manager, follow these steps:

1.  Download the latest version of IBM Installation Manager from
    <https://jazz.net/downloads/ibm-installation-manager/>. Save the
    file on the server. 2. Select the latest version, and click
    **Next**. 3. Read and accept the license agreement, and click
    **Next**. 4. Select your installation location, and click
    **Next**. 5. Review your installation choices, and click
    **Install**. 6. When the installation completes, you are prompted to
    restart Installation Manager. You can then exit or proceed with
    installing the next program.

## Installing Rational solution for CLM 6.0.6.1 applications

-   Jazz Team Server
-   Rational DOORS Next Generation
-   Rational Team Concert
-   Rational Quality Manager
-   Design Management
-   Rhapsody Model Manager
-   Jazz Reporting Service (Report Builder, Data Collection Component,
    Lifecycle Query Engine)
-   Global Configuration Management (GCM)
-   Link Index Provider (LDX)
-   Rational Engineering Lifecycle Manager, the Eclipse client for
    Rational Team Concert, and Rational Team Concert Build System
    Toolkit.

**Note**: Rational DOORS Next Generation is part of the CLM package. If
you are using Rational DOORS as your requirements management
application, install Rational DOORS Next Generation and migrate your
data to Rational DOORS Next Generation.

Follow the instructions in the CLM documentation:

-   [Installing the Rational solution for Collaborative Lifecycle
    Management](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/c_install_overview.html)

**Installing the Build System Toolkit and CLM Eclipse client**

Once you have installed, configured and verified the required components
from CLM, install the Build System Toolkit and Eclipse client.

-   [Installing the Build System
    Toolkit](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/t_install_build_toolkit.html)
-   [Installing the CLM Eclipse
    client](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.jazz.install.doc/topics/c_client_installation.html)

#### Configuring the integration among development lifecycle applications

-   Learn about [integrating CLM applications with other development
    lifecycle management
    applications](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.help.common.jazz.calm.doc/topics/c_node_integrating.html).
-   Learn about [OSLC
    integrations](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.help.common.oslc.doc/topics/c_oslc_overview.html).
-   Learn how to [integrate applications that are registered with
    different Jazz Team
    Servers](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.help.common.jazz.calm.doc/topics/r_calm_cfg_roadmap.html).

## Installing IBM Rational DOORS v9.6.1.11

Download Rational DOORS 9.6.1.11 through your Passport Advantage
account:
<https://www.ibm.com/software/howtobuy/softwareandservices/passportadvantage>

There are several components required to install Rational DOORS with
DOORS Web Access:

-   Rational DOORS client
-   Rational DOORS database server
-   Rational DOORS Web Access server - An adaptation of Apache Tomcat.
    Tomcat is an application server that executes Java servlets and
    renders web pages that include JavaServer Pages (JSP) code.
-   Rational DOORS Web Access broker - An adaptation of Apache ActiveMQ.
    ActiveMQ is an open source message broker that implements the Java
    Message Service (JMS).
-   Interoperation server - A Rational DOORS client that you run from
    the command line.

<!-- -->

-   For more information on installing Rational DOORS, read
    [Installation and upgrade roadmap for Rational DOORS and Rational
    DOORS Web
    Access](http://www.ibm.com/support/knowledgecenter/SSYQBZ_9.6.1/com.ibm.doors.install.doc/topics/c_planninginstallationorupgrade.html).
-   To learn how to administer Rational DOORS, read the [Administration
    chapter](http://www.ibm.com/support/knowledgecenter/SSYQBZ_9.6.1/com.ibm.doors.administering.doc/topics/c_node_administering.html).
-   To comply with security standards, follow the configuration
    instructions in [Configuring Rational DOORS Web Access to comply
    with security
    standards](http://www.ibm.com/support/knowledgecenter/SSYQBZ_9.6.1/com.ibm.doors.configuring.doc/topics/c_security_compliance.html).
-   Complete the configuration steps described in [Configuring
    integrations using
    OSLC](http://www.ibm.com/support/knowledgecenter/SSYQBZ_9.6.1/com.ibm.rational.doors.integrating.doc/topics/c_integratejazz.html).

#### Configuring DOORS Web Access to communicate with other components

After you installed Rational DOORS Web Access, you must configure the
components to communicate with one another, and to provide OSLC
services.

-   **Setting Rational DOORS database server parameters**: You must
    configure the Rational DOORS database server to communicate with the
    Rational DOORS Web Access broker and the Rational DOORS Web Access
    server by adding parameters to the command line. For instructions,
    read [Configuring the Rational DOORS database server to
    communicate](http://www.ibm.com/support/knowledgecenter/SSYQBZ_9.6.1/com.ibm.rational.dwa.install.doc/topics/c_setupddbs.html).
-   **Setting up the Rational DOORS Web Access server**: Once you have
    installed DOORS web access, you must set up the DOORS Web Access
    server to communicate with the broker, the license server, and the
    Rational DOORS database server. For instructions, read [Setting up
    the Rational DOORS Web Access
    server](http://www.ibm.com/support/knowledgecenter/SSYQBZ_9.6.1/com.ibm.rational.dwa.install.doc/topics/c_setupdwaserver.html).
-   **Configuring Rational DOORS Web Access to use SSL**: The Rational
    DOORS Web Access server can be configured to use SSL, which is the
    default used by the IoT Continuous Engineering Solution. To enable
    Rational DOORS Web Access to use SSL, follow the instructions in
    [Configuring Rational DOORS Web Access to use SSL or
    TLS](http://www.ibm.com/support/knowledgecenter/SSYQBZ_9.6.1/com.ibm.rational.dwa.install.doc/topics/t_configureSSL.html).

ICON{tip} **Tip**: Because several web browsers such as Mozilla Firefox
now block mixed SSL content (that is, having SSL and non-SSL content on
the same page), we recommend enabling all applications in the IoT
Continuous Engineering Solution to use SSL.

#### Increasing the OAuth timeout

Increase the OAuth timeout allowances to match the Jazz applications (24
hours). **Note**: For DOORS Web Access version 9.5 or later this step is
optional.

1.  Open `[DWA_path]/server/conf/web.xml`. 2. Search for
    session-timeout. Change the value to `1440` (minutes). Save the
    file. 3. Open `[DWA_path]/server/festival/config/festival.xml`. 4.
    Search for `OauthAccessTokenTimeout`. Change the value to `1440`
    (minutes). Save the file.

#### Integrating DOORS with other development lifecycle management applications

To learn how to configure the product to integrate with your reporting,
design, quality, change, and configuration management solutions, read
the [product
documentation](http://www.ibm.com/support/knowledgecenter/SSYQBZ_9.6.1/com.ibm.rational.doors.integrating.doc/topics/c_node_integrating.html).

## Installing IBM Rational Rhapsody v8.4

Download Rational Rhapsody v8.4 through your Passport Advantage account:
<https://www.ibm.com/software/howtobuy/softwareandservices/passportadvantage>

For more information on which Rational Rhapsody edition to use, read
about [Rational Rhapsody
editions](http://www.ibm.com/support/knowledgecenter/SSB2MU_8.4.0/com.ibm.rhp.overview.doc/topics/rhp_c_po_specailized_editions.html).
Not all optionally installed Add-Ons are available with every edition.
The Architect editions have the most functionality in the IoT Continuous
Engineering Solution environment.

Follow the instructions outlined in the [Rational Rhapsody installation
guide](http://www.ibm.com/support/knowledgecenter/SSB2MU_8.4.0/com.ibm.rhp.installing.doc/topics/rhp_c_iu_installing_rational_rhapsody.html).
The IoT Continuous Engineering Solution requires the following options:

-   **Rational Rhapsody Gateway Add On** - Requirements Traceability
    connects Rational Rhapsody to Rational DOORS, IBM Rational
    RequisitePro, and other requirements authoring tools provided by
    other vendors for requirements traceability throughout the lifetime
    of a project, and to navigate online between the design and the
    requirements. Basic export to Rational DOORS and Rational
    RequisitePro is included in base products. Advanced bidirectional
    Rational DOORS and Rational RequisitePro synchronization, impact
    analysis, coverage analysis, and integration with other authoring
    tools is included with the Rational Rhapsody Tools and Utilities Add
    On.
-   **Rational Rhapsody XMI Toolkit** - XML Metadata Interchange imports
    and exports model information to or from other tools, and is part of
    the Rational Rhapsody Tools and Utilities Add On.
-   **Rational Rhapsody TestConductor Add On** provides model-driven
    testing to automate testing tasks; defines tests with code and
    graphically with sequence diagrams, state charts, activity diagrams,
    and flowcharts; and runs the tests interactively or in batch mode.

#### Integrate Rational Rhapsody with other development lifecycle management applications

After you installed Rational Rhapsody, complete the following
integration tasks:

-   [Integrating Rational Rhapsody and Rational Team
    Concert](http://www.ibm.com/support/knowledgecenter/SSB2MU_8.4.0/com.ibm.rhp.integ.collabtools.doc/topics/rhp_c_int_rhp_and_rtc.html)
-   [Integrating Rational Rhapsody and Rational
    DOORS](http://www.ibm.com/support/knowledgecenter/SSB2MU_8.4.0/com.ibm.rhp.integ.reqmgttools.doc/topics/rhp_c_int_rhp_and_doors.html)
-   [Integrating Rational Rhapsody and Rational Quality
    Manager](http://www.ibm.com/support/knowledgecenter/SSB2MU_8.4.0/com.ibm.rhp.integ.testingtools.doc/topics/rhp_c_int_rhp_and_rqm.html)

##### Related topics: [related-topics]

-   [Installation
    overview](IoTContinuousEngineeringSolutionInstallationRoadmap6061)
-   [Installation
    requirements](IoTContinuousEngineeringSolutionInstallationRequirements6061)
-   [Installing from the
    launchpad](IoTContinuousEngineeringSolutionInstallWizard6061)

##### External links: [external-links]

-   [Downloading IoT Continuous Engineering
    Solution](https://jazz.net/downloads/continuous-engineering-solution/)
