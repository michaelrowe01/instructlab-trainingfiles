META:TOPICINFO{author="rnaranjo" date="1705520959" format="1.1"
reprev="1.64" version="1.64"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Upgrade insider [upgrade-insider]

DKGRAY Authors: Main.RosaNaranjo, Main.PaulEllis Build basis:
Engineering Lifecycle Management (ELM) 7.0.x, Engineering Lifecycle
Management (ELM) 6.0.x, Collaborative Lifecycle Management (CLM) 5.0
ENDCOLOR

TOC{title="Page contents"}

This page has a list of concerns along with work items of interest all
in the context of the IBM Engineering Lifecycle Management (ELM) 6.0.x
upgrade capability. It will also start to include 7.0.x Upgrade topics.

This page has been updated with information for 6.0.6.1 and 7.0.x.

This article was originally targeting the following additional releases:
The Rational solution for Collaborative Lifecycle Management 2012,
Rational Team Concert 4.0.x, Rational Quality Manager 4.0.x, Rational
Requirements Composer 4.0.x, Rational Reporting for Development
Intelligence 2.0.x. We have removed these from the Build Basis to
concentrate on the supported Engineering Lifecycle Management 6.x
series.

## Bookmarks

\* START HERE --\> [7.0.3 Knowledge Center Interactive Upgrade
Guide](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=management-interactive-upgrade-guide)
\* [ELM 7.0.3 Upgrading
tabs](https://jazz.net/downloads/elm/releases/7.0.3?p=upgrading) \*
[Upgrade Checklist - advice is generic to all
releases](https://jazz.net/wiki/bin/view/Deployment/UpgradeMustReadList)
\* [ELM Install & Upgrade New &
Noteworthy](https://jazz.net/pub/new-noteworthy/install_upgrade/7.0.3/index.html)
\* [Staging a test environment for the upgrade
process](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.3/com.ibm.jazz.install.doc/topics/t_prepare_staging_env.html)

## Important

-   If you are planning to upgrade to the Engineering Lifecycle
    Management, plan to upgrade to 7.0.3, which is the latest release.
    **VERY IMPORTANT** Check for the latest fix pack available at the
    time you begin planning to stage your upgrade. There can be fixes
    that help avoid serious upgrade issues and are hard to recover from.

<!-- -->

-   Generate an interactive upgrade guide from the latest Knowledge
    Center so that you do not miss out on any important steps that have
    been added to the upgrade.

\* [Whats new in IBM Engineering Lifecycle Management
7.0.3](https://jazz.net/blog/index.php/2023/10/31/ibm-engineering-lifecycle-management-v7-0-3-is-available-today-sign-up-for-the-launch-webinar-on-november-7/)
\* [Whats new for IBM Engineering
Administrators?](https://jazz.net/blog/index.php/2023/12/06/whats-new-for-ibm-engineering-7-0-3-administrators/)
\* [What's new for IBM Engineering Rhapsody Model Manager
7.0.3?](https://jazz.net/blog/index.php/2023/10/30/whats-new-in-ibm-engineering-rhapsody-model-manager-7-0-3/)

## 7.0.x information

### **New for 7.0.3**

7.0.3 includes Java 11 which no longer includes fonts. Check to see that
fonts are installed prior to upgrading or you may run into a
NullPointerException during the repotools -addtables execution. For X11
on Linux, these are provided by a package called fontconfig. To find out
if fonts are installed use *fc-list* which is installed with fontconfig.
If fontconfig not installed use e.g. `dnf install fontconfig` then
`fc-list` will work to show the fonts installed or use `fc-cache -v` to
see the folders where fonts are installed.

[Whats new in IBM Engineering Lifecycle Management 7.0 enterprise
deployments](https://jazz.net/blog/index.php/2020/04/16/whats-new-in-ibm-engineering-lifecycle-management-7-0-enterprise-deployments/)

-   Upgrade order is an important aspect to be aware of with upgrades to
    7.0. Upgrade order should always be JTS first, then GC (if
    applicable), followed by other apps like EWM, ETM, Reporting, and
    lastly DN (DOORS Next). As it is expected that your DN upgrade
    duration will be longer than your ETM(Engineering Test Management)
    or EWM(Engineering Workflow Management) upgrade, then it would be
    possible to concurrently run these applications' upgrade. There
    other considerations, if you upgrade applications concurrently such
    as contention for resources on your database server and application,
    virtualized hardware.

For RM, you will need to understand the concept and applicability of
link validity data migration. See [Migrating the Requirements Management
application link validity data in a single-server
topology](MigratingTheRequirementsManagementLinkValidityData) if you
have collocated your JTS and RM within the same webcontainer.

-   repotools-rm -rebuildTextIndices - Best practice is to run this
    offline command. Prior to v7.0, this command was not applicable to
    RM. It is now applicable. It is highly recommended that this command
    be run prior to bringing the RM server online and for use by your
    user community. Fulltext search and other areas such as view query
    results may produce inconsistent or incorrect results if these
    indices rebuild is not complete. There is an online process that
    will rebuild these indices while online and at times there is a
    message displayed that this process is underway but the most
    reliable approach is to do this operation offline prior to server
    start post-upgrade.

### AM 6.0.6.1 to 7.0 Upgrade information

RMM 6.x (AM) was built on top of RTC 6.x to utilize SCM functionality
provided by RTC, however, it was shipped as a standalone application
which used "/am" context root by default.

In 7.0, RMM 6.x is now EWM+RMM Extension 7.x. It is no longer a
standalone application in 7.x.

When generating an IUG, you must be cognizant of the answers provided to
some of the questions such as the one regarding the use of custom
context root. The most confusing part, which is not properly explained
in IUG (yet), is that the upgrade of RMM 6.x to EWM+RMM 7.x must be
treated in the same way as the upgrade of RTC 6.x to EWM 7.x with the
custom context root "/am".

Thus, the answer to "Did you use a custom context root in your previous
deployment?" must be "Yes" and the context root used by RMM 6.x ("am" or
the other if it is not equal to the default one) must be explicitly
specified in the corresponding field under the section "Enter the
context root you used for your application:". Without these answers,
commands generated in IUG will contain no mandatory parameters (such as
"-applicationContextRoot am") and the upgrade will fail.

## Updates

## Issues encountered when upgrading to Engineering Lifecycle Management 7.0.x

### [Full ETL job fails after upgrading to 7.0.1 if the Default Workflow was assigned to an artifact type - DNG upgrade](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=137042)

07/28/2020 14:43:48,912 \[dcc_etl_RRC_ODS_RRCResourceGroup0_fetcher_0\]
ERROR An exception occurred when connecting to the server:
com.ibm.rational.datacollection.etl.authentication.OAuthETLHttpClient\$3:
Error 400: Bad RequestError 400: Bad Request Slug should be decorated
but is not 'DefaultWorkflow'Requirements Management/7.0.1 07/28/2020
14:43:48,912 \[dcc_etl_RRC_ODS_RRCResourceGroup0_fetcher_0\] ERROR Can
not retrieve the resources after 10 retries.
com.ibm.rational.datacollection.etl.authentication.OAuthETLHttpClient\$3:
Error 400: Bad RequestError 400: Bad Request Slug should be decorated
but is not 'DefaultWorkflow'Requirements Management/7.0.1 at
com.ibm.rational.datacollection.etl.authentication.OAuthETLHttpClient.send(OAuthETLHttpClient.java:162)
at
com.ibm.rational.datacollection.etl.fetcher.DataFetcher.call(DataFetcher.java:247)
at
com.ibm.rational.datacollection.etl.fetcher.DataFetcher.call(DataFetcher.java:1)

### [Reconcile of collection/module/view fail in projects that were upgraded from 6.x to 7.0](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=135850)

See defect for more steps on how to reproduce this defect. The
fingerprint in the logs is as follows:

\- QM log:

2020-05-11 07:36:56,499 \[ pool-40-thread-1\] WARN com.ibm.rqm.oslc -
Fail to query for the update requirement for Collection:
<https://clmsupport:9443/rm/materializedviews/_4u1p8ZN4EeqMLJD9ydmLig>
Error accessing
<https://clmsupport:9443/rm/calmFilter/_jjc7cHgHEeqNiJdF5ysg7w/requirementsChangedSince?collection=https://clmsupport:9443/rm/materializedviews/_4u1p8ZN4EeqMLJD9ydmLig&after=2020-05-11T11:18:22Z>:
Bad Request

\- RM log:

2020-05-11 07:36:56,311 \[\] \[\] \[ Default Executor-thread-2313\] WARN
.ibm.rdm.fronting.server.services.uri.UriDecorator - Slug should be
decorated but is not '\_4u1p8ZN4EeqMLJD9ydmLig' 2020-05-11 07:36:56,326
\[\] \[\] \[ Default Executor-thread-2313\] ERROR
erver.services.process.internal.ProjectAreaService - CRRRS4122E Error in
HEAD request to determine project context. Falling back to DESCRIBE
java.lang.IllegalArgumentException: Slug should be decorated but is not
'\_4u1p8ZN4EeqMLJD9ydmLig'

Fixed in: 7.0 ifix 4; 7.0.1 ifix 1 (See [Maintenance
dashboard](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.dashboard.viewDashboard&team=Jazz20Collaborative20ALM20Maintenance&tab=_1)
for dates and confirmation these ifixes contained APAR PH25384.

[Error during version 7.0 upgrade of IBM Engineering Lifecyle Management
solution "CRJAZ3170E The operation cannot continue because a previous
database operation is in progress: Add tables in
progress](https://www.ibm.com/support/pages/error-during-version-70-upgrade-ibm-engineering-lifecyle-management-solution-crjaz3170e-operation-cannot-continue-because-previous-database-operation-progress-add-tables-progress)

### DNG upgrade SQL Server

[DOORS Next upgrade from ELM 6.x to 7.x on SQL Server appears to hang at
Initialization Complete
phase](https://www.ibm.com/support/pages/node/6254393)

## Where can I find workarounds, technotes or late-breaking updates for the 7.0.x release(or latest generally available release)?

Workaround articles will be published on Jazz.net. A workaround article
is a Jazz.net article that documents a single issue that is applicable
to one or more GA releases. Here are some shortcuts to help you find
what you need:

[IBM Engineering Workflow Management 7.0.1
Workarounds](https://jazz.net/library/article/95631)

[IBM Engineering Test Management
Workarounds](https://jazz.net/library/#q=&tag=workaround2C7.0.1&project=test-management&sort=pubDate)

[IBM Engineering Requirements Management DNG 7.0.1
Workarounds](https://jazz.net/library/#q=&tag=workaround2C7.0.1&project=requirements-management-doors-next&sort=pubDate)

[Jazz Foundation 7.0.1
Workarounds](https://jazz.net/library/#q=&tag=workaround2C7.0.1&project=jazz-foundation&sort=pubDate)

[Jazz Reporting Service 7.0.11
Workarounds](https://jazz.net/library/#q=&tag=workaround2C7.0.1&project=jazz-reporting-service&sort=pubDate)

[Engineering Insights
Workarounds](https://jazz.net/library/#q=&tag=workaround2C7.0.1&project=rational-engineering-lifecycle-manager&sort=pubDate)

## Issues encountered when upgrading to Collaborative Lifecycle Management 6.0.6 and Engineering Lifecycle Management 6.0.6.1

-   [QM CleanupUnreferencedCollectionRecordsAsyncTask in 6.0.6.1 may
    cause unintended data
    deletion](QMCleanupTaskInMayCauseUnintendedDataDeletion)
-   [QM addTables command can fail on 6.0.6.1
    upgrade](QMAddTablesFailedOn6061Upgrade)

### CRJAZ1431E - The model COMPONENT_ID_IDX was illegally changed to be unique

When upgrading to CLM 6.0.4, 6.0.6 or ELM 6.0.6.1, we have observed:
CRJAZ1431E - The model COMPONENT_ID_IDX was illegally changed to be
unique being reported for SQL Server customers. The [Interactive Upgrade
Guide for ELM
7.0](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.rational.clm.doc/helpindex_clm.html&scope=null)
will now include this information. The work item where this change is
tracked is [Document CRJAZ1431E - The model COMPONENT_ID_IDX was
illegally changed to be unique in the Interactive Upgrade Guide for SQL
Server](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=490306).
The new details are:

Resolving the CRJAZ1431E error message

If during the upgrade you encounter the following error message:
CRJAZ1431E - The model COMPONENT_ID_IDX was illegally changed to be
unique, you can use the SQL Server Management Studio to resolve the
issue.

1.  Log into SQL Server Management Studio 2. Set the indices property to
    Unique for both VVCMODEL_CHANGE_SET_ID_IDX and
    VVC_MODEL_COMPONENT_ID_IDX.

Note - you should make the same change in the CCM, QM, and RM databases

### "Error syncing enumerated values of ArtifactFormats Attribute Data Types." during upgrade

The defect [Build to build migration failed with "Error syncing
enumerated values of ArtifactFormats Attribute Data
Types.](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=121310)
details a scenario that has been seen in multiple upgrades. If you
encounter this problem then contact IBM Support.

If you are able to follow the error in the addTables.log to the
offending project, then you can evaluate if that project's data is
required to upgrade. This should be relatively straight forward. If we
take a look at the error, then we see:

Error syncing enumerated value of ArtifactFormats Attribute Data Type:
Enumerated model entry number: 12 out of 22 Type location:
<https://myserver.com/rm/types/_M0qOEz1nEeiGR5Ps3_opqR> Component name:
my_Component Component location:
<https://myserver.com/rm/cm/component/_L8JRsD1nEeiGR5Ps3_opqR> Project
name: My Project Name Project location:
<https://myserver.com/rm/process/project-areas/_AZbcDEfGHijKL1Mn2_opqR>
Created by user: <https://myserver.com/jts/users/myuser> Created on
time: 2017-04-11T11:05:31.594Z Modified by user:
<https://myserver.com/jts/users/ADMIN> Modified on time:
2018-05-02T17:10:54.686Z Type RDF model:

The rest of the error messages from the log would continue over each
issue being reported.

If you need to keep this data, then you will need to contact IBM Support
and create a case via IBM Support Portal.

If you are able to delete the data, say as it was test data then refer
to: [Deleting data permanently from a DOORS Next Generation
project](https://www.ibm.com/support/pages/deleting-data-permanently-doors-next-generation-project)
If you do decide to delete the offending project data, then ensure to
note the full description of the command in the documentation:
[Repository tools command for permanently deleting
resources](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6/com.ibm.jazz.install.doc/topics/r_repotools_deleteprojectarearesources.html).

Rather unhelpfully, there is a cosmetic APAR associated with this delete
command to further confuse you. APAR PH08726. [Defect 471238: upgrade -
upgrading from 501ifix11 to 6061N: CRJAZ1090I The method "updateCounter"
on service
"com.ibm.team.repository.service.internal.counters.CounterService"](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=471238)

\[ERROR\] 2019-01-28 10:50:52.001 - CRJAZ1090I The method
"incrementCounter" on service
"com.ibm.team.repository.service.internal.counters.CounterService" can
not be executed when it is in the "DEACTIVATED" state.

Ensure you are running against an application server that has been shut
down and check the log file generated from your deleteJFSresources to
see if the content of the project actually was deleted.

### CRLQE0697E An error occurred perform an upgrade encountered upgrading Lifecycle Query Engine

We have seen this occur with other products during non-upgrade use
cases, albeit rarely. This error is occurring when the migration is
attempting to populate a new Lucene index with the data from the
[TDB](https://jena.apache.org/documentation/tdb/architecture.html)
index. The migration takes every graph in the TDB index and puts every
triple from that graph into the Lucene index. It is failing on the part
that iterates over every triple in a graph. So at least one graph in
their TDB is corrupt at the time migration is executing.

2019-12-25 07:54:59,593 \[lqe.UpgradeTask\] \[ERROR\]
m.ibm.team.jis.lqe.maintenance.upgrade.UpgradeTask - CRLQE0697E An error
occurred perform an upgrade.

com.ibm.team.jis.lqe.maintenance.upgrade.UpgradeException: CRLQE0657E
Unable to upgrade Lucene index. at
com.ibm.team.jis.lqe.maintenance.upgrade.handler.Lucene7ReindexHandler.doUpgrade(Lucene7ReindexHandler.java:114)
... Caused by: com.hp.hpl.jena.tdb.base.StorageException:
RecordRangeIterator: records not strictly increasing:
0000000000057e5a0000000000057ee100000000000034bc0000000000000f3c //
000000000004766e00000000000476f50000000000000b5d0100000000000002

The LQE GUI will display:

Migrate Lifecycle Query Engine has detected that migration is required
from 6.0.6.1 M1 to 6.0.6.1 Lifecycle Query Engine encountered problems
during migration. Review LQE and server logs files, correct the errors
and migrate again. CRLQE0657E Unable to upgrade Lucene index.
RecordRangeInterator: records not strictly increasing

You can find more details and resolutions steps in a [IBM technote
1074116: Upgrade operation fails with CRLQE0697E
error](https://www.ibm.com/support/pages/node/1074116)

### Exception in com.ibm.rdm.fronting.server.rrs.vvcproxy.internal.VvcProxyActivator.start() of bundle when executing repotools- -addTables

The error below indicates that an Ifix has been applied to the
installation, but has not been fully provisioned. The IFix readme
includes the command: repotools- -clean which needs to be run after
applying the patch. If you exeperience the following error when running
repotools-rm -addTables then run the clean command and try again.

2019-09-09 12:26:12,540 CRJAZ1363I Loading the configuration from
"<file:conf/rm/teamserver.properties>". 2019-09-09 12:26:14,392
Exception in
com.ibm.rdm.fronting.server.rrs.vvcproxy.internal.VvcProxyActivator.start()
of bundle com.ibm.rdm.fronting.server.rrs.vvcproxy.
org.osgi.framework.BundleException: Exception in
com.ibm.rdm.fronting.server.rrs.vvcproxy.internal.VvcProxyActivator.start()
of bundle com.ibm.rdm.fronting.server.rrs.vvcproxy.

It is important to note the following when you re-attempt the addTables
command: 2019-09-09 13:56:57,093 Starting RM Server Migration. Current
repository version set at \[6.0.6\].

If this value is not the previous version you are migrating from, then
you will need to rollback the application being upgraded.

### Rational DOORS Next Generation or Design Management upgrade to 6.0.4

If you are upgrading a version 6 release of Rational DOORS Next
Generation or Design Management to version 6.0.4, the Interactive
Upgrade Guide instructs you to query for whether artifacts have more
than one current version, and, if so, to run the
-repairMultipleVersionsMarkedAsCurrent repository tools command before
the upgrade. This command addresses a known issue where concurrent
changes to an artifact can cause version issues in configurations. The
-repairMultipleVersionsMarkedAsCurrent repository tools command is
available in the latest interim fix of each version 6 release. You
**must apply the latest interim fix before** you can use the command. If
you run the query and it detects more than one current version of an
artifact, but the -repairMultipleVersionsMarkedAsCurrent repository
tools command is not available, do not upgrade to version 6.0.4. Contact
support.

### Rational Quality Manager 5.x to 6.x upgrade

Attempts to upgrade to Rational Quality Manager 6.0 using online
migration will not be possible. Support for 6.0.1 is being tracked with
[QM Support online migration for RQM 5.x to
6.x](https://jazz.net/jazz02/web/projects/Rational20Quality20Manager#action=com.ibm.team.workitem.viewWorkItem&id=134955)

Note that the upgrade guide is incorrect as well. See [Workitem
361962](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=361962)

### Reporting Upgrade 5.x to 6.0

-   In version 6.0, RRDI is no longer bundled with the CLM solution.
    Instead there is a Cognos BI Adapter package that is made available
    in the Optional Downloads page. This adapter needs to be installed
    along with a Cognos BI Server in order for RRDI reports to be used
    with CLM v6.0.

### Rational DOORS Next Generation 4.x to 5.x upgrade

Attempts to upgrade from a 4.0.x release of IBM Rational Requirements
Composer (RRC) or Rational DOORS Next Generation (RDNG) to 5.0 or higher
results in all project areas being deleted.

-   [Tech note describing how to run
    finalizeApplicationMigration](http://www-01.ibm.com/support/docview.wss?uid=swg21695623)
-   [All Project Areas are deleted during upgrade to RDNG 5.0.2 if
    finalizeApplicationMigration is rerun following a
    failure](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=343736)

If you use the Interactive Upgrade Guide to get your the instructions
for your situation and you are running in an Enterprise Topology and are
using WebSphere Application Server instead of Tomcat, the instructions
for upgrading the Requirements Management application are not correct.
Specifically, the step **Run the -migration_rm_updateConfigurationFiles
repotools command to merge the existing configuration files** is missing
the `updateTomcatFiles=no` parameter.

This is the incorrect command as it appears in the Interactive Upgrade
Guide (the paths may be different depending on your situation):

./repotools-rm.sh -migration_rm_updateConfigurationFiles
oldApplicationHome=/opt/IBM/JazzTeamServer/server/conf
ignoreJTSVersionCheck

The correct command is as follows:

./repotools-rm.sh -migration_rm_updateConfigurationFiles
oldApplicationHome=/opt/IBM/JazzTeamServer/server/conf
ignoreJTSVersionCheck updateTomcatFiles=no

### Rational Team Concert 4.0.x to 5.0.x upgrade

Upgrading to Rational Team Concert 5.0.x using online migration should
only be attempted if the latest iFix for 5.0.x is used. Otherwise, there
is a corruption problem with workspaces and streams as indicated by this
bulletin: [Using online Migration to migrate CCM server from 4.x to 5.x
can result in corruption of streams and
workspaces](http://www-01.ibm.com/support/docview.wss?uid=swg21699466).

### Rational Quality Manager 4.0.6

New feature of RQM 4.0.6 is the ability to upgrade artifacts while the
server is still online. Read the following topic for more information.
[Online
Migration](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.rational.test.qm.doc/topics/c_online_mig_rqm.html)

### Rational Requirements Composer 4.0.3

As of this release, it is no longer necessary to have a 4.0 RM Analyst
license installed to complete RM Online migration. The issue was fixed
by Jazz Foundation via [License asserts should be suppressed during
migration
(249151)](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/249151)

The issue was initially submitted via [Eliminate the need to have any
license assigned in order to complete RM Online migration
(65651)](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=65651)

## Concerns

The IBM Support portal is a good place to look for any troubleshooting
technotes regarding upgrade. Some notable ones are mentioned here but
there are more if you search the Support portal for upgrade related
technotes.

### Email notifications after upgrading to 6.0.3

[Email Notification may fail after upgrading to CLM
6.0.3](http://www-01.ibm.com/support/docview.wss?uid=swg22001673)

### AddTable fails due to performance optimizations in DOORS Next Generation

[Performance tuning recommendations modify the schema in a way the
upgrade is not
expecting](http://www-01.ibm.com/support/docview.wss?uid=swg21980867)

### Performance issues after upgrading to DOORS Next Generation

[Performance issues and CRRRW7556E after upgrading IBM Rational DOORS
Next Generation (DNG)
repository](http://www-01.ibm.com/support/docview.wss?uid=swg21975746)

### Functional CALs disappear when upgrading from 3.0.1.x or 4.0 to 4.0.1 or later

<http://rhnaranjo.wordpress.com/2013/03/01/upgrade-alert-license-package-changes-affect-some-upgrade-scenarios>

### CLM 4.0.x and WebSphere 8.0.0.5 - Disappearing dashboard BIRT report widgets

If you are planning to upgrade to version 4.0.x of the Rational solution
for CLM or have version 4.0.x of the Rational solution for CLM installed
and are upgrading to WebSphere Application Server 8.0.0.5, be aware of
the problem discussed in work item
[BIRTreportsanddashboardwidgetsarenotworkingcorrectlywithWAS8.0.0.5(242945)](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=242945)
You will need to request a WebSphere Application Server fix (WSAS APAR
PM79419 ) from IBM Software Support. You can also choose to use
WebSphere 8.0.0.4 or earlier, but be careful to NOT apply all the JIT
patches or else the problem will resurface. Note: The workaround
provided in this technote has been shown to be problematic and does not
persist upon reboot.
<http://www.ibm.com/support/docview.wss?uid=swg21616615>

### Upgrade order: RRDI 2.0.x and CLM 4.0.x

CLM should be upgraded first followed by RRDI.

#### Rational Insight 1.1.1 with the Rational solution for CLM 3.0.1.x

This is supported only if Jazz Team Server is at 4.0.0.x. This means
that the CCM, QM, and RM applications (distributed topology only) can be
at 3.0.1.x and work with Rational Insight 1.1.1, but you have to also
use the 'new with 1.1.1' data manager ETLs for 3.0.1. The data manager
ETLs that ship with Insight come in various flavors: ones that are for
use with the Rational solution for CLM 3.0.1 and ones that are for use
with the Rational solution for CLM 4.0.

#### Rational Insight 1.1.1.1 with the Rational solution for CLM 4.0

This is supported only if Jazz Team Server is at 4.0.1 This means that
the CCM, QM, and RM applications (distributed topology only) can be at
4.0.0.x and work with Rational Insight 1.1.1.1, but you have to also use
the 'new with 1.1.1.1' data manager ETLs for 4.0. The data manager ETLs
that ship with Rational Insight come in various flavors: ones that are
for use with the Rational solution for CLM 4.0 and ones that are for use
with the Rational solution for CLM 4.0.1.

#### Rational solution for CLM installations that use Oracle

Use 4.0.0.1 or later at a minimum or use 4.0.1 because 4.0 contained
defects that affect upgrade. The two critical fixes that have to be
present BEFORE doing the upgrade to 4.0 are documented. The first fix is
part of version 4.0.0.1 and should be the upgrade target release used
rather than using the 4.0 GA release.

In the case of the "repotools -upgradeWarehouse" error, the fix does not
work on an already attempted upgrade to the 4.0 GA release. Rather, the
customer was instructed to restore their data warehouse from backup
before running the upgrade with the test fix applied. This amounts to a
data corruption of the data warehouse when you attempt and fail the
upgrade using 4.0 GA code.For details, see Escalation 231794.

#### Errors upgrading the data warehouse

The upgrade script is not able to update the RICALM schema. Until this
schema is updated, no DataManager ETLs can be executed. This issue only
happens when a data warehouse is created by Rational Insight and later
upgraded by the Rational solution for CLM. If the original data
warehouse was created by the Rational solution for CLM, future upgrades
work. A code fix is needed for this issue.

### Jazz Team Server 4.0.1

In distributed topologies with various CLM applications deployed, you
may attempt to upgrade Jazz Team Server to 4.0.1. If you do plan to do
this, be aware of the following: If you use a version of Rational
Requirements Composer that is earlier than 4.0.1, 4.0.0.2, or 3.0.1.6
and you upgrade Jazz Team Server to 4.0.1, the Requirements ETL job will
fail to complete.For more details, see [RM 4.0.0.1 ETL fails after
upgrade of JTS to 4.0.1
(68057)](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/68057)
comment 54.

### Rational Requirements Composer 4.0.1

If you are upgrading to 4.0.1 from 3.0.1.x, see [RRC online migration
fails with licensing errors for rm_user
(68474)](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/68474)
below under Work items of interest If you are upgrading to 4.0.1 from
2.x, see [Can't create PDF/Word on RRC 4.0.1 for migrated artifacts from
RRC 2.0.0.3-\>RRC3.0.1.5-\>RRC4.0.1
(68894)](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/68894)
below under Work items of interest

### Rational Requirements Composer 4.0

IMPORTANT UPDATE - ALERT: Critical stability update for Rational
Requirements Composer 4.0 - this issue is significantly less pervasive
than originally thought and can occur only under a more limited set of
conditions. Before you upgrade to Rational Requirements Composer 4.0,
specifically for customers still at version 2.x, be aware of the issues
in this work item: [Technote required RRC3 fixes for RRC4 upgrade
(60482)](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/60482).
You must contact IBM Software Support for these repair tools that have
been provided by development to address issues in Rational Requirements
Composer 2.x based datasets after to upgrade to 3.0.1.x. If not already
upgraded, use 3.0.1.4 or higher when upgrading from version 2.x. Prior
to upgrading to version 4.0, make sure to validate your Rational
Requirements Composer data and check the upgrade error logs for any
issues. The Rational Requirements Composer development team has wiki
pages that provide more information on how to proceed when encountering
errors during the upgrade process. RRC3Upgrade Wiki

### Default WebSphere profile port may change when using the WebSphereMigration Wizard

WebSphereprovides a tool to easily migrate WebSphereApplication Server
(WAS) profiles from one version to another (for instance from 7.0.0.27
to 8.0.0.3). This tool can create a new application server profile on
the destination version and while doing that it will attempt to assign
the same default ports (9080 for insecure HTTP and 9443 for secure
HTTPS), however if it detects a port conflict (for instance because
another profile on the destination version is already using these ports)
it will resolve this conflict by increasing all port numbers by 1 until
a free port is found. For instance, if ports 9080 and 9443 are found to
be in use, the migrated profile will be configured to use ports 9081 and
9444 (assuming these ports are free, otherwise the port numbers will be
even higher).

Since the public URI must not change (outside of a Server Rename
scenario), the port numbers need to be adjusted after the profile
migration is complete. (Note: If there is a genuine port conflict the
other application using the port(s) needs to be re-configured such that
it doesn't occupy these ports before.) To adjust the ports, change the
`WC_defaulthost_secure` and `WC_defaulthost` ports in the
WebSphereIntegrated Solutions Console. You will also need to change the
ports that are associated to the `default_host` virtual host
accordingly.

## Miscellaneous

Upgrade Rational Quality Manager first to avoid the incompatibility
between a 4.0 Jazz Team Server and Rational Quality Manager 3.0.1.2 or
earlier. Only Rational Quality Manager 3.0.1.3 or later is compatible
with the 4.0 DW schema. Rational Requirements Composer 3.0.1.3 or
earlier is not compatible with Jazz Team Server 4.0. Snapshots broken:
[Snapshot does not have any contents when only JTS is upgraded from
3.0.1.2 to 4.0
(54708)](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/54708).
Use 3.0.1.4 or later in a mixed version topology. Upgrade wrapper
scripts improved -

\* If the index location from 3.0.1 has relative paths, it will copy
indices to the 4.0 directory. (Tomcat only) \* If index location from
4.0 is absolute, copy takes place if the 3.0.x index location differs
from the 4.0 index location.The index location can remain the same in
the 4.0 teamserver.properties file if it is a stable directory. 'Run all
data warehouse jobs' from JTS/admin page should be run after every
upgrade phase is completed.The ETLs play a role in data
validation.Upgrade Scripts - Usage guidance

|  |  |
|----|----|
| If CCM or QM + distributed + can mount | Upgrade with upgrade scripts. |
| If CCM or QM + distributed + cannot mount | Upgrade by using repotools (migration, addtables, etc.) commands. |
| If RM + distributed + can mount | Upgrade with upgrade scripts. |
| If RM + distributed + cannot mount | Upgrade by following the unique instructions documented in the 4.0.x interactive guide. (Select RM, distribute, no mount). |
| All other scenarios | Upgrade with upgrade scripts. |

## Work items of interest

[59775](https://jazz.net/jazz03/web/projects/Requirements Management#action=com.ibm.team.workitem.viewWorkItem&id=59775)
documents [Snapshot does not have any contents when only JTS is upgraded
from 3.0.1.2 to 4.0
(54708)](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/54708)
[Error when ETL Jobs fails no longer mentions that it may be caused by
the user not having the Data Collector CAL as it did in 3.0.1.x
(193849)](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/193849)
(**Fixed in 4.0.0.1**) Rational Requirements Composer known issue:
[Suspect links and recent comments not working in upgraded environment
3.0.1.3 to 4.0
(60433)](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/60433)
\* requires a scoped (partial) reindex.The workaround is still being
investigated. If you have a small repository and/or do not mind some
hours added to your upgrade time, running repotools-jts reindex fixes
the problem. The workaround that is being investigated involves avoiding
a full re-index. \* A patch is available on this Jazz.net wiki page:
[https://jazz.net/wiki/bin/view/Main/RRC4Patches](https://jazz.net/wiki/bin/view/Main/RRC4Patches")
Problem with trial licenses and upgrade process (affects the Rational
Requirements Composer upgrade) - [3.0.1 CALs appear to block
visibility/ability to activate 4.0 Trial Licenses on the License Key
Management page
(214312)](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/214312)
Problem with Tomcat and Basic authentication post 4.0 upgrade
(workaround provided in work item) - [Problem accessing RTC client after
upgrading from CLM 3.0.1 to 4.0 using Basic authentication
(215699)](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/215699)
[RRC online migration fails with licensing errors for rm_user
(68474)](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/68474)
Problem with RM upgrade, 3.0.1.x to 4.0.1, specifically distributed
topology Important: Check the Jazz Team Server License Key Management
page prior to starting RM online migration to ensure the rm_user
internal license is assigned and available; otherwise, the RM online
migration will fail. Fail checks have been added by RM team for 3.0.1.x
to 4.0 and 4.0 to 4.0.1 upgrades so will not encounter the problem then.
Documentation added via [RM upgrade guide needs to be updated with
critical information
(241597)](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/241597)
[RM 4.0.0.1 ETL fails after upgrade of JTS to 4.0.1
(68057)](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/68057) -
Distributed topology, see comment 54 for the crux of the issue.
Can'tcreatePDF/WordonRRC4.0.1formigratedartifactsfromRRC2.0.0.3-\>RRC3.0.1.5-\>RRC4.0.1
BIRTreportsanddashboardwidgetsarenotworkingcorrectlywithWAS8.0.0.5(242945)

### Rational Build Forge integration

N-1 Compatibility issue discovered, Change to
IBuildForgeServicesLayerService.getProjects method signature breaks N-1
compatibility (217378) Workaround: The above issue affects the Rational
Team Concert client, not JBE. There was a breaking API change that
Rational Team Concert is unable to fix, which affects the Get Projects
button in a Rational Build Forge build definition editor when a 3.0.1.x
client is trying to connect to a 4.0 server. The workaround is to use a
4.0 client to edit the build definition.After the build definition is
set up, this does not affect other uses from a 3.0.1.x client; for
example, users can request builds, view build results, etc.

##### Related topics: None [related-topics-none]

##### External links: [external-links]

-   None

##### Additional contributors: Main.PaulEllis Main.DanToczala Main.ChristianGlockner , Main.KrzysztofKazmierczyk [additional-contributors-main.paulellis-main.dantoczala-main.christianglockner-main.krzysztofkazmierczyk]

META:FILEATTACHMENT{name="RRDI20_DW_warningmsg.png"
attachment="RRDI20_DW_warningmsg.png" attr="" comment=""
date="1361292047" path="RRDI20_DW_warningmsg.png" size="11399"
user="rnaranjo" version="1"}
