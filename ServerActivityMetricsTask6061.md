META:TOPICINFO{author="zz00tc" date="1543490693" format="1.1"
version="1.5"} META:TOPICPARENT{name="Common6061Beans"}

# ServerActivityMetricsTask [serveractivitymetricstask]

Build basis: 6.0.6.1 ENDCOLOR \#TopPage

TOC{title="Managed Beans"}

# Server Activity Summary Metrics MBean

Publish the server activity (active users count, active services count,
etc.) during the specified interval as a MBean. This is useful to
understand the usage and load patterns in a production system.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Server Activity Metrics MBean**
to **true**

### Object Name [object-name]

com.ibm.team.foundation.serveractivity:name=\<\>,
type=serverActivitySummaryMetrics

### Default Frequency for Publishing [default-frequency-for-publishing]

10 minutes

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
| activeUsersCount | This is the total number of active users during the specified interval | Long |
| activeServicesCount | This is a total number of actives services during the specified interval | Long |
| activityInterval | This indicates the duration of the interval in seconds | Long |
| userWithMostServicesInInterval | This is the user with the most active services during the interval | String |

[Back to top](#TopPage)

# Active Service Counter Metrics MBean Captures the response time for service methods

### Advanced Property [advanced-property-1]

You enable this bean by setting **Enable Active Service Counter Metrics
MBean** to **true**

### Object Name [object-name-1]

com.ibm.team.foundation.counter:name=\<\>, type=counterMetrics,
group=activeServices, facet=\<\>, counterName=\<\>

### Default Frequency for Publishing [default-frequency-for-publishing-1]

10 minutes

### Attributes [attributes-1]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| averageOverInterval | This is the average value of the range counter for this collection time interval | Double |
| component | This represents the component name associated with this web service. Value of UnKnown is returned if component name cannot be derived | String |
| contextRoot | This is the application root context for the CLM application | String |
| countOverInterval | This is the count for this collection time interval | Long |
| domain | This is the namespace for the application under which the MBean data is published | String |
| facet | This represents a particular aspect of this counter | String |
| group | This is the group that the counter belongs to | String |
| host | This is the host name where the CLM application is running | String |
| id | This represents a unique id for this counter | String |
| intervalDuration | This is the collection time interval in seconds | Double |
| mbeanCreationTimestamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| name | This is the name of specific counter | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | Integer |
| stdDev | This is the standard deviation value of the range counter | Double |
| totalOverInterval | This is the total value of the range counter for this collection time interval | Double |
| transactionRate | This is the transaction rate (countover interval/interval duration) in counts per second | Double |

[Back to top](#TopPage)

# Active Services Counter Summary Metrics

Captures the response time for service methods and reports by component
and across all components

### Advanced Property [advanced-property-2]

You enable this bean by setting **Enable Active Service Counter Metrics
MBean** to **true**

### Object Name [object-name-2]

com.ibm.team.foundation.activeservices:name=\<\>,
type=activeServicesCounterSummaryMetrics, facet=\<\>, component=\<\>

### Default Frequency for Publishing [default-frequency-for-publishing-2]

10 minutes

### Attributes [attributes-2]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimestamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |
| averageOverInterval | This is the average value across all range counters for this collection time interval | Double |
| component | This represents the component name associated with this active service summary. Value of Unknown is returned if component name cannot be derived | String |
| countOverInterval | This is the total count across all range counters for this collection time interval | Long |
| facet | This represents a particular aspect of this summary | String |
| group | This is the group that this counter summary belongs to | String |
| intervalDuration | This is the collection time interval in seconds | Double |
| maxOverInterval | This is the maximum average value across all range counters for this collection time interval | Double |
| totalOverInterval | This is the total value across all range counters for this collection time interval | Double |
| transactionRate | This is the transaction rate (countover interval/interval duration) in counts per second | Double |

[Back to top](#TopPage)

##### Related topics: [Common Managed Beans](Common606Beans) [related-topics-common-managed-beans]
