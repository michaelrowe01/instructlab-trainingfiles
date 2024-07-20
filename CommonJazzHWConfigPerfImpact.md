META:TOPICINFO{author="paulellis" date="1581000504" format="1.1"
version="1.22"} META:TOPICPARENT{name="PerformanceTroubleshooting"}

# Common Jazz hardware configuration and performance impact overview [common-jazz-hardware-configuration-and-performance-impact-overview]

DKGRAY Authors: [DanToczala](Main.DavidToczala) Build basis: CLM 3.x and
later ENDCOLOR

TOC{title="Page contents"}

Common Jazz hardware configurations and their impact on performance

In this section I will go over some of the broad principles to keep in
mind when deploying and configuring the hardware supporting your Jazz
solution. As I begin looking at the various elements of the physical
Jazz architecture, it is probably a good idea to remind ourselves of the
basic pieces of a Jazz solution architecture.

We will start at the top of this diagram and work our way down, as we
begin considering some of the hardware choices that you have and their
implications for Jazz performance.

## The Jazz Client

The Jazz client can be many different things. There are clients for
mobile devices, an Eclipse client, and web browser based clients. There
can also be specialty clients, based on the Plain Java Client that comes
with each release of the Jazz tools, which are created to ease
maintenance or automate certain operations within a Jazz solution. Jazz
clients need to have enough processing and memory to easily handle the
load placed on them. Since many of these clients support more than just
the Jazz tools, it is important to have a client that has significantly
more processing power and memory than is required by the Jazz
applications, since it will typically be running other programs and
utilities.

The web browser client needs to have an appropriate network connection
to handle the communications to the Jazz applications. It should also
have enough CPU and memory to run multiple web sessions. Performance of
web clients will vary based on network latency, browser performance, and
the browser JavaScript engine.

## The IBM HTTP Server (IHS)

The HIHS server accepts all of the traffic bound for the Jazz
applications, and routes it to the appropriate WebSphere (or Tomcat)
instance that is hosting a Jazz application. Often this will be
configured as a reverse proxy server, and hiding the implementation
details of the Jazz application servers.

**Note:** For more on reverse proxy servers and setting up a reverse
proxy server:

-   [Proxy server installation](InstallProxyServers)
    -   [Understanding reverse proxy](UnderstandingReverseProxy)
    -   [Configuring Enterprise CLM Reverse Proxies: WebSphere 8 and IHS
        8](ConfigureCLMEnterpriseReverseProxy)
    -   [Configuring Enterprise CLM Reverse Proxies: Apache and
        mod_proxy](ConfigureCLMEnterpriseReverseProxyWithApache)
    -   [Configuring Enterprise CLM Reverse Proxies: WebSphere 8.5 ND
        Proxy](ConfiguringEnterpriseCLMReverseProxiesWebSphere85NDProxy)

The primary issues and concerns with the performance of the IHS server
are primarily concerned with being able to handle the volume of requests
coming into it, and the ability to resolve SSH certificates. The things
that you can control that will impact the performance of the Jazz
solution are the specifications of the hardware supporting the IHS
server, and the session pool settings in IHS. I suggest a minimum of 2
CPUs (or 4vCPUs) and 4GB of memory on an IHS server. This is what I will
typically see in well performing Jazz solutions. The session pool
settings should be left at the default values unless there is reason to
believe that the HIHS server is impacting performance and the user
experience. By default, IHS will support 2000 concurrent connections.
When looking at these settings, it has been our experience that defaults
are almost always the best configuration, and the only parameters that I
have looked at in specific situations have been the Max Connections and
Connection Timeout parameters in IHS.

