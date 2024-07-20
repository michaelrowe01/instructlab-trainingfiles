META:TOPICINFO{author="sbeard" date="1589970730" format="1.1"
version="1.7"} META:TOPICPARENT{name="Common605Beans"}

# LicenseMetricsCollectorTask [licensemetricscollectortask]

Build basis: 6.0.5 ENDCOLOR \#TopPage

TOC{title="Managed Beans"}

# Floating license consumption statistics Concurrent use

This facet captures the floating license consumption from the servers.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable License Consumption Metrics
MBean** to **true**

### Object Name [object-name]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=Floating license concurrent use, facet=All servers, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing]

15 minutes

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# Floating license consumption statistics License checkout time

This facet captures the floating license checkout time from the servers.

### Advanced Property [advanced-property-1]

You enable this bean by setting **Enable License Consumption Metrics
MBean** to **true**

### Object Name [object-name-1]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=Floating license checkout time, facet=All servers, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-1]

15 minutes

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| count | This is the current total count of the range counter samples | Long |
| total | This is the total value of all the range counter samples | Double |
| min | This is the minimum value of the range counter | Double |
| max | This is the maximum value of the range counter | Double |
| average | This is the average value of the range counter | Double |
| averageOverInterval | This is the average value of the range counter for this collection time interval | Double |
| totalOverInterval | This is the total value of the range counter for this collection time interval | Double |
| countOverInterval | This is the count for this collection time interval | Long |
| intervalDuration | This is the collection time interval in seconds | Double |
| transactionRate | This is the transaction rate (countover interval/interval duration) in counts per second | Double |
| stdDev | This is the standard deviation value of the integral range counter | Long |

[Back to top](#TopPage)

# Floating license consumption statistics License Denials

This publishes the basic node information for each node in the cluster
and also the node state.

### Advanced Property [advanced-property-2]

You enable this bean by setting **Enable License Consumption Metrics
Mbean** to **true**

**NOTE:** This Mbean does not appear until you have any license denials.

### Object Name [object-name-2]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=Floating license denials, facet=All servers, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-2]

15 minutes

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# Token License consumption statistics Concurrent use

This facet captures the token license consumption from the servers.

### Advanced Property [advanced-property-3]

You enable this bean by setting **Enable License Consumption Metrics
MBean** to **true**

### Object Name [object-name-3]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics, group=
License token use, facet=All providers, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-3]

15 minutes

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# Token License consumption statistics License Denials

This facet captures the token license denials from the providers.

### Advanced Property [advanced-property-4]

You enable this bean by setting **Enable License Consumption Metrics
Mbean** to **true**

**NOTE:** This Mbean does not appear until you have any license denials.

### Object Name [object-name-4]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics, group=
License token provider denials, facet=All providers, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-4]

15 minutes

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# Client compatibility with server statistics: Compatible client logins

This facet captures the number of login attempts from different versions
of the client.

### Advanced Property [advanced-property-5]

You enable this bean by setting **Enable Compatible Client Logins
MBean** to **true**

### Object Name [object-name-5]

com.ibm.team.foundation.counters:name=\<\< contextRoot\>\>,
type=counterMetrics, group= Compatible client logins, facet=Number of
logins, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-5]

15 minutes

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
