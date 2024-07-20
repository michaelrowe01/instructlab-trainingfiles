META:TOPICINFO{author="narasim_5f7" date="1555404270" format="1.1"
reprev="1.2" version="1.2"} META:TOPICPARENT{name="RTC6061Beans"}

# BuildQueueMetricsCollectorTask [buildqueuemetricscollectortask]

Build basis: 6.0.6.1 ENDCOLOR

TOC{title="Managed Beans"}

Refer to [BuildQueueMetricsCollectorTask in
605](Rtc605BuildQueueMetricsCollectorTask) for other mbeans published by
this task.

# Build Engine Information

This provides build engine information at regular intervals, the
interval is determined by the frequency at which the background task
runs. The build engine data consists of active, inactive, idle,
unresponsive engines accross four engine categories

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Build Engine Metrics Mbean** to
**true**

### Object Name [object-name]

com.ibm.team.build.engine:name`"",type=repositoryBuildEngineMetrics,engineCategory`

### Default Frequency for Publishing [default-frequency-for-publishing]

10 Minutes

### Attributes [attributes]

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
| unresponsiveBusy | The number of unresponsive build engines that are processing some build requests. These build engines have not contacted the server within the threshold (minutes) and they are processing some build requests | Long |
| engineType | The category (type) of engines for which this MBean is for. See the section "Engine Template Ids" for possible values for engineType | String |
| total | The total number of build engines | Long |
| active | The number of build engines that are active. Active build engines does not imply that they are running | Long |
| inactive | The number of build engines that are inactive | Long |
| unresponsive | The number of unresponsive build engines. These build engines have not contacted the server within the threshold (minutes) configured in each of the build engine. Some build engines could be processing a build request | Long |
| responsive | The number of responsive build engines. The build engines have contacted the server within the threshold (minutes) configured in each of the build engine | Long |
| responsiveIdle | The number of responsive build engines that are idle. These build engines are not processing any builds | Long |
| reposiveBusy | The number of responsive build engines that are busy. These build engines are processing a build | Long |

#### Engine template Ids

-   com.ibm.rational.buildforge.buildagent.engine
-   com.ibm.rational.connector.buildforge.engine.template
-   com.ibm.rational.connector.hudson.engine.template
-   com.ibm.team.build.engine.jbe

##### Related topics: [related-topics]

-   [Common Managed Beans in 6061](Common6061Beans)
-   [RTC Managed Beans in 6061](RTC6061Beans)
