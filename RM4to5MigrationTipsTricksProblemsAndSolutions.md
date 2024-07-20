META:TOPICINFO{author="sbeard" date="1417373291" format="1.1"
version="1.6"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Migrating the RM application to V5 from V4.x: Tips, common problems, and workarounds [migrating-the-rm-application-to-v5-from-v4.x-tips-common-problems-and-workarounds]

DKGRAY Authors: Main.MinIdzelis with Main.RichForziati and
Main.GailBurati Build basis: IBM Rational Requirements Composer 4.x and
IBM Rational DOORS Next Generation 4.x, 5.0 ENDCOLOR

TOC{title="Page contents"}

In version 5.0 of the Requirements Management (RM) application, the data
is no longer stored on Jazz Team Server (JTS). Rather, data is stored in
the RM server. Because of this change in where the data is stored, the
steps for the upgrade procedure significantly changed. Compared to the
procedure to upgrade to version 4.x, the procedure to upgrade to version
5.0 has more steps.

First, the database administrator must create a copy of the Jazz Team
Server database to be the new RM database. Then, the application
administrator uses the interactive upgrade guide to create a customized
set of instructions to follow during upgrade. Most of the time, the
`rm_upgrade.[sh|bat]` wrapper script will guide CLM administrators
through the upgrade. However, in some cases, such as if your environment
is distributed without a shared drive or is on a Windows system with a
DBCS code page, the script will create a sequence of Repository Tools
(repotools) commands that does not use the wrapper script.

The RM upgrade script (`rm_upgrade.[sh|bat]`) includes these steps:

1.  updateConfigurationFiles\*
2.  addTables\*\*
3.  finalizeApplicationMigration (RM)
4.  finalizeApplicationMigration (JTS)
5.  reindex
6.  updateProjectBacklinks\*\* (when RM is offline) or
    updateProjectBacklinksOnline\*\* (when RM is online)

\* Requires user interaction to specify the new JDBC database
connection. The rest of the prompts are confirmations.

\*\* Requires user interaction for confirmation prompts only.

## Tips

### Before you begin

-   Generate the upgrade instructions for your deployment by using the
    [interactive upgrade guide](https://jazz.net/).
-   Practice the upgrade by using a staging area with copies of your
    data. Based on the practice run, create time estimates for your
    particular upgrade.
-   Back up your CLM databases. During this same downtime, copy the Jazz
    Team Server database to the new RM database.
-   Make sure that you have the following information:
    -   The installation directory or directories of your CLM 4.X
        applications
    -   The installation directory of your new Jazz Team Server 5.0
        (possibly via mount, if remote)
    -   The JDBC connection syntax for the new RM database
    -   The JDBC connection password for the new RM database
    -   The RM public URL of your deployment

### Know your upgrade order

Upgrade Jazz Team Server first, and then upgrade the RM application.
Finally, upgrade the other CLM applications.

### Determine when to run the reindex step

The reindex step is not required; if you skip it, the indexes are built
after the RM server is brought online. For improved performance, wait
until after the server is online before you run the reindex step to
complete the upgrade. If you are running the `rm_upgrade.[bat|sh]`
script, no progress indicator is shown in the command window during the
reindex. For more information, see [Work Item
87722](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=87722).
Progress updates are written to the `rm_upgrade_rmupgrade.log` file in
the server directory. If you are manually running the reindex step, the
progress indicator is shown in the command window.

### Do not simultaneously upgrade multiple applications

Do not upgrade all of the applications in a distributed CLM environment
at the same time. During the first portion of the RM upgrade, the other
applications must be offline. Then, for the updateProjectBacklinks step,
the applications must be brought online.

It can be confusing to determine when each of the applications should be
upgraded during this process. At this time, the interactive upgrade
guide does not fully document how to determine the order. For more
information, see [Work Item
314856](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=314856).

### Run the script from the server directory

When you use the `rm_upgrade.[sh|bat]` script, be sure to run it from
the `/server` directory, specifying the path to the script. For example:

C:\Program Files\IBM\JazzTeamServer\server\>upgrade\rm\rm_upgrade.bat

To complete the updateProjectBacklinks step, the other applications do
not have to be version 5.0.

Fully complete the update process for Jazz Team Server, and then upgrade
the RM application separately from the CCM and QM applications. After
the Jazz Team Server upgrade is complete, you can upgrade the CLM
applications in any order. However, it is less confusing to complete the
upgrades separately.

### Run the finalizeApplicationMigration commands carefully

Two steps run repotools commands that have almost identical names:

`repotools-rm.bat -finalizeApplicationMigration`

`repotools-jts.bat -finalizeApplicationMigration checkOauthDomain=true applicationId=RM-application-id newPublicUrl=NEW_RM_PUBLIC_URL`

## Common problems and workarounds

### The editor that verifies properties does not work on Linux systems

During the updateConfigurationFiles step, the Jazz Team Server and RM
`teamserver.properties` files open in an editor where you can inspect or
update them. On Linux systems, the editor does not work. For more
information, see [Work Item
87659](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=87659).
**Workaround** Manually open the files.

------------------------------------------------------------------------

### After a step fails, you cannot resume the upgrade

If the upgrade script fails during any of the steps, you cannot resume
from the point of failure. **Workaround** Run the upgrade script again
from the beginning and skip the steps that succeeded. For more
information, see [Work Item
87732](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=87732).

------------------------------------------------------------------------

### Errors occur when you upgrade the RM application first

Before you upgrade the RM application, be sure to upgrade Jazz Team
Server. If you upgrade the RM application first, you might encounter
errors like the ones shown in this example:

2014-05-07 15:17:59,432 Repo Tools 2014-05-07 15:17:59,432
java.version=1.6.0 2014-05-07 15:17:59,432
java.runtime.version=pwa6460sr15fp1-20140110_01 (SR15 FP1) 2014-05-07
15:17:59,448 Provisioning using "c:\Program
Files\IBM\JazzTeamServer\server\upgrade\rm\\.\\.\conf\rm\provision_profiles".
2014-05-07 15:17:59,479 repotools-rm -addTables 2014-05-07 15:17:59,479
Rational Requirements Composer, Version 5.0 (RMS5.0-I20140502_1820) Jazz
Foundation - Core Libraries, Version 5.0 (RJF-I20140502-1642)

2014-05-07 15:17:59,526 To submit questions about issues, go to the
Jazz.net forum at <https://jazz.net/forum>. To find more information
about a message, see the CLM Messages Information Center at
<https://jazz.net/help-dev/CLMErrorMessages/index.jsp>. 2014-05-07
15:17:59,526 CRJAZ1363I Loading the configuration from
"<file:conf/rm/teamserver.properties>". 2014-05-07 15:18:01,245 Rational
Requirements Composer is starting. Rational Requirements Composer,
Version 5.0 (RMS5.0-I20140502_1820) Jazz Foundation - Core Libraries,
Version 5.0 (RJF-I20140502-1642)

2014-05-07 15:18:01,245 CRRRS9938I Repository state is: INITIALIZING
2014-05-07 15:18:01,370 CRJAZ1778I This server is configured as an
application. 2014-05-07 15:18:01,729 CRJAZ2558I Setting the local server
rename state to false and the openServerDescriptionServiceTemporarily
state to false. 2014-05-07 15:18:02,885 CRJAZ1365I The server is
attempting to connect to the following database:
"conf/rm/derby/repositoryDB" 2014-05-07 15:18:04,214 CRJAZ1364I The
connection to the following database was successful: Db Product Name:
Apache Derby Db Product Version: 10.8.2.3 - (1212722) Db URL:
jdbc:derby:conf/rm/derby/repositoryDB;create=true Jdbc Driver Name:
Apache Derby Embedded JDBC Driver Jdbc Driver Version: 10.8.2.3 -
(1212722) 2014-05-07 15:18:05,667 CRJAZ1970I The application is
configured with: Public URI: "<https://minvm.ibm.com:9443/rm>" Jazz Team
Server location: "<https://minvm.ibm.com:9443/jts/>" 2014-05-07
15:18:06,073 CRJAZ2523I Setting the global server rename state to false
and the validation state to false. 2014-05-07 15:18:09,854 CRJAZ2105I
Checking for a running server... 2014-05-07 15:18:13,542 CRJAZ1886E The
configured database lock id does not match the lock id in the database.
This can happen if two applications or Jazz Team Servers are trying to
access the same set of tables, or if the lock id was overwritten or lost
in the teamserver.properties configuration file. Check the server
configuration and the database connection spec and ensure they are
correct. To recover from an emergency lockout, the lock can be reset
using the 'repotools-rm -resetRepoLockId' command.
com.ibm.team.repository.common.TeamRepositoryException: CRJAZ1886E The
configured database lock id does not match the lock id in the database.
This can happen if two applications or Jazz Team Servers are trying to
access the same set of tables, or if the lock id was overwritten or lost
in the teamserver.properties configuration file. Check the server
configuration and the database connection spec and ensure they are
correct. To recover from an emergency lockout, the lock can be reset
using the 'repotools-rm -resetRepoLockId' command. at
com.ibm.team.repotools.commands.local.internal.AddTablesCommand.execute(AddTablesCommand.java:153)
at
com.ibm.team.repotools.command.AbstractCommand.execute(AbstractCommand.java:67)
at
com.ibm.team.repotools.rcp.internal.RepositoryToolsApplication.run(RepositoryToolsApplication.java:816)
at
com.ibm.team.repotools.rcp.internal.RepositoryToolsApplication.start(RepositoryToolsApplication.java:891)
at
org.eclipse.equinox.internal.app.EclipseAppHandle.run(EclipseAppHandle.java:196)
at
org.eclipse.core.runtime.internal.adaptor.EclipseAppLauncher.runApplication(EclipseAppLauncher.java:110)
at
org.eclipse.core.runtime.internal.adaptor.EclipseAppLauncher.start(EclipseAppLauncher.java:79)
at
org.eclipse.core.runtime.adaptor.EclipseStarter.run(EclipseStarter.java:369)
at
org.eclipse.core.runtime.adaptor.EclipseStarter.run(EclipseStarter.java:179)
at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method) at
sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:60)
at
sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:37)
at java.lang.reflect.Method.invoke(Method.java:611) at
org.eclipse.equinox.launcher.Main.invokeFramework(Main.java:620) at
org.eclipse.equinox.launcher.Main.basicRun(Main.java:575) at
org.eclipse.equinox.launcher.Main.run(Main.java:1408) at
org.eclipse.equinox.launcher.Main.main(Main.java:1384) Caused by:
com.ibm.team.repository.common.TeamRepositoryException: Server lock id
value \[none\] and database lock id \_2nasMNXuEeONBLWylHGefg do not
match for database
jdbc:derby:c:/PROGRA\~1/IBM/JAZZTE\~1/server/conf/rm/derby/repositoryDB.
Use the 'repotools-rm -resetRepoLockId' command to remove the DB lockID,
after ensuring this DB is not used by another JTS or application. at
com.ibm.team.repository.service.internal.db.util.RepoLockIdUtil.checkServerToSchemaLockAndReturn(RepoLockIdUtil.java:207)
at
com.ibm.team.repository.service.internal.db.util.RepoLockIdUtil.checkServerToSchemaLockAndReturn(RepoLockIdUtil.java:161)
at
com.ibm.team.repository.service.internal.db.util.RepoLockIdUtil.checkServerToSchemaLock(RepoLockIdUtil.java:141)
at
com.ibm.team.repotools.commands.local.LocalRepositoryCommand.checkIfRepoLockIdValid(LocalRepositoryCommand.java:228)
at
com.ibm.team.repotools.commands.local.internal.AddTablesCommand.execute(AddTablesCommand.java:149)
... 16 more 2014-05-07 15:18:13,542 CRJAZ1728E A Repository Tools error
occurred. For more information, see this log file: c:\Program
Files\IBM\JazzTeamServer\server\repotools-rm_addTables.log 2014-05-07
15:18:13,682 CRRRS4120I Rational DOORS Next Generation Fronting Service
bundle stopped

