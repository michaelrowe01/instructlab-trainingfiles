META:TOPICINFO{author="ianbarnard" date="1709833210" format="1.1"
version="1.39"}
META:TOPICPARENT{name="TroubleshootingDOORSNextUpgrades"}

# DOORS Next 7.x upgrade Warning and Error codes [doors-next-7.x-upgrade-warning-and-error-codes]

DKGRAY Authors: Main.PaulEllis, Main.MarkGoossen, Main.IanBarnard Build
basis: DOORS Next 7.x ENDCOLOR

TOC{title="Page contents"}

This page is to explain the warning and error codes returned during the
upgrade from DOORS Next Generation 6.x to DOORS Next 7.x.

This page will evolve constantly as new error and warning messages are
encountered.

NOTE if you get *any* error codes shown in the summary at/near the end
of migrationOutput.log then you *must* also check for database errors
(in e.g. repotools_rm.log or, for 7.0.2, repotools_rm_error.log) and if
any are found then you must resolve these first before (most likely)
repeating the upgrade. See here for some assistance with DB2/Oracle
errors during upgrade.

## Error codes

### CRRRS2094E Failure transforming state

This exception has multiple root causes, including:

-   [0.6 migration: Migration06Exception:
    com.ibm.team.repository.common.validation.PropertyConstraintException
    (136361)](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/136361)
-   [0.6 migration: NPE processing wrapper resource - the Function
    passed to Optional.transform() must not return null.
    (136189)](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/136189)

These are both fixed in 7.0.2 GA, 7.0.1 ifix 1 and 7.0 ifix 4

-   [0.6 migration: WrapperResource with incorrect WrappedResourceURIs
    causes error in
    upgrade](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=143092)

This defect is only fixed in 7.0.2 ifix 12 and beyond.

java.lang.IllegalArgumentException: Multiple entries with same key:

-   CRRRS2094E can also indicate a problem with duplicate root folders
    which is fixed in **V7.0.2 ifix021** with [Task 145295: port
    duplicate root folder repair to v7 and integrate into
    upgrade](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=145295)

For Customers running upgrades prior to **V7.0.2 ifix021** check the
**migrationOutput.log** for folders referenced under the **CRRRS2094E**
error:

Component: Test_IBM_Component (1 issues)
xxxxx/rm/cm/component/\_BgqbUBU9Eeu4EvfsInWItA CRRRS2094E Failure
transforming state Explanation: Artifact state could not be transformed
to new data form, the state will not be migrated. Issues detected
within: xxxxxx/rm/folders/\_Bh4uIRU9Etu5EvfxInWItA (Severity: Error)

If folders are referenced then search for **"already has root folder"**
in the **repotools_rm.log** which can indicate the Customer is hitting
the issue with duplicate root folders:

2023-02-14T11:05:47,600 Upgrade initial txn:19437, attempt 1\[ADMIN\]\[
primary-consumer-11 txn:19437\] ERROR
otools.internal.migration.m06.TransformableConcept - Failure
transforming state:StateInfo
\[storageUri=storage/com.ibm.rdm.folders/\_Bh4uIRU9Etu5EvfxInWItA,
itemId=\_Bh4uIRU9Etu5EvfxInWItA, stateId=\_Ah2uJBU9Eeu5EvfxInWItA,
isArchived=false, versionInfo=Optional\[VersionInfo
\[concept=<https://xxxxxxxxxxx/rm/folders/_Bh4uIRU9Etu5EvfxInWItA>,
version=<https://xxxxxxxxxxx/rm/folders/_Bh4uIRU9Etu5EvfxInWItA>,
configInfos=\[ConfigInfo \[configurationId=\_AhaCNhU9Eeu5EvfxInWItA,
changeSetId=\_AiUBIBU9Eeu5EvfxInWItA, mapType=current,
mappingTime=2020-10-23 14:35:33.81,
creator=\_KPQPgD9_Eeixc-DUbEGFvA\]\]\]\], revisionModifiedTs=2020-10-23
14:35:33.762, status=Migration06Status \[state=IN_PROGRESS\]\]
java.lang.IllegalStateException: Component '\_AgqbUBU9Eeu5EvfxInWItA'
already has root folder '\_LbzRaH6Ffu7EvfxInJq4C', it cannot be changed
to '\_Bh4uIRU9Etu5EvfxInWItA'. at
com.ibm.rdm.repotools.internal.migration.m06.handlers.types.FolderUuidHelper.recordRootFolderId(FolderUuidHelper.java:82)
\~\[bundleFile:?\]

