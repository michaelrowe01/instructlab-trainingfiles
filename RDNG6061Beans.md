META:TOPICINFO{author="timneilson" date="1551362183" format="1.1"
version="1.2"} META:TOPICPARENT{name="CLM6061MXBeans"}

# RM MBean Descriptions [rm-mbean-descriptions]

Build basis: 6.0.6.1 ENDCOLOR

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
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
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
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
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
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
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
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
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
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
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
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
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
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
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
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
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
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| Value | A table of values | Table |

# RogueQuerySummary

BEAN_DESCRIPTION - Publish data gathered from the rogue query monitor.
This looks at the list of long running queries, and return figures about
the size of that list, and statistics about the times that the queries
in the list have been executing.This is useful for monitoring a
production system, checking that the list size isn't increasing and the
times are not degrading.

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
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| domain | This is the namespace for the application under which the MBean data is published | String |
| average | The average wait in the list | java.lang.Integer |
| min | The minimum wait in the list | java.lang.Integer |
| median | The median wait in the list | java.lang.Integer |
| max | The maximum wait in the list | java.lang.Integer |
| queryCount | The number of queries being monitored | java.lang.Integer |

##### Related topics: [MBeans in CLM 6.0.6.1](CLM6061MXBeans) [related-topics-mbeans-in-clm-6.0.6.1]
