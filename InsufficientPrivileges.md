META:TOPICINFO{author="sbeard" date="1368525019" format="1.1"
version="1.6"} META:TOPICPARENT{name="CLMUpgradeScripts"}

# Why does qm_upgrade script fail with the error message `"java.sql.SQLException: ORA-01031: insufficient privileges?"` [why-does-qm_upgrade-script-fail-with-the-error-message-java.sql.sqlexception-ora-01031-insufficient-privileges]

DKGRAY Authors: Upgrade Troubleshooting Team Build basis: CLM 3.x and
later ENDCOLOR

TOC{title="Page contents"}

A very common problem when running qm_upgrade script is this error
message `"java.sql.SQLException: ORA-01031: insufficient privileges?"`.
You can follow below sections to resolve the error.

## Running qm_upgrade script

The qm_upgrade script upgrades Jazz Team Server version 3.0.1.x or
4.0.0.x to 4.0.1 or later. Here is an example on running qm_upgrade
script on Windows and UNIX:

Example

Windows:

cd C:\Program Files\IBM\JazzTeamServer\Server\\
upgrade\qm\qm_upgrade.bat -oldApplicationHome
old_QM_install_dir\server\conf

UNIX:

cd opt/IBM/JazzTeamServer/Server/ ./upgrade/qm/qm_upgrade.sh
-oldApplicationHome old_QM_install_dir/server/conf

## Resolution

The error message
`"java.sql.SQLException: ORA-01031: insufficient privileges?"` occurs
when qm_upgrade script attempts to add new tables to the QM repository
database but the database login ID for Oracle database does not have DBO
privileges. Other database vendors would raise similary SQL exception
messages.

The Quality Management application teamserver.properties file under
old_QM_install_dir\server\conf directory contains database schema
connection information, including login ID and password for current
database vendor. The login ID must have database DBO permission on all
CLM applications, including databases for jts, qm, ccm, dw and rm.

The creation of the warehouse on Oracle requires more permissions as
compared to other databases. When you specify the database user in the
connection spec for data warehouse, ensure that the database user has
DBA permissions. Then you can remove that privilege after data warehouse
configuration is complete.

##### Related topics: [DeploymentTroubleshooting](DeploymentTroubleshooting) [related-topics-deploymenttroubleshooting]

##### External links: \* None [external-links-none]

##### Additional contributors: Main.WilliamChen, Main.BrettBohnn [additional-contributors-main.williamchen-main.brettbohnn]
