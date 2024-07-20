META:TOPICINFO{author="narasim_5f7" date="1555403662" format="1.1"
version="1.7"} META:TOPICPARENT{name="WebPreferences"}

# Rational Team Concert Managed Beans 6.0.6.1 DKGRAY Authors: Lakshmi Narasimhan T V [rational-team-concert-managed-beans-6.0.6.1-dkgray-authors-lakshmi-narasimhan-t-v]

Build basis: CLM 6.0.6.1 ENDCOLOR

TOC{title="Page contents"}

## Introduction

Refer to [RTC 6.0.5 MBeans
introduction](https://jazz.net/wiki/bin/view/Deployment/RTC605Beans#Introduction)

## Table 1 - Categories

Refer to the following links for existing categories and tasks

-   [RTC 6.0.5 MBeans
    categories](https://jazz.net/wiki/bin/view/Deployment/RTC605Beans#Table_1_Categories)

New or updated tasks introduced in 6.0.6.1 are listed below TABLE{
sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Category | Description | Background Tasks |
|:---|:---|:---|
| Serviceability | Additional resource consumption metrics were introduced under a new category called Serviceability. | BuildQueueMetricsCollectorTask SCMMetricsTask |

Background tasks are the mechanism we use to populate the managed beans.
These are enabled in Advanced properties. Changing the interval of a
background task will only go into effect **after** the next interval or
when the application is restarted. Background tasks group beans based on
the frequency of data collection, so background tasks can appear in more
than one category.

## Table 2 - Background Tasks

The following table lists the new or updated tasks in 6.0.6.1. For
existing tasks, refer to

-   [RTC 6.0.5 MBeans reference](RTC605Beans)

Note: No new mbeans were added in RTC for 6.0.6 release.

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Background Task | Description | Managed Beans |
|:---|:---|:---|
| [BuildQueueMetricsCollectorTask](Rtc6061BuildQueueMetricsCollectorTask) |  | Build Engine Information |
| [ScmMetricsTask](Rtc6061ScmMetricsTask) |  | SCM Component Metrics SCM Stream Metrics |

##### Related topics: [related-topics]

-   [CLM 6.0.5 Monitoring Managed Beans Reference](CLM605MXBeans)
-   [CLM 6.0.6 Monitoring Managed Beans Reference](CLM606MXBeans)
-   [CLM 6.0.6.1 Monitoring Managed Beans Reference](CLM6061MXBeans)

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