To fix this for upgrades prior to **V7.0.2 ifix021** the duplicate root
folders need to be repaired in **V6.X** before upgrading see: [Important
new IBM Engineering Requirements Management DOORS Next V6.0.x verifier
for customers who have yet to complete their upgrade to
V7.0.2](https://www.ibm.com/support/pages/node/6845466)

### CRRRS2103E/CRRRS2103W Ill-formed URI cannot be set on link

This error indicates that a URL encoding is invalid and the link cannot
be recreated. This is typically experienced when file system paths are
used, or where characters that require URL encoding exist. See [How to
identify ill-formed URIs in your data that cause links to break and
upgrades to 7.x to fail](https://www.ibm.com/support/pages/node/6453317)
on how to proceed.

### CRRRS2103E/CRRRS2094E referring to the same link

If you see the combination of CRRRS2094E Failure transforming state with
CRRRS2103E Ill-formed URI cannot be set on link then you should focus on
the first error. The link is not complete in the DOORS Next 6.x
repository, hence why the 2nd code check states that the URI is bad.
Identify the link(s) failing, for example
<https://someserver.com/rm/links/_12Z-INn8EeD1XfSZ7SJ2UA> (Severity:
Error)

In your (restored) DOORS Next 6.x repository, see if the link returns an
error when you paste that into the browser. Contact IBM Support if an
error is returned. Possible errors are: "CRRRS4142E
getInternalRequestHandlerService(context) returned null" or HTTP 403

### CRRRS2114E Unable to migrate type model

Explanation: The type could not be transformed to new data form, the
type will not be migrated.

So far we have only encountered one occurrence of this issue and it was
found in an old archived project. If you encounter this error, check the
associated project area to confirm if its archived or still in use. If
its archived and no longer required confirm if it can be deleted before
the upgrade. See
[deleteJFSresources](https://www.ibm.com/docs/en/elm/6.0.6.1?topic=reference-deletejfsresources)
command for deleting unwanted, archived projects.

### CRRRS2130E/CRJAZ0447E Consumer processing encountered error

The error in the MigrationOutput.log is the generic **Consumer
processing encountered error** error. The more pertinent error though is
detailed by the **Caused by:**

Caused by: com.ibm.team.repository.common.InternalRepositoryException:
CRJAZ0447E The SQL statement did not run successfully.Integrity
constraint violation SQL: INSERT INTO
RM1USER.DNGMIGRATION_DB_CONCEPT_MAPPNG(STATE_ID, ITEM_ID, CONTEXT_ID,
MODIFIED, MODIFIED_BY_ITEM_ID, RESOURCE_COL, UPGRADED_ID,
UPGRADED_ITEM_ITEM_ID, JZ_UPGRADED_ITEM_DISCRIMINATOR) values (?, ?, ?,
?, ?, ?, ?, ?, ?) SQL Exception \#1 SQL Message: ORA-00001: unique
constraint (RM1USER.DNGMGRTNDNGMGRTNDBCNCPTMPPNGRS) violated

SQL State: 23000 Error Code: 1

SQL Exception \#2 SQL Message: ORA-00001: unique constraint
(RM1USER.DNGMGRTNDNGMGRTNDBCNCPTMPPNGRS) violated

SQL State: 23000 Error Code: 1

Exception Details: Integrity constraint violation

If you encounter a constraint violation then contact IBM Support.
[137387 - 0.6 migration: Integrity constraint violation on
concept_mapping_table](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=137387)
was fixed since 7.0.1 ifix 4, however, we have seen data-related issues
since that require data inspection and deletion.

## Warning Codes

### CRRRS2092W Unable to identify which folder this artifact belongs in

There are multiple causes for this warning. This is a warning that a
folder bookmark could not be found for a resource. If a folder cannot be
identified, the 7.x migration will place the artifact into the root
folder. The list of issues per components are detailed in the
MigrationOutput.log. For example:

Component: MySystemRequirements(Requirements) (1 issues)
<https://myuri.ibm.com/rm/cm/component/_EWJbEbPkbsAhRKeeoBN_Bg>
CRRRS2092W Unable to identify which folder this artifact belongs in
Explanation: Unable to identify which folder the artifact belongs in.
The artifact will not be available in any folder hierarchy.
Recommendation: Orphan artifacts can be reclaimed using the
FolderIntegrityCheck support tool to recover the orphaned artifacts into
a LOST AND FOUND folder. Issues detected within:
<https://myuri.ibm.com/rm/cm/component/_EWJbEbPkbsAhRKeeoBN_Bg>
(Severity: Possible Issue)

Update August 2022: This error has been removed from the next release of
DOORS Next under development (known as 7.0.3 at the time of writing). It
can therefore be ignored for any upgrade post 7.0.2 ifix 8a.

In earlier Ifix versions, this warning message was more concerning, as
it was also seen due to [Defect 142084: 0.6 migration: exceptions when
migrating requirements due to invalid parent
folder](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/142084).
We recommend that you apply the latest ifix (at least 7.0.2 SR1).

#### You do not have the required privileges for this operation. Missing privilege:create (com.ibm.rrs.team.saveFolder).

If when running the Folder Integrity Tool you encounter the message:

This message is telling us that we need to add Save Folder and Create
Artifacts in the project area to our user/role. a. Allocate permissions
to Save Folder and Create Artifacts to your role. b. If Change
Management constraints are set in the stream (see Project Area \>
Administration \> Manage Component and Configurations \> Component \>
Stream \> Details) create a change set in the stream c. Depending on
(b), execute the FolderIntegrityCheck tool either against the stream or
against ChangeSet choosing the "Reparent Orphaned Artifacts and Folders"
option.

If you experience the error **Project area cannot be saved - duplicate
permissions operation id specified** then see [Attempts to save a
project after a process change results in "Project area cannot be
saved - duplicate permissions operation id
specified"](https://www.ibm.com/support/pages/node/6595145).

### CRRRS2096W Skipping binding because invalid state

"The artifact associated with binding may not be visible in the
associated module because either the module was missing, the artifact
was missing, or the binding was invalid."

This message is listed in [DOORS Next some warnings during upgrade to
7.x must not be ignored and need to be
investigated](https://www.ibm.com/support/pages/node/6464861) due to
defect [0.6 migration: Bindings are not upgraded when the associated
core artifact is missing the artifact format property in the latest
version/revisions](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=142850).

The CRRRS2096W warning is logged for a number of different reasons, but
they all mean that the binding could not be created during upgrade. The
reasons include:

-   the binding is missing the module property
-   the bound artifact is missing, this may be because the bound
    artifact was malformed (we have fixed several cases of this issue.
    IBM Support will send you an L3 tool, the
    bindingAndArtifactAnalyzer, which provides more detail on this)
-   the binding points to a bound artifact URI which is not a bound
    artifact

The original data being unusable can occur during a failed import, for
example, via csv import or ReqIF. Prior to 7.0.2 ifix 8, defect [0.6
migration: Bindings are not upgraded when the associated core artifact
is missing the artifact format property in the latest
version/revisions](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=142850),
meant that upgrade could skip the last version of an artifact, resulting
in "missing" data in 7.x when compared with the original data in DOORS
Next 6.0.6.x.

If you upgraded prior to 7.0.2 ifix 8, follow the technote to identify
if migrationOutput.log reported any of these error types. If any were
reported, contact IBM Support, who will send you a tool to validate your
data.

### CRRRS2097W Skipping the artifact revision because it does not have a format (and is not a binding):

Skipping the artifact revision because it does not have a format (and is
not a binding) Explanation: Skipping the artifact revision for artifact
because it does not have a format (and is not a binding).

[DOORS Next some warnings during upgrade to 7.x must not be ignored and
need to be
investigated](https://www.ibm.com/support/pages/doors-next-some-warnings-during-upgrade-7x-must-not-be-ignored-and-need-be-investigated)

It is essential that you use the latest ifix when upgrading to DOORS
Next 7.x. The minimum release levels that includes defect [141071: 0.6
migration: requirements which are missing an artifact format are not
migrated
(CRRRS2097W)](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/141071)
are:

-   7.0 iFix012
-   7.0.1 iFix010
-   7.0.2 iFix005

If you encounter this error code in the MigrationOutput.log then please
contact IBM Support. IBM Support will send an additional validation tool
"BindingAndArtifactAnalyzer" to ensure that this data migrated
correctly - NOTE this will be run against 7.x rather than before the
upgrade, i.e. no need to revert.

The CRRRS2096W and CRRRS2097W errors are still valid even when the
latest Ifix is released, and will continue to be seen during upgrade.
These will occur when all of the states of an artifact are invalid.
[141071: 0.6 migration: requirements which are missing an artifact
format are not migrated
(CRRRS2097W)](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/141071)
addresses an issue where the initial states of an artifact are invalid,
and later states are valid.

For example, you could have requirement1 and requirement2:
requirement1.version1 -\> invalid requirement1.version2 -\> invalid
requirement1.version3 -\> **valid**

and

requirement2.version1 -\> invalid requirement2.version2 -\> invalid
requirement2.version3 -\> invalid

With the defect fix, we can now upgrade requirement1. With requirement2,
you would still see the upgrade warning.

### CRRRS2098W Artifact revision content reset because the XHTML/XML was invalid

The primary text or diagram XML is not valid according to the DNG XHTML
schema.

### CRRRS2100W Unable to make handle for fallback type.

The fallback type failed to create handle for without typed handle. The
migration for the artifact failed. Note this will cause the upgrade to
fail so cannot be ignored.

If you check the **repotools-rm_addTables.log** for a corresponding
**"One or more corrupt nodes in module structure"** error (See example
below) then you are hitting [APAR:PH29889 Migration06Exception: One or
more corrupt nodes in module
structure(137718)](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=137718)
Originally fixed in **V7.0.1 ifix004** but recently reopened and under
review. Raise a Case with IBM support referencing this entry in the
Wiki.

Problem details: problem:
com.ibm.rdm.repotools.internal.migration.m06.exceptions.Migration06Exception
Migration exception:
com.ibm.rdm.repotools.internal.migration.m06.exceptions.Migration06Exception:
One or more corrupt nodes in module structure at
com.ibm.rdm.repotools.internal.migration.m06.handlers.artifacts.ArtifactConceptMigrationHandler.loadStructureContent(ArtifactConceptMigrationHandler.java:958)
at
com.ibm.rdm.repotools.internal.migration.m06.handlers.artifacts.ArtifactConceptMigrationHandler.access\$5(ArtifactConceptMigrationHandler.java:927)
at
com.ibm.rdm.repotools.internal.migration.m06.handlers.artifacts.ArtifactConceptMigrationHandler\$4.load(ArtifactConceptMigrationHandler.java:361)
at
com.ibm.rdm.repotools.internal.migration.m06.handlers.artifacts.ArtifactConceptMigrationHandler\$4.load(ArtifactConceptMigrationHandler.java:1)
at
com.google.common.cache.LocalCache\$LoadingValueReference.loadFuture(LocalCache.java:3527)
at
com.google.common.cache.LocalCache\$Segment.loadSync(LocalCache.java:2319)
at
com.google.common.cache.LocalCache\$Segment.lockedGetOrLoad(LocalCache.java:2282)
at com.google.common.cache.LocalCache\$Segment.get(LocalCache.java:2197)
at com.google.common.cache.LocalCache.get(LocalCache.java:3937) at
com.google.common.cache.LocalCache.getOrLoad(LocalCache.java:3941) at
com.google.common.cache.LocalCache\$LocalLoadingCache.get(LocalCache.java:4824)
at
com.ibm.rdm.repotools.internal.migration.m06.handlers.artifacts.ArtifactConceptMigrationHandler.getStructureContent(ArtifactConceptMigrationHandler.java:909)
at
com.ibm.rdm.repotools.internal.migration.m06.handlers.artifacts.ArtifactConceptMigrationHandler.transformModuleWithRoot(ArtifactConceptMigrationHandler.java:1134)
at
com.ibm.rdm.repotools.internal.migration.m06.handlers.artifacts.ArtifactConceptMigrationHandler.transformModule(ArtifactConceptMigrationHandler.java:1032)
at
com.ibm.rdm.repotools.internal.migration.m06.handlers.artifacts.ArtifactConceptMigrationHandler.transformWithTransformRecorder(ArtifactConceptMigrationHandler.java:695)
at
com.ibm.rdm.repotools.internal.migration.m06.handlers.artifacts.ArtifactConceptMigrationHandler.transformWithTransformRecorder(ArtifactConceptMigrationHandler.java:1)
at
com.ibm.rdm.repotools.internal.migration.m06.TransformableConcept.importStates(TransformableConcept.java:407)
at
com.ibm.rdm.repotools.internal.migration.m06.TransformableConcept.transformSingleConcept(TransformableConcept.java:318)
at
com.ibm.rdm.repotools.internal.migration.m06.TransformableConcept.transformWithPerfRecorder(TransformableConcept.java:230)
at
com.ibm.rdm.repotools.internal.migration.m06.MigrationTransformer\$Consumer.consume(MigrationTransformer.java:193)
at
com.ibm.rdm.repotools.internal.migration.m06.TransactionAwareConsumer\$2.run(TransactionAwareConsumer.java:418)
at
com.ibm.rdm.repotools.internal.migration.m06.TransactionAwareConsumer\$2.run(TransactionAwareConsumer.java:1)
at
com.ibm.team.repository.service.internal.PrimitiveTransactionService\$4.run(PrimitiveTransactionService.java:214)
at
com.ibm.team.repository.service.internal.rdb.RepositoryDatabase\$Transaction.run(RepositoryDatabase.java:628)
at
com.ibm.team.repository.service.internal.rdb.RepositoryDatabase\$3.run(RepositoryDatabase.java:408)
at
com.ibm.team.repository.service.internal.rdb.ConnectionPoolService.withCurrentConnection(ConnectionPoolService.java:531)
at sun.reflect.GeneratedMethodAccessor21.invoke(Unknown Source) at
sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:55)
at java.lang.reflect.Method.invoke(Method.java:508) at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord.invoke(ExportProxyServiceRecord.java:361)
at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord.access\$0(ExportProxyServiceRecord.java:347)
at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord\$ExportedServiceInvocationHandler.invoke(ExportProxyServiceRecord.java:56)
at com.sun.proxy.\$Proxy185.withCurrentConnection(Unknown Source) at
com.ibm.team.repository.service.internal.rdb.RepositoryDatabase.runTransaction(RepositoryDatabase.java:405)
at
com.ibm.team.repository.service.internal.rdb.RepositoryDatabase.runInTransaction(RepositoryDatabase.java:342)
at
com.ibm.team.repository.service.internal.rdb.RepositoryDatabase.runInNewTransaction(RepositoryDatabase.java:332)
at
com.ibm.team.repository.service.internal.PrimitiveTransactionService\$2.run(PrimitiveTransactionService.java:170)
at
com.ibm.team.repository.service.internal.rdb.ConnectionPoolService.withCurrentConnection(ConnectionPoolService.java:531)
at
com.ibm.team.repository.service.internal.rdb.ConnectionPoolService.withNewConnection(ConnectionPoolService.java:585)
at sun.reflect.GeneratedMethodAccessor203.invoke(Unknown Source) at
sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:55)
at java.lang.reflect.Method.invoke(Method.java:508) at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord.invoke(ExportProxyServiceRecord.java:361)
at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord.access\$0(ExportProxyServiceRecord.java:347)
at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord\$ExportedServiceInvocationHandler.invoke(ExportProxyServiceRecord.java:56)
at com.sun.proxy.\$Proxy185.withNewConnection(Unknown Source) at
com.ibm.team.repository.service.internal.PrimitiveTransactionService.runInNewTransaction(PrimitiveTransactionService.java:168)
at sun.reflect.GeneratedMethodAccessor202.invoke(Unknown Source) at
sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:55)
at java.lang.reflect.Method.invoke(Method.java:508) at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord.invoke(ExportProxyServiceRecord.java:361)
at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord.access\$0(ExportProxyServiceRecord.java:347)
at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord\$ExportedServiceInvocationHandler.invoke(ExportProxyServiceRecord.java:56)
at com.sun.proxy.\$Proxy233.runInNewTransaction(Unknown Source) at
com.ibm.team.repository.service.internal.TransactionService.runInNewTransaction(TransactionService.java:54)
at sun.reflect.GeneratedMethodAccessor201.invoke(Unknown Source) at
sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:55)
at java.lang.reflect.Method.invoke(Method.java:508) at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord.invoke(ExportProxyServiceRecord.java:361)
at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord.access\$0(ExportProxyServiceRecord.java:347)
at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord\$ExportedServiceInvocationHandler.invoke(ExportProxyServiceRecord.java:56)
at com.sun.proxy.\$Proxy382.runInNewTransaction(Unknown Source) at
com.ibm.team.repository.service.internal.vvc.ConfigurationManagementImportService.runInNewTransactionWithRetries(ConfigurationManagementImportService.java:461)
at
com.ibm.team.repository.service.internal.vvc.ConfigurationManagementImportService.runAsConsolidatedImportTransaction(ConfigurationManagementImportService.java:306)
at sun.reflect.GeneratedMethodAccessor209.invoke(Unknown Source) at
sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:55)
at java.lang.reflect.Method.invoke(Method.java:508) at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord.invoke(ExportProxyServiceRecord.java:361)
at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord.access\$0(ExportProxyServiceRecord.java:347)
at
org.eclipse.soda.sat.core.internal.record.ExportProxyServiceRecord\$ExportedServiceInvocationHandler.invoke(ExportProxyServiceRecord.java:56)
at com.sun.proxy.\$Proxy878.runAsConsolidatedImportTransaction(Unknown
Source) at
com.ibm.rdm.repotools.internal.migration.m06.Migration06DAO.runAsConsolidatedImportTransaction(Migration06DAO.java:923)
at
com.ibm.rdm.repotools.internal.migration.m06.TransactionAwareConsumer.consumeInTransaction(TransactionAwareConsumer.java:428)
at
com.ibm.rdm.repotools.internal.migration.m06.TransactionAwareConsumer.consumeInRetryableTransaction(TransactionAwareConsumer.java:296)
at
com.ibm.rdm.repotools.internal.migration.m06.TransactionAwareConsumer.access\$5(TransactionAwareConsumer.java:288)
at
com.ibm.rdm.repotools.internal.migration.m06.TransactionAwareConsumer\$1.run(TransactionAwareConsumer.java:261)
at
com.ibm.team.repository.service.internal.TeamServiceContext.runAsAdmin(TeamServiceContext.java:278)
at
com.ibm.rdm.service.provider.internal.JazzContext.runAsAdmin(JazzContext.java:76)
at
com.ibm.rdm.repotools.internal.migration.m06.TransactionAwareConsumer.call(TransactionAwareConsumer.java:213)
at
com.ibm.rdm.repotools.internal.migration.m06.MigrationTransformer.call(MigrationTransformer.java:337)
at
com.ibm.rdm.repotools.internal.migration.m06.MigrationTransformer.call(MigrationTransformer.java:1)
at java.util.concurrent.FutureTask.run(FutureTask.java:277) at
java.util.concurrent.Executors\$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277) at
java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1160)
at
java.util.concurrent.ThreadPoolExecutor\$Worker.run(ThreadPoolExecutor.java:635)
at java.lang.Thread.run(Thread.java:825)

