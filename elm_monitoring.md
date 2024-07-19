# CLM Monitoring

**_A guide on how to improve the reliability and predictability of your CLM_**

**_System._**

By Vishwanath Ramaswamy, Vaughn Rokosz, Richard Watts

Covers: CLM 6.0.5 and beyond

## Introduction

Complex distributed systems require an automated, layered approach of

monitoring. Most organizations monitor key parts of their infrastructure, but this

typically stops at the application layer because it can be difficult to know what

and how to effectively monitor applications without an understanding of the

application architecture.

This article describes some key application metrics to monitor and a high

level overview of the distributed application architecture. We will describe how

to enable managed beans and briefly touch on what managed beans are.

## Application Reliability and Predictability

Why monitor your applications?

Application monitoring has a proven track record of improving the

predictability and reliability of your applications.

### Monitoring in general is looking at trends over time. This trending is done by
 collecting data, through polling (pull) or publish (push) models. Once the data is


-----

### available in some form, it needs to be collected, stored, and we can look at trends in the data. Most monitoring applications have analytical tools that allow the administrators to aggregate the data in charts or reports.

 Applications do not, as a general rule, fail instantly, they degrade over time.
 Application monitoring tools collect metrics over time that can be used to perform trend analysis. Rules can be applied to these trends to alert administrators to situations that require intervention.

 Armed with trends, you can further refine your rules to ensure that
 administrators are notified in advance of issues and they can proactively resolve them before outages occur.

 These trends help with the “Why”… An application suddenly failed. Users
 are seeing behavior that they can’t explain and neither can the administrator. Armed with application metrics and trend information, administrators are more comfortable with diagnosing the behaviors that led up to a failure and can better determine ways to avoid it in the future.

A monitoring system with warnings and alerts allow you to see potential

issues and give you time to take steps to proactively address the problem. In

cases where the system does something unexpected, you can look at specific

trends to see if these can lead you to what caused the problem (resource intensive

scenarios for example).

Armed with the information, you can build better warnings and alerts that

allow you to proactively manage your systems.

**Use Cases**

When developing a monitoring strategy, it is important to understand your


-----

stakeholder use cases to ensure that you are monitoring those parts of the

system, they use the most. This is part of your “what” to monitor.

**Service Level Agreement**

Depending on stakeholder expectations, you need to customize your

monitoring to help you meet your service level agreements. This may require

additional monitoring or more warnings than we would recommend in a basic

deployment.

Typically you measure system availability or application uptime as the

minimum bar. Some stakeholders use a combination of metrics that measure

response and/or transaction times to build a better picture of how the system is

responding.

## Java Management Extensions

As part of the CLM Serviceability strategy, we have implemented J2EE

industry standard managed beans which are defined and part of the Java

Management Extensions specification. This gives us a defined, well understood

way of providing information about what our applications are doing.

Java Management Extensions (JMX) are a standard component of the Java

Platform. It specifies a method and design patterns for developers to integrate

applications with management or monitoring software by assigning Java objects

with attributes.

It is dynamic, making it possible to monitor resources when they are created,

implemented or installed. For this article, we only focus on the monitoring

aspects of JMX and managed beans but the specification covers more than that.

The Java objects, called managed beans (mBeans) follow the design pattern

described in the JMX specification and provide common access points for agents


-----

to consume data from the mBeans. In the CLM implementation, we leverage

MXBeans which are a documented variant of managed bean. MXBeans use a

predefined set of datatypes making them portable and easy for any monitoring

client to consume.

**Jazz Application Framework SDK**

Many of the jazz based applications are built on a common framework called

the Jazz Application Framework SDK. These applications all share a common set

of services and the MXBeans are part of that common set of services.

Applications built on other application frameworks will be covered in a future

article.

**Jazz Service Invocation Architecture**

When we set out to instrument the application, we needed to look at the

architecture from a slightly different perspective, the service invocation

perspective. This gives us a better picture of where specifically we needed to

build MXBeans based on entry points to provide data to a monitoring system.

This is a diagram of the Service invocation architecture with the kinds of data

