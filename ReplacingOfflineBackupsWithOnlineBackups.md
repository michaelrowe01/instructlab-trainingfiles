META:TOPICINFO{author="rschoon" date="1389713811" format="1.1"
reprev="1.4" version="1.4"} META:TOPICPARENT{name="BackupCLM"}

# Replacing offline backups with online backups [replacing-offline-backups-with-online-backups]

DKGRAY Authors: Main.HariVetsa Build basis: CLM ENDCOLOR

TOC{title="Page contents"}

This article is intended to replace existing offline backup process with
online backup of database during maintenance activities.

Currently, Rational Engineering Services (RES) takes backups of all the
databases, work item indices and full text indices before every
scheduled upgrade of the CLM Server. The above backups are being taken
after the application was shut down but before the upgrade process
starts.

Unfortunately, this process is causing longer application unavailability
than necessary. Both RES and CLM Development are in constant search for
opportunities to reduce the downtime required to upgrade CLM software.
This initiative promoted us to reevaluate our process.

The primary objective for the offline backups before an upgrade process
is to guarantee the application state of recovery in case we have to
backout the change. This is traditional recommendation from every
software and hardware vendor. Our hunt was to ensure the objectives are
not compromised, but break out the traditional thought process that
doesn't work for us any longer.

What happens if we use online backups instead of offline backups for
backout plan? We already use the online backups and rollforward recovery
for Business Continuity Process (BCP). Why cant we use the same online
backups for application recovery before any software upgrade?

The only difference we have observed is, the BCP Process minimizes the
data loss (we want to recovery to the latest point possible) whereas the
backout process needs to recover the application to an exact point
before the software upgrade. The recovery information is already there
in the Archive logs.

After little bit more analysis, the following process can be used to
replace offline backups with online backups:

1.  2-3 hours before the application upgrade, take an online backup of
    all the databases
2.  Make sure all the online backups are completed successfully
3.  Stop the CLM applications for upgrade
4.  Note the timestamp after all the applications are stopped and
    disconnected from the databases. (This timestamp will be used for
    recovery.)
5.  Take a backup of work item indices and full text indices
6.  Make sure you have all the archive log files of the databases to
    rollforward
7.  Perform application upgrade

The following diagram depicts the change in backup processes using
offline backups and online backups.

In case you need to execute a backout plan, there is only one difference
between the backout plan between offline and online backups. Instead of
just restoring your backup, you will restore the backup and rollforward
the transactions. Since the online backups are taken just few hours
before the upgrade, the recovery of these transactions will be quick.

We upgrade the CLM server behind jazz.net, which is being used by RTC
development team, once every milestone (or sprint). On average this
server gets upgraded 15-20 times in a calendar year. We had to execute a
backout procedure one in the last 2 years. Given the low probability of
needing to resort to a backout plan, it makes sense to move to an online
backup process before starting application upgrades.

Please ensure the process works for you in our staging or test
environments before adopting into production.

Here are some commands that can be used as reference:

1.  How to determine last successful backup for IBM DB2? \|SELECT
    MAX(start_time) FROM SYSIBMADM.DB_HISTORY WHERE operation = 'B' AND
    operationtype = 'N' AND sqlcode IS NULL\|
2.  How can I obtain details of archive logs produced since last backup
    for IBM DB2? \|SELECT start_time, end_time, location, entry_status,
    sqlcode, sqlstate FROM SYSIBMADM.DB_HISTORY WHERE operation = 'X'
    AND operationtype = '1' AND start_time \> (SELECT MAX(start_time)
    FROM SYSIBMADM.DB_HISTORY WHERE operation = 'B' AND operationtype =
    'N' AND sqlcode IS NULL)\|

##### Related topics: [related-topics]

-   [Backing up the Rational solution for Collaborative Lifecycle
    Management (CLM)](BackupCLM)
-   [Tip: Configuring IBM DB2 V9.5 for online backups for Rational Team
    Concert](https://jazz.net/library/article/98)

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="offlineonlinebackupprocess.png"
attachment="offlineonlinebackupprocess.png" attr="h" comment=""
date="1387309621" path="offlineonlinebackupprocess.png" size="95440"
user="gcovell" version="1"}
