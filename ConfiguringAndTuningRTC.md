META:TOPICINFO{author="krzysztofkazmierczyk" date="1673868305"
format="1.1" version="1.20"}
META:TOPICPARENT{name="DeploymentAdminstering"}

# Configuring and tuning Engineering Workflow Management (EWM) [configuring-and-tuning-engineering-workflow-management-ewm]

DKGRAY Authors: [DanToczala](Main.DavidToczala) Build basis: CLM 2011
(product versions 3.x) and later ENDCOLOR

TOC{title="Page contents"}

Configuring EWM should be simple and straightforward for most initial
implementations. There should not be too many things to consider during
the initial configuration of EWM. After the application is deployed,
sometimes performance issues dictate that you consider [configuring and
tuning the Java Virtual Machine (JVM)](ConfiguringAndTuningTheJVM) of
EWM.

## General concerns

When you consider how to configure EWM, it is critical to know the
workload that EWM will support, and the expected user load on the
solution. It is also essential to know how the EWM instance is related
to the Jazz Team Server (JTS), and how the JTS will control licensing
and user access to the resources being managed by the EWM instance. Make
sure that sufficient licenses are available for your user community, and
that user authentication and roles have been considered when configuring
the JTS.

### Hardware needs

In general, an instance of EWM should have at least 2 cores associated
with it, and 4 cores if the instance is planned to be used by a larger
number of users (more than 50 users).

It should also have at least 4 GB of JVM heap memory available to use
for processing, and this amount might need to be tuned and increased
depending on the workload. When you initially configure EWM, there
should also be an equal amount of memory available for the operating
system, so a total of 8 GB of memory should be available to support a
single EWM instance. Some solutions with lighter workloads might be able
to achieve satisfactory performance with less memory, but this is
considered a good starting point.

The EWM instance should also have a fast network connection between
itself, the JTS instance, and the database instance. In an ideal
scenario, these will all reside on the same subnet, but they should at
least have a minimal number of network hops, and by physically
co-located (that is, in the same data center) for acceptable
performance.

The EWM instance will also need disk storage. This storage is used by
the operating system, as well as by the EWM instance itself for the
storage of configuration settings and index files. Making 40 GB of hard
drive storage available is usually sufficient.

### Configuration settings

A EWM instance comes with a default set of configuration parameters. For
initial implementations, these default settings provide the best option.
There are some default options that you might like to modify, to improve
the overall performance and stability of your Jazz deployment.

#### Limiting feed traffic

In deployments with a large number of end users with the Eclipse client,
the Eclipse client requests for feed traffic can put a large load on the
Jazz system. You have the ability to throttle, or reduce these feed
requests. For deployments supporting over 200 concurrent users we
strongly suggest throttling these feed requests. Feeds are useful for
finding out what is going on in a project, but in general they only need
to be updated every 30 minutes or so. The defaults are typically Note
that each Jazz application server (the CCM, RM, QM, and even the JTS)
has it's own feed update interval settings. Here is how you can change
those default update intervals, and limit the amount of feed traffic on
your Jazz server:

1.  Go to the Administration Console for the Jazz application.
2.  Select the Server page
3.  Select "Feed Settings" under the Configuration option in the left
    side menu bar.
4.  In the feed configuration properties, find out:
    -   Is "Feed Query Maximum Entries" more than 200? You probably
        don't want to return more than 100 feed events for any feed
        query. \* The following options are available in version 4.0.3
        or greater:
    -   Is the Feed Throttle Management Enabled is set to true? You want
        this set to true to throttle feed processing.
    -   Is "Update feed automatically" checked? If so, what is the
        update interval set for? Every 30 minutes should be sufficient.
    -   Is "Reload feed automatically on startup" checked? You may want
        to disable this.
    -   Is "Override server configuration" checked? This allows clients
        to override the server settings.
    -   Is "Limit number of items" checked? If so, what is the value for
        "Maximum news items"? You probably don't want more than 100.
    -   Is "Limit age of items" checked? If so, what is the value for
        "Days to keep news items"? You probably only want to keep items
        for 7 days.

For more information, see [work item
255974](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=255974).
Note that only RTC 4.0.3 clients support the Feed Throttling feature at
this time

#### Limiting the size of attachments

Attachments eat up DB space, and they hog bandwidth. Limiting the size
of these can help immediate performance and long term performance of
your system. The default limit on attachment size is 50MB (as of v4.x),
but you can adjust this. I would strongly suggest adjusting it lower,
and never higher than 50MB. Here is how you can do it:

1.  Login to EWM (CCM) as the admin user
2.  Go to Advanced Properties
3.  Search for the
    com.ibm.team.workitem.service.internal.WorkItemRepositoryService
    entry in Work Item Component
4.  Edit the Maximum Attachment Size to a required value and save the
    changes

#### Limiting the size of source control files

Large files put in source control are the most common for large database
size and outages due to out of memory for different configurations.
There is no limit set as default for file or changeset size and you need
to consider if you want to store files larger than 1GB. You can
automatically limit changeset size according to [How to set the limit of
a file size for SCM on
RTC](https://www.ibm.com/support/docview.wss?uid=swg21419931). In RTC
6.0.5 there was introduced external repository feature which allows you
to store large files in external repository. You can find more
information [Enabling an external content repository for source
control](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.repository.web.admin.doc2Ftopics2Ftenableexternalcontentrepoforscm.html)
document.

#### Enabling synchronized channel write

If you still want to use large files (above 2GB) in your repository
under WebSphere, consider using synchronized channel write type
according to [Tuning WebSphere servers for Rational Team Concert
performance](https://jazz.net/library/article/1430) document.

### Scalability

Keep in mind that any single Jazz solution might contain multiple RTC
instances. As you reach the limits of what a single EWM instance can
support, there is no way to move projects to new EWM instances, and no
way to move workload off of the existing EWM instance.

For this reason, you should consider the deployment of new EWM instances
in a Jazz solution proactively, and you should do so before performance
issues become apparent on the existing EWM instance or instances.

### Use of content caching proxies

The use of content caching proxies allows a solution to offload some of
the processing that is associated with the retrieval of files from the
SCM system with EWM. The establishment of a content caching proxy will
allow requests for frequently accessed source code to be satisfied by
the content caching proxy, instead of having the request get routed to
the RTC instance, having the EWM instance request the resource from the
database, and then return this to the requesting user or process. In
solution environments where there are frequent builds, these proxies can
greatly reduce the load on both the EWM application instance and on the
database supporting that instance.

See the section on [concerns when using a content caching
proxy](ContentCachingProxyJazzSCM).

### Configuring the Java Virtual Machine (JVM) settings

One of the most important things that you configure are the JVM settings
that are used when you deploy the JTS. These settings often have a large
impact on the performance of your JTS application, and you should have
these tracked somewhere as part of your solution architecture
description. Often, it is best to start with the [default JVM
settings](https://jazz.net/wiki/bin/view/Deployment/ConfiguringAndTuningTheJVM)
suggested by the development team.

##### Related topics: [Configuring and tuning the JVM](ConfiguringAndTuningTheJVM), [Using content caching proxies for Jazz Source Control](ContentCachingProxyJazzSCM) [related-topics-configuring-and-tuning-the-jvm-using-content-caching-proxies-for-jazz-source-control]

##### External links: \* None [external-links-none]

##### Additional contributors: [KrzysztofKazmierczyk](Main.KrzysztofKazmierczyk) [additional-contributors-krzysztofkazmierczyk]

META:TOPICMOVED{by="sbeard" date="1385848203"
from="Deployment.ConfigureRTC" to="Deployment.ConfiguringAndTuningRTC"}
