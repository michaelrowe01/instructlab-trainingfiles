META:TOPICINFO{author="clin" date="1435333919" format="1.1"
version="1.9"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Version Compatibility Matrix for CLM, ALM Cognos Connector, RRDI, and Rational Insight [version-compatibility-matrix-for-clm-alm-cognos-connector-rrdi-and-rational-insight]

DKGRAY Authors: Main.ChengYeeLin Build basis: CLM 6.0 and Insight
1.1.1.7 Latest update: June, 2015 ENDCOLOR

TOC{title="Page contents"}

For CLM 3.0.1 through 5.0.2, Rational Reporting for Development
Intelligence (RRDI) provides Cognos-based reporting solution for the CLM
product family: RTC, RQM, and RDNG. It provides reporting capabilities
through a bundled Cognos Business Intelligence (BI) installation with
CLM integration. Specifically in its 5.0.x versions, RRDI also includes
additional capabilities, Data Collection Component (DCC), for addressing
key performance and deployment concerns with the existing ETL solutions,
and, Jazz Reporting Service (also known as Report Builder in a later
release), for providing self-serve reporting capability and
out-of-the-box operational reports with easy integration with the CLM
dashboards through the widget catalog.

For CLM 6.0, the reporting package has been changed/expanded and becomes
a more integral part of the CLM products. As a result, a top-level Jazz
Reporting Service (JRS) package is created as a part of the CLM
installer that includes DCC, Report Builder, and Lifecycle Query Engine
(LQE) which implements a linked lifecycle data index over data provided
by multiple lifecycle tools and enables cross-tool queries and links. In
the area of Cognos-based reporting, RRDI is no longer available for the
CLM 6.0 version, while an ALM Cognos Connector package is available on
the Jazz Reporting Service download page for configuring and integrating
with a standalone Cognos BI solution.

Rational Insight builds on RRDI by adding additional capabilities below:

-   Ability to aggregate data from multiple JTS into a single data
    warehouse for integrated reporting
-   Data acquisition from more Rational products
-   Many Out Of The Box reports providing directly useful information.
    They can also be customized to meet customer specific requirements.
-   Ability to customize the Data Warehouse, ETL, and reporting data
    model
-   Scorecard creation tools
-   Support for namespaces other than "Jazz"
-   Provdes additional Cognos functionality:
    -   Business Insight
    -   Business Insight Advanced
    -   Event Studio

The Insight 1.1.1.7 version works with CLM 6.0.

Both RRDI and Insight can integrate with CLM for data acquisition, use
of a common data warehouse, user authentication, and the ability to
execute and view reports through the CLM product's UI. This brings up
the question of what versions of these products are compatible and
whether an upgrade path or a migration path exists.

The migration from RRDI 5.0.2 to ALM Cognos Connector for CLM 6.0 can be
found in the CLM 6.0 Knowledge Center. The general process is to upgrade
CLM first, and then migrate from RRDI to ALM Cognos Connector. See
[Migrating
RRDI](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_6.0.0/com.ibm.rational.rrdi.admin.doc/topics/t_migrate_cognos_ov.html)
for the detailed procedure.

The upgrade procedure for Rational Insight 1.1.1.7 can be found in the
updated Insight 1.1.1.7 Knowledge Center. See [Upgrading Rational
Insight](http://www.ibm.com/support/knowledgecenter/SSRL5J_1.1.1.7/com.ibm.rational.raer.migrating.doc/topics/c_upgrade_overview.html)
for the detailed procedure.

## RRDI Upgrade compatibility (No update after the CLM 5.0.2 version)

For RRDI, the following rules govern upgrades and version compatibility
with CLM:

-   When upgrading, upgrade CLM first, then RRDI. The report packages
    for CLM (in the form of Cognos archives) should be loaded after RRDI
    upgrade.
-   RRDI and CLM upgrades do not have to be done atomically.
    Intermediate states are supported.
-   When upgrading from CLM 3.0.1.\*, there are required minimum
    versions of the RQM and RDNG applications. See the CLM documentation
    for details.
-   The table below shows the supported combinations.
-   RRDI 1.0.2.\* versions refer to the 1.0.2 and 1.0.2.1 versions.
-   RRDI 2.0.0.\* versions refer to the 2.0 and 2.0.0.1 versions.
-   RRDI 2.0.\* version refer to the 2.0.1 through 2.0.6 versions.
-   RRDI 5.0.\* version refer to the 5.0 through 5.0.2 versions.

|  |  |
|----|----|
| RRDI Version | Supported CLM Versions |
| 1.0.2.\* | JTS 3.0.1.\* and RTC, RQM, RDNG at 3.0.1.\* |
| 2.0, 2.0.0.1 | JTS 4.0.0.\* and RTC, RQM, RDNG at 3.0.1.\* or 4.0.0.\* |
| 2.0.1 | JTS 4.0.1.**/4.0.2 and RTC, RQM, RDNG at 3.0.1.**, 4.0.0.**, 4.0.1, or 4.0.2 \| \| 2.0.3 \| JTS 4.0.3 and RTC, RQM, RDNG at 3.0.1.**, 4.0.0.**, 4.0.1.**, 4.0.2, or 4.0.3 |
| 2.0.4 | JTS 4.0.4 and RTC, RQM, RDNG at 3.0.1.**, 4.0.0.**, 4.0.1.**, 4.0.2, 4.0.3, or 4.0.4 \| \| 2.0.5 \| JTS 4.0.5 and RTC, RQM, RDNG at 3.0.1.**, 4.0.0.**, 4.0.1.**, 4.0.2, 4.0.3, 4.0.4, or 4.0.5 |
| 2.0.6 | JTS 4.0.6/4.0.7 and RTC, RQM, RDNG at 3.0.1.**, or 4.0.** |
| 5.0 | JTS 5.0 and RTC, RQM, RDNG at 3.0.1.**, 4.0.**, or 5.0 |
| 5.0.1 | JTS 5.0.1 and RTC, RQM, RDNG at 3.0.1.**, 4.0.**, 5.0, or 5.0.1 |
| 5.0.2 | JTS 5.0.2 and RTC, RQM, RDNG at 3.0.1.**, 4.0.**, or 5.0.\* |

Upgrade paths exists for the following release combinations. CLM
versions in the following table refer primarily to the JTS version where
the actual CLM applications (RTC, RQM, RDNG) can be that same version or
a prior version supported by that JTS version.

|                              |                                        |
|------------------------------|----------------------------------------|
| From Release                 | To Release                             |
| CLM 3.0.1.\* / No RRDI       | CLM 3.0.1.\* with RRDI 2.0.\* or 5.0.2 |
| CLM 3.0.1.\* / No RRDI       | CLM 4.0.\* with RRDI 2.0.\* or 5.0.2   |
| CLM 3.0.1.\* / No RRDI       | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 3.0.1.\* / RRDI 1.0.2    | CLM 3.0.1.\* with RRDI 2.0.\* or 5.0.2 |
| CLM 3.0.1.\* / RRDI 1.0.2    | CLM 4.0.\* with RRDI 2.0.\* or 5.0.2   |
| CLM 3.0.1.\* / RRDI 1.0.2    | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 3.0.1.\* / RRDI 2.0.0.\* | CLM 3.0.1.\* with RRDI 2.0.\* or 5.0.2 |
| CLM 3.0.1.\* / RRDI 2.0.0.\* | CLM 4.0.\* with RRDI 2.0.\* or 5.0.2   |
| CLM 3.0.1.\* / RRDI 2.0.0.\* | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 3.0.1.\* / RRDI 2.0.\*   | CLM 3.0.1.\* with RRDI 2.0.\* or 5.0.2 |
| CLM 3.0.1.\* / RRDI 2.0.\*   | CLM 4.0.\* with RRDI 2.0.\* or 5.0.2   |
| CLM 3.0.1.\* / RRDI 2.0.\*   | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 3.0.1.\* / RRDI 5.0.\*   | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 4.0.0.\* / No RRDI       | CLM 4.0.0.\* with RRDI 2.0.\* or 5.0.2 |
| CLM 4.0.0.\* / No RRDI       | CLM 4.0.\* with RRDI 2.0.\* or 5.0.2   |
| CLM 4.0.0.\* / No RRDI       | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 4.0.0.\* / RRDI 2.0.0.\* | CLM 4.0.0.\* with RRDI 2.0.\* or 5.0.2 |
| CLM 4.0.0.\* / RRDI 2.0.0.\* | CLM 4.0.\* with RRDI 2.0.\* or 5.0.2   |
| CLM 4.0.0.\* / RRDI 2.0.0.\* | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 4.0.0.\* / RRDI 2.0.\*   | CLM 4.0.0.\* with RRDI 2.0.\* or 5.0.2 |
| CLM 4.0.0.\* / RRDI 2.0.\*   | CLM 4.0.\* with RRDI 2.0.\* or 5.0.2   |
| CLM 4.0.0.\* / RRDI 2.0.\*   | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 4.0.0.\* / RRDI 5.0.\*   | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 4.0.1.\* / No RRDI       | CLM 4.0.1.\* with RRDI 2.0.\* or 5.0.2 |
| CLM 4.0.1.\* / No RRDI       | CLM 4.0.\* with RRDI 2.0.\* or 5.0.2   |
| CLM 4.0.1.\* / No RRDI       | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 4.0.1.\* / RRDI 2.0.\*   | CLM 4.0.1.\* with RRDI 2.0.\* or 5.0.2 |
| CLM 4.0.1.\* / RRDI 2.0.\*   | CLM 4.0.\* with RRDI 2.0.\* or 5.0.2   |
| CLM 4.0.1.\* / RRDI 2.0.\*   | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 4.0.1.\* / RRDI 5.0.\*   | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 4.0.\* / No RRDI         | CLM 4.0.\* with RRDI 2.0.\* or 5.0.2   |
| CLM 4.0.\* / No RRDI         | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 4.0.\* / RRDI 2.0.\*     | CLM 4.0.\* with RRDI 2.0.\* or 5.0.2   |
| CLM 4.0.\* / RRDI 2.0.\*     | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 4.0.\* / RRDI 5.0.\*     | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 5.0 / No RRDI            | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 5.0 / RRDI 2.0.\*        | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 5.0 / RRDI 5.0.\*        | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 5.0.1 / No RRDI          | CLM 5.0.2 with RRDI 5.0.2              |
| CLM 5.0.1 / RRDI 5.0.\*      | CLM 5.0.2 with RRDI 5.0.2              |

## Rational Insight Upgrade compatibility

The latest release of Rational Insight is 1.1.1.7.

The following rules govern Rational Insight upgrades:

-   Insight 1.1.1.7 requires JTS 6.0 and 6.0 Data Manager ETLs for the
    minimal configuration. You can have CLM applications with prior
    versions, though you must use the proper corresponding version of
    the ETLs. JTS 6.0 Data Manager ETLs are also compatible with Insight
    1.1.1.7.
-   CLM 6.0 requires Insight 1.1.1.7.
-   When upgrading both JTS and Insight, Insight MUST be upgraded first
    and both upgrades MUST be done atomically. Intermediate states are
    not supported. The CLM applications can be upgraded later, provided
    you use the correct ETLs.
-   When upgrading the JTS from 3.0.1.\* to 4.0.0.\* or above, CLM has
    minimum required versions of RQM and RDNG. See the CLM upgrade
    documentation.
-   The table below shows supported release combinations.

If you are using Rational Insight with CLM, this table shows which
Insight version works with each JTS version. Note that you must choose
the proper Insight version for the JTS version. Unlike RRDI, an Insight
version will need to work with a compatible JTS version (or at least one
JTS with a compatible version in a multi-JTS deployment topology). Older
CLM applications will work with Insight, provided the JTS version is
compatible. To use older CLM applications, you must get the proper
Cognos Data Manager ETL jobs. They are supplied with the JTS. The reason
for this is that the ETL jobs must match the Data Warehouse schema
created by the JTS, and use the proper REST web interface to access the
CLM application.

|  |  |  |
|----|----|----|
| Insight Version | Supported CLM Versions | ETL Requirement |
| 1.1 | JTS 3.0.1.\* and RTC, RQM, RDNG at 3.0.1.\* |  |
| 1.1.1 | JTS 4.0.0.\* and RTC, RQM, RDNG at 3.0.1.\* | Data Manager ETLs from JTS 4.0.0.\* for the 3.0.1.\* apps |
| 1.1.1 | JTS 4.0.0.\* and RTC, RQM, RDNG at 4.0 or 4.0.0.\* |  |
| 1.1.1.1 | JTS 4.0.1.**/4.0.2 and RTC, RQM, RDNG at 3.0.1.** | Data Manager ETLs from JTS 4.0.1.**/4.0.2 for the 3.0.1.** apps. See CLM documentation for required 3.0.1 fixpack levels |
| 1.1.1.1 | JTS 4.0.1.**/4.0.2 and RTC, RQM, RDNG at 4.0.0.** | Data Manager ETLs from JTS 4.0.1.**/4.0.2 for the 4.0.0.** apps |
| 1.1.1.1 | JTS 4.0.1.**/4.0.2 and RTC, RQM, RDNG at 4.0.1.** | Data Manager ETLs from JTS 4.0.1.**/4.0.2 for the 4.0.1.** apps |
| 1.1.1.1 | JTS 4.0.2 and RTC, RQM, RDNG at 4.0.2 |  |
| 1.1.1.2 | JTS 4.0.3/4.0.4 and RTC, RQM, RDNG at 3.0.1.\* | Data Manager ETLs from JTS 4.0.3/4.0.4 for the 3.0.1.\* apps. See CLM documentation for required 3.0.1 fixpack levels |
| 1.1.1.2 | JTS 4.0.3/4.0.4 and RTC, RQM, RDNG at 4.0.0.\* | Data Manager ETLs from JTS 4.0.3/4.0.4 for the 4.0.0.\* apps |
| 1.1.1.2 | JTS 4.0.3/4.0.4 and RTC, RQM, RDNG at 4.0.1.\* | Data Manager ETLs from JTS 4.0.3/4.0.4 for the 4.0.1.\* apps |
| 1.1.1.2 | JTS 4.0.3/4.0.4 and RTC, RQM, RDNG at 4.0.2 | Data Manager ETLs from JTS 4.0.3/4.0.4 for the 4.0.2 apps |
| 1.1.1.2 | JTS 4.0.3/4.0.4 and RTC, RQM, RDNG at 4.0.3 | Data Manager ETLs from JTS 4.0.3/4.0.4 for the 4.0.3 apps |
| 1.1.1.2 | JTS 4.0.4 and RTC, RQM, RDNG at 4.0.4 |  |
| 1.1.1.3 | JTS 4.0.5/4.0.6/4.0.7 and RTC, RQM, RDNG at 3.0.1.\* | Data Manager ETLs from JTS 4.0.5/4.0.6/4.0.7 for the 3.0.1.\* apps. See CLM documentation for required 3.0.1 fixpack levels |
| 1.1.1.3 | JTS 4.0.5/4.0.6/4.0.7 and RTC, RQM, RDNG at 4.0.0.\* | Data Manager ETLs from JTS 4.0.5/4.0.6/4.0.7 for the 4.0.0.\* apps |
| 1.1.1.3 | JTS 4.0.5/4.0.6/4.0.7 and RTC, RQM, RDNG at 4.0.1.\* | Data Manager ETLs from JTS 4.0.5/4.0.6/4.0.7 for the 4.0.1.\* apps |
| 1.1.1.3 | JTS 4.0.5/4.0.6/4.0.7 and RTC, RQM, RDNG at 4.0.2 | Data Manager ETLs from JTS 4.0.5/4.0.6/4.0.7 for the 4.0.2 apps |
| 1.1.1.3 | JTS 4.0.5/4.0.6/4.0.7 and RTC, RQM, RDNG at 4.0.3 | Data Manager ETLs from JTS 4.0.5/4.0.6/4.0.7 for the 4.0.3 apps |
| 1.1.1.3 | JTS 4.0.5/4.0.6/4.0.7 and RTC, RQM, RDNG at 4.0.4 | Data Manager ETLs from JTS 4.0.5/4.0.6/4.0.7 for the 4.0.4 apps |
| 1.1.1.3 | JTS 4.0.5/4.0.6/4.0.7 and RTC, RQM, RDNG at 4.0.5 | Data Manager ETLs from JTS 4.0.5/4.0.6/4.0.7 for the 4.0.5 apps |
| 1.1.1.3 | JTS 4.0.6/4.0.7 and RTC, RQM, RDNG at 4.0.6 | Data Manager ETLs from JTS 4.0.6/4.0.7 for the 4.0.6 apps |
| 1.1.1.3 | JTS 4.0.7 and RTC, RQM, RDNG at 4.0.7 |  |
| 1.1.1.4 | JTS 5.0 and RTC, RQM, RDNG at 3.0.1.\* | Data Manager ETLs from JTS 5.0 for the 3.0.1.\* apps. See CLM documentation for required 3.0.1 fixpack levels |
| 1.1.1.4 | JTS 5.0 and RTC, RQM, RDNG at 4.0.0.\* | Data Manager ETLs from JTS 5.0 for the 4.0.0.\* apps |
| 1.1.1.4 | JTS 5.0 and RTC, RQM, RDNG at 4.0.1.\* | Data Manager ETLs from JTS 5.0 for the 4.0.1.\* apps |
| 1.1.1.4 | JTS 5.0 and RTC, RQM, RDNG at 4.0.2 | Data Manager ETLs from JTS 5.0 for the 4.0.2 apps |
| 1.1.1.4 | JTS 5.0 and RTC, RQM, RDNG at 4.0.3 | Data Manager ETLs from JTS 5.0 for the 4.0.3 apps |
| 1.1.1.4 | JTS 5.0 and RTC, RQM, RDNG at 4.0.4 | Data Manager ETLs from JTS 5.0 for the 4.0.4 apps |
| 1.1.1.4 | JTS 5.0 and RTC, RQM, RDNG at 4.0.5 | Data Manager ETLs from JTS 5.0 for the 4.0.5 apps |
| 1.1.1.4 | JTS 5.0 and RTC, RQM, RDNG at 4.0.6 | Data Manager ETLs from JTS 5.0 for the 4.0.6 apps |
| 1.1.1.4 | JTS 5.0 and RTC, RQM, RDNG at 4.0.7 | Data Manager ETLs from JTS 5.0 for the 4.0.7 apps |
| 1.1.1.4 | JTS 5.0 and RTC, RQM, RDNG at 5.0 |  |
| 1.1.1.5 | JTS 5.0.1 and RTC, RQM, RDNG at 3.0.1.\* | Data Manager ETLs from JTS 5.0.1 for the 3.0.1.\* apps. See CLM documentation for required 3.0.1 fixpack levels |
| 1.1.1.5 | JTS 5.0.1 and RTC, RQM, RDNG at 4.0.0.\* | Data Manager ETLs from JTS 5.0.1 for the 4.0.0.\* apps |
| 1.1.1.5 | JTS 5.0.1 and RTC, RQM, RDNG at 4.0.1.\* | Data Manager ETLs from JTS 5.0.1 for the 4.0.1.\* apps |
| 1.1.1.5 | JTS 5.0.1 and RTC, RQM, RDNG at 4.0.2 | Data Manager ETLs from JTS 5.0.1 for the 4.0.2 apps |
| 1.1.1.5 | JTS 5.0.1 and RTC, RQM, RDNG at 4.0.3 | Data Manager ETLs from JTS 5.0.1 for the 4.0.3 apps |
| 1.1.1.5 | JTS 5.0.1 and RTC, RQM, RDNG at 4.0.4 | Data Manager ETLs from JTS 5.0.1 for the 4.0.4 apps |
| 1.1.1.5 | JTS 5.0.1 and RTC, RQM, RDNG at 4.0.5 | Data Manager ETLs from JTS 5.0.1 for the 4.0.5 apps |
| 1.1.1.5 | JTS 5.0.1 and RTC, RQM, RDNG at 4.0.6 | Data Manager ETLs from JTS 5.0.1 for the 4.0.6 apps |
| 1.1.1.5 | JTS 5.0.1 and RTC, RQM, RDNG at 4.0.7 | Data Manager ETLs from JTS 5.0.1 for the 4.0.7 apps |
| 1.1.1.5 | JTS 5.0.1 and RTC, RQM, RDNG at 5.0 | Data Manager ETLs from JTS 5.0.1 for the 5.0 apps |
| 1.1.1.5 | JTS 5.0.1 and RTC, RQM, RDNG at 5.0.1 |  |
| 1.1.1.6 | JTS 5.0.2 and RTC, RQM, RDNG at 3.0.1.\* | Data Manager ETLs from JTS 5.0.2 for the 3.0.1.\* apps. See CLM documentation for required 3.0.1 fixpack levels |
| 1.1.1.6 | JTS 5.0.2 and RTC, RQM, RDNG at 4.0.0.\* | Data Manager ETLs from JTS 5.0.2 for the 4.0.0.\* apps |
| 1.1.1.6 | JTS 5.0.2 and RTC, RQM, RDNG at 4.0.1.\* | Data Manager ETLs from JTS 5.0.2 for the 4.0.1.\* apps |
| 1.1.1.6 | JTS 5.0.2 and RTC, RQM, RDNG at 4.0.2 | Data Manager ETLs from JTS 5.0.2 for the 4.0.2 apps |
| 1.1.1.6 | JTS 5.0.2 and RTC, RQM, RDNG at 4.0.3 | Data Manager ETLs from JTS 5.0.2 for the 4.0.3 apps |
| 1.1.1.6 | JTS 5.0.2 and RTC, RQM, RDNG at 4.0.4 | Data Manager ETLs from JTS 5.0.2 for the 4.0.4 apps |
| 1.1.1.6 | JTS 5.0.2 and RTC, RQM, RDNG at 4.0.5 | Data Manager ETLs from JTS 5.0.2 for the 4.0.5 apps |
| 1.1.1.6 | JTS 5.0.2 and RTC, RQM, RDNG at 4.0.6 | Data Manager ETLs from JTS 5.0.2 for the 4.0.6 apps |
| 1.1.1.6 | JTS 5.0.2 and RTC, RQM, RDNG at 4.0.7 | Data Manager ETLs from JTS 5.0.2 for the 4.0.7 apps |
| 1.1.1.6 | JTS 5.0.2 and RTC, RQM, RDNG at 5.0 | Data Manager ETLs from JTS 5.0.2 for the 5.0 apps |
| 1.1.1.6 | JTS 5.0.2 and RTC, RQM, RDNG at 5.0.1 | Data Manager ETLs from JTS 5.0.2 for the 5.0.1 apps |
| 1.1.1.6 | JTS 5.0.2 and RTC, RQM, RDNG at 5.0.2 |  |
| 1.1.1.7 | JTS 6.0 and RTC, RQM, RDNG at 3.0.1.\* | Data Manager ETLs from JTS 6.0 for the 3.0.1.\* apps. See CLM documentation for required 3.0.1 fixpack levels |
| 1.1.1.7 | JTS 6.0 and RTC, RQM, RDNG at 4.0.0.\* | Data Manager ETLs from JTS 6.0 for the 4.0.0.\* apps |
| 1.1.1.7 | JTS 6.0 and RTC, RQM, RDNG at 4.0.1.\* | Data Manager ETLs from JTS 6.0 for the 4.0.1.\* apps |
| 1.1.1.7 | JTS 6.0 and RTC, RQM, RDNG at 4.0.2 | Data Manager ETLs from JTS 6.0 for the 4.0.2 apps |
| 1.1.1.7 | JTS 6.0 and RTC, RQM, RDNG at 4.0.3 | Data Manager ETLs from JTS 6.0 for the 4.0.3 apps |
| 1.1.1.7 | JTS 6.0 and RTC, RQM, RDNG at 4.0.4 | Data Manager ETLs from JTS 6.0 for the 4.0.4 apps |
| 1.1.1.7 | JTS 6.0 and RTC, RQM, RDNG at 4.0.5 | Data Manager ETLs from JTS 6.0 for the 4.0.5 apps |
| 1.1.1.7 | JTS 6.0 and RTC, RQM, RDNG at 4.0.6 | Data Manager ETLs from JTS 6.0 for the 4.0.6 apps |
| 1.1.1.7 | JTS 6.0 and RTC, RQM, RDNG at 4.0.7 | Data Manager ETLs from JTS 6.0 for the 4.0.7 apps |
| 1.1.1.7 | JTS 6.0 and RTC, RQM, RDNG at 5.0 | Data Manager ETLs from JTS 6.0 for the 5.0 apps |
| 1.1.1.7 | JTS 6.0 and RTC, RQM, RDNG at 5.0.1 | Data Manager ETLs from JTS 6.0 for the 5.0.1 apps |
| 1.1.1.7 | JTS 6.0 and RTC, RQM, RDNG at 5.0.2 | Data Manager ETLs from JTS 6.0 for the 5.0.2 apps |
| 1.1.1.7 | JTS 6.0 and RTC, RQM, RDNG at 6.0 |  |

Upgrade paths exists for the following release combinations. CLM
versions in the following table refer primarily to the JTS version where
the actual CLM applications (RTC, RQM, RDNG) can be that same version or
a prior version supported by that JTS version. However, use of a prior
version application will also require usage of the appropriate Data
Manager ETL.

|                                |                                      |
|--------------------------------|--------------------------------------|
| From Release                   | To Release                           |
| No CLM / Insight 1.1 or prior  | No CLM with Insight 1.1.1.7          |
| No CLM / Insight 1.1 or prior  | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| No CLM / Insight 1.1 or prior  | CLM 6.0 with Insight 1.1.1.7         |
| No CLM / Insight 1.1.1         | No CLM with Insight 1.1.1.7          |
| No CLM / Insight 1.1.1         | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| No CLM / Insight 1.1.1         | CLM 6.0 with Insight 1.1.1.7         |
| No CLM / Insight 1.1.1.1       | No CLM with Insight 1.1.1.7          |
| No CLM / Insight 1.1.1.1       | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| No CLM / Insight 1.1.1.1       | CLM 6.0 with Insight 1.1.1.7         |
| No CLM / Insight 1.1.1.2       | No CLM with Insight 1.1.1.7          |
| No CLM / Insight 1.1.1.2       | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| No CLM / Insight 1.1.1.2       | CLM 6.0 with Insight 1.1.1.7         |
| No CLM / Insight 1.1.1.3       | No CLM with Insight 1.1.1.7          |
| No CLM / Insight 1.1.1.3       | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| No CLM / Insight 1.1.1.3       | CLM 6.0 with Insight 1.1.1.7         |
| No CLM / Insight 1.1.1.4       | No CLM with Insight 1.1.1.7          |
| No CLM / Insight 1.1.1.4       | CLM 6.0 with Insight 1.1.1.7         |
| No CLM / Insight 1.1.1.5       | No CLM with Insight 1.1.1.7          |
| No CLM / Insight 1.1.1.5       | CLM 6.0 with Insight 1.1.1.7         |
| No CLM / Insight 1.1.1.6       | CLM 6.0 with Insight 1.1.1.7         |
| No CLM / Insight 1.1.1.6       | No CLM with Insight 1.1.1.7          |
| No CLM / Insight 1.1.1.7       | CLM 6.0 with Insight 1.1.1.7         |
| CLM 3.0.1.\* / No Reporting    | CLM 3.0.1.\* with Insight 1.1.1      |
| CLM 3.0.1.\* / No Reporting    | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 3.0.1.\* / No Reporting    | CLM 6.0 with Insight 1.1.1.7         |
| CLM 3.0.1.\* / Insight 1.1     | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 3.0.1.\* / Insight 1.1     | CLM 6.0 with Insight 1.1.1.7         |
| CLM 3.0.1.\* / RRDI 1.0.2      | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 3.0.1.\* / RRDI 1.0.2      | CLM 6.0 with Insight 1.1.1.7         |
| CLM 3.0.1.\* / RRDI 2.0.0.1    | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 3.0.1.\* / RRDI 2.0.0.1    | CLM 6.0 with Insight 1.1.1.7         |
| CLM 3.0.1.\* / RRDI 2.0.\*     | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 3.0.1.\* / RRDI 2.0.\*     | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.0.\* / No Reporting    | CLM 4.0.0.\* with Insight 1.1.1      |
| CLM 4.0.0.\* / No Reporting    | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.0.\* / No Reporting    | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.0.\* / Insight 1.1.1   | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.0.\* / Insight 1.1.1   | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.0.\* / RRDI 2.0.0.1    | CLM 4.0.0.\* with Insight 1.1.1      |
| CLM 4.0.0.\* / RRDI 2.0.0.1    | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.0.\* / RRDI 2.0.0.1    | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.0.\* / RRDI 2.0.\*     | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.0.\* / RRDI 2.0.\*     | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.1.\* / No Reporting    | CLM 4.0.2 with Insight 1.1.1.1       |
| CLM 4.0.1.\* / No Reporting    | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.1.\* / No Reporting    | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.1.\* / Insight 1.1.1.1 | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.1.\* / Insight 1.1.1.1 | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.1.\* / RRDI 2.0.\*     | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.1.\* / RRDI 2.0.\*     | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.2 / No Reporting       | CLM 4.0.2 with Insight 1.1.1.1       |
| CLM 4.0.2 / No Reporting       | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.2 / No Reporting       | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.2 / Insight 1.1.1.1    | CLM 4.0.6/4.0.7 Insight 1.1.1.3      |
| CLM 4.0.2 / Insight 1.1.1.1    | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.2 / RRDI 2.0.\*        | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.2 / RRDI 2.0.\*        | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.3 / No Reporting       | CLM 4.0.4 with Insight 1.1.1.2       |
| CLM 4.0.3 / No Reporting       | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.3 / No Reporting       | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.3 / Insight 1.1.1.2    | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.3 / Insight 1.1.1.2    | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.3 / RRDI 2.0.\*        | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.3 / RRDI 2.0.\*        | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.4 / No Reporting       | CLM 4.0.4 with Insight 1.1.1.2       |
| CLM 4.0.4 / No Reporting       | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.4 / No Reporting       | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.4 / Insight 1.1.1.2    | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.4 / Insight 1.1.1.2    | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.4 / RRDI 2.0.\*        | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.4 / RRDI 2.0.\*        | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.5 / No Reporting       | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.5 / No Reporting       | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.5 / Insight 1.1.1.3    | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.5 / Insight 1.1.1.3    | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.5 / RRDI 2.0.\*        | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.5 / RRDI 2.0.\*        | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.6 / No Reporting       | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.6 / No Reporting       | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.6 / Insight 1.1.1.3    | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.6 / RRDI 2.0.6         | CLM 4.0.6/4.0.7 with Insight 1.1.1.3 |
| CLM 4.0.7 / No Reporting       | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.7 / Insight 1.1.1.3    | CLM 6.0 with Insight 1.1.1.7         |
| CLM 4.0.7 / RRDI 2.0.6         | CLM 4.0.7 with Insight 1.1.1.3       |
| CLM 5.0 / No Reporting         | CLM 6.0 with Insight 1.1.1.7         |
| CLM 5.0 / Insight 1.1.1.4      | CLM 6.0 with Insight 1.1.1.7         |
| CLM 5.0 / RRDI 5.0             | CLM 5.0 with Insight 1.1.1.4         |
| CLM 5.0 / RRDI 5.0             | CLM 6.0 with Insight 1.1.1.7         |
| CLM 5.0.1 / No Reporting       | CLM 5.0.1 with Insight 1.1.1.5       |
| CLM 5.0.1 / No Reporting       | CLM 6.0 with Insight 1.1.1.7         |
| CLM 5.0.1 / Insight 1.1.1.5    | CLM 6.0 with Insight 1.1.1.7         |
| CLM 5.0.1 / RRDI 5.0.1         | CLM 5.0.1 with Insight 1.1.1.5       |
| CLM 5.0.1 / RRDI 5.0.1         | CLM 6.0 with Insight 1.1.1.7         |
| CLM 5.0.2 / No Reporting       | CLM 5.0.2 with Insight 1.1.1.6       |
| CLM 5.0.2 / No Reporting       | CLM 6.0 with Insight 1.1.1.7         |
| CLM 5.0.2 / Insight 1.1.1.6    | CLM 6.0 with Insight 1.1.1.7         |
| CLM 5.0.2 / RRDI 5.0.2         | CLM 6.0 with Insight 1.1.1.7         |
| CLM 5.0.2 / RRDI 5.0.2         | CLM 6.0 with Insight 1.1.1.7         |
| CLM 6.0 / No Reporting         | CLM 6.0 with Insight 1.1.1.7         |

Multiple Jazz Team Server Deployment Consideration: Insight also
supports an integration with multiple Jazz Team Servers at different
versions (e.g. one JTS v4.0.3 and one JTS at v3.0.1.1). In order to
support this, the Insight version must match the highest level JTS in
your multiple-JTS environment. For example, if you have two CLM
environments, one with a JTS v4.0.3 and the other with a JTS v3.0.1.1.
Insight must support the highest version of the JTS you have, which in
this case is 4.0.3. Per our support matrix, you need Insight 1.1.1.2 to
integrate with JTS 4.0.3. In this scenario, one other important note is
that you must use the CLM 4.0.3 collateral in all of your development
tools, regardless of what prior versions you are using. The 4.0.3
collateral comes bundled with previous versions of CLM collateral. So
with the CLM 4.0.3 collateral, you would receive all the builds for
prior versions (e.g. 4.0, 3.0.1.1, etc).

##### Related topics: [Installing, Upgrading and Migrating](DeploymentInstallingUpgradingAndMigrating), [System Requirements for Collaborative Lifecycle Management 4.0.5 ](CLMSystemRequirements405) [related-topics-installing-upgrading-and-migrating-system-requirements-for-collaborative-lifecycle-management-4.0.5]

##### Additional contributors: Main.MichaelFox, Main.RosaNaranjo [additional-contributors-main.michaelfox-main.rosanaranjo]
