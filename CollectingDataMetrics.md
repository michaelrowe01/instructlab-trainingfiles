META:TOPICINFO{author="tfeeney" date="1595435362" format="1.1"
reprev="1.3" version="1.3"} META:TOPICPARENT{name="MBeansUsage"}

# Collecting data related metrics using JMX MBeans DKGRAY Authors: Main.TimFeeney Build basis: 6.0.6.1 and later [collecting-data-related-metrics-using-jmx-mbeans-dkgray-authors-main.timfeeney-build-basis-6.0.6.1-and-later]

ENDCOLOR

TOC{title="Page contents"}

One element of sizing the servers for the IBM ELM solution is the
current and projected data scale (along with data shape, user scale and
workload). There are also recommended artifact limits to stay within to
keep an application performing well. There are a few different MBeans
that will help keep track of data counts.

## Item Count Details MBean

This bean will list several objects of various types (i.e. different
typeName values), such as *com.ibm.team.workitem.Attachment* when
collected for the Engineering Workflow Management (EWM) application.
Each object collected has several attributes with those of prime
interest being:

-   ***itemTypeName*** - the name of the type of item being counted,
    e.g. com.ibm.team.workitem.Attachment,
    com.ibm.team.workitem.WorkItem, com.ibm.team.vvc.ChangeSet
-   ***noOfContents*** - how many items of this type exist in the
    application's repository
-   ***totalSize*** - the total size in the application's repository for
    items of this type
-   ***sizePercentage*** - the size of this item type as a percentage of
    all the other item types in the application's repository

A common use of this information is to see what is contributing to the
size of a repository database. For the EWM application, workitem
attachments often take up a lot of the space. This bean will help track
growth of those items typically taking up most space in the repository.
Strategies then can be put in place to reduce their size, such as use of
the [attachment migration utility](WorkitemAttachmentMigrationUtility)
to [remove orphaned
attachments](https://trfeeney.wordpress.com/2020/05/29/reduce-your-engineering-workflow-management-database-size-by-removing-orphaned-attachments/).

Further, tracking the number of artifacts in a repository for some
applications is important given some applications have known size
limits. For example, the Engineering Test Management (ETM) application
has been [tested with up to 15 million artifacts in
v7.0.1](ELMLargeScaleAndPerformanceReportRelease701). Tracking all the
relevant item types that contribute to the [overall ETM artifact count
size](ELMLargeScaleAndPerformanceReportRelease701#Data_volume_and_shape),
would be advisable to ensure you stay within the limit and track your
growth towards it. This allows you to be proactive in managing growth
and taking appropriate actions, such as deploying another application
server.

## Project Area Information MBean

Whereas the Item Count Details MBean provides data counts at the
application repository level, the Project Area Information provides some
details on the project areas of an application. There are several
attributes of interest, but for purposes of tracking data counts
relevant to sizing, consider the following (see the reference
documentation for the full list).

-   ***workitemCount*** - total number of workitems in an EWM project
    area
-   ***attachmentCount*** - total number of workitem attachments in an
    EWM project area
-   ***attachmentTotalLength*** - total size of workitem attachments in
    an EWM project area
-   ***totalNoOfComponents*** - total number of components in a
    configuration management enabled project area
-   ***totalNoOfStreams*** - total number of streams in a configuration
    management enabled project area
-   ***totalNoOfBaselines*** - total number of baselines in a
    configuration management enabled project area
-   ***rmArtifactCount*** - total number of artifacts in a configuration
    management enabled DOORS Next project area

There are no known limits for the different EWM data elements (work
items, files, builds, etc.) in a project area, however you might find it
useful to track which projects are most active and making use of
workitems. Per the discussion on the Item Count Details MBean, tracking
the size of attachments in a repository is important to help manage the
overall EWM database size. Tracking *attachmentTotalLength* in the
Project Area Information MBean allows you to see which projects are the
primary contributors to attachment storage.

In [7.0 performance: IBM Engineering Requirements Management DOORS
Next](RequirementsManagement70Performance#DataLimits), there are
recommended data limits for a project area, such as its total artifacts
and components. These can be monitored with the *totalNoOfComponents*
and *rmArtifactCount* attributes of this MBean.

Note that collecting data for the Item Count Details MBean can be
[resource intensive](CLMExpensiveScenarios#Item_count_metrics); care
should be taken to when it is scheduled and how frequent.

## DOORS Next MBeans

In 7.0, DOORS Next implemented several [MBeans](RDNG70Beans) to aid in
tracking various data shapes at the repository level. At a minimum, plan
to monitor these DOORS Next MBeans:

-   ***TotalNumberOfArtifacts*** - total artifacts in a DOORS Next
    application repository
-   ***TotalNumberOfComponents*** - total components in a DOORS Next
    application repository
-   ***TotalNumberOfBaselines*** - total baseline configurations in a
    DOORS Next application repository
-   ***TotalNumberOfStreams*** - total stream configurations in a DOORS
    Next application repository
-   ***TotalNumberOfLinks*** - total links within and between components
    and projects in a DOORS Next application repository

Each of these have their own *Value* attribute that publishes the count
for the data item it is tracking. Of these *TotalNumberOfArtifacts* and
*TotalNumberOfComponents* have [published limits for
7.0](RequirementsManagement70Performance#Data_limits_in_7_0).

Note that calculation of the values for these DOORS Next MBeans can add
substantial load on large repositories; care should be taken to when it
is scheduled and how frequent.

##### External links: [external-links]

-   [How many artifacts do I have in my Jazz application
    repository?](https://trfeeney.wordpress.com/2018/06/12/how-many-artifacts-do-i-have-in-my-jazz-application-repository/)
