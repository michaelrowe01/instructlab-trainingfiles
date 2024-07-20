META:TOPICINFO{author="syeshin" date="1536848741" format="1.1"
reprev="1.2" version="1.2"} META:TOPICPARENT{name="Common605Beans"}

# ItemCountMetricsCollectorTask [itemcountmetricscollectortask]

Build basis: 6.0.5 ENDCOLOR

TOC{title="Managed Beans"}

# Item Count Details

This provides information about each type of item in the repository and
their counts in terms of number of states and the overall size of these
items in relation to the total size. This is useful to understand the
data growth in the system and also the breakdown between the different
types of items. Sometimes items like attachments or build results may be
growing at an alarming rate and tracking this metric can explain the
reason for this growth. Added to this, increase in DB size during a
period can also be explained by the items that were added during this
period.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Item Count Metrics Mbean** to
**true**

### Object Name [object-name]

com.ibm.team.foundation.itemcounts:name=\<\>, type=itemCountMetrics,
type Name=\*

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
| itemTypeName | This is the name of the item type | String |
| dbId | This is a unique id assigned to the type in the database | Integer |
| noOfStates | This is total number of states that exists in the REPOSITORY.ITEM_STATES system table for this item type | Integer |
| statesSize | This is total size of all the states that exists in the REPOSITORY.ITEM_STATES system table for this item type in bytes | Long |
| noOfContents | This is total number of content blobs that exists in the REPOSITORY.CONTENT_STORAGE system table for this item type | Integer |
| contentsSize | This is total size of content blobs that exists in the REPOSITORY.CONTENT_STORAGE system table for this item type in bytes | Long |
| sizePercentage | This is percentage of the total size of this item type in relation to the total size of all item types together | Integer |
| totalSize | This is sum of all the content objects and state objects for this item type in bytes | Long |
| totalAllSize | This is sum of all the content objects and state objects for all item types in bytes | Long |

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