### CRRRS2101W None of the states for a version of concept were upgraded. Skipping remaining versions of the concept.

This is stating that the artifact and all its versions in DOORS Next
Generation 6.x were incomplete and unusable. This is likely due to a
failed import and the data's state would have been known (as unusable)
at the time, but not deleted.

### CRRRS2102W Last revision for a version of concept were not upgraded. Skipping remaining versions of the concept

An error occurred while upgrading a revision of an artifact version.
Subsequent revisions will be skipped. The warning means that at least 1
state is not being upgraded from each of different modules. Possible
reasons for the warning are that the module state cannot be read, or is
is missing required information. Use the Module Analyzer Tool in the
post-migration database to ensure the modules are as expected.

### CRRRS2104W Unable to determine link handle for subject URI

This is no longer in use in 7.0.3. Links were not migrated. These are
often double reported with the CRRRS2102W and CRRRS2104W codes. These
are often links to an internal endpoint, that is not a valid link
target. It could be invalid because it points to a resource which does
not support linking, or it points to an artifact which does not exist.

### CRRRS2110W Ignore state due to missing model.

The artifact or link model content either does not exist or cannot be
parsed. Subsequent states **will** be migrated.

### CRRRS2112W An attribute definition could not be found. Artifact types and values will be affected.

The attribute definition that is referenced by an artifact type does not
exist. The artifact type might have been archived. The artifact type
will be migrated without the attribute definition. If this message is
unexpected, check the Component Properties to ensure that the artifact
type does not exist.

