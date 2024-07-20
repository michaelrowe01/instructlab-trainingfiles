META:TOPICINFO{author="timneilson" date="1579697557" format="1.1"
version="1.1"} META:TOPICPARENT{name="CLM70MXBeans"}

# RM MBean Descriptions [rm-mbean-descriptions]

Build basis: 7.0 ENDCOLOR

TOC{title="Managed Beans"}

# TotalNumberOfArtifacts

BEAN_DESCRIPTION - Publish the total number of RM artifacts on this
server as a MBean, as a single integer value. This is useful for sizing
a production system. Note that the calculation of this value can add
substantial load on large repositories, so should be scheduled to run
infrequently at quiet times.

### Advanced Property [advanced-property]

ADVANCED_PROPERTY_TO_ENABLE_BEAN - You enable this bean by setting
**TotalNumberOfArtifacts.enableMBean** to **true**

### MBean Category: **artifact** [mbean-category-artifact]

### Object Name [object-name]

BEAN_SYNTAX_EXAMPLE com.ibm.rdm.metric:name=TotalNumberOfArtifacts,
type=artifact

### Default Frequency for Publishing [default-frequency-for-publishing]

DEFAULT_BEAN_COLLECTION_FREQUENCY - Weekly, on Saturday evening at 10.30
pm

### Attributes [attributes]

BEAN_ATTRIBUTES_EXAMPLE

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the ELM application is running | String |
| port | This is the port number where the ELM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the ELM application | String |
| nodeId | This is the application node id in case the ELM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| Value | A single Integer value | Integer |

# TotalNumberOfComponents

BEAN_DESCRIPTION - Publish the total number of RM components, across all
projects, on this server, as a single integer value. If configuration
management is not enabled for a project, it has only one component. If
configuration management is enabled, each project can have multiple
components. This is useful for sizing a production system. Note that the
calculation of this value can add substantial load on large
repositories, so should be scheduled to run infrequently at quiet times.

### Advanced Property [advanced-property-1]

ADVANCED_PROPERTY_TO_ENABLE_BEAN - You enable this bean by setting
**TotalNumberOfComponents.enableMBean** to **true**

### MBean Category: **cm** [mbean-category-cm]

### Object Name [object-name-1]

BEAN_SYNTAX_EXAMPLE com.ibm.rdm.metric:name=TotalNumberOfComponents,
type=cm

### Default Frequency for Publishing [default-frequency-for-publishing-1]

DEFAULT_BEAN_COLLECTION_FREQUENCY - Weekly, on Saturday evening at 10.30
pm

### Attributes [attributes-1]

BEAN_ATTRIBUTES_EXAMPLE

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the ELM application is running | String |
| port | This is the port number where the ELM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the ELM application | String |
| nodeId | This is the application node id in case the ELM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| Value | A single Integer value | Integer |

# TotalNumberOfConfigurations

BEAN_DESCRIPTION - Publish the total number of RM comfigurations, across
all projects, on this server, as a single integer value. If
configuration management is not enabled for a project, it has only one
configuration. If configuration management is enabled, each project can
have multiple configurations. This is useful for sizing a production
system. Note that the calculation of this value can add substantial load
on large repositories, so should be scheduled to run infrequently at
quiet times.

### Advanced Property [advanced-property-2]

ADVANCED_PROPERTY_TO_ENABLE_BEAN - You enable this bean by setting
**TotalNumberOfConfigurations.enableMBean** to **true**

### MBean Category: **cm** [mbean-category-cm-1]

### Object Name [object-name-2]

BEAN_SYNTAX_EXAMPLE com.ibm.rdm.metric:name=TotalNumberOfConfigurations,
type=cm

### Default Frequency for Publishing [default-frequency-for-publishing-2]

DEFAULT_BEAN_COLLECTION_FREQUENCY - Weekly, on Saturday evening at 10.30
pm

### Attributes [attributes-2]

BEAN_ATTRIBUTES_EXAMPLE

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the ELM application is running | String |
| port | This is the port number where the ELM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the ELM application | String |
| nodeId | This is the application node id in case the ELM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| Value | A single Integer value | Integer |

# TotalNumberOfBaselines

BEAN_DESCRIPTION - Publish the total number of baselines, across all
projects, on this server, as a single integer value. If configuration
management is not enabled for a project, each project can have multiple
baselines. If configuration management is enabled, each component of the
project can have multiple baselines. This is useful for sizing a
production system. Note that the calculation of this value can add
substantial load on large repositories, so should be scheduled to run
infrequently at quiet times.