you can get from the JMX service.


-----

## What should you monitor in CLM

Application monitoring should compliment your enterprise monitoring

strategy. If you have a hybrid environment (a mixture of on-premises and SaaS or

PaaS services), it is important that the key distributed services are monitored at

the network, operating system, database and application levels. A topology

diagram of your CLM system will show you the potential points of failure and

the applications that should be monitored.

For CLM Specifically, we have six key application areas that should be

monitored. We provide much more instrumentation, but these key areas to

monitor will get you started.

**(1) Alerts on Active Services Summary Bean**

An active service consumes CPU on the server while it is running. If the

number of active services exceeds the number of processors available on the


-----

server, then the server is most likely nearing 100%CPU utilization and the

performance of the server will suffer.





|Attribute|Description|Threshold|
|---|---|---|
|longestDuration|longestDuration looks at the active service that has been running the longest, and reports how long it has been running (in ms).|ALERT: longestDuration > 30s|
|totalCount|Count of active services. Alert when the number of active services is nearing the number of processors available on the system. If multiple applications are hosted on one server, then take the sum of the totalCount attribute across all mbeans and alert on that. AvailableProcessors attribute is reported by the java.lang:type=OperatingSystem mbean.|ALERT: totalCount > AvailableProcessors WARN: totaCount > 75% of AvailableProcessors|
|countExceedingThresh oldDuration|This is the number of active services that have been running longer than a specified threshold (5s by default). Long-running active services consume CPU, so this is an indication that the scalability of the server may be compromised.|ALERT: countExceedingThresholdDur ation > 0|
|cpuRatio|totalCount / AvailableProcessors. Can be used instead of totalCount if the AvailableProcessors metric is not available or hard to access. If multiple applications are hosted on one server, then take the sum of the cpuRatio across all mbeans and alert on that.|ALERT: cpuRatio > 1 WARN: cpuRatio > .75|


You would use the active services summary metrics to compliment system

CPU utilization metrics. The Active Services Summary bean is part of the

**HighFrequencyMetricsNodeScopedTask and is enabled by setting the Enable**

**_Active Services MBean to true._**

Use the Active Services metric bean to collect details about all of the active

services for drilling down into what is causing the alert conditions.


-----

Long running active services indicate one of two things; (a) performance will

degrade if the system is overloaded, resulting in large numbers of long running

active services, (b) long running active services under low load conditions

suggest that the scalability of the system is compromised. If enough people

access the slow service at once, the server will overload.

**(2) Alerts on Resource Usage beans (JDBC, RDB mediator)**

The Java Database Connectivity (JDBC) and Relational Database mediators

are used to monitor access to critical application resources. Both (JDBC and RDB)

sets of beans should be monitored, there have been cases where RDB beans alert

before JDBC beans.

If there are multiple applications installed on a server, then alert on each

mbean separately. Don’t aggregate across multiple mbeans.

If the JDBC or RDB mediator pool have non-zero queue lengths, then the

server is throttling access to the database. Increase the JDBC or RDB mediator

pool size in the Server->Advanced Properties.

The usage percentage can be used to warn you when you are close to

exhausting the pools, so you can plan to increase the pool sizes during your next

maintenance window (a server restart is required).

Active connections gives you similar information to usage percentage — you

can divide the active connection value by the PoolSize to get a usage percentage.

It is recommended that you alert on usage percentage and graph active

connections.


-----

|Facet|Attribute|Description|Threshold|
|---|---|---|---|
|Queue length|value|If the size of the resource pool is exceeded, this value becomes non-zero and indicates how many threads were waiting for a connection.|ALERT: value > 0|
|Usage percentage|averageOverInterval|Active Connections / Pool size at the time of last collection.|ALERT: averageOverInterval > 90% WARN: averageOverInterval > 80%|
|Active connections|value|This is the number of active connections at the time of last collection.|Alert on usage percentage instead of active connections|


**(3) Database metrics bean**


Average times for SQL operations will usually be under 1ms. Periods of long

response times can indicate a database problem. Sustained periods of poor SQL

