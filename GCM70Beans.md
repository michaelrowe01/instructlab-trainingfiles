META:TOPICINFO{author="tfeeney" date="1590770343" format="1.1"
reprev="1.6" version="1.6"} META:TOPICPARENT{name="MBeansReference"}

# Global Configuration Management (GCM) application MBeans for ELM 7.x DKGRAY Authors: David Honey, Tom Poulin, Main.TimFeeney Build basis: 7.0, 7.0.1 [global-configuration-management-gcm-application-mbeans-for-elm-7.x-dkgray-authors-david-honey-tom-poulin-main.timfeeney-build-basis-7.0-7.0.1]

ENDCOLOR

TOC{title="Page contents"}

In ELM 7.0, GCM introduced basic metrics and statistics on the usage of
GCM to guide deployment, best practices and recommendations for usage.
This information is available via a metrics page on the GCM UI and JMX
MBeans visible through [MBean Utilities](MXBeanUtilities) or an
enterprise monitoring tool.

Formal documentation of the GCM MBeans is not yet available. In the mean
time, this page provides some temporary documentation for the MBeans.
For more information, see [495434: Provide basic GC
metrics](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/495434)
which provided the original capability and [506795: document existing
GCM
metrics](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/506795)
which is tracking the documentation to be provided.

The metrics are provided per project area and across all project areas
(in same GCM repository). Types of metrics include:

-   Size and composition of global configuration (GC) trees
-   Number of global components and GCs (by type)
-   Counts of GC, local configuration (LC), and external GC
    contributions

### Advanced Property [advanced-property]

There are two steps needed to provide regularly updated metrics via an
MBean. First, the metrics need to be collected and second the metrics
need to be published in the requisite MBean.

