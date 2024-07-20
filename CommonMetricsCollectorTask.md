META:TOPICINFO{author="zz00tc" date="1537780454" format="1.1"
reprev="1.4" version="1.4"} META:TOPICPARENT{name="Common605Beans"}

# CommonMetricsCollectorTask [commonmetricscollectortask]

Build basis: 6.0.5 ENDCOLOR \#TopPage

TOC{title="Managed Beans"}

# Cluster Member Information

This publishes the basic node information for each node in the cluster
and also the node state.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Cluster Metrics MBean** to
**true**

### Object Name [object-name]

com.ibm.team.foundation.clustermembers:name=\<\>,
type=clusterMemberDataMetrics, nodeId=\*

### Default Frequency for Publishing [default-frequency-for-publishing]

60 minutes

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
| nodeURL | This is the URL for the specified node id | String |
| nodeState | This is state of the node id. Values are INACTIVE=0, STALE=1 and ACTIVE=2 | Integer |

[Back to top](#TopPage)

# Contributor Information

This publishes the number of active and archived users in the
repository. This is useful to understand the active registered users.

### Advanced Property [advanced-property-1]

You enable this bean by setting **Enable Contributor Metrics MBean** to
**true**

### Object Name [object-name-1]

com.ibm.team.foundation.contributors:name=\<\>, type=contributorMetrics

### Default Frequency for Publishing [default-frequency-for-publishing-1]

60 minutes

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
| unarchivedCount | This is the count of the unarchived users in the repository | Integer |
| archivedCount | This is the count of the archived users in the repository | Integer |
| totalCount | This is the count of the total users in the repository | Integer |

[Back to top](#TopPage)

# Project Area Summary Information

This publishes the number of projects in the repository and if they are
archived or not.

### Advanced Property [advanced-property-2]

You enable this bean by setting **Enable Project Metrics MBean** to
**true**

### Object Name [object-name-2]

com.ibm.team.foundation.projectarea:name=\<\>,
type=projectSummaryMetrics

### Default Frequency for Publishing [default-frequency-for-publishing-2]

60 minutes

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
| archivedCount | This is total number of archived project areas in this application | Integer |
| unarchivedCount | This is the total number of unarchived project areas in this application | Integer |
| totalCount | This is total number of project areas in the application | Integer |

[Back to top](#TopPage)

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
