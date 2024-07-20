META:TOPICINFO{author="aalaird" date="1502376949" format="1.1"
reprev="1.5" version="1.5"} META:TOPICPARENT{name="BackupCLM"}

# Backup and restoration of Jazz Foundation Service index files for Rational DOORS Next Generation [backup-and-restoration-of-jazz-foundation-service-index-files-for-rational-doors-next-generation]

DKGRAY Authors: Main.PaulBoney Build basis: Rational DOORS Next
Generation 4.0+ ENDCOLOR

TOC{title="Page contents"}

This document outlines the preferred steps for creating and restoring
backup files of the Jazz Foundation Service (JFS) that are used by
Rational DOORS Next Generation. These steps must be performed by the
server administrator.

Using a Rational DOORS Next Generation repository tools (repotools)
command, you can create an archive of the indexes and save it to a
location of your choice. This backup process is performed online while
the server is running. If the JFS indexes ever get corrupted, you can
use offline repotools commands to restore and synchronize the indexes
from the backup file.

Note that this process is for creating and restoring backups of the JFS
indexes only; it will not create a backup of the Rational DOORS Next
Generation database. For detailed information on performing a full
backup, see [BackupCLM](BackupCLM)

## Quick reference

The following steps provide an overview of the repository tools commands
that are required to back up and restore the Rational DOORS Next
Generation JFS indexes for version 4.0 and later. For detailed
information about these commands, refer to the relevant sections of this
document.

#### Online backup

*repotools-rm -backupJFSIndexes adminUserID= adminPassword= toFile=*

#### Offline restore

*repotools-rm -restoreJFSIndexes fromFile=*

#### Synchronization

*repotools-rm -synchronizeJFSIndexes teamserver.properties=*

## Creating a backup of JFS indexes in Rational DOORS Next Generation 4.0+

As of version 4.0, server administrators can use a repotools command to
create a backup of the JFS index files while the server is online.

### The repotools location

Repository tools command-line reference (repotools) is included with
Rational DOORS Next Generation and is available at the installed server
location. In a typical installation, the repotools scripts are found at
*/server/repotools-rm*.

For more information on how to run repotools commands, and to view a
list of available commands, see the [Repository tools command-line
reference](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.5/com.ibm.jazz.install.doc/topics/c_repotools_overview.html)
topic in the online help.

### Backup command

To start the online backup of the JFS indexes, run the following
repotools command: *repotools-rm -backupJFSIndexes adminUserID=
adminPassword= toFile=*

Example: *repotools-rm -backupJFSIndexes adminUserID=admin
adminPassword=adminPass toFile=C:\backup\myBackup.zip*

Note that while the backup is in progress, the server might appear
sluggish or unresponsive to users. Also note that write processes to the
indexes are queued and are run when the backup is complete. After the
process is finished, the generated backup file is available in the
location that you specified in the toFile command parameter.

For more information, see the [Repository tools command to back up Jazz
Foundation Service
indexes](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.5/com.ibm.jazz.install.doc/topics/r_repotools_backupjfsindexes.html)
topic in the online help.

## Restoring JFS indexes from a backup file in Rational DOORS Next Generation 4.0+

There are two steps to restoring the JFS indexes from a backup file by
using the repository tools commands:

1.   Restore the indexes by running the restoreJFSIndexes command. 2.
    Synchronize the indexes by running the synchronizeJFSIndexes
    command.

Note that backup files that are more than 90 days old cannot usually be
restored.

### Restore command

The restoreJFSIndexes command is used to restore the JFS indexes from a
backup file that was created by using the backupJFSIndexes command. The
restore command must be run within 90 days from when the backup file was
captured. In the event a database restore is also being performed, the
index backup being restored must not be ahead of the database.

To restore the index, stop the server and run the following repotools
command: *repotools-rm -restoreJFSIndexes fromFile=*

Example: *repotools-rm -restoreJFSIndexes
fromFile=C:\backup\myBackup.zip*

For more information, see the [Repository tools command to restore Jazz
Foundation Service indexes from a backup
file](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.4/com.ibm.jazz.install.doc/topics/r_repotools_restorejfsindexes.html)
topic in the online help.

### Synchronize command

The synchronizeJFSIndexes command is used to synchronize the JFS indexes
and the full text indexes with the resources in the database. It updates
older indexes to the same level as the current one.

To synchronize the indexes, run the following repotools command:
*repotools-rm -synchronizeJFSIndexes teamserver.properties=*

Example: *repotools-rm -synchronizeJFSIndexes
teamserver.properties=C:\myJTSInstall\server\conf\rm\teamserver.properties*

For more information, see the [Repository tools command to synchronize
JFS indexes with
database](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.4/com.ibm.jazz.install.doc/topics/r_repotools_synchronizejfsindexes.html)
topic in the online help.

##### Related topics: [BackupCLM](BackupCLM) [related-topics-backupclm]
