META:TOPICINFO{author="natarajan_2ethirumeni" date="1669019557"
format="1.1" version="1.6"}
META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Impact of network latency on Engineering Lifecycle Management (ELM) user performance from remote locations DKGRAY Authors: Main.StevenBeard Build basis: This is general guidance suitable for all ELM/CLM versions [impact-of-network-latency-on-engineering-lifecycle-management-elm-user-performance-from-remote-locations-dkgray-authors-main.stevenbeard-build-basis-this-is-general-guidance-suitable-for-all-elmclm-versions]

ENDCOLOR

TOC{title="Page contents"}

Poor network latency from a user's location to the ELM servers can
significantly impact user performance. Firstly, this page will outline
the ranges of network latency that should provide good to acceptable
user performance from remote locations and above what latency the
performance is likely to be compromised and generally unacceptable.
Secondly, we will outline approaches to mitigate poor network latency.

## Overview of the impact of network latency

As you can see from the ELM Performance Health Check widget:

-   Less than 250ms network latency should contribute to good to
    reasonable user experienced performance overall

<!-- -->

-   Between 250ms to 400ms network latency the overall user experience
    performance will be noticeably affected, with some types of user
    interactions that require multiple operations becoming unacceptably
    slow:
    -   Certain user interactions that fundamentally require multiple
        operations will have their user experienced performance
        noticeably effected.
    -   Of the ELM products, IBM Engineering DOORS Next (DOORS Next) is
        most affected because many of the user interactions require
        multiple operations to provide the required functionality
        whereas IBM Engineering Workflow Management (EWM) often has
        simpler interactions with less operations.
    -   Within this range of network latencies some
        interaction/operation of the ELM products will be unacceptably
        slow from a user experienced performance perspective, therefore
        we usually recommend alternative approaches to effectively
        reduce the latency such as Citrix/Windows Terminal Server (see
        later).

<!-- -->

-   Above 400ms the overall user performance will be compromised and
    generally unacceptable:
    -   Within this range of network latencies some
        interaction/operation of the ELM products will be unacceptably
        slow from a user experienced performance perspective, therefore
        we usually recommend alternative approaches to effectively
        reduce the latency such as Citrix/Windows Terminal Server (see
        later).

If you choose the shortest route, the maximum distance between the two
locations will never be more than halfway around the planet, which is
about 20,000 km. Considering that Ping goes to a destination and then
back again, the packet sent by Ping would travel 40,000 km, the
equivalent of a trip around Earth. - [Theoretical vs real-world speed
limit of
Ping](https://www.pingdom.com/blog/theoretical-vs-real-world-speed-limit-of-ping/)

Based upon the theoretical speed of light that would be 134
milliseconds, but with network routing, repeaters and switches, the
zigzag route that will really be taken and the inefficiencies of light
transmission through fibre optic cable, this will more realistically be
264ms (2 x theoretical), but within the usually acceptable range of
latency for ELM products.

So, if your ELM servers being hosted in Germany, the theoretical and
reasonable network latency from worldwide remote development sites would
be:

| Location | Distance | Theoretical Ping time | Realistic Ping time (2 x theoretical) |
|:---|:---|:---|:---|
| Beijing, China | 7,850km | 53ms | 106ms |
| Bangalore, India | 7,360km | 49ms | 98ms |
| Tokyo, Japan | 9,440km | 63ms | 126ms |
| Sacramento, USA | 9,170km | 61ms | 122ms |

All well under 250ms, which should contribute to good user experienced
performance overall.

## Approaches to mitigate poor network latency

We have worked with a number of customers to monitor the network latency
over their intranet from remote locations. Unfortunately, it is quite
common for the intranet latency from remote locations to be very poor
over 400ms and some times up to 1000+ms! In this situation, the customer
can try to improve the network latency to the specific locations, which
can be very costly, or try using the internet for the majority of the
network hops and only come back into their intranet via a VPN gateway at
the datacenter where the ELM servers are hosted. Typically the latency
over the internet from a remote location is better than a companies
intranet, sometimes dramatically better, and typically under 250ms
resulting in good user performance.

We have observed at some customers their local wireless network can
result in significantly higher latency from the client machines to the
WAN. Using a wired connection will resolve this issue. If the overall
network latency is poor, this should be investigated.

There are a few ways to tune ELM to partially mitigate poor network
latency, such as a [Squid content caching proxy servers for EWM Software
Configuration
Management](https://jazz.net/wiki/bin/view/Deployment/SquidProxyJazzSCMWindows),
but fundamentally our tools are user-interactive applications that rely
upon reasonable network latency from the clients to the ELM servers.
Where that is not possible, the best solution is to use a remote
terminal solution such as Citrix or Windows Remote Desktop as is the
case with many other third-party applications. A few customers have
found that going over the internet and coming back into the WAN via a
VPN Gateway near the ELM servers is faster than going across the
corporate WAN!

Optimizing the server-side performance will help with the overall user
performance but cannot completely mitigate poor client to ELM server
network latency. There are product specific sizing and tuning guides in
the deployment wiki e.g. [7.0 performance: IBM Engineering Requirements
Management DOORS Next](RequirementsManagement70Performance).

Overall user experienced performance also depends upon the time it takes
to process the operations server-side between the application and
database servers, so lack of sufficient systems resources and/or very
high load can independently result in poor user experienced performance.

##### External links: [external-links]

-   [Theoretical vs real-world speed limit of
    Ping](https://www.pingdom.com/blog/theoretical-vs-real-world-speed-limit-of-ping/)

##### Additional contributors: [additional-contributors]

META:FILEATTACHMENT{name="PerformanceHealthCheck.png"
attachment="PerformanceHealthCheck.png" attr="h" comment=""
date="1592582410" path="PerformanceHealthCheck.png" size="259804"
user="sbeard" version="1"}
