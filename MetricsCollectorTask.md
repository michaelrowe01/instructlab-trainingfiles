META:TOPICINFO{author="toobaahmed" date="1539920733" format="1.1"
version="1.9"} META:TOPICPARENT{name="Common605Beans"}

# MetricsCollectorTask [metricscollectortask]

Build basis: 6.0.5 ENDCOLOR

TOC{title="Managed Beans"}

\#TopPage

# Log Events

This provides all the errors and warnings from the log files and for
each log entry provides additional contextual information like userd id,
active configuration, servlet request URL etc. This is useful to
understand error log entries occurring in the system when other aspects
of the system are misbehaving. This provides a maximum of 1000 entries
during the collection interval.

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
| contributorId | This is the id of the user who initiated a request that caused this error | String |
| accessedUrl | This is the URL accessed in the system when this error occurred | String |
| queryString | This is the query string portion of the accessed URL | String |
| activeConfigId | This is the active configuration id which the user was working in when the error occurred | String |
| errorTime | This is the time of error occurrence | Timestamp |
| errorId | This is the error id | String |
| errorTitle | This is the error title | String |
| errorDetails | This is the details of the error | String |
| userId | This is the user id who initiated the request that caused this error | String |
| activeConfigName | This is the name of the active configuration in which the user was working when this error occurred | String |
| errorLevel | This is the level of the error. Values are ERROR or WARN | String |

