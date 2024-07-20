META:TOPICINFO{author="paulellis" date="1680274612" format="1.1"
version="1.3"} META:TOPICPARENT{name="DeploymentMonitoring"}

# Engineering Lifecycle Management monitoring using IBM Instana DKGRAY Authors: Main.PaulEllis, Main.ManojKandala Build basis: Engineering Lifecycle Management 7.x, Instana- current [engineering-lifecycle-management-monitoring-using-ibm-instana-dkgray-authors-main.paulellis-main.manojkandala-build-basis-engineering-lifecycle-management-7.x-instana--current]

ENDCOLOR

TOC{title="Page contents"}

Engineering Lifecycle Management is agnostic to the choice of monitoring
tool used. However, it is vitally important that you use a monitoring
tool to understand your systems' usage as well as to plan future needs.
IBM [Instana](https://www.ibm.com/docs/en/instana-observability/current)
is a fully automated Application Performance Management (APM) solution
designed specifically for the challenges of managing microservice and
cloud-native applications. The same capabilities also allow for
observability of an ELM software stack from the platform to the
application.

[ELM monitoring](https://jazz.net/library/article/91590) and
serviceability have an extensive history over many releases. It is
possible to monitor the ELM applications through [JMX
MBeans](https://www.ibm.com/docs/en/instana-observability/current?topic=technologies-jmx-custom-metrics),
which is just one aspect of the Instana telemetry that provides
system-wide observability, indeed, systems-of-systems-wide
observability.

## What is IBM Instana?

[Getting started is
easy:](https://www.ibm.com/docs/en/instana-observability/current?topic=getting-started)

Completely new to Instana? Watch this [3-min explainer
video.](https://www.ibm.com/links?url=https3A2F2Fwww.instana.com2Finstana-application-performance-monitoring-video-overview2F)
Take the [guided tour and play with
Instana.](https://www.ibm.com/links?url=https3A2F2Fplay-with.instana.io2F232F)
See Instana in action in your own environment: [try Instana for
free.](https://www.ibm.com/links?url=https3A2F2Fwww.instana.com2Ftrial2F)
Explore our ecosystem of hundreds of [supported
technologies.](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/ecosystem/index.html)
Start collecting data with one of our
[agents.](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/setup_and_manage/index.html)
Learn [how to use
Instana](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/using_instana/index.html)
for your use-cases. Read about our unique [Core
Capabilities.](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/core_capabilities/index.html)
Extend Instana with our [Integrations, SDKs &
APIs.](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/integrations/index.html)

### Golden Signals

[Monitoring Distributed
Systems](https://sre.google/sre-book/monitoring-distributed-systems/)
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text

### Heading 2 (use sentence-style capitalization)

Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text

## Heading 1

##### Related topics: [ELM Monitoring](https://jazz.net/library/article/91590), [Deployment web home](DeploymentWebHome) [related-topics-elm-monitoring-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
