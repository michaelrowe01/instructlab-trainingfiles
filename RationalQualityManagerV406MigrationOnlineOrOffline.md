META:TOPICINFO{author="wbchen" date="1455549212" format="1.1"
reprev="1.16" version="1.16"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Guidelines for running Rational Quality Manager online migration in a production environment [guidelines-for-running-rational-quality-manager-online-migration-in-a-production-environment]

DKGRAY Authors: Main.WilliamChen Build basis: IBM Rational Quality
Manager 4.0.6 and later ENDCOLOR

TOC{title="Page contents"}

IBM Rational Quality Manager (RQM) V4.0.6 introduced a new online
migration feature that you can use to migrate large amounts of quality
management (QM) data to 4.0.6 and later versions while the old
production server is still online. The online migration is built for
large amounts of repository data that have extremely high volume manual
test script states and manual execution scripts. In most cases, you do
not need to use online migration for production upgrades; the
traditional offline migration method is still the most common migration
path.

If you use the online migration method to migrate data for large
enterprise QM server upgrades, before you begin, read these guidelines.

## Determining whether to run an online migration

IBM Rational developers tested online migration against large databases
internally. You can use their test results to determine whether online
migration is right for you. For more information, see the Rational
Quality Manager online migration test matrix.

## Backing up the QM database for the production environment

Before you run the online migration commands, back up your production QM
database. If issues occur during the online migration, it is difficult
to roll back to a clean state. If a rollback is required in a production
environment, you might lose some of the data that changed since the last
full backup.

If you encounter problems during an online migration, immediately
contact IBM Rational Support. **Important:** Do not try to run any more
commands until IBM Support instructs you to.

## Repository tools commands

The Repository Tools application now supports these new commands and
parameters:

-   `-onlineMigrateEstimate`: Finds the number of states in the database
    that need to be migrated.
-   `[teamserver.properties=conf/qm/teamserver.properties]`: The path to
    the teamserver.properties file of the server that is currently
    running.
-   `[logFile=repotools-qm_onlineMigrate.log]`: The path to the log
    file.
-   `-onlineMigrate`: Runs the online migration on a live server.
-   `[numStatesPerRun=100]`: The number of item states to process for
    each iteration.
-   `[priority=<1-100> (default=50)]`: The percentage of time that
    online migration should run.
-   `[noPrompt]`: Will not prompt before the migration starts.
-   `-onlineMigrateRevert`: Reverts the database changes that were made
    from an online migration.
-   `-onlineMigrateStop`: Prompts the online migration process to finish
    the current transaction and exit. If you need to stop online
    migration to make sure that database locks are not held
    unnecessarily, use this command.
-   `-validateMigration`: Validates the QM online migration result.
-   `[validateLevel=<1-3> (default=1)]`: The detailed level to validate.
    The default is 1. If the value is 2, the number of states for each
    manual script are compared. If the value is 3, the number of steps
    for the current state of the manual script are compared.

For detailed information about repository tools commands, run
`repotools-qm.bat` or `repotools-qm.sh`.

## Issues and workarounds

-   If the tables and statistics are out of date, the online migration
    might result in poor performance. Make sure that statistics are up
    to date by checking them against these online migration tables:
    -   REPOSITORY.ITEM_STATES
    -   REPOSITORY.ITEM_CURRENTS
    -   REPOSITORY.ITEM_TYPES
    -   LINKS.AUDITABLE_LINK

<!-- -->

-   You might encounter this error:
    `ORA-01555: snapshot too old: rollback segment number xx with name "systemValue" too small.`
    The exception occurs on the following query, which calculates the
    percentage of complete values that involves a table scan against the
    ITEM_STATES table. Typically, that percentage is large. select
    count(\*), {ITEM_TYPE_DBID}

from {REPOSITORY.ITEM_STATES} where {ITEM_TYPE_DBID} in (s) and
{KEY_UUID} not like '-' group by {ITEM_TYPE_DBID} To resolve this issue,
a database administrator must increase the size of the rollback segment
(undo) size or extend the tablespace on the small segment. Then, you can
restart the online migration. The migration will start at the point
where you left off.

-   If the Rational Quality Manager online migration fails with the
    `ORA-00955` error, see this technote: Technote 1680939: Rational
    Quality Manager online migration fails with ORA-00955.

<!-- -->

-   You might encounter this error:
    `Failed to add tables to the database. The database has not been modified.`
    This error can occur when you run an online migration without the
    noPrompt parameter: 2014-07-27 07:19:47,815 CRJAZ2523I Setting the
    global server rename state to false and the validation state to
    false.

2014-07-27 09:30:43,708 Failed to add tables to the database. The
database has not been modified. To resolve this issue, add the
`noPrompt` parameter to the online migration command. Then, the
`addTables` command can begin to run as part of the online migration
process.

## Log files for troubleshooting

If you encounter issues with the online migration, try to provide the
following information to the IBM support and development teams:

Full online migration command syntax
:   You can get this information from the console window when you run
    any online migration command.

`onlineMigrateEstimate.log`
:   By default, this log file resides in the online migration server
    logs directory. The `onlineMigrateEstimate.log` file contains the
    number of states in the QM database that must be migrated.

`repotools-qm_onlineMigrate.log`
:   This file contains online migration events and related activities.
    By default, this file is in the online migration server logs
    directory.

`onlineMigrateStateProcessed.log`
:   This log file is specific to the online migration process and can
    provide details about the process time and activities. The file also
    contains timestamps of each state migration. By default, this file
    is in the online migration server logs directory.

## Enabling logging for online migration

You can enable online migration logging to determine what tables might
need to be optimized. For example, the CONTENT_STORAGE table is heavily
used during the online migration. To verify that other online migration
tables statistics are up to date, turn on both
`log4j.logger.sqlTxLogger` and `log4j.appender.file.Threshold` to debug
mode:

1 Stop the online migration by entering this command:
`repotools-qm -onlineMigrateStop` 2 Edit
`install_dir\conf\repotools_log4j.properties`. 3 Add these lines:

\# Turn on debugging of all SQL *log4j.logger.sqlTxLogger=DEBUG* 4
Update this property: `_log4j.appender.file.Threshold=DEBUG_` 5 Save and
restart the online migration. 6 After the `repotools_onlineMigrate log`
updates with a time estimate again, which can take some time, let the
online migration command run for 30 minutes to capture enough SQL
tracing for a full anlaysis. 7 Stop the migration, as you did earlier in
this procedure. 8 Collect the online migration log or logs
(`repotools-qm_onlineMigrate`) and states processed log or logs
(`onlineMigrateStatesProcessed`) and send them to IBM Support. 9 Undo
the edits that you made in steps 3 and 4. 10 Restart the online
migration.

## Q & A

### 1. How accurate is the estimated completion time from the `onlineMigrateEstimate` command? [how-accurate-is-the-estimated-completion-time-from-the-onlinemigrateestimate-command]

When you run the `onlineMigrateEstimate` command, the estimated
completion time is the best estimate that is based on the available
data. Fluctuations are unavoidable because of several unknown variables;
for example, the database server load or the complexity of test cases
over time. During performance testing, old statistics on the ITEM_STATES
and ITEM_CURRENTS tables resulted in long run times. If you have not
already done so, ensure that the statistics are up to date on those
tables.

The `/server/OnlineMigrateSettings.cfg` file contains the priority of
the process. You can change this file while the online migration is
running. To improve efficiency, you can adjust it to a larger value such
as '90' during off peak hours.

If you need to migrate large databases that contain a lot of data, the
migration runs in the background while the server is online so that the
amount of time that the server is offline is minimized and performance
is not noticeably affected.

### 2. How much can I gain by increasing the priority value when running the `onlineMigrate` command? [how-much-can-i-gain-by-increasing-the-priority-value-when-running-the-onlinemigrate-command]

The priority is equal to the percentage of time that the online
migration runs. You can specify a percentage value between 1 and 100.
The primary consideration is how much load the database can handle and
how responsive the old server is.

For example, if the priority value is 10, the task for online migration
runs 10 of the time and is idle the remaining 90. If the priority value
is 100, the migration process never pauses. You might notice improvement
in the estimated completion time. At priority=50, the online migration
runs half the time and waits half the time.

Increasing the priority to 90 might make the application somewhat
slower, but it is unlikely to be noticeable. Offline migration is
identical to online migration running at priority=100. The process is
the same except there is no pause between transactions.

You can change `/server/OnlineMigrateSettings.cfg` to adjust the
priority while the online migration is running. This adjustment is
dynamic; it does not require you to stop and restart the migration. You
can maximize the available system resources during offpeak hours by
increasing the priority as close to 100 as possible. This means that
online migration runs all the time, and users who need to access QM
projects might be affected. Therefore, take a conservative approach to
reducing priority during peak times while the online migration is
running until the true impact is acceptable for users to continue with
their work on the same QM server.

### 3. What new tables are used by the online migration process? [what-new-tables-are-used-by-the-online-migration-process]

The following tables are used during online migration. A query or insert
is done on the tables.

-   **Existing tables:**
    -   REPOSITORY_CONTENT_STORAGE
    -   REPOSITORY_ITEM_STATES
    -   REPOSITORY_ITEM_CURRENTS
    -   REPOSITORY_ITEM_TYPES
    -   LINKS_AUDITABLE_LINK
-   **New tables created for migrated data:**
    -   PLANNING_EXECUTION_ELEMENT2
    -   PLNNNGMNLXCTNSCRPTSTPLKPLMNT2H
    -   PLANNNG_MNL_XCTN_SCRPT_STP_LKP

When the online migration starts, query the REPOSITORY_ITEM_STATES to
get the total counts of how many states you need to migrate. Then,
migrate them by time order. Process the oldest one first. Then, cache
50,000 records at a time, process each one ManualScriptSate, read all of
its steps, create ones and put the data into the above related tables.

Commit to database no more than (numStatesPerRun=100) states are
processed. It is important for the database administrator to keep these
table statistics up to date to optimize online migration process.

### 4. How can I enable logging for online migration? [how-can-i-enable-logging-for-online-migration]

See the information about `onlineMigrateStateProcessed.log` in the "Log
files for troubleshooting" section of this article.

##### Related topics: [Deployment web home](DeploymentWebHome), [related-topics-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com) Rational Quality Manager 4.0.6 New &
    Noteworthy page

##### Additional contributors: : Main.JingQian, Main.JamesBognar, Main.PaulEllis, Main.RosaNaranjo, Main.DeniseMcKinnon, Main.LauraHinson [additional-contributors-main.jingqian-main.jamesbognar-main.paulellis-main.rosanaranjo-main.denisemckinnon-main.laurahinson]
