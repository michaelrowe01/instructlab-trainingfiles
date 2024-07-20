META:TOPICINFO{author="syeshin" date="1536800906" format="1.1"
reprev="1.7" version="1.7"} META:TOPICPARENT{name="Common605Beans"}

# ClusterMetricsTask [clustermetricstask]

Build basis: 6.0.5 ENDCOLOR \#TopPage

TOC{title="Managed Beans"}

Clustering has several managed beans for monitoring the overall state of
the distributed system. These beans will display no data until (a)
Clustering is enabled/deployed and (b) the collection interval has
occurred.

# MQTT Endpoint Metrics

This provides information about configured end points with the
MessageSight MQTT broker. It has details like total connections, bytes
read or written, messages sent/received/lost etc.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name]

com.ibm.team.foundation.cluster.mqtt:name=\<\>,
type=mqttEndpointStatistics

### Default Frequency for Publishing [default-frequency-for-publishing]

15 Minutes

### Attributes [attributes]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |
| Enabled | Endpoint is enabled? | Boolean |
| NodeName | Name of the appliance | String |
| TimeStamp | Date and time | Date |
| Name | Name of the endpoint | String |
| TotalConnections | Total number of connections | Long |
| ActiveConnections | Number of currently active connections | Long |
| BadConnections | Number of connections that failed to connect since reset | Long |
| MsgRead | Number of messages that are read since reset | Long |
| MsgWrite | Number of messages that are written since reset | Long |
| BytesRead | Number of bytes read since reset | Long |
| BytesWrite | Number of bytes written since reset | Long |
| LostMessageCount | Number of messages that are lost since reset | Long |
| WarnMessageCount | Warn Message Count | Long |
| ResetTime | Time at which the statistics for the topic were reset | Date |

