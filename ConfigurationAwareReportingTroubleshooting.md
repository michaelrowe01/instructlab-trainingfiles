META:TOPICINFO{author="wchatham" date="1701854796" format="1.1"
version="1.6"} META:TOPICPARENT{name="ReportingTroubleshooting"}

# Configuration aware reporting Troubleshooting DKGRAY Authors: Main.ErnestMah, Main.RosaNaranjo Build basis: Lifecycle Query Engine (LQE), Lifecycle Index (LDX) 7.0.x [configuration-aware-reporting-troubleshooting-dkgray-authors-main.ernestmah-main.rosanaranjo-build-basis-lifecycle-query-engine-lqe-lifecycle-index-ldx-7.0.x]

ENDCOLOR

TOC{title="Page contents"}

The objective of page is to provide an overview of troubleshooting
techniques for configuration-aware reporting.

## Architecture

## Troubleshooting

### Reindex operations

-   Reindex operation should be a measure of **LAST RESORT**. Only
    perform if requested by Support team.
-   Reindex is an expensive of operation for LQE and LDX as well as the
    application providing the data.
    -   especially for large data providers such as DNG, ETM and EWM.
-   Requesting a reindex essentially renders reporting from a data
    provider unreliable until the reindex operation is complete.
-   If the root cause is not properly diagnosed, one can end up in the
    same state as prior to the reindex AND cause unnecessary outages.

#### What to check before requesting a reindex on a LQE or LDX datasource

-   Check the number of threads for initial/reindexing specified for
    that data provider
-   Ensure that the LQE/LDX has enough CPU/RAM to handle the additional
    work that occurs during the reindex for that data provider

For Example: if the number of threads specified for reindexing in LQE or
LDX is 10

-   There will be 10 threads within LQE/LDX simultaneously contacting
    the tool providing the data. Ensure the number of CPU/vCPU is
    greater than this number as the remaining CPU/vCPU capacity will be
    used to handle other LQE/LDX operations from end users or ongoing
    LQE/LDX activity for other data providers.
-   Ensure the application (its CPU/RAM, etc) can handle 10 simultaneous
    ongoing requests from LQE/LDX. The number of CPU/vCPU needs to be
    greater than this number as the remaining CPU/vCPU capacity will be
    used to handle other operations from end users of the application as
    well as activity within the tool itself

<!-- -->

-   If other data sources have large amounts of data being created
    simultaneously (large scale data imports, automated test case
    execution records created during builds)
    -   Check the number of threads for ongoing/changelog processing of
        each data source and add this number to the number of overall
        threads that are actively being used and ensure to size the
        LQE/LDX application

#### Reasons and considerations for reindexing all datasources again

-   If an LQE/LDX system was overloaded with continuous running queries
    causing the number of writebacks to be exceeded from the default
    threshold setting, it can cause a corrupt Jena index
-   You want to reset the data for any other reason
-   First check the number of threads for reindexing on all the data
    sources
-   Start by indexing the smaller data providers (not EWM, DNG, ETM)
    these can be done in parallel as long as you add up the number of
    threads from the set of simultaneous data providers you want to kick
    off at the same time
-   Next index each large data provider in a sequential manner (DNG, ETM
    EWM)
    -   As was described in the previous slide, ensure the data provider
        tool has enough resources to handle the indexing/reindexing load
        that will be placed from LDE/LDX
-   If there is enough CPU / RAM to consider indexing more than one
    large data provider, make sure you monitor the LQE/LDX system and
    watch that CPU/RAM is not maxed out to an unusable level.

### **How can I make sure the set of data from a data provider is complete in LQE/LDX**

Validation, Validation, Validation!!! The TRS feed is essentially the
contract between the data provider and the data consumer. A data
providers TRS defines the set of data that should be indexed by a
consumer (LQE/LDX).

-   Data provider validation operation checks the TRS is accurate to the
    Data provider's representation.
-   Data consumer validation checks that the consumer (LQE/LDX) index
    (datasources) has the same set of Data.

**Key Limitation**

-   Does not check the content of resources
    -   Global configurations can contain other global or local
        configurations
    -   Local configurations have selection resources that define the
        set of versioned artifacts that are a part of the baseline or
        stream

### **What can happen from the Data Provider (TRS)?**

-   Data Provider server or Network path temporarily down
    -   LQE/LDX app logs issue fetching TRS and will retry at next
        interval

<!-- -->

-   TRS change log truncation - last read change log event not present
    in TRS
    -   LQE/LDX cannot proceed safely with indexing as there could be
        missing events must reindex

**What can lead to change log truncation?**

-   a defect during change log maintenance
-   a data provider or LQE outage longer than 7 days
    -   why do I need to mention the 606 IFix003 improvement? 6.0.6
        ifix003 Increase resiliency of overall system by increasing
        change log event retention period to 14 days for the n-1 version
        of the TRS base document or 28 days from the current version
-   TRS content prior to LQE/LDX's last known event is modified
    -    LQE (7.0) will review one interval priors set of change events
        to see if there are any discrepancies. If there are, it will log
        the discrepancies and attempt to process the events.
-   TRS provides patches that are invalid
    -   Before state (eTag) does not match what is in LQE/LDX
    -   LQE (7.0) will refetch the resource at a later interval to
        recover \* TRS content is not accurate compared to the data
        providers repository \* Action required is a data provider TRS
        validation. for example, RM TRS validation.

**What can happen from the Data Consumer (LQE/LDX)?**

