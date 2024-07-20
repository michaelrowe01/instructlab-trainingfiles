# Attempting to use Collaborative Lifecycle Management on Windows operating system leads to NativeOutOfMemoryException (NOOME).

Authors: Main.NatarajanThirumeni , Main.PaulEllis 
Build basis: Engineering Lifecycle Management 5.x, 6.x, 7.x


This article was originally scoped to explain a situation observed when
using Rational Team Concert (RTC) on Microsoft Windows 2008 R2 Operating
System which can result in a NativeOutOfMemoryException (NOOME). This
article has been updated due to similar observations being made on
Microsoft Windows operating systems in general, also including 2008 and
2012, during evaluation use of Engineering Lifecycle Management (ELM)
6.x

There have been additional use cases where we have observed native out
of memory exceptions, with the Engineering Lifecycle Management 7.x
suite, which are documented below with the advised actions to resolve.

A more comprehensive [Troubleshooting native memory
issues](https://www.ibm.com/support/pages/node/619631) is available from
the IBM Java team. If this simple wiki page is insufficient, then IBM
Support recommend following the IBM Java reference document and create a
case with IBM Support.

## NOOMEs due to contention in the 4GB Windows memory space

Typically, we have observed NOOMEs when multiple Engineering Lifecycle
Management applications were collocated on the same Windows server. This
was especially prevalent when the Lifecycle Query Engine (LQE) had been
installed alongside all of the other ELM applications required in a
global configuration environment. This issue is one of many discussed in
the [Proof of Concept
Sizing](https://jazz.net/wiki/bin/view/Deployment/ProofOfConceptSizingIn6x)
page, where we discuss implications of architectural decisions and what
constitutes a supported configuration.

This tech note talks about Native out of memory error. Native OOM is
totally different from Out of Memory Error (java.lang.OutOfMemoryError).

This tech note is about debugging Native out of memory error on Windows
operating system. To debug NOOM - you'll have to collect number of
performance logs or use logs which were created when system ran out of
native memory error. Usually, these are essential logs to investigate
Native out of memory error:

Application logs (ELM application and WAS or Liberty Logs)

Java core,

verbose:gc

heapdump

In some cases, system core dumps.

IBM support teams, level 2 & 3 should be able to investigate these logs
to find out what may have caused an application server ran out of native
out of memory. Based on our experience, we want to document at least
couple of use cases where RTC ran out of native out of memory error.
With the help of this documentation, you may be able to look at the logs
on your own to see if you could take an appropriate action to prevent
NOOM.

On Windows OS, there are many cases where an application server could
ran out of native out of memory. Lets us take a look at two different
use cases of NOOM where EWM (Engineering Workflow Manager) is deployed
on a Window operating system.

There are a few options to resolve this problem. Please ensure that you
test whichever solution is preferred before implementing in your
production environment.

### **Use Case \#1 (NOOM due to a shortage of 32-bit address space)**

The ELM application server is running and unexpectedly the application
server crashes with a NOOME. The crash generates Java cores and heap
dumps and may even generate system core dumps. Looking at the Javacore
in the first few lines reads

java.lang.OutOfMemoryError: native memory exhausted /Detail
"java/lang/OutOfMemoryError" "native memory exhausted" received

and followed by NATIVEMEMINFO section shows various memory information
and its allocation:

NATIVEMEMINFO subcomponent dump routine

**`=========================`**

JRE: 27,993,948,032 bytes / 652964 allocations

\| +--VM: 27,114,530,200 bytes / 423805 allocations

\| \| \| +--Classes: 624,129,600 bytes / 218169 allocations \| \| \| \|
\| +--Shared Class Cache: 94,371,840 bytes / 1 allocation \| \| \| \| \|
+--Other: 529,757,760 bytes / 218168 allocations \| \| \| +--Memory
Manager (GC): 26,293,463,080 bytes / 5200 allocations \| \| \| \| \|
+--Java Heap: 25,769,865,216 bytes / 1 allocation \| \| \| \| \|
+--Other: 523,597,864 bytes / 5199 allocations \| \| +--Threads:
123,430,888 bytes / 1764 allocations \| \| \| \| \| +--Java Stack:
16,110,464 bytes / 368 allocations \| \| \| \| \| +--Native Stack:
102,662,144 bytes / 369 allocations \| \| \| \| \| +--Other: 4,658,280
bytes / 1027 allocations

The allocation of VM and Garbage Collection indicate that this is due to
shortage of 32-bit address space. The address space allocation is
discussed in details in [IBM Java tech
note](https://www-01.ibm.com/support/docview.wss?uid=swg21660890), for
more information please read / review.

If
[Xmcrs](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=options-xmcrs)
does not help, you may consult with IBM support.

Note, changes to Xmcrs require a an application server restart.

#### When using Link Index Provider (LDX)

We have seen the most successful remedy has been to use the Microsoft
article [FAQ for Development on 64-bit
Windows](http://msdn.microsoft.com/en-us/library/bb190527.aspx), which
states:

"On Windows, the operating system allocates memory in the lowest 4 GB of
address space by default until that area is full. A large -Xmx value
might be insufficient to avoid OutOfMemoryError exceptions.

Advanced users can change the default Windows allocation options by
setting the registry key named
HKLM\System\CurrentControlSet\Control\Session Manager\Memory
Management\AllocationPreference to (REG_DWORD) 0x100000.." This option
will force allocations in top-down order, instead of the lower areas of
RAM.

### **Use Case \#2 (NOOM due to a Direct Byte Buffers (DBB) allocation on top of available OS memory)**

Use case \#2, is similar to use case \#1, where you'll see Java core is
pointing out to "java.lang.OutOfMemoryError: native memory exhausted".
However if you take a closer look in the core file, you'll see
application server is demanding high volume of Direct Byte Buffers. The
direct memory region is demanding more memory because, the users are
working with large files (examples, number of files in workspace and its
content, parallel workspace loads and workitem attachments). These large
files, could drive DBB region to run of native memory. Lets take a look
how to prevent:

a\) You may want to reduce amount of files which are being downloaded on
the client systems (developers workspace , build machines and etc). If
you believe client systems are repeatedly downloading same content from
the server then you should consider to introduce a content proxy server
to reduce load om the application server.

b\) If you can't control amount of files are being loaded on the client
systems, another option is provide more memory to operating system
itself which may prevent NOOM.

In our case \#2, system run out of native memory - to confirm this
symptoms, open a Java core, search for Direct Byte Buffers: under
NATIVEMEMINFO region

NATIVEMEMINFO subcomponent dump routine

**`=============================`**

\|JRE: 33,704,575,224 bytes / 1899498 allocations

+--VM: 18,037,204,920 bytes / 41309 allocations \| \| \| +--Classes:
336,463,736 bytes / 22753 allocations \| \| \| \| \| +--Shared Class
Cache: 94,371,840 bytes / 1 allocation \| \| \| \| \| +--Other:
242,091,896 bytes / 22752 allocations \| \| \| +--Memory Manager (GC):
17,531,872,344 bytes / 3572 allocations \| \| \| \| \| +--Java Heap:
17,179,930,624 bytes / 1 allocation \| \| \| \| \| +--Other: 351,941,720
bytes / 3571 allocations \| \| \| +--Threads: 70,219,216 bytes / 1123
allocations

.......

.........

............

\| \| \| +--Direct Byte Buffers: 15,169,455,128 bytes / 1832570
allocations

As you can see, Direct Byte Buffers is demanding over 15 GBs. And in our
case, the OS has 32 GB of RAM. The JVM is using 16 GB of heap.
Naturally, the OS don't have enough memory to go beyond 32 GBs. At this
point, native out of memory is expected as there isn't enough memory.

The changes to OS memory changes require a server restart.

### **Other Solutions**

If either of these use cases (use case \#1 or use case \#2) does not
help - its highly suggested go to to IBM support and seek for further
level of debugging.

## Need more helps? Open PMR

Should you have any issues or concerns, open a PMR then we can help you.

IBM Service Request links:

IBM Service Request: <https://www.ibm.com/support/servicerequest/>

IBM Service Request user information: <https://www-946.ibm.com/sr/help/>

IBM Service Request Helpdesk:
<https://www-946.ibm.com/sr/help/sr_helpdesk.html>

##### Related topics: 
* [Deployment web home](DeploymentWebHome), 
* [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: 
<http://www-01.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.doc.60_26/vm626/J9/VM/xcompressedrefs.html> [external-links-httpwww-01.ibm.comsupportknowledgecenterssyke2_6.0.0com.ibm.java.doc.60_26vm626j9vmxcompressedrefs.html]

-   [IBM](https://www.ibm.com)

##### Additional contributors: 
Main.KeithWells, Main.MariusLuca [additional-contributors-main.keithwells-main.mariusluca]
