META:TOPICINFO{author="syeshin" date="1469821681" format="1.1"
version="1.44"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# System Requirements for IBM Rational Collaborative Lifecycle Management (CLM) 5.0, 5.0.1 and 5.0.2 [system-requirements-for-ibm-rational-collaborative-lifecycle-management-clm-5.0-5.0.1-and-5.0.2]

DKGRAY ***CLM includes the Rational Team Concert, Rational Quality
Manager, and Rational DOORS Next Generation products*** Build basis: CLM
5.0, 5.0.1 and 5.0.2

TOC{title="Page contents"}

For prior release requirements please see the specific articles for each
version listed below:

-   For the CLM 2011 (3.0.1.x) system requirements please see [this
    article](http://jazz.net/library/article/632).
-   The system requirements for CLM 2012 (v4.0) were published in [this
    article](https://jazz.net/library/article/811).
-   The system requirements for v4.0.1 and v4.0.2 are published in [this
    article](https://jazz.net/library/article/1109).
-   The system requirements for v4.0.3 and v4.0.4 are published in [this
    article](https://jazz.net/wiki/bin/view/Deployment/CLMSystemRequirements403).
-   The system requirements for v4.0.5, 4.0.6 and 4.0.7 are published in
    [this
    article](https://jazz.net/wiki/bin/view/Deployment/CLMSystemRequirements405406).

For platform pressures (enhancements and more) please see the [CLM
Platform Plans and Pressures
Dashboard](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.dashboard.viewDashboard&tab=_79).

This is the list of system requirements for **Collaborative Lifecycle
Management (CLM)** 5.0, 5.0.1 and 5.0.2 incorporating:

-   The **Jazz Foundation (JAF)** technology project.
-   The **Rational Team Concert (RTC)**, **Rational Quality Manager
    (RQM)** and **Rational DOORS Next Generation (RDNG)** products.
-   **Rational Reporting for Development Intelligence (RRDI)** for
    customized reporting. RED Before upgrading, please see this
    additional article [Version Compatibility Matrix for RRDI, CLM, and
    Rational Insight](VersionCompatibilityCLMRRDIAndInsight). ENDCOLOR
-   The system requirements are broken down into various components
    including the server-based CLM applications that are deployed on one
    or more servers and various optional tools and clients.
-   ***Please Note:*** From CLM 5.0 onward, Rational Requirements
    Composer (RRC) has been renamed to Rational DOORS Next Generation
    (RDNG).

RED **Please Note: From CLM 5.0 onwards, RDNG's data is no longer stored
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

RED **Please Note: Starting in CLM 5.0.2, Lifecycle Project
Administration (LPA) is now a component of the Jazz Team Server (JTS).
Prior to 5.0.2, it was a separate application. Because of this change,
some steps of the upgrade procedure have changed. Please see [Migrating
the LPA application from 4.0.x, 5.0 or 5.0.1 to 5.0.2 or
higher](https://jazz.net/wiki/bin/view/Main/LifecycleProjectAdmin#Migrating_the_LPA_application_to)**
ENDCOLOR

## A. Server Requirements

### A1. Server Operating Systems

The operating systems below may be used to host CLM applications:

| Server Operating System | CLM Server Support | RRDI Support | Notes |
|:---|:---|:---|:---|
| **AIX 6.1 POWER System - Big Endian** and future OS fixpacks | 64 bit | 64 bit | *\* See RDNG Converter note below* \* RRDI support is for the Cognos-based reporting tools only |
| **AIX 7.1 POWER System - Big Endian** and future OS fixpacks | 64 bit | 64 bit | *\* See RDNG Converter note below* \* RRDI support is for the Cognos-based reporting tools only |
| **IBM i 6.1 POWER System - Big Endian** and future OS fixpacks | 64 bit | 64 bit | *\* For RRDI, Only the Data Warehouse is supported on IBM i (Cognos does not support this platform) \* See RDNG Converter note below \* For the latest IBM i Group PTFs, go to [Preventive Service Planning](http://www-912.ibm.com/s_dir/sline003.nsf/GroupPTFs?OpenView&view=GroupPTFs) \* See RDNG Document Preview note below* |
| **IBM i 7.1 POWER System - Big Endian** and future OS fixpacks | 64 bit | 64 bit | *\* For RRDI, Only the Data Warehouse is supported on IBM i (Cognos does not support this platform) \* See RDNG Converter note below \* For the latest IBM i Group PTFs, go to [Preventive Service Planning](http://www-912.ibm.com/s_dir/sline003.nsf/GroupPTFs?OpenView&view=GroupPTFs) \* See RDNG Document Preview note below* |
| **IBM i 7.2 POWER System - Big Endian** and future OS fixpacks | 64 bit | 64 bit | BLUE \* New version for CLM 5.0.2 onlyENDCOLOR *\* For RRDI, Only the Data Warehouse is supported on IBM i (Cognos does not support this platform) \* See RDNG Converter note below \* For the latest IBM i Group PTFs, go to [Preventive Service Planning](http://www-912.ibm.com/s_dir/sline003.nsf/GroupPTFs?OpenView&view=GroupPTFs) \* See RDNG Document Preview note below* |
| **IBM z/OS System z v1.12** and future OS fixpacks | 64 bit | 64 bit | *\* z/OS is supported for RTC, RQM, RDNG Only. RRDI support for z/OS is for the Cognos Content Store and Data Warehouse Only (not the Report Server) \* See RDNG Converter note below \* See additional REXX support required for Rational Team Concert promotion and deployment below \* See note on zAAP or run zAAP on zIIP below \* See RDNG Document Preview note below* |
| **IBM z/OS System z v1.13** and future OS fixpacks | 64 bit | 64 bit | *\* z/OS is supported for RTC, RQM, RDNG Only. RRDI support for z/OS is for the Cognos Content Store and Data Warehouse Only (not the Report Server) \* See RDNG Converter note below \* See additional REXX support required for Rational Team Concert promotion and deployment below \* See note on zAAP or run zAAP on zIIP below \* See RDNG Document Preview note below* |
| **IBM z/OS System z v2.1** and future OS fixpacks | 64 bit | 64 bit | BLUENew version for CLM 5.0ENDCOLOR\* z/OS is supported for RTC, RQM, RDNG Only. RRDI support for z/OS is for the Cognos Content Store and Data Warehouse Only (not the Report Server) \* See RDNG Converter note below \* See additional REXX support required for Rational Team Concert promotion and deployment below \* See note on zAAP or run zAAP on zIIP below \* See RDNG Document Preview note below |
| **Red Hat Enterprise Linux (RHEL) Server 6 x86-64** and future OS fixpacks | 64 bit | 64 bit |  |
| **Red Hat Enterprise Linux (RHEL) Server 7 x86-64** and future OS fixpacks | 64 bit | Not Supported | BLUE \* RHEL 7 x86-64 New for 5.0.1 and 5.0.2ENDCOLOR \* RRDI is also not suppporting RHEL 7 (it has not yet been adopted by Cognos) |
| **Red Hat Enterprise Linux (RHEL) Server 6 POWER System - Big Endian** and future OS fixpacks | 64 bit | Not Supported | *\* RRDI does not support POWER platforms \* See RDNG Document Preview note below* |
| **Red Hat Enterprise Linux (RHEL) Server 7 POWER System - Big Endian** and future OS fixpacks | 64 bit | Not Supported | BLUE \* New version for CLM 5.0.2 onlyENDCOLOR \* RHEL 7 is only supported for Linux for Power from CLM 5.0.2 due to a critical defect \* RRDI does not support POWER platforms \* See RDNG Document Preview note below |
| **Red Hat Enterprise Linux (RHEL) Server 6 System z** and future OS fixpacks | 64 bit | Not Supported | \* RRDI does not support RHEL only SLES \* See RDNG Document Preview note below |
| **Red Hat Enterprise Linux (RHEL) Server 7 System z** and future OS fixpacks | 64 bit | Not Supported | BLUE \* New version for CLM 5.0.2 onlyENDCOLOR \* RHEL 7 is only supported for System Z from CLM 5.0.2 due to a critical defect \* RRDI does not support RHEL only SLES \* See RDNG Document Preview note below |
| **Solaris 10 SPARC** and future OS fixpacks | 64 bit | Not Supported | \* Solaris SPARC Server is supported for RTC, RQM and RDNG only. RRDI does not support Solaris \* See RDNG Converter note belowBLUE \* No new customers on Solaris, this platform will be dropped in a future CLM releaseENDCOLOR \* See RDNG Document Preview note below |
| **Solaris 11 SPARC** and future OS fixpacks | 64 bit | Not Supported | \* Solaris SPARC Server is supported for RTC, RQM and RDNG only. RRDI does not support Solaris \* See RDNG Converter note belowBLUE \* No new customers on Solaris, this platform will be dropped in a future CLM releaseENDCOLOR \* See RDNG Document Preview note below |
| **SUSE Linux Enterprise Server (SLES) 11 x86-64** and future OS fixpacks | 64 bit | 64 bit |  |
| **SUSE Linux Enterprise Server (SLES) 11 POWER System - Big Endian** and future OS fixpacks | 64 bit | Not Supported | *\* RRDI does not support POWER platforms \* See RDNG Converter note below \* See RDNG Document Preview note below* |
| **SUSE Linux Enterprise Server (SLES) 11 System z** and future OS fixpacks | 64 bit | 64 bit | \* *See RDNG Document Preview note below* |
| **Windows Server 2008 R2 Enterprise and Standard Editions** and future OS fixpacks | 64 bit | 64 bit | BLUE\* This platform will EOS in Jan 2015, Please prepare to upgrade to 2012 prior to that date. [Windows Server Lifecycle](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PNα=Windows+Server&Filter=FilterNO) |
| **Windows Server 2012 Datacenter and Standard Editions** and future OS fixpacks | 64 bit | 64 bit |  |
| **Windows Server 2012 R2 Datacenter and Standard Editions** and future OS fixpacks | 64 bit | 64 bit | BLUE \* Windows Server 2012 R2 Datacenter and Standard Editions New for 5.0.1 and 5.0.2ENDCOLOR \* WAS supports Windows Sever 2012 R2 starting from version 8.5.5 \* DB2 supports Windows Sever 2012 R2 starting from version 10.5.0.4 |

##### Server Operating System Notes

-   *Host Operating Systems are supported on x86-64, POWER, z/OS and
    SPARC hardware. Itanium is not supported.*
-   *CLM and RRDI require 64 bit server OS to host CLM applications.
    32-bit servers are not supported except for small-scale evaluation
    or demonstration purposes.*
-   *The RDNG Converter application will ***not*** run on AIX, IBM i,
    Linux for Power, Solaris or z/OS systems. The server-side
    converter.war, needed to view graphical artifacts, must be deployed
    on a supported Windows, x86 Linux or zLinux platform. If your RDNG
    installation is on a platform not currently supported by the
    converter application, this document describes the delegated
    converter configuration option: [RM Converter Application
    Configuration and Troubleshooting
    Guide](https://jazz.net/library/article/1089).*
-   For the PTFs that need to be installed on enterprise platforms,
    depending on the components you install with IBM Rational
    Collaborative Lifecycle Management (CLM), see *[Recommended Fixes
    for the Rational Collaborative Lifecycle Management applications on
    z/OS and IBM
    i](http://www.ibm.com/support/docview.wss?uid=swg27043083)*
-   *For IBMi PTF's are required. For the latest IBM i Group PTFs, go to
    <http://www-912.ibm.com/s_dir/sline003.nsf/GroupPTFs?OpenView&view=GroupPTFs>.*
-   *IBM z/OS System z 1.10 and 1.9 are only supported if you have paid
    for an IBM Lifecycle Extension for z/OS as mentioned on
    <http://www.ibm.com/systems/z/os/zos/support/zos_eos_dates.html>.*
-   *Rational Team Concert promotion and deployment support for z/OS
    require the REXX runtime or REXX alternate libraries
    (REXX.\***.SEAGLPA, or REXX.\***.SEAGALT). If you do not have either
    the REXX Library or the REXX Alternate Library installed, you can
    install the REXX Alternate Library to fulfill the REXX Library
    requirement. The REXX Alternate Library is shipped as part of the
    z/OS operating system beginning with release 1.9. The Alternate
    Library is also available as a free download from
    <http://www.ibm.com/support/entry/portal/>.*
-   *"and future OS fixpacks" includes Service Releases (SR's) and
    Updates (RHEL). Fix pack is IBM terminology for a minor release that
    includes fixes (vs. features).*
-   When running any of the following components on z/OS it is highly
    recommended to have a zAAP or run zAAP on zIIP: Rational Team
    Concert Build System toolkit, Rational Build Agent, Rational Team
    Concert ISPF daemon, CLM Server (or any of the capabilities). When
    using DB2 for z/OS as the database it is highly recommended to have
    a zIIP to allow the offloading of the JDBC processing. Follow this
    link for more information about the [System z Application Assist
    Processor
    (zAAP)](http://www-03.ibm.com/systems/z/hardware/features/zaap/index.html).
    Follow this link for more information about the [zAAP on zIIP
    Capability](http://www-03.ibm.com/systems/z/hardware/features/ziip/capability.html).
    Follow this link for more information about the [IBM System z
    Integrated Information Processor
    (zIIP)](http://www-03.ibm.com/systems/z/hardware/features/ziip/index.html).
-   Server Operating System Pressures - [CLM Platform Plans and
    Pressures
    Dashboard](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.dashboard.viewDashboard&tab=_79).
-   The RDNG Document Preview feature is not supported on: IBM i; IBM
    z/OS on System z; RHEL on POWER System or System z; SUSE on POWER
    System or System z; or Solaris operating systems. On those operating
    systems, image generation is not supported, so files will behave the
    same way they did in pre-CLM 5.0.2 releases. For more details, see:
    [Uploaded file
    previews](https://jazz.net/wiki/bin/view/Main/UploadedFilePreviews).
-   The Data Collection Component and Report Builder components of RRDI
    do not support AIX.

### A2. Server Virtualization

For the supported Server Operating Systems above, virtualization is now
supported using any of the IBM SWG supported hypervisors listed in the
[Server Virtualization Policy for IBM
Software](http://www-01.ibm.com/software/support/virtualization_policy.html).
Notes:

-   Virtualization is supported for the Application layer (Server) Only.
    CLM does not currently support virtualization for the client(s).
-   Please check that the system requirements or release notes of the
    respective hypervisor (edition and version) supports the host
    operating system (edition and version) you plan to use for deploying
    the CLM application(s).

### A3. Memory Requirements

#### CLM Application Server Memory Requirements

-   For CLM 5.0 and later you need a 64-bit operating system and a
    minimum of 4 GB of server memory allocated to the Java virtual
    machine running the Jazz Team Server and all three applications
    (Change and Configuration Management, Quality Management,
    Requirements Management) on one server for small deployments. Larger
    deployments or loads may require significantly more memory.
-   The Java virtual machine max heap memory setting is configured to
    -Xmx4000M for 64-bit platforms and -Xmx1200M for 32-bit platforms
    (for small-scale evaluation or demonstration purposes only). Note
    that the Java virtual machine heap size should only represent a
    fraction of the physical memory (RAM) of the server.
-   For 64-bit deployments where less memory is available, it is
    possible - although strongly discouraged - to configure the Java
    virtual machine memory size to a lower setting (e.g. -Xmx1200M to
    match the 32-bit setup) - be aware that it may results in memory
    outages and/or performance degradation. For the Tomcat installation,
    the server.startup script file to edit is located under
    JazzInstallDir/server/, and controlled by the line: set
    JAVA_OPTS=JAVA_OPTS -Xmx4000M. For a WebSphere Application Server
    installation, please consult the WebSphere Administrative Console,
    and modify Servers\>Application Servers\>server1\>Java and Process
    Management\>Process Definition\>Java Virtual Machine\>Maximum Heap
    Size.
-   Memory requirements can be reduced by running a subset of
    applications such as just CCM to support RTC-only functionality.
    Additionally if applications and/or the Jazz Team Server are running
    on different machines, memory requirements for specific machines may
    be reduced.

#### RRDI Server Memory Requirements

-   8 GB RAM. More memory generally improves performance; required
    memory depends on the number of concurrent users, amount of data
    being requested, and the size of the database. Optimum swap space is
    double the physical memory.

### A4. Network Infrastructure

-   IPv6
-   IPv4

### A5. Application Servers The following application servers can be used to host CLM applications:

| Application Servers | CLM Server | RRDI | Notes |
|:---|:---|:---|:---|
| **Apache Tomcat 7.0.52** and future fixpacks | Supported | Supported | BLUE \* Tomcat 7.0.52 is bundled with CLM 5.0 only ENDCOLOR \* Tomcat is not supported on IBM i \* Tomcat is not supported for the Cognos-based report server in RRDI |
| **Apache Tomcat 7.0.54** and future fixpacks | Supported | Supported | BLUE \* New Tomcat 7.0.54 is bundled with CLM 5.0.1 and 5.0.2 ENDCOLOR \* Tomcat is not supported on IBM i \* Tomcat is not supported for the Cognos-based report server in RRDI |
| **WebSphere Application Server Base v8.0.0.6 x86-64** and future fixpacks | Supported | Supported | *\* Excludes the Liberty profile configuration option \* See note below for BIRT issue* |
| **WebSphere Application Server Network Deployment v8.0.0.6** and future fixpacks | Supported | Supported | *\* CLM supports WAS ND but **not** for high availability clustering \* Excludes the Liberty profile configuration option \* See note below for BIRT issue* |
| **WebSphere Application Server for z/OS v8.0.0.6** and future fixpacks | Supported | Not Supported | *\* Excludes the Liberty profile configuration option \* See note below for BIRT issue \* See bundling notes below* |
| **WebSphere Application Server Base v8.5.0.2 x86-64** and future fixpacks | Supported | Supported | *\* Excludes the Liberty profile configuration option \* See note below for BIRT issue* |
| **WebSphere Application Server Network Deployment v8.5.0.2** and future fixpacks | Supported | Supported | *\* CLM supports WAS ND but **not** for high availability clustering \* Excludes the Liberty profile configuration option \* See note below for BIRT issue* |
| **WebSphere Application Server for z/OS v8.5.0.2** and future fixpacks | Supported | Not Supported | *\* Excludes the Liberty profile configuration option \* See note below for BIRT issue* |
| **WebSphere Application Server Base v8.5.5 x86-64** and future fixpacks | Supported | Supported | BLUE \* New Bundle for CLM 5.0ENDCOLOR \* Excludes the Liberty profile configuration option |
| **WebSphere Application Server Network Deployment v8.5.5** and future fixpacks | Supported | Supported | *\* CLM supports WAS ND but **not** for high availability clustering \* Excludes the Liberty profile configuration option* |
| **WebSphere Application Server for z/OS v8.5.5 - Liberty Profile** and future fixpacks | Supported | Not Supported | BLUE \* New for CLM 5.0 - Websphere Liberty Profile support for z/OS onlyENDCOLOR |

##### Application Server Notes

-   WebSphere Application Server support for CLM and RRDI is 64-bit only
    to align with 64-bit server platforms.
-   Bundling: WAS 8.5.5 and DB2 10.5 bundles are only available on
    Passport Advantage and in the CLM Media (not on Jazz.net). Customers
    upgrading from CLM 4.0.x are entitled to continue using WAS 8.0.x
    and 8.5 as long as CLM supports those versions.
-   There is a known issue with BIRT reports running WAS v8.0.0.5 and
    before and v8.5.0.1 and before please see this [Tech
    Note](http://www-01.ibm.com/support/docview.wss?uid=swg21616615) for
    WAS patch. BLUEThis issue applies only to WAS 8.x and 8.5.x only. It
    is fixed WAS 8.5.5 ENDCOLOR

### A6. Databases

The following databases can be used to host CLM applications:

| Database | CLM Server | RRDI | Notes |
|:---|:---|:---|:---|
| **IBM Derby SDK 10.8** and future fixpacks | Supported | Not Supported | \* For Evaluation purposes only (for small teams of 10 users or less) \* CLM bundles Derby |
| **IBM Derby SDK 10.10** and future fixpacks | Supported | Not Supported | BLUE \* CLM bundles Derby 10.10 New for 5.0.1 and 5.0.2ENDCOLOR \* For Evaluation purposes only (for small teams of 10 users or less) |
| **IBM DB2 Enterprise Server Edition v10.1** and future fixpacks | Supported | Supported | *\* See bundling note below* |
| **IBM DB2 Workgroup Server Edition v10.1** and future fixpacks | Supported | Supported |  |
| **IBM DB2 Express Edition v10.1** and future fixpacks | Supported | Supported | \* (for small teams of 50 users or less) |
| **IBM DB2 Express-C 10.1** and future fixpacks | Supported | Not Supported | \* (for small teams of 25 users or less) |
| **IBM DB2 Enterprise Server Edition v10.5** and future fixpacks | Supported | Supported | BLUE \* New version for CLM 5.0ENDCOLOR |
| **IBM DB2 Workgroup Server Edition v10.5** and future fixpacks | Supported | Supported | BLUE \* New version and bundled for CLM 5.0ENDCOLOR |
| **IBM DB2 Express Edition v10.5** and future fixpacks | Supported | Supported | BLUE \* New version for CLM 5.0ENDCOLOR\* (for small teams of 50 users or less) |
| **IBM DB2 for i 6.1** and future fixpacks | Supported | Not Supported |  |
| **IBM DB2 for i 7.1** and future fixpacks | Supported | Not Supported |  |
| **IBM DB2 10 for z/OS 10.1** (with PTF UK77844) and future fixpacks | Supported | Supported | \* CLM, Cognos Content Store and Data Warehouse only. RRDI Report Server not supported. |
| **IBM DB2 11 for z/OS 11.1** and future fixpacks | Supported | Supported | BLUE \* New version for CLM 5.0ENDCOLOR \* CLM, Cognos Content Store and Data Warehouse only. RRDI Report Server not supported. |
| **Microsoft SQL Server Enterprise Edition 2012** and future fixpacks | Supported | Supported | BLUE \* New version for CLM 5.0ENDCOLOR |
| **Microsoft SQL Server Standard Edition 2012** and future fixpacks | Supported | Supported | BLUE \* New version for CLM 5.0ENDCOLOR |
| **Microsoft SQL Server Enterprise Edition 2014** and future fixpacks | Supported | Supported | BLUE\* New version for CLM 5.0.2 onlyENDCOLOR |
| **Microsoft SQL Server Standard Edition 2014** and future fixpacks | Supported | Supported | BLUE\* New version for CLM 5.0.2 onlyENDCOLOR |
| **Oracle Database 11g Enterprise Edition Release 2 11.2.0.2** and future fixpacks | Supported | Supported | \* Requires Oracle Java Database Connectivity (JDBC) ojdbc6.jar.11.2.0.3 or higher |
| **Oracle Database 11g Standard Edition Release 2 11.2.0.2** and future fixpacks | Supported | Supported | \* Requires Oracle Java Database Connectivity (JDBC) ojdbc6.jar.11.2.0.3 or higher |
| **Oracle Database 12c Enterprise Edition** and future fixpacks | Supported | Supported | BLUE \* New version for CLM 5.0.2 onlyENDCOLOR \* Requires Oracle Java Database Connectivity (JDBC) ojdbc6.jar.11.2.0.3 or higher |
| **Oracle Database 12c Standard Edition** and future fixpacks | Supported | Supported | BLUE \* New version for CLM 5.0.2 onlyENDCOLOR \* Requires Oracle Java Database Connectivity (JDBC) ojdbc6.jar.11.2.0.3 or higher |

#### A6.1 High Availability Database Support

CLM also supports setting up High Availability support with these
databases:

| Database | CLM Server | RRDI | Notes |
|:---|:---|:---|:---|
| **DB2 10.1 HADR** | Supported | Supported |  |
| **DB2 10.5 HADR** | Supported | Supported |  |
| **DB2 10 for z/OS 10.1** (with PTF UK77844) | Supported | Supported | \* CLM, Cognos Content Store and Data Warehouse only. RRDI Report Server not supported. |
| **IBM DB2 11 for z/OS 11.1** | Supported | Supported | BLUE \* New version for CLM 5.0ENDCOLOR \* CLM, Cognos Content Store and Data Warehouse only. RRDI Report Server not supported. |
| **Oracle 11g Release 2 Real Application Clustering Edition** | Supported | Supported | \* Oracle RAC requires Oracle Java Database Connectivity (JDBC) ojdbc6.jar.11.2.0.3 or higher |
| **Oracle 12c Real Application Clustering Edition** | Supported | Supported | BLUE \* New version for CLM 5.0.2 onlyENDCOLOR \* Oracle RAC requires Oracle Java Database Connectivity (JDBC) ojdbc6.jar.11.2.0.3 or higher |

##### Database Support Notes

-   Database support is 64-bit only to align with 64-bit server
    platforms. For RRDI the 32-bit database client library is required
    (even though the database server is 64-bit).
-   Bundling: WAS 8.5.5 and DB2 10.5 bundles are only available on
    Passport Advantage and in the CLM Media (not on Jazz.net). Customers
    upgrading from CLM 4.0.x are entitled to continue using DB2 10.1 as
    long as CLM supports that version.
-   The DB2 HADR functionality is included and can be used with the
    Limited Use Workgroup and Enterprise Server Editions. However, there
    must be entitlement coverage for the secondary/standby server. There
    is a 1:1 entitlement ratio for DB2 with the entitlement purchased by
    the customer of the bundling product. For eg. 500 PVUs of Portal
    entitles customer to use a maximum of 500 PVUs of DB2 in support of
    Portal. The entitlement requirement for the standby server depends
    on the standby configuration used, and is defined in the DB2
    license. ie. Hot standby requires equivalent entitlement as the
    Primary. Warm standby requires 100 PVUs/25 AUs, regardless of
    Primary. Cold standby server is free. Definition of hot/warm/cold
    standby configurations is also in the DB2 license.
-   Oracle is not supported for System z or IBM i.
-   SQL Server is supported on Windows Server only.
-   JTS Setup for Microsoft SQL Server does not support Integrated
    Authentication. You will be unable to install CLM in your
    environment. Ensure that server security is in mixed mode. To
    validate this, check server security -- it should be set to SQL
    Server and Windows Authentication Mode.
-   Database Pressures - these items are NOT currently in plan but are
    under consideration for future quarterly releases:
    -   Oracle 12 [CLM
        273293](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.workitem.viewWorkItem&id=276293l)
    -   DB2 PureScale CLM
        [317096](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.workitem.viewWorkItem&id=317096)
        Please watch this dashboard for updates to System Requirements
        [CLM Platform Plans and Pressures
        Dashboard](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.dashboard.viewDashboard&tab=_79).

### A7. Eclipse (Server)

-   Eclipse SDK 3.6.2.3 (Eclipse Runtime, Equinox and EMF) \[Bundled\].

### A8. HTTP Reverse Proxy Support

-   Apache Server 2.2.19 on RHEL and SLES \[Non-secure Only (no HTTPS)\]
-   IBM HTTP Server 8.0.0.6
-   IBM HTTP Server 8.5.0.2
-   IBM HTTP Server 8.5.5
-   Websphere Application Server Network Deployment v8.0.0.6
-   Websphere Application Server Network Deployment v8.5.0.2
-   Websphere Application Server Network Deployment v8.5.5
-   Squid 3.3.3 for caching (see [Using content caching proxies for Jazz
    Source
    Control](https://jazz.net/wiki/bin/view/Deployment/ContentCachingProxyJazzSCM)).

See [Proxy server installation landing page](InstallProxyServers) for
detail on installing and configuring proxy servers.

### A9. Java Runtime Environment (Server)

| JRE | CLM Server | RRDI | Notes |
|:---|:---|:---|:---|
| **IBM Java SDK 6.0.15 iFix 1 (6.0.15.1)** and future fixpacks | Supported | Supported | BLUE \* New version for CLM 5.0 onlyENDCOLOR \* This is the bundled version of Java for the CLM Server |
| **IBM Java SDK 6.0.16 (6.0.16)** and future fixpacks | Supported | Supported | BLUE \* New version for CLM 5.0.1 onlyENDCOLOR \* This is the bundled version of Java for the CLM Server |
| **IBM Java SDK 6.0.16 iFix 1 (6.0.16.1)** and future fixpacks | Supported | Supported | BLUE \* New version for CLM 5.0.2 onlyENDCOLOR \* This is the bundled version of Java for the CLM Server |
| **Java 6 64 bit for IBM i V6R1 and V7R1** and future fixpacks | Supported | Not Supported | \* For IBM i - PTF SI49257 |
| **IBM Java SDK 6.0.1.5 (J9 2.6)** and future fixpacks | Supported | Supported | *\* Specifically for z/OS \* FixPack 5 or later is required (6.0.1.5)* |

### A10. Identity Management

-   Apache Directory Server 1.5.5
-   IBM Resource Access Control Facility (RACF) V1R12, V1R13 and V2R1 as
    bundled with all supported z/OS versions listed above
-   IBM Tivoli Directory Server 6.3
-   Microsoft Active Directory 2008 R2 BLUEPlease note this version will
    EOS in January 2015 please plan to upgrade before that time.ENDCOLOR
-   Microsoft Active Directory 2012 BLUENew version for CLM 5.0.ENDCOLOR

### A11. Installation Manager

-   IBM Installation Manager 1.7.2 BLUENew version for CLM 5.0ENDCOLOR
    and bundled with CLM media.
-   IBM Installation Manager 1.7.3 BLUENew version for CLM 5.0.1ENDCOLOR
    and bundled with CLM media.
-   IBM Installation Manager 1.8 BLUENew version for CLM 5.0.2ENDCOLOR
    and bundled with CLM media.

### A12. License Server

-   Rational License Server 8.1.4 BLUENew version for CLM 5.0ENDCOLOR
    and bundled with CLM media.

### A13. Report Customization

-   Rational Reporting for Development Intelligence 5.0 BLUENew version
    for CLM 5.0ENDCOLOR and bundled with CLM.
-   Rational Reporting for Development Intelligence 5.0.1 BLUENew
    version for CLM 5.0.1ENDCOLOR and bundled with CLM.
-   Rational Reporting for Development Intelligence 5.0.2 BLUENew
    version for CLM 5.0.2ENDCOLOR and bundled with CLM.

## B. **Client Requirements**

-   **Reminder: The platforms listed below are the starting point for
    CLM support and unless otherwise indicated support includes this
    level and all future OS fixpacks. For RedHat, Updates are equivalent
    to fix packs.**

### B1. Client Operating Systems

| Client Operating System | RTC Eclipse Client | RTC client for Visual Studio | RTC zLinux Client | Web Clients (Browsers) | Notes |
|:---|:---|:---|:---|:---|:---|
| **Red Hat Enterprise Linux (RHEL) Client and Workstation Editions v6** and future Updates | 32 & 64 bit | Windows Only | zLinux Only | Supported | \* See RTC Eclipse Client Note below |
| **Red Hat Enterprise Linux (RHEL) Client and Workstation Editions v7** and future Updates | 32 & 64 bit | Windows Only | zLinux Only | Supported | BLUE \* New for CLM 5.0.1 and 5.0.2 ENDCOLOR \* See RTC Eclipse Client Note below |
| **SUSE Linux Enterprise Desktop (SLED) 11.0 x86-32, x86-64** and future OS fixpacks | 32 & 64 bit | Windows Only | zLinux Only | Supported | \* See RTC Eclipse Client Note below |
| **Mac OS X Lion 10.7 x86-32, x86-64** BLUEand future versions of MAC OS XENDCOLOR | 32 & 64 bit | Windows Only | zLinux Only | Supported | BLUE \* New for CLM 5.0 - new versions of Mac OS X are also supported ENDCOLOR |
| **Ubuntu Desktop 12.04 LTS x86-64** this version only | 32 & 64 bit\* | Windows Only | zLinux Only | Supported | \* RTC Eclipse and Web Client support only \* See xlrunner in Client OS Notes below |
| **Windows 7 Enterprise, Professional and Ultimate Editions** and future OS fixpacks | 32 & 64 bit | 32 & 64 bit | zLinux Only | Supported |  |
| **Windows 8.1 Enterprise, Professional and Standard Editions** and future OS fixpacks | 32 & 64 bit | 32 & 64 bit | zLinux Only | Supported | BLUE \* New version for CLM 5.0ENDCOLOR \* Does not include Metro Support \* Supported for RTC Eclipse 4.2.2 client and higher |
| **Red Hat Enterprise Linux (RHEL) Server 6 System z** and future Updates | NA | NA | 64 bit | NA | \* RTC zLinux Client only |
| **SUSE Linux Enterprise Server (SLES) 11 System z** and future OS fixpacks | NA | NA | 64 bit | NA | \* RTC zLinux Client only |

#### Client Operating System Notes

-   If you are running the RTC Eclipse client on Linux please ensure
    that you have a compatible xulrunner or webkitgtk installed and
    configured on your system. Failure to do so can result in various
    issues including failure to start. See
    [Article](https://jazz.net/library/article/952) for additional
    details and instructions.
-   Smart Card Support for ALL CLM Products (Windows Only).
-   MAC OSX is supported for RTC, RQM and RDNG Only (not RRDI).

### B2. Browsers

| Browser | CLM Web Client | RRDI | Notes |
|:---|:---|:---|:---|
| **Apple Safari 5.1** BLUEand future versionsENDCOLOR | Supported | Not Supported | BLUE \* New for CLM 5.0 - new versions of Safari are also supportedENDCOLOR \* The Safari browser shows graphical artifacts in preview mode, but does not support editing \* See note below for RM Graphical Editors |
| **Firefox 31 ESR** and future fixpacks | Supported | Supported | BLUE \* Firefox 31 ESR New for 5.0.1 and 5.0.2ENDCOLOR \* See note below for mixed http/https content and self-signed certificates \* See note below for RM Graphical Editors |
| **Google Chrome** BLUEthree latest releasesENDCOLOR | Supported | See below | BLUE \* Chrome does not provide ESR releases so CLM supports the three latest releases (current and 2 prior) based on the Chrome versions available at the time of the CLM release. \* Testing for each quarterly release is run on the latest released version of ChromeENDCOLOR \* See note below for mixed http/https content and self-signed certificates \* See note below for RM Graphical Editors |
| Google Chrome 34 | See above | Supported | \* Supported by Cognos 10.2.1 FixPack 1 and later \* Only particular Cognos components are supported: Cognos Workspace, Cognos Connection, Cognos Viewer, Report Studio and Cognos Workspace Advanced \* The current version of Google Chrome is supported based on testing with earlier versions of Chrome during development. We will work to maintain compatibility with Google Chrome, please be aware that issues may be introduced if and when Google makes significant changes to Chrome between rapid-releases \* Active Reports are not supported |
| **Internet Explorer 9** and future fixpacks | Supported | Supported | \* See note below for mixed http/https content and self-signed certificates \* See note below for RTC Quick Planner |
| **Internet Explorer 10 for the Desktop** and future fixpacks | Supported | Supported | \* RRDI supports IE10 in compatibility mode only (Cognos 10.2.x limitation) \* See note below for mixed http/https content and self-signed certificates |
| **Internet Explorer 11 for the Desktop** and future fixpacks | Supported | Supported | BLUE \* New version for CLM 5.0ENDCOLOR \* See note below for mixed http/https content and self-signed certificates |

#### Browser Support Notes

-    BLUEPlease see these tech note articles for [mixed http/https
    content](http://www-01.ibm.com/support/docview.wss?uid=swg21653966)
    and [self-signed
    certificates](http://www-01.ibm.com/support/docview.wss?uid=swg21654984)
    which may result in content not being shown as expected. ENDCOLOR
-   The RDNG Graphical Editor is supported in 32-bit mode using Internet
    Explorer and Firefox on Windows (Only). Chrome and Safari browsers
    will show graphical artifacts in preview mode, but will not support
    editing.
-   RTC Quick Planner DOES NOT support IE9 and will not present as a
    menu option when used with IE9.
-   Macromedia Flash Player 10,11\* and future releases, mods and
    fixpacks is supported for graphical view in Work Item Statistics
    dashboard viewlet.

### B3. RTC Clients Memory and Hardware Requirements

-   For both the Eclipse and VS.Net clients and for each instance of an
    RTC clients these are the minimum requirements:
    -   Memory: 1GB RAM minimum, (2GB recommended)
    -   Disk Space: 1GB minimum
    -   Hardware - Intel Pentium 4 processor minimum.

### B4. Eclipse IDE (RTC Eclipse Client)

\| **IES** \| **Notes** \| \| **IBM Eclipse SDK 3.6.2.3** and future
fixpacks \| \* IES 3.6.2.3 and 4.2.2.1 are provided with the RTC client
install \| \| **IBM Eclipse SDK 4.2.2.1** and future fixpacks \| \* IES
3.6.2.3 and 4.2.2.1 are provided with the RTC client install \| \| **IBM
Eclipse SDK 4.3.2** and future fixpacks \| \* BLUEIES 4.3.2 New for
5.0ENDCOLOR \| \| **IBM Eclipse SDK 4.4** and future fixpacks \| BLUE \*
IES 4.4 New for 5.0.1 and 5.0.2ENDCOLOR \* The RTC Client bundles IES
3.6.2.3 or 4.2.2.1 (two installation options) \* You may also use the
4.2.2.1 installation to install RTC via p2 install over Eclipse 4.4 \*
For IBM Eclipse 4.4 SDK, there are no translations available for any new
strings added in 4.4 \* Rational Team Concert 5.0.2 clients do not
install into Eclipse 4.4 Package Groups. Please see [this
technote](https://jazz.net/library/article/1527) for a workaround. \| \|
**IBM Eclipse SDK 4.4.1** and future fixpacks \| BLUE \* IES 4.4.1 New
for 5.0.2 onlyENDCOLOR \* The RTC Client bundles IES 3.6.2.3 or 4.2.2.1
(two installation options) \* You may also use the 4.2.2.1 installation
to install RTC via p2 install over Eclipse 4.4.1 \* For IBM Eclipse 4.4
SDK, there are no translations available for any new strings added in
4.4 \|

#### Eclipse IDE Notes

\* **If you are installing the Rational Team Concert Client into an
existing instance of Eclipse IDE 3.6, please read [this
technote](https://www-304.ibm.com/support/docview.wss?rs=3488&uid=swg21502374&wv=1).**

### B5. Other Runtime Enviroments (RTC Only)

\| **Runtime** \| **Notes** \| \| **Microsoft Visual Studio 2010** and
future fixpacks \| \* VS.Net is supported for the RTC Client for Visual
Studio \* RTC specifically supports the Visual Studio Professional,
Premium and Ultimate Editions \| \| **Microsoft Visual Studio 2012** and
future fixpacks \| \* VS.Net is supported for the RTC Client for Visual
Studio \* RTC specifically supports the Visual Studio Professional,
Premium and Ultimate Editions \| \| **Microsoft Visual Studio 2013** and
future fixpacks \| \* VS.Net is supported for the RTC Client for Visual
Studio \* RTC specifically supports the Visual Studio Professional,
Premium and Ultimate Editions \|

### B6. Java SDK (RTC Eclipse Client)

|  |  |
|----|----|
| \* **IBM Java SDK 6.0.15 iFix 1** and future fixpacks | BLUE \* New for CLM 5.0 only ENDCOLOR \* Bundled with CLM |
| \* **IBM Java SDK 6.0.16** and future fixpacks | BLUE \* New for CLM 5.0.1 only ENDCOLOR \* Bundled with CLM |
| \* **IBM Java SDK 6.0.16 iFix 1** and future fixpacks | BLUE \* New for CLM 5.0.2 only ENDCOLOR \* Bundled with CLM |
| \* **IBM Java SDK 7.0.1 iFix 1** and future fixpacks | *\* For Java 7 Development* |
| \* **IBM Java SDK 7.0.7 iFix 1** and future fixpacks | BLUE \* New for CLM 5.0.2 only ENDCOLOR \* For Java 7 Development |

## C. Additional RTC Clients and Optional Tools

### C1.RTC Clients N-1 Compatibility

-   For upgrades, after upgrading the Server, teams may choose to
    gradually upgrade the clients. CLM supports N-1 (keeping the clients
    one release behind) to allow for this more gradual update of
    workstations.
-   This applies to all the RTC clients including the Eclipse, VS.Net
    SCM CLI, Windows Shell and ISPF Clients. For clarity we also include
    the table below:

|  |  |  |  |  |  |  |  |  |  |  |
|----|----|----|----|----|----|----|----|----|----|----|
| Server | Compatible Clients |  | CLM 5.0.x Server | RTC Eclipse Client 5.0.y, (x\>=y)RTC Eclipse Client v4.0.y or Later |  |  | RTC VS.Net Client v.5.0.y, x\>=y VS.Net Client v.4.0.y or later |  |  | RTC SCM CLI v.5.0.y, x\>=y RTC SCM CLI v.4.0.y or later |
|  | RTC ISPF Client v.5.0.y, x\>=y RTC ISPF Client v.4.0.y or later |  |  |  |  |  |  |  |  |  |
|  | RTC Windows Shell Client y, x\>=y RTC Windows Shell Client v.4.0.y or later |  |  |  |  |  |  |  |  |  |
|  | RTC MSSCCI Provider v.5.0.y, x\>=y RTC MSSCCI Provider v.4.0.y or later |  |  |  |  |  |  |  |  |  |

### C2. RTC Build System Toolkit

-   The Build System Toolkit is a 32 bit client that can be run on the
    RTC Server and the Client Operating Systems. Please see the
    downloads page for the specific executable on your platform. For the
    RTC Eclipse client platforms there is an Installation Manager
    install. For z/OS there is a SMP/E install. For IBM i there is a
    LICPGM install. For all other platforms there are Plain Zips.
-   The Build System Toolkit is supported using the the versions of Java
    that RTC supports on the selected install platform. When installed
    on z/OS, the Build System Toolkit is also supported using Java 7.

### C3. RTC SCM Command-Line Tool

-   The SCM Command-Line Tool is supported on all Server Platforms
    except for IBM i.

### C4. RTC ISPF Client and ISPF Gateway

-   The Rational Team Concert ISPF Client is supported on all zOS
    platforms as specified under Server Operating Systems.
-   Prior to RTC 4.0.5, the Rational Team Concert ISPF client required
    cURL, an open source tool supplied through IBM Ported Tools
    Supplementary Toolkit for z/OS. Information on IBM Ported Tools can
    be found at: [IBM Ported Tools for z/OS Product and Feature
    Information](http://www.ibm.com/systems/z/os/zos/features/unix/ported/).
    If you already have IBM Ported Tools installed, cURL for z/OS is
    available by ordering the PTF for APAR OA2. Release 4.0.5 and later
    do not have this dependency.
-   For 4.0.5 the ISPF client supports the same Java versions as the CLM
    Server on z/OS. For 4.0.6 and later, the ISPF client supports those
    plus Java 7 on z/OS.
-   Information on the Supplementary Toolkit for z/OS can be found at
    [Supplement Toolkit for
    z/OS](http://www.ibm.com/systems/z/os/zos/features/unix/ported/suptlk/index.html.).
-   Rational Team Concert uses the ISPF Gateway component of ISPF for
    access to z/OS files. For the ISPF Gateway component to function
    correctly, you must install a number of PTFs for the listed APARs.
    If you do not install the appropriate PTF, you might encounter
    problems with ISPF Gateway usage. For the supported ISPF releases,
    the PTFs are as follows:
    -   for APAR OA35689:
        -   z/OS 1.9: UA63763
        -   z/OS 1.10: UA59950
        -   z/OS 1.11: UA59951
        -   z/OS 1.12: UA59951
        -   z/OS 1.13: - code is at appropriate level
    -   for APAR OA38740:
        -   z/OS 1.10: UA65381
        -   z/OS 1.11: UA65382
        -   z/OS 1.12: UA65382
        -   z/OS 1.13: UA65383
    -   for APAR OA39666:
        -   z/OS 1.11: UA65909
        -   z/OS 1.12: UA65909
        -   z/OS 1.13: UA65910
    -   for APAR OA43014:
        -   z/OS 1.12: UA71732
        -   z/OS 1.13: UA71733
    -   for APAR OA43738
        -   z/OS 1.12: UA71471
        -   z/OS 1.13: UA71472
        -   z/OS 2.1: UA71473
    -   for APAR OA43888
        -   z/OS 2.1: UA71763
    -   for APAR OA44263:
        -   z/OS 1.12: UA72897
        -   z/OS 1.13: UA72898
        -   z/OS 2.1: UA72899
    -   for APAR OA44369:
        -   z/OS 2.1: UA72964
    -   for APAR OA44388:
        -   z/OS 2.1: UA73005

### C5. Rational Team Concert (RTC) Shell Client (introduced in v4.0)

-   The RTC Shell is distributed as a downloadable file through IBM
    Installation Manager.
-   Windows 7 and Windows 8.1 (both 32-bit and 64-bit) operating systems
    are supported.
-   RTC Shell requires Microsoft Visual C++ 2010 x64 Redistributable
    package for 64-bit systems or Microsoft Visual C++ 2010 x86
    Redistributable package for 32-bit systems. The .NET Framework 4.0
    is also required.

### C6. Rational Team Concert (RTC) MSSCCI Provider (introduced in v4.0)

-   The RTC MSSCCI Provider is distributed as a downloadable file
    through IBM Installation Manager.
-   Only Windows 7 and Windows 8.1 (both 32-bit and 64-bit) operating
    systems are supported. On Windows 7 and Windows 8.1 (64-bit), MSSCCI
    provider only integrates with applications running in 32-bit mode.
-   RTC MSSCCI Provider requires that the Microsoft .NET framework
    version 4.0 and Microsoft Visual C++ 2010 x86 Redistributable
    package (32-bit) are pre-installed.

### C7. Rational ClearQuest (CQ) Synchronizer Gateway ---++++ C7.1 CQ Synchronizer Server Operating Systems The following application servers can be used to host the synchronizer gateway:

| Server Operating System | Bits | Notes |
|:---|:---|:---|
| **Windows Server 2008 R2 SP1/SP2 Enterprise/Standard** and future fixpacks | 64 bit |  |
| **Windows Server 2012 DataCenter/Essentials/Standard Edition x86-64** and future fixpacks | 64 bit | \* New in Rational Team Concert 4.0.5 with ClearQuest v8.0.0.06 or newer |
| **Red Hat Enterprise Linux (RHEL) Server 6 x86-64** and future fixpacks | 64 bit |  |
| **SUSE Linux Enterprise Server (SLES) 11 SP1 x86-64** and future fixpacks | 64 bit |  |

##### *CQ Synchronizer Gateway Server Host Operating System Notes*

-   The ClearQuest Synchronizer Setup Wizard is not supported on Linux.
-   The ClearQuest client is required to install the Sychronizer Gateway
    on the host server.
-   CQ must be 7.1.2 or later. Please consult the [system requirements
    for
    ClearQuest](http://www-01.ibm.com/support/docview.wss?uid=swg27023170).

#### C7.2 CQ Synchronizer Gateway Memory Requirements

-   Minimum of 4 GB. Recommend 8 GB RAM. More memory generally improves
    performance.

#### C7.3 CQ Sycnronizer Gateway Application Server(s)

-   Apache Tomcat 7 \[Bundled\] New version for CLM 2012.

#### C7.4 CQ Synchronizer Gateway Java Runtime Environment

-   IBM Java SDK 6.0.10 iFix 1 and future fixpacks \[Bundled\].

## D. CLM Integrations, Migrations and Adapters

CLM applications integrate with each of the products listed below.

### D1. Integrations

| Capability Group | Integration | with RTC | with RQM | with RDNG | Notes |
|:--:|---:|:--:|:--:|:--:|:--:|
| Architecture & Design | **IBM Rational Rhapsody 8.0** and future fix packs | Supported | Supported | NA | Rhapsody integrates with RTC and RQM only |
|  | **IBM Rational Rhapsody Design Manager 4.0** and future mod levels and their fix packs | Supported | Supported | NA | Rhapsody DM integrates with RTC, RQM, RDNG. Use the web client for creating and deleting OSLC links. |
|  | **IBM Rational Rhapsody Design Manager 5.0** and future mod levels and their fix packs | Supported | Supported | NA | Rhapsody DM integrates with RTC, RQM, RDNG. Use the web client for creating and deleting OSLC links. |
|  | **IBM Rational Software Architect Design Manager 4.0** and future mod levels and their fix packs | Supported | Supported | Supported | RSA DM integrates with RTC, RQM, RDNG. Use the web client for creating and deleting OSLC links. |
|  | **IBM Rational Software Architect 8.5** and future mod levels and their fix packs | Supported | NA | NA | RSA integrates with RTC only |
|  | **IBM Rational Software Architect for WebSphere Software 8.5** and future mod levels and their fix packs | Supported | NA | NA | RSA integrates with RTC only |
|  | **IBM Rational Software Architect 9.1** and future mod levels and their fix packs | Supported | NA | NA | RSA integrates with RTC only |
|  | **IBM Rational Software Architect for WebSphere Software 9.1** and future mod levels and their fix packs | Supported | NA | NA | RSA integrates with RTC only |
|  | **IBM Rational Software Architect RealTime Edition 9.1** and future fix packs | Supported | NA | NA | RSA integrates with RTC only |
| Asset Management | **IBM Rational Asset Manager Enterprise Edition 7.5.1** and future fix packs, mod levels and their fix packs | Supported | Supported | Supported | RAM integrates with RTC, RQM, RDNG |
|  | **IBM Rational Asset Manager Standard Edition 7.5.1** and future fix packs, mod levels and their fix packs | Supported | Supported | Supported | RAM integrates with RTC, RQM, RDNG |
| Change and Release Management | **Rational Change 5.3** and future mod levels and their fix packs | Supported | Supported | Supported | Change and Synergy are closely linked and share the same repository. Change integrates with RTC, RQM, RDNG. For RTC that integration is made via Rational Synchronization Server. For the RQM and RDNG integrations Change uses OSLC.Use the web client for creating and deleting OSLC links |
|  | **Rational Synergy 7.2** and future mod levels and their fix packs | Supported | Supported | NA | Synergy integrates with RTC and RQM. Synergy integrates with RTC via Rational Synergy For Rational Team Concert Interface. |
|  | **IBM Rational Clearquest 7.1.2\*** and future fix packs | Supported | Supported | Supported | CQ 7.1.2 integrates with RTC, RQM, RDNG |
|  | **IBM Rational Clearquest 8.0** and future mod levels and their fix packs | Supported | Supported | Supported | CQ 8.0 integrates with RTC, RQM, RDNG.Use the web client for creating and deleting OSLC links |
| Collaboration | **Rational Lifecycle Integration Adapters 1.0** and future fix packs | Supported | Supported | Supported | RLIA enables integrations with Jira, GIT and HPQC. |
|  | **Atlassian JIRA 4.4.x** and future fix packs | Supported | Supported | Supported | Jira integrates with RTC, RDNG and RQM via RLIA. |
|  | **Git 1.7.1** and future fix packs | Supported | NA | NA | GIT integrates with RTC via RLIA. |
|  | **HP Quality Center 11.0** and future fix packs | Supported | NA | Supported | HPQC integrates with RTC, RDNG via RLIA. Use the web client for creating and deleting OSLC links. |
|  | **IBM Connections 4.0, 4.5** and future fix packs | Supported | NA | NA | IBM Connections integrates with RTC only. Please note that this integration supports form based auth, but not OAuth which means that the integration is not supported on the IBM SmartCLoud |
| Configuration Management | **IBM Rational Build Forge Enterprise, Enterprise Plus & Standard Editions 7.1.1.4** and future fix packs | Supported | Supported | NA | BF integrates with RTC only |
|  | **IBM Rational Build Forge Enterprise, Enterprise Plus & Standard Editions 7.1.2** and future fix packs, mod levels and their fix packs | Supported | Supported | NA | BF integrates with RTC only |
|  | **IBM Rational Build Forge Enterprise, Enterprise Plus & Standard Editions 8.0.0.1** and future fix packs, mod levels and their fix packs | Supported | Supported | NA | BF integrates with RTC only |
|  | **IBM Rational ClearCase 7.1.2** and future fix packs | Supported | NA | NA | CC integrates with RTC only |
|  | **IBM Rational ClearCase 8.0** and future fix packs, mod levels and their fix packs | Supported | NA | NA | CC integrates with RTC only |
|  | **IBM Rational UrbanCode Deploy 6.0** and future fix packs | Supported | NA | NA | UrbanCode integrates with RTC only |
|  | **IBM Rational UrbanCode Deploy 6.0.1.1** and future fix packs | Supported | NA | NA | UrbanCode integrates with RTC only |
|  | **IBM Rational UrbanCode Deploy 6.1** and future fix packs | Supported | NA | NA | UrbanCode integrates with RTC only |
|  | **IBM Rational UrbanCode Deploy 6.1.1** and future fix packs | Supported | NA | NA | BLUE \* New version for CLM 5.0.2 onlyENDCOLOR \* UrbanCode integrates with RTC only |
| Connectors | **IBM Rational Connector for SAP Solution Manager 4.0** and future fix packs | Supported | Supported | NA | SAP Connector integrates with RTC, RQM |
| Development Tools | **Rational Application Developer for WebSphere Software 8.5** and future mod levels and their fix packs | Supported | NA | NA | RAD integrates with RTC only |
|  | **Rational Application Developer for WebSphere Software 9** and future mod levels and their fix packs | Supported | NA | NA | RAD 9 integrates with RTC 4.0.3 and future mod releases and fixpacks |
|  | **IBM Rational Business Developer 8.5** and future fix packs | Supported | NA | NA | RBD integrates with RTC only |
|  | **IBM Rational Developer for Power System Software 8.5** and future mod levels and their fix packs | Supported | NA | NA | The RD Power integration is specific to the EE features in RTC. |
|  | **IBM Rational Developer for System z 8.5** and future fix packs | Supported | NA | NA | RDz integrates with RTC only |
|  | **IBM Rational Programming Patterns 8.5** and future mod levels and their fix packs | Supported | NA | NA | RPP integrates with RTC only |
| Instant Messaging | **IBM Lotus Sametime Standard 8.0** and future mod levels and their fix packs | Supported | NA | NA | Sametime integrates with RTC only |
|  | **IBM Lotus Sametime Standard 8.5** and future fix packs | Supported | NA | NA | Sametime integrates with RTC only. |
|  | **Jabber Openfire 3.4.1** and future fix packs | Supported | NA | NA | Jabber integrates with RTC only |
| Process Management | **IBM Rational Method Composer 7.5.2** and future fix packs | Supported | NA | NA | RMC integrates wtih RTC only |
| Project Management | **IBM Rational Focal Point 6.5.2** and future fix packs, mod levels and their fix packs | Supported | NA | Supported | Focal Point integrates with RTC, RDNG |
|  | **IBM Rational Focal Point 6.6** and future fix packs only | Supported | NA | Supported | Focal Point integrates with RTC, RDNG. |
| Reporting and Analysis | **IBM Rational Insight 1.1.1.4** and future fix packs | Supported | Supported | Supported | Note - A schema change was made in 1.1.1.3 for additional reporting in RQM so this new version of Insight is required for integrating with CLM 4.0.5 and later fixpacks and Mod releases |
|  | **IBM Rational Publishing Engine 1.1.1 and 1.2** and future fix packs, mod levels and their fix packs | Supported | Supported | Supported | RPE integrates with RTC, RQM, RDNG |
| Requirements Management | **IBM Rational DOORS 9.6** and future mod levels and their fix packs | Supported | Supported | NA | DOORS 9.3 and earlier, you can integrate DOORS and RQM by using RQMi. For additional information see: <https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.rational.test.qm.doc/topics/t_ovw_int_rqm_doors.html&scope=null> Starting in DOORS 9.4, you can integrate DOORS and RQM by using the OSLC specification. For additional information see: <https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.rational.test.qm.doc/topics/t_ovw_int_rqm_doors.html&scope=null> |
|  | **IBM Rational DOORS Web Access 9.6** and future mod levels and their fix packs | Supported | Supported | Supported | DWA 9.6 integrates with RTC, RQM, RDNG |
| Security Management | **IBM Rational AppScan Enterprise Edition 8.5** and future mod levels and their fix packs | Supported | Supported | NA | AppScan Enterprise integrates with RTC,RQM |
|  | **IBM Security AppScan Enterprise Edition 8.6** and future mod levels and their fix packs | Supported | Supported | NA | formerly Rational AppScan EnterpriseAppScan Enterprise integrates with RTC,RQM |
|  | **IBM Rational AppScan Source Edition 8.5** and future mod levels and their fix packs | Supported | NA | NA | AppScan Source integrates with RTC only |
|  | **IBM Security AppScan Source Edition 8.5** and future mod levels and their fix packs | Supported | NA | NA | formerly Rational AppScan SourceAppScan Source integrates with RTC only |
| Systems Engineering | **IBM Rational Engineering Lifecycle Manager 1.0** and future releases, mod levels and fix packs | Supported | Supported | NA | RELM integrates with RTC, RQM |
| Test Tools | **Rational Functional Tester 8.5** and future fix packs, mod levels and their fix packs | Supported | Supported | NA | RFT integrates with RTC, RQM |
|  | **IBM Rational Performance Tester 8.1.1.4 and 8.3** and and future mod levels and their fix packs | Supported | Supported | NA | RPT integrates with RTC, RQM |
|  | **IBM Rational Service Tester for SOA Quality 8.2.1 and 8.3** and future fix packs | Supported | Supported | NA | SOA Tester integrates with RTC, RQM |
|  | **IBM Rational Robot 7.0.3** and future fix packs, mod levels and their fix packs | NA | Supported | NA | Robot integrates with RQM only |
|  | **IBM Rational Test RealTime 8.0** and future mod levels and their fix packs | Supported | Supported | NA | TestRT integrates with RTC, RQM |

### D2. Migration Support

| Capability Group | Migration From | to RQM | to RDNG | Notes |
|:---|:---|:---|:---|:---|
| Test Artifacts | **IBM Rational Clearquest 7.1.2** and future fix packs | CQ TM artifacts to RQM | NA |  |
|  | **IBM Rational Clearquest 8.0** and future mod levels and their fix packs | CQ TM artifacts to RQM | NA |  |
|  | **IBM Rational Manual Tester 7.0.1** and future fix packs | RMT aftifacts to RQM | NA |  |
|  | **IBM Rational Test Manager 7.0.2** and future fix packs | TM aftifacts to RQM | NA |  |
|  | **IBM Rational Test RealTime 8.0** and future fix packs | TestRT aftifacts to RQM | NA |  |
| Requirements | **IBM Rational RequisitePro 7.1.3** and future mod levels and fix packs | NA | ReqPro Requirements to RDNG |  |

### D3. Test Tool Adapters

-   **IBM Rational Functional Tester 8.5** and future fix packs, mod
    levels and their fix packs
-   **IBM Rational Performance Tester 8.2.1.4 and 8.3** and future fix
    packs, mod levels and their fix packs
-   **IBM Rational Service Tester for SOA Quality 8.2.1 and 8.3** and
    future fix packs, mod levels and their fix packs
-   **IBM Security AppScan Enterprise Edition 8.6** and future mod
    levels and their fix packs
-   **IBM Rational Robot 7.0.3** and future fix packs, mod levels and
    their fix packs
-   **IBM Rational Test RealTime 8.0** and future mod levels and their
    fix packs

## E. Related Articles

-   [CLM Sizing Strategy](CLMSizingStrategy)

## F. Track Changes

-   New for CLM 5.0
    -   IBM z/OS System z v2.1
    -   Windows 8.1 (Desktop)
    -   Internet Explorer 11
    -   WAS 8.5.5 (new bundle)
    -   WAS Liberty Profile support
    -   DB2 10.5 (and new bundle)
    -   DB2 11 for z/OS 11
    -   SQL Server 2012
    -   Java 6.0.15 iFix 1
    -   IES 4.3.2 (RTC Client support)
    -   Google Chrome - Latest 3 versions
    -   MAC OSX 10.6 and Safari 5.1 - and later versions are now
        supported
-   These platforms were dropped for CLM 5.0: (and are not included in
    the lists above). Note that this list was previously included in
    4.0.5 and 4.0.6 announcements and in release articles.
    -   Internet Explorer 8
    -   IBM z/OS System z v1.9 (out of Service)
    -   IBM z/OS System z v1.10 (out of Service)
    -   IBM z/OS System z v1.11 (out of Service)
    -   RHEL 5
    -   SUSE Linux 10
    -   Windows Server 2008 (keeping support for Windows Server 2008 R2)
    -   Websphere Application Server v7.0.x
    -   DB2 9.7.x
    -   DB2 9 for z/OS 9.1
    -   Microsoft SQL Server 2008 (EOS April 2014)
    -   Microsoft SQL Server 2008 R2 (EOS July 2014)
    -   Oracle 10 (EOS July 2010)
    -   Windows XP (which went out of service in 2010)
    -   Windows Vista
    -   Mac OS X 10.5 Snow Leopard
    -   Internet Explorer 8
    -   Visual Studio 2005 and 2008 Customers who still need to run CLM
        products on these platforms may continue to run existing
        releases, such as CLM V4.0.6 and others that will continue to
        provide this support. However, to gain access to 5.0 and future
        releases of the CLM products, customers will need to plan for
        moving off the dropped platforms.
-   New for CLM 5.0.1
    -   IBM Eclipse SDK 4.4
    -   IBM Derby SDK 10.10
    -   Windows Server 2012 R2 Datacenter and Standard Editions
    -   Firefox 31 ESR
    -   Tomcat 7.0.54 is bundled with CLM 5.0.1 (Tomcat 7.0.52 is
        bundled with CLM 5.0)
    -   RHEL 7 x86-64 New for 5.0.1 (RRDI not supported)
    -   Java 6.0.16 support added
    -   JRE 7.0.7

<!-- -->

-   New for CLM 5.0.2
    -   Java 6.0.16 iFix 1 support added
    -   IBM i 7.2 POWER System - Big Endian
    -   RHEL Server 7 POWER System - Big Endian
    -   RHEL Server 7 System z
    -   IBM Eclipse SDK 4.4.1
    -   Microsoft SQL Server 2014 Enterprise and Standard Editions
    -   Oracle 12c Standard, Enterprise and Real Application Clustering
        Editions
    -   IBM Installation Manager 1.8
    -   IBM Java SDK 7.0.7 iFix 1 RTC Eclipse Client

<!-- -->

-   You will also see notes in the article above about intentions to
    drop these platforms:
    -   Solaris - no new customers for 5.0, this platform will be
        dropped in a future release.
    -   Windows Server 2008 R2 - this platform goes EOS in January 2015
        please make plans to upgrade to Windows Server 2012 before that
        time.

For additional platform plans, pressures and drops information please
see the [CLM Platform Plans and Pressures
Dashboard](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.dashboard.viewDashboard&tab=_79).
