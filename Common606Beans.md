META:TOPICINFO{author="rwatts" date="1536361112" format="1.1"
reprev="1.1" version="1.1"} META:TOPICPARENT{name="CLM606MXBeans"}

# Common Managed Beans DKGRAY Authors: Richard Watts, Vishwanath Ramaswamy, Vaughn Rokosz [common-managed-beans-dkgray-authors-richard-watts-vishwanath-ramaswamy-vaughn-rokosz]

Build basis: CLM 6.0.6 ENDCOLOR

TOC{title="Page contents"}

## Introduction

The Common Managed Beans that were **changed or introduced in 6.0.6**.
They are grouped into four categories, Cluster, Performance, Server
Health and Usage Metrics. From there, they are further categorized by
background task.

## Table 1 - Categories

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Category | Description | Background Tasks |
|:---|:---|:---|
| Cluster Metrics | Rational Team Concert supports being deployed clustered. Clustered Metrics are only available in a CLM Instance where you are using clustering. If you enable cluster metrics without deploying clustering, you will not see any clustered related values. | No Changes |
| Performance Metrics | The Performance metrics category covers collecting metrics related to overall system performance from users, services, data or database loads. | MetricsCollectorTask HighFrequencyMetricsNodeScopedTask |
| Server Health Metrics | Server Health Metrics covers important mbeans that ensure your system is up and running (diagnostics) and data integrity (online verify). | No Changes |
| Usage Metrics | The Usage Metrics category collects common, project and license metrics from the system. | No Changes |

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
| [MetricsCollectorTask](MetricsCollectorTask606) |  | Enable Configuration Management Service Metrics MBean Enable Local Versioning Cache Metrics MBean Enable Web Service Metrics MBean |
| [HighFrequencyMetricsNodeScopedTask](HighFrequencyMetricsNodeScopedTask606) |  | MQTTBrokerSubscriptionStatsMBean |

##### Related topics: [CLM 6.0.6 Monitoring Managed Beans Reference](CLM606MXBeans) [related-topics-clm-6.0.6-monitoring-managed-beans-reference]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
