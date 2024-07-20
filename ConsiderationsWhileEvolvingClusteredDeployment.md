META:TOPICINFO{author="tfeeney" date="1696869031" format="1.1"
reprev="1.16" version="1.16"}
META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Considerations in Evolving a Clustered Deployment DKGRAY Authors: [Dinesh Kumar B](Main.DineshKumar) Build basis: ELM 7.0 and higher [considerations-in-evolving-a-clustered-deployment-dkgray-authors-dinesh-kumar-b-build-basis-elm-7.0-and-higher]

ENDCOLOR

TOC{title="Page contents"}

ETM (earlier known as RQM) Clustering was introduced in v7.0. Clustering
EWM (earlier known as RTC) is been available since v6.0.5. This article
is for those who have EWM Cluster in their Deployment and looking to
evolve this deployment by clustering ETM. With RTC/EWM clustered, the
clustering specific components namely - Distributed Cache Microservice
(DCM), Cluster Load Balancer (HAProxy) and MQTT Broker (IBM IOT
MessageSight Server) would already be part of that deployment. RED Can
these clustering related components be shared among multiple
applications clusters? ENDCOLOR Quick answer is "Technically Yes! but
NOT recommended for Production" This article touches upon considerations
to make, for either sharing or having dedicated DCM and MQTT components
between multiple application clusters.

## DCM Considerations

This section talks about considerations to make before sharing DCM among
multiple applications clusters Since DCM Cache has the distributed
objects prefixed with the MQTT Endpoint Port number. When multiple
application clusters are connected to the common DCM, the value used for
Unique cluster name in the applications advanced properties page is seen
prefixed to the individual objects. This helps to uniquely identify the
objects w.r.to their cluster in the common cache. The distributeddata
directory also maintains this distinction by creating directories that
corresponds to the "Unique cluster name". When "Unique cluster name" is
not used, the port number of the MQTT Endpoint used by the application
is used instead. So, if you are to cleanup DCM cache for a specific
application cluster, you can do so by restarting the nodes of that
cluster and clearing content of the corresponding folder under
distributed data.

First of the considerations comes from our Tests. Tests show that for a
5 node cluster meant to handle 2500u concurrency, the order of cluster
related calls reaching this service is close to 8.5 Millions! As more
and more nodes are added or more and more applications are clustered,
due to multifold increase in cluster traffic, this model of "common DCM
for all" is bound to become potential single point of failure.

Second consideration is from Monitoring perspective. When the common DCM
shows up as a performance bottleneck, it may not be possible to point
out the contributing cluster. Further, if a common DCM is used, DCM
performance health metrics can be visualized through only one of the
applications. If that application cluster is down, visibility into DCM
performance metrics is lost, though the other application clusters are
still alive.

Third Consideration from Upgrading Individual Apps perspective. The
version of DCM must match the version of the clustered ELM application.
Sharing the DCM will prevent upgrading individual applications.

Lastly from Maintenance Perspective, you need to also consider the fact
that a shared DCM brought down for maintenance, brings all clustered
apps down.

While its possible to have a common DCM for multiple Application
Clusters, Dedicated DCM for each Clustered Application is how we
envisioned the cluster evolution to happen and would be the recommended
approach.

The main wiki article for clustering also re-iterates this in its
statement For optimal performance, the DCM should be moved to a
dedicated machine.

Important from configuration perspective is to know that with Dedicated
DCM model, there will be multiple DCM's registered to a common JAS. So,
the crucial step when adding newer DCM is to identify it with a unique
Client ID. Once a unique ClientID has been specified, you could continue
with "Distributed Cache Microservice (DCM) for clustered applications
(#step14)" of the [Interactive Installation
Guide](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.0/com.ibm.jazz.install.doc/topics/roadmap_form.html).

## MQTT Broker Endpoint Considerations

This section brings up the considerations to make before using a common
MQTT Broker Endpoint among multiple applications clusters.

IBM IoT MessageSight Server, our preferred MQTT Broker allows to create
multiple Endpoints on a single MessageSight Server. Each identified with
a unique Port and characterized by a set of Connection Policy, Messaging
Policy and Security Profiles.

MessageSight is known to be capable of handling higher loads than
typical of ELM apps. A common MQTT Endpoint can be used for multiple ELM
Application Clusters but a unique Endpoint for each application cluster
would be recommended. The Unique Cluster Name advanced property on the
application admin page is the key to maintain the messages in a
cluster-specific way. Typical of any MQTT Broker use, the size of the
messages exchanged between MQTT Server and the Nodes is small. With
every new node added into the cluster, and with the Publish Subscribe
model used my MQTT, there will be multifold increase in communicated
messages. Hence, sharing the endpoint should be considered as an option
for Evaluation or Training purposes only and for Production, use Unique
Endpoints for each cluster of applications.

The unique MQTT Broker Endpoint can be obtained in one of the following
ways : - through a new MQTT Endpoint on a common MQTT Server With this
approach you may be tempted to reuse the Messaging and Connection
Policies and Security Profiles already created. However, to keep things
discrete, and help troubleshooting scenarios, we recommend creating a
unique Messaging Hub, with its own connection and messaging policies,
and security profiles for each Endpoint. - through an unique MQTT Server
for each Clustered Application With a unique MQTT Server for each
Clustered Application, a complete Messaging Hub would be created afresh
and allows you to create Cluster specific limits and constraints through
the dedicated connection and messaging policies. This will keep the MQTT
Server discrete to each deployment and would be the most performant
option.

Creating an MQTT Endpoint for use in an ELM Cluster is detailed under
"Set up IBM IoT MessageSight (#step8)" of the [Interactive Installation
Guide](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.0/com.ibm.jazz.install.doc/topics/roadmap_form.html).

##### Related topics: [Deployment web home](DeploymentWebHome), [Considerations for HAProxy vs IHS](https://jazz.net/wiki/bin/view/Deployment/CompareProxyServers), [MQTT message broker deployment options with IBM Engineering Lifecycle Management solution](https://jazz.net/wiki/bin/view/Deployment/MQTTMessageBrokerDeploymentOptions) [related-topics-deployment-web-home-considerations-for-haproxy-vs-ihs-mqtt-message-broker-deployment-options-with-ibm-engineering-lifecycle-management-solution]

META:TOPICMOVED{by="din" date="1603442681"
from="Deployment.NewApplicationClusters"
to="Deployment.ConsiderationsWhileEvolvingClusteredDeployment"}
