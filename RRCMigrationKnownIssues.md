META:TOPICINFO{author="dmmckinn" date="1432673091" format="1.1"
reprev="1.3" version="1.3"}
META:TOPICPARENT{name="CLMUpgradeTroubleshooting"}

# RDNG 4.0 to 5.x Migration: Known Issues [rdng-4.0-to-5.x-migration-known-issues]

Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam) Build
basis: CLM 5.x ENDCOLOR

TOC{title="Page contents"}

This topic discusses the migration of Rational Doors NG (formerly RRC)
in 5.0, where it is separated from the JTS database.

## Troubleshooting

During this step in the upgrade process, a log file will be created in
the ../server directory of the Collaborative Lifecycle Management (CLM)
application installation directory.

## Known Issues

Below are some known issues which arise during the RDNG Migration in the
upgrade process

### "Roll-Forward pending" error in log files

**Version:** Upgrade to 5.x, DB2 **Error During Upgrade:** After
restoring a copy of the JTS database for use as RM database, the log
files are flooded with "Roll-Forward pending" errors when connecting to
the database. **Cause:** This error occurs because the backup of the JTS
database was taken online. **Resolution:** Run the following SQL command
to resolve this error. db2 rollforward db RMDB to end of backup and
complete If the above SQL still results in the "Roll-Forward pending"
error in the log files, run the following command: db2 rollforward db
RMDB to end of logs and complete

### RM projects are listed "-Unresolved Context-"

**Version:** Upgrade to 5.x **Error During Upgrade:** After completing
the upgrade, RDNG projects will display as "-Unresolved Context-".
**Cause:** The finalize application step was skipped. **Resolution:**
Run the Finalize Application command from repotools. The applicationId
can be found in \server\rm_upgrade_rmUpgrade.log file. repotools-jts.bat
-finalizeApplicationMigration checkOauthDomain=true applicationId=xxxxx
newPublicUrl=<https://:9443/rm>

### Updating Project BackLinks Fails

**Version:** Upgrade to 5.x \* Make sure the CLM server is up and
running \* Make sure the User credentials you enter has the 5.0 license
assigned prior to completing this step. If you have token license server
setup, enable the trial licenses and assign a license to the user prior
to completing this step.

##### Related topics: [related-topics]

\* For more upgrade troubleshooting topics, refer to [Upgrade
Troubleshooting](UpgradeTroubleshooting).

##### External links: [external-links]

-   None

##### Additional contributors: Main.StephanieBagot [additional-contributors-main.stephaniebagot]
