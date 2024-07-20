META:TOPICINFO{author="ajurj" date="1510694105" format="1.1"
version="1.2"}
META:TOPICPARENT{name="IoTContinuousEngineeringSolution605"}

# Upgrading the IBM Internet of Things Continuous Engineering Solution DKGRAY Authors: Main.AndreeaJurj Build basis: Version 6.0.5 [upgrading-the-ibm-internet-of-things-continuous-engineering-solution-dkgray-authors-main.andreeajurj-build-basis-version-6.0.5]

ENDCOLOR

TOC{title="Page contents"}

To upgrade the IBM Internet of Things (IoT) Continuous Engineering
Solution, install the new application versions, update configuration
files, add, or update tables in existing database repositories, and
upgrade the data warehouse.

## Supported upgrade paths

If you upgrade multiple products that are running on multiple
application servers, those applications continue to run on separate
application servers after the upgrade. You cannot merge multiple
applications into a single application server. However, you can register
multiple applications with the same Jazz Team Server.

## Planning your upgrade

1.  **Learn about the upgrading process.** When you upgrade the current
    version, you must be prepared to make decisions about URIs, servers,
    deployment topologies, licensing, authentication, and more. To learn
    about the system and software requirements, upgrade process, client
    and server version compatibility, licensing and more, read these
    [articles](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.5/com.ibm.jazz.install.doc/topics/c_upgrade_consideration.html).
    For more information, read the [Collaborative Lifecycle Management
    (CLM) deployment and upgrade planning
    documentation](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.5/com.ibm.jazz.install.doc/topics/c_planning_upgrade.html). 2.
    **Customize your upgrading documentation** by using the [CLM
    interactive upgrade
    guide](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.5/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html).
    Select the options that best describe your installation environment,
    and follow the instructions.

## Upgrade constraints

-   Each Jazz Team Server must be at the same level as the highest
    version of the product that is registered to it.
-   If you install the Jazz Team Server and an application using the
    Jazz Team Server (such as Rational Team Concert) on the same
    WebSphere Application Server, you must apply any future service
    releases to both at the same time.

## Upgrade path overview

Upgrade your applications in this order:

1.  Jazz Team Server version 6.0.5 (if on the same application server as
    other applications) 2. Rational solution for Collaborative Lifecycle
    Management version 6.0.5: Rational Team Concert, Rational DOORS Next
    Generation, Rational Quality Manager, Jazz Reporting Service (Report
    Builder and Lifecycle Query Engine), Global Configuration, Rational
    Engineering Lifecycle Manager, and Design Management 3. Rational
    DOORS and DOORS Web Access version 9.6.1.10 4. Rational Rhapsody
    version 8.3

It is not necessary to upgrade all the products and components. Ensure
that you meet the requirements that are listed under Upgrade constrains.

### Upgrading applications by using the CLM interactive upgrade guide

Use the [Rational solution for CLM
documentation](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.5/com.ibm.help.common.jazz.calm.doc/topics/c_node_jts_upgrading.html)
to upgrade the following applications:

-   Jazz Team Server
-   Rational Team Concert
-   Rational DOORS Next Generation
-   Rational Quality Manager
-   Jazz Reporting Service (Report Builder and Lifecycle Query Engine)
-   Global Configuration
-   Rational Engineering Lifecycle Manager
-   Design Management.

Install the new version of the product, update configuration files, add
or update tables in existing database repositories, and upgrading the
data warehouse.

-   For an overview of the upgrade process, read [Upgrading the Rational
    solution for
    CLM](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.5/com.ibm.jazz.install.doc/topics/c_upgrade_overview.html).
-   Of particular importance is the topic [Understanding the deployment
    and upgrade
    process](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.5/com.ibm.jazz.install.doc/topics/c_understand_upgrade.html).
-   To learn the step by step procedure, see the [Rational solution for
    CLM interactive upgrade
    guide](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.5/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html).

To upgrade Rational Engineering Lifecycle Manager queries, see
[Migrating queries to version
6.0.5](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.5/com.ibm.team.jp.relm.doc/topics/t_relm_migrate_queries.html).

### Upgrading Rational DOORS and DOORS Web Access

To upgrade Rational DOORS, back up all DOORS data, and then install
Rational DOORS to a new directory while the previous version is removed.
Follow the instructions in the [Rational DOORS
documentation](http://www.ibm.com/support/knowledgecenter/SSYQBZ_9.6.1/com.ibm.doors.install.doc/topics/c_upgradingpreviousversion.html).

### Upgrading Rational Rhapsody

To upgrade Rational Rhapsody, back up your data, uninstall the existing
version of Rational Rhapsody, and install the new version. Follow the
instructions in the [Rational Rhapsody
documentation](http://www.ibm.com/support/knowledgecenter/SSB2MU_8.3.0/com.ibm.rhp.migration.doc/topics/rhp_t_iu_upgrading_rhp.html).

##### Related topics: \* [Installing the IoT Continuous Engineering Solution](IoTContinuousEngineeringSolution605) [related-topics-installing-the-iot-continuous-engineering-solution]

##### External links: \* [Introduction to the Internet of Things Continuous Engineering Solution](https://http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.5/com.ibm.help.common.jazz.calm.doc/topics/c_sse_over.html) [external-links-introduction-to-the-internet-of-things-continuous-engineering-solution]

-   [IoT Continuous Engineering Solution
    overview](https://jazz.net/products/continuous-engineering-solution/)
-   [Downloading IoT Continuous Engineering
    Solution](https://jazz.net/downloads/continuous-engineering-solution/)