-   LQE/LDX server or Network path temporarily down
    -   LQE/LDX resumes indexing from last known event per data provider
        at the next interval

<!-- -->

-   Content of the LQE/LDX does not match what is supplied in TRS

Referring to the image above...

**LQE/LDX data validation**

-   Compares the set of resources in the index with the Tracked Resource
    Set (TRS)
-   Utilized eTags for comparisons
    -   EWM TaP TRS contains eTags for all artifacts
    -   Configurations modified with patch events in the changelog
        contain eTags (Global Config Management, RM, ETM) (RMM, SCM
        Future)

### **What can happen fetching resources identified by TRS?**

-   Server or network temporarily down (transient)
    -   LQE/LDX captures resources it is unable to fetch during the
        interval into the Skipped Resources list
    -   Administrators can manually retry the entire skip list for
        recovery
    -   LQE/LDX auto retries for skipped resources (\*needs to be
        enabled by LQE or LDX Admin)
-   Application fails to return the artifact
    -   Check Skipped Resource Diagnostic page from Data Provider
    -   Run data provider complimentary diagnostics coordinated with
        skipped resource list
    -   Manage skipped resources
        -   Ignore skipped resources
            -   remove from TRS feed
        -   ability to provide comments for ignoring skipped resources
            (EWM 7.0.1, ETM 6.0.6.1 or later, DNG (target next
            release??)

**Remediation of missing data** \* Identify the data provider (ELM
application) that owns the missing data \* Ensure validation has been
run at the data provider level - this operation compares the data
provider TRS to the actual data in the repository and records the
results \* Validation results that show repairs can provide data
provider developers an idea of where to look for issues. \* Repairs done
by the validation operation may fix the issue but **best practice** is
to run a corresponding LQE/LDX validation for that data provider.

**In general, the idea is to use validation to keep reporting data in
good shape, and fix the primary cause of any regular recurring
validation issues. And, over time, the frequency of the validation can
be reduced.**

### In a configuration-aware report, what controls which artifacts are within scope?

What controls which artifacts are part of a query?

1.  User's access permissions
    1.  Project permission - DNG, ETM, SCM/RMM
    2.  Project or category/Iteration permission - EWM 2. Configuration
        scoped reports
    3.  Full Configuration hierachy
        1.  GC containing other GCs or LCs b. GC - Global configuration
            comes from GCM c. LC - Local configuration comes from ETM,
            DNG, SCM/RMM
            1.  Selections Resource - list of versioned artifacts
    4.  PLUS unversioned resources
        1.  If GC\<-\>EWM release mapped, artifacts and contained links
            will only be returned if GC is selected for which the link
            to the workitem is mapped.

#### Report Builder - Data Completeness Checker

-   Focus on a single global or local configuration to determine if
    everything that is referenced by the configuration is available to
    be considered by the report
    -   Unable to determine if the query itself would have included it
        or filtered it out (if a requirement is skipped, or missing it
        cant know what are the properties/relationships of that
        requirement)
    -   Reduces the scope of what it reports to only those referenced by
        the configuration selected. Does not focus on all skipped
        resources.
    -   looks for resources that the configuration is looking for but
        arent included in the TRS itself
-   Running it once for that configuration is enough to know the status
    of what may be missing which could affect any reports run against
    that same configuration
-   Do not need to run it for every report
-   Slows down reports by up to 20, which is why it should be only run
    on demand, not enabled across the entire system.

**What can be done with this information?** Skipped Resources

-   Inspect the URL. Based on the URL, are these artifacts involved in
    the report at all? If not, you can ignore them
-   If the artifacts are involved in the report, retry the skipped
    resource from LQE and observe if it can now be retrieved.
-   If not, report the issue against the ELM application providing the
    data

Missing Artifacts

-   This represents artifacts that were never found in the TRS from the
    data provider.
-   If a data provider validation does not properly fix the TRS to
    include this artifact, report the issue against the data provider
-   If it is in the TRS from the data provider, then run LQE/LDX
    validation against the datasource from the data provider

Not up-to-date artifacts

-   Go to the LQE admin view for the datasource
-   Go to the Invalid update/patch tab and attempt to repair it there
-   Work with the data provider to see if there is a way to repair the
    selection resource for that configuration (L3 TRS Selections
    Validation/Repair Tool tool for RM)

### What can be done to check that selection resources are correct?

-   RM L3 TRS Selections Validation/Repair Tool (trsSelections.jar)
-   ETM - force refetch of selections via ETM TRS console

### LQE Query Execution details

[https://jazz.net/pub/new-noteworthy/jrs/7.0.2/7.0.2/index.html#11](Detailed Lifecycle Query Engine status information available in Report Builder)

##### Related topics: [TroubleShooting](DeploymentTroubleshooting) , [TRS Validation](https://jazz.net/wiki/bin/view/Deployment/TRSValidation) [related-topics-troubleshooting-trs-validation]

META:FILEATTACHMENT{name="2023-08-01_12-59-00.png"
attachment="2023-08-01_12-59-00.png" attr="" comment="TRS Reporting
Architecture" date="1690909374" path="2023-08-01_12-59-00.png"
size="223678" user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="2023-08-01_13-23-00.png"
attachment="2023-08-01_13-23-00.png" attr="" comment=""
date="1690910618" path="2023-08-01_13-23-00.png" size="29769"
user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="2023-12-05_17-01-49.png"
attachment="2023-12-05_17-01-49.png" attr="h" comment=""
date="1701814326" path="2023-12-05_17-01-49.png" size="67797"
user="rnaranjo" version="2"}
