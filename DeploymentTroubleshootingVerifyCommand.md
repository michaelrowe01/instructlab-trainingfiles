META:TOPICINFO{author="paulellis" date="1685358067" format="1.1"
version="1.24"} META:TOPICPARENT{name="DeploymentTroubleshooting"}

# Repotools Verify command - additional guidance DKGRAY Authors: Main.PaulEllis, Main.ZeeshanChoudhry, Main.GlennBardwell, Main.PrabhatGupta, Build basis: None. [repotools-verify-command---additional-guidance-dkgray-authors-main.paulellis-main.zeeshanchoudhry-main.glennbardwell-main.prabhatgupta-build-basis-none.]

ENDCOLOR

TOC{title="Page contents"}

This document expands upon [repository tools command to verify the
integrity of a
database](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fr_repotools_verify.html)
to provide common errors and their resolution, as well as further
explanation of how and when to use the verify command.

The command "repotools -verify" can be used to verify your database as
part of a weekly/monthly maintenance schedule, or prior to an upgrade or
other major deployment activities. This command allows logical
verification of objects, in addition to some mid-level concepts, such as
context checking. We also recommend to include this as a post-upgrade
task using level 4 (see below for more details on levels).

./repotools-rm.sh -verify level=4

Use the repotools verify command to verify the integrity of a database.
There are different levels for use with this command, using what level;
and document the error messages so you can contextualize the seriousness
of the warning/errors.

Purpose The verify command is used for contents verification in the
database with verification levels set between number one and ten.

### Online Verify

The repotools onlineverify command verifies the integrity of repository
database tables. Specifically, it verifies that the ITEM_TYPES,
ITEM_CURRENTS, CONTENT_STORAGE, and ITEM_STATES tables have consistent
values. From a user perspective, these are the low-level tables that
store much of the data in CLM. Some data is duplicated in these tables.
This analysis looks for inconsistency in the duplicated elements.

You can use onlineverify directly from your browser via
<https://://onlineVerify> (eg.
<https://mymachine:9443/ccm/onlineVerify>. You need to enable repodebug
in the the application Advanced Settings.

The repotools -verify command verifies the integrity of resources at the
application level. This command analyzes the self-consistency of the
tables that make each of the application components. Each component
contributes its own verification.

The verify command looks for higher-level logical inconsistencies in the
application data.

If you install onlineverify from
<https://jazz.net/wiki/bin/view/Main/L3DevTool> and run -verify, the
-verify command will also run onlineverify.

### What level should I use?

Each component uses these levels with different verbose checks so it is
hard to be definitive which level would do what for Builds or SCM
component for example. **Level 5** should be the base to start with if
verification is needed.

**Level one** is the minimum verification level. Level one for example,
verifies if the item can be fetched by simple fetch call at a very top
level. If some components show major problems, then you can start with a
higher level to get more verbose output. This is the default and is good
for your maintenance tasks (monthly check) or prior to upgrade to ensure
there are no problems. If after the execution, the log reports any
issues then you will need to increase verbosity to at least 5 to
understand them.

**Level ten** is the maximum verification level. When the level is set
to ten, it looks for the particular content of the component in all
database tables and verifies their validity. Only run level 10, if
instructed to do so by IBM Support. This level produces a large verbose
output and takes some time to complete.

It is expected that you run this command as a scheduled task on at least
a monthly basis. It is especially recommended that you run this command
prior to an upgrade to ensure that any output is verified by IBM
Support. Therefore, it is also recommended to perform the command with
plenty of time to allow analysis and resolution of any more serious
errors (so not 4 hours prior to upgrade).

### Changes with Log4j2 and Verify

DOORS Next introduced log4j2 in ELM 7.0. All subsequent applications
introduced log4j2 as part of the 7.0.2 SR1 (ifix 15) release. This
changes how verify logs output. The base output now is to summarize the
main sections of verify and report a summary of any problems.

If you need to understand the error further then contact IBM Support.

DOORS Next, made the change whereby you need to update: the
C:\IBM\JazzTeamServer_7.0.2SR1\server\conf\repotools_log4j2.xml file
with the following

For online verify, use these options to control the log output level of
internal verifiers and online verify debug.

Once set, you may re-run verify and then send in the repotools-.log to
IBM Support.

### Types of errors

This page summarizes those errors that could be returned from the tool.
Those errors that are non-serious and do not currently have a technote
elsewhere are explicitly listed. There are some errors which were
documented prior to this page, which will reference the published
technote.