### Advanced Property [advanced-property-3]

ADVANCED_PROPERTY_TO_ENABLE_BEAN - You enable this bean by setting
**TotalNumberOfBaselines.enableMBean** to **true**

### MBean Category: **cm** [mbean-category-cm-2]

### Object Name [object-name-3]

BEAN_SYNTAX_EXAMPLE com.ibm.rdm.metric:name=TotalNumberOfBaselines,
type=cm

### Default Frequency for Publishing [default-frequency-for-publishing-3]

DEFAULT_BEAN_COLLECTION_FREQUENCY - Weekly, on Saturday evening at 10.30
pm

### Attributes [attributes-3]

BEAN_ATTRIBUTES_EXAMPLE

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the ELM application is running | String |
| port | This is the port number where the ELM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the ELM application | String |
| nodeId | This is the application node id in case the ELM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| Value | A single Integer value | Integer |

# TotalNumberOfStreams

BEAN_DESCRIPTION - Publish the total number of streams, across all
projects, on this server, as a single integer value. If configuration
management is not enabled for a project, there is one stream per
project. If configuration management is enabled, there can be multiple
streams for each project. This is useful for sizing a production system.
Note that the calculation of this value can add substantial load on
large repositories, so should be scheduled to run infrequently at quiet
times.

### Advanced Property [advanced-property-4]

ADVANCED_PROPERTY_TO_ENABLE_BEAN - You enable this bean by setting
**TotalNumberOfStreams.enableMBean** to **true**

### MBean Category: **cm** [mbean-category-cm-3]

### Object Name [object-name-4]

BEAN_SYNTAX_EXAMPLE com.ibm.rdm.metric:name=TotalNumberOfStreams,
type=cm

### Default Frequency for Publishing [default-frequency-for-publishing-4]

DEFAULT_BEAN_COLLECTION_FREQUENCY - Weekly, on Saturday evening at 10.30
pm

### Attributes [attributes-4]

BEAN_ATTRIBUTES_EXAMPLE

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the ELM application is running | String |
| port | This is the port number where the ELM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the ELM application | String |
| nodeId | This is the application node id in case the ELM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| Value | A single Integer value | Integer |

# TotalNumberOfChangesets

BEAN_DESCRIPTION - Publish the total number of active changesets, across
all projects, on this server, as a single integer value. If
configuration management is not enabled for a project, there are no
changesets. If configuration management is enabled, there can be
multiple open changesets for each project. This is useful for sizing a
production system. Note that the calculation of this value can add
substantial load on large repositories, so should be scheduled to run
infrequently at quiet times.

### Advanced Property [advanced-property-5]

ADVANCED_PROPERTY_TO_ENABLE_BEAN - You enable this bean by setting
**TotalNumberOfChangesets.enableMBean** to **true**

### MBean Category: **cm** [mbean-category-cm-4]

### Object Name [object-name-5]

BEAN_SYNTAX_EXAMPLE com.ibm.rdm.metric:name=TotalNumberOfChangesets,
type=cm

### Default Frequency for Publishing [default-frequency-for-publishing-5]

DEFAULT_BEAN_COLLECTION_FREQUENCY - Weekly, on Saturday evening at 10.30
pm

### Attributes [attributes-5]

BEAN_ATTRIBUTES_EXAMPLE

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the ELM application is running | String |
| port | This is the port number where the ELM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the ELM application | String |
| nodeId | This is the application node id in case the ELM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| Value | A single Integer value | Integer |

# TotalNumberOfLinks

BEAN_DESCRIPTION - Publish the total number of links, within and between
components and projects, as a single integer value.This is useful for
sizing a production system. Note that the calculation of this value can
add substantial load on large repositories, so should be scheduled to
run infrequently at quiet times.

### Advanced Property [advanced-property-6]

ADVANCED_PROPERTY_TO_ENABLE_BEAN - You enable this bean by setting
**TotalNumberOfLinks.enableMBean** to **true**

### MBean Category: **link** [mbean-category-link]

### Object Name [object-name-6]

BEAN_SYNTAX_EXAMPLE com.ibm.rdm.metric:name=TotalNumberOfLinks,
type=link

### Default Frequency for Publishing [default-frequency-for-publishing-6]

DEFAULT_BEAN_COLLECTION_FREQUENCY - Weekly, on Saturday evening at 10.30
pm

### Attributes [attributes-6]