To enable periodic collection of the metrics, set **"Enable periodic GC
metrics collection"** to **true** on the GCM Serviceability tab
(*https://hostname:port/gc/admin#action=com.ibm.team.repository.admin.serviceability*)
and set the collection frequency or schedule. Note that metrics
collection can be invoked on demand as well from the Global
Configuration Metrics page (*https://hostname:port/gc/metrics*) page. GC
metrics data persists in the repository between restarts.

To enable publishing of the metrics to an MBean, set **"Enable GC
metrics MBean"** to **true** on the GCM Serviceability tab and set the
collection frequency or schedule. Note the default for this property is
**true**. If metrics collection is disabled, the MBean will be populated
with the metrics from the last collection, which may be nothing if the
collection has never been run.

### Object Name [object-name]

com.ibm.team.gc.application:name=\<\>,
type=globalConfigurationsAndComponents, scope=projectArea,
projectAreaName=\<\>, projectAreaUri=\<\>

or

com.ibm.team.gc.application:name=\<\>,
type=globalConfigurationsAndComponents, scope=allActiveProjectAreas

### Default Frequency [default-frequency]

-   24 hours for metrics collection
    (com.ibm.team.gc.service.metrics.GcMetricsCollectorTask)
-   15 seconds before publication of saved GC metrics after startup
    (com.ibm.team.gc.service.metrics.GcMetricsPublishSavedMetricsOnStartupTask)

### Attributes [attributes]

The following is a **sample** list of GCM MBean attributes when
scope=projectArea for a test project area called "JKE Banking (Global
Configuration)"

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| computationEndTime | The time when computation of metrics completed | Timestamp |
| contextRoot | This is the application root context for the CLM application | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| hierarchyMaximumDepth | The The maximum depth of any GC hierarchy for project area "JKE Banking (Global Configuration)" | Integer |
| hierarchyMaximumDepth.rootGC.name | The name of a root GC that has the The maximum depth of any GC hierarchy for project area "JKE Banking (Global Configuration)" | String |
| hierarchyMaximumDepth.rootGC.uri | The URI of a root GC that has the The maximum depth of any GC hierarchy for project area "JKE Banking (Global Configuration)" | String |
| hierarchyMaximumNumberOfExternalGlobalConfigurations | The maximum number of external global configurations of any GC hierarchy for project area "JKE Banking (Global Configuration)" | Integer |
| hierarchyMaximumNumberOfExternalGlobalConfigurations.rootGC.name | The name of a root GC that has the The maximum number of external global configurations of any GC hierarchy for project area "JKE Banking (Global Configuration)" | String |
| hierarchyMaximumNumberOfExternalGlobalConfigurations.rootGC.uri | The URI of a root GC that has the The maximum number of external global configurations of any GC hierarchy for project area "JKE Banking (Global Configuration)" | String |
| hierarchyMaximumNumberOfGlobalConfigurationsInThisServer | The The maximum number of global configurations hosted by this server in any GC hierarchy for project area "JKE Banking (Global Configuration)" | Integer |
| hierarchyMaximumNumberOfGlobalConfigurationsInThisServer.rootGC.name | The name of a root GC that has the The maximum number of global configurations hosted by this server in any GC hierarchy for project area "JKE Banking (Global Configuration)" | String |
| hierarchyMaximumNumberOfGlobalConfigurationsInThisServer.rootGC.uri | The URI of a root GC that has the The maximum number of global configurations hosted by this server in any GC hierarchy for project area "JKE Banking (Global Configuration)" | String |
| hierarchyMaximumNumberOfNonGlobalConfigurations | The maximum number of non-global configuration of any GC hierarchy for project area "JKE Banking (Global Configuration)" | Integer |
| hierarchyMaximumNumberOfNonGlobalConfigurations.rootGC.name | The name of a root GC that has the The maximum number of non-global configuration of any GC hierarchy for project area "JKE Banking (Global Configuration)" | String |
| hierarchyMaximumNumberOfNonGlobalConfigurations.rootGC.uri | The URI of a root GC that has the The maximum number of non-global configuration of any GC hierarchy for project area "JKE Banking (Global Configuration)" | String |
| hierarchyMaximumSize | The maximum size of any GC hierarchy for project area "JKE Banking (Global Configuration)" | Integer |
| hierarchyMaximumSize.rootGC.name | The name of a root GC that has the The maximum size of any GC hierarchy for project area "JKE Banking (Global Configuration)" | String |
| hierarchyMaximumSize.rootGC.uri | The URI of a root GC that has the The maximum size of any GC hierarchy for project area "JKE Banking (Global Configuration)" | String |
| hierarchyMaximumWidth | The maximum width of any GC hierarchy for project area "JKE Banking (Global Configuration)" | Integer |
| hierarchyMaximumWidth.rootGC.name | The name of a root GC that has the The maximum width of any GC hierarchy for project area "JKE Banking (Global Configuration)" | String |
| hierarchyMaximumWidth.rootGC.uri | The URI of a root GC that has the The maximum width of any GC hierarchy for project area "JKE Banking (Global Configuration)" | String |
| host | This is the host name where the CLM application is running | String |
| mbeanCreationTimestamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| numberOfContributionsFromExternalGlobalConfigurations | The number of contributions to unarchived global configurations from external global configurations for project area "JKE Banking (Global Configuration)" | Integer |
| numberOfContributionsFromGlobalConfigurationsInThisServer | The number of contributions to unarchived global configurations from global configurations in this server for project area "JKE Banking (Global Configuration)" | Integer |
| numberOfContributionsFromNonGlobalConfigurations | The number of contributions to unarchived global configurations from non global configurations for project area "JKE Banking (Global Configuration)" | Integer |
| numberOfUnarchivedGlobalBaselines | The number of unarchived global baselines for project area "JKE Banking (Global Configuration)" | Integer |
| numberOfUnarchivedGlobalBaselineStagingStreams | The number of unarchived global baseline staging streams for project area "JKE Banking (Global Configuration)" | Integer |
| numberOfUnarchivedGlobalComponents | The number of unarchived global components for project area "JKE Banking (Global Configuration)" | Integer |
| numberOfUnarchivedGlobalConfigurations | The number of unarchived global configurations for project area "JKE Banking (Global Configuration)" | Integer |
| numberOfUnarchivedGlobalPersonalStreams | The number of unarchived global personal streams for project area "JKE Banking (Global Configuration)" | Integer |
| numberOfUnarchivedGlobalSharedStreams | The number of unarchived global shared streams for project area "JKE Banking (Global Configuration)" | Integer |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | Integer |
| projectArea.name | The name of the project area for the metrics | String |
| projectArea.uri | The URI of the project area for the metrics | String |

The following is a **sample** list of GCM MBean attributes when
scope=allActiveProjectAreas

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| computationEndTime | The time when computation of metrics completed | Timestamp |
| contextRoot | This is the application root context for the CLM application | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| hierarchyMaximumDepth | The The maximum depth of any GC hierarchy | Integer |
| hierarchyMaximumDepth.rootGC.name | The name of a root GC that has the The maximum depth of any GC hierarchy | String |
| hierarchyMaximumDepth.rootGC.uri | The URI of a root GC that has the The maximum depth of any GC hierarchy | String |
| hierarchyMaximumNumberOfExternalGlobalConfigurations | The The maximum number of external global configurations of any GC hierarchy | Integer |
| hierarchyMaximumNumberOfExternalGlobalConfigurations.rootGC.name | The name of a root GC that has the The maximum number of external global configurations of any GC hierarchy | String |
| hierarchyMaximumNumberOfExternalGlobalConfigurations.rootGC.uri | The URI of a root GC that has the The maximum number of external global configurations of any GC hierarchy | String |
| hierarchyMaximumNumberOfGlobalConfigurationsInThisServer | The The maximum number of global configurations hosted by this server in any GC hierarchy | Integer |
| hierarchyMaximumNumberOfGlobalConfigurationsInThisServer.rootGC.name | The name of a root GC that has the The maximum number of global configurations hosted by this server in any GC hierarchy | String |
| hierarchyMaximumNumberOfGlobalConfigurationsInThisServer.rootGC.uri | The URI of a root GC that has the The maximum number of global configurations hosted by this server in any GC hierarchy | String |
| hierarchyMaximumNumberOfNonGlobalConfigurations | The The maximum number of non-global configuration of any GC hierarchy | Integer |
| hierarchyMaximumNumberOfNonGlobalConfigurations.rootGC.name | The name of a root GC that has the The maximum number of non-global configuration of any GC hierarchy | String |
| hierarchyMaximumNumberOfNonGlobalConfigurations.rootGC.uri | The URI of a root GC that has the The maximum number of non-global configuration of any GC hierarchy | String |
| hierarchyMaximumSize | The The maximum size of any GC hierarchy | Integer |
| hierarchyMaximumSize.rootGC.name | The name of a root GC that has the The maximum size of any GC hierarchy | String |
| hierarchyMaximumSize.rootGC.uri | The URI of a root GC that has the The maximum size of any GC hierarchy | String |
| hierarchyMaximumWidth | The The maximum width of any GC hierarchy | Integer |
| hierarchyMaximumWidth.rootGC.name | The name of a root GC that has the The maximum width of any GC hierarchy | String |
| hierarchyMaximumWidth.rootGC.uri | The URI of a root GC that has the The maximum width of any GC hierarchy | String |
| host | This is the host name where the CLM application is running | String |
| mbeanCreationTimestamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| numberOfContributionsFromExternalGlobalConfigurations | The number of contributions to unarchived global configurations from external global configurations | Integer |
| numberOfContributionsFromGlobalConfigurationsInThisServer | The number of contributions to unarchived global configurations from global configurations in this server | Integer |
| numberOfContributionsFromNonGlobalConfigurations | The number of contributions to unarchived global configurations from non global configurations | Integer |
| numberOfUnarchivedGlobalBaselines | The number of unarchived global baselines | Integer |
| numberOfUnarchivedGlobalBaselineStagingStreams | The number of unarchived global baseline staging streams | Integer |
| numberOfUnarchivedGlobalComponents | The number of unarchived global components | Integer |
| numberOfUnarchivedGlobalConfigurations | The number of unarchived global configurations | Integer |
| numberOfUnarchivedGlobalPersonalStreams | The number of unarchived global personal streams | Integer |
| numberOfUnarchivedGlobalSharedStreams | The number of unarchived global shared streams | Integer |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | Integer |

##### Related topics: [JMX MBeans for ELM application monitoring](JMXMBeans) [related-topics-jmx-mbeans-for-elm-application-monitoring]
