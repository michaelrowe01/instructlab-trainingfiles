META:TOPICINFO{author="sbagot" date="1432746427" format="1.1"
version="1.12"} META:TOPICPARENT{name="CLMUpgradeTroubleshooting"}

# Migrating the requirements management application [migrating-the-requirements-management-application]

DKGRAY Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam)
Build basis: CLM 3.x and later ENDCOLOR

TOC{title="Page contents"}

This page will discuss the IBM Rational Requirements Requirement
Composer (RRC) migration step during the upgrade

## Migration types for the RRC 3.0.1.x to 4.0.x

Rational Requirements Composer (RRC) requires a two-stage upgrade
process. The offline upgrade, using the upgrade scripts, and the online
migration.

### RRC offline migration

The RRC offline migration consists of the rm_upgrade and jts_upgrade
scripts. For the 3.0.1.x to 4.0.1, 4.0.2, the offline migration copies
the full-text search and Jazz Team Server indices and merges
configuration/properties files (Tomcat files, server.xml and web.xml
files with the new version and copies the old version tomcat-users.xml
file, teamserver.proprties files based on the information from the
previous version, merges the old version friendsconfig.rdf file). The
offline migration is a much simpler process when upgrading from RRC
3.0.1.x to 4.0.x. Unlike the upgrade from 2.0.1.x to 3.0.1.x, the
offline migration does not move data from one repository to another (an
RM repository to a Jazz Team Server repository) using the repotools
export/import process.

### RRC online migration

During the online migration, RRC data is transformed (if necessary) to
any new format conventions required by the new release. This was fairly
extensive when ugprading from RRC 2.x to 3.0.1.x and typically very time
consuming. For 3.0.1.x to 4.0.x, there is a small amount of
transformation which takes place, primarily in the area of:

-   Folders which need additional information to handle the new
    permissions support
-   Types - some changes to the type system

This most notable difference between the upgrade process from 3.0.1.x to
4.0.x and the online migration for RRC 2.0.x to 3.0.1.x is that the
Rational Requirements Composer data is not re-indexed in the former case
if the 3.0.1.x indices can be used by the upgrade process.

## Possible problems in the RRC 3.0.1.x to 4.0.1/4.0.2 offline and online migration

This section will discuss known issues or problems which can arise
during the online and offline migration steps for RRC.

### Indices

Absolute vs. relative paths for indices: When doing an upgrade, the
indices from 3.0.1.x must be usable by the 4.0.1 upgrade process. As a
result, indices must be moved when specified at a relative location. If
an absolute path is used, than the index is maintained in the previous
3.x location, which is typically why the indices are either moved, or
the server is re-indexed.

Changing from relative to absolute paths during the upgrade:

Changing index paths from relative to absolute will be unsuccessful
unless the indices are copied from the location indicated by the
relative location to the absolute location specified in the new
configuration. Changing of the index location from relative to absolute
should be made in the 3.0.1.x, prior to running the offline upgrade
script process.

#### WebSphere

Using an absolute path is required with WebSphere Application Server
installations. If the full-text indices
(com.ibm.team.fulltext.index.location from the Jazz Team Server
teamserver.properties) are configured with a relative path, the path
will be located within the WebSphere Application Server profile (such as
C:\IBM\WebSphere\AppServer\profiles\appsrv01) instead of the JAZZ_HOME
location. The Jazz Team Server indices (com.ibm.jfs.index.root.directory
location from the Jazz Team Server teamserver.properties) use the
JAZZ_HOME property if its value is left as the default relative path.

#### Tomcat

Tomcat deployments exists within the JAZZ_HOME directory, but it is
still recommended to use an absolute path for the indices. NOTE: Always
back up the 3.0.1.x Jazz Team Server and full-text indices prior to any
upgrade. This could save valuable time if a rollback is required.

### READ_ONLY mode

When the RRC upgrade is started, the repository is automatically set to
READ ONLY mode and will remain in that state until the online portion of
the Rational Requirements Composer upgrade is complete. This will
prevent any 'lost writes' from occurring during the upgrade.

1\. If any application is performing an upgrade, the repository will be
in read-only mode

2\. If an upgrade exits abnormally or is unsuccessful, read-only mode is
effectively permanently. This will force the recovery of an earlier
back-up and re-try in order to affect the upgrade.

#### Forcing read-only mode to be unset This is not recommended unless the ramifications of forcing it to be unset are fully understood. Contact IBM support for more information.

### License requirements for online migration

Ensure the appropriate licenses are available for the Rational
Requirements Composer upgrade before you being the online migration. The
online migration will fail if license requirements are not met.

#### RRC analyst license requirement

If the RRC Analyst license (Rational Requirements Composer - Analyst or
Rational Quality Manager - Quality Professional-Floating) is not
available the user will encounter a failure in the online migration
portion of the upgrade. When the admin logs into the web UI migration
page, an error will occur indicating that the required license is not
present.

If the license was not assigned, it can be assigned in read-only mode.
The following operations are permitted while Jazz Team Server 4.x is in
read only mode:

-   Upgrading the existing version 3.0.x licenses to their 4.x
    counterparts
-   Installing new version 4.x licenses which were not utilized for
    3.0.x applications
-   Updating or altering user license assignments

See [Install 4.0 license to complete the IBM Rational Requirements
Composer on-line migration](https://jazz.net/library/article/958/) for
more information

#### Functional user The functional user rm_user requires the RM Application-Internal license for RRC online migration

Ensure that the 4.0 RM Application-Internal license is assigned to the
rm_user before you start the RM online migration. For more information,
see [Work item 68474: RRC online migration fails with licensing errors
for
rm_user](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=68474)
for more information. This license assignment is especially important if
you are upgrading from a version 3.0.1.x release, because this error
requires restoring from a backup and restarting.

### Import Mode set to true

**Version:** Upgrade to 4.0.x **Error During Upgrade:** HTTP 500
Internal Server error; JTS cannot reach RM/RDM **Cause:** During the
upgrade process, IBM Support may request you run a FixWrappers tool to
correct some inconsistencies. To run this tool, you need to set the
Import Mode in the Advanced Properties of the JTS to true. Leaving this
setting as is will cause the online migration to update the log files
indicating a success, but the web UI will force a Finalization to occur.
**Resolution:** Ensure that the Import Mode is set to false to avoid
this failure. Changing this setting will require a server restart to
come into effect.

### CRRRS1008E Error during online migration

**Version:** Upgrade to 4.0.x **Error During Upgrade:** CRRRS1008E
**Cause:** This error may be related to limited space on the database or
server **Resolution:** Check the database log files to ensure there are
on errors. Ensure there is enough space on the database server to
complete the migration.

##### Related topics: None [related-topics-none]

##### External links: \* None [external-links-none]

##### Additional contributors: Main.BrettBohnn, Main.StephanieBagot [additional-contributors-main.brettbohnn-main.stephaniebagot]
