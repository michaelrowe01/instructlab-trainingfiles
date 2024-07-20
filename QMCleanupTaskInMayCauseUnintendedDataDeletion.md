META:TOPICINFO{author="mguertin77" date="1590766727" format="1.1"
reprev="1.3" version="1.3"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# QM CleanupUnreferencedCollectionRecordsAsyncTask may cause unintended data deletion on 6.0.6.1 DKGRAY Authors: Main.VidyaMalkarnekar, Main.WilliamChen [qm-cleanupunreferencedcollectionrecordsasynctask-may-cause-unintended-data-deletion-on-6.0.6.1-dkgray-authors-main.vidyamalkarnekar-main.williamchen]

Build basis: IBM Rational Quality Manager 6.0.6.1, 6.0.6.1 iFix001, and
6.0.6.1 iFix002 ENDCOLOR

TOC{title="Page contents"}

In IBM Rational Quality Manager (RQM) 6.0.6.1, the newly added
CleanupUnreferencedCollectionRecordsAsyncTask may cause unintended
deletion of rows from certain internal database tables resulting in the
data not being visible in some artifact section views. The task is
designed to remove rows that are no longer referenced from certain
internal database tables. However, it may incorrectly remove some rows
that are still referenced. Therefore, users must disable the
CleanupUnreferencedCollectionRecordsAsyncTask on these 6.0.6.1 servers,
including 6.0.6.1, 6.0.6.1 iFix001, and 6.0.6.1 iFix002.

Important: The CleanupUnreferencedCollectionRecordsAsyncTask is disabled
and removed from 6.0.6.1 iFix003 and above.

## Symptoms

Users might see empty result lists when sorting or filtering in certain
section views, e.g. Test Cases/Test Suites list view in Test Plans.

Note: The data is still in the database and IBM is actively working on a
repair tool to restore it.

## Temporarily solution

Users must follow these steps to disable the
CleanupUnreferencedCollectionRecordsAsyncTask on these servers: 6.0.6.1,
6.0.6.1 iFix001, and 6.0.6.1 iFix002:

1\. Navigate to RQM Administration page via <https://://admin> page.

2\. Click Advanced Properties link under Configuration.

3\. Search for CleanupUnreferencedCollectionRecordsAsyncTask, and change
the value for "The time interval in seconds between the execution of
this task" to -1.

4\. Save the new changes and restart the server.

## Repair utility

A new repair utility is required to restore all impacted QM data. The
instructions for how to run the repair utility can be found at the
following locations:

-   6.0.6.1: [Repository tools command to recreate incorrectly removed
    queryable table
    data](https://supportcontent.ibm.com/support/pages/repository-tools-command-recreate-incorrectly-removed-queryable-table-data-0)
-   7.0: [Repository tools command to recreate incorrectly removed
    queryable table
    data](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.0/com.ibm.jazz.install.doc/topics/r_repotools_repairqueryabletables.html)

The issue was being tracked via this Jazz workitem:

[Create repair utility to recreate incorrectly removed Queryable table
data.](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=486231)

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.ChristopherRobinson [additional-contributors-main.christopherrobinson]