BEAN_ATTRIBUTES_EXAMPLE

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the ELM application is running | String |
| port | This is the port number where the ELM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the ELM application | String |
| nodeId | This is the application node id in case the ELM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| Value | A single Integer value | Integer |

# TotalNumberOfReviews

BEAN_DESCRIPTION - Publish the total number of reviews, within and
between components and projects, as a single integer value.This is
useful for sizing a production system. Note that the calculation of this
value can add substantial load on large repositories, so should be
scheduled to run infrequently at quiet times.

### Advanced Property [advanced-property-7]

ADVANCED_PROPERTY_TO_ENABLE_BEAN - You enable this bean by setting
**TotalNumberOfReviews.enableMBean** to **true**

### MBean Category: **review** [mbean-category-review]

### Object Name [object-name-7]

BEAN_SYNTAX_EXAMPLE com.ibm.rdm.metric:name=TotalNumberOfReviews,
type=review

### Default Frequency for Publishing [default-frequency-for-publishing-7]

DEFAULT_BEAN_COLLECTION_FREQUENCY - Weekly, on Saturday evening at 10.30
pm

### Attributes [attributes-7]

BEAN_ATTRIBUTES_EXAMPLE

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the ELM application is running | String |
| port | This is the port number where the ELM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the ELM application | String |
| nodeId | This is the application node id in case the ELM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| Value | A single Integer value | Integer |

# TotalArtifactsByType

BEAN_DESCRIPTION - Publishes a table of a count of the artifacts in the
system, by artifact type.This can be useful for sizing a production
system. Note that the calculation of this value can add substantial load
on large repositories, so should be scheduled to run infrequently at
quiet times.

### Advanced Property [advanced-property-8]

ADVANCED_PROPERTY_TO_ENABLE_BEAN - You enable this bean by setting
**TotalArtifactsByType.enableMBean** to **true**

### MBean Category: **artifact** [mbean-category-artifact-1]

### Object Name [object-name-8]

BEAN_SYNTAX_EXAMPLE com.ibm.rdm.metric:name=TotalArtifactsByType,
type=artifact

### Default Frequency for Publishing [default-frequency-for-publishing-8]

DEFAULT_BEAN_COLLECTION_FREQUENCY - Weekly, on Saturday evening at 10.30
pm

### Attributes [attributes-8]

BEAN_ATTRIBUTES_EXAMPLE

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the ELM application is running | String |
| port | This is the port number where the ELM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the ELM application | String |
| nodeId | This is the application node id in case the ELM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| Value | A table of values | Table |

# RogueQuerySummary

BEAN_DESCRIPTION - Publish data gathered from the rogue query monitor.
This looks at the list of long running queries, and return figures about
the size of that list, and statistics about the times that the queries
in the list have been executing.This is useful for monitoring a
production system, checking that the list size isn't increasing and the
times are not degrading. In 7.0 the Rogue Query Monitor is still
available, but as it covers only SPARQL queries and these are now mainly
only used for Reviews and Comments, it is of less importance to the
health of the system.

### Advanced Property [advanced-property-9]

ADVANCED_PROPERTY_TO_ENABLE_BEAN - You enable this bean by setting
**RogueQuerySummary.enableMBean** to **true**

### MBean Category: **query** [mbean-category-query]

### Object Name [object-name-9]

BEAN_SYNTAX_EXAMPLE com.ibm.rdm.metric:name=RogueQuerySummary,
type=query

### Default Frequency for Publishing [default-frequency-for-publishing-9]

DEFAULT_BEAN_COLLECTION_FREQUENCY - Weekly, on Saturday evening at 10.30
pm

### Attributes [attributes-9]

BEAN_ATTRIBUTES_EXAMPLE

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the ELM application is running | String |
| port | This is the port number where the ELM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the ELM application | String |
| nodeId | This is the application node id in case the ELM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| average | The average wait in the list | java.lang.Integer |
| min | The minimum wait in the list | java.lang.Integer |
| median | The median wait in the list | java.lang.Integer |
| max | The maximum wait in the list | java.lang.Integer |
| queryCount | The number of queries being monitored | java.lang.Integer |

# Counter Mbeans

Counter MBeans expose internal Counters within the product. There are a
large number of these counters, and they each have a name, a type and a
reporting category. They are only created and exposed when particular
areas of the code are exercised - so for example if a server has never
run any ReqIF operations, no ReqIF MBeans will be available.

Please note that the names, types, and information provided by these
MBeans do not form part of the product API, and so may change
considerably from release to release.

## Default Frequency for Publishing [default-frequency-for-publishing-10]

