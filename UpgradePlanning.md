META:TOPICINFO{author="paulellis" date="1595583015" format="1.1"
reprev="1.35" version="1.35"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Upgrade planning [upgrade-planning]

DKGRAY Author: Main.PaulEllis, Main.BenjaminSilverman Build basis: None.
Release agnostic. ENDCOLOR

TOC{title="Page contents"}

This article provides you with a list of actions you should consider
when planning an upgrade. It is intended to help you think through the
upgrade process without getting lost in the execution details.

The following advice has been adapted from presentations various
InterConnect and Think conferences and is intended to be release
agnostic. However, where links are release specific and pertinent then
the links are for the latest 7.0.x release.

# The 3 core aspects to an upgrade

Over the past number of years the IBM teams, that focus on Engineering
Lifecycle Management(ELM) upgrades, have realized that there are
essentially 3 core elements to completing a successful upgrade. The
technical aspects of an upgrade, whilst important, are certainly not the
most critical. This article details what lies behind the 3 core aspects
of an upgrade, from planning through to execution.

# Planning

-   [Run book for planning your ELM 7.0
    upgrade](https://www.ibm.com/support/pages/sites/default/files/inline-files/ELM720Upgrade20Runbook20Template.docx)
    which reflects the points discussed in this article.

## "What considerations should be in my plan?":

### People There are essentially three sets of people who are involved during the upgrade lifecycle. Users and the various stakeholders are the most obvious. However, as an upgrade is so much more than the technical steps on the day/weekend, utilizing project management techniques is strongly advised for larger deployments.

Also consider which IT teams need to be involved during the upgrade, who
owns each of the systems, who owns each operation

-   application server admin
-   database admin
-   networking admin
-   dont forget the training aspect

### Documentation

The most important document is the [Interactive Upgrade Guide
(IUG)](http://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.0/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html),
where you can generate instructions tailored to your configuration. The
IUG asks that you specify your configuration, operating system,
application(s) to be upgraded, data warehouse requirements,
integrations, etc and uses this input to generate detailed instructions
and an upgrade checklist specifically tailored for your configuration.

Also ensure you utilize:

-   [Upgrading to IBM Engineering Lifecycle Management
    7.0](https://jazz.net/downloads/elm/releases/7.0?p=upgrading) - new
    overall summary of upgrade for ELM 7.0. As the Interactive Upgrade
    Guide is only updated at release delivery, this document now
    contains all the known additional steps required. It is very much a
    READ ME FIRST document.
-   Technotes, alerts, and iFix readmes are available on the [IBM
    Support Portal](https://www.ibm.com/support/entry/portal/overview).
    The **all documentation links** page allows you to apply content
    filters to narrow down your search results.
-   [System Requirements for all
    releases](https://jazz.net/wiki/bin/view/Deployment/DeploymentInstallingUpgradingAndMigrating)
-   [System Requirements for
    7.0](https://jazz.net/wiki/bin/view/Deployment/ELMSystemRequirements70)
-   [Performance data and sizing
    guidelines](PerformanceDatasheetsAndSizingGuidelines)
-   <https://jazz.net/wiki/bin/view/Deployment/RequirementsManagement70Performance>\[Performance
    data and sizing guidelines for DOORS Next 7.0\]\]
-   [Disk
    benchmarking](https://jazz.net/wiki/bin/view/Deployment/DiskBenchmarking)
    New article that covers tools that can benchmark the performance of
    storage systems, and includes some sample results from the IBM labs.
-   [Technote describing how to find ELM 7 licenses in Passport
    Advantage](https://www.ibm.com/support/pages/node/6252343)

The support portal and jazz.net sizings are generally used as a basis
for sizing based on the typical requirements stated. Plan to have the
available capability to expand and explore past the minimum requirements
if possible. When sizing, consider your future expansion needs and most
stressful usage scenarios to determine the needed capacity and topology.

### Timings

Ensure that there is plenty of contingency within an upgrade plan. Add a
time buffer to each major operation to allow for unforeseen problems.
Depending on your data, some of the upgrade processes can take quite a
bit of time and if a problem is discovered, the upgrade will need to be
restarted.

-   The best upgrade plans, will state the hand-off between operations
    and how these steps will be validated
-   Plan for your applications to be unavailable
-   Someone must manage the various parties and the overall progress
-   Ultimately, if the upgrade does not go to plan, there must be a
    focal point that determines if the upgrade is canceled or whether
    there is sufficient contingency not to roll-back

**Note:** When upgrading to DOORS Next 7.x from a DOORS Next 6.x
release, there are additional time considerations to be aware of. In
order to understand your data shape, run the
[SQL](UnderstandingDOORSNextSizingsin6X) against your RM (Requirements
Management) database and follow the instructions on how to [interpret
your data](UnderstandingDOORSNextSizingsin6).

### Features

New features help support your business case for an upgrade. There are
several pages on jazz.net that are designed to assist you with
understanding the release you're looking to adopt.

-   The **Overview** tab in the product/solution [downloads
    page](https://jazz.net/products/elm/) provides a summary of the main
    features along with video demonstrations.
-   For further details, look at the **New and Noteworthy** section on
    the product [downloads
    page](https://jazz.net/downloads/clm/releases/7.0?p=news)
-   [Release
    Notes](https://jazz.net/downloads/elm/releases/7.0?p=releaseNotes)
    states what was fixed in the release, enhancements, workarounds,
    current open issues, etc.

When reviewing features of the CLM application, ensure also that you
look at the each of these pages for each of the applications you wish to
upgrade

-   Verify that your hotfixes are in the release
-   Verify that all system requirements are met, required integrations
    are supported, and product release levels are compatible

### Environments

Unless you are running as a managed service, or in the cloud, then
Collaborative Lifecycle Management (CLM) is a software stack with many
considerations. Where multiple components require changing, you need to
understand in which order to execute these.

-   Ensure any customizations/settings are brought forward, for example:
    Java Virtual Machine heap size changes

### Approach

If there are multiple instances of Engineering Lifecycle Management
(ELM), or any particular application involved, then that invariably also
means multiple instances of users, stakeholders and considerations to
balance. This should dictate your approach, whether it be one colossal
upgrade effort for all or a more segmented piecemeal option. The
interested parties may make this simpler for you by not being able to
upgrade simultaneously due to conflicting release schedules etc. Embrace
the approach most suited to you and your stakeholders.

[Get Ready for IBM Engineering Lifecycle Management
v7.0](https://jazz.net/blog/index.php/2019/12/20/get-ready-for-ibm-engineering-lifecycle-management-v7-0/)
discusses the various considerations for this release and is a great
article for how to approach all new releases of ELM.

### Example scenario

In terms of selecting which component to upgrade first, see how an
upgrade from ELM 6.0.6.1 to 7.0 could be approached.

The operating systems below may be used to host CLM applications:

\| \| **Before** \| **After** \| \| **ELM Version** \| 6.0.6.1 \| 7.0 \|
\| **Database version** \| DB2 11.1ENDCOLOR \| DB2 11.1 / 11.5 (bundled)
\| \| **Application Server**\| WebSphere 9.0ENDCOLOR \| WebSphere 9.0 \|
\| **Operating System**\| Redhat Enterprise Linux (RHEL) 7ENDCOLOR \|
Redhat Enterprise Linux (RHEL) 7 \| \| **Operating System**\| Windows
2016 ENDCOLOR \| Windows 2016 \|

The recommended order for the situation above would be:

-   Upgrade the CLM Operating System(s)
-   Upgrade the Application Server
-   Upgrade the Database Management System
-   Upgrade CLM

## Review your topology

When planning an upgrade, review your topology to ensure it will meet
your business needs. This is the time to consider changing it if
necessary.

To simplify CLM deployment options, IBM has outlined several
[topologies](https://jazz.net/wiki/bin/view/Deployment/DeploymentPlanningAndDesign)
which are the recommended and most frequently chosen deployment patterns
seen in the field. They represent tried and true examples of how
customers have successfully deployed the CLM solution and are used by
our system testing organization to perform deep customer simulation
testing which includes installation, upgrade, functional, performance,
and robustness testing.

When the need to switch topologies, application servers, databases, or
other resources is discovered, make sure to migrate only one system part
at a time where possible to isolate changes to the system.

## Verify that your hot fixes are in the release

To avoid regression, an important step in upgrade planning is to ensure
that any hot fixes that have been deployed in your enterprise are fixed
in the new release. Where there are gaps, contact IBM Technical Support
who will help you get the necessary fixes.

You can get a list of hot fixes by clicking on **about this
application** in the top right-hand side of the web UI. For Rational
Requirements Composer releases prior to 5.0, you will need to maintain a
separate inventory of hot fixes that have been applied.

# Testing

## Setting up a staging environment

Ideally, a staging environment is a test sandbox that includes a
snapshot of production data isolated from the production environment. It
is **imperative** that you test the upgrade procedure prior to
attempting it with your production system. This is especially true when
upgrading to ELM 7.x from ELM 6.x It is strongly recommended you do this
with your **production** data, so that you can fully test links and
artifacts. This again is especially true when upgrading to ELM 7.x from
ELM 6.x See [Topologies and mapping files for setting up a test staging
environment](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.0/com.ibm.jazz.install.doc/topics/c_server_rename_ex2_stage.html)
for details.

Finally, the test environment should be clean and not used for other
evaluation or testing purposes unless the changes can be completely
backed out.

The options, at a glance, for achieving a staging area with production
data are:

-   Isolated subnet environment
-   Isolated Virtual environment
-   Use a local hosts file
-   SOCKs server
-   DNS server

## Reasons for a staging environment

The main three good reasons to test an upgrade are:

The planning process and documentation to be used during the upgrade
depend upon the timings and bespoke steps ascertained during testing.
You are also looking to:

-   Define a repeatable process
-   Realize any defects now
-   Run any performance tests
-   Experimentation; particularly for users to understand new features

You should be or become very familiar with the
[monitoring](https://jazz.net/wiki/bin/view/Deployment/DeploymentMonitoring)
section of this wiki during testing, to be able to recognize performance
patterns during upgrade. Knowing when and whether your system should be
under stress could be the difference between a successful, or aborted
upgrade.

## Further considerations for testing

There are several techniques designed to ensure that the testing of the
upgrade, through iterations, as well as the upgrade itself run more
smoothly.

-   [Expedite Websphere
    configuration](https://jazz.net/wiki/bin/view/Deployment/ExpediteWASconfigurationforupgrade)
    -   Prepare separate JVMs
    -   Use Jython scripts for setup
-   IBM HTTP Server switch the URI easily between repos
-   [Use
    Themes](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.repository.web.admin.doc/topics/c_configuring_themes.html&scope=null)
    to differentiate test and production systems

Although production data is preferred, there are two recommended
scenarios you can use to validate your CLM upgrade:

-   [Money That Matters (MTM)
    sample](https://jazz.net/library/article/88519)
-   [Automated Meter Reader
    sample](http://www.ibm.com/developerworks/rational/library/rational-doors-next-generation-getting-started/tutorial/index.html)

There is also the historical project:

-   [CLM Build Verification Test (BVT)](../Main/ClmTesting) - This test
    scenario, available on jazz.net, is based on a CD Classic
    application that provides a site to buy and rate classic music CDs.

## Downtime Mitigation

Below are some of the strategies used by customers to mitigate downtime
during an upgrade:

-    Collocation - Temporary moving the DBMS closer (or in some cases
    on) to the application server
-    Temporarily increasing system resources (CPU/RAM) and increasing
    the heap size for repotools ([This is particularly relevant to the
    DOORS Next 7.0 upgrade](UnderstandingDOORSNextSizingsin6X)).
-    Keeping the machines use exclusively during the upgrade in the case
    other applications are running any consuming system resources
-    Cleaning up any unwanted data prior to the upgrade. For example,
    large sandbox projects or even instances of the application that
    have been migrated and no longer used
-    Re-indexing applications prior to upgrading to ensure index
    integrity (repotools- -reindex all). See [repotools command
    reference](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.3/com.ibm.jazz.install.doc/topics/r_repotools_reindex.html)
    for usage.

# Utilizing experiences

## Rollback and recovery

The IUG provides guidance in the event you need to back out of an
upgrade. Make sure you have a backout plan. Built on top of the IUG, our
client-facing teams have developed good practice tips based on their
experiences upgrading the CLM application suite, which is summarized
below and

-   Restore points prevent abandoned upgrades

<!-- -->

-   Document a full rollback procedure
-   Dont panic its a tested part of the procedure

As with any backup and recovery procedure, it is important that the back
out plan is tested. It is likely that you will only need to return to a
previous restore point, for example, restore to the point of having
successfully upgraded the Jazz Team Server. You may need to coordinate a
virtual machine rollback to the point of a database backup, so ensure
these tasks are completed concurrently.

## Upgrades are successful when...

We collated experiences of the successful upgrades, even among the most
complex of scenarios. Upgrades are successful when...

-   Defined custom test cases for common usage scenarios
-   Detailed Use Cases define how to perform actions
-   Step-by-step plans for an overall upgrade
-   Full detailed plan of the day/weekend upgrade, including who, when,
    how etc..

Trial runs of upgrade

-   Append newly learned information to plans and improve upgrade
    procedures
-   Provide better estimates of each action and more accurately predict
    downtime for end-users
-   Catch problems before the day of upgrade

## Reporting considerations

The Reporting considerations have changed since the CLM 4.x to CLM 5.x
upgrades when we moved to the Jazz Reporting Service from Cognos
(Insight). The information below is kept for historical reasons as the
data warehouse and JRS considerations are still true, even when
upgrading to ELM 7.x.

Over time, there have been updates to the recommended upgrade order when
there exists a reporting server (either RRDI or Insight) in your
deployment. It is recommended that you review the [Version Compatibility
Matrix for CLM, RRDI, and
Insight](VersionCompatibilityCLMRRDIAndInsight) prior to upgrading.
Currently:

-   CLM should be upgraded before RRDI/Insight
-   It is not required to upgrade CLM/RRDI at the same time
-   Follow pre-upgrade tasks for upgrading RRDI (disabling SSL and
    backing up configuration)
-   If using Insight, skip the data warehouse upgrade during the CLM
    upgrade and run migrateDW first. Then run the repotools-jts
    upgradeWarehouse
-   Like other applications, DCC should always be at the same level as
    the JTS

It is worth reiterating the benefits that were mainly introduced in 5.0
for consideration:

-   Enable the Jazz Reporting Service (JRS) (5.x)
-   Improve dashboard performance by replacing widgets with JRS reports
    when possible
-   Allow the average user to create lifecycle traceability reports

Enable the Data Collection Component (DCC) (5.0.x)

-   Disable Java ETL or Data Manager CLM ETL (Insight)
-   Delegating ETL processing to the DCC takes the strain of ETL
    processing away from the CLM systems. Great for globally distributed
    deployments.
-   Provides faster and more frequent ETL refresh for closer to
    real-time reporting data

## Evaluate using Online Migration

Online migration is possible in Engineering Workflow Management (EWM)
only. This has been possible since Rational Team Concert 5.x.

The main options for online migration of your SCM and tracking and
planning data are documented within the [Online migration for
Engineering Workflow
Management](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.0/com.ibm.jazz.install.doc/topics/c_online_migration_rtc.html)
knowledge centre. You will first estimate how long this will take,
before planning when best to run the commands.

There is an [EMW Online Migration Test
Matrix](RationalTeamConcertOnlineMigrationTestMatrix) as a rough guide,
but the document is somewhat old and as always, your mileage may vary.

#### Historical information for Engineering Test Management (ETM)

As of 4.0.6, online migration and estimates are available for RQM.

[RQM Online Migration Test
Matrix](RationalQualityManagerOnlineMigrationTestMatrix)

RED**Note:** There are some important updates regarding Online Migration
noted on the [Upgrade Insider](UpgradeInsider) page.ENDCOLOR

## Final checklist

As this article explains, the majority of work for an upgrade is prior
to the actual event itself. The last appreciation of an upgrade is that
it is usually performed by real people, over a weekend and/or late at
night. Therefore, reducing the manual steps and ensuring all
eventualities are documented will relieve pressure on those executing
the upgrade.

Here is a basic checklist for the upgrade event itself and a summary of
this article:

-   ICON{checked} Staged communications
-   ICON{checked} Dont deviate from the plan
-   ICON{checked} Ensure operator follows each step
-   ICON{checked} Abort and return another day
-   ICON{checked} Track each step against experience
-   ICON{checked} Monitor for deviance from expected
-   ICON{checked} Once complete run confirmation tests
-   ICON{checked} Scour logs to ensure error-free
-   ICON{checked} Inform users system is available

## Contact us when you need help

There are several ways in which you can get help:

You can contact your Technical Sales Representative or, if you are an
Accelerated Value Partner, then you can also reach out to your
Accelerated Value Lead to review and answer any questions you have
regarding the upgrade.

You can also post questions in the [Jazz Forum
](https://jazz.net/forum/questions/71215/clm-move-data-from-one-server-to-another)
on jazz.net. It is monitored by the jazz community and email
notifications let you know when your question has been answered or has
been commented upon. Before posting your question, please search the
forum as it might already be answered.

##### Related topics: [Deployment installing upgrading and migrating](DeploymentInstallingUpgradingAndMigrating), [Using the product information centers](InformationCenter) [related-topics-deployment-installing-upgrading-and-migrating-using-the-product-information-centers]

##### External links: [external-links]

-   [Basics for Upgrading ANY
    Software](https://dtoczala.wordpress.com/2015/07/22/basics-for-upgrading-any-software/)

##### Additional contributors: Main.RosaNaranjo, Main.RickMaludzinski, Main.GeraldMitchell [additional-contributors-main.rosanaranjo-main.rickmaludzinski-main.geraldmitchell]

META:FILEATTACHMENT{name="3coreaspects.JPG"
attachment="3coreaspects.JPG" attr="" comment="Title - 3 core aspects"
date="1432549194" path="3coreaspects.JPG" size="65292" user="paulellis"
version="1"} META:FILEATTACHMENT{name="Planning.jpg"
attachment="Planning.jpg" attr="" comment="Planning" date="1432552247"
path="Planning.jpg" size="25107" user="paulellis" version="1"}
META:FILEATTACHMENT{name="checklist1.JPG" attachment="checklist1.JPG"
attr="" comment="" date="1432557472" path="checklist1.JPG" size="67331"
user="paulellis" version="3"} META:FILEATTACHMENT{name="checklist2.JPG"
attachment="checklist2.JPG" attr="" comment="features, envs, approach"
date="1432557159" path="checklist2.JPG" size="75163" user="paulellis"
version="2"} META:FILEATTACHMENT{name="Upgradecomponents.JPG"
attachment="Upgradecomponents.JPG" attr="" comment="Components of an
upgrade" date="1432563916" path="Upgradecomponents.JPG" size="75565"
user="paulellis" version="1"} META:FILEATTACHMENT{name="testing.jpg"
attachment="testing.jpg" attr="" comment="" date="1432566049"
path="testing.jpg" size="28103" user="paulellis" version="1"}
META:FILEATTACHMENT{name="3goodreasons.JPG"
attachment="3goodreasons.JPG" attr="" comment="" date="1432567318"
path="3goodreasons.JPG" size="21062" user="paulellis" version="1"}
META:FILEATTACHMENT{name="experiences.jpg" attachment="experiences.jpg"
attr="" comment="" date="1432568707" path="experiences.jpg" size="31131"
user="paulellis" version="1"} META:FILEATTACHMENT{name="rollback.JPG"
attachment="rollback.JPG" attr="" comment="Rollback" date="1432628708"
path="rollback.JPG" size="32034" user="paulellis" version="1"}
META:FILEATTACHMENT{name="clipboard.jpg" attachment="clipboard.jpg"
attr="" comment="" date="1432631903" path="clipboard.jpg" size="14505"
user="paulellis" version="1"} META:FILEATTACHMENT{name="planning2.png"
attachment="planning2.png" attr="" comment="" date="1512571207"
path="planning2.png" size="254280" user="paulellis" version="1"}
