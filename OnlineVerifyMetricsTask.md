META:TOPICINFO{author="syeshin" date="1536850812" format="1.1"
reprev="1.3" version="1.3"} META:TOPICPARENT{name="Common605Beans"}

# OnlineVerifyMetricsTask [onlineverifymetricstask]

Build basis: 6.0.5 ENDCOLOR

TOC{title="Managed Beans"}

# Repotools Verify Information

This provides the results of the repository verifiers, which are used in
the verify repotools infrastructure. This is useful to keep an eye on
the data integrity of the production database. This is useful to track
the status of the periodic execution of data verification rules against
the repository.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Online Verify Metrics MBean**
to **true**

### Object Name [object-name]

com.ibm.team.foundation.datavalidation:name=\<\>,
type=onlineVerifyMetrics, componentId=\*

### Default Frequency for Publication [default-frequency-for-publication]

1 Week

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
| duration | This is the time taken in milliseconds to execute the data validation for this component | Long |
| startTime | This is the start time of the data validation for this component | Timestamp |
| componentId | This is the id of the component which has registered the data validator | String |
| statusCode | The component specific status code describing the outcome of the validation | Integer |
| severity | This is the severity of the result. Values are OK=0, INFO=1, WARNING=2, ERROR=4 and CANCEL=8 | Integer |
| message | This is the message describing the outcome of the validation | String |
| exception | Returns the low level exception message if there was an error. Otherwise value is NA | String |

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
