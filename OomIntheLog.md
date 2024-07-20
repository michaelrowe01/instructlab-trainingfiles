META:TOPICINFO{author="paulellis" date="1488372742" format="1.1"
reprev="1.34" version="1.34"}
META:TOPICPARENT{name="PerformanceTroubleshooting"}

# Why do I get out-of-memory (OOM) errors? DKGRAY Authors: Main.MichaelAfshar Build basis: IBM Java v1.6 and later, WebSphere v7 and later (for use with CLM 4.x and later) [why-do-i-get-out-of-memory-oom-errors-dkgray-authors-main.michaelafshar-build-basis-ibm-java-v1.6-and-later-websphere-v7-and-later-for-use-with-clm-4.x-and-later]

ENDCOLOR

TOC{title="Page contents"}

Use this guide to understand the out-of-memory (OOM) error messages, to
identify the different root causes of these errors, and to learn how to
prevent future occurrences.

## Symptoms

You might see out-of-memory error messages in one of the following ways:

-   Displayed on the screen from the Eclipse or browser client while you
    are attempting to perform an operation
-   Written to a server log file (the standard error file)

## Identifying the root cause

When you observe a `java.lang.OutOfMemoryError` error, the first step is
to determine which kind of memory has been exhausted:

-   **Heap memory**: Java heap memory is used by the JVM to store all
    objects.
-   **Native memory**: Native memory is used by a more limited subset of
    activities, such as JIT compilers, creating threads, loading a
    class, or some types of file I/O (more specifically, NIO direct byte
    buffers).

This distinction is important because it determines the approaches
necessary to troubleshoot the root cause and to prevent a recurrence of
these kind of errors.

Not all native memory depletions necessarily result in a Java OOM error.
Other symptoms (such as excessive paging, errors in the standard error
file, or even process termination) can accompany this condition.

However, in the case of an OOM exception from the JVM, the first place
to check is standard error files of the Apache Tomcat or WebSphere
Application Server instance. If the OOM condition is accompanied by
errors messages indicating an inability to allocate buffer space, or to
stack space, or a malloc() failure, the Java OOM exception was caused by
native memory exhaustion.

If a javacore file was produced by the OOM exception (and with recommend
JVM settings, it should be) the analysis should then proceed to that
file.

### Analyzing the javacore file

A javacore file is a formatted text file that is usually created by the
JVM as a result of a system event, but can also be created by manual
action, such as sending a signal. A javacore file contains information
about the running JVM process, its threads, monitors, and memory
consumption, and can be used to determine the type of out-of-memory
condition.

In some cases, depending on the logic executing when the out-of-memory
error occurred, it is straightforward to distinguish which kind of
memory has been exhausted. There might be additional comments with the
exception in the log file reporting the OOM error, or in the javacore
file that is generated.

#### TITLE section

For example, in the TITLE subcomponent of the javacore file, the
`1TISIGINFO` line in this snippet from a javacore file makes it clear
that the problem is in the Java heap space. Notice the "Java heap space"
after `"java/lang/OutOfMemoryError"`:

0SECTION TITLE subcomponent dump routine NULL
**`===========================`** 1TISIGINFO Dump Event "systhrow"
(00040000) Detail "java/lang/OutOfMemoryError" "Java heap space"
received 1TIDATETIME Date: 2012/12/10 at 05:33:3

However, there are times that more information about memory exhaustion
is not available in the log files or TITLE subcomponent of the javacore
file. In those cases, more analysis of the associated javacore file is
necessary.

#### MEMINFO section

The meminfo section of the javacore file contains information about how
much Java heap space was free when the OOM condition occurred. In the
example below, at the time the javacore file was generated, there was
about 5 GB of heap space free out of a maximum size of 6 GB. So, if this
javacore file was generated during an out-of-memory event, it was not a
heap space problem.

NULL
------------------------------------------------------------------------
0SECTION MEMINFO subcomponent dump routine NULL
**`=============================`** 1STHEAPFREE Bytes of Heap Space
Free: 14ACBBFD8 1STHEAPALLOC Bytes of Heap Space Allocated: 180000000

