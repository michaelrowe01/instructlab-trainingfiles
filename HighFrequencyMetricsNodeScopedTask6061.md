META:TOPICINFO{author="zz00tc" date="1543318194" format="1.1"
version="1.3"} META:TOPICPARENT{name="Common6061Beans"}

# HighFrequencyMetricsNodeScopedTask [highfrequencymetricsnodescopedtask]

Build basis: 6.0.6.1 ENDCOLOR

TOC{title="Page contents"}

# Active Services Summary

This is a summary of the total count of active services running in the
system. This provides information like total count, CPU ratio and
services that have exceeded duration thresholds. This is useful to
understand the active services that are long running. Helps also to
understand if the system specifications are adequate to meet the user
load.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Active Services Mbean** to
**true**

### Object Name [object-name]

com.ibm.team.foundation.activeservices:name=\<\>,
type=activeServicesSummaryMetrics

### Default Frequency for Publishing [default-frequency-for-publishing]

30 Seconds

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
| totalCount | This is the total number of active services currently running | Long |
| countExceedingThresholdDuration | This is a number of actives services whose execution duration has exceeded the threshold | Long |
| longestDuration | This indicates how long has the longest active service been running in milliseconds | Long |
| cpuRatio | Count of active services divided by the number of processors on the server | Double |
| thresholdDuration | This is duration in milliseconds used for identifying the services who have exceeded the threshold | Long |
| thresholdDuration | This is duration in milliseconds used for identifying the services who have exceeded the threshold | Long |
| concurrentUsers | This is total number of concurrent users at the time the bean was created | Long |

##### Related topics: [Common Managed Beans](Common606Beans) [related-topics-common-managed-beans]
