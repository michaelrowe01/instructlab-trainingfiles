META:TOPICINFO{author="syeshin" date="1536849742" format="1.1"
reprev="1.2" version="1.2"} META:TOPICPARENT{name="Common605Beans"}

# DiagnosticsMetricsTask [diagnosticsmetricstask]

Build basis: 6.0.5 ENDCOLOR

TOC{title="Managed Beans"}

# Diagnostics

This provides the results of the server diagnostics which by default
runs every 70 minutes. This is useful to track the status of the
periodic execution of server diagnostics.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Diagnostic Metrics Mbean** to
**true**

### Object Name [object-name]

com.ibm.team.foundation.diagnostic:name=\<\>, type=diagnosticMetrics,
testId=\*

### Default Frequency for Publishing [default-frequency-for-publishing]

70 Minutes

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
| duration | This is the time taken in milliseconds to execute the diagnostic for this test id | Integer |
| startTime | This is the start time of the diagnostic for this test id | Timestamp |
| statusDesc | This is the message describing the status | String |
| detailStatusDesc | This is the detailed message describing the outcome of the diagnostic | String |
| status | This is the status of the diagnostic. Values are OK, WARN or ERROR | String |
| testId | This is the id of this specific diagnostic | String |
| nodeId | This is the application node id in case the CLM application is clustered. Otherwise value is NA | String |

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