performance may also be a side effect of increasing data volumes, or complex

CLM queries/reports.

com.ibm.team.foundation.sqlactivity:name=jts,type=sqlActivitySummaryMet

rics,sqlStmtType=[read, write, other]

If SQL thresholds are exceeded, make sure that the database statistics are up

to date.




|SQLStmtType|Attribute|Description|Threshold|
|---|---|---|---|
|read|sqlAverageTim e|Overall average time (in ms) for all SQL read operations.|ALERT: sqlAverageTime > 250ms|


-----

|write|sqlAverageTim e|Overall average time (in ms) for all SQL write operations.|ALERT: sqlAverageTime > 500ms|
|---|---|---|---|
|other|sqlAverageTim e|Overall average time (in ms) for rollbacks and commits.|None|


If there are multiple applications installed on a server, then alert on each

mbean separately. Don’t aggregate across multiple mbeans. It is important to

remember that the SQLActivityMetricsTask updates less frequently (60

**minutes) instead of the typical 15.**

**(4) Liberty and Java Virtual Machine beans**

If the CPU utilization of the JVM (ProcessCpuLoad) is much lower than the

overall CPU utilization, there may be other processes competing for CPU on the

CLM server. If the overall CPU usage is high, you should investigate to see if

there are multiple services than can be disabled or moved to other systems.

The java.lang:type=OperatingSystem and

WebSphere:type=ThreadPoolStats,name=Default Executor are managed beans

that are enabled by default.

If the JVM uses too much physical memory, it can be killed by the operating

system. Generate an alert if the JVM grows to be 80% of the available physical

memory.

ActiveThreads can be used instead of active services summary mbean, to alert

when service calls are backing up.

|MBean|Attribute|Description|Threshold|
|---|---|---|---|


-----

|java.lang:type=OperatingSys tem|SystemCpuLoa d|Overall CPU utilization (from 0 to 1).|ALERT: SystemCpuLoad > .9 WARN: SystemCpuLoad > .8|
|---|---|---|---|
|java.lang:type=OperatingSys tem|ProcessCpuLo ad|CPU utilization of the JVM (from 0 to 1).|ALERT: ProcessCpuLoad/ SystemCpuLoad < .5|
|java.lang:type=OperatingSys tem|ProcessPhysic alMemorySize|Memory used by the JVM.|ALERT: ProcessPhysicalMem orySize/ TotalPhysicalMemory > .8|
|WebSphere:type=ThreadPo olStats,name=Default Executor|ActiveThreads|Number of active threads (web containers) used by Liberty.|ALERT: ActiveThreads > AvailableProcessors WARN: ActiveThreads > 80% of AvailableProcessors|


**Note:** **_AvailableProcessors is a java.lang:type=OperatingSystem ->_**

AvailableProcessors attribute. You would be building a rule based on attributes

from two separate managed beans.

**(5) Diagnostics bean**

The diagnostics managed bean is part of our server health metrics and

performs a series of diagnostic tests on the system. This is also an administrative

task in the Admin UI. This mbean updates every 70 minutes. The diagnostics

bean data is collected when the DiagnosticsMetricsTask is enabled.




|MBean|Attribute|Description|Threshold|
|---|---|---|---|
|Diagnostics|com.ibm.team.f oundation.diag nostic:name=< < contextRoot>>, type=diagnosti cMetrics,testId =*|This provides the results of the server diagnostics which by default runs every hour. This is useful to track the status of the periodic execution of server diagnostics.|ALERT: Throw an alert if any of the diagnostic result shows a failure|


-----

There are several diagnostic tests, and these vary by application. To monitor

your diagnostic output (only alerting on failures) you need to build a pattern

based rule. You would build these rules based on each tool.

_com.ibm.team.foundation.diagnostic:name=<<contextRoot>>,_

_type=diagnosticMetrics,_

_testId=*,_

**_statusDesc=failure_**

The testId would be a wildcard, meaning all diagnosticMetrics, and the

attribute to evaluate is statusDesc looking for the failure value.

**(6) Resource Intensive Scenarios Summary bean**