|  |
|----|
| \^ **Note:** To learn more about the HIHS session pool settings, see: [IBM Infocenter for WAS](http://pic.dhe.ibm.com/infocenter/wasinfo/v7r0/index.jsp?topic=/com.ibm.websphere.base.doc/info/aes/ae/tihs_remotesetup.html). |

## The Jazz Applications and WebSphere (WAS)

I group these two things together because they will reside on the same
hardware. The Jazz applications can be thought of as running inside of a
WAS instance. When dealing with jazz solution performance issues, most
of your investigations will begin here. The logs for the WAS instance
and the Jazz applications will often be the first places where issues
may be surfaced. This also happens to be where most configuration
mistakes and poor root cause determinations are made. Many of the issues
that I see are the result of a poorly configured WAS and Jazz
applications, or the allocation of insufficient resources to this
physical piece of the solution architecture. A typical node in a
distributed enterprise topology will have a single WAS instance
supporting a single Jazz application. It is strongly suggested that you
architect your Jazz solution in this way, because it allows you more
flexibility in the following areas:

-   Performance issues can be more easily isolated and debugged
-   Hardware resources can be easily added, if needed
-   Resources can be more easily moved, with no need for using server
    rename (when used in conjunction with a reverse proxy)
-   New server instances can be more easily deployed (since you know the
    performance, allocation, and configuration characteristics of your
    existing well-behaved application instances)

In this straightforward approach, I have found the following guidelines
to be helpful for determining the hardware resources to allocate, and
for the configuring of the WAS and Jazz applications:

-   Allocate at least 2 dual core CPUs per WAS container/Jazz
    application. If using virtualization, allocate at least 4 vCPUs.
-   Have a machine with at least 6GB of memory available, and dedicate
    at least 2MB to the JVM inside of WAS. The preferred configuration
    has a machine with 8GB of memory, with 4GB of this being assigned to
    the JVM.
-   If using a virtual machine (VM), make sure that the machine is not
    over-subscribed. In other words, make sure that the images running
    your WAS/Jazz application servers have memory and CPU allocated to
    them, and are not sharing it with other VMs.

|  |
|----|
| \*Note:\*Some may ask if using virtual machines is worthwhile, since I suggest not sharing the resources assigned to the WAS/Application VM. I find that it is worthwhile in that it allows you to easily add or remove memory or CPU from a VM, and also provides some portability, since the VM can be moved onto different physical hardware without any configuration changes. |

For the JVM, you should use the default settings for WAS. I suggest
using the settings indicated in the Infocenter for the various Jazz
products. In most Jazz implementations, IBM suggests use of the
following settings:

-Xmx4G -Xms4G -Xmn512M -Xgcpolicy:gencon -Xcompressedrefs
-Xgc:preferredHeapBase=0x100000000

The garbage collection algorithm used above is referred to as gencon,
and it will perform optimally for most situations. In some cases, with
particular workloads, it has been found that a modification of the
garbage collection algorithm can be beneficial for performance. For a
discussion of the various garbage collection algorithms and their impact
on performance, read [Java technology, IBM style: Garbage collection
policies, Part
1](http://www.ibm.com/developerworks/java/library/j-ibmjava2/) on the
IBM Support website.

The load on the system is determined by the workload, which is variable
and depends on the users and the usage models. Planning your server
needs based on concurrent user counts will not be accurate, but I
understand that it is often the only measure that some organizations
have available to them.

\|**Note:** When doing initial planning for a Jazz deployment, limit
concurrent user sessions on any given Jazz instance to the following:
RTC 200-500 RQM 100-150 RRC 100-150 JTS 400-2000

**PLEASE NOTE THAT THESE ARE EDUCATED GUESSES**! These are conservative
rule of thumb estimates. You should base any real planning of hardware
resources for the deployment of your Jazz solution on the workload that
you see on your system, since workloads for different deployments will
vary widely.

RRC must share a repository with the JTS. This does not mean that they
need to reside on the same WAS instance. For versions prior to RRC
4.0.1, an upper limit of 200 concurrent users per RRC instance is a good
rule of thumb. For RRC 4.0.1 and beyond, an upper limit of 400
concurrent users per RRC instance is a good rule of thumb.\|

## The Database Server

The database server is the portion of most Jazz solutions that is often
out of the control of most solution architects and Jazz administrators.
Often the choice of database vendor will be a corporate directive, and
you will be told the database technology that you will be using. If you
decide to support your own database, you can choose the database
technology that you want. Keep in mind that Jazz licenses also carry an
entitlement for the use of DB2 Workgroup edition as part of the Jazz
licensing agreement.

However, there are some general things that you can do to help improve
the performance of your Jazz solution. These suggestions are valid for
all of the database technologies that support Jazz.

-   Make sure that your database has sufficient physical memory and
    enough allocated memory to perform a lot of data transfers. All of
    the REST based objects will need to be stored and retrieved here,
    and the rest of the solution architecture depends on the repository.
    Dont try to cut costs, make sure that the foundation for your
    solution is solid.
-   Your database should be on a dedicated server. While it is
    technically possible to install the database software onto the same
    machine as other software, the load on the database is heavy (since
    almost every user action implies multiple database events, like
    queries, inserts, or modifications). Deploy the database on a
    dedicated database server.
-   Monitor the performance of your database. Do not go overboard with
    monitoring, since excessive monitoring can lead to performance
    degradation of the database software. I suggest monitoring the
    amount of data (inbound and outbound), the number of queries over
    time, and some measure of the amount of time from the receipt of a
    SQL request to the time a response is generated.

## The Network

The key performance indicator for a network is speed. Bandwidth is only
a concern if the lack of bandwidth causes a reduction in speed. The key
thing to find out is if your organization monitors its network, and to
find out if there is any way for you to get a look at the monitoring
data. Often a slowdown in Jazz performance can be traced to a general
network slowdown. Being able to access the network performance data will
help you determine if the network is having an adverse impact on your
performance, and also help you eliminate network issues when
troubleshooting problems.

## The LDAP Server

Most Jazz architects and administrators will have no control over the
LDAP configuration used to support identity authentication. You should
just monitor the connectivity to the LDAP resources provided, and make
sure that you have an established procedure for onboarding new users of
the Jazz solution, that makes allowances for any corporate procedures
surrounding changes to LDAP.

## The Operating Systems

Jazz works on a variety of operating systems. Some people will suggest
that one operating system will perform better than another, but a
typical Jazz solution, with sufficient hardware and network resources,
will not show noticeable performance differences based on the operating
system deployed.

A Jazz administrator should take care to keep the operating system
properly patched, and make sure that they have left sufficient memory
for OS operations (like network communications and file manipulation)
when allocating memory to the JVM that hosts the Jazz application. I
suggest leaving half of the available memory on the machine hosting the
Jazz application allocated to the OS, and the other half allocated to
the JVM supporting the Jazz application.

## Conclusions

In this section of the document I have looked at the hardware and
software configuration of the systems supporting the Jazz
infrastructure, and some of the observed impacts that these can have on
Jazz performance.

It is important to keep in mind that there is no single right
configuration for a Jazz solution. Different organizations will have
different usage models, different workloads, different processes, and
different software development cultures. In addition, the people using
the Jazz infrastructure will change over time. There may be new
employees, new processes, and more efficient ways of doing things.

However, while every Jazz solution will be unique, and have its own
characteristics, the general concepts should hold true. It is important
to have an idea of some of the characteristics of how Jazz provides its
capabilities, so future scaling needs can be better anticipated.

It is also important to keep in mind that Jazz performance is dependent
on a number of different variables. When dealing with Jazz deployments,
you may make tuning changes which will greatly improve performance,
which you do not see immediate results from. That is because other areas
of your solution architecture are throttling performance.

In the scenario pictured above, a poorly configured WebSphere
installation is causing performance issues that are making end users
unhappy. Notice that the other major impacts on performance are tuned
with varying degrees of precision. So although we have our Linux
filesystem perfectly tuned, our end users never see the benefits of
this. The same holds true for Jazz applications. These are tuned well,
but due to the bottleneck presented by the poorly configured WebSphere,
we can improve our tuning of the Jazz applications and our end users
would never see any benefit in terms of improved performance.

In the next diagram, we have addressed our poorly tuned WebSphere
issues. This has resulted in some improved performance for our end
users, but the results may not be as dramatic as we had hoped. This is
because we are now being throttled by poorly configured JVM settings.

So once we address the poorly configured JVM, we realize additional
improvements in performance, and our end users appear to be satisfied.
At this point, if we wanted to further improve performance, we would
need to address the bottlenecks in both DB2 and our usage model (the way
that we use the Jazz applications). These are often the toughest
scenarios to deal with, since isolated changes seem to have either no
impact, or a negative impact. When you see this happening in your
environment, then you should believe that you have multiple chokepoints.

The key thing to remember is that as you relieve pressure from one area
of the architecture, you will increase the pressure on other areas. So
if we increase the throughput at the web server layer, we end up putting
more pressure on the backend database, since more requests are now
passing through to this layer within any given time period. I have heard
it compared to a balloon filled with water, as you squeeze one end, the
other end expands.

When working on Jazz solution performance, realize that at some point
you will reach a point of diminishing returns. Tune your various areas
of the architecture for best performance, but also realize when it is
time to stop tuning, and time to scale with more infrastructure and/or
Jazz application instances.

## Common Performance Impacts

In a number of customer environments we have observed some common
patterns and issues that lead to degraded performance. Anyone who is
responsible for the health, performance, and general availability of a
Jazz based solution should be aware of these common issues.

### Common architecture issues

**Hardware Configuration and Placement** - sometimes the hardware is not
well positioned in terms of physical location, or network configuration.
Jazz application servers and their supporting infrastructure should
ideally be in the same physical location, and should ideally be on the
same subnet. See [Common Jazz Hardware Configurations Impact on
Performance](CommonJazzHWConfigPerfImpact) for more details.

**Server Rename Has Been Performed** - if you have done a server rename
operation (initially available in the 4.x versions of the Jazz tools) in
your environment, then you will see a degradation in performance due to
the URI remapping that needs to be done. This performance penalty is
usually in the 5 range, but will vary from installation to installation.

### Common infrastructure issues

**JVM is incorrectly configured or sized** - Often a JVM that is well
tuned when initially deployed, will slowly become less so as new users
and projects are added to the Jazz application environment. For example,
a properly sized and configured JVM supporting an RQM instance with 100
users spread over 5 projects may perform well initially, but will not
perform well a year later as the RQM application now need to support 400
users spread over 50 projects. See [Why is my Server
Unresponsive?](WhydoIgeterror500) for more guidance on JVM
configuration.

**Database not Optimized** - Often the repository databases will benefit
from some periodic optimization, through the indexing of particular
tables in the database. See the applicable section under tuning
databases on the [Deployment Administering](DeploymentAdminstering)
page.

### Common application issues

**Plans Too Large** - Users may complain that large plans take too long
to display. See [Why does my RTC Plan take so long to
load?](RTCPlanLoading) for more details.

##### Related topics: None [related-topics-none]

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="highleveldiagramofjazzarch.png"
attachment="highleveldiagramofjazzarch.png" attr="h" comment=""
date="1380295879" path="highleveldiagramofjazzarch.png" size="112525"
user="gcovell" version="1"} META:FILEATTACHMENT{name="thruput_red.png"
attachment="thruput_red.png" attr="h" comment="" date="1380296227"
path="thruput_red.png" size="15149" user="gcovell" version="1"}
META:FILEATTACHMENT{name="thruput_yellow.png"
attachment="thruput_yellow.png" attr="h" comment="" date="1380296243"
path="thruput_yellow.png" size="14739" user="gcovell" version="1"}
META:FILEATTACHMENT{name="thruput_gren.png"
attachment="thruput_gren.png" attr="h" comment="" date="1380296273"
path="thruput_gren.png" size="14822" user="gcovell" version="1"}
