META:TOPICINFO{author="rrakich" date="1710777850" format="1.1"
reprev="1.61" version="1.61"}

# ELM - Moving from one database vendor to another using the optimized concurrent repotools migration commands \[BETA\] [elm---moving-from-one-database-vendor-to-another-using-the-optimized-concurrent-repotools-migration-commands-beta]

DKGRAY Authors: Main.ChrisAustin, Main.DanielMoul Build basis:
Engineering Lifecycle Management 6.0.6, 6.0.6.1, 7.0.1, 7.0.2, 7.0.3
ENDCOLOR

TOC{title="Page contents"}

## Abstract

**General Availability customers should refer to the formal technote
[Database Migration: IBM Engineering Lifecycle Management
products](https://www.ibm.com/support/pages/node/6552594).**

17th August 2022 Update: Patches that contain the new migration tools:
(this list will be updated as patches are released)

-   7.0.2 iFix025 - ELM 7.0.2 SR1 ifix025 with patch, can be used for
    migration of production data. (reach out to IBM ELM support for the
    patch)
-   6.0.6.1 iFix025 - [Download the patch from Fix
    Central.](https://www.ibm.com/support/fixcentral/swg/selectFixes?parent=ibm7ERational&product=ibm/Rational/Rational+Collaborative+Lifecycle+Management+Solution&release=6.0.6.1&platform=All&function=all)
-   6.0.6 iFix026 - [Download the patch from Fix
    Central.](https://www.ibm.com/support/fixcentral/swg/selectFixes?parent=ibm7ERational&product=ibm/Rational/Rational+Collaborative+Lifecycle+Management+Solution&release=6.0.6&platform=All&function=all)

New repotools -concurrentExport and repotools -concurrentImport commands
provide faster migration of Engineering Lifecycle Management (ELM)
application repositories from MS SQL Server to Db2 or Oracle. This page
can be used as a guide to plan out and execute a migration using the
optimized repotools commands.

## ELM applications in scope

The repositories of the following applications can be exported and
imported using these new commands:

-   `JTS` (Jazz Team Server)
-   `RM` (primary application of DOORS Next)
-   `QM` (primary application of Engineering Test Management)
-   `CCM` (primary application of Engineering Workflow Management)
-   `GC` (Global Configuration Management)
-   `RELM` (Engineering Insights)

Other ELM repositories:

-   RS (Report Builder) no need to migrate; has its own file-based data
    store
-   LQE (Lifecycle Query Engine) no need to migrate; has its own
    file-based data store
-   LDX (Link Index Provider) no need to migrate; has its own file-based
    data store
-   Data warehouse migration not supported; keep using existing
    database, or create a new data warehouse after migrating to new
    database vendor (losing any historical metrics). There are options
    how to mitigate the situation that you are loosing the trends. You
    can find more information on [How can you keep your trend data after
    migrating data warehouse database to different
    vendor](https://jazz.net/forum/questions/277294/how-can-you-keep-your-trend-data-after-migrating-data-warehouse-database-to-different-vendor?page=1&focusedAnswerId=277297#277297)
    (which offers the same suggestions as for PUB Doc Builder directly
    below). For DCC configuration database, it is faster to drop and
    create from scratch in a new environment than migrating it.
-   PUB Document Builder - Use database migration
    documentation/utilities/practices such as the following:
    -   Db2 migration from non-Db2 relational database documentation,
        see
        <https://www.ibm.com/docs/en/db2/11.5?topic=ueds-migrating-from-non-db2-relational-database-management-systems>
    -   Oracle SQL Developer database migration utility, see
        <https://www.oracle.com/database/technologies/migrating-sql-to-oracle.html>

## Prerequisite Considerations

-   A non-production test environment with a copy of data from
    production is needed to run a test migration.
    -   The copy of production data should be recent enough that you are
        confident it represents all data in the product repository--for
        example, within the last few months for teams following
        established development processes.
    -   You need test data for each application and application instance
        you will migrate. For example, if you have two RM servers, you
        need to do a test migration of each. This statement does not
        apply to clustered CCM or QM servers, since clustered servers
        share one database instance.
    -   A staging environment with hardware equivalent to production is
        the most reliable indicator of expected migration time.
-   A user with administrative privileges must perform the migration.
-   The ELM server(s) needs to be offline, so an outage window will be
    required.
-   Migration requires an export and import of data together. There is
    no support for a partial migration, or for the servers to come
    online between an export and import.
-   The ELM server(s) must have sufficient disk space to hold export
    file(s). The database data is compressed during export, but it is
    not the same compression ratio on all databases. A good rule of
    thumb is to use the size of the database when determining how much
    disk space should be available for export files.
-   Well-performing hardware is required for high speed migration.

### Review existing migrations

There are some documented examples of repositories and environments that
have used the optimized migration. When preparing an environment for
optimized migration, looking at these use cases can help you to compare
other hardware specifications to your current environment.

-   [OptimizedMigrationTestScenarioMatrix.3-12-21.xlsx](ATTACHURL/OptimizedMigrationTestScenarioMatrix.3-12-21.xlsx):
    Environment and migration testing times for various ELM application
    repositories

## Supported Migrations

-   ELM 7.0.2 SR1 ifix025 with patch, can be used for migration of
    production data.
-   ELM 7.0.3 includes additional optimizations, bug fixes and logging
    and (after general availability) can be used for migration of
    production data.
-   In both, the optimized concurrent migration supports migrating from
    Microsoft SQL Server to IBM Db2 or Oracle databases.
-   Export and import ELM application versions must be the same. It is
    **not** possible to export one version of an ELM application and
    import it into a newer or older version.
-   Source and target databases must be at a version supported by your
    version of ELM within the [System
    Requirements](DeploymentInstallingUpgradingAndMigrating).
-   To request early access to these new repotools commands on earlier
    releases so that you can test with your data, contact IBM Support.

## Preparing Servers

While the optimized repotools migration code has been reworked to reduce
the outage time for a migration, the operating environment also plays a
crucial role in how fast a migration can complete. The new repotools
-concurrentExport and repotools -concurrentimport commands make use of
multiple CPU cores and fast disk and network I/O.

### Disk

-   If possible, use a local disk for writing and reading export files.
    Exporting to or importing from a network share or network storage
    device may limit the processing speed of the migration.
-   Solid State Disks (SSD) are recommended for migration storage. Disk
    speeds are an important part of migration, both on the ELM server
    running the repotools commands, and the database server. Refer your
    ELM server admin and DBA to our article on [Disk
    Benchmarking](Deployment.DiskBenchmarking).

### CPU Cores

The optimized migration relies heavily on concurrency to reduce its
runtime speed. Running ELM and database servers with at least 8 to 16
cores is recommended.

### System Memory

Running the concurrent db migration repotools commands
(-exportConcurrent, -importConcurrent, and -compare) can use a lot of
system memory. It is important to minimize other processes competing for
system resources when running these commands. On Linux, the Out Of
Memory Killer has terminated concurrent migration processes early.
Administrators are then forced to correct the issue by reducing memory
usage, and re-running the terminated command.

### Databases

You may not need to modify database specific settings for all cases of
migration. In general, databases that are tuned for ELM daily use will
be appropriate to use in the export context. Import databases should be
created with ELM application specific recommendations in mind, found in
the product documentation.

In practice, we have seen that import databases optimize their execution
plans based on the large occurrence of writes after -importConcurrent
has been run. This can have a negative impact on query performance
during compare or when running the ELM server using the new database
vendor initially. To clear the execution plan on Oracle, run alter
system flush shared_pool;. To clear the execution plans on Db2, either
leave the DB2 AUTO_MAINT job enabled, or do the following to execute
runstats in a script: 1 Connect to the database using the db2 connect
command. 1 Create a script (like this example): db2 -x "SELECT 'RUNSTATS
ON TABLE ' \|\| TRIM(TABSCHEMA) \|\| '.' \|\| TRIM(TABNAME) \|\| ' AND
INDEXES ALL;' FROM SYSCAT.TABLES WHERE TYPE = 'T' AND TABSCHEMA NOT LIKE
'SYS' ORDER BY TABSCHEMA, TABNAME" \> db2_runstats.sql.out

1 Validate the db2_runstats.sql.out contains all the table names to
execute runstats on. 1 Run the script using db2 -tvf:
C:\IBM\SQLLIB\BIN\>db2 -tvf db2_runstats.sql.out \> outcomestats.txt

#### Db2

Customers have seen some performance gains importing to DB2 by doing the
following:

-   Set the memory to be automatic which allows memory growth: db2
    "update db cfg for \[DatabaseName\] using DATABASE_MEMORY 5000000
    automatic"
-   Increase the bufferpool: db2 "ALTER BUFFERPOOL IBMDEFAULTBP SIZE
    \[Appropriate size based on avaiable physical memory\]"
-   Enabling the statement concentrator: db2 "update db cfg using
    stmt_conc off immediate"
-   Increase the heap size: db2 "update db cfg using APPLHEAPSZ 10000
    automatic"
-   Increase the DB2 Log File size files: db2 "update db cfg for
    \[DatabaseName\] using LOGFILSIZ 12288"
-   Increase the DB2 Log primary transactions log files: db2 "update db
    cfg for \[DatabaseName\] using LOGPRIMARY 128"
-   Increase the DB2 Log Secondary transactions log files: db2 "update
    db cfg for \[DatabaseName\] using LOGSECOND 128"

These are not meant to be definitive settings, but can be discussed with
database administrators and implemented when appropriate.

## Migration Task List

1 **Before beginning your test migration, delete unnecessary attachments
to reduce space.** Orphaned work item attachments can take up space in
your database, and increase migration times and complexity. To reduce
that risk, you can use the
[WorkitemAttachmentMigrationUtility](Deployment.WorkitemAttachmentMigrationUtility).
You can also [configure EWM to store large attachments outside of the
default
database](https://jazz.net/pub/new-noteworthy/ewm/7.0.2/7.0.2/index.html#10).
1 **Before beginning your test migration, perform a -verify to check
database integrity.** A verify is one way to determine the health of the
database BEFORE you begin a migration, and also as a method of
determining AFTER whether the migration introduced any problems. To run
a verify: /server/repotools\_\[app\] -verify level=5 If any issues are
reported then use [Troubleshooting the Verify
command](https://jazz.net/wiki/bin/view/Deployment/DeploymentTroubleshootingVerifyCommand)
or contact IBM Support 1 **Back up the application(s) to be migrated.**
When you migrate from one database vendor to another database vendor
(for example, Microsoft SQL Server to IBM Db2), it is critical to back
up each application database before you perform the migration. It is
recommended to store your data for a six-month period after a database
migration, providing enough time to ensure that the product is
functioning as expected and that no remedial actions are necessary
later. For more information, consult the IBM Documentation (aka
Knowledge Center) topic "Backing up and restoring IBM Engineering
Lifecycle Management (ELM) applications." 1 **Increase repotools script
heap XMX to at least 4096M.** The migration commands require more then
the default 1500M heap space. In internal testing, 4096M has proved to
be sufficient, but there could be cases where an even larger value will
prevent potential memory contention issues. In repositories with many
large multi-gigabyte sized attachments, consider using an Xmx of 8192M.
To increase the heap, define the following system environment variable
(note that M should not be appended to the system environment variable):
REPOTOOLS_MX_SIZE=4096 1 **Install any necessary patches, and use
-clean.** The Tech Preview optimized migration requires a patch to
enable the migration commands, `JTS_DB_Migration_Patch__.zip`. For
7.0.3, this is the only required patch. If you are using 6.0.6.1 or
7.0.1 an additional backport patch is also required. Any patch files
should be installed to the `[install]/server/patch` directory with care
to follow any associated patch readme files. It is important to run
repotools commands with the `-clean` parameter whenever using patches. 1
**Export the data with -exportConcurrent.** To perform an export:
/server/repotools\_\[app\] -exportConcurrent -clean
toFile=../export/\[app\].zip Important statistical information about the
migration execution can be gathered and saved to the repotools log. The
new statistics collection behavior is effective from 06-2021. This
information can be used by support if troubleshooting a migration is
required. Note that statsLogFrequency is only required to change the
default logging period once every 60 minutes./server/repotools\_\[app\]
-exportConcurrent -clean toFile=../export/\[app\].zip
statsLogFrequency=60 If want to ignore the statistics while exporting
the data, need to pass the parameters like
below/server/repotools\_\[app\] -exportConcurrent
statsEnabled`false -clean toFile`../export/\[app\].zip
/server/repotools\_\[app\] -exportConcurrent
statsEnabled`no -clean toFile`../export/\[app\].zip 1 **Check the log
file for error messages and runtime statistics.**
/server/repotools\_\[app\]\_exportConcurrent.log 1 **Update the ELM
server with new database settings.** You can either set up a new ELM
server install using the same version as your export ELM Server, or use
the existing export server. If you re-use the existing server, backup
the old teamserver.properties file(s) so they can be used in the
-compare tool later on (Example: teamserver-sql.properties). If you set
up a new ELM instance, ensure you keep the same URI, by changing IHS, or
installing side-by-side on the existing server. Update the following
properties in the server/conf/\[app\]/teamserver.properties file to
point to the new location. com.ibm.team.repository.db.vendor
com.ibm.team.repository.db.jdbc.location
com.ibm.team.repository.db.jdbc.password

1 **Import the data with -importConcurrent.** To perform an import:
/server/repotools\_\[app\] -importConcurrent -clean
fromFile`../export/[app].zipImportant statistical information about the migration execution can be collected and saved to the repotools log. The new statistics collection behavior is effective from 06-2021.  This information can be used by support if troubleshooting a migration is required. Note that statsLogFrequency is only required to change the default logging period once every 60 minutes.  /server/repotools_[app] -importConcurrent -clean fromFile`../export/\[app\].zip
statsLogFrequency=60 If you want to ignore the statistics when importing
the data, need to pass the parameters like below:
/server/repotools\_\[app\] -importConcurrent
statsEnabled`false -clean fromFile`../export/\[app\].zip
/server/repotools\_\[app\] -importConcurrent
statsEnabled`no -clean fromFile`../export/\[app\].zip 1 **Check the log
file for error messages and runtime statistics.**
/server/repotools\_\[app\]\_importConcurrent.log 1 **Rebuild Indices.**
In earlier releases of the importConcurrent tool, rebuildIndices is not
run automatically. You can verify if rebuild indices happens
automatically by running: /server/repotools-\[app\] -help
command=importConcurrent If the **\[skipRebuildIndices\]** argument is
present in the help output, rebuildIndices has been performed
automatically. Otherwise, run the -rebuildIndices command to restore the
database indices in the import environment: /server/repotools-\[app\]
-rebuildIndices 1 **Consult the appropriate database vendor guidance
above for clearing execution plans, and clear the plans.** 1
**Important: It is necessary to run compare successfully in a test
environment before planning your production migration. This is to ensure
there are no discrepancies between the source and target databases.**

-   It is not recommended to run compare after your production
    migration, because it could require an outage of the production
    system longer than is feasible. Using the test system, to validate
    the exported data is all present in the import database, a repotools
    compare can be used to perform an exhaustive cell by cell comparison
    of two ELM databases. This requires two teamserver.properties files,
    one that contains connection information to the old database, and
    one that contains connection information to the new database. It
    also requires that both databases are accessible from one ELM server
    location.
-   Do not start any of the ELM applications accessing the source or
    target databases until the compare completes. If you start any of
    the servers, changes in the tables may occur, creating false
    positive errors in the compare log.
-   While the compare *can* run with either database set as source or
    target, **performance is much better when the SQL Server database is
    used in the source.teamserver.properties argument**, and Oracle or
    Db2 is used in the target.teamserver.properties argument.
-   To run a compare: ExportJazzServerInstall/server/repotools\_\[app\]
    -compare
    target.teamserver.properties=/opt/IBM/ImportJazzServerInstall/server/conf/jts/teamserver.properties
    1 **Re-run the verify to check database integrity.** After the
    migration and compare, run the -verify again to ensure no new issues
    were introduced by the migration. Any migration patches should be
    removed, and original patches (if any) restored prior to running the
    verify. /server/repotools\_\[app\] -verify level=5

## Troubleshooting

### Failures

Most issues in the tool will be denoted by an error message of some kind
in the repotools command log file. Some errors will cause the tool to
stop running immediately, while other issues can be safely logged and
allow the tool to continue, allowing multiple issues to be identified in
one run. If the error message is unclear or does not provide an obvious
path to resolution, most information IBM Support will need is contained
in the log file. In some cases, the export file can be helpful as well,
provided it is not too large for transfer and any private data sharing
issues can be resolved.

Specific issues:

-   If rebuilding indices fails because data is not unique, this will
    require a support case to resolve any duplicate data issues before
    rebuilding indices and using the server.
-   If you see the error "Results file already exists." when running
    compare, or "The file already exists. Use the option "overwrite" to
    overwrite an existing file." when running exportConcurrent. Both the
    -exportConcurrent and -compare commands can fail if they are run
    multiple times without clearing out any generated files. Both
    commands allow the parameter **overwrite=true** to allow the command
    to overwrite any existing files.
-   Applications sometimes write log events to the database on serivice
    initialization, however this interferes with compare operations. So
    it is possible to see exceptions like the following in the log;
    these can be safely ignored:

2021-12-09 08:20:53,328 Unable to log startup event
com.ibm.team.repository.common.MigrationInProgressException: CRJAZ1966E
Write operations cannot be performed on item type "DBEvent" at this
time. An application migration is currently in progress.

-   When loading a Project area after a migration, you see a 400 bad
    request. You need to ensure the Jena indices are configured
    properly, i.e. com.ibm.team.jfs.index.root.directory=indices Do not
    put the application name in the root directory path.

### Performance

If the export and import in your test environment takes longer than the
time window you have available as an outage, review repotools Statistics
Monitoring output and consider ways you can optimize your operational
environment. The Statistics Monitoring tracks useful hardware, software,
and system performance information that can be used to compare an
environment to a more highly performing setup. Server ping times between
ELM and database machines should be as low as possible.

Some ways to speed up migrations:

-   Disable Anti-Virus software for the duration of the migration
-   Use SSD drives
-   Provide ample RAM and cores for both the ELM and Database servers
-   Add more heap space to the repotools script commands

The threadpool sizes used by optimized migration can also be modified
using java System Properties defined in the repotools script file:

-Dcom.ibm.team.repository.migration.internal.service.sql.MigrationThreadPool.THREAD_POOL_SIZE=50
(default is 20)
-Dcom.ibm.team.repository.migration.internal.service.sql.DBStore.STORE_THREAD_POOL_SIZE`60 (default is 26.  Should always be 6 or more than the number defined in =MigrationThreadPool.THREAD_POOL_SIZE`.
Example if `MigrationThreadPool.THREAD_POOL_SIZE` is set to 50,
`DBStore.STORE_THREAD_POOL_SIZE` should be set to 56 or higher)

-- Main.ChrisAustin - 2021-03-08

META:FILEATTACHMENT{name="OptimizedMigrationTestScenarioMatrix.3-12-21.xlsx"
attachment="OptimizedMigrationTestScenarioMatrix.3-12-21.xlsx" attr=""
comment="Environment and migration testing times for various ELM
application repositories" date="1617028773"
path="OptimizedMigrationTestScenarioMatrix.3-12-21.xlsx" size="15448"
user="chaustin" version="1"} META:TOPICMOVED{by="chaustin"
date="1617115142" from="Sandbox.ChrisAustinSandbox"
to="Deployment.OptimizedConcurrentDatabaseMigration"}
