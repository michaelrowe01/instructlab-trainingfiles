META:TOPICINFO{author="din" date="1707386638" format="1.1" reprev="1.20"
version="1.20"} META:TOPICPARENT{name="DeploymentMigratingAndEvolving"}

# Liberty Vs Websphere Full Profile for CLM DKGRAY Authors: Main.DineshKumar Build basis: CLM 6.0.6.1, ELM 7.x [liberty-vs-websphere-full-profile-for-clm-dkgray-authors-main.dineshkumar-build-basis-clm-6.0.6.1-elm-7.x]

ENDCOLOR

TOC{title="Page contents"}

This article focuses on answering the curious question on if Liberty is
the right choice for CLM Deployment. The article is a one-stop place for
comparative study on Websphere vs Liberty for CLM/ELM. Read on for the
experience share from our internal hosting and from Customer
deployments..

## Support for TWAS Deprecated from ELM 7.0.3

ELM 7.0.2 is the last version with support for Traditional WAS, starting
ELM 7.0.3 Liberty is the only Supported Application Server.

## What IBM Websphere Team says about Liberty One of the frequent asks from Websphere deployments was the start times. Websphere Team says that "Application start is generally faster on Liberty."

Next common concern when comparing the two is performance, on which the
Websphere Team says "The performance of request processing is very
similar on the two profiles in most scenarios, because the application
request paths are mostly common code (channels, transports, containers
etc)."

The differences between the two profiles is touched upon at high-level
in the below article, a whitepaper is referred inside gives in-depth
details : [ Traditional WebSphere or Liberty: how to choose?
](https://developer.ibm.com/wasdev/docs/was-classic-or-was-liberty-how-to-choose/)

## Why Liberty, a word from CLM Development Team

**CLM applications** are typical **J2EE applications** and **only
require** standard **J2EE application server container**. **WebSphere
Liberty** is a standard **J2EE application container**.

Liberty is much lighter (200mb) than traditional WebSphere (1gb+) (as an
example, we do not require EJB support, which is one of several features
that make TWAS heavy). This makes Liberty more suitable for many of the
modern use cases.

For example Clustering... RTC nodes should be light and fast... starting
up a Liberty node takes two - four minutes, this could be much longer
with the heavier Traditional Websphere.

With Cluster use cases, Liberty is much simpler to handle.. in terms of
starting, stopping, upgrading, monitoring, and overall resource
footprint.

Clustering requires Jazz Authorization Server (JAS) and **JAS is
supported only on Liberty**. If you are looking **to Scale your
Deployments**, its important to **migrate to Liberty**.

## What we see in our Internal Hosting

**Jazz.net, ClearObject** runs on Liberty and haven't witnessed any
performance degradation.

By Migrating to Liberty, **Jazz.net Team** found that it was much easier
to administer and maintain due to :

-   Relieved of the Thread Pool management. For more details, refer to
    [Why you probably dont need to tune Liberty Thread
    Pool](https://developer.ibm.com/wasdev/docs/was-liberty-threading-and-why-you-probably-dont-need-to-tune-it/)
-   Easier to stage the deployment for any testing purposes.
-   Startup times are noticeably faster, which makes it easier for
    incorporating quick changes.

Jazz.net Team migrated to Liberty mid 2017, and now some of RTC
instances have further been clustered, making them more scalable. During
migration, some key things to take care of were Certificates, LDAP
config and custom properties.

A link that helps with Certificates is here : [Migrate from Traditional
WebSphere to WebSphere Liberty](MigrateFromTWAStoLiberty)

Some Websphere custom properties that had to be mapped are listed below
:

-   com.ibm.ws.webcontainer.channelwritetype to channelwritetype
-   com.ibm.ws.webcontainer.extractHostHeaderPort to
    extractHostHeaderPort
-   trusthostheaderport to trustHostHeaderPort
-   HttpSessionIdReuse to idReuse

Properties that are valid for Liberty can be found
[here](https://www.ibm.com/support/knowledgecenter/SSRTLW_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/autodita/rwlp_metatype_4ic.html)

A **word of caution** from them though, about changing the XML files.
Liberty loads the files automatically, without necessitating a restart
and that might catch you off-guard, test your changes well before
updating anything on the XML configuration files.

**ClearObject Team** see that, with Liberty Performance is better with
startup as well as during runtime. Like Jazz.net Team, even the
ClearObject Team opines that Migration is simple, could be accounted for
in person-hours rather than in person-days. For some CLM Instances, only
few applications were migrated to Liberty while others continued to be
on WAS Full Profile. Even with such mix, the interop between
applications remains unaffected.

Admin/IT Team was well-versed with Full Profile and were skeptic of the
learning curve involved in moving over to Liberty. However, they found
that learning curve was short and post migration, Admin/IT Team is happy
since they find it easier to administer and maintain a Liberty setup, a
few examples mentioned include :

-   editing User Roles to Group mappings, visiting each profile through
    the admin console is avoided
-   [enforcing TLS
    v1.2](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Ft_enable_tls1.2_liberty.html)
    is simpler

Some things to **be cautious** about before switching to Liberty though
:

-   verify if your integrations are covered
-   any war file that is not CLM, needs to be investigated before
-   test authentications before planning the migration

Overall experience with and/or post Migration has been positive and now,
mostly the CLM instances that are older (v5.x and pre v6.0.1), continue
to be on WAS Full Profile and they are looking forward to moving more
and more instances to Liberty sooner.

## What we have seen with our Customers

Several large Customers have migrated to Liberty.

Some of them were further able to Cluster RTC and were able to support
over 900 concurrent user base on a single RTC instance, running as a
3-Node Cluster.

A number of customers have observed slow application restart times with
WAS. IBM's experience has been that restart times with Liberty are
faster and more consistent. Based on some customer data collected, we
have further observed that Liberty restarts a mere fraction of WAS
restarts. See the graphic showing restarts of a CCM server on WAS vs CCM
server on Liberty.

##### Related topics: [Deployment web home](DeploymentWebHome),[Migrate from Traditional WebSphere to WebSphere Liberty](https://www.ibm.com/support/pages/node/6513066) [Migrate from Apache Tomcat to WebSphere Liberty](MigrateTomcatToLiberty), [WebSphere Liberty threading (and why you probably dont need to tune it)](https://developer.ibm.com/wasdev/docs/was-liberty-threading-and-why-you-probably-dont-need-to-tune-it/) [related-topics-deployment-web-homemigrate-from-traditional-websphere-to-websphere-liberty-migrate-from-apache-tomcat-to-websphere-liberty-websphere-liberty-threading-and-why-you-probably-dont-need-to-tune-it]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

META:FILEATTACHMENT{name="was-v-wlp-production-restart-times-histogram-100-dpi.png"
attachment="was-v-wlp-production-restart-times-histogram-100-dpi.png"
attr="" comment="WAS vs Liberty restart time comparison"
date="1605532266"
path="was-v-wlp-production-restart-times-histogram-100-dpi.png"
size="47924" user="tfeeney" version="1"}
