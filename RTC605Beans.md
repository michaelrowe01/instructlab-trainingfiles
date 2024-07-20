META:TOPICINFO{author="rwatts" date="1536347665" format="1.1"
reprev="1.2" version="1.2"} META:TOPICPARENT{name="CLM605MXBeans"}

# Rational Team Concert Managed Beans DKGRAY Authors: Richard Watts, Vishwanath Ramaswamy, Vaughn Rokosz [rational-team-concert-managed-beans-dkgray-authors-richard-watts-vishwanath-ramaswamy-vaughn-rokosz]

Build basis: CLM 6.0.5 ENDCOLOR

TOC{title="Page contents"}

## Introduction

Rational Team Concert publishes managed beans that provide metrics of
certain aspects of the system (build queue, client usage, large files).
These beans can be used to monitor performance of the system and provide
guidance for troubleshooting performance issues. In addition, we have an
attribute that is RTC Specific in the ProjectMetricsCollectorTask (also
usage metrics related). While Rational Team Concert is the first
application to adopt clustering, the clustering mbeans are part of the
common foundation mbean collection (available to all tools that adopt
foundation clustering).

The managed beans are not enabled by default out of the box. You need to
consider your monitoring strategy and only turn on those managed beans
you will actually consume. These managed beans are enabled through the
advanced properties admin UI. To turn them on, you would locate the
background task in the table below and enable it by setting the enable
property to true. It is recommended that you take the default values
because these have been carefully considered and tuned for optimal
efficiency.

## Table 1 - Categories

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Category | Description | Background Tasks |
|:---|:---|:---|
| Usage Metrics | The Usage Metrics category collects common, project and license metrics from the system. | ProjectMetricsCollectorTask LicenseMetricsCollectorTask |
| Serviceability | Additional resource consumption metrics were introduced under a new category called Serviceability. | BuildQueueMetricsCollectorTask VersionedContentMetricsTask |

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
| [ProjectMetricsCollectorTask](Rtc605ProjectMetricsCollectorTask) |  | Project Area Information |
| [LicenseMetricsCollectorTask](Rtc605LicenseMetricsCollectorTask) |  | Compatible Client Login Details Number of logins |
| [BuildQueueMetricsCollectorTask](Rtc605BuildQueueMetricsCollectorTask) |  | Build Queue Information |
| [VersionedContentMetricsTask](Rtc605VersionedContentMetricsTask) |  | SCM Versioned Content Component Metrics SCM Versioned Content Repository Metrics SCM Versioned Content Top File Sizes Metrics |

##### Related topics: [CLM 6.0.5 Monitoring Managed Beans Reference](CLM605MXBeans) [related-topics-clm-6.0.5-monitoring-managed-beans-reference]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