DEFAULT_BEAN_COLLECTION_FREQUENCY - Weekly, on Saturday evening at 10.30
pm. Note that as these counters do not incur much runtime overhead, then
for full usefulness a more frequent smaple time is recommended, eg every
300 seconds.

## Counter MBean Types [counter-mbean-types]

MBeans in Application types are available while the server is in normal
running state.

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

\| **Application MBean Types** \| \| artifactCopy \| \| asyncTasks \| \|
auditHistory \| \| changesetTransactionService \| \| coreServices \| \|
fullTextIndexingService \| \| fullTextQuery \| \| glossary \| \|
linkQuery \| \| loadingCache \| \| publishing \| \| reportingServices \|
\| restServices \| \| reqIFDefinitionQueryService \| \| reqifImport \|
\| reqIFMappingContextQueryService \| \| requirementQuery \| \|
ResourceTypeService \| \| storage06 \| \| structureAnnotationService \|
\| syncTasks \| \| threadPools \| \| typeQueryService \| \| view \|

MBeans in Migration types are only available while the server migrating
up to 7.0.

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Migration MBean Types    |
|:-------------------------|
| DBMigrationMetrics       |
| Migration                |
| migrationMetrics         |
| migrationTimeMetrics     |
| MigrationTransformer     |
| TransactionAwareConsumer |
| UpgradeMapping           |

## Name and Reporting Type MBeans of each type [name-and-reporting-type-mbeans-of-each-type]

### System Created MBeans [system-created-mbeans]

MBeans of four types are created 'on the fly' with the name of each task
or service requested of them, and therefore individual MBeans of this
type are not named in this document.

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

\| **Type** \| **Reporting Type** \|

