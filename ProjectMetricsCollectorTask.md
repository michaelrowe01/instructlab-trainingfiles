META:TOPICINFO{author="zz00tc" date="1586330913" format="1.1"
version="1.7"} META:TOPICPARENT{name="Common605Beans"}

# ProjectMetricsCollectorTask [projectmetricscollectortask]

Build basis: 6.0.5 ENDCOLOR \#TopPage

TOC{title="Managed Beans"}

# Project Area Information

This publishes the number of contributor, team, development lines, work
items and attachments for each project area in the repository.
Additionally it indicates if the project is archived or not. You can
monitor these and also setup alerts if the usage patterns are not within
normal parameters. In future it will contain an attribute for the total
size of the project area in the repository. This will help determine if
the project warrants its own server and can be a candidate for server
split. It also provides if the project area has be opted in and provides
configuration management metrics like number of component, streams,
baselines etc. Note:- This Configuration management metrics are not
applicable for GC and CCM application.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Project Metrics MBean** to
**true**

### Object Name [object-name]

com.ibm.team.foundation.projectarea:name=\<\>, type=projectMetrics,
projectNameAndId=\*

### Default Frequency for Publishing [default-frequency-for-publishing]

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
| isArchived | This is the boolean to indicate is the project area is archived or not | Boolean |
| noOfContributors | This is the total contributors associated with this project area | Integer |
| noOfTeams | This is total number of team areas within this project area | Integer |
| projectName | This is name of the project area | String |
| projectId | This is id of the project area | String |
| workitemCount | This is the total number of work items within this project area | Integer |
| attachmentCount | This is total number of attachments within this project area | Integer |
| attachmentTotalLength | This is the total size of all the attachments (in bytes) within this project area | Long |
| pleEnablementState | This is the PLE enablement state for the project area. Values are OPT_OUT, OPT_IN_SINGLE_STREAM_PER_COMPONENT or OPT_IN_FULL | String |
| totalNoOfComponents | This is the total number of components within this project area | Long |
| totalNoOfStreams | This is total number of streams for all the components in this project area | Long |
| totalNoOfBaselines | This is total number of baselines for all the components in this project area | Long |
| totalNoOfVersionMappings | This is total number for version mappings for all concepts in all the project area components | Long |
| MaximumDepthOfRootStream | This is maximum depth of any of the root component streams in this project area | Long |

[Back to top](#TopPage)

# Work Item Information

This provides the type of work item and the total count of this type of
work items for each project area.

### Advanced Property [advanced-property-1]

You enable this bean by setting **Enable Project Metrics MBean** to
**true**

### Object Name [object-name-1]

com.ibm.team.foundation.projectarea:name=\<\>,
type=projectWorkItemMetrics, typeNameAndProjectNameAndId=\*

### Default Frequency for Publishing [default-frequency-for-publishing-1]

1 Week

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
| projectName | This is name of the project area | String |
| projectId | This is the id of the project area | String |
| count | This is the total number of work items of this type within this project area | Integer |
| workItemType | The type name of the work item type | String |

[Back to top](#TopPage)

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
