META:TOPICINFO{author="narasim_5f7" date="1555407606" format="1.1"
version="1.4"} META:TOPICPARENT{name="RTC6061Beans"}

# ScmMetricsTask [scmmetricstask]

Build basis: 6.0.6.1 ENDCOLOR \#TopPage

TOC{title="Managed Beans"}

Refer to [VersionContentMetricsTask](Rtc605VersionedContentMetricsTask)
for SCM Mbeans in 605.

# SCM Stream Metrics

This captures information about SCM streams, including the name, owner,
the number of snapshots, the number of contained components and their
history size.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable SCM stream metrics** to
**true**

#### Other properties [other-properties]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Name | Description | Default Value |
|:---|:---|:---|
| Custom attribute key | Specifies a custom attribute key that streams and components should be tagged with to enable metrics collection for them. An empty string means metrics will be collected for streams, and components that are owned by a project or team area. |  |

### Object Name [object-name]

com.ibm.team.scm:name="", type=com.ibm.team.scm.Workspace, itemName=**,
itemId=**

### Default Frequency for Publishing [default-frequency-for-publishing]

1 Week

#### Attributes [attributes]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| nodeId | This is the application node id in case the CLM application is clustered | String |
| contextRoot | This is the application root context for the CLM application | String |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set | Integer |
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| domain | This is the namespace for the application under which the MBean data is published | String |
| owner | The owner of the stream | CompositeData |
| itemType | The type of item | String |
| components | The components contained in this stream | ArrayType |
| snapshots | The number of snapshots owned by this stream | Long |
| itemId | The item ID | String |
| name | The name of the item | String |
| numComponents | The number of components contained in this stream | java.lang.Long |

#### owner Attributes

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description                                      | Type   |
|:----------|:-------------------------------------------------|:-------|
| itemId    | The item ID                                      | String |
| itemType  | The type of item. Usually a project or team area | String |

#### components Attributes

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| changeSetsInHistory | The number of change sets in the history of this component in the stream | Long |
| itemId | The item ID | String |
| itemType | The type of item | String |
| name | The name of the item | String |
| numSelections | The number of state selections in the configuration for this component in the stream | Long |
| numSelectionsBase | The number of state selections in the base configuration for this component in the stream | Long |
| operationsInHistory | The number of operations performed on this component in the stream | Long |

# SCM Component Metrics

This captures information about SCM components, including the name,
owner, content size, and the numbers of contained baselines, change
sets, and workspaces that contain the component.

### Advanced Property [advanced-property-1]

You enable this bean by setting **Enable SCM Component Metrics** to
**true**

#### Other properties [other-properties-1]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Name | Description | Default Value |
|:---|:---|:---|
| Custom attribute key | Specifies a custom attribute key that streams and components should be tagged with to enable metrics collection for them. An empty string means metrics will be collected for streams, and components that are owned by a project or team area. |  |

### Object Name [object-name-1]

com.ibm.team.scm:name="", type=com.ibm.team.scm.Component, itemName=**,
itemId=**

###  [section]

Default Frequency for Publishing 1 Week

#### Attributes

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| nodeId | This is the application node id in case the CLM application is clustered | String |
| contextRoot | This is the application root context for the CLM application | String |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set | Integer |
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| domain | This is the namespace for the application under which the MBean data is published | String |
| owner | The owner of the component | CompositeType |
| itemType | The type of the item | String |
| baselines | The number of baselines in the component | Long |
| totalNoOfContent | The number of unique content objects claimed by files in this component | Long |
| changeSets | The number of change sets in this component | Long |
| dbSize | The total size of compressed data stored in the database for content claimed by files in this component | Long |
| baselineConfigs | The number of configurations that correspond to baselines in this component | Long |
| containingWorkspaces | The number of workspaces or streams that contain this component | Long |
| externalStores | A list of external content repositories in which content is stored for this component. This value will be empty if all content is stored in the CCM database | ArrayType |
| itemId | The Item ID | String |
| totalSize | The total uncompressed size of content claimed by files in this component | Long |
| name | The name of the item | String |

#### owner Attributes

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description                                              | Type   |
|:----------|:---------------------------------------------------------|:-------|
| itemId    | The item ID                                              | String |
| itemType  | The type of item. Usually a project or team area or user | String |
| Name      | The name of the item                                     | String |

#### externalStore attributes

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| externalURI | The External Content Repository URI | String |
| totalSize | The total uncompressed size of all content stored in this external content repository | Long |
| totalNoOfContent | The number of content blobs stored in this external content repository | Long |

##### Related topics: [related-topics]

-   [RTC Managed Beans in 6061](RTC6061Beans)
-   [Common Managed Beans in 6061](Common6061Beans)