**Note:** The Bytes of Heap Space Free and Bytes of Heap Space Allocated
are displayed in Hex format.

#### Garbage collection (GC) HISTORY section

You should also check the garbage collection history section of the
javacore file. If this section is empty, the OOM error was probably
caused by a native memory shortage. If the history shows that garbage
collection is running too frequently, the JVM can issue an OOM exception
and the following message is recorded in the file, which points to a
Java heap memory exhaustion.

......... j9mm.83 - Forcing J9AllocateObject() to fail due to excessive
GC

Also, check the requested bytes that triggered the last allocation
failure. If that was very large (and larger than the available memory in
the heap), the OOM was caused by the JVM heap space exhaustion.

In summary, if the analysis of the garbage collection history section of
the javacore file shows no sign of excessive garbage collection, and
there is memory available in the Java heap, the cause of the OOM
exception is most likely a native heap depletion.

## Java heap exhaustion

An out-of-memory exception occurs when the live object population of a
JVM requires more space than is available in the Java managed heap. This
situation can occur for one of the following reasons:

-   The Java heap size is not large enough for the workload that the JVM
    is performing
-   There is not enough contiguous memory in the heap for an object
-   There is an object leak, probably caused by faulty application logic

### Analyzing the garbage collection logs

With a Java heap exhaustion, troubleshooting continues by (if not
already enabled) enabling verbose garbage collection, and analyzing the
verbose GC logs. The `-verbose:gc` switch causes the JVM to print
messages when a garbage collection cycle begins and ends. These messages
indicate how much heap space is consumed by live data on the heap, how
much space has been reclaimed at the end of a collection cycle, and
other helpful information. For more information, see [verbose garbage
collection](http://publib.boulder.ibm.com/infocenter/java7sdk/v7r0/index.jsp?topic=/com.ibm.java.zos.70.doc/diag/tools/gcpd_verbosegc.html).

If the heap size is not large enough, the solution is to increase the
numeric value of the -Xmx and -Xms arguments that are specified to start
the JVM. However, this can only be done if there is enough physical
memory installed on the system (or allocated to the VM). It is very
difficult to provide a definition of "enough" that covers all possible
end-user situations; but as a general guideline, it is imperative that
an administrator ensures that there is enough free memory on the
Rational Team Concert host to prevent paging of the Java process address
space with its increased heap size.

If the OOM error was generated because there is insufficient contiguous
memory in the heap for the object being allocated, check the size of the
object requested in the garbage collection log. If the size is not
unusually large, the fix, also, is to increase heap size by modifying
the numeric value of the -Xmx and -Xms arguments. The following extract
shows an unusually large requested object:

The request was memory for about a 142 MB object. If you encounter a
situation such as this, and you are constrained from increasing the heap
size by available physical memory, contact [Rational customer
support](DataCollectionandSupportResources#Rational_Support_Resources).

Finally, in the relatively rare case of a Java object leak, the amount
of free space on the heap decreases after a garbage collection cycle
over time. Increasing the size of the Java heap will delay, but still
eventually result in, an out-of-memory exception. If there is physical
memory to spare, increasing the heap size will be a useful workaround to
reduce the mean time between failures, but at this point, you should
engage IBM customer support for further assistance.

A Java object leak is caused when an application retains references to
objects that are no longer in use. In a Java application, the programmer
must remove references to objects that are no longer required, usually
by setting references to null. When references are not removed, the
object and anything the object references stays in the Java heap and
cannot be removed. Such leaks can only be corrected by the IBM
programmers.

Note that garbage collection errors do not always lead to out-of-memory
errors. It is possible to search a verbose garbage-collection log for
"JVMST\*", and if errors appear, they can be looked up and checked
against a list in this document: [IBM JVM Garbage Collection and Storage
Allocation
techniques](http://download.boulder.ibm.com/ibmdl/pub/software/dw/jdk/diagnosis/GCandMemory-042005.pdf).

## Native memory exhaustion

Native memory exhaustion is either simple or difficult to track down.

A Jazz administrator should first check the system configuration first.
Is the JVM configured with a (say 4 GB) heap size on a system with the
same amount (say 4GB) of physical memory? That will provide poor
performance, and the high probability of a native memory OOM exception.

If the basic configuration seems OK, you will probably need to involve
Rational customer support for assistance. However, if you suspect that
native heap exhaustion is the source of the OOM exception, the one
important distinction to make is identifying when the memory footprint
of the Java process increases:

1.   Is there a continual increase?
2.   Is the increase only happening during the start of the application?
3.   Is the increase only happening under certain workload-related
    operations?

In the 6.0.x release stream due to the introduction of more applications
being collocated on one application server, especially when the
Lifecycle Query Engine(LQE) application resides alongside other CLM
applications, these issues have become common on Windows. [Native Out Of
Memory
Exceptions](AttemptingToUseRTCOnWindowsOperatingSystemLeadsIntoNativeOutOfMemory)
attempts to offer advice on recognizing these and also resolving them.

### Data gathering

To obtain the data needed to make this distinction, the best approach is
to run a script to collect native memory that is consumed by the Java
process. These scripts or procedures are described in [Setting up the
generation of diagnostic data for an
OutOfMemoryError](http://publib.boulder.ibm.com/infocenter/javasdk/tools/index.jsp?topic=/com.ibm.java.doc.igaa/_1vg000131402ee-11e49e6e566-7fdb_1004.html).
On the AIX operating system, there is an `aix_memory_monitor.sh` script
that can be downloaded from that link to collect `svmon` data for this
process. However, the `aix_memory_monitor.sh` script must be run prior
to the occurrence of the OOM situation. Output from this script can then
be analyzed with a tool, such as [The GC and memory visualization
tool](http://www.ibm.com/developerworks/java/library/j-ibmtools2/index.html )
from IBM.

### Analysis

In the case of a continual increase in the Java process memory footprint
(case 1 above), the root cause is probably a native memory leak.

In the case of an increase only during the application startup (case 2
above), the JVM does not have access to enough native memory within its
address space. Check that [technote 1265655 - Native-memory shortage
causes out of memory
error](http://www.ibm.com/support/docview.wss?uid=swg21265655) does not
apply, and if not, adding more physical memory to the system (or
allocating more memory to the VM) is necessary.

In the case of an increase that is only seen under workload-related
operations (case 3 above), an assessment must be made to determine
whether the following situations are occurring:

-   The application logic is using native memory inefficiently
-   The workload peaks that result in these increases can be modulated

If neither of the above is true, adding more physical memory to the
system (or allocating more memory to the VM) is necessary.

Additional debugging steps will involve data collection including not
only the Java process memory footprint data monitoring you have
performed, but also periodic javacore files, verbose GC logs, and even
(possibly) generating a Java heap dump (.phd) file.

## Other memory issues

You can reduce the probability of encountering native memory exhaustion
by configuring sufficient memory on the CLM application host. Check
[Does my server have enough memory?](HowToDetermineServerMemory).

Although this page has focused on the OOM errors, consideration should
also given to memory on all architectural components in a CLM
configuration. A broad overview of memory demands on the client system,
the load balancer, the IHS server, and the database server should be
performed.

An end user can experience an OOM error when starting an Eclipse client.
For more information, see [technote 1624397 - Rational Team Concert
Eclipse client fails to start with Out of Memory
error](http://www.ibm.com/support/docview.wss?uid=swg21624397).

IBM JVM heap dump files can be analyzed with [IBM
HeapAnalyzer](https://www.ibm.com/developerworks/mydeveloperworks/wikis/home/wiki/W3b463571efc8_4f02_99af_3cbc0da42ddc/page/IBM20HeapAnalyzer20Information?lang=de_DE)
)

##### Related topics: None [related-topics-none]

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]
