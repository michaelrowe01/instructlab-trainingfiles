META:TOPICINFO{author="sbeard" date="1422401282" format="1.1"
version="1.7"} META:TOPICPARENT{name="DeploymentIntegrating"}

# Rational Team Concert and Rational ClearQuest integration cookbook [rational-team-concert-and-rational-clearquest-integration-cookbook]

DKGRAY Authors: [Yuhong Yin](Main.YuhongYin) Build basis: Rational Team
Concert 3.0.1.x, 4.0.x, Rational ClearQuest 7.1.2.x, 8.0.0.x, 8.0.1.x
ENDCOLOR

TOC{title="Rational Team Concert and Rational ClearQuest Integration
Cookbook"}

## Summary

This document provides guidance for deploying Rational Team Concert into
an existing Rational ClearQuest environment. There are various types of
integration capabilities between Rational Team Concert and Rational
ClearQuest: the bridge, the synchronizer, and the importer. The goal of
this document is to help you decide which integration capability best
suits your current deployment or your future deployment plan. After
reading this document, you will have a better understanding about the
technologies that are available to you, as well as some of the
deployment considerations.

The integration of Rational ClearQuest and Rational Team Concert is not
a one-size-fits-all integration. Each user can have a unique integration
deployment. It is beyond the scope of this document to discuss every
possible type; therefore, this document provides a variety of resources
that give you detailed information or videos on quick tour and extended
topics.

## Rational ClearQuest Bridge

The **Rational ClearQuest Bridge** provides a bi-directional
traceability link from records in Rational ClearQuest to work items in
Rational Team Concert. It is a linked-data type integration based on the
[Open Services for Life-cycle Collaboration
(OSLC)](http://open-services.net/). It provides a seamless user
experience with rich hover UI preview, and delegated dialogs including
advanced selection dialogs, and fully functional creation dialogs. These
dialogs support ClearsQuest record form layout and hooks. The bridge
integration also enables ClearQuest live data on a Rational Team Concert
dashboard.

ATTACHURL/ClearQuestRTCBridge.jpg

Rational ClearQuest Bridge is primarily for users who want to continue
to use Rational ClearQuest as a change management system, but also want
to take advantage of other features of Rational Team Concert, such as
agile planning and dashboards. You do not have to change your current
usage of Rational ClearQuest, but you can enhance your Rational
ClearQuest deployment by using Rational Team Concert in a complementary
fashion. It provides a ClearQuest shop with a fast path to realize the
value of Rational Team Concert.

It is implemented as a function of the ClearQuest Web and uses the
[ClearQuest OSCL REST API
interface](https://jazz.net/wiki/bin/view/Main/CqOslcV2). ClearQuest is
an OSLC Change Management(CM) provider and a consumer. It provides OSLC
CM v1 and v2 interfaces, and also consumes OSLC CM services provided by
other tools. [ClearQuest OSCL REST API
](https://jazz.net/wiki/bin/view/Main/CqOslcV2)is also a desired
interface if you want to integrate your own application to ClearQuest.
Since it is HTTP-based, you can call it from any program that supports
HTTP, and it does not require the ClearQuest client to be installed on
the machine where you execute your application.

Through the same bridge integration technology, you can also integrate
ClearQuest with other Rational tools, such as Rational Quality Manager
(RQM), Rational Requirement Composer (RRC), and Rational DOORS, and with
3rd party tools, such as HPALM and Git.

### Quick Tours

**Configure Rational Team Concert and Rational ClearQuest Bridge**:
walks thorough the configuration process for setting up Rational
ClearQuest and Rational Team Concert Bridge integration.

**Use Rational Team Concert and Rational ClearQuest Bridge**:
demonstrates how Rational ClearQuest users can take advantage of
Rational Team Concert. The tasks include linking between ClearQuest
record and Rational Team Concert work item, using creation and selection
dialogs, OSLC link rich hover, showing ClearQuest link from Agile
Planning view, and displaying ClearQuest live data from Rational Team
Concert Dashboard.

### Getting Started

The deployment of the Rational ClearQuest Bridge is straightforward. As
long as you have a working ClearQuest Web server, and your ClearQuest
database has the OSLCLinks package applied and at least one record type
enabled with it, you are ready to integrate ClearQuest with the Rational
Team Concert through the bridge integration. The following infoCenter
content provides step-by-step setup instructions:

-   [Configuring and using the Rational ClearQuest
    Bridge](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.team.rcm.doc/topics/c_configuring_and_using_rcm.html)

### Learn more

-   [Change Management Advanced for Jazz Team Server 4.0 entitlement for
    ClearQuest
    users](http://www-01.ibm.com/support/docview.wss?uid=swg21599656)
-   [Change Management Advanced for Jazz Team Server 3.0 entitlement for
    ClearQuest
    users](http://www-01.ibm.com/support/docview.wss?uid=swg21451088)
-   [Configuring and using Collaborative Lifecycle Management
    integrations](http://pic.dhe.ibm.com/infocenter/cqhelp/v8r0m0/topic/com.ibm.rational.clearquest.integrations.doc/topics/c_clm_int_config_use.htm)
-   [Rational ClearQuest and Rational
    DOORS](https://www-304.ibm.com/support/docview.wss?uid=swg21456993)
-   [Using the ClearQuest and HP ALM
    integration](http://pic.dhe.ibm.com/infocenter/rliahelp/v1/index.jsp?topic=2Fcom.ibm.rational.rlia.hpqc.cq.doc2Ftopics2Fc_hpalm_cq_wkw_ovw.html)
-   [Using the ClearQuest and JIRA
    integration](http://pic.dhe.ibm.com/infocenter/cqhelp/v8r0m0/topic/com.ibm.rational.clearquest.integrations.doc/topics/c_lia_int_jira_ovw.htm)
-   [ClearQuest OSLC 2.0 REST
    API](https://jazz.net/wiki/bin/view/Main/CqOslcV2): These ClearQuest
    REST APIs adhere to the OSLC Core 2.0 and Change Management 2.0
    specifications
-   [ClearQuest OSLC 1.0 REST
    API](https://jazz.net/wiki/bin/view/Main/RcmRestCmApi): These
    ClearQuest REST APIs adhere to the OSLC Core 1.0 and Change
    Management specifications
-   [Extending Rational Team Concert by using OSLC
    services](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.team.concert.sdk.doc/topics/r_oslc_services.html)

## Rational ClearQuest Synchronizer

The **Rational ClearQuest Synchronizer** is a data replication between
Rational ClearQuest records and Rational Team Concert work items. It
supports flexible bi-directional or one-directional synchronization
between a Rational ClearQuest record and a Rational Team Concert work
item. Changes in one application are applied to another using
synchronization rules, which provide the mapping and transformation
information.

ATTACHURL/ClearQuestRTCSynchronizer.jpg

It is primarily for the customers that want to incrementally adopt
Rational Team Concert by having different teams use different tools.
Some projects/teams (for instance, a development team) can choose to
start using Rational Team Concert while other teams (for instance, a
support team) continue to use ClearQuest. The teams using Rational Team
Concert and the teams using ClearQuest have access to the same data
(duplicated by the Synchronizer based on the configured sync rules).
Reports can also be run in either system since the data is consolidated.

The ClearQuest Synchronizer is implemented as an application of the
general Jazz item connector framework. It is a separate component of the
Rational Team Concert offering, and requires setting up a Gateway
service. It uses ClearQuest CM API interface to communicate with
ClearQuest. It can also be used between [Rational Qualify Manager (RQM)
and
ClearQuest](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.test.qm.doc/topics/c_admin_rtc_overview.html).

Please note that there is a high maintenance and support cost associated
with the Rational ClearQuest Synchronizer. Conflicts can occur when two
users make nearly simultaneous changes to a ClearQuest record and its
corresponding work item, and an administrator needs to constantly
monitor these conflicts and resolve them manually by selecting the
appropriate value. It is highly recommend that you evaluate the Rational
ClearQuest Bridge integration before jumping into the Synchronizer
integration.

### Getting Started

It is important that an experienced administrator with knowledge on both
Rational Team Concert and the Rational ClearQuest plans, designs and
configures the synchronizer environment. Please read the Synchronizer
information center contents.

-   [Configuring and using the Rational ClearQuest
    Synchronizer](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.team.connector.cq.doc/topics/c_configuring_and_using_the_clearquest_connector.html)

Before you attempt to use the ClearQuest Synchronizer in your production
environment, go through the ClearQuest Synchronizer tutorial.

-   [Get started with the Rational ClearQuest Synchronizer
    tutorial](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.team.concert.tutorial.doc/topics/tut_cqconnector_abstract.html)

### Transition from ClearQuest Synchronizer to ClearQuest Bridge

If you deployed and used the ClearQuest Synchronizer, but later realized
that the ClearQuest Bridge is a better fit, you can use the
**syncToBridge** tool to migrate the synchronized Rational Team Concert
work items and Rational ClearQuest change requests so that they use the
ClearQuest Bridge and have OSLC links between them. Read the following
information center topic about the tool and the process.

-   [Migrating from the ClearQuest Synchronizer to the ClearQuest
    Bridge](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.team.connector.cq.doc/topics/t_migrate_from_cqsynch_to_cqbridge.html)

## Rational ClearQuest Importer

The **Rational ClearQuest Importer** provides a one-way data migration
from Rational ClearQuest records to Rational Team Concert work items. It
imports ClearQuest records based on a user specified query, and uses a
mapping file to declare how fields and values are mapped from a
ClearQuest scheme to a Rational Team Concert process definition. It
supports importing stateful record types, Users, Notes, Attachments,
Work Item Relationships (duplicates, parent / child, blocks / depends
on, and related), and creates missing objects, such as Contributors,
categories, and iteration, on the fly.

ATTACHURL/ClearQuestRTCImporter.jpg

The Rational ClearQuest Importer is primarily for the customers that
want to move from using ClearQuest to Rational Team Concert as the
change management system instead of maintaining both applications, and
want to bring over certain ClearQuest records to Rational Team Concert.

It is implemented as a function in the Rational Team Concert eclipse
client. It is based on the Bugzilla Importer, and uses the ClearQuest CM
API to communicate to ClearQuest You must install ClearQuest client on
the machine you run the ClearQuest Importer.

### Quick Tour

**Use Rational ClearQuest and Rational Team Concert Importer**:
demonstrates how to use the Importer to migrate ClearQuest Records to
Rational Team Concert work items.

### Getting Started

It is important that an experienced administrator with knowledge on both
the Rational Team Concert and the Rational ClearQuest performs plan,
design and execution of the importing. The following page will help a
Rational ClearQuest administrator to understand Rational Team Concert
work items:

-   [Comparing concepts between ClearQuest and
    RTC](/library/article/499)

Reading the following information center contents is recommended before
beginning the import.

-   [Migrating Rational ClearQuest records to work
    items](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m6/topic/com.ibm.team.connector.cq.doc/topics/t_using_cq_import_wizard.html)

The following jazz.net articles also provide guides or step-by-step
instructions on using the Rational ClearQuest Importer.

-   [Guide to migrating defects from Rational ClearQuest to Rational
    Team Concert](/library/article/391)
-   [Additional guidance and a workshop on importing ClearQuest records
    in to Rational Team Concert](/library/article/1211)
-   [Guide for Importing Jazz Work Items from Bugzilla and Other
    Systems](/library/article/69)

META:FILEATTACHMENT{name="ClearQuestRTCBridge.jpg"
attachment="ClearQuestRTCBridge.jpg" attr="" comment="Rational Team
Concert and Rational ClearQuest Bridge" date="1391394441"
path="ClearQuestRTCBridge.jpg" size="43885" user="yyin" version="1"}
META:FILEATTACHMENT{name="ClearQuestRTCSynchronizer.jpg"
attachment="ClearQuestRTCSynchronizer.jpg" attr="" comment="Rational
Team Concert and Rational ClearQuest Synchronizer" date="1391394542"
path="ClearQuestRTCSynchronizer.jpg" size="44992" user="yyin"
version="1"} META:FILEATTACHMENT{name="ClearQuestRTCImporter.jpg"
attachment="ClearQuestRTCImporter.jpg" attr="" comment="Rational
ClearQuest to Rational Team Concert Importer" date="1391394578"
path="ClearQuestRTCImporter.jpg" size="43718" user="yyin" version="1"}
