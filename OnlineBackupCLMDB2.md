META:TOPICINFO{author="syeshin" date="1454600841" format="1.1"
version="1.5"} META:TOPICPARENT{name="BackupStrategies"}

# Transitioning to online backup of CLM databases using IBM DB2 DKGRAY Authors: Main.HariVetsa JohnOwen [transitioning-to-online-backup-of-clm-databases-using-ibm-db2-dkgray-authors-main.harivetsa-johnowen]

Build basis: v4.0.x and 5.0 Jazz applications in CLM ENDCOLOR

TOC{title="Page contents"}

# Summary

IBM DB2 is among the supported database servers that can be used to
store repository data for Jazz deployments. The Jazz product is designed
for Enterprise application deployment for teams to develop products
across geographies. It becomes quite apparent that the availability of
the Jazz server is as critical as the data that it manages. IBM DB2, as
other DBMSs, provides a facility to backup the critical data managed by
the Jazz server without compromising availability (uptime). In fact, by
implementing proper processes, normal maintenance can be accomplished
without interrupting the functioning of the Jazz server. The following
sections give an outline of the entire online backup and recovery
process for IBM DB2, which can also be used to restore the latest
production data available on staging/test servers.

# Assumptions

-   The DB2 backend server is running either DB2 V9.1 (Jazz V4.X), DB2
    V9.5 (Jazz V4.X) and DB2 V10.1 (Jazz V4.0.3 and later).
-   The directions are provided for DB2 running on a UNIX or Linux
    system. The commands on windows system will be identical with the
    exception of path names.
-   The Administrator is comfortable with UNIX shell environment.
-   Two destinations (directories) on File System are allocated, one for
    storing backups and one for storing Archive logs.
-   The user has basic knowledge of using DB2 command line on Windows
    and UNIX machines.

# Preparing the database for online backups

DB2 databases are created by default with Circular logging.

Logging is a concept in database systems where all modifications are
written to transaction logs as they happen when the actual data is
modified. In essence, all modifications to the database (insert, delete
and update) are stored twice; once in the data files and once, in the
transaction logs.

Circular logging is a method where the old transaction logs are
overwritten when there is a need to allocate a new transaction log file,
thus erasing the sequence of transactions happened to the database.

Archive logging is a method where the transaction logs are overwritten
when they are needed, after creating a backup copy of the transaction
log. This backup copy of the transaction log is called the ARCHIVE LOG
and is numbered sequentially to preserve the transaction sequence.

Setting Archive logging is a prerequisite of taking online backups for a
DB2 database. Setting Archive logging for the database requires a
directory that is writable for DB2 processes. We recommend creating a
directory that has the same ownership as the DB2 instance directory.

When defining a Archive log, you must also create a destination.Here is
how to create an Archive log destination:

\$ mkdir /backup/ArchiveDest \$ chown db2inst1:db2iadm1
/backup/ArchiveDest

Once the destination is ready, setup the database for Archive logging by
updating the database configuration using the following command:

\$ db2 update database configuration for using LOGARCHMETH1
'DISK:/backup/ArchiveDest'

NOTE: The DB2 configuration change described above does not become
effective until the next time DB2 is started. Prior to restarting DB2 an
offline backup of the database is required. Then once DB2 is started
again DB2 will begin to create archive logs and store them in the
archive destination directory:

/backup/ArchiveDest////

The disk size consumed by archive logs in the destination directory is
directly proportional to the database activity. They continually
accumulate to the Archive destination directory and we recommend
monitoring the directory and purging the Archive log files that are not
required for restoring database, or else pushing them to a tape backup.
We recommend making sure all the Archive logs are available on the disk
is as recent as the earliest online database backup kept on the disk.

# Taking the (final) offline backup

The change to the database configuration requires an offline backup to
be taken before before DB2 is started again. This can be achieved by
stopping Jazz and its associated databases. We recommend storing the
offline backup in the same target location configured for online
backups. This can be accomplished using the following command:

\$ db2 backup database JAZZDB to /backup/OnlineBackups

