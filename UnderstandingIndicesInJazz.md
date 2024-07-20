META:TOPICINFO{author="lekandrade" date="1694545740" format="1.1"
version="1.13"} META:TOPICPARENT{name="PerformanceTroubleshooting"}

# Understanding indices in Jazz [understanding-indices-in-jazz]

DKGRAY Authors: Main.GeraldMitchell main. Build basis: Collaboration
Lifecycle Management (CLM) 4.0 Jazz Team Server(JTS) 4.0 Rational Team
Concert(RTC) 4.0 ENDCOLOR

TOC{title="Page contents"}

This is guidance to understand the indices used in CLM (Jazz).

## Understanding Indices and Stores

There are several stores and indices associated with your Jazz
applications.

### Indices and their function

Indices will be a direct correlation with the performance of the
application. Essentially, the index is a look-up table for the
information that can be more easily queried and result in faster
responses.

#### General notes on rebuilding the indices.

There are a few ways of rebuilding an index within the Jazz system, and
several points where it is desired or necessary.

-   You may be presented with an option to rebuild the index through the
    Setup wizard.
-   The Administration Web User Interface has the capability to initiate
    an online index rebuild.
-   The command line interface through repotools has options to rebuild
    the index.

Rebuilding the index may be needed if the index has been deleted, become
stale, become fragmented, or if the data structure has changed.

-   For an initial install, the creation of an index is necessary
-   For some upgrades, the rebuild of the index may be presented in the
    Setup
-   After a database version change rebuilding the index may be needed.
-   After a database migration rebuilding the index is required.

