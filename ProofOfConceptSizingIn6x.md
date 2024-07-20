META:TOPICINFO{author="paulellis" date="1694168317" format="1.1"
version="1.17"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Proof of Concept Sizing when using Application Lifecycle Management capabilities in 6.x DKGRAY Authors: Main.PaulEllis Build basis: ALM 6.x [proof-of-concept-sizing-when-using-application-lifecycle-management-capabilities-in-6.x-dkgray-authors-main.paulellis-build-basis-alm-6.x]

ENDCOLOR

TOC{title="Page contents"}

This article intends to only discuss the limited use cases of a Proof of
Concept, and installations of 1-20 users, which we see exhibit similar
patterns and anti-patterns in terms of deployment. In general, a proof
of concept is usually synonymous with an evaluation. However, where
proof of concepts are to include real data as part of the evaluation,
then thought must be given to the topology from the very start. There
are excellent articles within this wiki on topologies for larger sizes,
as well as the blog post [Getting to a right-sized Jazz
environment](https://trfeeney.wordpress.com/2016/09/01/getting-to-a-right-sized-jazz-environment/),
which also discusses sizing considerations, but some of those are
outside the scope of this page.

With the introduction of advanced configuration management features in
Application Lifecycle Management (ALM) 6.x, the [Standard
Topologies](https://jazz.net/wiki/bin/view/Deployment/StandardTopologiesOverview#Evaluation_topologies)
now require more hardware than in releases prior to 6.x. If the
intention is to use the configuration management capabilities within
Rational DOORS Next Generation and/or Rational Quality Manager then you
need to adhere to the following guidelines.

Note: Engineering Lifecycle Management rearchitected DOORS Next (7.0)
and Lifecycle Query Engine (expected 7.0.3) to use relational stores
(Oracle/Db2 databases) which changes the considerations below.

## Why is a single-server topology no longer adequate for a Proof of Concept (PoC)?

As documented in the Evaluation topology, this was described as "The
evaluation topology does not meet the demands of a typical production
workload because of the limited scalability of the single application
server. While this topology is ideal for evaluations, demonstrations,
and training purposes realize that the data created in an evaluation
topology cannot be transferred to a scalable production environment when
the evaluation is complete."

The full list of applications within the ALM suite, prior to the 6.x
release stream was documented as an [Evaluation topology using
Windows/Tomcat](https://jazz.net/wiki/bin/view/Deployment/AlternativeSSEDeploymentTopologies5#SSE_V1_Evaluation_Windows_Tomcat)
: RTC, RQM, RDNG, DM, JTS, JRS, LQE, DCC, RELM and VVC, with the
CLMHelp, RM converter and admin applications all added too. This does
not even consider a reverse proxy setup, which quite often is added for
when the future expansion into an Enterprise Topology occurs.

The inclusion of configuration management capabilities in 6.x added a
Link Index Provider (LDX) and a Global Configuration Management (GCM)
application. This meant that if you were utilizing all of the ALM
applications, then there would be even more pressure on the server
during key moments of operation. Indeed, some experienced server strain
when using the Evaluation Topology in 5.x too when DCC (Data Collection
Component) and the Data Warehouse were collocated with the ALM
applications.

This situation is acerbated in 6.x with the inclusion of the Lifecycle
Query Engine (LQE) now being utilized by more than just RELM (Rational
Engineering Lifeycle Manager) and Design Manager. The main stream use
and it's fairly constant updates (to provide near real-time reporting)
necessitate some thought on how to deploy, even a simple setup.

The Evaluation topology was intended to be just that. A small setup to
trial features of the ALM suite, downloaded from jazz.net. In 2016, this
is better served by using the jazz.net sandbox, or doorsng.com for
learning about new features, but if a SaaS (Software as a Service) or
aaMS (as a Managed Service) option is not appropriate for you, then a
small on-premise setup should continue as detailed below.

## How ONE resource-intensive scenario can cause your PoC server serious harm

The sizing of a small setup is the same for 1 user as it is 10, or even
20. In many ways, your number of users are unlikely to be a major
consideration during your Proof of Concept phase, or indeed if you're a
deploying to a small number of users. The capabilities you wish to avail
of and the data which you work with will have a much more fundamental
impact on your decisions than a relatively small number of users.

There is an entire section of this wiki dedicated to
[monitoring](https://jazz.net/wiki/bin/view/Deployment/DeploymentMonitoring)
and another to
[performance](https://jazz.net/wiki/bin/view/Deployment/PerformanceWhereToStart),
but I have attempted to summarize below the cross-cutting considerations
in this one article.

### Considerations for RAM, CPU and disk Input/Output

When calculating a maximum server sizing, the first place we recommend
perusing is the [Performance Datasheets and Sizing
Guidelines](PerformanceDatasheetsAndSizingGuidelines), along with the
[Sizing Strategy for 6.x](CLMSizingStrategy60) and then probably add in
additional information per application, for example, [DNG Sizing Guide
for
6.x](DOORSToDNGMigrationSizingGuide#Sizing_recommendations_for_Ratio).

As it is not our recommendation to collocate all of our applications on
one server in a production environment, there is minimal performance
testing done at this level.

In terms of the most fundamental sizing advice, we have always advocated
that the database server (if not Derby) be located on its own server.
Oracle, DB2 and SQL Server will directly compete for the key 3 resources
and unless they're plentiful, problems will occur in an intermittent and
unpredictable manner. Essentially, if you're using not using the Derby
database, you're not in a Proof of Concept mode and must upgrade
expectations along with the scale of your middleware!

The Lifecycle Query Engine, whilst not new to 6.x has been adopted by
the newly configuration managed applications and should only be
installed if you're intending to use this in DM, RDNG or RQM. This
application, like RDNG, is using a file based Jena index for its triple
stores and is particularly RAM and I/O intensive as it grows. The
importance of this to the overall ability to run in a single server is
highlighted in the [Lifecycle Query Engine Best
Practises](LifecycleQueryEngineBestPractices) article. If you're at the
point of splitting now into a 2-application-server topology for
evaluation, you should consider that along with the LQE, the Data
Collection Component, and the Reporting Service (also known as JRS)
would also benefit from being separated from the main applications.

In terms of RAM, CPU and Input/Output then these 3 rules apply,
especially when RDNG and LQE are being considered:

1.  Add processors to support more concurrent users 2. Add faster disks
    to support more data 3. Add memory to support more data (and more
    concurrent users)

### Why is the data more important than the number of users?

When calculating the minimum sizing, then there isn't the same
information available, but as you can see from [DNG recommended hardware
settings](DOORSToDNGMigrationSizingGuide#Recommended_hardware_settings),
the point in the graph for 1 user really depends on the data that is in
use. If you are testing RDNG using data from your current system, say
DOORS 9, then you may use the migration utility to import 10,000 objects
across for the PoC. You may have several groups who want to work with
their data, so multiple modules of 10,000 objects. As you can see you
will soon climb the vertical access, even before you have unleashed your
full use base.

In Tim Feeney's page [CLM Expensive Scenarios](CLMExpensiveScenarios) we
can see why data might be more important across more than RDNG. Each
application lists its Achilles heel(s) to show where data is going to be
a significant factor in your sizing decision. These expensive scenarios
again have largely been experienced during peak times on enterprise
servers, however the guide is an essential list for your ALM
Administrator to reference, if they are trying to explain a degrading
system in terms of performance and/or reliability.

### The silver bullet of using Java Heap for better performance

One of the common misconceptions that we see, especially with PoC setups
is that the Java heap size (the Xmx, Xms, and Xmn) settings in your
webserver are often overset. In the use case we are discussing, the most
useful equation to consider is quite simply:

RAM \> Java Heap + OS needs + Jena indices (from LQE and RDNG) + native
memory requirements for so many applications + 1GB for DirectByteBuffers
(the value of "-XXMaxDirectMemorySize" JVM argument)

Therefore, using all of the available RAM for the Java heap is not going
to be the silver bullet for performance that you would perhaps otherwise
infer from our guidance elsewhere, where we are considering a single
application, like RDNG, per server. The most appropriate setting for the
heap is usually 50 of RAM and then use Garbage Collection to tune up, or
down if you see Native Memory errors. See below for more on Native
Memory errors.

Before I move on to monitoring the system, I want to make a delineation
on Garbage Collection. It is important to know how much RAM, CPU etc you
have on your server. It may be important to see the contents of the
Javacore at the time of any crash, but what IBM Support need to see more
than anything for a performance issue for these use cases is the
verboseGC log!

[Point 4 of Must Gather
Information](https://jazz.net/wiki/bin/view/Deployment/MustgatherPerformanceProblemsInCLM#Information_gathering)
describes how to set this. The overhead is minimal however the
information is invaluable. In most cases of performance and instability
issues I have seen on small server installations, it is this log that
allows me to get to root cause faster and tune more effectively than any
other tool.

### Monitor your way to good Java health

Tuning the Java heap is outside of the scope of this topic, but below
are some links for further reading. In essence though, you should let
data make decisions for you without the panic of a system-down
situation, or guesstimates based on load.

WebSphere Liberty has a very simple Admin tool which will allow you to
see how the CPU, RAM and threads are performing, which is available with
any web server through Java Management Extensions (JMX). The simplest
guide to setting this up is, [Monitor your server with
JMX](https://jazz.net/wiki/bin/view/Deployment/JazzMonitoringThroughJMX),
which you no longer need to uncomment and restart the application
server. To then access this information, use JConsole, which is part of
the RTC client and documented
[here](https://jazz.net/wiki/bin/view/Deployment/CLMServerMonitoringJMXConnectionTroubleshooting).

A false positive we have seen on Windows is when we see [Competition for
the 4GB Windows memory
space](https://jazz.net/wiki/bin/view/Deployment/AttemptingToUseRTCOnWindowsOperatingSystemLeadsIntoNativeOutOfMemory).
This is nothing new, but we have seen LQE in particular, when collocated
with the other applications encounter this problem. As described in the
link, you can move to uncompressedrefs to resolve this, but in doing so
you're increasing the RAM requirements...just to note.

### Non functional testing and small servers

If you intend to perform non functional testing on a server then we have
written two articles on how we perform this and also what you need to
tune in order to allow the simulation not to encounter unrelated issues
to the tests being performed.

-   [How to performance
    test](https://jazz.net/wiki/bin/view/Deployment/HowToPerformanceTestCLM)
-   [Tuning for a performance
    test](https://jazz.net/wiki/bin/view/Deployment/TuningForPerformanceTesting)

## Conclusion

I imagine that having read all the advice above, many people just want
to see a minimum specification laid out in a simple table. With all the
caveats detailed above, and indeed in the related articles, we're
recommending.

It is possible to load all of the applications on 1 machine of around
16GB RAM and 4vCPU (my old laptop), it just isn't advisable and it isn't
going to be stable. In essence you're going to spend a lot of time
unnecessarily chasing phantoms and creating a poor perception for your
users.

We would therefore strongly recommend that if you are evaluating all of
the applications for a Proof of Concept, or indeed initially for a small
set of users with aspirations to trial the additional
applications/features and then roll out further capabilities, then you
should start with (my new laptop):

1 x \[32 GB, 8 vCPU and fast disk (SSD)\* - non-reporting applications\]
1 x \[32 GB, 8 vCPU and fast disk (SSD)\*\* - reporting applications\] 1
x \[Separate DB Server - 12GB RAM, 4 vCPU\]

\*SSD is required if RDNG is to be used \*\*SSD is essential if LQE is
in use with configuration management enabled projects in RM and/or RQM

[Lifecycle Query Engine
Sizing](https://jazz.net/wiki/bin/view/Deployment/LifecycleQueryEngineBestPractices)
is the definitive guide for sizing of the LQE machine. The advice, even
in this conclusion once again reiterates the opening paragraph where it
needs to be stated that any proof of concept that makes extensive use of
real data should evaluate the needs and not assume that evaluation is
based on just the number of users.

There is an article from 2014 for basic DCC guidance: [Performance
summary and guidance for the Data Collection Component in Rational
Reporting for Development
Intelligence](https://jazz.net/library/article/1433)

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TimFeeney, Main.StevenBeard [additional-contributors-main.timfeeney-main.stevenbeard]
