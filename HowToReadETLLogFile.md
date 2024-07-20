META:TOPICINFO{author="sbagot" date="1432663644" format="1.1"
version="1.14"} META:TOPICPARENT{name="WhyDoMyETLsTakeSoLongToRun"}

# How to read ETL log files [how-to-read-etl-log-files]

DKGRAY Authors: Main.StephanieBagot Build basis: CLM 4.x, 5.x ENDCOLOR

TOC{title="Page contents"}

This analysis page will help to understand how to read ETL (Extract,
Transform, Load) log files when using reporting with IBM CLM
applications.

## Reading the ETL log file

A typical ETL log file will display the following information:
2013-02-18 19:07:34,106 \[ ccm: AsynchronousTaskRunner-3\] DEBUG
ervice.internal.common.CommonRemoteSnapshotService - ETL: \*\*\*Started
Build IterationParent at 2/18/13 7:07 PM**\*** 2013-02-18 19:07:34,216
\[ ccm: AsynchronousTaskRunner-3\] DEBUG
ervice.internal.common.CommonRemoteSnapshotService - ETL: Records
Selected: 0 2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\]
DEBUG ervice.internal.common.CommonRemoteSnapshotService - ETL: Records
Inserted: 0 2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\]
DEBUG ervice.internal.common.CommonRemoteSnapshotService - ETL: Records
Updated: 0 2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\]
DEBUG ervice.internal.common.CommonRemoteSnapshotService - ETL: Records
Ignored: 0 2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\]
DEBUG ervice.internal.common.CommonRemoteSnapshotService - ETL: Time
Inserting: 0ms 2013-02-18 19:07:34,216 \[ ccm:
AsynchronousTaskRunner-3\] DEBUG
ervice.internal.common.CommonRemoteSnapshotService - ETL: Time Updating:
0ms 2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\] DEBUG
ervice.internal.common.CommonRemoteSnapshotService - ETL: Time Looking
Up: 0ms 2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\] DEBUG
ervice.internal.common.CommonRemoteSnapshotService - ETL: Time Fetching
Data: Less than 1ms 2013-02-18 19:07:34,216 \[ ccm:
AsynchronousTaskRunner-3\] DEBUG
ervice.internal.common.CommonRemoteSnapshotService - ETL: Time Running:
Less than 1ms 2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\]
DEBUG ervice.internal.common.CommonRemoteSnapshotService - ETL:
\*\*\*Finished Build IterationParent at 2/18/13 7:07 PM. The build was
successful**\***

This can be broken down as follows: 2013-02-18 19:07:34,106 \[ ccm:
AsynchronousTaskRunner-3\] DEBUG
ervice.internal.common.CommonRemoteSnapshotService - ETL: \*\*\*Started
Build IterationParent at 2/18/13 7:07 PM**\*** 1. The first line
indicates which build within the ETL is run and the date and timestamp.
In the example above, the Build IterationParent was started on 2/18/13
at 7:07 PM.

2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\] DEBUG
ervice.internal.common.CommonRemoteSnapshotService - ETL: Records
Selected: 0 2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\]
DEBUG ervice.internal.common.CommonRemoteSnapshotService - ETL: Records
Inserted: 0 2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\]
DEBUG ervice.internal.common.CommonRemoteSnapshotService - ETL: Records
Updated: 0 2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\]
DEBUG ervice.internal.common.CommonRemoteSnapshotService - ETL: Records
Ignored: 0 2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\]
DEBUG ervice.internal.common.CommonRemoteSnapshotService - ETL: Time
Inserting: 0ms 2013-02-18 19:07:34,216 \[ ccm:
AsynchronousTaskRunner-3\] DEBUG
ervice.internal.common.CommonRemoteSnapshotService - ETL: Time Updating:
0ms 2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\] DEBUG
ervice.internal.common.CommonRemoteSnapshotService - ETL: Time Looking
Up: 0ms

2\. The ETL will first Look Up the data. This is where the data's
external IDs are obtained, and compared against the Data Warehouse
integer keys. In the example above, this time was 0 ms. Once the look up
finds data that matches, it will determine if the records will be
inserted (new data) or updated (existing data in the datawarehouse).
Time for each of the Update/Inserted steps will be provided in the log,
as well as how many records were selected for update/insert.

2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\] DEBUG
ervice.internal.common.CommonRemoteSnapshotService - ETL: Time Fetching
Data: Less than 1ms

3\. The next step is Fetching the Data. This will actually bring the
data from the application database into the data warehouse.

2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\] DEBUG
ervice.internal.common.CommonRemoteSnapshotService - ETL: Time Running:
Less than 1ms 2013-02-18 19:07:34,216 \[ ccm: AsynchronousTaskRunner-3\]
DEBUG ervice.internal.common.CommonRemoteSnapshotService - ETL:
\*\*\*Finished Build IterationParent at 2/18/13 7:07 PM. The build was
successful**\*** 4. The Total time running displays the amount of time
that the build ran for.

## Key areas to look for in the ETL log file

### Errors

You may see errors at the end of the ETL indicating that the ETL failed,
but errors may also be contained within each build. Oftentimes, if one
build fails, the ETL will move onto the next build which may contribute
to long running ETLs. Is is important to review each build as its own
item to ensure there are no failures.

### Time fetching data

If the time to fetch data increases dramatically between ETL runs, this
may be indicative of database latency problem as the data is brought
from one database into another. The time to run the ETL may also be
impacted if there are long delays between the entries. If this occurs,
it may be due to a process being waited for, garbage collection, logging
allocation, etc.

### Baseline and state history jobs

The Baseline and State History Jobs will actually move data from the
data warehouse. This type of data is used in trend reports and these
ETLs are often the slowest.

## How can reading the ETL log file help to isolate ETL performance?

## Keywords to aid searching [keywords-to-aid-searching]

ETL extract transform load data collection job star common RTC RQM
Insight JTS time delay report data long length slow freeze frozen
response XDC error exception disable variable STAR datamanager custom

##### Related topics: [related-topics]

-   Still need help troubleshooting your performance issue? Refer to
    [Performance Troubleshooting](PerformanceTroubleshooting) for
    additional topics.
-   [How to read ETL log files](HowToReadETLLogFile)
-   [Why do my OOB ETLs take so long to
    run?](WhyDoMyOutOfTheBoxETLsTakeSoLongToRUN)
-   [Why do my custom ETLs take so long to
    run?](WhyDoMyCustomETLsTakeSoLongToRun)
-   [Long-running ETLs with error(s)](LongRunningETLError)
-   [Long-running ETLs without error(s)](LongRunningETLNoError)

##### External links: [external-links]

-   <http://en.wikipedia.org/wiki/Extract,_transform,_load>
-   <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/topic/com.ibm.rational.reporting.admin.doc/topics/t_running_the_data_collection_jobs.html>
-   <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/topic/com.ibm.rational.reporting.admin.doc/topics/c_data_collection.html>

##### Additional contributors: None [additional-contributors-none]
