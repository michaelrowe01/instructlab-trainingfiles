META:TOPICINFO{author="sbagot" date="1380141900" format="1.1"
version="1.2"} META:TOPICPARENT{name="CLMUpgradeTroubleshooting"}

# Upgrade troubleshooting [upgrade-troubleshooting]

DKGRAY Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam)
Build basis: CLM 3.x and later ENDCOLOR

TOC{title="Page contents"}

This page is discusses reindexing the server after the upgrade, when
testing proves that the upgrade may not have been successful.

## Differences between re-index commands

There are three different re-index commands which can be run through
repotools. Below, each command will be discussed.

### reindex This command is used to rebuild the Jazz Foundation Server (JFS) index. JFS indices are only used by JTS and are utilized by the dashboards and on RTC/z (EE) for a particular build app, otherwise they are not used on ccm nor qm. If the dashboards are failing then that would indicate a problem with the JFS index. ---+++ rebuildIndices

This command will rebuild the database indices.

### rebuildTextIndices

This command will rebuild the workitem lucene indexer which is used by
the workitems for text searches. If workitems or query search results
are not accurate, that would indicate problem with workitem indexer and
you may consider running this command to rebuild it.

## Reindexing during the Upgrade

Reindex and RebuiltTextIndices repotools commands are run as part of the
upgrade process, executed by the upgrade script. It is not mandatory
that they are run seperately unless there is some indication that the
indices are corrupt.

## When to manually run the index commands

The following conditions may warrant running the reindex commands: \*
Indication of index corruption \* Full Text queries are failing \*
Dashboard issues after the upgrade (where no dashboard migration
occured)

## How long will this command take to run?

The time to run the reindexing commands will depend on the size of the
repository database and total workitems contained, and also the size of
workitemindex folder. Here is the benchmark we have for jazz.net:

-   Approx. total WIs in ccm: 248,000
-   ccm repository : 415 GB
-   jts repository: 15 GB
-   the workitemidex folder for ccm is approx. 1.5 GB

<!-- -->

-   Time took to complete repotools-ccm -rebuildTextIndices: approx. 2.5
    hours (this was to remove the old workitem indices and rebuild from
    scratch)
-   Time took to complete repotools-ccm -reindex: 15 minutes.

## Where do I go from here? If you are unable to resolve your issue using the available online resources, open a service request with IBM Rational Support. Refer to [Additional troubleshooting resources](DataCollectionandSupportResources) for further details.

##### Related topics: None [related-topics-none]

##### External links: \* None [external-links-none]

##### Additional contributors: Main.StephanieBagot, Main.SusanWu, Main.MichaelAfshar, Main.WilliamChen, Main.BrettBohnn [additional-contributors-main.stephaniebagot-main.susanwu-main.michaelafshar-main.williamchen-main.brettbohnn]
