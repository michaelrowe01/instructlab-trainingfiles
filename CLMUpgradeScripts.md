META:TOPICINFO{author="sbagot" date="1432745884" format="1.1"
version="1.16"} META:TOPICPARENT{name="CLMUpgradeTroubleshooting"}

# Running the upgrade scripts [running-the-upgrade-scripts]

Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam) Build
basis: CLM 3.x and later ENDCOLOR

TOC{title="Page contents"}

This page discusses common issues which are occured when running the CLM
Upgrade Scripts. When running the upgrade script files to upgrade CLM
applications, you might run into these common issues:

## CLM common upgrade questions

This section is currently in progress and will discuss running upgrade
scripts in a distributed environment.

## Known issues

Below are some common issues incurred when running the upgrade scripts
prior to step 0:

### Old Jazz Team Server version could not be determined

The Jazz Team Server upgrade script might fail with the following error:
CRJAZ2124E The old JTS version could not be determined. Verify that the
oldJTSHome is pointed at the correct installation and specify the
version using the old JTSVersion parameter. For more information on this
error navigate to [JTS Upgrade Script fails with "Old JTS version could
not be determined" error](OldJTSVersion).

### RM_upgrade.bat terminated at startup

The RM_Upgrade.bat might be terminated at startup in non-English
environments. For more information on this behavior, navigate to
[RM_Upgrade.bat is terminated in Non-English
environments](NonEnglishEnvironment).

## Additional steps in the upgrade script

AFter you have moved past step 0 of running the upgrade script, you
might incur issues at the following steps:

-   [Update configuration files (CCM, QM,
    JTS)](UpdateConfigurationFiles)
-   [Add database tables (CCM, QM, JTS)](AddDatabaseTables)
-   [Upgrade DW Schema (JTS)](UpgradeDwSchema)

## Troubleshooting

When the upgrade scripts run, each is executing a set of repotools
commands. If the scripts fail, adding in [repotools
trace](http://www-01.ibm.com/support/docview.wss?uid=swg21322003) can
help identify why the script is failing.

## Where do I go from here? If you are unable to resolve your issue using the available online resources, please open a service request with IBM Rational Support. Refer to [Additional Troubleshooting Resources](DataCollectionandSupportResources) for further details.

##### Related topics: \* [DeploymentTroubleshooting](DeploymentTroubleshooting) [related-topics-deploymenttroubleshooting]

##### External links: [external-links]

-   None

##### Additional contributors: Main.WilliamChen, Main.BrettBohnn [additional-contributors-main.williamchen-main.brettbohnn]

##### Questions and comments: [questions-and-comments]

META:TOPICMOVED{by="wbchen" date="1367976962"
from="Deployment.CLMUpgradeScript" to="Deployment.CLMUpgradeScripts"}
