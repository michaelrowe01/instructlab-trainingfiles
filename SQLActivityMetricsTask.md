META:TOPICINFO{author="syeshin" date="1537457476" format="1.1"
version="1.3"} META:TOPICPARENT{name="Common605Beans"}

# SQLActivityMetricsTask [sqlactivitymetricstask]

Build basis: 6.0.5 ENDCOLOR \#TopPage

TOC{title="Managed Beans"}

# SQL Activity

This provides the SQL activity during the specified interval as a MBean.
This is useful to understand the standard patterns of SQL activity in a
production system. This is useful to track the counts and average
response times for many SQL queries. Helps to understand the high
runners and optimize them. Also helps to drive data partitioning
decisions and preserve the query response time.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable SQL Activity Metrics MBean** to
**true**

### Object Name [object-name]

com.ibm.team.foundation.sqlactivity:name=\<\>, type=sqlActivityMetrics,
id=\*

### Default Frequency for Publishing [default-frequency-for-publishing]

60 Minutes

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
| sqlHash | This is unique hashcode for this specific SQL statement | String |
| sqlStmt | This is the SQL statement | String |
| sqlMinTime | The smallest execution time (in ms) for all instances of this statement | Integer |
| sqlMaxTime | The largest execution time (in ms) for all instances of this statement | Integer |
| sqlTotalTime | The total sum execution time (in ms) for all instances of this statement | Integer |
| sqlTotalCount | The number of times this statement was executed | Integer |
| sqlAverageTime | The average execution time (in ms) for all instances of this statement | Float |
| sqlLastExecutedTimestamp | The time this statement was last executed | Date |
| sqlStmtType | The type of transaction. Values are read, write or other | String |
| sqlActivityInterval | The interval in milliseconds used for capturing the sql activity in this bean | Long |

[Back to top](#TopPage)

# SQL Activity Summary

This provides the summary SQL activity during the specified interval as
a MBean. This is useful to understand the standard patterns of SQL
activity in a production system. This is useful to track the counts and
average response times for many SQL queries by type. Helps to understand
the high runners and optimize them. Also helps to drive data
partitioning decisions and preserve the query response time.

### Advanced Property [advanced-property-1]

You enable this bean by setting **Enable SQL Activity Metrics MBean** to
**true**

### Object Name [object-name-1]

com.ibm.team.foundation.sqlactivity:name=\<\>,
type=sqlActivitySummaryMetrics, sqlStmtType=\*

### Default Frequency for Publishing [default-frequency-for-publishing-1]

60 Minutes

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
| sqlTotalTime | The total sum execution time (in ms) for all sql statements of this type | Integer |
| sqlTotalCount | The number of times this type of statement was executed | Integer |
| sqlAverageTime | The average execution time (in ms) for all sql statements of this type | Double |
| sqlStmtTime | The type of statement. Values are read, write or other | String |
| sqlActivityInterval | The interval in milliseconds used for capturing the sql activity in this bean | Long |

[Back to top](#TopPage)

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