The errors occur because the file you used was a new Jazz Team Server
file and it did not have the required properties. **Workaround** To fix
this issue, upgrade Jazz Team Server first, and then run the upgrade
script again.

------------------------------------------------------------------------

### Unexpected behavior occurs when the RM finalizeApplicationMigration command is running When you run the RM `finalizeApplicationMigration` repotools command, unexpected behavior can occur if you specify any of these arguments: \* `checkOauthDomain=true`

-   `applicationId=RM-application-id`
-   `newPublicUrl=NEW_RM_PUBLIC_URL`

**Workaround** Do not specify any of those arguments when you run the RM
`finalizeApplicationMigration` repotools command.

------------------------------------------------------------------------

### 'Unresolved context' message is shown when you view RM projects

When you view RM projects on the `/admin` page, if you see
`unresolved context`, check the parameters to the JTS
`finalizeApplicationMigration` command. The parameters are not verified
and will be used as is. **Workaround** Check the `newPublicUrl` argument
for typos.

------------------------------------------------------------------------

### Problems occur when creating projects from the /admin page

If you have problems creating projects from the `/admin` page, verify
arguments for the JTS `finalizeApplicationMigration` command.
**Workaround** Specify `checkOauthDomain` or set
`checkOauthDomain=false`.

------------------------------------------------------------------------

### Problems occur during the addTables step

If you are not using the correct Oracle DB2 driver and database, during
the addTables step, an error occurs. **Workaround** Be sure to use the
correct Oracle DB2 driver and database for your setup.

##### Related topics: [Running the RM upgrade script for version 5.0](RunningTheRMUpgradeScriptForVersion50) [related-topics-running-the-rm-upgrade-script-for-version-5.0]

##### External links: None [external-links-none]

##### Additional contributors: None [additional-contributors-none]
