META:TOPICINFO{author="syeshin" date="1536848287" format="1.1"
version="1.2"} META:TOPICPARENT{name="Common605Beans"}

# IndexDataCollectorTask [indexdatacollectortask]

Build basis: 6.0.5 ENDCOLOR

TOC{title="Managed Beans"}

# JFS Index Information

This provides the results of the server diagnostics which by default
runs every 70 minutes. This is useful to track the status of the
periodic execution of server This provides the index size and index
queue information for the rdf and text index used by DNG and DM. Index
information is provided for RDF Live, RDF History, Text Live and Text
History indices. This is useful to track the size of the index and
indirectly help with determining the optimal RAM and JVM Heap memory for
the system.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Index Data Metrics MBean** to
**true**

### Object Name [object-name]

com.ibm.team.foundation.jfsindexing:name=\<\>, type=jfsIndexDataMetrics,
indexname=\*

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
| indexName | This is the name of the jfs index for the application | String |
| indexFormatType | This is type of index. Values are RDF or TEXT | String |
| indexAvailability | This reflects the current state of the index. The values are AVAILABLE, SUSPENDED, SUSPENDING, RESUMING, ABORTED, UNCONNECTABLE, RECOVERING or MIGRATION_IN_PROGRESS | String |
| indexSize | This is the size on disk of the specific jfs index in bytes | Long |
| indexLastProcessed | The timestamp of the last resource indexed by this indexer | Date |
| indexLastReceived | The timestamp of the last resource added to the index queue of this indexer | Date |
| indexDataType | This is type of data in the index. Values are HISTORY or LIVE | String |
| indexBacklog | The number of items waiting to be indexed | Integer |
| indexRemainingTime | An estimate of remaining time to finish to processing the indexing operation in milliseconds | Long |

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