See the [Possible Problems with Indices](#PossibleCausesAndSolutions)
section for more information.

#### Backing up the Indices

Before rebuilding an index, consider backing up the indices.

There may be cases where the previous index is needed by support or a
situation that desires a reversion to that index, such when the indexing
is taking longer than can be afforded to wait. Note that the indices
should be part of your normal backup schedule for the Jazz system and
coordinated with the Database backup.

Note that there is a way to rebuild the indices through the
Administrator Web UI, which will allow the system to be still
operational while rebuilding the index. In this case, from the command
line while the server is currently running, use repotools
-suspendIndexer, then backup the indices (possibly using repotools-jts
-backupJFSIndexes) and then repotools -resume Indexer.

### Query Triple store and index

The query triple store index can be rebuilt using repotools command
parameter -reindex scope=query.

### Full Text index

The full text index can be found where ever your setting in the
teamserver.properties of your application says it is located in the
property ***com.ibm.team.fulltext.indexLocation***
com.ibm.team.fulltext.indexLocation=/opt/IBM/JazzTeamServer/workitemindex

***Note***: For high availability applications, have the Jazz Team
Servers reference the same location for the full text index. To keep the
index up to date and available for all servers, each server
teamserver.properties should update the
***com.ibm.team.fulltext.indexLocation*** in teamserver.properties to
store the index for the full text on a single shared drive location.

More information on the full text search can be found in [Technote
1586008](http://www-01.ibm.com/support/docview.wss?uid=swg21586008)

#### Lucene Text store and index

-   What is Lucene?
    -   Lucene is an open-source full-text indexing and search engine
        library.
    -   It also has other capabilities such as spellchecking and
        highlighting.
    -   For more information see [Apache
        Lucene](http://lucene.apache.org/) and the [Getting the most out
        of full text search
        article](https://jazz.net/library/article/824)
    -   see [Technote
        1586008](http://www-01.ibm.com/support/docview.wss?uid=swg21586008)
        as well
-   Team Server Properties for Lucene
    -   teamserver.properties to be aware of include
        ***com.ibm.team.jfs.lucene.directory*** and
        ***com.ibm.team.jfs.lucene.history.directory***.
-   Rebuilding the Lucene index
    -   The repotools -rebuildTextIndices commmand is used. See the
        [rebuildTextIndices](#RepotoolsRebuildTextIndices)

#### Performance considerations

-   Because the Lucene is used for a lot of lookups, to increase
    performance:
    -   The Lucene Index Directory com.ibm.team.jfs.lucene.directory
        path should be on fast storage
    -   The Lucene History Index Directory
        com.ibm.team.jfs.lucene.history.directory path should be on fast
        storage
    -   The full text location should be on fast storage

### Database index

-   The database index is used to locate artifacts within the database
    quickly.
-   The database index may need to be reindexed in cases where the
    database index has become fragmented. \* Database indices are
    rebuilt using the repotools -rebuildIndices command. see
    [rebuildIndices](#RepotoolsRebuildIndices) for more information. \*
    Also consider using the full -reindex in cases where database
    indices need to be rebuilt, because a database index is used as a
    reference point.

## repotools functions

\#ReptoolsReindex

### repotools reindex

-   Repotools-(applications) -reindex: Repository tools command to
    regenerate indexes.
    -   The application must not be running before the command is run.
    -   Use the reindex command to regenerate stores.
    -   By default, the query triple store and the Lucene text store are
        regenerated
    -   The "scope" parameter can be used to rebuild the query, the text
        indexes, or both.
        -   all: to rebuild all indexes (default) - "all" in this case
            encompasses query triple store and the Lucene test store
            indexes
        -   query: to rebuild query triple store indexes
        -   search: to rebuild Lucene text store indexes
        -   An example repotools-jts.sh -reindex scope=query
        -   This parameter is useful to limit the scope of the reindex
            to the needed store indexes, making the reindex time shorter
    -   The "all" parameter to reindex both live and history indices
        -   An example repotools-jts.sh -reindex all
    -   The "baselines" parameter is allowlist (inclusive-only) set of
        baselines to reindex
        -   A comma separated list of baselines URI, without spaces.
        -   An example repotools-jts.sh -reindex
            baseline=<http://jazz.net/jts/dashboards>
        -   This parameter is useful to limit the reindex to the needed
            baselines, making the reindex time shorter

\#RepotoolsRebuildTextIndices

### repotools rebuildTextIndices

-   Repotools-(applications) -rebuildTextIndices: Repository tools
    command to rebuild text indexes in the event of them becoming
    fragmented. This command rebuilds the entire Lucene text index from
    the database, for use in full text searches across all artifacts.
    -   The application must not be running before the command is run. (
        you can check using repotools command -isServerRunning)
    -    An example repotools-jts.sh -rebuildTextIndices

### repotools compacttdb

-   Repotools-(applications) -compacttdb: Compact the TDB
    -   The application must not be running before the command is run. (
        you can check using repotools command -isServerRunning)
    -   The TDB indexes can grow to be large. The compacttdb command
        alleviates this problem by forcing a compaction of the indexes.
    -   srcdir The directory containing the RDF indexes to be compacted.
    -   tempdir The temporary directory to use while compacting the RDF
        indexes
    -   An example repotools-jts.sh -compacttdb srcdir={location of RDF
        indexes} tempdir={location of temporary directory}

\#RepotoolsRebuildIndices

### repotools rebuildindices

-   Repotools-(applications) -rebuildindices: Repository tools command
    to rebuild database indexes in the event of them becoming
    fragmented.
    -   The application must not be running before the command is run. (
        you can check using repotools command -isServerRunning)
    -    An example repotools-jts.sh -rebuildindices

\#PossibleCausesAndSolutions

## Possible Causes and Solutions

### The queries are slow or having issues

-   The query triple store indexes need to be re-indexed

### Items seem to be disappearing

-   May also manifest as known artifacts that cannot be found through
    search or related items
-   The database index may need to be rebuilt. All of the indices may
    need to be rebuilt.
-   If this condition persists, or continuously occurs, contact support.

### Text searches are not finding the correct artifacts

-   May also manifest as not finding artifacts during searches in which
    the searched text is known to exist
-   The full text index needs to be rebuilt.

### The TDB has grown too large

-   The TDB needs to be compacted

##### Related topics: None [related-topics-none]

##### External links: \* [Query and Search indices management in the Rational solution for Collaborative Lifecycle Management Part 1: Query, Search and indexing technologies in CLM jazz.net article 1271](https://jazz.net/library/article/1271) [external-links-query-and-search-indices-management-in-the-rational-solution-for-collaborative-lifecycle-management-part-1-query-search-and-indexing-technologies-in-clm-jazz.net-article-1271]

-   [JQuery and Search indices management in the Rational solution for
    Collaborative Lifecycle Management Part 2: Indices storage and
    management: Backup, recovery and recreation jazz.net article
    1272](https://jazz.net/library/article/1272)

##### Additional contributors: None [additional-contributors-none]