[Back to top](#TopPage)

# MQTT Memory Metrics

This provides information about the memory characteristics of the
MessageSight MQTT broker machine. It includes details like free memory,
message payloads etc.

### Advanced Property [advanced-property-1]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-1]

com.ibm.team.foundation.cluster.mqtt:name=\<\>, type=mqttMemorytatistics

### Default Frequency for Publishing [default-frequency-for-publishing-1]

15 Minutes

### Attributes [attributes-1]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |
| NodeName | Name of the appliance | String |
| TimeStamp | Date and time | Date |
| MemoryTotalBytes | The total amount of physical memory on IBM MessageSight | Long |
| MemoryFreeBytes | The amount of physical memory that is available | Long |
| MemoryFreePercent | The amount of free memory as a percentage of total physical memory on MQTT Broker | Long |
| ServerVirtualMemoryBytes | The amount of virtual memory that is being used by IBM MessageSight | Long |
| ServerResidentSetBytes | The amount of physical memory that is being used by IBM MessageSight | Long |
| MessagePayloads | The amount of memory that is being consumed by IBM MessageSight for message payloads | Long |
| PublishSubscribe | The amount of memory that is being consumed by IBM MessageSight for publish/subscribe data structures | Long |
| Destinations | The amount of memory that is being consumed by IBM MessageSight for destinations on which messages can be buffered | Long |
| CurrentActivity | The amount of memory that is being consumed by IBM MessageSight for current activity | Long |
| ClientStates | The amount of memory that is being consumed by IBM MessageSight for Client States | Long |

[Back to top](#TopPage)

# MQTT Store Metrics

This provides information about the disk and pool characteristics of the
MessageSight MQTT broker machine.

### Advanced Property [advanced-property-2]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-2]

com.ibm.team.foundation.cluster.mqtt:name=\<\>, type=mqttStoretatistics

### Default Frequency for Publishing [default-frequency-for-publishing-2]

15 Minutes

### Attributes [attributes-2]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |
| NodeName | Name of the appliance | String |
| TimeStamp | Date and time | Date |
| DiskUsedPercent | Specifies the percentage of disk space that is used | Long |
| DiskFreeBytes | Specifies the amount of disk space that is available | Long |
| MemoryUsedPercent | Specifies the percentage of persistent memory that is used, and therefore not available | Long |
| MemoryTotalBytes | Total memory in bytes | Long |
| \*TotalBytes | Pool total bytes | Long |
| \*UsedBytes | Total used bytes by Pool | Long |
| \*UsedPercent | Memory in Percent used by Pool | Long |
| \*RecordsLimitBytes | Pool Records limit in bytes | Long |
| \*RecordsUsedBytes | Pool Records used memory in bytes | Long |

[Back to top](#TopPage)

# MQTT Topic Metrics

This provides information about the topics in the MessageSight MQTT
broker machine. It includes details like subscriptions, published
messages etc.

### Advanced Property [advanced-property-3]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-3]

com.ibm.team.foundation.cluster.mqtt:name=\<\>, type=mqttTopictatistics

### Default Frequency for Publishing [default-frequency-for-publishing-3]

15 Minutes

### Attributes [attributes-3]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |
| NodeName | Name of the appliance | String |
| TimeStamp | Date and time | Date |
| TopicString | The topic that is being monitored. The topic string always contains a wildcard. | String |
| Subscriptions | The number of active subscriptions on the topics that are monitored. The figure shows all active subscriptions that match the wild carded topic string. | Long |
| ResetTime | The time at which the statistics for the topic were reset. The ResetTime is usually the time when the topic monitor is created. | Date |
| PublishedMsgs | The number of messages that are successfully published to a topic that matches the wildcarded topic string. | Long |
| RejectedMsgs | The number of messages that are rejected by one or more subscriptions where the quality of service level did not cause the publish request to fail. | Long |
| FailedPublishes | The number of publish requests that failed because the message is rejected by one or more subscriptions. | Long |

[Back to top](#TopPage)

# Jazz MQTT Service Messages Received Count

This facet captures the count of messages received by the Jazz MQTT
service.

### Advanced Property [advanced-property-4]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-4]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService, facet=Count, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-4]

15 Minutes

### Attributes [attributes-4]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Messages Received Frequency (msgs/sec)

This facet captures the frequency of messages received by the Jazz MQTT
service.

### Advanced Property [advanced-property-5]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-5]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService, facet=Frequency (msg/s), counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-5]

15 Minutes

### Attributes [attributes-5]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Messages Received Reset Counter

This facet captures the count of reset messages received by the Jazz
MQTT service.

### Advanced Property [advanced-property-6]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-6]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService, facet=Reset, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-6]

15 Minutes

### Attributes [attributes-6]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Messages Sent Count

This facet captures the count of messages sent by the Jazz MQTT service.

### Advanced Property [advanced-property-7]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-7]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService, facet=Count, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-7]

15 Minutes

### Attributes [attributes-7]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Messages Sent Frequency (msgs/sec)

This facet captures the frequency of messages sent by the Jazz MQTT
service.

### Advanced Property [advanced-property-8]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-8]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService, facet=Frequency (msg/s), counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-8]

15 Minutes

### Attributes [attributes-8]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Messages Sent Reset Counter

This facet captures the count of reset messages sent by the Jazz MQTT
service.

### Advanced Property [advanced-property-9]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-9]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService, facet=Reset, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-9]

15 Minutes

### Attributes [attributes-9]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Messages Sent Queued Counter

This facet captures the count of queued messages to be sent by the Jazz
MQTT service.

### Advanced Property [advanced-property-10]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-10]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService, facet=Queued, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-10]

15 Minutes

### Attributes [attributes-10]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Messages Received Queue Exhausted Counter

This facet captures the count of times when the thread pool size to
process received messages has maxed out and the queue to hold excess is
full.

### Advanced Property [advanced-property-11]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-11]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService, facet=Queue Exhausted, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-11]

15 Minutes

### Attributes [attributes-11]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Published Messages Lost Count

This facet captures the count of published messages that got lost and
did not make it to the broker.

### Advanced Property [advanced-property-12]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-12]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService Stats, facet=Send Success rate, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-12]

15 Minutes

### Attributes [attributes-12]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Message Processing Time

This facet captures the average processing time for handling messages
received by the Jazz MQTT service.

### Advanced Property [advanced-property-13]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-13]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService Stats, facet=Elapsed time in seconds, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-13]

15 Minutes

### Attributes [attributes-13]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Message Sent Result - Success

This facet captures the count of published messages that were
successfully delivered to the broker.

### Advanced Property [advanced-property-14]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-14]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService Stats, facet=Send Success rate, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-14]

15 Minutes

### Attributes [attributes-14]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Message Sent Result - Failure

This facet captures the count of published messages that failed to be
delivered to the broker.

### Advanced Property [advanced-property-15]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-15]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService Stats, facet=Send Success rate, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-15]

15 Minutes

### Attributes [attributes-15]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Message processed on main thread

This facet captures the count of received messages that were processed
on the main thread in the Jazz MQTT Service as the service was being
deactivated and also when the threadpool and the queue to use for
holding tasks before they are executed were exhausted.

### Advanced Property [advanced-property-16]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-16]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService Stats, facet=Send Success rate, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-16]

15 Minutes

### Attributes [attributes-16]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Received Messages - Queue Size

This facet captures the size of the queue in MQTT service used to hold
incoming messages before a background thread becomes available to
process them.

### Advanced Property [advanced-property-17]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-17]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService Stats, facet=Arrived Messages Processing,
counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-17]

15 Minutes

### Attributes [attributes-17]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Received Messages thread pool size

This facet captures the size of the thread pool used to handle the
incoming messages by the Jazz MQTT service. The excess messages will be
held in queue.

### Advanced Property [advanced-property-18]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-18]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService Stats, facet=Arrived Messages Processing,
counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-18]

15 Minutes

### Attributes [attributes-18]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Failed connections to broker

This facet captures the count of failed connections to the broker from
the Jazz MQTT service.

### Advanced Property [advanced-property-19]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-19]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService Client Stats, facet=Failed to connect, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-19]

15 Minutes

### Attributes [attributes-19]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Jazz MQTT Service Lost connections to broker

This facet captures the count of lost connections to the broker from the
Jazz MQTT service.

### Advanced Property [advanced-property-20]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-20]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=MqttService Client Stats, facet=Connection lost, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-20]

15 Minutes

### Attributes [attributes-20]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |

**Missing Attributes**

[Back to top](#TopPage)

# Distributed Data Microservice Key Size

Facet reports the size of the object used as a map Key.

### Advanced Property [advanced-property-21]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-21]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=Distributed Maps and Values Sizes, facet=Key Size, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-21]

15 Minutes

### Attributes [attributes-21]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# Distributed Data Microservice Added Value Size

This facet reports the size of the data help in the map.

### Advanced Property [advanced-property-22]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-22]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=Distributed Maps and Values Sizes, facet=Added Value Size,
counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-22]

15 Minutes

### Attributes [attributes-22]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# Distributed Data Microservice Number of Elements in Map

This facet reports the number of elements in the map.

### Advanced Property [advanced-property-23]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-23]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=Distributed Maps and Values Sizes, facet=Number of Elements in
Map, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-23]

15 Minutes

### Attributes [attributes-23]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# Distributed Data Microservice Bytes transferred (in kb)

This facet reports the size of data (in KB) transferred between
persistence layer and distributed maps in memory.

### Advanced Property [advanced-property-24]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-24]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=Distributed Persistence Layer, facet=Bytes transferred (in kb),
counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-24]

15 Minutes

### Attributes [attributes-24]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# Distributed Data Microservice Elapsed time (in ms)

This facet reports the times it takes for the data transfers to and from
the persistence layer.

### Advanced Property [advanced-property-25]

You enable this bean by setting **Enable Cluster Metrics Mbean** to
**true**

### Object Name [object-name-25]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
Distributed Persistence Layer, facet=Elapsed time (in ms),
counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-25]

15 Minutes

### Attributes [attributes-25]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
