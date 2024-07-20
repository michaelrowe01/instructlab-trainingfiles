META:TOPICINFO{author="rnaranjo" date="1399653459" format="1.1"
version="1.7"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Rational Team Concert online migration test matrix [rational-team-concert-online-migration-test-matrix]

DKGRAY Authors: Main.AndrewNiefer, Main.LisaFrankel Build basis: CLM 5.0
ENDCOLOR

TOC{title="Page contents"}

Starting in Rational Team Concert V5.0, you can choose to migrate data
from an older version of the product to the latest product version while
the production server is still online. This migration method is called
pre-upgrade online migration. Before implementing an online migration,
determine whether offline or online migration is warranted for your
repository by running the migration estimation command and then checking
the following test results matrix for guidance on the results.

If online migration is recommended for your repository, follow the
detailed instructions in the [Collaborative Lifecycle Management V5.0
Knowledge Center, Interactive upgrade
guide](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.0/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html).

## Testing matrix

Unless noted as a production migration, the following times were
obtained on a Linux VM image with 2 CPUs and 16G RAM, running at
2.27GHz, with DB2 and the CCM server running on the same machine. The
default parameters for the online miration command are **`priority=50`**
and **`numStatesPerRun=100`**.

\| **Data** \| **Database** \| **Repository size** \| **Artifact counts
BR (migrating states / total)** \| **Parameters BR (priority,
numStatesPerRun)** \| **Online migration time** \| **Additional offline
time BR (addTables)** \| Notes \|

|  |  |  |  |  |  |  |  |
|----|----|----|----|----|----|----|----|
| Jazz.net CCM | DB2 | 489GB | 2.6M / 28M | p=100, n=1000 | 9h | 2h50m |  |
| \^ | \^ | \^ | \^ | p=100, n=100 | 8h50m | 2h50m |  |
| \^ | \^ | \^ | \^ | p=50, n=100 (defaults) | 12h | 1h45m | Production server migration |
| Jazzdev 02 | DB2 | 179GB | 658/10M | defaults | 2h 15m | 1h | Production server migration |
| SCM team test machine | DB2 | 173GB | 930K / 9.2M | defaults | 1h30m | 25m |  |
| Jazzdev 04 | DB2 |  | 240k | defaults | 1h | 20m | Production server migration |
| JazzHub staging | DB2 | 43GB | 35k / 6M | defaults | 6m | 9m | Many small project areas |

After an online migration has processed 1 of the states, an estimated
completion time is displayed.

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [Online migration for Rational Team Concert
    data](http://www-01.ibm.com/support/knowledgecenter/api/content/SSYMRC_5.0.0/com.ibm.jazz.install.doc/topics/c_online_migration_rtc.html)

##### Additional contributors: Main.RosaNaranjo [additional-contributors-main.rosanaranjo]
