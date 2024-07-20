META:TOPICINFO{author="rnaranjo" date="1692215457" format="1.1"
reprev="1.1" version="1.1"}
META:TOPICPARENT{name="ReportingTroubleshooting"}

# Link Validity datasource troubleshooting DKGRAY Authors: Main.RosaNaranjo, Main.ErnestMah Build basis: Lifecycle Query Engine, Jazz Team Server 7.0.2 [link-validity-datasource-troubleshooting-dkgray-authors-main.rosanaranjo-main.ernestmah-build-basis-lifecycle-query-engine-jazz-team-server-7.0.2]

ENDCOLOR

TOC{title="Page contents"}

Link Validity TRS feed can fail to provide a full response to LQE when a
high rate of changes are made to the system. This will result in the LQE
no longer being able read the TRS on reindexing or validation, as well
as potentially stopping regular change log indexing. Link validity
information will not be added or updated in LQE reports from that point
onwards. Within the tools Link Validity is checked for from foundation
directly and is unaffected by the Link Validity TRS issue. Any displayed
links within any application will show correct Link Validity information

## Scenarios affected

1.  Reindexing and full validation of the LQE datasource while high data
    creation is ongoing
    1.  Link Validity fails to return the initial base set of artifacts
        (returns it in pages) b. This base set is read during reindexing
        and full validation 2. Change log processing/indexing with high
        data creation ongoing (note it takes a higher rate to affect
        this than in number 1 above)

### What can help?

Make note of the JTS advanced property, TRS Item Query Result Set. This
property was introduced in 702 iFix024. Prior to 702 IFix024, it was an
internal default of 500.

Increasing this limit increases the volume of changes that can be
handled before failures can occur in retrieving the Link Validity TRS
base from JTS for reindexing or for validation. With an initial default
of 40,000 for this property setting, 40k changes would be allowed after
a reindex or validation is started. Increasing this limit increases the
volume of changes that can be handled in a change log processing
interval (1minute polling). This is a more profound effect on the Change
log processing capacity. With this setting, 40,000 changes would be
allowed in each LQE/LDX change processing interval (and the time it
takes to fully index those changes) Poll interval defaults to 1min, but
indexing all those changes might take 5 minutes

### For what scenarios is this setting relevant?

If you are importing a large set of data or making a large volume of
changes in DOORS Next, the following approaches are suggested from most
recommended to least recommended

1\. Handle ongoing changes as they are imported a. Attempt to complete
the reindex of the Link validity datasource past the initial base set of
artifacts. b. Pause imports into DOORS Next during this time. c. Once
successful, resume imports using a fixed unit of imports, and ensure the
Link Validity TRS changes can be returned during the import. d. If not
successful, increase the TRS Item Query Result Liimt 2. Handle ongoing
changes periodically a. Pause the Link Validity TRS indexing in LQE
during import after a successful reindex. b. Stop all imports and resume
indexing. **Do not pause for longer than the retention period for change
events of the Link Validity TRS or it will not be able to resume**

### Monitoring

MBean reference for LQE:
[https://jazz.net/library/article/90785](Monitoring the performance of Lifecycle Query Engine using MBeans)
Dataset suspension properties - suspensionCompletions, suspensionErrors,
suspensionPending, suspensionTimeouts Other useful properties are
available here

##### Related topics: [Deployment troubleshooting](DeploymentTroubleshooting) [related-topics-deployment-troubleshooting]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
