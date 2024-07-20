META:TOPICINFO{author="tfeeney" date="1590011225" format="1.1"
reprev="1.4" version="1.4"}
META:TOPICPARENT{name="DeploymentMonitoring"}

# JMX MBeans for ELM Application Monitoring [jmx-mbeans-for-elm-application-monitoring]

DKGRAY Authors: Richard Watts, Vishwanath Ramaswamy, Vaughn Rokosz,
Main.TimFeeney Build basis: 6.0.5 and later ENDCOLOR

TOC{title="Page contents"}

As part of our
[serviceability](https://en.wikipedia.org/wiki/Serviceability_(computer))
strategy for the ELM product suite, we provide detailed instrumentation
and best practices for collecting data on how your system is behaving.

[Managed beans
(MBeans)](https://docs.oracle.com/javase/tutorial/jmx/overview/index.html)
are "Java objects that represent a manageable resource, such as an
application, a service, a component, or a device". These objects are
available through a MBean Server or Java Management Extensions (JMX)
agent.

We have been working to instrument the ELM applications using managed
beans. We have implemented
[MXBeans](https://docs.oracle.com/javase/tutorial/jmx/mbeans/mxbeans.html)
which use a predefined set of data types that make consuming data from
the beans easier. There is no need to introspect the bean before
collecting the data.

\* [Overview](CLMMBeansOverview) \* [MBeans Reference
Guides](MBeansReference) \* [MBeans Usage Guides](MBeansUsage)
