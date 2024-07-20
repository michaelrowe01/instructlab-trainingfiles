META:TOPICINFO{author="sbeard" date="1368526416" format="1.1"
version="1.5"} META:TOPICPARENT{name="CLMUpgradeScripts"}

# RM_Upgrade.bat is terminated in Non-English environments [rm_upgrade.bat-is-terminated-in-non-english-environments]

DKGRAY Authors: Upgrade Troubleshooting Team Build basis: CLM 3.x and
later ENDCOLOR

TOC{title="Page contents"}

The RM_Upgrade.bat file may terminate upon initilization due to a
mis-configuration in a non-english environment. The information
contained on this page will help to bypass this behaviour.

## Running rm_upgrade script

The rm_upgrade script upgrades Jazz Team Server version 3.0.1.x or
4.0.0.x to 4.0.1 or later. Here is an example on running rm_upgrade
script on Windows and UNIX:

Example

Windows:

cd C:\Program Files\IBM\JazzTeamServer\Server\\
upgrade\rm\rm_upgrade.bat -oldApplicationHome
old_RM_install_dir\server\conf

UNIX:

cd opt/IBM/JazzTeamServer/Server/ ./upgrade/rm/rm_upgrade.sh
-oldApplicationHome old_RM_install_dir/server/conf

## Symptom

The rm_upgrade.bat will be terminated without any error messages. Once
the command is initialized, the command window will be closed out
immediately. However, there is no problem to run jts_upgrade.bat,
ccm_upgrade.bat and qm_upgrade.bat.

## Resolution

The parameter -oldJTSContextRoot is set incorrectly for Non-English
environment. You can resolve this issue by setting parameter
-oldJTSContextRoot to jts.

A working example with correct parameters is shown below for Windows and
UNIX.

Example

Windows:

cd C:\Program Files\IBM\JazzTeamServer\Server\\
upgrade\rm\rm_upgrade.bat -oldApplicationHome
old_RM_install_dir\server\conf -oldJTSContextRoot=jts
-newJTSContextRoot=jts

UNIX:

cd opt/IBM/JazzTeamServer/Server/ ./upgrade/rm/rm_upgrade.sh
-oldApplicationHome old_RM_install_dir/server/conf
-oldJTSContextRoot=jts -newJTSContextRoot=jts

##### Related topics: [DeploymentTroubleshooting](DeploymentTroubleshooting) [related-topics-deploymenttroubleshooting]

##### External links: \* None [external-links-none]

##### Additional contributors: Main.WilliamChen, Main.BrettBohnn [additional-contributors-main.williamchen-main.brettbohnn]

META:TOPICMOVED{by="wbchen" date="1367976306"
from="Deployment.NonEnglishEnvironments"
to="Deployment.NonEnglishEnvironment"}
