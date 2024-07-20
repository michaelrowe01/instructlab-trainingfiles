META:TOPICINFO{author="tfeeney" date="1581344359" format="1.1"
version="1.7"} META:TOPICPARENT{name="MBeansReference"}

# JMX Application MBeans Reference Guide for 6.0.6.1 DKGRAY Authors: Main.TimFeeney Build basis: 6.0.6.1 [jmx-application-mbeans-reference-guide-for-6.0.6.1-dkgray-authors-main.timfeeney-build-basis-6.0.6.1]

ENDCOLOR

TOC{title="Page contents"}

Revised approach to documenting MBeans

-   A reference guide for a release should be wholly complete, that is,
    it should include new MBeans for the release but also all other
    released MBeans
-   Organize the MBeans for each release by
    -   Java/JVM - since we don't 'own' these, it could be that these
        standalone outside the ELM MBean reference guides for each
        release
    -   Foundation/Common
    -   DOORS Next
    -   EWM
    -   LQE - this is an outlier too since we are just using MBeans
        available in Jena
    -   Future add ETM, RMM and other apps as they pub MBeans
-   Within an application domain category, organize the MBeans
    alphabetically. The current organization by collector task is not
    meaningful to end users. Alternatively, if a reasonable functional
    categorization can be defined, that could be considered, e.g.
    cluster, performance, server health, usage, etc. One idea would be
    to group so can tie the elements of the Jazz Service Invocation
    Architecture
    (<https://jazz.net/wiki/bin/view/Deployment/CLMMBeansOverview>) to
    the relevant MBeans.
-   Each release should have release notes that indicate any changes
    (high level) from previous release
    -   Changes to a release should NOT break client monitoring for a
        prior release, e.g. avoid changing object name paths
-   What to capture for each MBean:
    -   Name, Object name/path
    -   Advanced Property Namespace, Advanced Property Display Name,
        Advanced Property ID and their default values and unit of
        measurement (e.g. milliseconds, seconds....)
    -   Description/usage/why of value
    -   Do changes to the MBean or collector task settings require a
        restart?
    -   Default frequency and how to alter in UI and/advanced property
    -   Name of collector task, TaskID used in UI
    -   Attribute names with good descriptions
    -   it would be nice to provide a way to tag MBeans so some
        filtering/searching could be done within the documentation; use
        of Twiki likely prohibits that
    -   see [Serviceability Component MBean
        Mapping](CLM606ServiceabilityComponentMBeanMapping) especially
        the attached table
    -   need to show examples on how to find and use an MBean in the
        Serviceability page, RepoDebug and some monitoring tool, e.g.
        Splunk
    -   under what conditions does the MBean provide data (eg. some
        require a failure for anything to be published)
    -   consider how to tie an MBean to any related usage guidance, when
        available
-   Publishing the MBean reference
    -   in KnowledgeCenter? on deployment wiki? jazz.net?
    -   Websphere Liberty captures their MBeans in KC. For example, see
        [RuntimeUpdateNotificationMBean](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.javadoc.liberty.doc/com.ibm.websphere.appserver.api.basics_1.3-javadoc/com/ibm/websphere/runtime/update/RuntimeUpdateNotificationMBean.html?view=embed)

##### Related topics: [JMX MBeans for ELM application monitoring](JMXMBeans) [related-topics-jmx-mbeans-for-elm-application-monitoring]
