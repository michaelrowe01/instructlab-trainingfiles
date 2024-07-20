META:TOPICINFO{author="paulellis" date="1570103897" format="1.1"
reprev="1.15" version="1.15"}
META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Database Growth - Strategies for minimizing the growth of repository databases DKGRAY Authors: Main.RosaNaranjo Build basis: None [database-growth---strategies-for-minimizing-the-growth-of-repository-databases-dkgray-authors-main.rosanaranjo-build-basis-none]

ENDCOLOR

TOC{title="Page contents"}

In planning or maintaining your CLM deployment, you may ask yourself
these questions: "How do I ensure that my database size will not spiral
out of control?", "Are there any strategies I can put in place to help
with this in the beginning?", "Are there objects I should avoid storing
in my repository?". There are some recommendations that will be captured
in this page as well as some links to content that will help you
understand \<...\>

## Engineering Workflow Management/Rational Team Concert

In Engineering Workflow Management, formerly Rational Team Concert,
there are several items that can contribute greatly to database growth
if not kept in check. These items are build results, workitem
attachments, and binary content in SCM as versioned content. There are
several articles and presentations that have been written on this topic.

-   [Moving An Source Code Management Component To A New
    Server](MovingAComponentToANewServer)
-   [Help! My RTC Database is getting
    big!](https://trfeeney.wordpress.com/2014/12/09/help-my-rtc-database-is-getting-big/)
-   [Deleting data in Engineering Workflow Management](DataDeletionRTC)
-   [Reducing the size of the Rational Team Concert repository
    database](https://jazz.net/library/article/1459)
-   [Deleting content in RTC](https://jazz.net/library/article/1006)

## Engineering Test Management/Rational Quality Manager

For QM, there are some usages that can drive repository db growth. For
example, automations generating Execution Results and attachments on the
test artifacts such as HTML, images, etc. attached to either scripts or
results. QM does have some ability to permanently delete content. See
[Deletion and restoration of test
artifacts](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.3/com.ibm.rational.test.qm.doc/topics/c_deleting_artifacts.html).

## DOORS Next Generation

The "safest" way to reduce DB size is to archive projects and use the
repotools -deleteJFSResources
[command](https://jazz.net/help-dev/clmindex.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fr_repotools_deleteprojectarearesources.html)
Note that this can have consequences, for example, what if you have
cross project links from other projects?. You can also run that command
against unarchived projects to clean up artifacts in that project which
have been deleted, but that may affect baselines and history that may be
important.

One thing changed between 5.x and 6.x though, which is you can no longer
run deleteJFSResources without the "force" parameter which deletes
everything in the specified project. This is due to the way resources
are unmapped versus archived, so running without "force" in 6.x seems to
not find anything to delete. Otherwise, there is one other task,
com.ibm.team.jfs.indexing.service.internal.CompactIndexesTask that can
be scheduled daily/weekly to help manage the index size. See this
[page](https://jazz.net/downloads/jazz-foundation/releases/5.0?p=news#jfs_index_compaction)
for details.

[Deleting data permanently from a DOORS Next Generation
project](http://www-01.ibm.com/support/docview.wss?uid=swg21458233)

**UPDATE**: Prior to DOORS Next Generation 6.0.6, this task should NOT
be enabled,
com.ibm.team.jfs.indexing.service.internal.CleanUpUnusedIndexesVersionsTask
See [CleanUpUnusedIndexesVersionsTask incorrectly cleans up versions
still in
use](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/434658)
defect for details.

If you are using 6.0.6, then the task is automatically set to run daily.
See the following guidance issued on this task and the related repair
command. i. [OutOfMemoryException errors and performance degradation
caused by the CleanUpUnusedReferences task for DOORS Next
Generation](https://www-01.ibm.com/support/docview.wss?uid=ibm10796082)
ii. [Upgrading DOORS Next Generation to 6.0.6 requires that
repairUnreferencedVersions is run before running a
reindex](http://www.ibm.com/support/docview.wss?uid=ibm10796118)

The CleanUpUnusedIndexesVersionsTask is an important part of maintaining
a reduced index size and optimize DNG performance. The guidance above
will allow you to utilise this daily feature.

### Data Warehouse

[Data warehouse database size is huge and growing
fast](http://www-01.ibm.com/support/docview.wss?uid=swg21986358)

### Jazz.net forum resources

The forum contains many good suggestions from CLM Administrators who are
maintaining CLM deployments.

Question: I want to store binaries in RTC. Does RTC SCM support delta
compression?

Answer: Yes. RTC SCM supports delta compression of files, including
binary files. In fact, one of the properties you can change in advanced
properties is whether to enable or disable delta compression. If delta
compression results in larger gains than other compression types it will
be used to compress a given binary.

Question: Can I prevent binaries from being checked-in to RTC?

Answer: Yes, you can implement file limits in RTC.

Question:Does RTC store all versioned elements in the database?

Answer:Yes, RTC-SCM stores all versioned elements in the database.

Question:What can I do to monitor db growth and what does RTC do on its
own?

Answer:

-   RTC will run item cleanups daily (sometimes frequently throughout
    the day) to help clean stale data. You can investigate increasing
    this task, or the expiration time of these items (located in
    Advanced Properties)
-   You can also run the
    [onlineverify](https://jazz.net/wiki/bin/view/Main/L3DevTool) to
    ensure the consistency of the data and that there is no corruption
    which may be preventing the item clean up from running.
-   ensure all your builds are being pruned and any results cleaned up

**Question** How can you scrub ChangeEvents from the repository database
using IBM Rational Team Concert?

**Answer**
<http://www-01.ibm.com/support/docview.wss?rs=3488&uid=swg21390701>

<https://jazz.net/forum/questions/92505/data-warehouse-db-sizing>

<https://jazz.net/forum/questions/20098/are-there-ant-way-for-me-to-reduce-size-of-the-rtc-db>

<https://jazz.net/forum/questions/73442/rtc-compression-for-binary-files-vs-clearcase>

<https://jazz.net/forum/questions/66014/rtc-large-history-complexity-and-archiving-questions>

<https://jazz.net/forum/questions/128039/what-is-the-latest-metrics-by-namespace-report-means>

<https://jazz.net/forum/questions/19251/rather-surprising-db2-growth>

## References

[DatabaseMaintenanceFAQ](https://jazz.net/wiki/bin/view/Main/DatabaseMaintenanceFAQ)

[expected database growth when versioning binary
data](https://jazz.net/forum/questions/61330/expected-database-growth-when-versioning-binary-data)

[Versioning binary
artifacts](https://jazz.net/forum/questions/65323/versioning-binary-artifacts#page=0&type=&q=database2Bgrowth)

##### Related topics: [Deployment Planning and Design](DeploymentPlanningAndDesign), [Why is my database consuming so many resources?](WhyIsMyDatabaseConsumingSoManyResources) [related-topics-deployment-planning-and-design-why-is-my-database-consuming-so-many-resources]

##### Additional contributors: TimFeeney, StefVanDijk, BenjaminSilverman, KrzysztofKazmierczyk [additional-contributors-timfeeney-stefvandijk-benjaminsilverman-krzysztofkazmierczyk]

META:FILEATTACHMENT{name="RDNG.gif" attachment="RDNG.gif" attr=""
comment="" date="1467912076" path="RDNG.gif" size="18631"
user="rnaranjo" version="1"}
