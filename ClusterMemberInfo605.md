META:TOPICINFO{author="rwatts" date="1531903793" format="1.1"
reprev="1.1" version="1.1"} META:TOPICPARENT{name="Common605Beans"}

# CommonMetricsCollectorTask [commonmetricscollectortask]

Build basis: 6.0.5 ENDCOLOR

TOC{title="Page contents"}

# This page is under construction [this-page-is-under-construction]

## Cluster Member Information

This publishes the basic node information for each node in the cluster
and also the node state.

## Advanced Property [advanced-property]

You enable this bean by setting \[Advanced Property\] to **true**

## Syntax [syntax]

com.ibm.team.foundation.clustermembers:name=\<\>,
type=clusterMemberDataMetrics, nodeId=\*

## Frequency: 60 minutes [frequency-60-minutes]

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
| nodeURL | This is the URL for the specified node id | String |
| nodeState | This is state of the node id. Values are INACTIVE=0, STALE=1 and ACTIVE=2 | Integer |

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
