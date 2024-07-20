META:TOPICINFO{author="sbeard" date="1417903909" format="1.1"
reprev="1.18" version="1.18"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Rational solution for Collaborative Lifecycle Management Upgrade Guide [rational-solution-for-collaborative-lifecycle-management-upgrade-guide]

DKGRAY Authors: Main.RosaNaranjo Build basis: CLM 4.0.x ENDCOLOR

TOC{title="Page contents"}

RED This guide has been updated for CLM 4.0.6ENDCOLOR

This CLM Upgrade Guide includes a step-by-step follow-up to the [CLM
2011 Upgrade Workshop](https://jazz.net/library/article/662), a
troubleshooting guide and a FAQ. It provides a high-level overview of
the CLM Upgrade process. The upgrade process was greatly improved with
the CLM 2012 release and with additional improvements in subsequent
releases such as CLM 4.0.6. For example, there is no longer the need to
export and import any CLM repository databases and it is no longer
necessary to run JTS setup after an application is upgraded or register
upgraded applications with an existing JTS.

The CLM 2011 Upgrade workshop used a fully distributed WAS deployment of
all 3 CLM applications along with a DB2 server. At the end of the CLM
2011 upgrade workshop, the deployment topology looked as follows:

The topology will remain unchanged after the upgrade. The only
difference after the upgrade would be that the 3.0.1 software is
replaced with 4.0.x software.

We want to start the upgrade by [planning the
upgrade](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.jazz.install.doc/topics/c_planning_upgrade.html).
The CLM applications (RTC, RQM, and RRC) can be upgraded in any order.
However, keep in mind that the first application upgrade phase will also
include the upgrade of the JTS as the first component to be upgraded. If
you have a multi-application deployment, read the [Planning the
Upgrade](#PlanningTheUpgrade) section below.

In this article, I will upgrade JTS first along with the RRC
application, RTC second, and lastly, RQM. In order to understand the
upgrade process, we want to use the Interactive Upgrade guide (IUG)
available in the [4.0.x Infocenter Upgrade and Migrating
book](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html).
In this example, I chose to generate three separate upgrade guides.
However, you can choose to generate one guide for all four applications
and include RRDI if you have it deployed in your 3.0.1.x environment.

At a high level, the upgrade outline will look as follows:

1 Complete the Planning Checklist 1 Abbreviations for applications and
directories 1 Known issue: Base Licenses are not installed with Trial
Keys package 1 \[Optional\] Staging a test environment for the upgrade
process **Note: This is not in the outline anymore but should be.** 1
Install CLM 4.0.x 1 Optional: Online migration of quality management
data 1 Backup the WebSphere Application Server profile 1 Uninstall the
previously installed applications from WebSphere Application Server 1
Update JAZZ_HOME and log4j.configuration custom properties 1 Stop the
WebSphere Application Server 1 Clean up the WebSphere Application Server
temp directories 1 Clean up the logs directory 1 Backup the indices 1
Backup the database 1 Verify index locations 1 Run the upgrade script 1
Start the WebSphere Application Server 1 Deploy the 4.0.x war files in
WebSphere Application Server 1 Start the applications 1 Version 4.0.x
and licenses 1 \[In case of RM\] Migrating the Requirements Management
application 1 \[In case of RRDI\] Upgrade Rational Reporting for
Development Intelligence 1 Redeploying predefined templates 1
Verification Checklist

## Workshop Environment

Windows 2008 R2 64-bit, WebSphere Application Server v7.0.0.15 or
higher, DB2 9.7 Enterprise Server, RTC 3.0.1.3, RQM 3.0.1.3, and RRC
3.0.1.3

**NOTE:** CLM 2012 only supports 64 bit OS platforms. There is no 32-bit
support. For more information, see [CLM System
Requirements](DeploymentInstallingUpgradingAndMigrating)

The workshop environment assumes the CLM applications are all deployed
on a single Microsoft Windows machine (perhaps a VM) but distributed
across 4 application server profiles in order to simulate a distributed
topology. However, the workshop can be performed across multiple
machines (Linux or Windows) just as easily. In this environment, we do
not need to be concerned with synchronization of the clocks on all
machines hosting a CLM application. This step appears as part of the IUG
but is not covered here.

## Reporting Considerations

In CLM 2011, the common data warehouse (DW) and RRDI v1.0.2 were
introduced. By now, most users will have configured a DW at the time
that they installed or upgraded to 3.0.1.x, or shortly thereafter. If
you have not configured a DW yet, you should wait to do so until after
you upgrade all applications in your topology to v4.0.x. See this topic:
<http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.jazz.install.doc/topics/t_ugrade_configure_dw_late.html>

If you are using RRDI v1.0.2 or later, you will need to upgrade to RRDI
v2.0.x to work with CLM 4.0.x. Upgrade RRDI to 2.0 **AFTER** upgrading
to CLM 2012. For more information, visit the [Upgrading
RRDI](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.rational.rrdi.admin.doc/topics/c_upgrading_rrdi.html)
topic. **NOTE:** This upgrade order is a change from previous
recommendations made for CLM 2012.

\#PlanningTheUpgrade

## Planning the Upgrade

Prior to upgrading to CLM 4.0.x, you should read the following topics:

<http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.jazz.install.doc/topics/c_planning_upgrade.html>

Upgrading from version 2 is a two-step process. First, upgrade to
version 3.0.1.6 or higher and then upgrade to CLM 4.0.x. See [Upgrading
from version
2](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.jazz.install.doc/topics/c_upgrade_to_301.html).

Pay attention to the bulleted list called "Important Notes" generated by
the Interactive Upgrade Guide.

## Licensing

If you are still using Early Access licenses with a 3.0.1.x deployment,
then the upgrade to 40x will convert these licenses to 4.0.xx Early
Access licenses. In a 'real'customer scenario with a 3.0.1.x deployment,
you most probably have floating, token, or Authorized User Single
Install client access licenses (CALs).

The upgrade process will not convert your existing CALs from 3.0 to
4.0.x. As part of the 4.0.x installation of the Jazz Team Server (JTS),
you will need to install the 'Required Base License Key' package. See
screenshot for what this looks like in Installation Manager.

This package installs Early Access trial licenses. Once the Early Access
trial licenses are installed, they still need to be activated. In a
distributed deployment, this should be done when the JTS is upgraded and
prior to subsequently upgrading any other registered applications. The
4.0.x applications only work with 4.0 licenses. The Early Access trial
licenses once activated allow you to use the 4.0.x applicatons until you
have a chance to obtain your purchased CALs.

Review the section in the generated interactive upgrade guide called
**Version 4.0.x and licenses** for the most up to date information.

## Upgrade RRC and JTS

Begin by generating an upgrade guide for RRC using the [4.0.x Infocenter
Upgrade and Migrating
Guide](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html).
Select 'Jazz Team Server, Requirements Management, CLM 3.0.1 or any fix
pack of that version, I distribute applications on multiple servers,
Yes, I can mount shared directories or drives, Microsoft Windows, IBM
WebSphere Application Server, IBM DB2, Yes, I have configured data
warehouse in CLM 3.0.1, No (RRDI), No (integrate with other products).

Proceed with the following steps: (replace '40x' below with a name
compatible with your environment)

-   Install CLM 40x JTS to c:\upgradews\JTS40x
-   Install CLM 40x RRC to c:\upgradews\RRC40x
-   Backup the JTS WAS profile on AppSrv04 and RRC WAS profile on
    AppSrv03
-   Backup the JTS and DW database.
-   Backup the JTS index files
-   Uninstall the JTS application from AppSrv04
    -   Remove jts.war, admin.war and clmhelp.war
-   Update the JAZZ_HOME and log4j properties to point to the JTS40
    server installation directory. JAZZ_HOME =
    <file:///C:/UpgradeWS/IBM/JTS40/server/conf>

log4j.configuration=
<file:///C:/UpgradeWS/IBM/JTS40/server/conf/startup_log4j.properties>

-   Stop AppSrv04
-   Clean up the temp directories for AppSrv04.
    -   Delete
        C:\upgradews\WebSphere\AppServer\profiles\appsrv04\temp\\server1\jts_war
    -   C:\upgradews\WebSphere\AppServer\profiles\appsrv04\temp\\server1\admin_war
    -   C:\upgradews\WebSphere\AppServer\profiles\appsrv04\temp\\server1\clmhelp_war
    -   If it exists, delete
        C:\upgradews\WebSphere\AppServer\profiles\appsrv04\wscache\jts_war
    -   If it exists, delete
        C:\upgradews\WebSphere\AppServer\profiles\appsrv04\wscache\admin_war
    -   If it exists, delete
        C:\upgradews\WebSphere\AppServer\profiles\appsrv04\wscache\clmhelp_war
-   Clean up the logs. Make a backup copy of the existing jts**.log,
    etl**.log and admin\*.log files. Then delete the existing logs so as
    to start with fresh logs with the 40 JTS and Admin applications.
-   Uninstall the RRC application from AppSrv03
    -   Remove rrc.war and converter.war
-   Update the JAZZ_HOME and log4j properties to point to the RRC40
    server installation directory. JAZZ_HOME =
    <file:///C:/UpgradeWS/IBM/RRC40/server/conf>

log4j.configuration=
<file:///C:/UpgradeWS/IBM/RRC40/server/conf/startup_log4j.properties>

-   Stop AppSrv03
-   Clean up the temp directories for AppSrv03.
    -   Delete
        C:\upgradews\WebSphere\AppServer\profiles\appsrv04\temp\\server1\rdm_war
    -   C:\upgradews\WebSphere\AppServer\profiles\appsrv04\temp\\server1\converter_war
    -   If it exists, delete
        C:\upgradews\WebSphere\AppServer\profiles\appsrv04\wscache\rdm_war
    -   If it exists, delete
        C:\upgradews\WebSphere\AppServer\profiles\appsrv04\wscache\converter_war
-   Clean up the logs. Make a backup copy of the existing rdm**.log and
    rrdg**.log files. Then, delete the existing logs so as to start
    fresh logs with the 40 RM application.

<!-- -->

-   REDNot needed if upgrading from 3.0.1.6ENDCOLORVerify the Index
    locations In both Tomcat and Websphere Application Server
    deployments, it is important to pay attention to your index file
    locations within the 3.0.1 teamserver.properties
    (\_3.0.1_install*dir\server\conf\\*) directory. There are 2 index
    file locations given in the following two properties:
    -   com.ibm.team.fulltext.index.location
        -   For Websphere, the default relative path value for full-text
            indices will actually be located relative to the path of the
            WAS profile hosting the application and not relative to your
            local installation, for example
            C:\upgradews\WebSphere\AppServer\profiles\appsrv04
        -   The fulltext index file location should always be an
            absolute path location.
    -   com.ibm.jfs.index.root.directory
        -   this JFS indices can use the JAZZ_HOME property if its value
            is left as the default relative path.

<!-- -->

-   RED **Note:** ENDCOLOR The indices from the previous release MUST be
    usable by the upgrade process. Both index file locations will get
    merged into your new configuration files as part of the upgrade
    script execution below. If the fulltext index location is relative,
    for example,
    com.ibm.team.fulltext.index.location=conf/jts/indices/workitemindex,
    indices must be moved to an absolute location. Perform this step
    prior to running the upgrade script. Change the relative path to the
    absolute path of the index location. In our workshop environment, it
    should be
    com.ibm.team.fulltext.index.location=c\\\\upgradews\\WebSphere\\AppServer\\profiles\\appsrv04\\conf\\jts\\indices\\workitemindex
    During the *repotools-rm* upgrade script execution, this will enable
    a copy of the indices to take place. . Verify that artifact search
    works, once the upgraded application is brought online.

<!-- -->

-   In order to ensure that the indices are usable, a repotools -reindex
    it is often run. There is a natural expectation that this will
    recreate an index. This is true but this causes an issue with
    upgrade: when repotools -reindex is run, upon completion it adds a
    reindexing request to the indexing queue. When the server next
    starts, it is read, and triggers reindexing - the extent of which is
    not usually comprehendable.

<!-- -->

-   Therefore the correct way to rebuild an index is in 3.x, prior to
    upgrade is:
    1.  Stop CLM 3.x 2. Change your teamserver.properties path for the
        indices to a new path, not under the 3.x installation, for
        example c\\\\CLMindices\\Instance1\\indices 3. Delete the
        existing indices directory, see above for details of where the
        relative path location defaults to 4. Start CLM 3.x 5. Wait for
        indexing to complete by ensuring all \_\_ values within
        <https://yourURI/jts/indexing> are set to 0, for example: 0 6.
        Stop CLM 3.x 7. Upgrade JTS, ensuring that when you run
        repotools-jts -upgrade, the teamserver.properties for both index
        locations is set to the new path. See below for a more detail on
        running this step.

<!-- -->

-   Go to the JTS 40 installation directory and run the jts_upgrade
    script. This will migrate the JTS configuration files from 301x
    to 40. Cd c:\upgradews\ibm\jts40\server Run upgrade\jts\jts_upgrade
    -oldJTSHome c:\upgradews\ibm\jts301x\server\conf updateTomcatFiles
    no During this time, the script will update the configuration files,
    add tables to your existing JTS database and upgrade the data
    warehouse schema. **NOTE:** During the execution of the upgrade
    script, a prompt for review of the JTS teamserver.properties will be
    presented. At this point, change the location of the index files to
    an absolute path of a stable location. A stable location is one that
    will not be deleted as part of an application uninstall for example.
    The upgrade script will perform a copy of the indices if there is an
    update during the prompt for review. For example,
    com.ibm.team.fulltext.indexLocation=JTS_4.0_install_dir/server/conf/jts/indices/workitemindex
    where JTS_4.0_install_dir is the location where Jazz Team Server 4.0
    application is installed. **NOTE:** If the script prompts for a
    re-index or rebuildtextindices operation, this is an un-necessary
    step that has been observed intermittently in test. It can be safely
    skipped. In large repositories, this will save you alot of time.
    Your indices from v301 are compatible with v40. And, if you followed
    the instructions above, the indices should be located at the
    locations identified by the 2 properties:
    com.ibm.team.fulltext.index.location,
    com.ibm.jfs.index.root.directory. If artifact search works after the
    upgrade, then your indices are fine.
-   Start AppSrv04
-   Deploy the 4.0 JTS WAR files.
    -   There will be 3 WAR files to deploy: jts, admin and clmhelp. For
        details on the steps for deploying these WAR files to WAS, see
        this topic:
        <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.jazz.install.doc/topics/t_deploy_was.html>
-   Start the JTS applications: JTS, Admin and CLMHelp
-   Install and Activate the licenses.
    -   Open a web browser and go to the following URL:
        <https://jts.clm.upgrade.ws:9446/jts/admin#action=com.ibm.team.repository.admin.manageLicenses>
    -   Activate, at a minimum, the following licenses: RRC Analyst, RRC
        Contributor, RQM Quality Professional, RQM Contributor, RTC
        Developer, RTC Build System, RTC Contributor **NOTE:** If you
        have v30 floating, token or Authorized Single User Licenses
        installed, install the v40 equivalents at this time. By default,
        only Early Access (EA) licenses are installed with the Required
        Base license keys package. If you have one of the other types of
        licenses in use, there is no automatic license assignment for
        any user from that license type to the EA license. But, if you
        install the v40 floating license and had v30 floating licenses,
        then there will be automatic license assignment done for all
        users in the system.
-   Switch to the RRC 40 Installation environment and run the rm_upgrade
    script. This will migrate the RRC configuration files from 301x
    to 40. Cd c:\upgradews\ibm\rrc40\server Run upgrade\rdm\rm_upgrade
    -oldJTSHome c:\upgradews\ibm\jts301\server\conf -updateTomcatFiles
    no -newJTSHome=c:\upgradews\ibm\jts40\server\conf
    -oldApplicationHome=c:\upgradews\ibm\rrc301\server\conf **Note:**
    The log file for the command launched by the upgrade script will be
    located in the newJTSHome directory, not the RM server installation
    directory.
-   Start AppSrv03
-   Deploy the 4.0 RRC WAR files.
    -   There will be 2 WAR files to deploy: rdm, and converter. For
        details on the steps for deploying these WAR files to WAS, see
        this topic:
        <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.jazz.install.doc/topics/t_deploy_was.html>
-   Start the RM applications: RDM, and Converter
-   Make sure all other CLM applications associated with the JTS in this
    environment are all running.
-   Make sure that the JazzAdmin user has a v40 license assigned and
    activated prior to starting the RM Online migration. Go to the
    License Key Management page and the Users page of the JTS admin UI:
    <https://jts.clm.upgrade.ws:9446/jts/admin>
-   Run the RM Online Migration wizard.
-   REDNo longer needed with 4.0.6ENDCOLORRun a publish service
    initialize:
    <https://rrc.clm.upgrade.ws:9445/rdm/publish/initialize>. This will
    publish new templates for use with RRDG.
-   Redeploying predefined templates
    -   A project template called "Base" in previous versions was
        renamed to "Requirements Templates for Testers" in version
        4.0.6. To continue using this template after upgrade, you must
        update the lifecycle project templates. For detailed
        information, see Creating lifecycle projects from a template.

When the upgrade is complete, proceed with the verification steps listed
here:
<http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.jazz.install.doc/topics/t_update_post-mig_verif.html>

In addition, it is recommended that you verify the following:

-   All existing registered applications are operational. For example,
    start the application servers that are hosting RTC, RRC and RQM and
    verify that they are working with the upgraded JTS.
-   **NOTE:** In the workshop environment, we are running with RQM
    3.0.1.3. Thus, we can proceed with the next step. If you are not
    running RQM 3.0.1.3, you will need to upgrade to that level in order
    for the RQM Java ETLs to run properly with a 4.0 DW schema. See the
    Planning the upgrade section for more details.
-   Run the data collection jobs and check the status for any errors.
    The data collection jobs must be run from the JTS Admin UI Reports
    page.
    <https://jts.clm.upgrade.ws:9446/jts/admin#action=com.ibm.team.reportsManagement.etlConfig>
    -   Run the following action: Run all data warehouse collection jobs
        for all jobs. The ETLs for applications that have been upgraded
        will then take care of performing any necessary migration of
        data in the data warehouse repository.
-   Search for artifacts within the registered applications to ensure
    the indices are all valid.
-   Run diagnostics on each server and verify the diagnostics complete
    successfully.

## Upgrade RTC

Next, generate an upgrade guide for Rational Team Concert. Select Change
and Configuration Management, CLM 3.0.1 or any fix pack of that version,
I distribute my applications on multiple servers, Yes, I can mount
shared directories or drives, Microsoft Windows, IBM WebSphere
Application Server, IBM DB2, Yes, I have configured data warehouse in
CLM 3.0.1, No (RRDI), No (integrate with other products).

Proceed with the following steps: (replace '40x' below with a name
compatible with your environment)

-   install CLM 40x RTC to c:\upgradews\RTC40
-   Backup the RTC WAS profile on AppSrv01
-   Backup the RTC database
-   Uninstall the RTC application from AppSrv01
-   Update the JAZZ_HOME and log4j properties to point to the RTC40
    server installation directory. JAZZ_HOME =
    <file:///C:/UpgradeWS/IBM/RTC40/server/conf>

log4j.configuration=
<file:///C:/UpgradeWS/IBM/RTC40/server/conf/startup_log4j.properties>

-   Stop AppSrv01
-   Clean up the temp directories for AppSrv01.
    -   Delete
        C:\upgradews\WebSphere\AppServer\profiles\appsrv01\temp\\server1\jazz_war
    -   If it exists, delete
        C:\upgradews\WebSphere\AppServer\profiles\appsrv01\wscache\jazz_war
-   Clean up the logs. Make a backup copy of the existing jazz\*.log
    files. Delete the existing log files.
-   Verify the Index locations Not needed if upgrading from 3.0.1.6 In a
    WAS deployment, it is important to pay attention to your index file
    locations in the 3.0.1 teamserver.properties file, which is located
    in 3.0.1_install_dir\server\conf\\ directory. There are 2 index file
    locations given in the following two properties:
    com.ibm.team.fulltext.index.location,
    com.ibm.jfs.index.root.directory. The JFS indices
    (com.ibm.jfs.index.root.directory) uses the JAZZ_HOME property if
    its value is left as the default relative path. The fulltext indices
    (com.ibm.team.fulltext.index.location), if left as the default
    relative path value, will actually be located relative to the path
    of the WAS profile hosting the application, i.e.
    C:\upgradews\WebSphere\AppServer\profiles\appsrv01. You may have
    assumed it was relative to your local installation. In a WAS
    deployment, the fulltext index file location should always be an
    absolute path location. Both index file locations will get merged
    into your new configuration files as part of the upgrade script
    execution below. If the fulltext index location is relative, for
    example,
    com.ibm.team.fulltext.index.location=conf/jts/indices/workitemindex,
    perform this step prior to running the upgrade script. Change the
    relative path to the absolute path of the index location. In our
    workshop environment, it should be
    com.ibm.team.fulltext.index.location=c:\upgradews\WebSphere\AppServer\profiles\appsrv01\conf\jazz\indices\workitemindex
    During the upgrade script execution, this will enable a copy of the
    indices to take place. If the 301x index locations already contained
    absolute paths and pointed to a stable location, then no further
    action is necessary. Verify that artifact search works, once the
    upgraded application is brought online.
-   Run the upgrade script. This will migrate the RTC configuration
    files from 301x to 40. Cd c:\upgradews\ibm\rtc40\server Run
    upgrade\jazz\ccm_upgrade
    -newJTSHome=c:\upgradews\ibm\jts40\server\conf
    -oldApplicationHome=c:\upgradews\ibm\rtc301\server\conf
    updateTomcatFiles no During this time, the script will update the
    configuration files and add tables to your existing RTC database.
    **NOTE:** During the execution of the upgrade script, a prompt for
    review of the CCM teamserver.properties will be presented. At this
    point, change the location of the index files to an absolute path of
    a stable location. A stable location is one that will not be deleted
    as part of an application uninstall for example. The upgrade script
    will perform a copy of the indices if there is an update during the
    prompt for review. For example,
    com.ibm.team.fulltext.indexLocation=CCM_4.0_install_dir/server/conf/jts/indices/workitemindex
    where CCM_4.0_install_dir is the location where CCM 4.0 application
    is installed. **NOTE:** If the script prompts for a re-index or
    rebuildtextindices operation, this is an un-necessary step that has
    been observed intermittently in test. It can be safely skipped. In
    large repositories, this will save you alot of time. Your indices
    from v301 are compatible with v40. And, if you followed the
    instructions above, the indices should be located at the locations
    identified by the 2 properties:
    com.ibm.team.fulltext.index.location,
    com.ibm.jfs.index.root.directory. If artifact search works after the
    upgrade, then your indices are fine.
-   Start AppSrv01
-   Deploy the 4.0.x RTC WAR file.
    -   There will be 1 WAR files to deploy: jazz. For details on the
        steps for deploying these WAR files to WAS, see this topic:
        <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.jazz.install.doc/topics/t_deploy_was.html>
-   Start the RTC application: Jazz
-   Stop and restart AppSrv01 When the upgrade is complete, proceed with
    the verification steps listed here:
    <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.jazz.install.doc/topics/t_update_post-mig_verif.html>

In addition, it is recommended that you verify the following:

-   All existing registered applications are operational.
-   Run the data collection jobs and check the status for any errors.
    The data collection jobs must be run from the JTS Admin UI Reports
    page.
    <https://jts.clm.upgrade.ws:9446/jts/admin#action=com.ibm.team.reportsManagement.etlConfig>
    -   Run the following action: Run all data warehouse collection jobs
        for all jobs. The ETLs for applications that have been upgraded
        will then take care of performing any necessary migration of
        data in the data warehouse repository.
-   Search for artifacts within the registered applications to ensure
    the indices are all valid.
-   Run diagnostics on each server and verify the diagnostics complete
    successfully.

## Upgrade RQM

Next, generate an upgrade guide for Rational Quality Manager. Select
Quality Management, CLM 3.0.1 or any fix pack of that version, I
distribute my applications on multiple servers, Yes, I can mount shared
directories or drives, Microsoft Windows, IBM WebSphere Application
Server, IBM DB2, Yes, I have configured data warehouse in CLM 3.0.1, No
(RRDI), No (integrate with other products).

Proceed with the following steps:

-   Install CLM 40x RQM to c:\upgradews\RQM40
-   Backup the RQM WAS profile on AppSrv02
-   Backup the RQM database.
-   Uninstall the RQM application from AppSrv02
-   Update the JAZZ_HOME and log4j properties to point to the RQM40
    server installation directory. JAZZ_HOME =
    <file:///C:/UpgradeWS/IBM/RQM40/server/conf>

log4j.configuration=
<file:///C:/UpgradeWS/IBM/RQM40/server/conf/startup_log4j.properties>

-   Stop AppSrv02
-   Clean up the temp directories for AppSrv02.
    -   Delete
        C:\upgradews\WebSphere\AppServer\profiles\appsrv02\temp\\server1\jazz_war
    -   If it exists, delete
        C:\upgradews\WebSphere\AppServer\profiles\appsrv02\wscache\jazz_war
-   Clean up the logs. Make a backup copy of the existing jazz\*.log
    files. Delete the existing log file.
-   Verify the Index locations In a WAS deployment, it is important to
    pay attention to your index file locations in the 3.0.1
    teamserver.properties file, which is located in
    3.0.1_install_dir\server\conf\\ directory. There are 2 index file
    locations given in the following two properties:
    com.ibm.team.fulltext.index.location,
    com.ibm.jfs.index.root.directory. The JFS indices
    (com.ibm.jfs.index.root.directory) uses the JAZZ_HOME property if
    its value is left as the default relative path. The fulltext indices
    (com.ibm.team.fulltext.index.location), if left as the default
    relative path value, will actually be located relative to the path
    of the WAS profile hosting the application, i.e.
    C:\upgradews\WebSphere\AppServer\profiles\appsrv02. You may have
    assumed it was relative to your local installation. In a WAS
    deployment, the fulltext index file location should always be an
    absolute path location. Both index file locations will get merged
    into your new configuration files as part of the upgrade script
    execution below. If the fulltext index location is relative, for
    example,
    com.ibm.team.fulltext.index.location=conf/jts/indices/workitemindex,
    perform this step prior to running the upgrade script. Change the
    relative path to the absolute path of the index location. In our
    workshop environment, it should be
    com.ibm.team.fulltext.index.location=c:\upgradews\WebSphere\AppServer\profiles\appsrv02\conf\jazz\indices\workitemindex
    During the upgrade script execution, this will enable a copy of the
    indices to take place. If the 301x index locations already contained
    absolute paths and pointed to a stable location, then no further
    action is necessary. Verify that artifact search works, once the
    upgraded application is brought online.
-   Run the upgrade script. This will migrate the RQM configuration
    files from 301x to 40.
    -   Cd c:\upgradews\ibm\rqm40\server
    -   Run upgrade\jazz\qm_upgrade -updateTomcatFiles no
        -newJTSHome=c:\upgradews\ibm\jts40\server\conf
        -oldApplicationHome=c:\upgradews\ibm\rqm301\server\conf
        **NOTE:** During the execution of the upgrade script, a prompt
        for review of the QM teamserver.properties will be presented. At
        this point, change the location of the index files to an
        absolute path of a stable location. A stable location is one
        that will not be deleted as part of an application uninstall for
        example. The upgrade script will perform a copy of the indices
        if there is an update during the prompt for review. For example,
        com.ibm.team.fulltext.indexLocation=QM_4.0_install_dir/server/conf/jts/indices/workitemindex
        where QM_4.0_install_dir is the location where CCM 4.0
        application is installed. **NOTE:** If the script prompts for a
        re-index or rebuildtextindices operation, this is an
        un-necessary step that has been observed intermittently in test.
        It can be safely skipped. In large repositories, this will save
        you alot of time. Your indices from v301 are compatible with
        v40. And, if you followed the instructions above, the indices
        should be located at the locations identified by the 2
        properties: com.ibm.team.fulltext.index.location,
        com.ibm.jfs.index.root.directory. If artifact search works after
        the upgrade, then your indices are fine.
-   Start AppSrv02
-   Deploy the 4.0.x RQM WAR file.
    -   There will be 1 WAR files to deploy: jazz. For details on the
        steps for deploying these WAR files to WAS, see this topic:
        <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.jazz.install.doc/topics/t_deploy_was.html>
-   Start the RQM application: Jazz
-   Stop and restart AppSrv02

In addition, it is recommended that you verify the following:

-   All existing registered applications are operational.
-   Run the data collection jobs and check the status for any errors.
    The data collection jobs must be run from the JTS Admin UI Reports
    page.
    <https://jts.clm.upgrade.ws:9446/jts/admin#action=com.ibm.team.reportsManagement.etlConfig>
    -   Run the following action: Run all data warehouse collection jobs
        for all jobs. The ETLs for applications that have been upgraded
        will then take care of performing any necessary migration of
        data in the data warehouse repository.
-   Search for artifacts within the registered applications to ensure
    the indices are all valid.
-   Run diagnostics on each server and verify the diagnostics complete
    successfully.

## Troubleshooting and FAQ

Here are some frequently asked questions (FAQs) and tips on some things
to do if you encounter any issues during or after the upgrade.

**What are the supported CLM 4.0.x supported upgrade paths?** See the
spreadsheet attached to [workitem
218962](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.workitem.viewWorkItem&id=218962)
for the information. It also covers build engine compatibility, client
compatibility, and reporting migration.

**My RRC Online migration failed. How do I recover?** If you encounter
any errors or issues with the RRC Online migration, you will need to
repeat the online migration. If so, restore the copy of the JTS database
and restart the upgrade process from that point. If you have a
distributed setup, I recommend backing up the JTS after its own upgrade
so that if RRC Online migration must be repeated you can restore to this
backup copy of the JTS. This avoids having to repeat the JTS upgrade
process.

**The RRC Online migration is not running. What could be the problem?**
In order to run RM Online migration, you must be logged in as a user
with JazzAdmins privileges and this user must be assigned a 4.0 Analyst
license. Check this on the JTS Admin UI under Users Administration and
License Key Management. Next, check the rm.log in the WAS profile logs
directory or the Tomcat logs directory.

**I started one of my applications and I cant execute an artifact
query?** You need to inspect the following property
com.ibm.team.fulltext.indexLocation in your applications
teamserver.properties file. There may be a mismatch between the location
listed there and where the server is looking for the indices. For
example, if the property still points to a relative path and you are
using WAS, you may find in the applications log file that the Fulltext
index location is pointing to a directory such as
C:\UpgradeWS\WebSphere\AppServer\profiles\AppSrv01\conf\jazz\indices\workitemindex\fulltext_index
which in fact does not contain the indices. To resolve, stop the server.
Edit the teamserver.properties file and convert the relative path to an
absolute path where the indices are actually located such as
C:\\server\conf\jazz\indices\workitemindex\fulltext_index.

**I never configured a DW for my 301x environment. What do I do now?**
You can configure a DW either before the upgrade to v4.0 or after. You
will need to run JTS setup which will walk you through the steps to
complete the DW configuration. However, please note that if you choose
to configure it after the upgrade to v4.0, do this only after all
applications in your topology (all applications that are shared by one
JTS) are upgraded to v4.0. This will ensure that the JTS setup steps are
all running against v4.0 applications.

**Can I rename my server prior to upgrading to 40?** No, server rename
is only possible with the 40 release and is only supported for staging a
test environment, not renaming a production environment. Thus, you must
upgrade to 40 prior to attempting a server rename.

**I have a distributed CLM deployment but I cannot mount drives between
the various machines. Are there special upgrade processes to follow in
that case?** We cover this case in the 4.0 interactive guide. Just
select the option for distributed deployment and that mounting drives is
not possible. Generate a guide for each of the distributed applications
you plan to upgrade. All applications with the exception of RM can be
upgraded without having to connect to the JTS machine.

**Where can I find workarounds, technotes or late-breaking updates for
the 4.0.x release?** Workaround articles will be published on Jazz.net.
A workaround article is a jazz.net article used to document a single
issue applicable to one or more GA releases. Here are some shortcuts to
help you find what you need. Note: Change the 4.0.x below to match the
latest GA release

-   <https://jazz.net/library/#q=&tag=workaround,4.0.6&project=rational-team-concert>
-   <https://jazz.net/library/#q=&tag=workaround,4.0.6&project=rational-quality-manager>
-   <https://jazz.net/library/#q=&tag=workaround,4.0.6&project=rational-requirements-composer>
-   <https://jazz.net/library/#q=&tag=workaround,4.0.6&project=jazz-foundation>
-   <https://jazz.net/library/#q=&tag=workaround,2.0.6&project=rrdi>

## Next Steps

-   Prepare a staging test environment. Here is a reference on that
    topic:
    <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.jazz.install.doc/topics/c_upgrade_staging_env.html>
-   Download [CLM
    4.0.6](https://jazz.net/downloads/rational-team-concert/releases/4.0.6)

##### Related topics: None [related-topics-none]

##### External links: [external-links]

-   [CLM 4.0.6 Interactive Upgrade
    Guide](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html)
    (IUG)
-   [CLM Improve Upgrade
    (169175)](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/169175)
-   [Confirm supported paths for upgrading to CLM 2011 fixpacks and CLM
    2012
    (174745)](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/174745)
-   [Confirm supported paths for upgrading to CLM 2012 fixpacks and mod
    packs
    (218962)](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.workitem.viewWorkItem&id=218962)
-   [Confirm supported paths for upgrading to CLM 5.0 fixpacks and mod
    packs
    (299988)](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.workitem.viewWorkItem&id=299988)
-   [CLM System Requirements](DeploymentInstallingUpgradingAndMigrating)

##### Additional contributors: Main.SudarshaWijenayake, Main.GailBurati, Main.PaulEllis, Main.AlastairStewart [additional-contributors-main.sudarshawijenayake-main.gailburati-main.paulellis-main.alastairstewart]

META:FILEATTACHMENT{name="RequiredBaseLicenseKeys.png"
attachment="RequiredBaseLicenseKeys.png" attr="h" comment=""
date="1392136974" path="RequiredBaseLicenseKeys.png" size="41473"
user="rnaranjo" version="2"} META:FILEATTACHMENT{name="topology.gif"
attachment="topology.gif" attr="h" comment="" date="1362585738"
path="topology.gif" size="37669" user="rnaranjo" version="1"}
META:TOPICMOVED{by="rnaranjo" date="1392133227"
from="Deployment.CLM2012UpgradeGuide" to="Deployment.CLMUpgradeGuide"}
