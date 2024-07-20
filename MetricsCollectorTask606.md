META:TOPICINFO{author="toobaahmed" date="1538129300" format="1.1"
version="1.4"} META:TOPICPARENT{name="Common606Beans"}

# MetricsCollectorTask [metricscollectortask]

Build basis: 6.0.6 ENDCOLOR \#TopPage

TOC{title="Managed Beans"}

# Enable Configuration Management Service Metrics MBean

Description

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Error Details Mbean** to
**true**

### Object Name [object-name]

com.ibm.team.foundation.logevents:name=\<\>,
type=logEventDetailsMetrics, errorNameAndId=\*

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

[Back to top](#TopPage)

# Local configuration management cache statistics Cache hit ratio

This is useful to understand how the caches are performing. In a
production environment the hit ratio of the caches should be greater
than 95 ([Blog](https://blog.stackpath.com/glossary/cache-hit-ratio/)).
Other facets are Entry added to cache, Entry removed from cache, Entry
found in cache, Entry not found in cache, Entry replaced in cache and
Entry garbage collected from cache.

### Advanced Property [advanced-property-1]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-1]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Cache hit ratio as a
percentage, counterName=\*

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
| min | This is the minimum value of the range counter | Long |
| max | This is the maximum value of the range counter | Long |
| count | This is the current total count of the range counter samples | Long |
| total | This is the total value of all the range counter samples | Double |
| average | This is the average value of the range counter | Double |
| averageOverInterval | This is the average value of the range counter for this collection time interval | Double |
| totalOverInterval | This is the total value of the range counter for this collection time interval | Double |
| countOverInterval | This is the count for this collection time interval | Long |
| intervalDuration | This is the collection time interval in seconds | Double |
| transactionRate | This is the transaction rate (countover interval/interval duration) in counts per second | Double |
| stdDev | This is the standard deviation value of the integral range counter | Long |

[Back to top](#TopPage)

# Local configuration management cache statistics Entry added to cache

This is useful to understand how the caches are performing. In a
production environment the hit ratio of the caches should be greater
than 95 ([Blog](https://blog.stackpath.com/glossary/cache-hit-ratio/)).
This facet highlights the entries added to the cache

### Advanced Property [advanced-property-2]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-2]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Entry added to cache,
counterName=\*

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

# Local configuration management cache statistics Entry found in cache

This is useful to understand how the caches are performing. In a
production environment the hit ratio of the caches should be greater
than 95 ([Blog](https://blog.stackpath.com/glossary/cache-hit-ratio/)).
This facet highlights the entries found in cache.

### Advanced Property [advanced-property-3]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-3]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Entry found in cache,
counterName=\*

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

# Local configuration management cache statistics Entry not found in cache

This is useful to understand how the caches are performing. In a
production environment the hit ratio of the caches should be greater
than 95 ([Blog](https://blog.stackpath.com/glossary/cache-hit-ratio/)).
This facet highlights the entries not found in cache

### Advanced Property [advanced-property-4]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-4]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Entry not found in
cache, counterName=\*

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

# Local configuration management cache statistics Entry removed from cache

This is useful to understand how the caches are performing. In a
production environment the hit ratio of the caches should be greater
than 95 ([Blog](https://blog.stackpath.com/glossary/cache-hit-ratio/)).
This facet highlights the entries removed from cache

### Advanced Property [advanced-property-5]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-5]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Entry removed from
cache, counterName=\*

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

# Local configuration management cache statistics Entry replaced in cache

This is useful to understand how the caches are performing. In a
production environment the hit ratio of the caches should be greater
than 95 ([Blog](https://blog.stackpath.com/glossary/cache-hit-ratio/)).
This facet highlights the entries replaced in cache

### Advanced Property [advanced-property-6]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-6]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Entry replaced in cache,
counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-6]

15 minutes

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# Local configuration management cache statistics Entry garbage collected from cache

This is useful to understand how the caches are performing. In a
production environment the hit ratio of the caches should be greater
than 95 ([Blog](https://blog.stackpath.com/glossary/cache-hit-ratio/)).
This facet highlights the entries garbage collected from cache.

### Advanced Property [advanced-property-7]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-7]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Entry garbage collected
from cache, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-7]

15 minutes

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# Local configuration management cache statistics Time for computing a value in ms

This is useful to understand how the caches are performing. In a
production environment the hit ratio of the caches should be greater
than 95 ([Blog](https://blog.stackpath.com/glossary/cache-hit-ratio/)).
This facet highlights the average time to compute a value in ms.

### Advanced Property [advanced-property-8]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-8]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Time for computing a
value in ms, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-8]

15 minutes

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| min | This is the minimum value of the range counter | Long |
| max | This is the maximum value of the range counter | Long |
| count | This is the current total count of the range counter samples | Long |
| total | This is the total value of all the range counter samples | Double |
| average | This is the average value of the range counter | Double |
| averageOverInterval | This is the average value of the range counter for this collection time interval | Double |
| totalOverInterval | This is the total value of the range counter for this collection time interval | Double |
| countOverInterval | This is the count for this collection time interval | Long |
| intervalDuration | This is the collection time interval in seconds | Double |
| transactionRate | This is the transaction rate (countover interval/interval duration) in counts per second | Double |
| stdDev | This is the standard deviation value of the integral range counter | Long |

[Back to top](#TopPage)

# Web Services Statistics Summary Over Collection Intervals

This bean captures the summary information over collection intervals.
The summary includes total count, average over interval, max over
interval, transaction rate, the total value over interval etc. The
summary bean is create by facet and within each facet you can get a
summary by component.

### Advanced Property [advanced-property-9]

You enable this bean by setting **Enable Web Service Metrics MBean** to
**true**

### Object Name [object-name-9]

com.ibm.team.foundation.webservices:name=\<\>, type=webServicesSummary
Metrics, facet=**, component=**

### Default Frequency for Publishing [default-frequency-for-publishing-9]

15 minutes

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
| group | This is the group that this counter summary belongs to | String |
| facet | This represents a particular aspect of this summary | String |
| component | This represents the component name associated with this web service summary. Value of UnKnown is returned if component name cannot be derived | String |
| averageOverInterval | This is the average value across all range counters for this collection time interval UPDATED in 6.0.6 | Double |
| maxOverInterval | This is the maximum average value across all range counters for this collection time interval | Double |
| totalOverInterval | This is the total value across all range counters for this collection time interval | Double |
| countOverInterval | This is the total count across all range counters for this collection time interval | Double |
| intervalDuration | This is the collection time interval in seconds | Double |
| transactionRate | This is the transaction rate (countover interval/interval duration) in counts per second | Double |

[Back to top](#TopPage)

##### Related topics: [Common Managed Beans](Common606Beans) [related-topics-common-managed-beans]
