# CLM 6.0.6 Monitoring Managed Beans Reference 

Authors: Vishwanath Ramaswamy, Vaughn Rokosz, Richard Watts 

Build basis: CLM 6.0.6 

This document outlines the **changes since 6.0.5** to our managed beans
in the CLM 6.0.6 product suite.

## New and Noteworthy

**Common Beans**

HighFrequencyMetricsNodeScopedTask

-   New Managed Bean: MQTTBrokerSubscriptionStatsMBean

**MetricsCollectorTask**

-   New Managed Bean: Enable Configuration Management Service Metrics
    MBean
-   New Managed Bean: Enable Local Versioning Cache Metrics MBean
-   **Removed Managed Bean:** Enable Cache Metrics MBean
-   Corrected: Enable Web Service Metrics MBean (maxOverInterval
    Attribute fixed)

#### Common Beans

-   [Common Beans](Common606Beans)
-   [Rational Team Concert Beans in 6.0.5](RTC605Beans)

Note: No new MBeans were added in Rational Team Concert in 6.0.6

#### LQE Beans

-   [LQE Beans](https://jazz.net/library/article/90785)

#### Serviceability Component MBean Mapping

Please see [Serviceability Component MBean
Mapping](CLM606ServiceabilityComponentMBeanMapping) for a better
understanding how the CLM Serviceability Component, the MBeans, the
advanced properties admin UI, the property ID's and the MBean
documentation relate to each other.

##### Related topics: 
-   [JMX MBeans for ELM application monitoring](JMXMBeans)

##### Additional contributors: 
-   Main.RichardWatts - 2018-03-20

##### Additional contributors: 
-   [Ralph Schoon](Main.RalphSchoon)
