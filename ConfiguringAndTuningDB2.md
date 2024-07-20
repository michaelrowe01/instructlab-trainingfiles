META:TOPICINFO{author="sbeard" date="1422035663" format="1.1"
version="1.18"} META:TOPICPARENT{name="DeploymentAdminstering"}

# Configuring and tuning DB2 [configuring-and-tuning-db2]

DKGRAY Authors: [DanToczala](Main.DavidToczala) Build basis: CLM 2012,
CLM 2011 ENDCOLOR

TOC{title="Page contents"}

## Initial assessment

|  |
|----|
| Database tuning is outside of the scope of the Jazz Administrator. Any information provided below is for reference only and should be passed to your database administrator. |

When discussing the tuning of DB2, it is important to note the various
editions of DB2, such as DB2 Workgroup, DB2 Enterprise, and DB2 for
z/OS. Jazz licensing currently supports the use of DB2 Workgroup
Edition.

DB2 Express is also supported, but it should *not* be used for anything
other than a product demo, pilot project, or functionality review,
because it will not scale to support a typical user load.

## DB2 for z/OS

Most DB2 customers turn on the following monitoring and tracing for
their Jazz-supporting DB2 instance on z/OS:

|     |       |              |      |      |       |
|-----|-------|--------------|------|------|-------|
| TNO | TYPE  | CLASS        | DEST | QUAL | IFCID |
| 01  | STAT  | 01,03,04,05, | SMF  | NO   |       |
| 01  |       | 06           |      |      |       |
| 02  | ACCTG | 01,02,03,07, | SMF  | NO   |       |
| 02  |       | 08           |      |      |       |
| 04  | MON   | 01,02,03,05, | OP1  | NO   |       |
| 04  |       | 07, 08       |      |      |       |

How to interpret the previous table:

-   For statistics, monitor classes 1, 3, 4, 5, and 6. This shows
    overall health.
-   For accounting purposes, monitor classes 1, 2, 3, 7, and 8. This
    gets into more specifics about what is happening.
-   For monitoring purposes, monitor classes 1, 2, 3, 5, 7, and 8.

When working with DB2 you should be doing a RUNSTATS \[multi-table,
multi-index\] whenever you make changes to the DB2 database. The
database administrator should complete this action on a regular basis to
ensure that DB2 performs efficiently.

If this doesnt work, you might want to increase MAX_R_BLOCK in the z/OS
parameters.

|  |
|----|
| **Note:** Thorough DB2 administrators will want to create indexes based on the results from some of the monitoring and the RUNSTATS commands. They can do this, but make sure that you measure database performance both before and after doing this, so you can determine the impact on performance. |

## DB2 Enterprise Edition

Need real tuning examples here.

## DB2 Workgroup Edition

Need real tuning examples here.

##### Related topics: [Deployment troubleshooting](DeploymentTroubleshooting), [Deployment monitoring](DeploymentMonitoring) [related-topics-deployment-troubleshooting-deployment-monitoring]

##### External links: [external-links]

###### System requirements \* [Rational CLM 4.0.3](CLMSystemRequirements403)

-   [Rational CLM 4.0.1 and
    4.0.2](https://jazz.net/library/article/1109)
-   [Rational CLM 4.0](https://jazz.net/library/article/811)
-   [Rational CLM 3.0.1.x](https://jazz.net/library/article/632)
-   Including: Rational Team Concert, Rational Quality Manager, Rational
    Requirements Composer, Rational DOORS Next Generation, and Rational
    Reporting for Development Intelligence

##### Additional contributors: None [additional-contributors-none]

##### Questions and comments: [questions-and-comments]

COMMENT{type="below" target="ConfiguringAndTuningDB2Comments"
button="Submit"}

INCLUDE{"ConfiguringAndTuningDB2Comments"}

META:TOPICMOVED{by="sbeard" date="1385833391"
from="Deployment.TuningDB2" to="Deployment.ConfiguringAndTuningDB2"}
