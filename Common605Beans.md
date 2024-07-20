META:TOPICINFO{author="sbeard" date="1589969327" format="1.1"
version="1.15"} META:TOPICPARENT{name="CLM605MXBeans"}

# Common Managed Beans DKGRAY Authors: Richard Watts, Vishwanath Ramaswamy, Vaughn Rokosz [common-managed-beans-dkgray-authors-richard-watts-vishwanath-ramaswamy-vaughn-rokosz]

Build basis: CLM 6.0.5 ENDCOLOR

TOC{title="Page contents"}

## Introduction

The Common Managed Beans that were introduced in 6.0.5. They are grouped
into four categories, Cluster, Performance, Server Health and Usage
Metrics. From there, they are further categorized by background task.

## Table 1 - Categories

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Category | Description | Background Tasks |
|:---|:---|:---|
| Cluster Metrics | Rational Team Concert supports being deployed clustered. Clustered Metrics are only available in a CLM Instance where you are using clustering. If you enable cluster metrics without deploying clustering, you will not see any clustered related values. | CommonMetricsCollectorTask ClusterMetricsTask NodeMetricsTask HighFrequencyMetricsClusterScopedTask HighFrequencyMetricsNodeScopedTask |
| Performance Metrics | The Performance metrics category covers collecting metrics related to overall system performance from users, services, data or database loads. | MetricsCollectorTask HighFrequencyMetricsNodeScopedTask FullTextIndexDataCollectorTask IndexDataCollectorTask ItemCountMetricsCollectorTask SQLActivityMetricsTask |
| Server Health Metrics | Server Health Metrics covers important mbeans that ensure your system is up and running (diagnostics) and data integrity (online verify). | DiagnosticsMetricsTask MetricsCollectorTask OnlineVerifyMetricsTask |
| Usage Metrics | The Usage Metrics category collects common, project and license metrics from the system. | CommonMetricsCollectorTask ProjectMetricsCollectorTask LicenseMetricsCollectorTask |

Background tasks are the mechanism we use to populate the managed beans.
These are enabled in Advanced properties. Changing the interval of a
background task will only go into effect **after** the next interval or
when the application is restarted. Background tasks group beans based on
the frequency of data collection, so background tasks can appear in more
than one category.

## Table 2 - Background Tasks

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Background Task | Description | Managed Beans |
|:---|:---|:---|
| CommonMetricsCollectorTask |  | Cluster Member Information Contributor Information Project Area Summary Information |
| ClusterMetricsTask |  | MQTT Memory Metrics Distributed cache metrics |
| MetricsCollectorTask |  | Asynchronous Tasks Elapsed Time Asynchronous Tasks Queued Count Expensive Scenario Details JDBC Connection Pool Active Connections JDBC Connection Pool Queue Length JDBC Connection Pool Usage Percentage JDBC Connection Pool Wait Time in milliseconds RDB Mediator Connection Pool Active Connections RDB Mediator Connection Pool Queue Length RDB Mediator Pool Usage Percentage RDB Mediator Pool Wait Time in milliseconds Local configuration management cache statistics Cache hit ratio Local configuration management cache statistics Entry added to cache Local configuration management cache statistics Entry found in cache Local configuration management cache statistics Entry not found in cache Local configuration management cache statistics Entry removed from cache Local configuration management cache statistics Entry replaced in cache Local configuration management cache statistics Entry garbage collected from cache Local configuration management cache statistics Time for computing a value in ms Local configuration management service statistics Elapsed time in milliseconds Local configuration management service statistics Creation time in milliseconds Local configuration management service statistics Rows created in in a new stream Transaction cache statistics Number of hits Transaction cache statistics Number of misses Transaction cache statistics Number of invalidations Transaction cache statistics Number of entries added Transaction cache statistics Number of entries auto updated Resource Intensive Scenarios Elapsed time in milliseconds Resource Intensive Scenarios Summary Elapsed time in milliseconds Web Service Statistics Elapsed time in seconds Web Service Statistics Bytes sent to client Web Service Statistics Bytes received from client Web Services Statistics Summary Over Collection Intervals Log Events Server Information |
| HighFrequencyMetricsNodeScopedTask |  | Active Services Active Services Summary MQTT broker subscription metrics |
| HighFrequencyMetricsClusterScopedTask |  | Distributed Cache Microservice online status - Downtime Counts |
| NodeScopedTask |  | Jazz MQTT service metrics - Message Sent Result Success Ratio Jazz MQTT service metrics - Message Handling Thread pool Usage Percentage |
| FullTextIndexDataCollectorTask |  | Full Text Index Information |
| ItemCountMetricsCollectorTask |  | Item Count Details |
| SQLActivityMetricsTask |  | SQL Activity SQL Activity Summary |
| DiagnosticsMetricsTask |  | Diagnostics |
| OnlineVerifyMetricsTask |  | Repotools Verify Information |
| ProjectMetricsCollectorTask |  | Project Area Information Work Item Information |
| LicenseMetricsCollectorTask |  | Floating license consumption statistics Concurrent use Floating license consumption statistics License checkout time Floating license consumption statistics License Denials Token License consumption statistics Concurrent use Token License consumption statistics License Denials Client compatibility with server statistics: Compatible client logins |

##### Related topics: [CLM 6.0.5 Monitoring Managed Beans Reference](CLM605MXBeans) [related-topics-clm-6.0.5-monitoring-managed-beans-reference]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