|              |                    |
|--------------|--------------------|
| asyncTasks   | [Time](#TimeStats) |
| coreServices | [Time](#TimeStats) |
| restServices | [Time](#TimeStats) |
| syncTasks    | [Time](#TimeStats) |

### Named MBeans [named-mbeans]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

\| **Type** \| **Name** \| **Reporting Type** \| \| DBMigrationMetrics
\| commentNumberTableSize \| [Number](#NumberStats) \| \|
DBMigrationMetrics \| conceptMappingTableSize \| [Number](#NumberStats)
\| \| DBMigrationMetrics \| resourceTypeTableSize \|
[Number](#NumberStats) \| \| DBMigrationMetrics \|
upgradeMappingTableSize \| [Number](#NumberStats) \| \|
DBMigrationMetrics \| wrapperInfoTableSize \| [Number](#NumberStats) \|
\| Migration \| fetchItem \| [Time](#TimeStats) \| \| Migration \|
fetchState \| [Time](#TimeStats) \| \| Migration \| fetchStates \|
[Time](#TimeStats) \| \| Migration \| injectedFailures \|
[Number](#NumberStats) \| \| Migration \| mapItemState \|
[Time](#TimeStats) \| \| Migration \| runstats \| [Time](#TimeStats) \|
\| migrationMetrics \| fetchContentCounterStates \|
[Number](#NumberStats) \| \| migrationMetrics \| numberOfDBRowsRead \|
[Number](#NumberStats) \| \| migrationMetrics \| numberOfProducedObjects
\| [Number](#NumberStats) \| \| migrationMetrics \| statesEncountered \|
[Number](#NumberStats) \| \| migrationMetrics \| statesIgnored \|
[Number](#NumberStats) \| \| migrationMetrics \| statesToBeProcessed \|
[Number](#NumberStats) \| \| migrationMetrics \| totalAbsentChangeSets
\| [Number](#NumberStats) \| \| migrationMetrics \|
totalAbsentConfigurations \| [Number](#NumberStats) \| \|
migrationMetrics \| totalAdditionalConcepts \| [Number](#NumberStats) \|
\| migrationMetrics \| totalArchivedResources \| [Number](#NumberStats)
\| \| migrationMetrics \| totalConceptInfosFailedToEnqueue \|
[Number](#NumberStats) \| \| migrationMetrics \|
totalConceptInfosQueuedForProcessing \| [Number](#NumberStats) \| \|
migrationMetrics \| totalConceptsSaved \| [Number](#NumberStats) \| \|
migrationMetrics \| totalConceptsUnsaved \| [Number](#NumberStats) \| \|
migrationMetrics \| totalDeletionsFailed \| [Number](#NumberStats) \| \|
migrationMetrics \| totalDeletionsMapped \| [Number](#NumberStats) \| \|
migrationMetrics \| totalDeletionsProduced \| [Number](#NumberStats) \|
\| migrationMetrics \| totalSkippedMapStates \| [Number](#NumberStats)
\| \| migrationMetrics \| totalStatesFailedToGenerate \|
[Number](#NumberStats) \| \| migrationMetrics \|
totalStatesInAdditionalConcepts \| [Number](#NumberStats) \| \|
migrationMetrics \| totalStatesSkippedDueToDiscardedCS \|
[Number](#NumberStats) \| \| migrationMetrics \|
totalStatesSkippedDueToNonexistentConfig \| [Number](#NumberStats) \| \|
migrationMetrics \| totalStatesSkippedDueToNullCS \|
[Number](#NumberStats) \| \| migrationMetrics \|
totalStatesSubmittedToQueue \| [Number](#NumberStats) \| \|
migrationTimeMetrics \| convertContentTime \| [Time](#TimeStats) \| \|
migrationTimeMetrics \| fetchContentCounterStatesTime \|
[Time](#TimeStats) \| \| migrationTimeMetrics \|
importItemsToRepositoryTime \| [Time](#TimeStats) \| \|
migrationTimeMetrics \| totalFetchConfigTime \| [Time](#TimeStats) \| \|
migrationTimeMetrics \| upgradeMappingsTime \| [Time](#TimeStats) \| \|
migrationTimeMetrics \| waitingOnProducerQueueTime \| [Time](#TimeStats)
\| \| MigrationTransformer \| conceptsTransformed \| [Time](#TimeStats)
\| \| TransactionAwareConsumer \| txn \| [Time](#TimeStats) \| \|
UpgradeMapping \| saveConceptMapping \| [Time](#TimeStats) \| \|
UpgradeMapping \| saveUpgradeMapping \| [Time](#TimeStats) \| \|
artifactCopy \| createBacklinks_CLMLinks \| [Time](#TimeStats) \| \|
artifactCopy \| createBacklinks_queryCLMLinks \| [Time](#TimeStats) \|
\| artifactCopy \| generateCreateBacklinks \| [Time](#TimeStats) \| \|
auditHistory \| RetrieveHistoryRequest06 \| [Time](#TimeStats) \| \|
auditHistory \| VvcQueryRevisionsRequest06 \| [Time](#TimeStats) \| \|
changesetTransactionService \| abandonedBatchTx \|
[Number](#NumberStats) \| \| changesetTransactionService \| allBatchTx
\| [Number](#NumberStats) \| \| changesetTransactionService \|
allChangesetTx \| [Number](#NumberStats) \| \|
changesetTransactionService \| batchDeadlockedFirstTime \|
[Number](#NumberStats) \| \| changesetTransactionService \| batchRetries
\| [Number](#NumberStats) \| \| changesetTransactionService \|
changesetCommit \| [Time](#TimeStats) \| \| changesetTransactionService
\| failedBatchTx \| [Number](#NumberStats) \| \|
changesetTransactionService \| failedChangesetTx \|
[Number](#NumberStats) \| \| changesetTransactionService \|
itemsInTx_saved \| [Number](#NumberStats) \| \|
changesetTransactionService \| itemsInTx_deleted \|
[Number](#NumberStats) \| \| changesetTransactionService \|
saveDeleteItem \| [Time](#TimeStats) \| \| changesetTransactionService
\| transactionSaveDeleteCommit \| [Time](#TimeStats) \| \|
fullTextIndexingService \| textIndexBatchDeletionTime \|
[Time](#TimeStats) \| \| fullTextIndexingService \|
textIndexBatchSubmissionTime \| [Time](#TimeStats) \| \| fullTextQuery
\| bindingToResults \| [Time](#TimeStats) \| \| fullTextQuery \|
luceneQuery \| [Time](#TimeStats) \| \| fullTextQuery \|
scopingQueryToCollection \| [Time](#TimeStats) \| \| fullTextQuery \|
scopingQueryToModule \| [Time](#TimeStats) \| \| glossary \|
fullTextSearch \| [Time](#TimeStats) \| \| linkQuery \|
linkCountQueryInProjectArea \| [Time](#TimeStats) \| \| linkQuery \|
linkCountQueryInServer \| [Time](#TimeStats) \| \| loadingCache \| All
Object Types Query Cache for Cross Project Link Feature \| [Cache
Statistics](#CacheStats) \| \| loadingCache \| Async Task Status
Resource \| [Cache Statistics](#CacheStats) \| \| loadingCache \|
Attribute Definition Types Query Cache for Cross Project Link Feature \|
[Cache Statistics](#CacheStats) \| \| loadingCache \| Component template
cache \| [Cache Statistics](#CacheStats) \| \| loadingCache \|
Components \| [Cache Statistics](#CacheStats) \| \| loadingCache \|
Configurations \| [Cache Statistics](#CacheStats) \| \| loadingCache \|
Contributors \| [Cache Statistics](#CacheStats) \| \| loadingCache \|
defaultProjectConfigurations \| [Cache Statistics](#CacheStats) \| \|
loadingCache \| Full Text Query Cache \| [Cache Statistics](#CacheStats)
\| \| loadingCache \| IFolderService \| [Cache Statistics](#CacheStats)
\| \| loadingCache \| License Cache \| [Cache Statistics](#CacheStats)
\| \| loadingCache \| Link Preferences Cache \| [Cache
Statistics](#CacheStats) \| \| loadingCache \| Link Retrieval Process
Cache \| [Cache Statistics](#CacheStats) \| \| loadingCache \| Lock
Graph Loader \| [Cache Statistics](#CacheStats) \| \| loadingCache \|
Method cache \| [Cache Statistics](#CacheStats) \| \| loadingCache \|
Operation permissions \| [Cache Statistics](#CacheStats) \| \|
loadingCache \| PartitionPointerModel \| [Cache Statistics](#CacheStats)
\| \| loadingCache \| Project Access Context Info Cache \| [Cache
Statistics](#CacheStats) \| \| loadingCache \| Project details cache \|
[Cache Statistics](#CacheStats) \| \| loadingCache \| Project Status
Cache \| [Cache Statistics](#CacheStats) \| \| loadingCache \| Publish
service links cache \| [Cache Statistics](#CacheStats) \| \|
loadingCache \| Root folder URI cache \| [Cache Statistics](#CacheStats)
\| \| loadingCache \| SameAs Cache \| [Cache Statistics](#CacheStats) \|
\| loadingCache \| StoragePointerModel \| [Cache
Statistics](#CacheStats) \| \| loadingCache \| Stream or baseline exists
state \| [Cache Statistics](#CacheStats) \| \| loadingCache \|
Transaction tracker \| [Cache Statistics](#CacheStats) \| \|
loadingCache \| Type System Provider Project Types \| [Cache
Statistics](#CacheStats) \| \| loadingCache \| Type System Provider
ValueTypes \| [Cache Statistics](#CacheStats) \| \| loadingCache \|
Validity content hash cache \| [Cache Statistics](#CacheStats) \| \|
loadingCache \| Validity content hash cache \| [Cache
Statistics](#CacheStats) \| \| loadingCache \| View Query Cache \|
[Cache Statistics](#CacheStats) \| \| loadingCache \| View Query Request
to Result Cache \| [Cache Statistics](#CacheStats) \| \| loadingCache \|
View Query Request to Result Cache - Time-Expiring \| [Cache
Statistics](#CacheStats) \| \| loadingCache \| View Query Requests per
Result Cache \| [Cache Statistics](#CacheStats) \| \| loadingCache \|
View Query Results Cache \| [Cache Statistics](#CacheStats) \| \|
loadingCache \| View Service Object Type Field Value Cache \| [Cache
Statistics](#CacheStats) \| \| loadingCache \| Workflow Types Cache \|
[Cache Statistics](#CacheStats) \| \| publishing \| abbreviatedUriGets
\| [Number](#NumberStats) \| \| publishing \| abbreviatedUrisRemoved \|
[Number](#NumberStats) \| \| publishing \| urisAbbreviated \|
[Number](#NumberStats) \| \| reportingServices \|
transformation_doCollaboration \| [Time](#TimeStats) \| \|
reqIFDefinitionQueryService \| reqIFDefinitionQuery \|
[Time](#TimeStats) \| \| reqifImport \| reqifImportFolders \|
[Time](#TimeStats) \| \| reqifImport \| reqifImportLinkPrefs \|
[Time](#TimeStats) \| \| reqifImport \| reqifImportResources_total \|
[Time](#TimeStats) \| \| reqifImport \| reqifImportResources_modules \|
[Time](#TimeStats) \| \| reqifImport \|
reqifImportResources_wrappedResources \| [Time](#TimeStats) \| \|
reqifImport \| reqifImportResources_externalAttachments \|
[Time](#TimeStats) \| \| reqifImport \|
reqifImportResources_URIReservation \| [Time](#TimeStats) \| \|
reqifImport \| reqifImportResources_looseRequirements \|
[Time](#TimeStats) \| \| reqifImport \| reqifImportResources_links \|
[Time](#TimeStats) \| \| reqifImport \| reqifImportTypes \|
[Time](#TimeStats) \| \| reqifImport \| reqifImportViewsAndTags \|
[Time](#TimeStats) \| \| reqIFMappingContextQueryService \|
reqIFMappingContextQuery \| [Time](#TimeStats) \| \| requirementQuery \|
artifactCountQueryInProjectArea \| [Time](#TimeStats) \| \|
requirementQuery \| artifactCountQueryInServer \| [Time](#TimeStats) \|
\| ResourceTypeService \| save_state \| [Time](#TimeStats) \| \|
storage06 \| conversion_fromModelItem \| [Time](#TimeStats) \| \|
storage06 \| conversion_toModelItem \| [Time](#TimeStats) \| \|
storage06 \| fetch_diagramIContent \| [Time](#TimeStats) \| \| storage06
\| fetch_states \| [Time](#TimeStats) \| \| storage06 \| fetch_state \|
[Time](#TimeStats) \| \| storage06 \| fetch_items \| [Time](#TimeStats)
\| \| storage06 \| fetch_item \| [Time](#TimeStats) \| \| storage06 \|
fetch_largeAttributeIContent \| [Time](#TimeStats) \| \| storage06 \|
fetch_primaryTextIContent \| [Time](#TimeStats) \| \| storage06 \|
saveItem_delete \| [Time](#TimeStats) \| \| storage06 \| saveItem_save
\| [Time](#TimeStats) \| \| structureAnnotationService \| typeQuery \|
[Time](#TimeStats) \| \| threadPools \| ChangeLogFeedHandler \| [Pool
Statistics](#PoolStats) \| \| threadPools \|
ChangeLogFeedHandlerMigrationTasks \| [Pool Statistics](#PoolStats) \|
\| threadPools \| Command-Executor \| [Pool Statistics](#PoolStats) \|
\| threadPools \| DefaultPartitioner \| [Pool Statistics](#PoolStats) \|
\| threadPools \| MultiRequest-Executor \| [Pool Statistics](#PoolStats)
\| \| threadPools \| Parser/Converter \| [Pool Statistics](#PoolStats)
\| \| threadPools \| Project Template Creation \| [Pool
Statistics](#PoolStats) \| \| threadPools \| ReportRunner06 \| [Pool
Statistics](#PoolStats) \| \| threadPools \| ReqIF-Operation \| [Pool
Statistics](#PoolStats) \| \| threadPools \| Task-Executor \| [Pool
Statistics](#PoolStats) \| \| threadPools \| Task-Scheduler \| [Pool
Statistics](#PoolStats) \| \| threadPools \| Update-Mappings-Executor \|
[Pool Statistics](#PoolStats) \| \| typeQueryService \| typeQuery \|
[Time](#TimeStats) \| \| view \| buildQuery \| [Time](#TimeStats) \| \|
view \| duplicateQueries \| [Time](#TimeStats) \| \| view \|
fullTextSearch \| [Time](#TimeStats) \| \| view \|
inline/Persisted_inline \| [Number](#NumberStats) \| \| view \|
inline/Persisted_persisted \| [Number](#NumberStats) \| \| view \|
overall \| [Time](#TimeStats) \| \| view \| processQueryResultRow \|
[Time](#TimeStats) \| \| view \| serverQueryService \|
[Time](#TimeStats) \| \| view \| transform \| [Time](#TimeStats) \| \|
view \| transformFullObjectFetch \| [Time](#TimeStats) \| \| view \|
viewQueryExcludingTransform \| [Time](#TimeStats) \|

## Reporting Types for Counter MBean Attributes [reporting-types-for-counter-mbean-attributes]

\#TimeStats

### Time Counters [time-counters]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the ELM application is running | String |
| port | This is the port number where the ELM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the ELM application | String |
| nodeId | This is the application node id in case the ELM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| active | Number of active requests. | java.lang.Long |
| active_Number_representation | User suitable string of corresponding field | java.lang.String |
| count | Count of all requests since server restart. | java.lang.Long |
| count_Number_representation | User suitable string of corresponding field | java.lang.String |
| longest | The duration of the longest request. | java.lang.Long |
| longest_Time_representation | User suitable string of corresponding field | java.lang.String |
| mean | The mean of all requests received. | java.lang.Long |
| mean_Time_representation | User suitable string of corresponding field | java.lang.String |
| peak.active | The largest number of concurrent requests. | java.lang.Long |
| peak.active_Number_representation | User suitable string of corresponding field | java.lang.String |
| shortest | The duration of the shortest request. | java.lang.Long |
| shortest_Time_representation | User suitable string of corresponding field | java.lang.String |
| std.dev | The standard deviation of request times. | java.lang.Long |
| std.dev_Time_representation | User suitable string of corresponding field | java.lang.String |
| total | The sum of durations measured by this counter. | java.lang.Long |
| total_Time_representation | User suitable string of corresponding field | java.lang.String |

\#PoolStats

### Thread Pool Counters [thread-pool-counters]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the ELM application is running | String |
| port | This is the port number where the ELM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the ELM application | String |
| nodeId | This is the application node id in case the ELM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| active threads | Count of active threads in this pool. | java.lang.Long |
| active threads_Number_representation | User suitable string of corresponding field | java.lang.String |
| completed tasks | Count of tasks completed by this pool. | java.lang.Long |
| completed tasks_Number_representation | User suitable string of corresponding field | java.lang.String |
| core pool size | Number of threads available in this pool. | java.lang.Long |
| core pool size_Number_representation | User suitable string of corresponding field | java.lang.String |
| max pool size | The maximum number of threads allowed in this pool. | java.lang.Long |
| max pool size_Number_representation | User suitable string of corresponding field | java.lang.String |
| pool size | Current pool size. | java.lang.Long |
| pool size_Number_representation | User suitable string of corresponding field | java.lang.String |
| queue size | Count of queued tasks waiting for a thread. | java.lang.Long |
| queue size_Number_representation | User suitable string of corresponding field | java.lang.String |
| scheduled tasks | All tasks that have been scheduled by this pool. | java.lang.Long |
| scheduled tasks_Number_representation | User suitable string of corresponding field | java.lang.String |

\#CacheStats

### Cache Statistics Counters [cache-statistics-counters]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the ELM application is running | String |
| port | This is the port number where the ELM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the ELM application | String |
| nodeId | This is the application node id in case the ELM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| avgLoadPenalty | The average load penalty in nanoseconds | java.lang.Long |
| avgLoadPenalty_Time_representation | User suitable string of corresponding field | java.lang.String |
| evictionCount | Number of evictions from this cache. | java.lang.Long |
| evictionCount_Number_representation | User suitable string of corresponding field | java.lang.String |
| hitCount | Number of successful lookups of this cache. | java.lang.Long |
| hitCount_Number_representation | User suitable string of corresponding field | java.lang.String |
| hitRate | Returns the ratio of cache requests which were hits. | java.lang.Double |
| hitRate_Percentage_representation | User suitable string of corresponding field | java.lang.String |
| loadCount | The number of loads through the cache. | java.lang.Long |
| loadCount_Number_representation | User suitable string of corresponding field | java.lang.String |
| loadExceptionCount | Count of exceptions encountered when loading the cache. | java.lang.Long |
| loadExceptionCount_Number_representation | String value of corresponding field | java.lang.String |
| loadExceptionRate | Returns the ratio of cache loading attempts which threw exceptions. | java.lang.Double |
| loadExceptionRate_Percentage_representation | User suitable string of corresponding field | java.lang.String |
| loadSuccessCount | No description available. | java.lang.Long |
| loadSuccessCount_Number_representation | User suitable string of corresponding field | java.lang.String |
| missRate | Returns the ratio of cache requests which were misses. | java.lang.Double |
| missRate_Percentage_representation | User suitable string of corresponding field | java.lang.String |
| missCount | Returns the number of times Cache lookup methods have returned an uncached (newly loaded) value, or null. | java.lang.Long |
| missCount_Number_representation | User suitable string of corresponding field | java.lang.String |
| requestCount | Number of requests received. | java.lang.Long |
| requestCount_Number_representation | User suitable string of corresponding field | java.lang.String |
| totalLoadTime | Total time spent loading the cache. | java.lang.Long |
| totalLoadTime_Time_representation | User suitable string of corresponding field | java.lang.String |

\#NumberStats

### Number Counters [number-counters]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| mbeanCreationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the ELM application is running | String |
| port | This is the port number where the ELM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the ELM application | String |
| nodeId | This is the application node id in case the ELM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| value | The single numeric value published by this MBean | Long |
| value_Number_representation | User suitable string of corresponding field | String |

##### Related topics: [MBeans in ELM 7.0](CLM6061MXBeans) [related-topics-mbeans-in-elm-7.0]
