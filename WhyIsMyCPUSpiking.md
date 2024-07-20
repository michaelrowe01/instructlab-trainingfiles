META:TOPICINFO{author="sbagot" date="1432664074" format="1.1"
version="1.26"} META:TOPICPARENT{name="PerformanceTroubleshooting"}

# Why is my CPU spiking? DKGRAY Authors: Main.MichaelAfshar Build basis: CLM 4.x and later [why-is-my-cpu-spiking-dkgray-authors-main.michaelafshar-build-basis-clm-4.x-and-later]

ENDCOLOR

TOC{title="Page contents"}

This section outlines the suggested approach for analyzing and
investigating *sporadic* high CPU loads on Collaborative Lifecycle
Management (CLM) servers.

## Scope

This page focuses only on CPU spikes on the application server host.

## Is the CPU spike actually causing a problem?

Variability in CPU consumption (depending on system workload) is, of
course, not unusual. High CPU consumption is not, in itself, a problem.

However, 100 percent CPU consumption can be, and almost always is, a
problem because it means there are insufficient resources at peak times
to execute the workload presented to the system.

High CPU consumption can be perceived as a problem if system
administrators worry about capacity with the projected growth in team
size or end-user population. High CPU consumption is also a problem if
it correlates with a degradation in end-user response times. Only in
these cases is the effort associated with tracking down the source of
the CPU spike(s) likely to be worthwhile.

## Data gathering basics

First, obtain an overview of the system and insight into the temporal
behavior of this symptom.

## System overview and temporal behavior

### Is this a virtual or physical system?

First, determine whether the system on which this application is running
is a real (physical) machine, or a virtual machine (VM).

If it is a physical system, operating system statistics present a
complete picture of CPU availability and consumption.

However, if it is a virtual machine, a complete understanding of CPU
availability and consumption must include information only available
from the hypervisor.

### Operating system perspective

Next, you must identify how many processors the (possibly guest)
operating system is managing. What level of multi-threading (or
simultaneous multi-processing) is each processor capable of performing?
Is each processor operating at its full theoretical clock speed, or is
power-saving enabled and active?

### What is happening when the CPU load is spiking?

It is the detailed answer to this question that will eventually lead to
the root cause of the CPU spike.

Because this is usually an easier thing to do, it is best to first
understand and eliminate possible 'external' sources of CPU consumption
before undertaking the data gathering and analysis required of the
application itself. Activities in the environment that might
sporadically affect CPU consumption are:

1.  If this is a VM, activities (CPU demands) from other VMs sharing the
    same physical resources as this VM.
2.  Specific system administrative activities (such as virus scans or
    backups) .
3.  More generally, other processes sharing the same operating system as
    this application.

Once you are sure that the problem is with the application itself (or,
more specifically, the Java process) you then need to determine which
tier in the Java process might be responsible for the elevated CPU.

The methodical approach to doing this is to identify which Java threads
are consuming the most CPU at the time that the Java process itself is
peaking in CPU consumption. This is not always straight forward and
involves rather tricky and lengthy data gathering and analysis. So
again, before undertaking this methodical approach, it might be more
efficient to first attempt to correlate the CPU spike with certain
activities. Answering the following questions might help:

1.  Do the spikes correlate with any of the administrative activities
    in (a) the infrastructure (such as: WebSphere Application Server,
    JVM, or database) or (b) the application (such as: asynchronous
    tasks, or report generation)
2.  Do the spikes correlate with any known end-user activity (such as:
    launching of system builds, periodicity of feeds, and others)

If there is nothing in the timing of the spikes that suggests a cause,
understanding the cause of spikes will require characterizing the CPU
spike and this in turn will require more detailed and protracted data
gathering, depending on the mean time between spikes. The purpose of
this data gathering is to collect concrete data that will tell you
(among other things):

1.  The amplitude of the CPU spike
2.  The frequency with which the CPU spikes
3.  Whether the CPU spike is in kernel, user, or I/O wait times.
4.  Whether other metrics show correlating deleterious behavior (such as
    interrupts, paging, file I/O).
5.  What the threads in the application are doing at the time of the
    spike.

Setting up scripts to collect this data is described in each of the
platform-specific sections below.

## Detailed data gathering

Monitoring of system activity is dependent on the operating system. An
outline of how this can be performed is provided at the following links:

1 [AIX](AixCpuSpike) 1 [RedHat Linux](RedHatCpuSpike)

## Possible causes and solutions

### Antivirus software enabled on production machine

Antivirus software has been known to cause slow performance when running
on a production server. Check whether your antivirus software is running
when you experience slow performance.

##### Related topics: None [related-topics-none]

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]
