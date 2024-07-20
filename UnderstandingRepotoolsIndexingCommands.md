META:TOPICINFO{author="rnaranjo" date="1544048392" format="1.1"
reprev="1.2" version="1.2"}
META:TOPICPARENT{name="DeploymentAdminstering"}

# Understanding the various repotools indexing commands DKGRAY Authors: Main.RosaNaranjo, Main.GlennBardwell Build basis: Rational Collaborative Lifecycle Management solution [understanding-the-various-repotools-indexing-commands-dkgray-authors-main.rosanaranjo-main.glennbardwell-build-basis-rational-collaborative-lifecycle-management-solution]

ENDCOLOR

TOC{title="Page contents"}

The question often comes up "When should I use one repotools indexing
command versus another?" Repotools includes the following command line
options for indexing, -reindex all,-synchronizeJFSIndexes, -reindex
scope=all, -reindex scope=query, -reindex scope=search,
-rebuildTextIndices and -rebuildIndices.

Don't use repotools -reindex scope=all. Instead use repotools -reindex
all.

Use repotools -rebuildTextIndices when you have the following symptoms:

You run a quick search (the edit box in the lower left hand side of the
thick client, or upper right side of the web client) for a workitem or
planning item and there's an error in the ccm.log or qm.log and the RTC
or QM doesn't return the expected workitem or other artifact. You run a
full text search for a workitem or planning item and RTC (CCM) gives and
error and doesn't return what is expected. Recall that full text is an
option in available in RTC. To use it you create a query in a project,
and select the Full Text condition. There should be ane error in the
ccm.log with a message like CRJAZ8201E, or something similar. The qm and
ccm application use full text search. Use repotools-ccm.bat or
repotools-qm-bat depending on what is corrupt.

Use repotools -reindex search when you have the following symptoms

-   You run a quick search (the edit box in the lower left hand side of
    the eclipse RTC client, or upper right side of the web client) for a
    requirement, and you don't get the result you expected.

Use repotools -reindex query when you have the following symptoms

-   When you run a query against dashboards or DNG, and you don't get
    what you expected and there is an error in the jts.log or rm.log
    indicating the index is corrupt. If you see problems reported on the
    diagnostics page referring to the JFS index and JFS storage, look at
    the jts.log for signs that the index is corrupt.

Use repotools-jts.bat for dashboard issues. Use repotools-rm.bat for DNG
issues. Use repotools-ccm.bat for Enterprise Edition issues.

Use repotools -rebuildIndices when you see an error in the Database
Indices section of the diagnostics.

Use repotools -synchronizeJFSIndexes if the index is found to be corrupt
via repotools verifyJFSIndexes.

-   Use this procedure. Restore the most recent indices that pass
    repotools verifyJFSIndexes. Then run repotools
    -synchronizeJFSIndexes to catch the indices up with the underlying
    database.

Each time you store data in RM, it's stored twice, once in the database
where it is fetched and displayed in the GUI, and once in the filesystem
indices, where queries can be run against it. These two copies of the
data must be in sync.

What about the functionality of -compacttdb --Compact the RDF indexes?
If the reindex is reducing the size of the indices to half and so does
-compacttd, what is it that this command does? Is there any specific
switch with -verifyJFSIndexes that could prompt the admins to opt for a
compacttdb?

Answer: The -verifyJFSIndexes command reads the indices into Jena Triple
store data structures. From there the data structures are checked to see
if they are internally consistent. That ensures the index.properties
file in the index matches the actual index files, and that the data
structures contain non-empty data, etc. The extended command looks more
extensively for issues.

If you find an issue with verifyJFSIndexes, you should reindex
(repotools -reindex all) . The tool makes this suggestion.

The -compactdb option changes the representation of the indices on disk,
but doesn't affect their underlying value. Data is sometimes stored in
journals, lists of commands to apply to the index data, as opposed to
the actual data that makes up the index. If the journal contains a list
of commands that was committed, it can be played back up to the commit
point. This reduces the total index size.

##### Related topics: [Administering home](DeploymentAdministering),[Part 1: Query, search and Indexing technologies in CLM](DeploymentJazzIndicesTechnology),[Indices storage and management: Backup, recovery and recreation](DeploymentJazzIndicesStorage) [related-topics-administering-homepart-1-query-search-and-indexing-technologies-in-clmindices-storage-and-management-backup-recovery-and-recreation]

##### External links: [external-links]

-   [Repository tools command-line
    reference](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6/com.ibm.jazz.install.doc/topics/c_repotools_overview.html)

##### Additional contributors: [additional-contributors]
