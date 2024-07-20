# What to backup prior to an upgrade

Authors: Main.StephanieBagot,
Build basis: CLM 3.x and later 

This page will discuss the necessary configuration and file backups
required prior to beginning an upgrade with the Collaborative Lifecycle
Management (CLM) family of products (Rational Team Concert, Rational
Requirements Composer, and Rational Quality Manager).

## What to backup

Below is a list of the necessary items to backup prior to an upgrade:

-   WebSphere Application Server profile
-   Application Database, Data Warehouse Database
-   Local Indices through [repotools-jts
    -backupJFSIndexes](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.install.doc/topics/r_repotools_backupjfsindexes.html&scope=null)

## Errors which may occur

Below discusses some errors which may occur at this stage of the upgrade
process

### repotools-jts -backupJFSIndexes

**Version:** Upgrade to 4.x **Error During Upgrade:** Backing up indices
failed. **Resolution:** Check the repotools-jts_backupJFSindexes.log
file for details as to why the backup failed.

##### Related topics: 
* None [related-topics-none]

##### External links: 
* None [external-links-none]

##### Additional contributors: 
* Main.StephanieBagot, [additional-contributors-main.stephaniebagot]
