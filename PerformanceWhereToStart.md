META:TOPICINFO{author="sbeard" date="1509370460" format="1.1"
version="1.21"} META:TOPICPARENT{name="WebHome"}

# Performance: Where to start? [performance-where-to-start]

DKGRAY Cross-cutting theme technical leaders and senior editors:
Main.VaughnRokosz, Main.HongyanHuo, Main.StevenBeard ENDCOLOR

TOC{title="Page contents"}

## When we think of performance, what do we mean?

Performance has many dimensions. Depending on who you ask (and perhaps
when) you will receive wide-ranging answers as to what dimension is most
important. In general the best software performance is never noticed -
users successfully complete their activities without any thought of
performance. In the Jazz portfolio, performance starts with response
time, scalability, and throughput. Further considerations are
performance goals (non-functional requirements), pre-production
performance testing, and post-deployment performance monitoring. Each
has a place in the overall performance picture.

## Different views of performance

### End user view

End-user performance looks at the overall performance of the web site
from the users perspective.

-   Why is the system so slow ?
-   Response time: Amount of time elapsed from when a request is sent to
    when a response is received.
-   Throughput: Number of requests per second
-   Load: Number of users concurrently using the Web site

### System view

System view of performance focuses upon overall health of the system by
monitoring critical system components and resources.

-   Is the application server running OK?
    -   Is CPU over-utilized? Is system paging memory to disk? How much
        time spent is accessing disk?
-   What is the application server's health?
    -   How much time is the JVM spending doing garbage collection? What
        is the WebSphere thread pool utilization?
-   Memory requirements; Server startup; Database health

### Application view

Application view of performance focuses upon performance of the
individual application components involved in processing the user
request.

-   Why are queries so slow? Why does it take so long to load a page?

## How the Deployment wiki can help

When a product doesn't perform the way we expect, we may turn to the
help pages, user manual or instructions to see if there's something
we're missing. Sometimes a product that we know and use frequently may
seem to behave slower. Often when we're pretty sure the problem isn't
something we're not doing right, we attribute the poor behavior to the
product and label it a performance problem.

Understanding and fixing performance problems can be very difficult, as
modern software applications can consist of many different inter-related
layers and components such as networks, databases and web servers.
Problems with any one of these components or layers can degrade
performance.

Our goal with this "Where to start?" page is to help you comprehend
issues and aspects which can influence CLM performance.

### Understand product requirements

-   [System Requirements in the Installing, Upgrading and Migrating
    section](DeploymentInstallingUpgradingAndMigrating)

### Start with a sound topology

-   [Standard deployment topologies
    overview](StandardTopologiesOverview)

### Tuning

-   [Configuring and tuning](DeploymentAdminstering)

### Monitoring

You can't improve what you don't actively monitor.

-   [Monitoring](DeploymentMonitoring)

### Performance testing

If you're thinking of taking on the complex task of Performance testing,
look at:

-   Part 1: [Creating a performance simulation for Rational Team Concert
    using Rational Performance Tester](HowToPerformanceTestCLM)
-   Part 2: [Tuning Jazz systems to support performance
    testing](TuningForPerformanceTesting)

### Troubleshooting

If you have problems, look at our [performance
troubleshooting](PerformanceTroubleshooting) pages.

### For further help

-   [Troubleshooting resources](DataCollectionandSupportResources)

### Performance datasheets and sizing guidelines

Performance datasheets and sizing guidelines can be found here:
PerformanceDatasheetsAndSizingGuidelines

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [Use Rational Performance Tester to monitor Collaborative Lifecycle
    Management server
    resources](http://www-01.ibm.com/support/docview.wss?uid=swg27039566&lnk=uctug_ratl_dw_2013-10-11_whitepaper_clm)

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="where_performance_problems_can_live.jpg"
attachment="where_performance_problems_can_live.jpg" attr="h"
comment="Where performance problems can live" date="1376081099"
path="where_performance_problems_can_live.jpg" size="74774"
user="gcovell" version="1"}
META:FILEATTACHMENT{name="whenwetinkofperformancewhatdowemean.jpg"
attachment="whenwetinkofperformancewhatdowemean.jpg" attr="h" comment=""
date="1403553324" path="whenwetinkofperformancewhatdowemean.jpg"
size="94674" user="gcovell" version="1"}
