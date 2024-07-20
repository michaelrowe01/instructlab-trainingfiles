META:TOPICINFO{author="sbeard" date="1431610562" format="1.1"
version="1.13"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# System Requirements for IBM Rational Systems and Software Engineering (SSE) 5.0, 5.0.1, and 5.0.2 [system-requirements-for-ibm-rational-systems-and-software-engineering-sse-5.0-5.0.1-and-5.0.2]

DKGRAY ***SSE include Rational DOORS and DOORS Web Access, Rational
DOORS Next Generation, Rational Team Concert, Rational Quality Manager,
Rational Rhapsody, Rational Rhapsody Design Manager, Rational
Engineering Lifecycle Manager*** Build basis: SSE 5.0, 5.0.1, 5.0.2
ENDCOLOR

TOC{title="Page contents"}

For a short list of track changes to this article please see the bottom
of this article. For prior release requirements please see the specific
articles for each version listed below:

-   The system requirements for SSE v4.0.3 were published in [this
    article](https://jazz.net/wiki/bin/view/Deployment/SSESystemRequirements403).
-   The system requirements for SSE v4.0.5 and v4.0.6 are published in
    [this
    article](https://jazz.net/wiki/bin/view/Deployment/SSESystemRequirements405).

CLM 5.0, 5.0.1, and 5.0.2 system requirements are published in [this
article](https://jazz.net/wiki/bin/view/Deployment/CLMSystemRequirements50).

-   This is the list of system requirements for \*Rational systems and
    software engineering (SSE) 5.0, 5.0.1, and 5.0.2 incorporating:

| Product | SSE 5.0 Version | SSE 5.0.1 Version | SSE 5.0.2 Version |
|:---|:---|:---|:---|
| Rational DOORS and DOORS Web Access (DWA) | 9.6 | 9.6.0.1 | 9.6.1 |
| Rational DOORS Next Generation (DNG) | 5.0 | 5.0.1 | 5.0.2 |
| Rational Team Concert (RTC) | 5.0 | 5.0.1 | 5.0.2 |
| Rational Rhapsody | 8.1 | 8.1.1 | 8.1.2 |
| Rational Rhapsody Design Manager | 5.0 | 5.0.1 | 5.0.2 |
| Rational Engineering Lifecycle Manager (RELM) | 5.0 | 5.0.1 | 5.0.2 |

\* ***Please Note:*** From SSE 5.0 onward, Rational Requirements
Composer (RRC) has been renamed to Rational DOORS Next Generation
(RDNG).

The system requirements are broken down into various components. These
are the most commonly supported platforms and middleware, for additional
options please refer to the individual product system requirements. For
recommended deployment topologies please refer to:
<https://jazz.net/wiki/bin/view/Deployment/RecommendedSSEDeploymentTopologies>

RED **Please Note: From SSE 5.0 onwards, RDNG's data is no longer stored
in the JTS database. Rather, RDNG's has it's own RM database. Because of
this change in where the data is stored, the steps for the upgrade
procedure significantly changed. Compared to the procedure to upgrade to
version 4.x, the procedure to upgrade to version 5.0 or later from 4.x
has more steps. Please see [Migrating the RM application to V5 from
V4.x: Tips, common problems, and
workarounds](RM4to5MigrationTipsTricksProblemsAndSolutions) and [Running
the RM upgrade script for version
5.0](RunningTheRMUpgradeScriptForVersion50).** ENDCOLOR

RED **Please Note: Starting in RTC 5.0, you can choose to migrate data
from an older version of the product to the latest product version while
the production server is still online. This migration method is called
pre-upgrade online migration. Before implementing an online migration,
determine whether offline or online migration is warranted for your
repository by running the migration estimation command and then checking
the [Rational Team Concert online migration test
matrix](RationalTeamConcertOnlineMigrationTestMatrix) for guidance on
the results. If online migration is recommended for your repository,
follow the detailed instructions in the [Collaborative Lifecycle
Management 5.0 Knowledge Center, Interactive upgrade
guide](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.0/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html),
[Collaborative Lifecycle Management 5.0.1 Knowledge Center, Interactive
upgrade
guide](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.1/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html)
and [Collaborative Lifecycle Management 5.0.2 Knowledge Center,
Interactive upgrade
guide](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.2/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html)
respectively.** ENDCOLOR

RED **Please Note: When using an Oracle database for RTC, workspaces and
streams become disconnected from internal configuration information
during migration from RTC 4.x to RTC 5.0 or later, causing some of the
SCM functionality to become unusable. Please see the
[NullPointerExceptions occur with Oracle DB after upgrade to Rational
Team Concert
5.0](http://www-01.ibm.com/support/docview.wss?uid=swg21676229) Technote
for more information.** ENDCOLOR

RED **Please Note: Starting in SSE 5.0.2, Lifecycle Project
Administration (LPA) is now a component of the Jazz Team Server (JTS).
Prior to 5.0.2, it was a separate application. Because of this change,
some steps of the upgrade procedure have changed. Please see [Migrating
the LPA application from 4.0.x, 5.0 or 5.0.1 to 5.0.2 or
higher](https://jazz.net/wiki/bin/view/Main/LifecycleProjectAdmin#Migrating_the_LPA_application_to)**
ENDCOLOR

## A. Server Requirements

### A1. Server Host Operating Systems

#### A1.1 Server Support

The operating systems below may be used to host SSE applications.

| Server Operating System | Server Version | Notes |
|:---|:---|:---|
| **Red Hat Enterprise Linux (RHEL) Server 6** and future OS fixpacks | 64 bit |  |
| **SUSE Linux Enterprise Server (SLES) 11** and future OS fixpacks | 64 bit |  |
| **Windows Server 2008 R2 Enterprise Edition and Standard Edition** and future OS fixpacks | 64 bit | BLUE\* This platform will EOS in Jan 2015, Please prepare to upgrade to 2012 prior to that date. [Windows Server Lifecycle](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PNα=Windows+Server&Filter=FilterNO) |
| **Windows Server 2012 Datacenter and Standard Editions** and future OS fixpacks | 64 bit |  |
| **Windows Server 2012 R2 Standard and Datacenter Edition** and future OS fixpacks | 64 bit | BLUE \* Windows Server 2012 R2 Datacenter and Standard Editions New for 5.0.1 and 5.0.2ENDCOLOR \* WAS supports Windows Sever 2012 R2 starting from version 8.5.5 \* DB2 supports Windows Sever 2012 R2 starting from version 10.5.0.4 |

##### Server Host Operating System Notes

\* *"and future OS fixpacks" includes Service Releases (SR's) and
Updates (RHEL). Fix pack is IBM terminology for a minor release that
includes fixes (vs. features).*

### A2. Application Servers ---++++ A2.1 Application Server Support

The following application servers can be used to host SSE applications
(non-clustered):

| Application Servers | Server Version | Notes |
|:---|:---|:---|
| **WebSphere Application Server v8.5 x86-64** and future fixpacks | Supported | Please see "Bundling" Note below.Please also see Note below for BIRT issue. |
| **WebSphere Application Server Network Deployment v8.5** and future fixpacks | Supported | Non-clustered Only |
| **WebSphere Application Server v8.5.5 x86-64** and future fixpacks | Supported | BLUE \* New Bundle for v5.0ENDCOLOR \* Excludes the Liberty profile configuration option |
| **WebSphere Application Server Network Deployment v8.5.5** and future fixpacks | Supported | *\* SSE supports WAS ND but **not** for high availability clustering \* Excludes the Liberty profile configuration option* |
| Apache Tomcat 7.0.52 and future fixpacks | Supported | BLUE \* Tomcat 7.0.52 is bundled with CLM 5.0 ENDCOLOR \* Tomcat is not supported on IBM i |
| **Apache Tomcat 7.0.54** and future fixpacks | Supported | BLUE \* New Tomcat 7.0.54 is bundled with CLM 5.0.1 and 5.0.2 ENDCOLOR \* Tomcat is not supported on IBM i |

##### Application Server Notes

-   Bundling: WAS 8.5.5 and DB2 10.5 bundles are only available on
    Passport Advantage and in the CLM Media (not on Jazz.net). Customers
    upgrading from CLM 4.0.x are entitled to continue using WAS 8.0.x
    and 8.5 as long as CLM supports those versions.
-   WebSphere Application Server support for SSE is 64-bit only to align
    with 64-bit server platforms.
-   DOORS Web Access only supports Tomcat AppServer, no support for
    WebSphere Application Server is available
-   There is a known issue with BIRT reports running WAS v8.0.0.5 and
    before and v8.5.0.1 and before please see this [Tech
    Note](http://www-01.ibm.com/support/docview.wss?uid=swg21616615) for
    WAS patch. BLUEThis issue applies only to WAS 8.x and 8.5.x only. It
    is fixed WAS 8.5.5 ENDCOLOR

### A3. Databases

The following databases can be used to host SSE applications:

| Database | Server | Notes |
|:---|:---|:---|
| **IBM Derby SDK 10.8.1.2** and future fixpacks | 64 bit | For Evaluation purposes only - for small teams of 10 users or less)CLM bundles Derby |
| **IBM Derby SDK 10.10** and future fixpacks | 64 bit | BLUE \* CLM bundles Derby 10.10 in 5.0.1 and 5.0.2ENDCOLOR \* For Evaluation purposes only, not supported by RRDI (for small teams of 10 users or less) |
| **IBM DB2 Enterprise Server Edition v10.5** and future fixpacks | 64 bit | BLUE \* New version and bundled for v5.0 |
| **IBM DB2 Workgroup Server Edition v10.5** and future fixpacks | 64 bit | BLUE \* New version and bundled for v5.0 ENDCOLOR \* DB2 10.5 WSE will be bundled with the CLM 5.0 media |
| **IBM DB2 Enterprise Server Edition v10.1** and future fixpacks | 64 bit |  |
| **IBM DB2 Workgroup Server Edition v10.1** and future fixpacks | 64 bit |  |
| **IBM DB2 Enterprise Server Edition v10.5** and future fixpacks | 64 bit | BLUE \* New for 5.0 and bundled with CLM v5.0ENDCOLOR |
| **IBM DB2 Workgroup Server Edition v10.5** and future fixpacks | 64 bit | BLUE \* New for 5.0 |
| **Microsoft SQL Server Enterprise Edition 2012** and future fixpacks | 64 bit | BLUENew version for SSE v5.0ENDCOLOR |
| **Microsoft SQL Server Standard Edition 2012** and future fixpacks | 64 bit | BLUENew version for SSE v5.0ENDCOLOR |
| **Microsoft SQL Server Enterprise Edition 2014** and future fixpacks | 64 bit | BLUE\* New version for SSE 5.0.2 onlyENDCOLOR |
| **Microsoft SQL Server Standard Edition 2014** and future fixpacks | 64 bit | BLUE\* New version for SSE 5.0.2 onlyENDCOLOR |
| **Oracle Database 11g Standard Edition Release 2** and future fixpacks | 64 bit |  |

##### Database Support Notes

-   Database support is 64-bit only to align with 64-bit server
    platforms.
-   WAS and DB2 bundles are only available on Passport Advantage and in
    the CLM Media (not on Jazz.net). Customers upgrading from CLM 3.0.1
    and 4.0.X are entitled to continue using DB2 10.1 as long as SSE
    supports that version.

### A4. Java Runtime Environment (Server)

| JRE | Notes |
|:---|---:|
| **IBM Java SDK 6.0.15 iFix1** and future fixpacks | BLUE \* New version for SSE v5.0ENDCOLOR \* This is the bundled version of Java for the CLM Server |

### A5. Identity Management

-   Apache Directory Server 1.5.5
-   IBM Tivoli Directory Server 6.3
-   Microsoft Active Directory 2008 R2 BLUEPlease note this version will
    EOS in January 2015 please plan to upgrade before that time.ENDCOLOR
-   Microsoft Active Directory 2012 BLUENew for v5.0.ENDCOLOR

### A6. Installation Manager

-   IBM Installation Manager 1.7.3 BLUENew for v5.0.1ENDCOLOR
-   IBM Installation Manager 1.8 BLUENew version for v5.0.2ENDCOLOR and
    bundled with CLM media.

### A7. License Server

\* Rational License Server 8.1.4 BLUENew for v5.0ENDCOLOR and bundled
with CLM media.

### A8. HTTP Reverse Proxy Support

-   Apache Server 2.2.19 on RHEL and SLES \[Non-secure Only (no HTTPS)\]
-   IBM HTTP Server 8.0.0.6 and future fixpacks
-   IBM HTTP Server 8.5.0.2 and future fixpacks
-   IBM HTTP Server 8.5.5 and future fixpacks
-   Squid 3.3.3 for caching (see [Using content caching proxies for Jazz
    Source
    Control](https://jazz.net/wiki/bin/view/Deployment/ContentCachingProxyJazzSCM)).

## B. **Client Requirements**

-   **Reminder: The platforms listed below are the starting point for
    SSE support and unless otherwise indicated support includes this
    level and all future OS fixpacks. For RedHat Updates are equivalent
    to fix packs**

### B1. Client Operating Systems

| Client Operating System | DOORS Client | Rhapsody | Web Clients (Browsers) | Notes |
|:---|:---|:---|:---|:---|
| **Red Hat Enterprise Linux (RHEL) Client 6 x86-32, x86-64** and future OS fixpacks | Windows Only | Supported | Supported | Please see Client OS Notes below |
| **Red Hat Enterprise Linux (RHEL) Workstation 6 x86-32, x86-64** and future OS fixpacks | Windows Only | none | Supported | Please see Client OS Notes below |
| **SUSE Linux Enterprise Desktop (SLED) 11.0 x86-32, x86-64** and future OS fixpacks | Windows Only | Supported | Supported | Please see Client OS Notes below |
| **Windows 7 Enterprise, Professional and Ultimate Editions** and future OS fixpacks | Supported | Supported | Supported |  |
| **Windows 8.1 Enterprise, Professional and Ultimate Editions** and future OS fixpacks | Supported | Supported | Supported | BLUE \* New version for v5.0ENDCOLOR \* Does not include Metro Support \* Supported for RTC Eclipse 4.2.2 client and higher |

#### Client Operating System Notes

\* If you are running the Eclipse client on Linux please ensure that you
have a compatible xulrunner or webkitgtk installed and configured on
your system. Failure to do so can result in various issues including
failure to start. See [Article](https://jazz.net/library/article/952)
for additional details and instructions. \* Smart Card Support for ALL
CLM Products (Windows Only) \* Supported only with IBM Rational Rhapsody
Developer for C++, C, and Java. IBM Rational Rhapsody Developer for Ada
and IBM Rational Rhapsody Developer supported only with Apex environment

### B2. Browsers

\| **Browser** \| \*Supported \| **Notes** \|

|  |  |  |
|----|----|----|
| **Firefox 24 ESR** and future fixpacks | Supported | \* See note below for mixed http/https content and self-signed certificates \* See note below for RM Graphical Editors |
| **Firefox 31 ESR** and future fixpacks | Supported | BLUE \* Firefox 31 ESR for 5.0.1 and 5.0.2ENDCOLOR \* See note below for mixed http/https content and self-signed certificates \* See note below for RM Graphical Editors |
| **Google Chrome 34** | Supported | Except for DOORS Web Access \* See note below for mixed http/https content and self-signed certificates \* See note below for RM Graphical Editors |
| **Internet Explorer 9** and future fixpacks | Supported |  |
| **Internet Explorer 11 for the Desktop** and future fixpacks | Supported | BLUE New version for v5.0ENDCOLOR \* See note below for mixed http/https content and self-signed certificates |

#### Browser Support Notes

-    BLUEPlease see these tech note articles for [mixed http/https
    content](http://www-01.ibm.com/support/docview.wss?uid=swg21653966)
    and [self-signed
    certificates](http://www-01.ibm.com/support/docview.wss?uid=swg21654984)
    which may result in content not being shown as expected. ENDCOLOR
-   The RDNG Graphical Editor is supported in 32-bit mode using Internet
    Explorer and Firefox on Windows (Only).
-   Macromedia Flash Player 10,11\* and future releases, mods and
    fixpacks is supported for graphical view in Work Item Statistics
    dashboard viewlet

### B3. Java SDK

\* \| IBM Java SDK 6.0.15 iFix1\* and future fixpacks \| BLUE \*New
version for v5.0ENDCOLOR\| \* \| IBM Java SDK 6.0.16\* and future
fixpacks \| BLUE \*New version for v5.0.1ENDCOLOR\| \* \| IBM Java SDK
6.0.16 iFix 1 (6.0.16.1)\* and future fixpacks \| BLUE \*New version for
v5.0.2ENDCOLOR\|

#### Java Runtime Notes

\*FYI - the DOORS Client is based on C++ (and DXL) not Java based.

## C. Related Articles

-   [Collaborative Lifecycle Management 2012 Sizing
    Guide](SizingReportCLM2012)
-   [Rational Requirements Composer 4.0 performance and tuning
    guide](https://jazz.net/library/article/844)
-   [IBM Rational Doors Next Generation 4.0.1 Performance
    Report](https://jazz.net/library/article/1216)
-   [Performance comparison: Rational Requirements Composer versions 4.0
    and 4.0.1](https://jazz.net/library/article/1232)
-   [Rational Team Concert 4.x performance tuning guide for
    z/OS](https://jazz.net/library/article/817)

## D. Summary of Updates by Release

### D1. Additions

-   New for v5.0:
    -   Windows 8.1 (Desktop)
    -   Internet Explorer 11 - Compatibility Mode Only
    -   WAS 8.5.5 (new bundle)
    -   DB2 10.5 (and new bundle)
    -   Java 6 SR15 FP1
    -   IES 4.3.2 (RTC Client support)

\* New for SSE 5.0.1

-   Windows Server 2012 R2 Datacenter and Standard Editions
-   Firefox 31 ESR
-   Tomcat 7.0.54 (Tomcat 7.0.52 is bundled with CLM 5.0)
-   IBM Java SDK 6.0.16

\* New for SSE 5.0.2

-   Microsoft SQL Server Enterprise Edition 2014
-   Microsoft SQL Server Standard Edition 2014
-   IBM Java SDK 6.0.16 iFix 1 (6.0.16.1)
-   IBM Installation Manager 1.8

\* You will also see notes in the article above about intentions to drop
these platforms:

-   Solaris - no new customers for 5.0, this platform will be dropped in
    a future release.
-   Windows Server 2008 R2 - this platform goes EOS in January 2015
    please make plans to upgrade to Windows Server 2012 before that
    time.

For additional platform plans, pressures and drops information please
see the [CLM Platform Plans and Pressures
Dashboard](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.dashboard.viewDashboard&tab=_79).
