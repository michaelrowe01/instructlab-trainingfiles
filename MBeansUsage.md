META:TOPICINFO{author="tfeeney" date="1694035250" format="1.1"
reprev="1.8" version="1.8"} META:TOPICPARENT{name="JMXMBeans"}

# Usage Guides for ELM JMX MBeans DKGRAY Authors: Main.TimFeeney Build basis: 6.0.5 and later [usage-guides-for-elm-jmx-mbeans-dkgray-authors-main.timfeeney-build-basis-6.0.5-and-later]

ENDCOLOR

TOC{title="Page contents"}

While [JMX MBeans Reference Guides](MBeansReference) defines each
available MBean, Usage Guides provide guidance on how they can be used
for different scenarios and goals.

-   [CLM Monitoring Primer](https://jazz.net/library/article/91590)
    provides guidance on the base set of MBeans to include in your
    monitoring strategy. If just getting started, we recommend
    implementing the set of MBeans described in the primer first and
    expand from there.
-   [Monitoring your Engineering Workflow Management (EWM), aka Rational
    Team Concert cluster](https://jazz.net/library/article/91971)
-   [Collecting user related metrics](CollectingUserMetrics)
-   [Collecting data related metrics](CollectingDataMetrics)
-   [Collecting basic health check
    metrics](CollectingBasicHealthCheckMetrics)
-   Sample [ELM Monitoring Guide](ATTACHURL/ELM-MonitoringGuide.pdf)
    from IBM consultant Ian Wilkins (<ian.wilkins@ca.ibm.com>)

<!-- -->

-   Potential future usage guides include:
    -   common troubleshooting scenarios that would be aided by use of
        available MBean data
    -   application specific guidance for DOORS Next, EWM, ETM, etc.
    -   monitoring the health and well being of your reporting subsystem
    -   monitoring non-EWM clustered environments, if different than EWM
    -   monitoring in a configuration management enabled environment
    -   monitoring CCM environments with high volume of builds
        supporting CI/CD

To be most valuable, usage guide content needs to be driven by
experience using the MBeans to monitor a variety of production
deployments. For any client/admin using these JMX MBeans to
monitor/manage production deployments, please contact Tim Feeney
(<tfeeney@us.ibm.com>) to share your experience.

##### Related topics: [JMX MBeans for ELM application monitoring](JMXMBeans) [related-topics-jmx-mbeans-for-elm-application-monitoring]

META:FILEATTACHMENT{name="ELM-MonitoringGuide.pdf"
attachment="ELM-MonitoringGuide.pdf" attr="" comment="sample ELM
monitoring guide as of 9/6/2023" date="1694032015"
path="ELM-MonitoringGuide.pdf" size="1151650" user="tfeeney"
version="1"}