[Back to top](#TopPage)

# Server Information

This publishes the server health information including memory usage, DB
ping time and status on services and DB connections. This is useful to
understand how the server is performing. Most important attribute is the
dbPingTime. If the latency between server and DB gets worse it will
impact the almost every use case in the product.

### Advanced Property [advanced-property-1]

You enable this bean by setting **Enable Server Metrics MBean** to
**true**

### Object Name [object-name-1]

com.ibm.team.foundation.server:name=\<\>, type=serverMetrics

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
| dbPingTime | This is the round trip time from the JTS or application server to the database in milliseconds | Integer |
| noOfServicesWithErrorStatus | This is a number of services from all components that have failed to initialize | Integer |
| servicesWithErrorStatusMsg | This is the error message associated with all the services not fully initialized | String |
| dbConnectionStatus | This is the status of the databse connection. Values are ERROR, OK or WARNING. | String |
| dbConnectionStatusMsg | This is message associated with an error for the database connection status | String |
| serverstateId | The etag of the jpi prefix mappings reflects the complete state of all prefix mappings. If there are no mappings this value is NA | String |
| serverStateMsg | This is message associated with when the server state Id indicates that a server renmae has occured | String |
| buildId | This is the build id associated with the server | String |
| freeMemory | The amount of free memory in the Java Virtual Machine in bytes | Long |
| totalMemory | The total amount of memory in the Java virtual machine in bytes | Long |
| maxMemory | The maximum amount of memory that the Java virtual machine will attempt to use in bytes | Long |

[Back to top](#TopPage)

# Asynchronous Tasks Elapsed Time

This is useful to track the average response time for background tasks
and help with tuning the frequency of these and also monitor the
degradation in their response time.

### Advanced Property [advanced-property-2]

You enable this bean by setting **Enable Async Task Metrics MBean** to
**true**

### Object Name [object-name-2]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=asynchronoustasks, facet=elapsed time in seconds, counterName=\*

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

# Asynchronous Tasks Queued Count

This is useful to track the backlog of the background tasks being queued
up.

### Advanced Property [advanced-property-3]

You enable this bean by setting **Enable Async Task Metrics MBean** to
**true**

### Object Name [object-name-3]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=asynchronoustasks, facet=queuedcount, counterName=\*

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

# Expensive Scenario Details

This will publish details about the active and completed resource
intensive scenarios in the system. This is useful to understand how the
resource intensive scenarios are performing and understand what are the
active scenarios at any given point in time. It also gives details about
the user who requested the scenario.

### Advanced Property [advanced-property-4]

You enable this bean by setting **Enable Scenario Details MBean** to
**true**

### Object Name [object-name-4]

com.ibm.team.foundation.scenarios:name=\<\>,
type=expensiveScenarioDetailsMetrics, scenarioNameAndId=\*

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
| scenarioName | This is the name of resource intensize scenario | String |
| scenarioId | This is a unique id assigned to this instance of the scenario | String |
| startTime | This is the start time of the scenario instance | Timestamp |
| endTime | This is end time of the scenario instance | Timestamp |
| userName | This is name of the user who initiated the scenario | String |
| isActive | This is a boolean value indicating if the scenario is completed or not. If it is not completed then the end time attribute is set as -1 | Boolean |
| duration | This is the total time this scenario was running in millisecs. If the scenario is still active then this value is indicating how long it has been running since it started until the current time when the snapshot was taken. If it is not active then it is the end time minus the start time | Long |

[Back to top](#TopPage)

# JDBC Connection Pool Active Connections

This is useful to understand the sizing for the JDBC pools and if these
pool sizes are correctly set for the current concurrency level of the
system. If the size is small then higher concurrency will result in
operations waiting and is the size is too big then system resources are
consumed even though the load does not exist
([Article](https://jazz.net/library/article/1484)). The different facets
are active connections, usage percentage, queue length and wait time.

### Advanced Property [advanced-property-5]

You enable this bean by setting **Enable Resource Usage MBean** to
**true**

### Object Name [object-name-5]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=resourceusage, facet=activeconnections, counterName= JDBC
connection pool

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
| poolSize | This is the maximum size of the pool | Integer |

[Back to top](#TopPage)

# JDBC Connection Pool Queue Length

This is useful to understand the sizing for the JDBC pools and if these
pool sizes are correctly set for the current concurrency level of the
system. This facet highlights the size of the queue of pending
connection requests.

### Advanced Property [advanced-property-6]

You enable this bean by setting **Enable Resource Usage MBean** to
**true**

### Object Name [object-name-6]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=resourceusage, facet=queuelength, counterName=JDBC connection pool

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

# JDBC Connection Pool Usage Percentage

This is useful to understand the sizing for the JDBC pools and if these
pool sizes are correctly set for the current concurrency level of the
system. If the size is small then higher concurrency will result in
operations waiting and is the size is too big then system resources are
consumed even though the load does not exist
([Article](https://jazz.net/library/article/1484)). The different facets
are active connections, usage percentage, queue length and wait time.

### Advanced Property [advanced-property-7]

You enable this bean by setting **Enable Resource Usage MBean** to
**true**

### Object Name [object-name-7]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=resourceusage, facet=usagepercentage, counterName=JDBC connection
pool

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

# JDBC Connection Pool Wait Time in milliseconds

This is useful to understand the sizing for the JDBC pools and if these
pool sizes are correctly set for the current concurrency level of the
system. This facet highlights the size of the queue of pending
connection requests.

### Advanced Property [advanced-property-8]

You enable this bean by setting **Enable Resource Usage MBean** to
**true**

### Object Name [object-name-8]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=resourceusage, facet=wait time in ms, counterName=JDBC connection
pool

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
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# RDB Mediator Connection Pool Active Connections

This is useful to understand the sizing for the RDB mediator pools and
if these pool sizes are correctly set for the current concurrency level
of the system. If the size is small then higher concurrency will result
in operations waiting and is the size is too big then system resources
are consumed even though the load does not exist
([Article](https://jazz.net/library/article/1484)). The different facets
are active connections, usage percentage, queue length and wait time.

### Advanced Property [advanced-property-9]

You enable this bean by setting **Enable Resource Usage MBean** to
**true**

### Object Name [object-name-9]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=resourceusage, facet=active connections, counterName=RDB mediator
pool

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# RDB Mediator Connection Pool Queue Length

This is useful to understand the sizing for the RDB mediator pools and
if these pool sizes are correctly set for the current concurrency level
of the system. This facet highlights the size of the queue of pending
connection requests.

### Advanced Property [advanced-property-10]

You enable this bean by setting **Enable Resource Usage MBean** to
**true**

### Object Name [object-name-10]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=resourceusage, facet=queue length, counterName=RDB mediator pool

### Default Frequency for Publishing [default-frequency-for-publishing-10]

15 minutes

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# RDB Mediator Pool Usage Percentage

This is useful to understand the sizing for the RDB mediator pools and
if these pool sizes are correctly set for the current concurrency level
of the system. If the size is small then higher concurrency will result
in operations waiting and is the size is too big then system resources
are consumed even though the load does not exist
([Article](https://jazz.net/library/article/1484)). The different facets
are active connections, usage percentage, queue length and wait time.

### Advanced Property [advanced-property-11]

You enable this bean by setting **Enable Resource Usage MBean** to
**true**

### Object Name [object-name-11]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=resource usage, facet=usage percentage, counterName=RDB mediator
pool

### Default Frequency for Publishing [default-frequency-for-publishing-11]

15 minutes

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# RDB Mediator Pool Wait Time in milliseconds

This is useful to understand the sizing for the RDB mediator pools and
if these pool sizes are correctly set for the current concurrency level
of the system. This facet highlights the size of the queue of pending
connection requests.

### Advanced Property [advanced-property-12]

You enable this bean by setting **Enable Resource Usage MBean** to
**true**

### Object Name [object-name-12]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=resource usage, facet=wait time in ms, counterName=RDB mediator
pool

### Default Frequency for Publishing [default-frequency-for-publishing-12]

15 minutes

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# Local configuration management cache statistics Cache hit ratio

This is useful to understand how the caches are performing. In a
production environment the hit ratio of the caches should be greater
than 95 ([Blog](https://blog.stackpath.com/glossary/cache-hit-ratio/)).
Other facets are Entry added to cache, Entry removed from cache, Entry
found in cache, Entry not found in cache, Entry replaced in cache and
Entry garbage collected from cache.

### Advanced Property [advanced-property-13]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-13]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Cache hit ratio as a
percentage, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-13]

15 minutes

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# Local configuration management cache statistics Entry added to cache

This is useful to understand how the caches are performing. In a
production environment the hit ratio of the caches should be greater
than 95 ([Blog](https://blog.stackpath.com/glossary/cache-hit-ratio/)).
This facet highlights the entries added to the cache

### Advanced Property [advanced-property-14]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-14]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Entry added to cache,
counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-14]

15 minutes

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

### Advanced Property [advanced-property-15]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-15]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Entry found in cache,
counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-15]

15 minutes

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

### Advanced Property [advanced-property-16]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-16]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Entry not found in
cache, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-16]

15 minutes

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

### Advanced Property [advanced-property-17]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-17]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Entry removed from
cache, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-17]

15 minutes

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

### Advanced Property [advanced-property-18]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-18]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Entry replaced in cache,
counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-18]

15 minutes

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

### Advanced Property [advanced-property-19]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-19]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Entry garbage collected
from cache, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-19]

15 minutes

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

### Advanced Property [advanced-property-20]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-20]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt cache statistics, facet=Time for computing a
value in ms, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-20]

15 minutes

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
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |
| value | This is the current average value of the scalar counter | Long |
| min | This is the minimum value of the scalar counter | Long |
| max | This is the maximum value of the scalar counter | Long |

[Back to top](#TopPage)

# Local configuration management service statistics Elapsed time in milliseconds

This helps with monitoring the average execution time of the different
local configuration management service API for DNG and DM. This includes
but not limited to operations like creating a changeset, creating a
stream, creating a baseline, committing a changeset etc.

### Advanced Property [advanced-property-21]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-21]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=local config mgmt service, facet=Elapsed time (in ms),
counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-21]

15 minutes

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

# Local configuration management service statistics Creation time in milliseconds

This helps with monitoring the average execution time of some of the
advanced config mgmt. operations like skew detection on streams and
baselines.

### Advanced Property [advanced-property-22]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-22]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=Configuration aware functionality, facet=Creation time (ms),
counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-22]

15 minutes

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

# Local configuration management service statistics Rows created in in a new stream

This helps with monitoring the number of rows created when a steam
create operation is executed.

### Advanced Property [advanced-property-23]

You enable this bean by setting **Enable Local Versioning Cache Metrics
MBean** to **true**

### Object Name [object-name-23]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=Configuration aware functionality, facet=Rows created,
counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-23]

15 minutes

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

# Transaction cache statistics Number of hits

This provides the transaction cache(s) operation metrics. This provides
counts for the following operations on ITEM currents and ITEM state
caches. The facets are added, misses, invalidated, hits and autoupdated.
This is useful to understand how the caches are performing. In a
production environment the hit ratio of the caches should be greater
than 95.

### Advanced Property [advanced-property-24]

You enable this bean by setting **Enable the item cache summary metrics
Mbean** to **true**

### Object Name [object-name-24]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=Item Cache Summary, facet=hits, counter Name=\*

### Default Frequency for Publishing [default-frequency-for-publishing-24]

15 minutes

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

# Transaction cache statistics Number of misses

This provides the transaction cache(s) operation metrics. This provides
counts for the following operations on ITEM currents and ITEM state
caches. This facet highlights the number of misses from the cache.

### Advanced Property [advanced-property-25]

You enable this bean by setting **Enable the item cache summary metrics
Mbean** to **true**

### Object Name [object-name-25]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=Item Cache Summary, facet=misses, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-25]

15 minutes

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

# Transaction cache statistics Number of invalidations

This provides the transaction cache(s) operation metrics. This provides
counts for the following operations on ITEM currents and ITEM state
caches. This facet highlights the number of invalidations from the
cache.

### Advanced Property [advanced-property-26]

You enable this bean by setting **Enable the item cache summary metrics
Mbean** to **true**

### Object Name [object-name-26]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=Item Cache Summary, facet=invalidated, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-26]

15 minutes

### Attributes [attributes-26]

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

# Transaction cache statistics Number of entries added

This provides the transaction cache(s) operation metrics. This provides
counts for the following operations on ITEM currents and ITEM state
caches. This facet highlights the number of entries added to the cache.

### Advanced Property [advanced-property-27]

You enable this bean by setting **Enable the item cache summary metrics
Mbean** to **true**

### Object Name [object-name-27]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=Item Cache Summary, facet=added, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-27]

15 minutes

### Attributes [attributes-27]

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

# Transaction cache statistics Number of entries auto updated

This provides the transaction cache(s) operation metrics. This provides
counts for the following operations on ITEM currents and ITEM state
caches. This facet highlights the number of entires that were updated in
the cache.

### Advanced Property [advanced-property-28]

You enable this bean by setting **Enable the item cache summary metrics
Mbean** to **true**

### Object Name [object-name-28]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=Item Cache Summary, facet=autoUpdated, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-28]

15 minutes

### Attributes [attributes-28]

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

# Resource Intensive Scenarios Elapsed time in milliseconds

This provides the counts and average response time for each of the
resource intensive scenarios in the system ([Deployment
Wiki](https://jazz.net/wiki/bin/view/Deployment/CLMExpensiveScenarios)).
This is useful to understand how the resource intensive scenarios are
performing and track any degradation in their response times.

### Advanced Property [advanced-property-29]

You enable this bean by setting **Enable Scenario Details MBean** to
**true**

### Object Name [object-name-29]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=scenarios, facet=elapsed time in millisecs, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-29]

15 minutes

### Attributes [attributes-29]

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

# Resource Intensive Scenarios Summary Elapsed time in milliseconds

This provides the counts and average response time for all the resource
intensive scenarios in the system during the collection interval. This
is useful to understand how the resource intensive scenarios are
performing and track any degradation in their response times.

### Advanced Property [advanced-property-30]

You enable this bean by setting **Enable Scenario Details MBean** to
**true**

### Object Name [object-name-30]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=scenarios, facet=elapsed time in millisecs,
counterNameAndId=summary\_\*

### Default Frequency for Publishing [default-frequency-for-publishing-30]

15 minutes

### Attributes [attributes-30]

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

# Web Service Statistics Elapsed time in seconds

This is useful to track the average response time for web services and
watch for degradations. Added to this the other facets are bytes sent to
client and bytes received from client. These are useful to track the
average request pay load and response pay load for web services and
watch for large payloads that may affect the network I/O.

### Advanced Property [advanced-property-31]

You enable this bean by setting **Enable Web Service Metrics MBean** to
**true**

### Object Name [object-name-31]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=web service, facet=elapsed time in secs, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-31]

15 minutes

### Attributes [attributes-31]

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

# Web Service Statistics Bytes sent to client

These are useful to track the average request pay load and response pay
load for web services and watch for large payloads that may affect the
network I/O.

### Advanced Property [advanced-property-32]

You enable this bean by setting **Enable Web Service Metrics MBean** to
**true**

### Object Name [object-name-32]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=web service, facet=bytes sent to client, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-32]

15 minutes

### Attributes [attributes-32]

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

# Web Service Statistics Bytes received from client

These are useful to track the average request pay load and response pay
load for web services and watch for large payloads that may affect the
network I/O.

### Advanced Property [advanced-property-33]

You enable this bean by setting **Enable Web Service Metrics MBean** to
**true**

### Object Name [object-name-33]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics,
group=web service, facet=bytes received from client, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing-33]

15 minutes

### Attributes [attributes-33]

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

# Web Services Statistics Summary Over Collection Intervals

This bean captures the summary information over collection intervals.
The summary includes total count, average over interval, max over
interval, transaction rate, the total value over interval etc. The
summary bean is create by facet and within each facet you can get a
summary by component.

### Advanced Property [advanced-property-34]

You enable this bean by setting **Enable Web Service Metrics MBean** to
**true**

### Object Name [object-name-34]

com.ibm.team.foundation.webservices:name=\<\>,
type=webServicesSummaryMetrics, facet=**, component=**

### Default Frequency for Publishing [default-frequency-for-publishing-34]

15 minutes

### Attributes [attributes-34]

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
| averageOverInterval | This is the average value across all range counters for this collection time interval | Double |
| maxOverInterval | This is the maximum average value across all range counters for this collection time interval | Double |
| totalOverInterval | This is the total value across all range counters for this collection time interval | Double |
| countOverInterval | This is the total count across all range counters for this collection time interval | Double |
| intervalDuration | This is the collection time interval in seconds | Double |
| transactionRate | This is the transaction rate (countover interval/interval duration) in counts per second | Double |

[Back to top](#TopPage)

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
