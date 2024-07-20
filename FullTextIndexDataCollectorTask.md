META:TOPICINFO{author="syeshin" date="1536846611" format="1.1"
version="1.2"} META:TOPICPARENT{name="Common605Beans"}

# FullTextIndexDataCollectorTask [fulltextindexdatacollectortask]

Build basis: 6.0.5 ENDCOLOR

TOC{title="Managed Beans"}

# Full Text Index Information

This provides the index size and index location information for the full
text lucene index used by RTC and RQM. This is useful to track the size
of the lucene index.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Full Text Index Data Metrics
MBean** to **true**

### Object Name [object-name]

com.ibm.team.foundation.fulltextindexing:name=\<\>,
type=richTextIndexDataMetrics

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
| duration | This is the time taken in milliseconds to execute the diagnostic for this test id | Integer |
| indexName | This is the name of the full text index for the application | String |
| indexLocation | This is the location of the full text index on disk | String |
| indexSize | This is the size of the full text index on disk in bytes | Long |

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