This will be the base backup to which archive logs can be applied to get
the database to a consistent state. At this point Jazz can be restarted,
along with its associated databases. Once DB2 has started it will
commence to archive the transactions and save the logs as specified in
the previous section. Though there will no longer be a need to take any
offline backups of the database after this configuration change, it is a
best practice to take offline backups before any major configuration
changes to environment like software patches, version upgrades etc. An
example would be to take an offline backup just before upgrading the RTC
Server from Version 4.0.6 to Version 5.0.1.

At this point online backups can now be taken.

# Taking online backups

Once all the prerequisites of setting the database configuration values
are completed, the DB2 database is ready for online backups. Online
backups can be taken using the following command:

\$ db2 backup database JAZZDB ONLINE to /backup/OnlineBackups COMPRESS
INCLUDE LOGS

Please note the two differences between the previous backup command and
this one. The keywords are explained below:

-   **ONLINE**: Instructs the database server to backup the database
    while transactions are in progress. There is no interruption to any
    activity while this operation is executing.
-   **COMPRESS**: This a very nifty feature of DB2 which compresses the
    backup image on the fly while backing up the database. For those who
    used to take backups and compress them to save disk space and tape,
    this comes in really handy. Be aware that using the COMPRESS option
    will extend the time it takes to complete the backup. Therefore if
    space isn't a problem and you want to keep the time taken for online
    backups to a minimum, for example to avoid extending the backup into
    a busier part of the day, then use of this option is not
    recommended.
-   **INCLUDE LOGS**: This two-word command gives DB2 an instruction to
    include any archive logs that are required to recover the database
    to a consistent image. This will be discussed further in the
    recovery section later in this article.

If you are planning to take nightly backups, it doesn't take long to
accumulate numerous backup images and use up your allocated disk space.
Even though most installations require only the most recent backup, we
recommend keeping the three recent database backup copies on the disk.

# Moving from offline to online backups

If your installation is already performing scheduled offline database
backups then it is possible to move from offline backups to online
backups without requiring additional outages. By way of example let's
assume that currently offline backups are taken at 01:00 AM each
morning. The procedure required is:

1.  Prior to the next scheduled offline backup perform the steps
    documented in section "Preparing the database for online backups."
2.  At 01:00 AM Jazz will be taken offline and an offline backup will be
    taken as normal. When Jazz is restarted DB2 will start to collect
    and save archive logs.
3.  Once Jazz is available and prior to the next scheduled offline
    backup, replace the scheduled offline backup with an online backup
    as described in section "Taking online backups", remembering that
    for online backups Jazz will not require stopping.
4.  The next morning at 01:00 AM the schedule will trigger an online
    database backup without stopping Jazz.
5.  No further changes are required. Online backups will continue to be
    collected at the scheduled time going forward.

# The recovery process

No backup is useful unless it can be used to recover the data that was
backed up. This section gives an overview of how to recover data from an
online backup.

## Scenario:

1.  Most recent online backup taken @ 2:00 AM
2.  Most recent Archive log spooled @ 10:15 AM
3.  You want to create a copy of the production database on test system
    as of 10:00 AM

## Recovery steps:

1\. Copy the most recent backup to the directory /testsystem/FromProd/
on the test system. To restore the database to test system issue the
command:

\$ db2 restore database JAZZDB from /testsystem/FromProd

2\. If you have more than one copy of the database stored in the
directory, you need to specify which backup copy to use for the restore
by using the keyword "TAKEN AT". (E. G.: TAKEN AT 20080603155403. Links
to DB2 documentation of related commands are provided in Section 7). At
this point the database is restored, but you still need to apply the
archive logs to make the database consistent. To query the rollforward
status of the database issue the command

\$ db2 rollforward database JAZZDB query status

3\. Next you need to extract the database archive logs that are bundled
into the backup image. To do so, create a temporary directory
/testsystem/FromProd/temparchivelogs and extract archive logs using the
command:

\$ db2 restore database JAZZDB LOGS from /testsystem/FromProd LOGTARGET
/testsystem/FromProd/temparchivelogs

Upon completion of this command all the logs required are extracted to
the directory provided by the key word LOGTARGET.

