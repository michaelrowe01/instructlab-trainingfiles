META:TOPICINFO{author="harryabadi" date="1368739881" format="1.1"
version="1.8"} META:TOPICPARENT{name="WhyIsMyCPUSpiking"}

# Red Hat CPU spike [red-hat-cpu-spike]

DKGRAY Authors: Main.MichaelAfshar Build basis: Redhat Linux 5.6 or
later ENDCOLOR

TOC{title="Page contents"}

This page describes the tools and procedure to use to identify the root
cause of a CPU spike in a RedHat Linux environment.

## Data to be collected

1.  system overview
2.  vmstat data with a 1 second granularity, timestamped
3.  top output with a 2 or 3 second granularity, also timestamped
4.  top -H output samples during the CPU spike
5.  javacores collected with a (say) 30 second granularity during the
    CPU spike
6.  snapshots of the "Active Services" running at the time of the CPU
    spike

### System overview

We start by trying to build up a picture of the CPU resources available
to the system. The kinds of questions we may have are:

1.  How many (virtual) processors are configured (or assigned to the
    LPAR)?
2.  What SMT level is enabled?
3.  If virtual, are the number of processors available to this LPAR
    capped, or uncapped? What is the entitlement for this Virtual
    Machine?
4.  Depending on the entitlement, and if uncapped, how large is the
    pool, and how many other LPARs share processors in this pool, how
    overcommitted is the pool of processors.

Running the RedHat Linux "xxxxx" command answers most of the questions
we may have.

xxxxxxxx

We refer the reader to the xxxxxx man page for field by field
descriptions of this output.

### vmstat

To locate the time of the CPU spike, and to gain an insight into whether
user or system CPU is being consumed at this time, the best tool to use
is vmstat. The preferred flags to use for this are:

nohup vmstat -a 1 \> vmstat.out &

This command runs vmstat in the background (and wrapped with a nohup
command) and redirects the output to a *vmstat.out* file. It will
collect data with a 1 second granularity. Maybe a value of 604800, which
collects data for a week, is appropriate for iterations. \[If so, the
output file could be quite large\]. If the mean time between CPU peaks,
is small (say daily) then a smaller value for \_\_ may be more
practical.

Please note that this level of granularity is necessary for a
comprehensive insight into the consumption of this resource. A system
administrator may well be running other tools that are also collecting
data (sar) with a larger (e.g. 5 minute or 15 minute) granularity - but
this output, though useful for capacity planning purposes, will not be
helpful in the analysis of possibly short-lived CPU spikes.

Check the vmstat output to identify the time of the CPU spike, its
duration, its amplitude, and whether, when CPU consumption is high,
whether this CPU is in kernel, user or wait I/O? Check also for
excessive paging.

### top output

Log top output to a file, for example with this command:

nohup top -b -n \> top.out &

which will collect "iterations" samples to an output file, *top.out*.
Assuming a 3-second delay time, maybe a value of 201600, which collects
data for a week, is appropriate for iterations. \[If so, the output file
could be quite large\]. If the mean time between CPU peaks, is small
(say daily) then a smaller value for \_\_ may be more practical.

Analyze the top output to check if there one process consuming a lot of
CPU, or several, or many? If it is just the java process that is
consuming memory, see the next section. If processes other than java are
responsible for the CPU peak, ascertain if these really need to run on
this system.

### top output for threads Follow the directions in [RedHat Java thread CPU monitoring](http://publib.boulder.ibm.com/infocenter/javasdk/tools/index.jsp?topic=2Fcom.ibm.java.doc.igaa2F_1vg0001475cb4a-1190e2e0f74-8000_1007.html) to collect per thread data for the Java threads.

### javacores

Run the [waittool](https://wait.ibm.com/) to collect javacores at the
time of the CPU spike with a 30 second frequency. Look at the stack
traces of the java threads that (in the above output) are responsible
for most of the CPU consumption.

##### Related topics: None [related-topics-none]

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]
