META:TOPICINFO{author="tfeeney" date="1480409344" format="1.1"
version="1.4"} META:TOPICPARENT{name="MonitoringWhereToStart"}

# Monitoring error messages DKGRAY Authors: Main.KathrynFryer, Main.TimFeeney Build basis: Rational Collaborative Lifecycle Management (CLM) and Watson Internet of Things Continuous Engineering (IoTCE) solutions 6.0.2 [monitoring-error-messages-dkgray-authors-main.kathrynfryer-main.timfeeney-build-basis-rational-collaborative-lifecycle-management-clm-and-watson-internet-of-things-continuous-engineering-iotce-solutions-6.0.2]

ENDCOLOR

TOC{title="Page contents"}

As part of their monitoring strategy for the CLM or IoTCE solution, some
clients opt to use third-party tools to parse and monitor messages
logged in log files to identify issues or potential issues. If you
choose to monitor the logs, this page describes some messages and
scenarios to watch for. The list provided here is intended as a starting
point; over time, you might choose to add or remove messages from your
"watch list" based on your experience. If the log file is not
specifically identified, the message could appear in any of the CLM/CE
application logs.

### Out-of-memory errors

Look for the text `OutOfMemoryError`, as well as `Native Memory` and
`Java Heap`.

Native memory is the memory reserved for the classes. When you include
compressedrefs in the JVM settings, native memory is the first 4G of
memory reserved. If you continue to see native out-of-memory errors, you
might need more than that 4G reserve, and switch to the nocompressedrefs
setting.

For out-of-memory errors in general, you can look at the verbose garbage
collection logs to see when memory started to increase, and then examine
the application logs or a thread dump for that time period to see what
was happening. You could use a tool like IBM Memory Analyzer to drill
into the heap dump to find leak suspects and classes consuming the most
memory.

### Java dumps

In the WebSphere Application Server (WAS) native_stderr.log, JVMDUMP032I
is logged any time a Java dump is requested, including thread dump,
system dump, and memory dump. JVMDUMP030W is logged if the dump cannot
be written, which could be due to issues with permissions, disk space,
or another reason.

Because users can trigger dumps with various tools and from the WAS
console, you probably do not want to monitor all the JVMDUMP messages,
which are documented in [this topic in the IBM Knowledge
Center](http://www.ibm.com/support/knowledgecenter/SSYKE2_7.1.0/com.ibm.java.messages/diag/appendixes/messages/dump/messages_dump.html).
Over time, you might add selected messages to your watch list based on
your experience. You would need to analyze the dump to determine the
root cause and take action accordingly.

### Long-running threads

Look in the WAS Systemout.log file for the text
`thread(s) in total in the server that may be hung`, or alternatively
WSVR0605W and WSVR0606W. WSVR0605W is generated if a thread runs longer
than the time set in WebSphere Application Server (the default is 10
minutes). In some cases, these alerts simply identify jobs that require
more time to complete; they indicate what's happening in your system and
can identify operations that impact performance. A second message
WSVR0606W is generated when the thread completes. When you suspect
problems, you can configure WAS to generate a javacore or thread dump
when this message occurs, as described in [this support
article](https://www-01.ibm.com/support/docview.wss?uid=swg21448581).

For reference, the message text appears as follows:

-   WSVR0605W Thread *{threadname}* has been active for *{time}* and may
    be hung. There are *{totalthreads}* in total in the server that may
    be hung.
-   WSVR0606W Thread *{threadname{* was previously reported to be hung
    but has completed. It was active for approximately *{time}*. There
    is/are *{n}* thread(s) in total in the server that still may be
    hung.

### Long-running queries in RM

In the RM log, warning message CRJZS5819W or CRJZS5820W is logged when a
query (to return a view or artifacts, for example) runs longer than the
threshold setting. Another message CRJZS5742W is logged when the query
completes. The threshold value is set in the RM Administration
**Advanced Properties** \> **Jena query operation logging time threshold
(in ms)**.

The default query threshold is 45 seconds, so not every instance of the
warning message indicates an issue. However, if you find multiple
sequential instances the same query id, especially without any
completion message, you could note the query id and investigate the
cause. You cannot stop the query while it is still running.

The full message text appears as follows:

-   CRJZS5819W Query *{id}* is still running after *{n}* seconds and has
    now exceeded the maximum amount of time allowed by the server. This
    query may be jeopardizing the memory and CPU health of the server.
    It has *{x}* user contexts: *{contexts}*
-   CRJZS5820W Query *{id}* is still running after *{n}* seconds and has
    now exceeded the maximum amount of time allowed by the server. This
    query may be jeopardizing the memory and CPU health of the server.
    It is scoped to *{scope}* and has *{x}* user contexts: *{context}*
-   CRJZS5742W Query *{id}* had an execution time of *{n}* ms, and
    produced *{x}* results

### SocketTimeoutException occurrences

Look for the text `SocketTimeoutException`. This exception indicates
that something has taken longer than one of the many configurable socket
timeouts set throughout the stack. The exception might indicate an
abnormally long running operation, network or server availability
issues, or other problem. Use the messages occurring around the
exception to determine the potential cause for the timeout. Call Support
if you cannot resolve the problem.

A SocketTimeoutException is logged as a Java exception, resembling the
following format:

... Caused by: java.net.SocketTimeoutException

### SqlTimeoutException occurrences

Look for the text `sqlTimeoutException`. This error indicates that a
JDBC timeout has been reached and the database did not return the
result. There are a number of possible causes; use the messages around
the exception to investigate the cause.

the error typically resembles the following format:

... Caused by: com.ibm.db2.jcc.am.SqlTimeoutException: DB2 SQL Error:
SQLCode = -{code}, SQLSTATE={code}, SQLERRMC={error}

### SQLException occurrences

SQL exceptions typically indicate a bad database state, corrupt indexes,
data integrity issues, or similar issue. Look for the text
`SQLException`. You would need to investigate the details of the
exception.

### Corrupt indices

The CLM/CE applications rely on various indices stored in the file
system, including Jena, test, and query indices. These indices can get
corrupted by incorrect server shutdown, lack of disk space, inability to
write to disk, or other reasons. Corrupt indices can cause unexpected
application behavior and query results, including missing data. Look for
messages with the text `indexing` and review the other messages in the
log to determine the cause.

To address corrupt indices, reindex using the appropriate repotools
command for the type of index; see the [Repository tools command-line
reference
topic](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.3/com.ibm.jazz.install.doc/topics/c_repotools_overview.html)
in the IBM Knowledge Center.

### Connection or handshake failures

Connection failures could occur when a new server is added, a
certificate expires, or other reasons. These messages are often more of
a troubleshooting aid, but could indicate problems. Message text to
watch for includes `unable to connect`, `connection refused`,
`connection timed out`, and `handshake`. Similarly, an inability to
connect to the database could indicate high server loads, underpowered
database server, or other issues. Watch for message CRRGW7022E
`A connection to the database "{0}" could not be acquired in {1} ms.`

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

META:TOPICMOVED{by="tfeeney" date="1480409344"
from="Deployment.MonitoringLoggedErrorMesages"
to="Deployment.MonitoringLoggedErrorMessages"}