**Note:** In versions of Rational Team Concert earlier than 3.0.0, it
was possible for a change set to be displayed multiple times in the
history of a workspace or a stream. When you run the verify command on
databases that contain data that was created with versions of Rational
Team Concert earlier than 3.0.0, messages similar to this one might be
displayed:
`History contains multiple references to change set _ifGCAfwOEdyMyflwGKMWgg.`
This error can be ignored.

If you are scripting these checks, then you can parse CRJAZ2222I
Verification was successful to see if there is anything to investigate.
If the verification is not successful then proceed to the errors below.
If it is successful, then there is no more to do.

#### 1) CRRTC3004E errors

Known examples of this error are:

-   CRRTC3004E: Build component item of type BuildResult with item ID
    .......
-   CRRTC3004E: Build component item of type BuildEngine with item ID
    .....
-   CRRTC3004E: Build component item of type BuildRequest with item
    ID....

Answer: These 3 errors are largely harmless and do not impact the
upgrade. The missing BuildEngineActivity item should not cause any
problems. When the last contact time for the engine is updated, this
item will get recreated if needed. If, however, you do see related
errors in the server log, the workaround would be to delete and recreate
the build engine.

#### 2) ...was found in the ITEM_CURRENTS table, but was not found in the Item query table

An example of this error would be:

The Item with ItemID "\_abCDEfg7HijKlMnWto3lwg" and StateId
"\_xyz-E8j7EeaQuJlWto3lwg" was found in the ITEM_CURRENTS table, but was
not found in the Item query table. Answer: This error can be ignored.
Having this in the Items Current and not in the Query table is not going
to cause any issue.

#### 3) The Item with item Id "UUID \_abCdeFG_EeCCUKUG0TjNNg", state Id "UUID \_abcde_bEeCCUKUG0TjNNg", and type "com.ibm.team.jfs.resource.Resource" references content "\_d1gogR_bEeCCUKUG0TjNNg" but that content does not exist.

An example of this error would be:

The ITEM_STATE row with itemId = \[UUID \_abCdeFG_EeCCUKUG0TjNNg\],
keyId = \[UUID \_abcde_bEeCCUKUG0TjNNg\], and itemType =
com.ibm.team.repository#RepositoryRoot contained an item that references
the predecessor state \[UUID \_d1gogR_bEeCCUKUG0TjNNg\], but that state
could not be found in the DB. There are no states older than this state,
so the history seems to have been truncated.

Answer: This error can be ignored. They have no impact for an upgrade.

#### 4) ...was found in the ITEM_CURRENTS table, but the same Item had a different StateId,...

An example of this error would be:

The Item with ItemID "\_3Ac5BCdeFgHIjkLm7nO6pQ" and StateId
"\_-vUbAMclEdeQfJlWgh3ijk" was found in the ITEM_CURRENTS table, but the
same Item had a different StateId, "\_Y64-zMyxEwvQuJlWts3rqp", in the
Item query table Answer: These sort of errors would need [Online
Verify](https://jazz.net/wiki/bin/view/Main/L3DevTool) to check what
ItemType this is. In the online verify those items are pointing to Build
Results, Build Engines or Build requests. Build engine activity and are
harmless for upgrade problems. However, these can be cleaned up if
needed. Send the output from [repotools
-verify](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fr_repotools_verify.html);
and [Online -verify](https://jazz.net/wiki/bin/view/Main/L3DevTool), to
IBM Support via Service Request (SR) if you wish to proceed with
removing the cause of these errors.

#### 5) CRJAZ1150E The repository was not verified errors

Known examples of this error are:

-   CRJAZ1150E The repository was not verified: Some problems were found
    while checking the consistency of the Item tables.
-   CRJAZ1150E The repository was not verified: Some problems were found
    in the tables related to the
    "com.ibm.team.enterprise.scd#ScanResult" Item type.
-   CRJAZ1150E The repository was not verified: There were some problems
    found in the Item query table for Item type
    "com.ibm.team.enterprise.scd#ScanResult".
-   CRJAZ1150E The repository was not verified: There were some problems
    found in the Item query table for Item type
    "com.ibm.team.enterprise.scd#ScanResult".
-   CRJAZ1150E The repository was not verified: Some problems were found
    in the tables related to the
    "com.ibm.team.enterprise.scd#ScanRequest" Item type.
-   CRJAZ1150E The repository was not verified: There were some problems
    found in the Item query table for Item type
    "com.ibm.team.enterprise.scd#ScanRequest".
-   CRJAZ1150E The repository was not verified: Some problems were found
    in the tables related to the "com.ibm.team.links#AuditableLink" Item
    type.

Answer: [Online verify](https://jazz.net/wiki/bin/view/Main/L3DevTool)
would problem better to check if its consistency problem or some thing
structural is not good enough. We would need to bring in the Enterprise
Extensions team to help resolve issues with these tables, so please
create a Problem Maintenance Record (PMR) via Service Request (SR) if
you encounter similar issues.

#### 6) CRJAZ1150E The repository was not verified...CRRTC5132E errors

Known examples of this error are:

Verifying items present in the "com.ibm.team.scm" component. CRJAZ1150E
The repository was not verified: SCM Verification failures CRJAZ1150E
The repository was not verified: CRRTC5132E The \_ktNhguc_EeSUf5igoHwgaQ
component entry has an invalid historic entry index. CRJAZ1150E The
repository was not verified: CRRTC5132E The \_4HP4lMmtEeWqiLLRAUIq4g
component entry has an invalid historic entry index.

Answer: The mentioned error indicating historical index missing for some
SCM item can be safely ignored. We have encountered these after
migrations, caused by history state references not handled in a clean
way, but they tend not to cause any issues. Run [Online
verify](https://jazz.net/wiki/bin/view/Main/L3DevTool) to check for DB
consistency issues.

#### 7) CRJAZ1150E The repository was not verified:...CRRTC5141E

A known example of this error are:

CRJAZ1150E The repository was not verified: CRRTC5141E The following
item does not have a persisted query record:
FileItem\[\_3zRTkKUuEd2m-sD01I2KJg\] Answer: The mentioned error can be
safely ignored.

#### 8) CRJAZ1150E The repository was not verified: CRRTC5113E

A known example of this error are: CRJAZ1150E The repository was not
verified: CRRTC5113E There is a claim for the
C4Ejryb1vBt7oAf6_vuwYS4pARgGikuIKn79RDVmyDY content hash, which does not
exist in the repository. Answer: The mentioned error can be safely
ignored.

#### 9) CRJAZ1150E The repository was not verified: CRJAZ0215E

CRJAZ1150E The repository was not verified: CRJAZ0215E The following
record was not found in the database:
com.ibm.team.apt.internal.common.nucleus.impl.IterationPlanRecordHandleImpl@32e06670
(stateId: \[UUID \_HaKTwckcEeaQuJlWto3lwg\], itemId: \[UUID
\_lzAVwPv_EeOPPKTEK6lM1Q\], origin: , immutable: ) Answer: These sort of
errors would need [Online
Verify](https://jazz.net/wiki/bin/view/Main/L3DevTool) to check what the
underlying problem is. Send the output from repotools -verify; and
Online -verify, to IBM Support via Service Request (SR) if you wish to
proceed with removing the cause of these errors.

If you are seeing this error message in the Rational Team Concert web
client, when viewing a work item's results, see: [Displaying a work item
results in "CRJAZ0215E the following record cannot be found" error in
RTC Web
client](http://www-01.ibm.com/support/docview.wss?uid=swg21671560).

#### 10)CRJAZ2221E The repotools command could not be verified or run

Answer: This comment can be found at the end of the verify log. It
signifies that there were some errors during verification and at the end
you get this error reported. If by any chance there is an exception to
run the command , you would also see that error.

#### 11) CRJAZ1150E The repository was not verified: CRJAZ6043E

CRJAZ1150E The repository was not verified: CRJAZ6043E The area cannot
be created because its name includes one or more of these invalid
characters: & \< \> " ' / Answer: See technote, [ Attempts to upgrade
the IBM Rational Team Concert (RTC) results in the error
CRJAZ6043E.](http://www.ibm.com/support/docview.wss?uid=swg21996330), to
resolve this problem prior to upgrading.

#### 12) CRJAZ1150E The repository was not verified: duplicate permission operation id

Duplicate permission operation id specified:
com.ibm.rrs.manageViewSchedule
com.ibm.team.process.common.service.ProcessDataValidationException:
Duplicate permissions operation id specified:
com.ibm.rrs.manageViewSchedule

Note that the duplicate permission id may vary but same answer still
applies.

Answer: This problem does not affect upgrade and can be ignored. The
issue can be resolved using a diagnostic tool called
NewProjectAreaValidator that can be requested from DNG support.The tool
is configurable using DNG web UI admin page. No restart is required. The
too can detect all DNG PA names which has "Duplicate permission
operation id"

#### 13) Data missing in Queryable join tables

2020-09-22 10:22:35,775 Data missing in Queryable join tables. Please
run the -repairQueryableTables command using repotools. 2020-09-22
10:22:35,775 CRJAZ1150E The repository was not verified: Verification
Failed. Please check logs for more information. 2020-09-22 10:22:35,790
CRJAZ1150E The repository was not verified: Data missing in Queryable
join tables. Please run the -repairQueryableTables command using
repotools.

This issue is new in DOORS Next 7.0.x. This issue occurs if the upgrade
occurred prior to applying an ifix which resolved [APAR PH28537: During
DN 0.6 migration from 6.0.x to 7.0.x, a queryable
helper](https://www.ibm.com/support/pages/node/6334295).

To resolve this issue, get the latest 7.0.x ifix (minimum 7.0.1 ifix 3 /
7.0 ifix 6). Make a backup of the database on the server. Run this
command ./repotools-rm.sh -repairQueryableTables analyzeOnly=true

This will report issues in the table. The report will look like below
2020-09-16 18:52:54,416 \[main\] Found issues with 11 item(s).

If this reports a problem run ./repotools-rm.sh -repairQueryableTables

## Additional details on the types of problems repotools verify find versus the types of problems onlineverify

The repotools -verify command reports errors detected by the
application. Each component can look at the artifacts that it
understands. The verify command looks to see if the tables make sense in
the context of the application.

### Verify Examples

Every Contributor (user), must have a details record (User Name,
photo...) associated with it.

[Project areas names can't have special
characters](http://www-01.ibm.com/support/docview.wss?uid=swg21993070).

For each source project area that has a link to a target project area,
the target project area must exist. The target project area must point
back to the source project area.

Versions of records created in configuration aware project areas must
have unique creation times.

In configuration aware project area, only one version in a given stream
can be the current version.

A given project area's development line references must logically sound.
The development line that is referenced must exist, and must be
considered part of the project area.

In SCM, a changeSet is not allowed to appear more than once in a
workspace's history.

### Online Verify

In ELM several tables hold duplicated data. These can get out of sync.
Here are the tables that are verified: ITEM_STATES, ITEM_TYPES,
ITEM_CURRENTS, CONTENT_STORAGE, and query tables (e..g FRIENDS,
DASHBOARD, MODEL - a workitem),

#### Background

Every time you save a workitem, project area, requirement, or other
artifact on CLM, it's saved into the repository into the tables
mentioned above.

Consider a workitem that is saved. All of the fields in the workitem are
saved in the ITEM_STATES table. This includes both fields that you can
query on and those that you can't.

Every time you save a workitem, a new entry is created in the
ITEM_STATES table. ELM also keeps all the older versions the history of
the workitem - in the ITEM_STATES table. To keep this history as small
as possible, ELM stores larger parts of the workitem (e.g. an
attachment) in CONTENT_STORAGE. So, if you have a large attachment
associated with a workitem. CLM doesn't resave the attachment each time
you save the workitem.

The query table MODEL holds the latest entry of the workitem. The MODEL
table is queried when you run queries to search for workitems. In
general, queries only look at the most recently saved workitem. Examples

Most of the issues are related to data inconsistency. Think of
onlineverify as a tool that finds data inconsistency in tables with
duplicated data. The errors look like this. See also
<https://jazz.net/wiki/bin/view/Deployment/DeploymentTroubleshootingVerifyCommand>

The error below indicates that the query table (e.g. MODEL in the
previous example) doesnt have the same workitem as the ITEM_STATES
table. The Item with ItemID "\_3Ac5BCdeFgHIjkLm7nO6pQ" and StateId
"\_-vUbAMclEdeQfJlWgh3ijk" was found in the ITEM_STATES table, but the
same Item had a different StateId, "\_Y64-zMyxEwvQuJlWts3rqp", in the
Item query table.

Heres another type of inconsistency. The XML for an ITEM is corrupt, or
its not the expected type

2017-04-08 23:49:32,344 The ITEM_STATE row with itemId =
\_xCDJABn-EeemLZ7uEhrfcA, keyId = \_F_sAuxn_EeemLZ7uEhrfcA and itemType
= com.ibm.team.workitem#WorkItem failed to be demarshalled.

Database transactions generally prevent these sort of errors. These
problems are more likely to be a result of database recovery done
incorrectly, or some sort of database administration error. That is, one
table was recovered from a backup but another wasn't.

Not all errors that are reported by online verify indicate that the
product won't work correctly. The errors have to be looked at one by
one.

##### Related topics: [Online Verify Tool](https://jazz.net/wiki/bin/view/Main/L3DevTool), [Repository tools command to verify the integrity of a database](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fr_repotools_verify.html) [related-topics-online-verify-tool-repository-tools-command-to-verify-the-integrity-of-a-database]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.ElisabethCarboneHodel, Main.SusanWu, Main.MichaelAfshar, Main.RosaNaranjo, Main.IanBarnard [additional-contributors-main.elisabethcarbonehodel-main.susanwu-main.michaelafshar-main.rosanaranjo-main.ianbarnard]
