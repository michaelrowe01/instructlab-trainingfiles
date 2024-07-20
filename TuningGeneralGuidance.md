META:TOPICINFO{author="sbeard" date="1422035667" format="1.1"
version="1.12"} META:TOPICPARENT{name="DeploymentAdminstering"}

# Tuning general guidance [tuning-general-guidance]

DKGRAY Authors: [DanToczala](Main.DavidToczala) Build basis: CLM 2012,
Rational Team Concert 4.0.1, Rational Quality Manager 4.0.1, Rational
Requirements Composer 4.0.1 ENDCOLOR

TOC{title="Page contents"}

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

## Example of performance tuning realities

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
mpact, or a negative impact. When you see this happening in your
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

##### Related topics: [Deployment troubleshooting](Deployment.DeploymentTroubleshooting), [Deployment monitoring](Deployment.DeploymentMonitoring) [related-topics-deployment-troubleshooting-deployment-monitoring]

##### External links: [external-links]

-   [Installation
    topologies](http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fc_topology_overview.html)

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="BadPerformance.png"
attachment="BadPerformance.png" attr="h" comment="Bad Performance
diagram" date="1360942711" path="BadPerformance.png" size="26276"
user="dtoczala" version="1"}
META:FILEATTACHMENT{name="MediocrePerformance.png"
attachment="MediocrePerformance.png" attr="h" comment="Mediocre
performance diagram" date="1360942750" path="MediocrePerformance.png"
size="26438" user="dtoczala" version="1"}
META:FILEATTACHMENT{name="OKPerformance.png"
attachment="OKPerformance.png" attr="h" comment="Acceptable performance
diagram" date="1360942782" path="OKPerformance.png" size="26782"
user="dtoczala" version="1"}
