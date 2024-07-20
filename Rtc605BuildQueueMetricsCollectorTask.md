META:TOPICINFO{author="narasim_5f7" date="1567093613" format="1.1"
version="1.4"} META:TOPICPARENT{name="RTC605Beans"}

# BuildQueueMetricsCollectorTask [buildqueuemetricscollectortask]

Build basis: 6.0.5 ENDCOLOR

TOC{title="Managed Beans"}

# Build Queue Information

This provides the size of the repository wide build queue at regular
intervals, the interval is determined by the frequency at which the
background task runs. The build queue contains in progress and pending
build requests. The total value of the build queue equals the sum of the
count of in progress and pending builds.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Build Queue Metrics Collector**
to **true**

### Object Name [object-name]

com.ibm.team.build.queue:name=ccm, type=repositoryBuildQueueMetrics

### Default Frequency for Publishing [default-frequency-for-publishing]

10 Minutes

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
| inQueue | The number of builds in the queue. This should be equal to the number of pending and running builds. | Long |
| personalBuilds | The number of personal builds out of the total builds in the queue | Long |
| pending | The number of pending builds | Long |
| running | The number of in progress builds | Long |

##### Related topics: [Common Managed Beans](Common605Beans) [related-topics-common-managed-beans]
