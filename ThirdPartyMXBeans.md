META:TOPICINFO{author="rwatts" date="1531304459" format="1.1"
reprev="1.1" version="1.1"}
META:TOPICPARENT{name="DeploymentMonitoring"}

# Java and Liberty Managed Beans DKGRAY Authors: Richard Watts, Vishwanath Ramaswamy, Vaughn Rokosz [java-and-liberty-managed-beans-dkgray-authors-richard-watts-vishwanath-ramaswamy-vaughn-rokosz]

ENDCOLOR

TOC{title="Page contents"}

Here is a brief list of suggested managed beans from the middleware
applications that are part of your CLM system. In the reference section,
we provide links to more detailed information.

### Java Virtual Machine Managed Beans

The two key managed beans we consume from the Java Virtual Machine are
the **Garbage Collector** and **Operating System** beans.

#### Garbage Collector

This managed bean is providing information about the Garbage Collector.
It is used for monitoring the virtual machine's garbage collection
metrics. The **CollectionTime**, **CollectionCount** should be used for
alerts.

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Key Attributes | Description | MBean | Frequency |
|:---|:---|:---|:---|
| CollectionCount | Returns the total number of collections that have occurred. This is set to -1 if the collection count is undefined for this collector. | [GarbageCollector](https://docs.oracle.com/javase/8/docs/api/java/lang/management/GarbageCollectorMXBean.html) | 15m |
| CollectionTime | Returns the approximate accumulated collection elapsed time in milliseconds. The Java virtual machine implementation may use a high resolution timer to measure the elapsed time. This method may return the same value even if the collection count has been incremented if the collection elapsed time is very short. | [GarbageCollector](https://docs.oracle.com/javase/8/docs/api/java/lang/management/GarbageCollectorMXBean.html) | 15m |
| MemoryUsed | Returns the amount of heap memory used by objects that are managed by the collector corresponding to this bean object. | [GarbageCollector](https://docs.oracle.com/javase/8/docs/api/java/lang/management/GarbageCollectorMXBean.html) | 15m |
| TotalMemoryFreed | Returns the cumulative total amount of memory freed, in bytes, by the garbage collector corresponding to this bean object. | [GarbageCollector](https://docs.oracle.com/javase/8/docs/api/java/lang/management/GarbageCollectorMXBean.html) | 15m |
| TotalCompacts | Returns the cumulative total number of compacts that was performed by garbage collector corresponding to this bean object. | [GarbageCollector](https://docs.oracle.com/javase/8/docs/api/java/lang/management/GarbageCollectorMXBean.html) | 15m |
| LastCollectionStartTime | Returns the start time in milliseconds of the last garbage collection that was carried out by this collector. | [GarbageCollector](https://docs.oracle.com/javase/8/docs/api/java/lang/management/GarbageCollectorMXBean.html) | 15m |
| LastCollectionEndTime | Returns the end time in milliseconds of the last garbage collection that was carried out by this collector. | [GarbageCollector](https://docs.oracle.com/javase/8/docs/api/java/lang/management/GarbageCollectorMXBean.html) | 15m |

-   Garbage Collector Object Name: java.lang:type=GarbageCollector,
    name=collector's name

#### Operating System

This managed bean is providing information about the operating system
metrics. It is used for monitoring CPU, Swap Space and Physical Memory
Usage. The **FreePhysicalMemorySize**, **FreeSwapSpaceSize**,
**SystemCpuLoad** should be used for alerts.

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Key Attributes | Description | MBean | Frequency |
|:---|:---|:---|:---|
| TotalPhysicalMemory | Returns the total available physical memory on the system in bytes. | [OperatingSystem](http://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html) | 15m |
| FreePhysicalMemorySize | Returns the amount of physical memory that is available on the system in bytes. | [OperatingSystem](http://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html) | 15m |
| TotalSwapSpaceSize | Returns the total amount of swap space in bytes. | [OperatingSystem](http://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html) | 15m |
| FreeSwapSpaceSize | Returns the amount of free swap space in bytes. | [OperatingSystem](http://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html) | 15m |
| SystemCpuLoad | Returns the "recent cpu usage" for the whole system. This value is a double in the \[0.0,1.0\] interval. A value of 0.0 means all CPUs were idle in the recent period of time observed, while a value of 1.0 means that all CPUs were actively running 100 of the time during the recent period of time observed. All values between 0.0 and 1.0 are possible. | [OperatingSystem](http://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html) | 15m |

-   Operating System Object Name: java.lang:type=OperatingSystem

### WebSphere Liberty Managed Beans

There are four managed beans we use from the WebSphere Liberty
Application Server are **Liberty Java Virtual Machine**, **Servlet
Statistics**, **Session Statistics** and **Thread Pools** beans.

#### Liberty Java Virtual Machine

This managed bean provides Liberty application server specific Java
Virtual Machine information. It is available when the monitor-1.0
feature is enabled. It is used for monitoring the JVM information.
Memory usage is a very important monitoring attribute for the
Application Server. High memory usage could indicate high usage by
deployed applications, heavy user workloads or memory leaks. The
**UsedMemory** and **ProcessCpu** attributes should be used for alerts.

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Key Attributes | Description | MBean | Frequency |
|:---|:---|:---|:---|
| Heap | Heap size used for current JVM. | [JvmStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |
| FreeMemory | Free team available for the current JVM. | [JvmStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |
| UsedMemory | Used heap for current JVM. | [JvmStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |
| ProcessCPU | Percentage of CPU used by JVM process. | [JvmStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |
| GcCount | Number of times GC has happened since JVM starts. | [JvmStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |
| GcTime | Total accumulated value of GC time. | [JvmStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |
| UpTime | Time in milliseconds since the JVM has started. | [JvmStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |

-   Liberty Java Virtual Machine Object Name: WebSphere:type=JvmStats

#### Servlet Statistics

The Servlet Statistics managed bean is used to provide servlet response
times. When the monitor-1.0 feature is enabled, one instance is
available for each servlet that has been served, where \* is of the form
AppName.ServletName. It is used to monitor servlet counts and average
response times. The **ResponseTime** should be used for alerts.

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Key Attributes | Description | MBean | Frequency |
|:---|:---|:---|:---|
| AppName | Name of the application. | [ServletStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |
| ServletName | Name of the Servlet. | [ServletStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |
| RequestCount | Number of hits to this servlet. | [ServletStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |
| ResponseTime | Average response time (nano-seconds) | [ServletStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |
| Description | Description of counter. | [ServletStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |
| RequestCountDetails | RequestCount details including last time stamp. | [ServletStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |
| ResponseTimeDetails | ResponseTime details including number of snapshot taken, min and max values. | [ServletStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |

-   Liberty Servlet Statistics Object Name:
    WebSphere:type=ServletStats,name=\*

#### Session Statistics

The session statistics managed bean is responsible for reporting
SessionStats for a single web application. It is available when the
monitor-1.0 feature is enabled.

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Key Attributes | Description | MBean | Frequency |
|:---|:---|:---|:---|
| CreateCount | Total number of sessions created. | [SessionStats](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/twlp_mon.html) | 15m |
| LiveCount | The total number of sessions that are currently cached in memory. | [SessionStats](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/twlp_mon.html) | 15m |
| ActiveCount | The total number of concurrently active sessions. A session is active if Liberty is processing a request that uses that session. | [SessionStats](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/twlp_mon.html) | 15m |
| InvalidatedCount | The total number of sessions that are invalidated. | [SessionStats](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/twlp_mon.html) | 15m |
| InvalidatedCountbyTimeout | The total number of sessions invalidated by a timeout. | [SessionStats](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/twlp_mon.html) | 15m |

-   Liberty Session Statistics Object Name:
    WebSphere:type=SessionStats,Name=\*

#### Thread Pools

The Thread Pool managed bean provides web container thread pool
information. It is available when the monitor-1.0 feature is enabled.
ThreadPoolStats is used to monitor the active threads usage in relation
to the pool size. Liberty uses an auto-tuning algorithm to find the
sweet spot for how many threads the server needs. Liberty is always
playing around and adjusting the number of threads in the pool
in-between and defined bounds for the coreThreads and maxThreads. In
Liberty the threadpool size is autosized by [Liberty
itself](https://developer.ibm.com/wasdev/docs/was-liberty-threading-and-why-you-probably-dont-need-to-tune-it).
The **ActiveThreads** attribute should be used for alerts.

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Key Attributes | Description | MBean | Frequency |
|:---|:---|:---|:---|
| PoolSize | Threads in the pool which represents the pool size. | [ThreadPoolStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |
| ActiveThreads | Active threads which are serving requests. | [ThreadPoolStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |
| PoolName | Only supports Default Executor thread pool. | [ThreadPoolStats](https://www.ibm.com/support/knowledgecenter/SS7JFU_8.5.5/com.ibm.websphere.wlp.express.doc/ae/rwlp_mbeans_list.html) | 15m |

-   Liberty Thread Pools Object Name:
    WebSphere:type=ThreadPoolStats,name=DefaultExecutor

##### Related topics: [related-topics]

-   [JVM
    MBeans](https://www.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.lnx.80.doc/diag/tools/mxbeans.html)
-   [WebSphere Liberty
    MBeans](https://www.ibm.com/support/knowledgecenter/en/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_jmx.html)

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: -- Main.RichardWatts - 2018-03-20 [additional-contributors----main.richardwatts---2018-03-20]
