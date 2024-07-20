# AIX CPU spike

Authors: Main.MichaelAfshar 
Build basis: AIX 6.1 or later

Introductory paragraph: TBD

## AIX CPU monitoring

1.  system overview
2.  vmstat data with a 1 second granularity, timestamped
3.  top output (with a 2 or 3 second granularity)
4.  tprof data samples during the CPU spike
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

Running the AIX "lparstat -i" answers most of the questions we may have.

lparstat -i

We refer the reader to the lparstat man page for field by field
descriptions of this output. One may need to look at CEC data to build
up a more complete picture of the LPARs sharing a CPU pool with this
one.

### vmstat

To locate the time of the CPU spike, and to gain an insight into whether
user or system CPU is being consumed at this time, the best tool to use
is vmstat. The preferred flags to use for this are:

vmstat -wtI 1

This command should be issued in the background, wrapped with a nohup
command, and redirecting the output to a file. This will collect data
with a 1 second granularity. Please note that this level of granularity
is necessary for a comprehensive insight into the consumption of this
resource. A system administrator may well be running other tools that
are also collecting data (e.g. topasrec, or sar) with a larger (e.g. 5
minute or 15 minute) granularity - but this output, though useful for
capacity planning purposes, will not be helpful in the analysis of
possibly short-lived CPU spikes.

Check the vmstat output to identify the time of the CPU spike, its
duration, its amplitude, and whether, when CPU consumption is high,
whether this CPU is in kernel, user or wait I/O? Check also for
excessive paging.

### topas output

Log topas output to a file.

Analyze the top output to check if there one process consuming a lot of
CPU, or several, or many? If it is just the java process that is
consuming memory, see the next section. If processes other than java are
responsible for the CPU peak, ascertain if these really need to run on
this system.

### top output for threads 
Follow the directions in [AIX Java thread CPU monitoring](http://publib.boulder.ibm.com/infocenter/javasdk/tools/index.jsp?topic=2Fcom.ibm.java.doc.igaa2F_1vg0001475cb4a-1190e2e0f74-8000_1006.html) to collect per thread data for the Java threads.

### javacores

Run the [waittool](https://wait.ibm.com/) to collect javacores at the
time of the CPU spike with a 30 second frequency. Look at the stack
traces of the java threads that (in the above output) are responsible
for most of the CPU consumption.

##### Related topics: 
None [related-topics-none]

##### External links: 
  * None [external-links-none]

##### Additional contributors: 
None [additional-contributors-none]
