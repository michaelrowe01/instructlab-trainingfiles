META:TOPICINFO{author="sbagot" date="1432745672" format="1.1"
version="1.9"} META:TOPICPARENT{name="CLMUpgradeTroubleshooting"}

# Environment checklist [environment-checklist]

DKGRAY Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam)
Build basis: CLM 4.x ENDCOLOR

TOC{title="Page contents"}

This page discusses some of the changes to the supported environments
for CLM deployments.

## Before you upgrade

Before upgrading to CLM 4.x, it is important to ensure you are running
in a supported environment. There are many changes between what is
supported in 3.x and 4.x. Navigate to the [4.x System
Requirements](https://jazz.net/library/article/811#mozTocId82758) page
for more information and to validate your environment is supported for
the upgrade.

## Important upgrade facts The sections below address some important changes in the 4.x System Requirments which should be considered when planning your upgrade.

### Database requirements

-   IBM Derby SDK 10.8.1.2 and future fix packs is supported for
    **evaluation purposes** only (for small teams of 10 users or less)
    in CLM 4.x
-   Database support is **64-bit only** to align with 64-bit server
    platforms
-   Oracle is not supported for System z or IBM i
-   SQL Server is supported on Windows Server only

### Application server

-   WebSphere Application Server **v7.0.0.23** is the minimum required
    v7 fixpack to host CLM 4.x, vs v7.0.0.19 in CLM 3.x
-   WebSphere Application Server **6.x** is no longer supported in CLM
    4.x

### General deployment changes

-   32-bit servers are **no longer supported** to host application
    servers running CLM applications, except for small-scale evaluation
    or demonstration purposes
-   For CLM4.x, clustering is supported with WAS ND (7.0.2.3 or 8.0.0.3)
    but also requires the bundled WXS 7.1.1.1

## Version specific system requirements pages

Below are the links to the version specific system requirments:

-   [4.0.1 System Requirements](https://jazz.net/library/article/1109)
-   [4.0 System
    Requirements](https://jazz.net/library/article/811#mozTocId82758)
-   [3.x System Requirements](https://jazz.net/library/article/632)
-   [2.x Server System
    Requirements](http://www-01.ibm.com/support/docview.wss?rs=3488&uid=swg27015746)
-   [2.x Server Rational Team Concert Client
    Requirements](http://www-01.ibm.com/support/docview.wss?rs=3488&uid=swg27015746)

##### Related topics: [related-topics]

\* For more upgrade troubleshooting topics, refer to [Upgrade
Troubleshooting](UpgradeTroubleshooting).

##### External links: [external-links]

\* None

##### Additional contributors: Main.SusanWu [additional-contributors-main.susanwu]
