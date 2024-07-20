META:TOPICINFO{author="toobaahmed" date="1541135473" format="1.1"
version="1.4"} META:TOPICPARENT{name="Common605Beans"}

# HighFrequencyMetricsNodeScopedTask [highfrequencymetricsnodescopedtask]

Build basis: 6.0.5 ENDCOLOR

TOC{title="Managed Beans"}

# Active Services

This is all the active services currently running in the server. Each
service provides information like service name, requested user, start
time and duration, and start time. This is useful to understand the
standard patterns of low level service activity in a production system.
Helps to understand the unique set of users currently working in the
system.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Active Services MBean** to
**true**

### Object Name [object-name]

com.ibm.team.foundation.activeservices:name=\<\>,
type=activeServicesMetrics, serviceName=\*

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
| scenarioName | This is the name of scenario this active service is associated with | String |
| scenarioId | This is a unique scenario instance id this active service is associated with | String |
| serviceName | This is the name of this active service | String |
| serviceId | The id of this active service | String |
| startTime | This is the start time of this active service in milliseconds | Long |
| duration | This is the total time this active service has been running since it started. This is the current time when the snapshot was taken minus the start time. This is reported in milliseconds | Long |
| serviceMethod | This is name of the service method | String |
| userName | This is name of the user who initiated this service | String |
| userId | This is id of the user who initiated this service | String |
| threadName | This is the name of the java thread executing this service | String |
| threadId | This is id of the java thread executing this service | Long |

[Back to top](#TopPage)

# Active Services Summary

This is a summary of the total count of active services running in the
system. This provides information like total count, CPU ratio and
services that have exceeded duration thresholds. This is useful to
understand the active services that are long running. Helps also to
understand if the system specifications are adequate to meet the user
load.

### Advanced Property [advanced-property-1]

You enable this bean by setting **Enable Active Services Mbean** to
**true**

### Object Name [object-name-1]

com.ibm.team.foundation.activeservices:name=\<\>,
type=activeServicesSummaryMetrics

### Default Frequency for Publishing [default-frequency-for-publishing-1]

30 Seconds

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
| totalCount | This is the total number of active services currently running | Long |
| countExceedingThresholdDuration | This is a number of actives services whose execution duration has exceeded the threshold | Long |
| longestDuration | This indicates how long has the longest active service been running in milliseconds | Long |
| cpuRatio | Count of active services divided by the number of processors on the server | Double |
| thresholdDuration | This is duration in milliseconds used for identifying the services who have exceeded the threshold | Long |

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
