META:TOPICINFO{author="sbagot" date="1432664047" format="1.1"
reprev="1.28" version="1.28"}
META:TOPICPARENT{name="PerformanceTroubleshooting"}

# Does my server have enough memory? [does-my-server-have-enough-memory]

DKGRAY Authors: PerformanceTroubleshootingTeam Build basis: CLM 4.x and
later ENDCOLOR

TOC{title="Page contents"}

This page provides information to help you determine if your Rational
Collaborative Lifecyle Management (CLM) server has sufficient memory and
lists resources that can be used to monitor memory usage.

Having sufficient memory and managing memory usage is probably the most
important factor in your system performance. One of the indications of a
memory shortage in your server is when your system is paging. Paging is
when your system runs out of memory and starts to move some parts of a
process address space from RAM to disk in order to free the memory.
Although some paging might be acceptable, frequent paging results in
significant system performance degradation.

## The lower bound

Performance of Java applications degrade significantly when parts of the
Java heap is paged out by the operating system. A key precondition of
ensuring reasonable performance from CLM applications is to configure
the system hosting the application so that this never occurs.

The system that is hosting the CLM applications must be configured with
sufficient memory to prevent each of the Java Virtual Machines (JVM)
hosted on that system from being paged out.

At a minimum, this means allocating enough memory for the maximum heap
size (the -Xmx setting) for each JVM, plus additional memory for the
instructions, thread stacks, data, and native memory demands of the
application(s) running in the JVM. So, for example, never host a JVM
with an Xmx value of 4 GB on a system with physical memory of 4 GB.
Because when the heap size grows to its maximum, there will not be
enough memory for the rest of the Java process memory needs, let alone
the memory needs of the operating system and other processes. Larger
amounts of physical memory (for example 5 GB or 6 GB) might still not be
enough, depending on the workload being presented to the JVM and its
host operating system. In these cases, monitoring of the system is
necessary to ascertain there is adequate physical memory allocated to
the host system.

## Monitoring memory usage

Monitoring of system memory depends on the operating system. An outline
of how this can be performed is provided at the following links: 1 [IBM
AIX](http://www.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.aix.70.doc/diag/problem_determination/aix_memory.html)
1 [Red Hat
Linux](https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/s1-sysinfo-memory-usage.html)
1 [SUSE
Linux](http://doc.opensuse.org/documentation/html/openSUSE/opensuse-tuning/cha.util.html#sec.util.memory)
1 [Microsoft
Windows](http://msdn.microsoft.com/en-us/library/ms176018(v=sql.105).aspx)
1 [Oracle
Solaris](http://docs.oracle.com/cd/E23824_01/html/821-1451/spconcepts-38776.html)

## Special considerations for Virtual Machines (VMs)

If using shared memory, make sure one of the following situations is
true: 1 Memory is dedicated to the VM on which the CLM application is
hosted 1 Enough memory is on the physical system hosting the VM to
prevent the hypervisor from stealing memory from the CLM VM and
triggering paging

To best serve CLM, because it forces the CLM VM to be independent of
other activities on other guest VMs, dedicate memory and CPU resources
to a VM hosting a CLM application.

##### Related topics: [related-topics]

-   Still need help troubleshooting your performance issue? Refer to
    [Performance Troubleshooting](PerformanceTroubleshooting) for
    additional topics.
-   [Why do I get out of memory (OOM)
    errors?](https://jazz.net/wiki/bin/view/Deployment/OomIntheLog)

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]
