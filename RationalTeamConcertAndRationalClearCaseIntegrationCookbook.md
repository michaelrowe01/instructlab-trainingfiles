META:TOPICINFO{author="koinuma" date="1406578139" format="1.1"
version="1.16"} META:TOPICPARENT{name="DeploymentIntegrating"}

# Rational Team Concert and Rational ClearCase integration cookbook [rational-team-concert-and-rational-clearcase-integration-cookbook]

DKGRAY Authors: [Masa Koinuma](Main.MasabumiKoinuma) Build basis:
Rational Team Concert 3.0.1.x, 4.0.x, 5.0, Rational ClearCase 7.1.2.x,
8.0.0.x, 8.0.1.x ENDCOLOR

TOC{title="Page contents"}

## Summary

This page provides guidance for deploying Rational Team Concert into an
existing Rational ClearCase environment. Rational Team Concert provides
various types of integration capabilities: the synchronizer, the
importer, and the bridge. The goal of this document is to help you
decide which integration capability best suits your current deployment
or your future deployment plan. After reading this page, you will have a
better understanding about the technologies that are available to you,
as well as some of the deployment considerations.

The integration of Rational ClearCase and Rational Team Concert is not a
one-size-fits-all integration. Each user can have a unique integration
deployment. It is beyond the scope of this document to discuss every
possible type; therefore, this document also provides detailed
information resources and videos on extended topics.

## Rational ClearCase Bridge

The **Rational ClearCase Bridge** provides a traceability link from
Rational ClearCase artifacts to work items in Rational Team Concert.
This is primarily for a customer who wants to continue to use Rational
ClearCase as a source control system, but also wants to take advantage
of Rational Team Concert features such as agile planning, dashboards,
etc. You do not have to change your current usage of Rational ClearCase,
but you can enhance your Rational ClearCase deployment by using Rational
Team Concert in a complementary fashion.

Rational ClearCase Lifecycle integration link

Planning Transparency

Work Item Build SCM

Jazz Team Server

Rational Team Concert

Developers can associate UCM activities or base Rational ClearCase
versions to Rational Team Concert's work items. You can then navigate
from one to the other in the developer IDE. Because a Rational Team
Concert work item is used as the "glue" for all development lifecycle
artifacts, it provides end-to-end traceability throughout the
development life-cycle, from project planning to source code changes.

### Quick Tours

**Using Rational Team Concert 4.0 with Rational ClearTeam Explorer**:
how Rational ClearCase users can take advantage of Rational Team Concert
4.0 while using Rational ClearTeam Explorer to manage their
source-controlled artifacts with the ClearCase UCM.

-----

**Using Rational Team Concert with Rational ClearTeam Explorer**: how to
use Rational Team Concert with Rational ClearTeam Explorer.

-----

**Using Rational ClearCase with Rational Team Concert 3.0**: how
Rational ClearCase users can take advantage of the Build, Work Items,
and Planning features in Rational Team Concert 3.0, while using Rational
ClearCase to manage their source-controlled artifacts. In addition, this
video demonstrates how to link Rational ClearCase artifacts to Rational
Team Concert work items using the Rational ClearCase Bridge.

-----

### Getting Started

The ClearCase Bridge supports various client types, and the deployment
step varies by the client.

#### Eclipse Client

The deployment of the ClearCase Bridge to the Eclipse client is
straight-forward. There are no pre-configurations for administrators.
The setup requires that you only need to install the Rational ClearCase
Eclipse client (Rational ClearTeam Explorer, CCRC, or SCM Adapter) into
the Rational Team Concert Eclipse client. The following articles provide
step-by-step instructions of how to set them up:

-   [Tip: Installing the ClearTeam Explorer to Rational Team
    Concert](/library/article/746) (new in Rational Team Concert 3.0.1.1
    and Rational ClearCase 8.0)
-   [Tip: Installing the ClearCase SCM adapter to Rational Team
    Concert](/library/article/579) (new in Rational Team Concert 3.0)
-   [Tip: Installing the Rational ClearCase Bridge to Rational Team
    Concert (CCRC)](/library/article/414) (UCM Rational ClearCase is
    supported since Rational Team Concert 2.0. Base Rational ClearCase
    is supported since Rational Team Concert 3.0)

In addition to the developer setup, administrators can configure UCM
streams for integration and can enforce the linkage of UCM activities
with work items. Refer to the "Cleartool Command-Line Client" section
below for configuring a UCM stream. When you configure a UCM stream, the
link enforcement is applicable to any client types.

#### Visual Studio Client

The ClearCase Bridge integration is now available to Visual Studio
users. The minimum supported version is Rational ClearCase 8.0.0.7. You
first need to set up the Eclipse client integration and select the
eclipse instance from the Visual Studio IDE options page. This technote
provides step-by-step instruction:

