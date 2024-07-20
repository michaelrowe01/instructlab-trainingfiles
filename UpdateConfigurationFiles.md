META:TOPICINFO{author="sbagot" date="1432746275" format="1.1"
reprev="1.10" version="1.10"}
META:TOPICPARENT{name="CLMUpgradeTroubleshooting"}

# Update configuration files (CCM, QM, JTS) [update-configuration-files-ccm-qm-jts]

Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam) Build
basis: CLM 4.x ENDCOLOR

TOC{title="Page contents"}

This topic discusses the first step in the upgrade which updates the
configuration files for each application.

## Troubleshooting

During this step in the upgrade process, a log file appended with
\_migration\_\_updateConfigurationFiles will be created in the ../server
directory of the Collaborative Lifecycle Management (CLM) application
installation directory. An example of this file is:
repotools-jts_migration_jts_updateConfigurationFiles.log

## Known Issues

Below are some known issues which arise during the update configuration
files step in the upgrade process

### Errors which can occur with any CLM application

This section will discuss errors common when updating configuration
files which can occur with any of the CLM applications.

### "The version string is not properly formatted" error

**Version:** Upgrade to 4.x **Error During Upgrade:** The version string
" -Dcom.ibm.team.repotools.rcp.allowInvalidBundles=true" is not properly
formatted. java.lang.IllegalStateException: The version string "
-Dcom.ibm.team.repotools.rcp.allowInvalidBundles=true" is not properly
formatted. **Cause:** The 3.x jazzTeamServer directory was renamed to
x_orig and its old name was used for 4.0. There could be some files got
corrupted during the folder rename process **Resolution:** Ensure that
the original 3.0.1.3 directory name is kept and install 4.0 in a new
jazz home location. Keep both folders separate.

##### Related topics: [related-topics]

\* For more upgrade troubleshooting topics, refer to [Upgrade
Troubleshooting](UpgradeTroubleshooting).

##### External links: [external-links]

-   None

##### Additional contributors: Main.SusanWu [additional-contributors-main.susanwu]
