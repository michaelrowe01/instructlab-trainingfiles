META:TOPICINFO{author="sbagot" date="1432664672" format="1.1"
version="1.16"} META:TOPICPARENT{name="PerformanceTroubleshooting"}

# Why does my RTC work item query take so long to run? DKGRAY Authors: Main.StephanieBagot Build basis: CLM 4.x and later [why-does-my-rtc-work-item-query-take-so-long-to-run-dkgray-authors-main.stephaniebagot-build-basis-clm-4.x-and-later]

ENDCOLOR

TOC{title="Page contents"}

This page will help you determine why Rational Team Concert queries are
slow to return results.

## When I run a query, what is actually happening?

All Rational Team Concert artifacts, such as work items, plans, and
source control artifacts, are indexed upon creation. The following
queries will run against the [Lucene
indexes](http://lucene.apache.org/core/): 1. "Full text" condition in
the query 2. The left bottom corner search box in Eclipse client for
quick search 3. The right top corner search box in web client for quick
search

All other queries (like regular query condition) will go against the
application database directly. For more information on how full-text
queries are formed, see [Getting the most out of full text
search](https://jazz.net/library/article/824).

## Symptoms and impact

Below are some additional questions to ask when troubleshooting query
performance:

-   Do the queries run for a long time and eventually complete? Or do
    they run for a long time and then fail?
-   Are you including multiple custom attributes in your query?
-   Is the slow query response time only related to some queries, or all
    queries?

## Initial assessment

1 Run the query from both the web client and Eclipse client to determine
if the behavior is the same. 1 Run multiple queries to see if the
behavior is the same across all queries.

## Possible causes and solutions

### Rebuilding the indexes

In some cases, the indexes used for queries become fragmented or grow
too large for quick searching capabilities. In this case, you should run
the following repotools commands to [Rebuild the text
indexes](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.install.doc/topics/r_repotools_rebuildtextindices.html),
and
[Reindex](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.install.doc/topics/r_repotools_reindex.html)
the triple store and Lucene indexes.

The Jazz Team Server manages a directory outside the database that
stores all data that is necessary to process full text queries. Below is
the relevant command to rebuild them: cd /server/ ./repotools-.sh
-rebuildTextIndices teamserver.properties= The queries will also use
triple store and Lucene text store indexes. Below is the relevant
command to rebuild them: cd /server/ ./repotools-.sh -reindex
teamserver.properties= scope=all

### Custom attributes

If multiple custom attributes are being queried, this might slow down
the application if the attributes are not synchronized with existing
work items. [Synchronize the work
items](https://www.ibm.com/support/docview.wss?uid=swg21372230) to
ensure that this is not contributing to the performance degradation.

### Database performance

Since queries (besides fulltext) run against the application database,
it is important to ensure you have no performance issues with the
database that can be contributing to the overall performance of your
queries. Review the article: [How to determine if my database has a
problem](https://jazz.net/wiki/bin/view/Deployment/HowToDetermineDBProblem)
for more information on troubleshooting.

### Complex queries

Queries will often return multiple rows of data. For example, a user
might want to see all of the work items that are in an open state for
which they are the owner. This makes the generation of the appropriate
SQL to retrieve data more complex, and can often return more data than a
simple query for a single work item.

### Malformed and non-optimal SQL queries

Malformed and non-optimal SQL queries can cause an increase in database
response times which might affect performance.

The Jazz applications are driven by user actions, and they use a dynamic
query building engine to build specific queries based on the user
actions and requests. Certain user requests to the Jazz application can
cause this dynamic query engine to produce queries that are not optimal.
The queries might not be well scoped, and might retrieve more data than
is needed. An administrator should note the time when these spikes in
database response times occur, and then check for a corresponding event
or events within the database specific metrics.

In these cases, the simple indexing of particular database tables within
the Jazz repository can address the performance issue. Use the database
specific metrics and diagnostics to help determine when these conditions
are being encountered, and when this can help address performance
issues.

## Known issues

-    **Queries on newly added data are slower after upgrading to
    Rational Team Concert 4.0.1** Although queries might keep responding
    when only dealing with pre-migration data, queries on newly added
    data might either take a significantly longer time or even time out.
    See [Upgrades to 4.0.1 create a significantly larger, incorrect
    index](http://www.ibm.com/support/docview.wss?uid=swg21620879) for
    more information.

##### Related topics: [related-topics]

-   Still need help troubleshooting your performance issue? Refer to
    [Performance Troubleshooting](PerformanceTroubleshooting) for
    additional topics.

##### External Links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]
