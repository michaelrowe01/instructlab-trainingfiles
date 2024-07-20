META:TOPICINFO{author="toobaahmed" date="1541135800" format="1.1"
version="1.2"} META:TOPICPARENT{name="Common606Beans"}

# HighFrequencyMetricsNodeScopedTask [highfrequencymetricsnodescopedtask]

Build basis: 6.0.6 ENDCOLOR

TOC{title="Page contents"}

# MQTTBrokerSubscriptionStatsMBean

Description

## Advanced Property [advanced-property]

You enable this bean by setting **Enable MQTT Broker Metrics Mbean** to
**true**

## Syntax [syntax]

com.ibm.team.foundation.clustering:name=\<\>,
type=MQTTBrokerSubscriptionMetrics,subscriptionName=\<\>

## Frequency: 30 Seconds [frequency-30-seconds]

## Attributes [attributes]

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
| subscriptionName | The name of the subscription | String |
| clusterName | The name of the cluster in which the application is running. | String |
| bufferedPercent | The percentage of the maximum buffered messages that the current buffered messages represent. | Double |
| bufferedMessages | The number of published messages that are waiting to be sent to clients. | Long |
| rejectedMessages | The number of messages that are rejected because the maximum number of buffered messages was reached when the messages were published to the subscription. | Long |
| discardedMessages | The number of messages that are not delivered because they were discarded when the buffer became full.. | Long |
| intervalDuration | This is the collection time interval in seconds. | Integer |

##### Related topics: [Common Managed Beans](Common606Beans) [related-topics-common-managed-beans]
