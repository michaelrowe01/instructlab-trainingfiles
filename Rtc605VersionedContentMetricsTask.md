META:TOPICINFO{author="narasim_5f7" date="1555407241" format="1.1"
version="1.6"} META:TOPICPARENT{name="RTC605Beans"}

# VersionedContentMetricsTask [versionedcontentmetricstask]

Build basis: 6.0.5 ENDCOLOR \#TopPage

TOC{title="Managed Beans"}

# SCM Versioned Content Component Metrics

This captures information about the content for all the scm components
in the server. It provides information like the component name, the
owner of the component, the number files in the component, the size of
the file contents, and where that content is stored.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Versioned Content Component
Metrics MBean** to **true**

### Object Name [object-name]

com.ibm.team.scm.content:name="", type=componentContent,
componentNameAndId=\*

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
| componentId | This is item id of the component | String |
| componentName | This is the name of the component | String |
| totalSize | This is the total uncompressed size of all the content claimed by files in this component | Long |
| dbSize | This is the total size of compressed data stored in the database for content claimed by files in this component | Long |
| totalNoOfContent | This is the total number of content blobs claimed by files in this component | Long |
| ownerId | The item id of the owning project area or contributor | String |
| ownerName | The name of the owning project area or contributor | String |
| externalStores | This is the list of external content stores used by this component | ArrayType |

#### externalStore Attributes

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| externalURI | The External Content Repository URI | String |
| totalSize | The total uncompressed size of all content stored in this external content repository | Long |
| totalNoOfContent | The number of content blobs stored in this external content repository | Long |

[Back to top](#TopPage)

# SCM Versioned Content Repository Metrics

This captures information about the content repositories in which scm
content has been stored. It provides information like the location of
the content repository, the number and total size of the content stored

### Advanced Property [advanced-property-1]

You enable this bean by setting **Enable Versioned Content Repository
Metrics MBean** to **true**

### Object Name [object-name-1]

com.ibm.team.scm.content:name="", type=repositoryMetrics

###  [section]

Default Frequency for Publishing 1 Week

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
| contentRepositories | This is the list of content stores used by this server | Array |

#### contentRepositories Attributes

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| externalURI | The external content repository URI or "DATABASE" | String |
| totalSize | The total uncompressed size of all content stored in this content repository | Long |
| compressedDBSize | The total compressed size of data stored in the database for this content repository | Long |
| totalNoOfContent | The number of content blobs stored in this content repository | Long |

[Back to top](#TopPage)

# SCM Versioned Content Top File Sizes Metrics

This captures information about the largest files stored in SCM
including the content repository where they are stored, their size and
which a list of components and paths where that file may be located.

### Advanced Property [advanced-property-2]

You enable this bean by setting **Enable Top File Sizes MBean** to
**true**

#### Other properties [other-properties]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Name | Description | Default value |
|:---|:---|:---|
| File Sizes MBean - Number of Files to report | The number of files to report for the Top File Sizes MBean | 20 |
| File Sizes MBean - size threshold (in bytes) | The minimum size in bytes for files to be consider by the Top File Sizes MBean | 1000000 |

### Object Name [object-name-2]

com.ibm.team.scm.content:name="", type=topContent,rank=\*

### Default Frequency for Publishing [default-frequency-for-publishing-1]

1 Week

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
| externalURI | The content repository URI where this content is stored | String |
| contentSize | The compressed size of this content if stored in the database, otherwise the full content size | Long |
| contentClaimers | The list of files which claim this content | ArrayType |

#### contentClaimers attributes

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| approximatePath | An approximate path for this file. The file may not exist at this path since full path resolution requires a workspace or stream | String |
| componentName | The name of the component which contains this file | String |
| itemId | The item id for this file | String |
| stateId | The state id for this file | String |

[Back to top](#TopPage)

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
