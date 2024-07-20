META:TOPICINFO{author="tfeeney" date="1696879969" format="1.1"
reprev="1.4" version="1.4"}
META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# MQTT message broker deployment options with IBM Engineering Lifecycle Management solution DKGRAY Authors: Main.TimFeeney [mqtt-message-broker-deployment-options-with-ibm-engineering-lifecycle-management-solution-dkgray-authors-main.timfeeney]

Build basis: 7.0.3 ENDCOLOR

TOC{title="Page contents"}

In IBM Engineering Lifecycle Management (ELM) 7.0.3, there are four
primary reasons why an MQTT message broker is needed.

1.  EWM or ETM clustering for user scalability
    -   see [Change and Configuration Management clustered
        environment](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=considerations-change-configuration-management-clustered-environment)
        and [Quality Management clustered
        environment](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=considerations-quality-management-clustered-environment)
2.  Deep skew detection in global configurations of contributions from
    EWM SCM or RMM
    -   see [Finding multiple different configurations of the same
        component in EWM SCM and RMM contributions (Detecting deep
        component
        skew)](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=areas-detecting-deep-component-skew)
3.  Live logging of running builds
    -   see [Live logging for
        builds](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=SSYMRC_7.0.3/com.ibm.team.build.doc/topics/c_ee_livelogging_overview.htm)
4.  Building global configurations with contributions from other GCM
    servers RED(experimental)ENDCOLOR
    -   see [Enabling GCM servers to contribute configurations to other
        GCM servers
        ](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=agcpa-enabling-gcm-servers-contribute-configurations-other-gcm-servers)

It is quite possible and highly likely that a client deployment will
need a supported MQTT message broker for one or more of the reasons
stated. Note the currently supported MQTT message broker is Eclipse
Amlen which only runs on CentOS and RHEL operating systems (see
[Provisioning your operating
system](https://eclipse.dev/amlen/docs/QuickStartGuide/qs00030_.html)).

We recommend that

-   The MQTT message broker be clustered for both scalability and high
    availability purposes. See [Configuring the cluster membership of an
    Eclipse Amlen
    server](https://eclipse.dev/amlen/docs/Administering/ad00940_.html)
    and [Configuring your system for high
    availability](https://eclipse.dev/amlen/docs/Administering/ad00400_.html).
    ELM provides several JMX MBeans that reporting on aspects of the
    MQTT message broker used by ELM. In particular, see the MQTT service
    metrics MBean in [Common Managed
    Beans](https://jazz.net/wiki/bin/view/Deployment/Common605Beans).
-   Each ELM instance requiring an MQTT message broker should have its
    own independent cluster. For example: one MQTT message broker
    cluster in QA and one in production where each cluster is providing
    EWM and ETM clustering and GC deep skew detection.
-   In cases where you are deploying the experimental capability to
    build global configurations with contributions from other GCM
    servers, you are required to share the cluster between ELM instances
    contributing to the common global configuration.

META:TOPICMOVED{by="tfeeney" date="1696868970"
from="Deployment.MessageSightDeploymentOptions"
to="Deployment.MQTTMessageBrokerDeploymentOptions"}