4\. The final step is to apply all the transactions stored in these log
files to the restored database using the following command:

\$ db2 "rollforward database JAZZDB to end of logs overflow log path
(/testsystem/FromProd/temparchivelogs)"

Upon successful completion of this command the database is consistent to
the earliest point (This includes all the changes written to the
database while the online backup is in progress). This point will
coincide the time of the last committed transaction before the online
backup is completed. It can be recovered using this backup. The status
should show "DB Working".

If you want to continue restoration by applying more logs, you can copy
all the archive logs that are more recent than the ones restored to
LOGTARGET and issue the above rollforward command again.

5\. Once you have restored the database to the desired state, the
rollforward process can be completed by issuing the command:

\$ db2 rollforward database test complete

You have successfully restored a DB2 database using an online backup.

# Miscellaneous Notes

Quiesce Database: Quiescing database is a feature provided by the DB2
server to put a particular database into isolation mode. While the
database is in this state, only Administrators can connect to the
database. You do not need to quiesce the database while taking online
backups, in fact, for Rational Team Concert to function normally; one
should never quiesce the database.

Size and number of LOGs files settings: Log file settings refer to the
setting used to specify the number and size of active transaction logs.
In DB2, all the transaction log files will have the same size. The
configuration of the LOGFILSIZ parameter is represented in 4KB pages, so
the value of 1024 for the transaction log size represents 4MB of size.
We recommend tuning the size to produce an archive log anytime between
10 to 30 minutes. Greater frequency impacts the database performance and
less frequency reduces the granularity of recovery, so it is important
to reach a configuration that provides the granularity you desire
without negative impact to the database performance.

The number of transaction logs can be configured using the LOGPRIMARY
database setting, will determine the size of the largest transaction. A
good starting point for the LOGPRIMARY configuration value is 10. The
value represented by LOGSECOND is used to allocate additional
transaction logs when all PRIMARY LOGS are in use. If you want to have
an infinite transaction size set LOGSECOND to a value of "-1".

# References

-   DB2 V9.1 documentation:
    <http://publib.boulder.ibm.com/infocenter/db2luw/v9/index.jsp>
-   DB2 V9.5 documentation:
    <https://publib.boulder.ibm.com/infocenter/db2luw/v9r5/index.jsp>
    -   [UPDATE DATABASE
        CONFIGURATION](https://publib.boulder.ibm.com/infocenter/db2luw/v9r5/index.jsp?topic=/com.ibm.db2.luw.admin.cmd.doc/doc/r0001987.html)
    -   [BACKUP
        DATABASE](https://publib.boulder.ibm.com/infocenter/db2luw/v9r5/index.jsp?topic=/com.ibm.db2.luw.admin.cmd.doc/doc/r0001933.html)
    -   [RESTORE
        DATABASE](https://publib.boulder.ibm.com/infocenter/db2luw/v9r5/index.jsp?topic=/com.ibm.db2.luw.admin.cmd.doc/doc/r0001976.html)
    -   [ROLLFORWARD
        DATABASE](https://publib.boulder.ibm.com/infocenter/db2luw/v9r5/index.jsp?topic=/com.ibm.db2.luw.admin.cmd.doc/doc/r0001978.html)
    -   [LOGPRIMARY](https://publib.boulder.ibm.com/infocenter/db2luw/v9r5/index.jsp?topic=/com.ibm.db2.luw.admin.config.doc/doc/r0000240.html)
    -   [LOGSECOND](https://publib.boulder.ibm.com/infocenter/db2luw/v9r5/index.jsp?topic=/com.ibm.db2.luw.admin.config.doc/doc/r0000241.html)
    -   [LOGFILESIZ](https://publib.boulder.ibm.com/infocenter/db2luw/v9r5/index.jsp?topic=/com.ibm.db2.luw.admin.config.doc/doc/r0000239.html)
    -   DB2 9.5 [data recovery
        concepts](https://publib.boulder.ibm.com/infocenter/db2luw/v9r5/index.jsp?topic=/com.ibm.db2.luw.admin.ha.doc/doc/c0052073.html)

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]