There are system and user actions performed on CLM systems that can be

resource intensive. When these actions occur on systems that already taxed, the

system can slow down or potentially run out of resources. We recommend

monitoring these scenarios to see if they are negatively impacting your system.

The resource intensive scenarios data is collected when the Scenario Metrics

MBean is enabled, which is part of the MetricsCollectorTask and an expensive

scenario is actually run.

[You can review the details on resource intensive scenarios on the Jazz.net](http://Jazz.net)

[deployment wiki (https://jazz.net/wiki/bin/view/Deployment/](https://jazz.net/wiki/bin/view/Deployment/CLMExpensiveScenarios)

[CLMExpensiveScenarios).](https://jazz.net/wiki/bin/view/Deployment/CLMExpensiveScenarios)

|MBean|Attribute|Description|Threshold|
|---|---|---|---|


-----

|Resource Intensive Scenarios – Summary Elapsed time in milliseconds|com.ibm.team.f oundation.coun ters:name=<<c ontextRoot>>, type=counterM etrics, group=scenario s,facet=elapse d time in millisecs,count erNameAndId =summary_*|This provides the counts and average response time for all the resource intensive scenarios in the system during the collection interval. This is useful to understand how the resource intensive scenarios are performing and track any degradation in their response times.|ALERT: Throw an alert if Elapsed time (averageOverInterval) is greater than 120s WARN: Throw a warning if countOverInterval is greater than 3 ALERT: Throw an alert if countOverInterval is greater than 5|
|---|---|---|---|


This is another pattern based rule where you are looking at the

averageOverInterval and countOverInterval attributes in all of the resource

intensive scenarios. They would look something like this.

_com.ibm.team.foundation.counters:name=<<contextRoot>>,_

_type=counterMetrics,_

_group=scenarios,_

_facet=elapsed time in millisecs,_

_counterNameAndId=summary_*,_

**_averageOverInterval > 120000_**

_com.ibm.team.foundation.counters:name=<<contextRoot>>,_

_type=counterMetrics,_

_group=scenarios,_

_facet=elapsed time in millisecs,_

_counterNameAndId=summary_*,_

**_countOverInterval > 3_**

_com.ibm.team.foundation.counters:name=<<contextRoot>>,_

_type=counterMetrics,_

_group=scenarios,_


-----

_facet=elapsed time in millisecs,_

_counterNameAndId=summary_*,_

**_countOverInterval > 5_**

## Enabling Managed Beans in CLM

We will be enabling the metrics collector tasks related to the specific managed

beans in the six categories we want to collect data for. To start, the administrator

must navigate to the Admin UI -> Manage Server -> Advanced Properties and

enable the serviceability services that generate the mxbean data.

Active Services Summary Bean (1) is part of the

**HighFrequencyMetricsNodeScopedTask and can be enabled by setting etting**

the Enable Active Services MBean to true.

Resource Usage Beans (2) are enabled through the MetricsCollectorTask, by

setting the Enable Resource Usage MBean to true.

Database Metrics Bean (3) is enabled through the SQLActivityMetricsTask by

setting the Enable SQL Activity Metrics MBean to true.

Liberty and JVM (4) Beans are enabled by default. There is nothing for you to

do to see attributes from these beans; (a) java.lang:type=OperatingSystem (b)

WebSphere:type=ThreadPoolStats,name=Default

Diagnostics Bean (5) is enabled through the DiagnosticsMetricsTask by

setting the Enable Diagnostic Metrics MBean to true.

Resource Intensive Scenarios Summary Bean (6) is part of the

**MetrictsCollectorTask and is enabled by setting the Enable Scenario Metrics**

**_MBean to true._**


-----

It is important to remember that enabled beans will only display data in

RepoDebug, or your monitoring application after the update interval. If there is

no information (for example resource intensive scenarios have not occurred), you

will not see a MBean in RepoDebug until there is data to show.

## Troubleshooting

Below are some basic troubleshooting topics. The JMX service has been

around for a long time, we have tested most of our MXBeans with a variety of

commercial monitoring tools. Usually the problems have to do with enabling the

MXBeans, Data sampling, or specifics of your monitoring system.

**RepoDebug**

The RepoDebug (Repository Debugger) service is a development tool to look

at the internals of your Jazz based system. The development team uses it to

troubleshoot issues that are not obvious from the logs or the admin user

interface. It has a simple UI and while it supports some manipulation, that

should only be done under the guidance of IBM Support or Development. This

tool provides you a mechanism to look at a single update of the enabled

MXBeans. It is a simple way to make sure the MXBeans are enabled and

publishing data.

**Enabling RepoDebug**

The RepoDebug service is disabled by default. You must enable it from the

administrative console. To enable the RepoDebug service, the property

**com.ibm.team.repository.debug.enabled Must be set to TRUE in the advanced**

properties. There is no need to restart your server, once saved, JazzAdmins will

be able to see the RepoDebug ui.

[You can then navigate to https://server:port/context-root/repodebug](https://server:port/context-root/repodebug)


-----

Where context-root is the application context root, so the Jazz Team Server

[(jts) would be https://server:port/jts/repodebug. This might be different](https://server:port/jts/repodebug)

depending on how you define your CLM context roots in your enterprise.


-----

-----

Navigate to the mxBeans link which will list the current enabled managed

beans (Primarily Java and WebSphere Liberty). We will use these beans to

monitor the operating system and thread pools (item #4 above).

To save a mouse click, you can navigate directly to the MXBeans page by

[using the following URL: https://server:port/context_root/repodebug/](https://server:port/context_root/repodebug/mxBeans)

[mxBeans. The specific information will appear as attributes in a child page.](https://server:port/context_root/repodebug/mxBeans)

**Data Sampling**

By default, most of our managed beans update every 15 minutes. The sample

rate was determined based on a frequency that would show trends without

incurring too much overhead on the system. Some monitoring tools collect data

more frequently, but this can usually be adjusted. Increasing the update

frequency will place more load on the system, but give you more data to look at.

Collecting data faster than the update rate will result in duplicate data in your

monitoring system, and should be avoided.

**Baselines**

Some of the more advanced APM tools have baseline features which allow

you to take snapshots of all data collected for the system and use that data to

build alerts when there is significant deviation from the baseline. These can be

very useful, but only if your use cases are consistent.

**Alerting**

Commercial application monitoring tools can be configured to generate alerts

if thresholds are exceeded. The capabilities vary from tool to tool. Most trigger an

alert if a value exceeds a threshold for a specified amount of time or frequency.

Alerts and alert history can be viewed in the monitoring UI. Most of these tools


-----

offer notification features in the form of email, SMS messages and calls. Alerting

systems usually check for threshold violations every 10 seconds.

## Reference

[Java Management Extensions - http://www.oracle.com/technetwork/](http://www.oracle.com/technetwork/articles/java/javamanagement-140525.html)

[articles/java/javamanagement-140525.html](http://www.oracle.com/technetwork/articles/java/javamanagement-140525.html)

[JMX Architecture - https://en.wikipedia.org/wiki/](https://en.wikipedia.org/wiki/Java_Management_Extensions)

[Java_Management_Extensions](https://en.wikipedia.org/wiki/Java_Management_Extensions)

[CLM Monitoring Managed Beans Reference - https://jazz.net/wiki/bin/](https://jazz.net/wiki/bin/view/Deployment/CLMMonitoringMBeans)

[view/Deployment/CLMMonitoringMBeans](https://jazz.net/wiki/bin/view/Deployment/CLMMonitoringMBeans)

[Resource Intensive Scenarios - https://jazz.net/wiki/bin/view/](https://jazz.net/wiki/bin/view/Deployment/CLMExpensiveScenarios)

[Deployment/CLMExpensiveScenarios](https://jazz.net/wiki/bin/view/Deployment/CLMExpensiveScenarios)

[RepoDebug - https://jazz.net/wiki/bin/view/Main/RepoDebug](https://jazz.net/wiki/bin/view/Main/RepoDebug)


-----