This should be considered as just a warning and are not considered
critical to the success of the upgrade.

### CRRR2103W Ill-formed URI cannot be set on link

The data within the DOORS Next repository contains non-standard URIs, as
defined by the Uniform Resource Identifiers(URI): Generic Syntax, for
example: prefixes, or spaces within the URI. See [How to identify
ill-formed URIs in your data that cause links to break and upgrades to
7.x to
fail](https://supportcontent.ibm.com/support/pages/how-identify-ill-formed-uris-your-data-cause-links-break-and-upgrades-7x-fail)
on how to proceed.

### CRRRS2116W Artifact revisions in JFS have inconsistent Wrapper/Text format.

Migrated data will be regularized to format Wrapper. An artifact has a
text format, but its predecessor had a wrapper format. The artifact
state will be migrated as a wrapper resource.

### CRRRS2118W Link Title was truncated

The existing link title was too long and so the title was truncated.

### CRRRS2119W Link URI was truncated

Explanation: The existing link URI was too long and so the URI was
truncated.

See [How to identify ill-formed URIs in your data that cause links to
break and upgrades to 7.x to
fail](https://supportcontent.ibm.com/support/pages/how-identify-ill-formed-uris-your-data-cause-links-break-and-upgrades-7x-fail)
on how to proceed.

### Skipping current LV; Bad URI not handled yet

This error reported in the repotool-rm.log indicates that we skip the
ignored validity entries to avoid NPEs when saving to the database. Not
all concepts get migrated and there may be validity records/assertions
about them still.

There are valid reasons for the validity records to be skipped. This
message can be ignored.

ERROR 06.handlers.linkvalidity.LinkValidityMigrationCore - Skipping
current LV; Bad URI not handled yet; Info: \[provenanceItemId: \[UUID
\_01_jMBqXEeeo3GJSBFjrO3A\]; provenanceStateId: \[UUID
\_01_jMBqXEeeo3GJSBFjrO3A\]; legacyVersionedResourceURL:
<https://myuri.com/rm/versionedResources/_f59252c8d0a876534a4ee6af96c86a572>;
legacyHashcode: e0efb82666b5f44c3f25cabd32faad67; legacyModified:
2017-04-06 09:08:24.675; uri type: BINDING_VERSION_BAD\];Type:
BINDING_VERSION_BAD

### CRJAZ0255W The deadlock event details could not be fetched for this deadlock

The following CRJAZ0255W is due to an APAR, PH44971 [(defect 143638 -
0.6 migration: retriable exception not being
retried.](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=143638)

See this error for more details. If you encounter this then please
contact IBM Support.

Serialization failure

CRJAZ0255W The deadlock event details could not be fetched for this
deadlock: CRJAZ0254W The deadlock event associated with the rolled back
application id (53.31.51.141.60004.220127103115) could not be fetched
from the database.

SQL: SELECT REPO.KEY_UUID

from REPOSITORY.ITEM_STATES REPO

WHERE REPO.ITEM_UUID = ?

ORDER BY REPO.MODIFIED ASC

SQL Exception \#1

SQL Message: DB2 SQL Error: SQLCODE=-911, SQLSTATE=40001, SQLERRMC=68,
DRIVER=4.26.14

### ERROR gration.m06.handlers.ContributorFinderForMigration

ERROR gration.m06.handlers.ContributorFinderForMigration - Contributor
"../../jts/users/bob" cannot be found

Does not impact upgrade. Found in repotools_rm_error.log

[144049: Contributor cannot be found type logs should be set to WARN
level](https://jazz.net/jazz03/resource/itemName/com.ibm.team.workitem.WorkItem/144049)

### A type resource was fetched from storage but no type was found in that resource

2019-07-11 18:33:32,559 A type resource was fetched from storage but no
type was found in that resource.

Types StorageArea <https://jazz.net/rm/types> all single

Does not impact upgrade: It is a bad URI that at one point made it into
a project mapping file. It will be filtered out by the migration logic.
The message found in **repotools-rm_addTables.log** and
**repotools-rm.log** is appropriate.

[131015: 0.6: migration: selfhost: A type resource was fetched from
storage but no type was found in that resource.
](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=131015)

### Null changeset id in ConfigInfo

This message can appear in rm-upgrade.log.

Does not impact upgrade; this is logged as an error when a state of a
resource has a null changeset. The state is skipped, and the upgrade
will continue processing other states of the resource. This does not
cause the upgrade to fail. These error log statements should be ignored.
Anything which is fatal to the upgrade will be shown in the summary and
in the final status of the upgrade.

##### Related topics: [Understanding DOORS Next sizings in ELM 6.x to estimate timings when upgrading to DOORS Next 7.x](UnderstandingDOORSNextSizingsin6X), [ Troubleshooting DOORS Next 6.x to 7.x Upgrades](TroubleshootingDOORSNextUpgrades) [related-topics-understanding-doors-next-sizings-in-elm-6.x-to-estimate-timings-when-upgrading-to-doors-next-7.x-troubleshooting-doors-next-6.x-to-7.x-upgrades]

##### External links: [external-links]

-   [IBM Engineering Lifecycle
    Management](https://www.ibm.com/products/engineering-lifecycle-management),
    [jazz.net](https://jazz.net/products/)

##### Additional contributors: Main.WillChatham, Main.Sudarshan,Main.RosaNaranjo [additional-contributors-main.willchatham-main.sudarshanmain.rosanaranjo]
