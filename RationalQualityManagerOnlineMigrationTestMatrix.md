META:TOPICINFO{author="qianjj" date="1443719530" format="1.1"
reprev="1.20" version="1.20"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Rational Quality Manager online migration test matrix [rational-quality-manager-online-migration-test-matrix]

DKGRAY Authors: Main.JingQian, Main.DavidWalker, Main.VaughnRokosz Build
basis: Rational Quality Manager 4.0.6, 4.0.7, 5.0.x ENDCOLOR

TOC{title="Page contents"}

## Disclaimer

The information in this testing matrix table is distributed AS IS. The
use of this information is a customer responsibility and depends on the
customers ability to evaluate into their operational environment. While
each item may have been reviewed by IBM for accuracy in a specific
situation, there is no guarantee that the same or similar results will
be obtained elsewhere. Any performance data contained in this document
was determined in a controlled environment, and therefore, the results
that might be obtained in other operating environments might vary
drastically. Users of this document should verify the applicable data
for their specific environment.

The actual throughput or performance that any user will experience will
vary depending upon many factors, including considerations such as the
network latency between servers, the I/O configuration, the storage
configuration, the workload processed, the DB server tuning and the
specific data shape. Therefore, no assurance can be given that an
individual user will achieve results similar to those stated here.

## Summary

Starting in Rational Quality Manager V4.0.6, you can choose to migrate
data from an older version of the product to the latest product version
while the production server is still online. This migration method is
called pre-upgrade online migration. Before implementing an online
migration, determine whether offline or online migration is warranted
for your repository by running the migration estimation command and then
checking the following test results matrix for guidance on the results.

If your database contains a large amount of data, online migration
reduces server downtime by running a few of the database migration tasks
while the old server remains active. The production server would
otherwise exceed the acceptable downtime window using the traditional
offline migration.

If online migration is recommended for your repository, follow the
detailed instructions in the [Online migration for Rational Quality
Manager
data](http://www-01.ibm.com/support/knowledgecenter/api/content/SSYMRC_5.0.2/com.ibm.rational.test.qm.doc/topics/c_online_mig_rqm.html).

**Note:** There is no online migration available from CLM 5.x to CLM 6.0
or CLM 6.0.1. The 6.0 [Infocenter
link](http://www-01.ibm.com/support/knowledgecenter/api/content/SSYMRC_6.0.0/com.ibm.rational.test.qm.doc/topics/c_online_mig_rqm.html)
for this topic is currently broken and will return "\_KC0024E: The topic
was not found. The link might not be correct, or the topic does not
exist. Check that the URL is correct and try again.\_". This is a known
issue, [defect
361962](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=361962).

## Understanding Performance Measure and Online Migration

Besides the ones mentioned above, the following factors also have
significant impact on your migration performance results. \* The network
latency from the server running migration to the database where your
repository resides \* If your database table index is up to date \* The
shape of your Rational Quality Manager data, specifically \* The number
of manual execution script state (you can get the count from the
onlineEstimate command) \* The number of script steps in each of the
script state \* The content size of each script step, does it contain
large amount of rich text, images.

The purpose of this testing matrix is to help customers extrapolate, in
terms of rough scale, what the migration performance might be. Using
this information, you can make a decision on whether to migrate using
the online or offline method. If in your environment the repository
exceeds 100GB and has 1,000,000 or more script states, it is strongly
recommended that application administrators should perform an online
migration to minimize production downtime. If you are unsure whether or
not online migration is correct for your deployment, we suggest that you
contact your support representative and the support team will guide you
to make the best decision for your organization.

During online migration, the online migration process runs as a separate
JVM against your live DB server. The data is migrated in such a way as
to not affect users on the existing server. The Rational Quality Manager
online migration process does not make modifications to your existing
data. It only migrates data into new tables in the database. Online
migration is designed to be stopped and resumed at any time. If there
are errors during online migration, once the underlying issues are
fixed, online migration can resume from where it left off.

RED **Best practice: To obtain a more accurate estimate of the migration
time, you should perform a practice migration using a sandbox
environment that replicates production data.** ENDCOLOR

## Testing matrix

| Customer data | Database | Repository size | Artifact counts ManualExecutionScript state counts | Data migration completed | Fully offline migration | Online migration recommended? | Online (priority=50) / Offline / Server impact (default setting) | DB statistics updated (Yes OR No) |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| Internal customer data |  |  |  |  |  |  |  |  |
| IGA (4.0.2) | DB2 | 380GB | 1 Million test script states | Yes | 38 hrs 35 minutes | Yes | 66 hrs / 1.5 hrs / negligible | Yes |
| IGA (3.0.1) | DB2 | 35GB | 46,000 test script states | Yes | 6 hours | No | Not applicable | No |
| Jazz.net (CLM selfhost test teams) | DB2 | 10GB | 1,000 test script states | Yes | One hour | No | 54 minutes / 6 minutes / Negligible | No |
| RESRQM01 | DB2 | 150GB | 120,000 test script states | Yes | 7 hrs 45 minutes | No | 11 hrs 50 minutes / 40 minutes / Negligible | Yes |
| External customer data |  |  |  |  |  |  |  |  |
| Healthcare sandbox | Oracle | 2GB | 200,000 test script states | Yes | 3 hours | No | Not applicable | No |
| Healthcare production data |  |  |  |  |  |  |  |  |
| Other |  |  |  |  |  |  |  |  |
| rqmx64d (RQM testbed) | DB2 | 42GB | 7,000 test script states | Yes | 35 minutes | No | Not applicable | No |

## Understanding how network latency can impact migration times

Our in-house testing identified network latency as one of the main
factors that influence the total migration time. Network latency refers
to the overhead of sending a data packet over the network from the
computer that is running the migration process to the database server.
You can get an estimate of network latency by running the "ping"
utility; run "ping" on the computer on which you plan to run the
migration utility, and "ping" the database server.

In the example below, the network latency can be estimated as the
average ping time (here, .36 millseconds):

Even small values of network latency (half a millisecond) will increase
the time required for migration, and this is multiplied as the number of
test scripts to be migrated increases.

The chart below shows how the time required to migrate 125,000 test
scripts increases as network latency is increased from .02 to 3
milliseconds. Each of these test runs used a priority of 100. The
migration was done while the Rational Quality Manager server was shut
down, to better isolate the impact of network latency from other
factors. In these tests, a network delay was injected artificially using
software running on the test system.

Each additional millisecond of network latency adds 343 minutes of
migration time for a 125K repository containing simple test scripts with
4 steps.

To estimate the additional time added to the migration process due to
network latency, you will first need to get the average ping time in
milliseconds between the migration server and the database server. You
will also need the total number of test scripts to be migrated (which
you can get by running "reptools-qm.sh -onlineMigrateEstimate" - use the
count of test script states but ignore the auditable link counts). Use
the following formula to estimate the overhead of network latency:

-   Migration time added due to network latency (minutes) = (343
    / 125000) \* (Average Ping Time) \* Total Script States \* ( 100 /
    Priority)

For example, if you had 2 million script states to migrate, with an
average ping time of 2 milliseconds and priority=100, the amount of
additional time required to migrate would be:

-   2 milliseconds \* 2,000,000 scripts ( 343 / 125000) (100 / 100) =
    10976 minutes (7.6 days)

If you ran the migration with priority=50, this would double the
migration time:

-   2 milliseconds \* 2,000,000 scripts ( 343 / 125000) (100 / 50) =
    21952 minutes (15.2 days)

If you have complex test scripts (more than 20 steps, or steps which
include images), increase the estimate by 25.

Note that this time is the additional cost due to network latency. To
get the total time, you can estimate the base migration time in a 0
latency environment and then add in the additional time due to latency.
For complex test scripts, a good rule of thumb is to assume that you can
migrate 300 scripts per minute (at priority = 100). In the prior
example, migration of 125,000 scripts would therefore take 125,000/300 =
416 minutes (7 hours). Over a 2 millisecond latency network, the total
migration time would be (Base time + latency cost) = 416 minutes + 21952
minutes = 15.5 days.

### Recommendations for dealing with latency

To reduce the total migration time, be sure to minimize the network
latency between the migration system and the database server. Consider
running the migration process on the database server if you don't have a
system with fast network access to the database server.

You can copy the "JazzTeamServer" directory to a temporary location on
your database server in order to run the migration. The migration
process is single-threaded, so it will add a small amount of CPU
overhead. The migration process will also consume roughly 1.5G of RAM.
For a typical database server which will have multiple CPU cores and RAM
sizes of 16G or more, the impact of running migration locally on the
database server will be small.

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [Online migration for Rational Quality Manager
    data](http://www-01.ibm.com/support/knowledgecenter/api/content/SSYMRC_5.0.1/com.ibm.rational.test.qm.doc/topics/c_online_mig_rqm.html)
-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.JingQian, Main.JohnNason, Main.RosaNaranjo, Main.PaulEllis [additional-contributors-main.jingqian-main.johnnason-main.rosanaranjo-main.paulellis]

META:FILEATTACHMENT{name="MigTimeVsLatency.png"
attachment="MigTimeVsLatency.png" attr="h" comment="Migration time as a
function of network latency" date="1410990169"
path="MigTimeVsLatency.png" size="8103" user="vrokosz" version="1"}
META:FILEATTACHMENT{name="PingExample.png" attachment="PingExample.png"
attr="h" comment="Example output from the ping command, to estimate
network latency" date="1410990765" path="PingExample.png" size="69350"
user="vrokosz" version="1"}
