META:TOPICINFO{author="sbagot" date="1432745427" format="1.1"
version="1.12"} META:TOPICPARENT{name="UpgradeTroubleshooting"}

# RRDI upgrade troubleshooting [rrdi-upgrade-troubleshooting]

DKGRAY Authors: Main.StephanieBagot,
[UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam) Build basis:
CLM 3.x and later, RRDI 2.x and later ENDCOLOR

TOC{title="Page contents"}

This page is the starting point for information and techniques to help
diagnose and troubleshoot upgrade issues when upgrading Rational
Reporting for Development Intelligence (RRDI) servers.

## Before upgrading

-   Check the [Known
    issues](https://jazz.net/wiki/bin/view/Deployment/RRDIKnownIssues)
    as a prerequisite for the upgrade
-   [Backup your current RRDI
    Configuration](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.rational.rrdi.admin.doc/topics/t_postupgrade_backup.html&scope=null)
-   Ensure that your current environment meets all the requirements by
    checking the [Environment checklist](EnvironmentCheckList) and
    [Version
    Compatibility](https://jazz.net/wiki/bin/view/Deployment/VersionCompatibilityCLMRRDIAndInsight)
-   Perform the upgrade in a test environment prior to upgrading your
    production environment

### Upgrade Philosophy During an RRDI Upgrade, you may be advised on some 'philosophies' on how to be best successful in your upgrade. Below we discuss some of these items.

#### Always upgrade CLM before RRDI

We advise the upgrade of CLM prior to RRDI to ensure that the data
warehouse is at the correct level prior to an RRDI upgrade. If you
choose to upgrade RRDI first, be prepared to see a "The datawarehouse
was created by a previous version" error. The workaround is discussed
below under Performing the Upgrade.

#### Always keep RRDI and CLM at the same version level

This is a recommendation to ensure that you are using a tested
compatible version of both products, as well as utilizing all features
or changes. However, this is not a hard rule. See [Version
Compatibility](https://jazz.net/wiki/bin/view/Deployment/VersionCompatibilityCLMRRDIAndInsight)
for more information on which versions are supported together if you
cannot keep RRDI and CLM at the same version.

#### You must download RRDI Installation Repository to install

While you have the option to download the RRDI Installation Repository
from jazz.net to install RRDI, you can also upgrade in-place referencing
the repositories on jazz.net.

## Performing the upgrade

This section will discuss known issues that can occur during the
outlined steps of the upgrade for the Rational Reporting for Development
Intelligence server.

### Install the new version RRDI

-   Some installation issues:

[Technote 1665912: RRDI Installation or upgrade fails with wrong
MD5](http://www-01.ibm.com/support/docview.wss?uid=swg21665912)

[Technote 1567843: Installation fails with error "CRRRD4515E Error
creating table
spaces"](http://www-01.ibm.com/support/docview.wss?uid=swg21567843)

### Starting the setup wizard for RRDI and proceeding with its configuration

-   The following article [Workarounds: Setup problems in RRDI
    2.0.3](https://jazz.net/library/article/1294) discusses known issues
    with RRDI Setup problems

#### Error "The datawarehouse was created by a previous version"

This error is indicative that the datawarehouse used by a CLM
application was created with an older version. For example, if you are
upgrading RRDI to 2.0., this error may occur if CLM is at version 3.0.1.
This error is document in [Technote 1614140: Running RRDI Setup during
upgrade results in Previous Version
error](http://www-01.ibm.com/support/docview.wss?uid=swg21614140).

#### Deploying report resources results in CRRRA2083E

Upon deploying the report resources in the setup wizard for RRDI, the
following error is seen: CRRRA2083E: Cannot connect to the report server
For information on this error, see [Technote 1652043: Upgrading RRDI
results in CRRRA2083E error during RRDI
setup](http://www-01.ibm.com/support/docview.wss?uid=swg21652043)

### Uninstalling the previous version of RRDI

## Issues during upgrade

If the setup fails, consult the technote [MustGather: Diagnostic
information for IBM Rational Reporting Development Intelligence and
Insight](http://www-01.ibm.com/support/docview.wss?uid=swg21645071)
section RRDI/Insight Setup Wizard for logs

Additional tips may be found under this topic: [Troubleshooting the
upgrade of Rational Reporting for Development
Intelligence](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.rational.rrdi.admin.doc/topics/r_upgrade.html&scope=null)

### Proceeding through the steps manually

In some cases, it may be necessary to proceed through a step manually.
These steps are not detailed in the Information Center. There is an
[Enhancement
(53215)](http://www.ibm.com/developerworks/rfe/execute?use_case=viewRfe&CR_ID=53215)
open to have the manual steps documented. Here are the detailed steps
for the setup wizard:

1\. Configure Database Management System

2\. Configure Content Store Database

-   [Creating the database for the content
    store](https://jazz.net/help-dev/clm/topic/com.ibm.rational.rrdi.admin.doc/topics/t_configure_content_store_combine.html)
-   During the setup, save configuration scripts to run after you finish
    deploying the report server.
-   [Configure connection to the Content
    Store](http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/index.jsp?topic=2Fcom.ibm.rational.rcpr.help.doc2Ftopics2Ft_add_content_store_object.html)

3\. Configure Data Warehouse

\* Create data warehouse \* [Populate data
warehouse](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fr_repotools_createwarehouse.html)
repotools-jts -createWarehouse

-   Connect report server to data warehouse

4\. [Configure Application
Server](http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/index.jsp?topic=2Fcom.ibm.rational.rcpr.help.doc2Ftopics2Ft_postreq_reportalserver_db2isdw_repservISwas.html)

5\. Configure Rational Reporting User Authentication

6\. [Build and Deploy Reporting
Components](http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/index.jsp?topic=2Fcom.ibm.rational.rcpr.help.doc2Ftopics2Ft_postreq_reportalserver_db2isdw_repservISwas.html)

#### How to Reinitialize the Setup Wizard

User data (all values entered in the RRDI Setup Wizard) is persisted in
a triple store database as a collection of files in the
\[RRDI-Install-Location\]/setup/tool/JazzTeamServer/server/conf/rrdi/repository
directory. You may want to re-initialize the setup wizard without having
to reinstall. For example, you need to reset the password or change a
port. Here are the steps:

1\. Back up all the files in
\[RRDI-Install-Location\]/setup/tool/JazzTeamServer/server/conf/rrdi/repository
directory

2\. Delete the content of this directory.

3\. Start the RRDI Setup Wizard again

4\. Re-enter values for all the steps and fields in the Wizard. This
will update the RRDI Setup Wizard's configuration data.

## Issues after upgrade

-   Check the [documented
    workarounds](https://jazz.net/library/#q=&tag=workaround2C2.0&project=rrdi&sort=pubDate)
    for known issues

## Where do I go from here? If you are unable to resolve your issue using the available online resources, open a service request with IBM Rational Support. Refer to [Additional troubleshooting resources](DataCollectionandSupportResources) for further details.

##### Related topics: None [related-topics-none]

##### External links: \* None [external-links-none]

##### Additional contributors: Main.AntoinetteIacobo [additional-contributors-main.antoinetteiacobo]
