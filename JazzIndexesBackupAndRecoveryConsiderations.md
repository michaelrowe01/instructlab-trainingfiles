META:TOPICINFO{author="sbeard" date="1490024167" format="1.1"
version="1.10"} META:TOPICPARENT{name="ApproachesToImplementingHAAndDR"}

# Jazz indexes backup and recovery considerations [jazz-indexes-backup-and-recovery-considerations]

DKGRAY Authors: Main.TimFeeney Build basis: v4.0.x and 5.0.x Jazz
applications in CLM and SSE ENDCOLOR

TOC{title="Page contents"}

The Jazz CLM applications utilize a set of indices to implement its
query and search services. Care must be taken to ensure these are backed
up in a consistent state and restored propertly to recover from various
errors, issues and failures that may occur

It is important to understand the structure and technology behind these
indices, the correct procedure for backup and restore and any
considerations for relevant failure scenarios.

## Jazz indices at a glance

In the Jazz CLM applications, different implementations of the query and
search services exist based on how their implementation architecture and
what frameworks are used. Since CLM v4.0, all the applications use the
Jazz Application Framework (JAF), however, how the application is
constructed and the SDKs in use lead to different implementations of the
query and search capabilities. The three primary implementations can be
categorized as Item Query Service, JFS Query and Search Services and
Fulltext Search Service. All applications make use of the JFS Query and
Search Services implementation. CCM and QM also make use of the Item
Query Service and Fulltext Search Service. This is important to know
because the implementation used impacts how backup and restore is
performed. In particular, it is the indexes based on a Fulltext Search
Service implementation that need to be handled more carefully. For more
complete details on the query and search service implementation see
[Query, Search and indexing technologies in
CLM](DeploymentJazzIndicesTechnology) and [Indices storage and
management: Backup, recovery and
recreation](DeploymentJazzIndicesStorage).

## Backup and Restore

As of 4.0.5, JFS indices can be backed up online, while their
application is running and as of 5.0.1, the Fulltext indices used by CCM
and QM can be backed up online as well. For that reason, prior to 5.0.1,
it is advised that all indices are backed up, along with their
corresponding databases, while the servers are shutdown. Similarly,
restore the indices and databases while the servers are shutdown.

See [Backing up CLM](BackupCLM) for the recommended strategy for a
comprehensive offline backup and restore of a CLM environment. In
particular see the sections on backup of the
[JFS](BackupCLM#Backing_up_the_JFS_index_files) and
[Fulltext](BackupCLM#Backing_up_the_Fulltext_index_fi) indices and
[temporal](BackupCLM#Temporal_database_consistency_du) considerations
when doing so.

## Failure scenarios/considerations

Prior to 5.0.1, with the exception of the work item Fulltext indices, if
Jazz indices are suspected of being corrupted, a backup could be
restored and the applications will eventually 'catch up' the indexes to
current state with no reindex operation required. Reindexes are costly
and time consuming. A more desirable strategy is to perform nightly
backups and if a failure occurs, restore from backup and let the indexes
be caught up incrementally by the applications. Starting with 5.0.1,
this can now be done with work item Fulltext indexes.

When a Jazz application fails or the indices are suspected of being
corrupt, it would be good to run some sort of verification on the
indices before performing any recovery process. This is now possible
starting in 5.0.1. See [Verifying
indices](DeploymentJazzIndicesStorage#Verifying_indices).

##### Related topics: [Approaches to implementing high availability and disaster recovery for Rational Jazz environments](ApproachesToImplementingHAAndDR) [related-topics-approaches-to-implementing-high-availability-and-disaster-recovery-for-rational-jazz-environments]

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]

META:TOPICMOVED{by="sbeard" date="1394442986"
from="Deployment.CLMIndexesBackupAndRecoveryConsiderations"
to="Deployment.JazzIndexesBackupAndRecoveryConsiderations"}