-   [Leverage ClearTeam Explorer and Rational Team Concert integration
    from within Visual
    Studio](http://www.ibm.com/support/docview.wss?uid=swg21637191) (new
    in Rational ClearCase 8.0.0.7)

#### Cleartool Command-Line Client

You can associate UCM activities or file versions to work items while
you work cleartool commands. The administrator or the project lead needs
to configure the UCM stream or the branch-type for integration, and
developer's makeactivity, checkout, or checkin operations associate
Rational ClearCase artifacts with work items automatically. These
technotes provide the setup instruction for administrators and also
describes end-user new commands:

-   [Configure the ClearCase UCM-RTC integration to use the Change
    Management
    Integration](http://www.ibm.com/support/docview.wss?uid=swg21640748)
    (new in Rational ClearCase 8.0.0.7)
-   [Configure the base ClearCase-RTC integration to use the Change
    Management
    Integration](http://www.ibm.com/support/docview.wss?uid=swg21641361)
    (new in Rational ClearCase 8.0.0.7)

#### ClearCase Native GUI Client (new in Rational ClearCase 8.0.0.9 / 8.0.1.2) Follow the set-up instruction above for the Cleartool Command-Line Client.

### Learn More

-   [Using the ClearCase
    Bridge](http://www.ibm.com/support/knowledgecenter/SSCP65_5.0.0/com.ibm.team.connector.scm.cc.doc/topics/c_bridge_intro.html):
    The Rational solution for Collaborative Lifecycle Management 5.0
    Information Center.
-   [Workaround: Opening ClearCase Bridge Links on Rational Team Concert
    Web Client](/library/article/1322): This document describes how to
    set up your web browser to navigate the ClearCase Bridge links from
    Rational Team Concert web client.
-   [Using ClearCase triggers to implement ClearCase Bridge capabilities
    in Rational Team Concert](/library/article/636): This document
    describes how to create traceability links in various Rational
    ClearCase clients, other than the Eclipse shell (ClearTeam Explorer,
    or CCRC), using Rational ClearCase triggers.
-   [Migrating from a ClearCase-ClearQuest integration to a
    ClearCase-Rational Team Concert integration](/library/article/785):
    This document provides guidance on how to migrate Rational
    ClearQuest-enabled UCM to a Rational ClearCase-Rational Team Concert
    integration.
-   [Utilizing Jazz Builds with ClearCase
    SCM](http://www.youtube.com/watch?v=TPnAUzdBZxc): This video
    demonstrates how to run an out-of-the-box Jazz build, using a
    Rational ClearCase dynamic view.

You can also browse discussions on future releases. The Rational
ClearCase Bridge enhancement items are tracked by ClearCase Bridge Open
Stories and Enhancements.

## Rational ClearCase Version Importer The **Rational ClearCase Version Importer** (new in Rational Team Concert 4.0.5) is a one-way data replication tool from Rational ClearCase to Rational Team Concert source control. You can migrate all the versions in any branches in Rational ClearCase in a single operation, and the version branching is also replicated in Rational Team Concert source control. The importer also preserves the checked-in user information.

Rational ClearCase one-way data migration

Planning Transparency

SCM Work Item Build

Jazz Team Server

Rational Team Concert

It can also import Rational ClearCase view configurations as Rational
Team Concert baselines since the version 4.0.6.

You can use the version importer for both Base ClearCase and UCM
ClearCase, but it does not import UCM metadata.

### Quick Tour

**ClearCase Version Importer features for Rational Team Concert 5.0**:
demonstrates enhanced migration capability in the 5.0 release such as
filtering options and migration of CC/CQ UCM integration.

**ClearCase Version Importer features for Rational Team Concert 4.0.6**:
demonstrates enhanced migration capability in the 4.0.6 release such as
multiple configurations import, and incremental migration.

**ClearCase Version Importer in Rational Team Concert**: demonstrates
how Rational ClearCase users can migrate the ClearCase version data to
Rational Team Concert 4.0.5.

-----------

### Getting Started

It is important that an administrator experienced with both the Jazz SCM
system and the Rational ClearCase system performs the setup tasks for
the synchronization or the import. The following article helps Rational
ClearCase administrators to understand the Jazz SCM system:

-   [Comparing concepts between ClearCase UCM and
    RTC](/library/article/502)

The recording/slides of the webinar session is available at ALM
community :

-   [Webinar: Import Version History into RTC](http://bit.ly/1i5WBbF)

Reading the following help topic is recommended before beginning setup:

-   [Migrating data with the ClearCase Version
    Importer](http://www.ibm.com/support/knowledgecenter/SSCP65_5.0.0/com.ibm.team.connector.scm.cc.doc/topics/c_version_importer_intro.html):
    The Rational solution for Collaborative Lifecycle Management 5.0
    Information Center.

If you are interested in large-scale migration and performance
consideration, read the following document:

-   [ClearCase Version Importer performance report in Rational Team
    Concert 4.0.6 release](ClearCaseVersionImporter406PerformanceReport)
-   [ClearCase Version Importer Performance Report in Rational Team
    Concert 4.0.5](/library/article/1368)
-   [Planning to migrate data
    incrementally](http://www.ibm.com/support/knowledgecenter/SSCP65_5.0.0/com.ibm.team.connector.scm.cc.doc/topics/c_plan_incremental_migration.html)

### Learn more

-   [Workaround: The ClearCase Version Importer fails to import multiple
    views and displays the error "Component has outstanding conflicts in
    workspace"](/library/article/1412): This document provides detailed
    information about a known issue of version 5.0.
-   [Workaround: The ClearCase Version Importer Fails to Export When
    Merge Hyperlinks Create Cyclic Dependencies](/library/article/1396):
    This document provides detailed information about a known issue of
    version 4.0.6.
-   [Limitation: ClearCase Version Importer fails to import versions
    with long branch names or long version extension
    names](/library/article/1365): This document provides detailed
    information about a known issue of version 4.0.5.

## Rational ClearCase Synchronizer and Baseline Importer

The **Rational ClearCase Synchronizer** is a two-way data replication
between Rational ClearCase and Rational Team Concert source control. You
can choose a UCM stream or a Rational ClearCase branch to set up
synchronization with a stream of Rational Team Concert source control.
It leverages the Jazz Team Build, and you can run the synchronization on
a scheduled basis or by request. This provides flexibility to enterprise
customers by allowing a subset of teams to choose SCM tools to work
with, while letting you manage all of the latest source code through a
single SCM repository.

The **Rational ClearCase Baseline Importer** is a one-way data
replication from Rational ClearCase to Rational Team Concert source
control. Like the synchronizer, you can choose a UCM stream where all
baselines or only selected baselines are imported, or you can choose to
import label types for base Rational ClearCase. It also leverages the
Jazz Team Build, so you can run the import of new baselines/label types
on a scheduled basis or by request.

Rational ClearCase Two-way synchronization orone-way data migration

Planning Transparency

SCM Work Item Build

Jazz Team Server

Rational Team Concert

### Version Importer or Baseline Importer ?

There are two migration tools available - the Version Importer and the
Baseline Importer. You can choose either of the technology that fits to
your requirements to migrate the data from Rational ClearCase to
Rational Team Concert source control.

-   The Version Importer is a new tool to allow you to import all the
    version histories from Rational ClearCase. You can import versions
    in all branches by a single operation and can import ClearCase view
    configurations as Rational Team Concert baselines. It has been
    available since Rational Team Concert 4.0.5.
-   The Baseline Importer migrates only the interested version (
    versions selected by label types or UCM Baselines ). You have to set
    up the synchronized stream for branch-by-branch or stream-by-stream
    because it is based on the synchronizer technology. It has been
    available since Rational Team Concert 2.0.

### Getting Started

It is important that an experienced administrator for both the Jazz SCM
system and the Rational ClearCase system performs the setup tasks for
the synchronization or the import. The following page will help a
Rational ClearCase administrator to understand the Jazz SCM system:

-   [Comparing concepts between ClearCase UCM and
    RTC](/library/article/502)

A variety of documents are available to help you prepare the
synchronizer or the baseline importer deployment. Reading the following
documents is recommended before beginning setup:

-   [Planning to synchronize and
    import](http://www.ibm.com/support/knowledgecenter/SSCP65_5.0.0/com.ibm.team.connector.scm.cc.doc/topics/t_sync_imp_planning.html):
    The Rational solution for Collaborative Lifecycle Management 5.0
    Information Center.
-   [Deploying Rational Team Concert into a ClearCase/ClearQuest
    Environment](/library/article/581)

The following documents also provide step-by-step instruction to deploy
the Rational ClearCase Synchronizer and Baseline Importer:

-   [Tutorial: Get started with the ClearCase
    Synchronizer](http://www.ibm.com/support/knowledgecenter/SSCP65_5.0.0/com.ibm.team.concert.tutorial.doc/topics/tut_cc_sync_abstract.html)
-   [Importing ClearCase/ClearQuest Unified Change Management into
    Rational Team Concert 3.x](/library/article/550): Step-by-step
    instruction to deploy both Rational ClearCase Synchronizer and
    Rational ClearQuest Synchronizer into a UCM environment.
-   [Using the ClearCase Importer to Import ClearCase
    History](/library/article/50): Step-by-step instruction to deploy
    the Rational ClearCase Baseline Importer with history into a UCM
    enviroment or a base Rational ClearCase environment.

If you are interested in large-scale deployment and performance
consideration, read the following documents. While this is not a
benchmark, because the performance largely depends on both the Rational
ClearCase deployment and the Rational Team Concert deployment, it gives
you an idea of what to expect when using the synchronizer or the
baseline importer.

-   [Deploying Rational Team Concert into a ClearCase/ClearQuest
    Environment (Appendix: Synchronization Performance Data of ClearCase
    Synchronizer 3.0.1)](/library/article/581): The synchronizer
    performance.
-   [Using the ClearCase Importer to Import ClearCase History (Appendix
    1: Performance Data in Rational Team Concert
    3.0.1)](/library/article/50): The baseline importer performance.

### Learn more

-   [Using the ClearCase Synchronizer and Baseline
    Importer](http://www.ibm.com/support/knowledgecenter/SSCP65_5.0.0/com.ibm.team.connector.scm.cc.doc/topics/c_sync_intro.html):
    Rational solution for Collaborative Lifecycle Management 5.0
    Information Center.
-   [Workaround: Conversion of source control provider in synchronized
    Visual Studio projects and solutions](/library/article/577):
    Reference this document when you synchronize or import a Microsoft
    Visual Studio project or a solution. You can configure it to convert
    the source control provider automatically.
-   [Workaround: Create a lock-free Rational ClearCase synchronization
    for UCM streams by running custom scripts](/library/article/1321)
-   [Workaround: Synchronizing base ClearCase MultiSite replicated VOBs
    with Rational Team Concert](/library/article/1011): This document
    outlines a few points to consider when you synchronize MultiSite
    replicated VOBs.
-   [How to switch Rational ClearCase streams and continue synchronizing
    with Rational Team Concert](/library/article/1035): This document
    outlines how to continue synchronizing when switching between
    Rational ClearCase streams or branch types.
-   [Tip: Requesting ClearCase synchronization from a host without
    ClearCase installed](/library/article/580)
-   [Running the ClearCase Synchronization Engine as a service in
    Windows](/wiki/bin/view/Main/CcSyncEngineAsAWindowsService)
-   [ClearCase Synchronizer and History Importer scalability
    improvements for initial import of large numbers of
    files](/library/article/1037)

META:FILEATTACHMENT{name="agileplanning-52.png"
attachment="agileplanning-52.png" attr="h" comment="" date="1387580171"
path="agileplanning-52.png" size="7013" user="koinuma" version="1"}
META:FILEATTACHMENT{name="bridge-arrow.png"
attachment="bridge-arrow.png" attr="h" comment="" date="1387580188"
path="bridge-arrow.png" size="6180" user="koinuma" version="1"}
META:FILEATTACHMENT{name="builds-52.png" attachment="builds-52.png"
attr="h" comment="" date="1387580207" path="builds-52.png" size="6111"
user="koinuma" version="1"} META:FILEATTACHMENT{name="cc-vtree.png"
attachment="cc-vtree.png" attr="h" comment="" date="1387580235"
path="cc-vtree.png" size="5404" user="koinuma" version="1"}
META:FILEATTACHMENT{name="jazz-foundation-16.png"
attachment="jazz-foundation-16.png" attr="h" comment=""
date="1387580255" path="jazz-foundation-16.png" size="827"
user="koinuma" version="1"}
META:FILEATTACHMENT{name="rational-team-concert-16.png"
attachment="rational-team-concert-16.png" attr="h" comment=""
date="1387580283" path="rational-team-concert-16.png" size="723"
user="koinuma" version="1"} META:FILEATTACHMENT{name="rcc-155.png"
attachment="rcc-155.png" attr="h" comment="" date="1387580308"
path="rcc-155.png" size="8425" user="koinuma" version="1"}
META:FILEATTACHMENT{name="sourcecontrol-52.png"
attachment="sourcecontrol-52.png" attr="h" comment="" date="1387580324"
path="sourcecontrol-52.png" size="4634" user="koinuma" version="1"}
META:FILEATTACHMENT{name="sync-arrow.png" attachment="sync-arrow.png"
attr="h" comment="" date="1387580343" path="sync-arrow.png" size="9414"
user="koinuma" version="1"}
META:FILEATTACHMENT{name="transparency-52.png"
attachment="transparency-52.png" attr="h" comment="" date="1387580359"
path="transparency-52.png" size="5180" user="koinuma" version="1"}
META:FILEATTACHMENT{name="workitem-52.png" attachment="workitem-52.png"
attr="h" comment="" date="1387580380" path="workitem-52.png" size="3501"
user="koinuma" version="1"} META:FILEATTACHMENT{name="oneWayArrow.png"
attachment="oneWayArrow.png" attr="h" comment="" date="1388191300"
path="oneWayArrow.png" size="6105" user="koinuma" version="1"}
