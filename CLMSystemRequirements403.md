META:TOPICINFO{author="sbeard" date="1417903382" format="1.1"
reprev="1.48" version="1.48"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# System Requirements for Collaborative Lifecycle Management 4.0.3 and 4.0.4 [system-requirements-for-collaborative-lifecycle-management-4.0.3-and-4.0.4]

DKGRAY ***(Rational Team Concert, Rational Quality Manager and Rational
Requirements Composer including Jazz Team Server and Rational DOORS Next
Generation)*** Authors: [Deborah Weil-O'Day](Main.DebWeil) Build basis:
CLM 4.0.3, 4.0.4 ENDCOLOR

TOC{title="Page contents"}

For a short list of track changes to this article please see the bottom
of this article.

-   This is the list of system requirements for **Collaborative
    Lifecycle Management (CLM)** 4.0.3 and 4.0.4 incorporating:
    -   The **Jazz Foundation (JAF)** technology project
    -   The **Rational Team Concert (RTC)**, **Rational Quality Manager
        (RQM)** and **Rational Requirements Composer (RRC)** products
    -   **Rational Reporting for Development Intelligence (RRDI)** for
        customized reporting
    -   We also include requirements for **Doors Next Generation (DNG)**
        which is closely aligned with the CLM products above but ships
        with DOORS 9.5.
-   For platform pressures (enhancements and more) please see the CLM
    Dashboard: [System Requirements
    dashboard](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.dashboard.viewDashboard&tab=_79).
-   Questions? Please contact [Deborah Weil-O'Day](Main.DebWeil).

The system requirements are broken down into various components
including the server-based CLM applications that are deployed on one or
more servers and various optional tools including connectors,
synchronizers and clients. Server Requirements are futher broken down
into Non-Clustered and Cluster support where applicable.

## A. Server Requirements

### A1. Server Host Operating Systems

#### A1.1 Server OS Non-Clustered Support

The operating systems below may be used to host CLM applications in a
non-clustered environment.

| Server Operating System | CLM Server Support | RRDI Support | Notes |
|:---|:---|:---|:---|
| **AIX 6.1 POWER System** and future OS fixpacks | 64 bit | 64 bit | *See RRC Converter note below* |
| **AIX 7.1 POWER System** and future OS fixpacks | 64 bit | 64 bit | *See RRC Converter note below* |
| **IBM i 6.1 POWER System** and future OS fixpacks | 64 bit | 32 & 64 bit \* | *\* Data Warehouse OnlySee RRC Converter note below* |
| **IBM i 7.1 POWER System** and future OS fixpacks | 64 bit | 64 bit \* | *\* Data Warehouse OnlySee RRC Converter note below* |
| **IBM z/OS System z v1.9** and future OS fixpacks | 64 bit | 32 & 64 bit \* | *\* Cognos Content Store and Data Warehouse Only (Report Server not supported on z/OS)See z/OS note belowSee RRC Converter note below* |
| **IBM z/OS System z v1.10** and future OS fixpacks | 64 bit | 32 & 64 bit \* | *\* Cognos Content Store and Data Warehouse Only (Report Server not supported on z/OS)See z/OS note belowSee RRC Converter note below* |
| **IBM z/OS System z v1.11** and future OS fixpacks | 64 bit | 32 & 64 bit \* | *\* Cognos Content Store and Data Warehouse Only (Report Server not supported on z/OS)See RRC Converter note below* |
| **IBM z/OS System z v1.12** and future OS fixpacks | 64 bit | 32 & 64 bit \* | *\* Cognos Content Store and Data Warehouse Only (Report Server not supported on z/OS)See RRC Converter note below* |
| **IBM z/OS System z v1.13** and future OS fixpacks | 64 bit | 32 & 64 bit \* | *\* Cognos Content Store and Data Warehouse Only (Report Server not supported on z/OS)See RRC Converter note below* |
| **Red Hat Enterprise Linux (RHEL) 5 Update 5 (RHEL) Advanced Platform** and future OS fixpacks | 64 bit | 32 & 64 bit |  |
| **Red Hat Enterprise Linux (RHEL) 5 Update 5 POWER System** and future OS fixpacks | 64 bit | Not Supported |  |
| **Red Hat Enterprise Linux (RHEL) 5 Update 5 System z** and future OS fixpacks | 64 bit | Not Supported |  |
| **Red Hat Enterprise Linux (RHEL) Server 6** and future OS fixpacks | 64 bit | 32 & 64 bit |  |
| **Red Hat Enterprise Linux (RHEL) Server 6 POWER System** and future OS fixpacks | 64 bit | Not Supported |  |
| **Red Hat Enterprise Linux (RHEL) Server 6 System z** and future OS fixpacks | 64 bit | Not Supported |  |
| **Solaris 10 SPARC** and future OS fixpacks | 64 bit | Not Supported | *See RRC Converter note below* |
| **Solaris 11 SPARC** and future OS fixpacks | 64 bit | Not Supported | See RRC Converter note below |
| **SUSE Linux Enterprise Server (SLES) 10 SP2** and future OS fixpacks | 64 bit | 32 & 64 bit |  |
| **SUSE Linux Enterprise Server (SLES) 10 SP2 POWER System** and future OS fixpacks | 64 bit | Not Supported | *See RRC Converter note below* |
| **SUSE Linux Enterprise Server (SLES) 10 SP2 System z** and future OS fixpacks | 64 bit | 64 bit |  |
| **SUSE Linux Enterprise Server (SLES) 11** and future OS fixpacks | 64 bit | 32 & 64 bit |  |
| **SUSE Linux Enterprise Server (SLES) 11 POWER System** and future OS fixpacks | 64 bit | Not Supported | *See RRC Converter note below* |
| **SUSE Linux Enterprise Server (SLES) 11 System z** and future OS fixpacks | 64 bit | 64 bit |  |
| **Windows Server 2003 R2 Enterprise Edition** and future OS fixpacks | Not Supported | 32 & 64 bit | *Windows Server 2003 is supported for RRDI only* |
| **Windows Server 2003 R2 Standard Edition** and future OS fixpacks | Not Supported | 32 & 64 bit | *Windows Server 2003 is supported for RRDI only* |
| **Windows Server 2003 SP2 Enterprise Edition** and future OS fixpacks | Not Supported | 32 & 64 bit | *Windows Server 2003 is supported for RRDI only* |
| **Windows Server 2003 SP2 Standard Edition** and future OS fixpacks | Not Supported | 32 & 64 bit | *Windows Server 2003 is supported for RRDI only* |
| **Windows Server 2008 SP2 Enterprise Edition** and future OS fixpacks | 64 bit | 32 & 64 bit |  |
| **Windows Server 2008 SP2 Standard Edition** and future OS fixpacks | 64 bit | 32 & 64 bit |  |
| **Windows Server 2008 R2 Enterprise Edition** and future OS fixpacks | 64 bit | 32 & 64 bit |  |
| **Windows Server 2008 R2 Standard Edition** and future OS fixpacks | 64 bit | 32 & 64 bit |  |

#### A1.2 Server OS Clustered Support

The operating systems below may be used to run application servers
hosting CLM applications in a clustered environment.

| Server Operating System | CLM Server | RRDI | Notes |
|:---|:---|:---|:---|
| **AIX 6.1 POWER System** and future OS fixpacks | 64 bit | 64 bit | *See RRC Converter note below* |
| **AIX 7.1 POWER System** and future OS fixpacks | 64 bit | 64 bit | *See RRC Converter note below* |
| **Red Hat Enterprise Linux (RHEL) 5 Update 5 (RHEL) Advanced Platform** and future OS fixpacks | 64 bit | 32 & 64 bit |  |
| **Red Hat Enterprise Linux (RHEL) 5 Update 5 POWER System** and future OS fixpacks | 64 bit | Not Supported |  |
| **Red Hat Enterprise Linux (RHEL) Server 6** and future OS fixpacks | 64 bit | 32 & 64 bit |  |
| **Red Hat Enterprise Linux (RHEL) Server 6 POWER System** and future OS fixpacks | 64 bit | Not Supported |  |
| **SUSE Linux Enterprise Server (SLES) 10 SP2** and future OS fixpacks | 64 bit | 32 & 64 bit |  |
| **SUSE Linux Enterprise Server (SLES) 10 SP2 POWER System** and future OS fixpacks | 64 bit | Not Supported | *See RRC Converter note below* |
| **SUSE Linux Enterprise Server (SLES) 11** and future OS fixpacks | 64 bit | 32 & 64 bit |  |
| **SUSE Linux Enterprise Server (SLES) 11 POWER System** and future OS fixpacks | 64 bit | Not Supported | *See RRC Converter note below* |

##### Server Host Operating System Notes

-   *Host Operating Systems are supported on x86-64, POWER, z/OS and
    SPARC hardware. Itanium is not supported.*
-   *CLM requires 64 bit server OS to host CLM applications. 32-bit
    servers are not supported except for small-scale evaluation or
    demonstration purposes.*
-   *The RRC Converter application will ***not*** run on AIX, IBM i,
    Linux for Power, Solaris or z/OS systems. The server-side
    converter.war, needed to view graphical artifacts, must be deployed
    on a supported Windows, x86 Linux or zLinux platform. If your RRC
    installation is on a platform not currently supported by the
    converter application, this document describes the delegated
    converter configuration option: [RM Converter Application
    Configuration and Troubleshooting
    Guide](https://jazz.net/library/article/1089).*
-   *[Recommended Fixes for the Rational Collaborative Lifecycle
    Management applications on z/OS and IBM
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
-   *Reminder - RRDI may be installed on a separate server (platform).
    Additional RRDI platforms are included in the list above.*
-   *"and future OS fixpacks" includes Service Releases (SR's) and
    Updates (RHEL). Fix pack is IBM terminology for a minor release that
    includes fixes (vs. features).*

### A2. Server Virtualization

#### A2.1 VM Support Non-Clustered

Host operating systems may be virtualized using the following
virtualization technologies (VMs are supported for application tier
only):

| Server Virtualization | Operating System(s) | CLM Server Support | RRDI Support | Notes |
|:---|:---|:---|:---|:---|
| IBM PowerVM Hypervisor (LPAR, DPAR, Micro-Partition) any supported version and future fix packs | AIX, IBMi, RHEL & SUSE POWER | 64 bit | Not Supported |  |
| IBM PR/SM any version and future fix packs | RHEL & SUSE System z & z/OS | 64 bit | Not Supported |  |
| IBM z/VM Hypervisor 6.1 and future fix packs | RHEL & SUSE System z & z/OS | 64 bit | Not Supported |  |
| Red Hat KVM as delivered with Red Hat Enterprise Linux (RHEL) 6.0 and future fix packs | RHEL 6 | 64 bit | Not Supported |  |
| Red Hat KVM as delivered with Red Hat Enterprise Linux (RHEL) 5.5 and future fix packs | RHEL 5 | 64 bit | Not Supported |  |
| KVM in SUSE Linux Enterprise Server (SLES) 11 and future fix packs | SUSE 11 | 64 bit | Not Supported | New for 4.0.3 |
| VMware VSphere, ESX and ESXi 4.0 and future fix packs | RHEL, SUSE & Windows Server x86-64 | 64 bit | 32 & 64 bit |  |
| VMware VSphere and ESXi 5.0 and future fix packs | RHEL, SUSE & Windows Server x86-64 | 64 bit | 32 & 64 bit |  |
| VMware ESXi 5.1 and future fix packs | RHEL, SUSE & Windows Server x86-64 | 64 bit | 32 & 64 bit | New for 4.0.2 |

#### A2.2 Conditional VM Support (Non-Clustered)

These additional IBM SWG priority virtualization platforms are
conditionally supported under the following terms: 1 The operating
system being hosted in the virtualized environment must be supported in
a non-virtualized environment 1 Any defects reported are reproducible
outside the virtualization environment 1 Rational Support may not have
access to the virtualization environment and will attempt to reproduce
the issues reported on a non-virtualized environment or one of the
specific virtualization technologies listed above 1 No cluster support
is available for these VM's

| Conditional Server Virtualization | Operating System(s) | CLM Server Support | RRDI Support | Notes |
|:---|:---|:---|:---|:---|
| Microsoft Hyper-V Server 2008 and future fix packs | Win Server 2008 | 64 bit | Not Supported | *Note conditional support terms* |
| Microsoft Hyper-V Server 2008 R2 and future fix packs | Win Server 2008 R2 | 64 bit | Not Supported | *Note conditional support terms* |

#### A2.3 Server Virtualization Clustered Support

Host operating systems may be virtualized for clustering using the
following virtualization technologies:

| Server Virtualization | with Operating System(s) | CLM Server | RRDI | Notes |
|:---|:---|:---|:---|:---|
| IBM PowerVM Hypervisor (LPAR, DPAR, Micro-Partition) any supported version and future fix packs | AIX 6.1, 7.1 | 64 bit | Not Supported |  |

### A3. Memory Requirements

#### CLM Memory Requirements

-   For CLM 4.0 and later you need a 64-bit operating system and a
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

#### RRDI Memory Requirements

-   8 GB RAM. More memory generally improves performance; required
    memory depends on the number of concurrent users, amount of data
    being requested, and the size of the database. Optimum swap space is
    double the physical memory.

### A4. Network Infrastructure

-   IPv6
-   IPv4

### A5. Application Servers ---++++ A5.1 Application Server Non-Clustered Support

The following application servers can be used to host CLM applications
(non-clustered):

| Application Servers | CLM Server | RRDI | Notes |
|:---|:---|:---|:---|
| **Apache Tomcat 7.0.32** and future fixpacks | Supported | Not Supported | New version for 4.0.2 - 7.0.32 \[Tomcat is bundled with CLM\] Note - Tomcat is not supported on IBM i |
| **WebSphere Application Server v7.0.0.23 x86-64** and future fixpacks | Supported | Supported |  |
| **WebSphere Application Server Network Deployment v7.0 Fixpack 23** and future fixpacks | Supported | Supported |  |
| **WebSphere Application Server for z/OS v7.0.0.23** and future fixpacks | Supported | Not Supported |  |
| **WebSphere Application Server OEM Edition for z/OS v7.0 Fixpack 23** and future fixpacks | Supported | Not Supported | \[Bundled with CLM\]Note: There is no v8 for WAS OEM for z/OS |
| **WebSphere Application Server v8.0.0.3 x86-64** and future fixpacks | Supported | Supported | \[WAS 8 is bundled with CLM 4.0.1 and 4.0.2 media\] Please see Note below for BIRT issue. |
| **WebSphere Application Server Network Deployment v8.0.0.3** and future fixpacks | Supported | Supported |  |
| **WebSphere Application Server for z/OS v8.0.0.3** and future fixpacks | Supported | Not Supported |  |
| **WebSphere Application Server v8.5.02 x86-64** and future fixpacks | Supported | Supported | New for 4.0.3 - Non-clustered Only \[CLM 4.0.3 media bundles WAS 8.5. Please see "Bundling" Note below.\]Please also see Note below for BIRT issue. |
| **WebSphere Application Server Network Deployment v8.5.0.2** and future fixpacks | Supported | Supported | New for 4.0.3 - Non-clustered Only |
| **WebSphere Application Server for z/OS v8.5.0.2** and future fixpacks | Supported | Not Supported | New for 4.0.3 - Non-clustered OnlyExcludes the Liberty profile configuration option |
| **WebSphere Application Server - Express 7.0.0.23** and future fixpacks | Not Supported | Supported | Express Edition supported for RRDI Only |
| **WebSphere Application Server - Express 8.0.0.2** and future fixpacks | Not Supported | Supported | Express Edition supported for RRDI Only |

#### A5.2 Application Server Clustered Support

CLM applications can be clustered using the following application
servers:

| Application Servers | CLM Server | RRDI | Notes |
|:---|:---|:---|:---|
| **WebSphere Application Server Network Deployment v7.0 Fixpack 23** and future fixpacks | Supported | Not Supported |  |
| **Websphere Application Server Network Deployment v8.0.0.3** and future fixpacks | Supported | Supported |  |
| **WebSphere eXtreme Scale 7.1.1.1** and future fixpacks | Required | Required | \[WXS 7.1.1 is bundled with CLM media (not on Jazz.net) and required for clustering\] |

##### Application Server Notes

-   WAS and DB2 bundles are only available on Passport Advantage and in
    the CLM Media (not on Jazz.net). Customers upgrading from CLM 3.0.1
    and 4.0 are entitled to continue using WAS 7.0.x and WAS 8.0.x as
    long as CLM supports those versions.
-   WebSphere Application Server support for CLM is 64-bit only to align
    with 64-bit server platforms. RRDI supports both 32 & 64 bit WAS.
-   WAS 8.5 is not supported for Clustering.
-   Clustering is supported with WAS ND (7.0.2.3 or 8.0.0.3) but also
    requires the bundled WXS 7.1.1.1
-   There is a known issue with BIRT reports running WAS 8.0.0.x and
    8.5.0.x please see this [Tech
    Note](http://www-01.ibm.com/support/docview.wss?uid=swg21616615) for
    WAS patch.

Note: CCM BIRT report issues running WAS 8.0.0.5 or 8.5.0.1 please see
technote for patch information.

### A6. Databases

#### A6.1 Database - Non-Clustered Support

The following databases can be used to host CLM applications:

| Database | CLM Server | RRDI | Notes |
|:---|:---|:---|:---|
| **IBM Derby SDK 10.8.1.2** and future fixpacks | 64 bit | Not Supported | For Evaluation purposes only - for small teams of 10 users or less)CLM bundles Derby |
| **IBM DB2 Enterprise Server Edition v9.7** and future fixpacks | 64 bit | 32 & 64 bit | \[CLM media for 4.0.1 and 4.0.2 bundled DB2 9.7 ESE\] |
| **IBM DB2 Workgroup Server Edition v9.7** and future fixpacks | 64 bit | 32 & 64 bit |  |
| **IBM DB2 Express Edition v9.7** and future fixpacks | 64 bit | 32 & 64 bit | (for small teams of 50 users or less) |
| **IBM DB2 Express-C 9.7** and future fixpacks | 64 bit | Not Supported | (for small teams of 25 users or less) |
| **IBM DB2 Enterprise Server Edition v10.1** and future fixpacks | 64 bit | 32 & 64 bit | New for CLM 4.0.3 and bundled with CLM 4.0.3 media |
| **IBM DB2 Workgroup Server Edition v10.1** and future fixpacks | 64 bit | 32 & 64 bit | New for 4.0.3 |
| **IBM DB2 Express Edition v10.1** and future fixpacks | 64 bit | 32 & 64 bit | New for 4.0.3. CLM 4.0.3(for small teams of 50 users or less) |
| **IBM DB2 Express-C 10.1** and future fixpacks | 64 bit | Not Supported | New for CLM 4.0.3(for small teams of 25 users or less) |
| **IBM DB2 for i 6.1** and future fixpacks | 64 bit | Not Supported |  |
| **IBM DB2 for i 7.1** and future fixpacks | 64 bit | Not Supported |  |
| **IBM DB2 9 or z/OS 9.1** and future fixpacks | 64 bit | 32 & 64 bit\* | \* CLM, Cognos Content Store and Data Warehouse only not RRDI Report Server |
| **IBM DB2 for z/OS 10.1** (with PTF UK77844) and future fixpacks | 64 bit | 32 & 64 bit\* | \* CLM, Cognos Content Store and Data Warehouse only. RRDI Report Server not supported. |
| **Microsoft SQL Server Enterprise Edition 2008 SP1** and future fixpacks | 64 bit | 32 & 64 bit |  |
| **Microsoft SQL Server Standard Edition 2008 SP1** and future fixpacks | 64 bit | 32 & 64 bit |  |
| **Microsoft SQL Server Express Edition 2008 SP1** and future fixpacks | 64 bit | Not Supported | CLM,Only. RRDI does not support MS SQL Express Edition |
| **Microsoft SQL Server Enterprise Edition 2008 R2** and future fixpacks | 64 bit | 32 & 64 bit |  |
| **Microsoft SQL Server Standard Edition 2008 R2** and future fixpacks | 64 bit | 32 & 64 bit |  |
| **Oracle Database 10g Enterprise Edition Release 2 10.2.0.1** and future fixpacks | 64 bit | 32 & 64 bit |  |
| **Oracle Database 10g Standard Edition Release 2 10.2.0.1** and future fixpacks | 64 bit | 32 & 64 bit |  |
| **Oracle Database 11g Enterprise Edition Release 2 11.2.0.2** and future fixpacks | 64 bit | 32 & 64 bit | Requires Oracle Java Database Connectivity (JDBC) ojdbc6.jar.11.2.0.3 or higher |
| **Oracle Database 11g Standard Edition Release 2 11.2.0.2** and future fixpacks | 64 bit | 32 & 64 bit | Requires Oracle Java Database Connectivity (JDBC) ojdbc6.jar.11.2.0.3 or higher |
| **Oracle Real Application Clustering (Oracle 11g Release 2)** and future fixpacks | 64 bit | 64 bit | Oracle RAC for High Availability (independent of clustering support) Requires Oracle Java Database Connectivity (JDBC) ojdbc6.jar.11.2.0.3 or higher New for 2.0.3 - RRDI support for Oracle RAC |
| **IBM DB2 Enterprise Server Edition v9.5** and future fixpacks | Not Supported | 32 & 64 bit | DB2 9.5 is supported for RRDI Only |
| **IBM DB2 Workgroup Server Edition v9.5** and future fixpacks | Not Supported | 32 & 64 bit | DB2 9.5 is supported for RRDI Only |
| **IBM DB2 Express Edition v9.5** and future fixpacks | Not Supported | 32 & 64 bit | DB2 9.5 is supported for RRDI Only |
| **Microsoft SQL Server Enterprise Edition 2005 SP4** and future fixpacks | Not Supported | 32 & 64 bit | RRDI Only. CLM does not support MS SQL 2005 |
| **Oracle Database 11g Enterprise Edition Release 1** and future fixpacks | Not Supported | 32 & 64 bit | RRDI Only (supports 11g Release 1) |
| **Oracle Database 11g Standard Edition Release 1** and future fixpacks | Not Supported | 32 & 64 bit | RRDI Only (supports 11g Release 1) |

#### A6.2 High Availability Database Support

When clustering we also suggest setting up High Availability support
with these databases:

-   **DB2 9.7 HADR** DB2 HADR is included with Enterprise Server Edition
    but requires additional DB2 licenses for anything other than cold
    standby. See note below.
-   **DB2 10.1 HADR** New for CLM 4.0.3 DB2 HADR is included with
    Enterprise Server Edition but requires additional DB2 licenses for
    anything other than cold standby. See note below.
-   **DB2 9 for z/OS 9.1**
-   **DB2 10 for z/OS 10.1** (with PTF UK77844)
-   **Oracle Real Application Clustering** (Oracle 11g Release 2)

##### Database Support Notes

-   Database support is 64-bit only to align with 64-bit server
    platforms.
-   WAS and DB2 bundles are only available on Passport Advantage and in
    the CLM Media (not on Jazz.net). Customers upgrading from CLM 3.0.1
    and 4.0.X are entitled to continue using DB2 9.7 as long as CLM
    supports that version.
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
-   Oracle is not supported for System z or IBM i
-   SQL Server is supported on Windows Server only

### A7. Eclipse (Server)

-   Eclipse SDK 3.6.2.3 (Eclipse Runtime, Equinox and EMF) \[Bundled\]

### A8. HTTP Reverse Proxy Support (Non-Clustered)

-   Apache Server 2.2.19 on RHEL and SLES \[Non-secure Only (no HTTPS)\]
-   IBM HTTP Server 7.0 Fixpack 23
-   IBM HTTP Server 8.0.0.3
-   IBM HTTP Server 8.5.0.2 BLUENew for CLM 4.0.3ENDCOLOR

<!-- -->

-   WebSphere Application Server Network Deployment v7.0 Fixpack 23
-   Websphere Application Server Network Deployment v8.0.0.3
-   Websphere Application Server Network Deployment v8.5.0.2 BLUENew for
    CLM v4.0.3ENDCOLOR
-   Squid 3.3.3 for caching (see [Using content caching proxies for Jazz
    Source
    Control](https://jazz.net/wiki/bin/view/Deployment/ContentCachingProxyJazzSCM))

### A9. Java Runtime Environment (Server)

| JRE | CLM Server | RRDI | Notes |
|:---|:---|:---|:---|
| **IBM Java SDK 6.0.1.5 (J9 2.6)** and future fixpacks | Supported | Not Supported | for z/OS |
| **Java 6 64 bit for IBM i V6R1 and V7R1** and future fixpacks | Supported | Not Supported | for IBM i - PTF SI49257 |
| **IBM Java SDK 6.0.13.1** and future fixpacks | Supported | Supported | CLM 4.0.1 bundled Java 6 SR11New version for CLM 4.0.3 Java 6 SR 13 FP1 |
| **Sun Java SDK/JRE/JDK 6.0 Update 23** and future fixpacks | Supported | Not Supported | RRDI does not support Sun/Oracle Java |

### A10. Identity Management

-   Apache Directory Server 1.5.5
-   IBM Resource Access Control Facility (RACF) as bundled with all
    supported z/OS versions listed above
-   IBM Tivoli Directory Server 6.3
-   Microsoft Active Directory 2008
-   Microsoft Active Directory 2008 R2

### A11. Installation Manager

-   IBM Installation Manager 1.6.3 \[Bundled\] CLM 4.0.1 bundled Install
    Manager 1.6.1 New for CLM 4.0.3 - media will bundle 1.6.3 For shell
    sharing with Rational Application Developer 9 please upgrade to IM
    1.6.3.1

### A12. License Server

-   Rational Common License 8.1.3 New for CLM 4.0.3. CLM media bundles
    RCLM 8.1.3 Server

### A13. Report Customization

-   Rational Reporting for Development Intelligence 2.0.3 \[Bundled\]CLM
    4.0.1 bundled RRDI 2.0.1 New for CLM 4.0.3 - RRDI 2.0.3

### A14. Load Balancer for Clustering

-   IBM HTTP Server 8.0
-   IBM HTTP Server 7.0 Fixpack 23
-   Websphere Application Server Network Deployment v8.0.0.3
-   WebSphere Application Server Network Deployment v7.0 Fixpack 23

## B. **Client Requirements**

-   **Reminder: The platforms listed below are the starting point for
    CLM support and unless otherwise indicated support includes this
    level and all future OS fixpacks. For RedHat Updates are equivalent
    to fix packs**

### B1. Client Operating Systems

| Client Operating System | RTC Eclipse Client | DNG Rich Client | RTC client for Visual Studio | RTC zLinux Client | Web Clients (Browsers) | Notes |
|:---|:---|:---|:---|:---|:---|:---|
| **Red Hat Enterprise Linux (RHEL) Desktop 5 Update 5 x86-32, x86-64** and future OS fixpacks | 32 bit | Windows Only | Windows Only | zLinux Only | Supported | Please see Client OS Notes below |
| **Red Hat Enterprise Linux (RHEL) Client 6 x86-32, x86-64** and future OS fixpacks | 32 & 64 bit | Windows Only | Windows Only | zLinux Only | Supported | Please see Client OS Notes below |
| **Red Hat Enterprise Linux (RHEL) Workstation 6 x86-32, x86-64** and future OS fixpacks | 32 & 64 bit | Windows Only | Windows Only | zLinux Only | Supported | Please see Client OS Notes below |
| **SUSE Linux Enterprise Desktop (SLED) 10.0 SP3 x86-32, x86-64** and future OS fixpacks | 32 & 64 bit | Windows Only | Windows Only | zLinux Only | Supported | Please see Client OS Notes below |
| **SUSE Linux Enterprise Desktop (SLED) 11.0 x86-32, x86-64** and future OS fixpacks | 32 & 64 bit | Windows Only | Windows Only | zLinux Only | Supported | Please see Client OS Notes below |
| **Mac OS X Snow Leopard 10.6 x86-32, x86-64** and future OS fixpacks | 32 & 64 bit | Windows Only | Windows Only | zLinux Only | Supported |  |
| **Mac OS X Lion 10.7 x86-32, x86-64** and future OS fixpacks | 32 & 64 bit | Windows Only | Windows Only | zLinux Only | Supported |  |
| **Ubuntu Desktop 10.04 LTS x86-64** this version only | 32 & 64 bit | Windows Only | Windows Only | zLinux Only | Supported | This version is out of support from Ubuntu. Please see Client OS Notes below |
| **Ubuntu Desktop 12.04 LTS x86-64** this version only | 32 & 64 bit | Windows Only | Windows Only | zLinux Only | Supported | BLUENew for RTC v4.0.4 (**Supported for RTC Only)ENDCOLORPlease see xlrunner in Client OS Notes below \| **Windows XP Professional SP2 x86-32, x86-64** and future OS fixpacks \| 32 & 64 bit \| 32 bit Only \| 32 & 64 bit \| zLinux Only \| Supported \| \| \| **Windows Vista SP2 Business x86-32, x86-64** and future OS fixpacks \| 32 & 64 bit \| in 32 bit mode only \| 32 & 64 bit \| zLinux Only \| Supported \| \| \| **Windows Vista SP2 Enterprise x86-32, x86-64** and future OS fixpacks \| 32 & 64 bit \| in 32 bit mode only \| 32 & 64 bit \| zLinux Only \| Supported\| \| \| **Windows Vista SP2 Ultimate x86-32, x86-64** and future OS fixpacks \| 32 & 64 bit \| in 32 bit mode only \| 32 & 64 bit \| zLinux Only \| Supported \| \| \| **Windows 7 Enterprise x86-32, x86-64** and future OS fixpacks \| 32 & 64 bit \| in 32 bit mode only \| 32 & 64 bit \| zLinux Only \| Supported \| \| \| **Windows 7 Professional x86-32, x86-64** and future OS fixpacks \| 32 & 64 bit \| in 32 bit mode only \| 32 & 64 bit \| zLinux Only \| Supported \| \| \| **Windows 7 Ultimate x86-32, x86-64** and future OS fixpacks \| 32 & 64 bit \| in 32 bit mode only \| 32 & 64 bit \| zLinux Only \| Supported \| \| \| **Red Hat Enterprise Linux (RHEL) 5 Update 5 Advanced Platform System z** and future OS fixpacks \| NA \| NA \| NA \| 64 bit \| NA \| RTC zLinux Client only \| \| **Red Hat Enterprise Linux (RHEL) Server 6 System z** and future OS fixpacks \| NA \| NA \| NA \| 64 bit \| NA \| RTC zLinux Client only \| \| **SUSE Linux Enterprise Server (SLES) 10 SP2 System z** and future OS fixpacks \| NA \| NA \| NA \| 64 bit \| NA \| RTC zLinux Client only \| \| **SUSE Linux Enterprise Server (SLES) 11 System z** and future OS fixpacks \| NA \| NA \| NA \| 64 bit \| NA \| RTC zLinux Client only \| \| **Windows XP Professional (no SP) x86-32, x86-64** and future OS fixpacks \| Not Supported \| Not Supported \| Not Supported \| zLinux Only \| Supported** |

#### Client Operating System Notes

-   If you are running the Eclipse client on Linux please ensure that
    you have a compatible xulrunner or webkitgtk installed and
    configured on your system. Failure to do so can result in various
    issues including failure to start. See
    [Article](https://jazz.net/library/article/952) for additional
    details and instructions.
-   Smart Card Support for ALL CLM Products (Windows Only)
-   MAC OSX is supported for RTC, RQM and RRC Only (not DNG or RRDI)
-   SLED 10 is no longer supported for RRDI, and for the RTC Eclipse
    Client using IES 4.2.2. This platform is out of support from SUSE.

### B2. Browsers

\| **Browser** \| **CLM Web Client** \| **DNG** \| **RRDI** \| **Notes**
\| \| **Apple Safari 5.1** and future fixpacks \| Supported \| Supported
\| Not Supported \| Please see note below for RM Graphical Editors \| \|
**Firefox 10 ESR** and future fixpacks \| Not Supported \| Not Supported
\| Not Supported \| Dropped in CLM 4.0.3 - Firefox 10ESR is out of
service from Mozilla \| \| **Firefox 17 ESR** and future fixpacks \|
Supported \| Supported \| Supported \| New for CLM 4.0.2 - Please see
4.0.2 Release Notes for known issues and workarounds \| \| **Google
Chrome 21** and future releases, mod levels and fixpacks \| Supported \|
Supported \| Not Supported \| Please see notes below for mixed
http/https content and RM Graphical Editors. \| \| **Internet Explorer
8** and future fixpacks \| Supported \| Supported \| Supported \| Please
note IE8 is not supported for the RTC Eclipse Client on 64-bit Windows
please use IE9. Please see additional known issues and workarounds for
IE8 in this [article](https://jazz.net/library/article/928) \| \|
**Internet Explorer 9** and future fixpacks \| Supported \| Supported \|
Supported \| \|

#### Browser Support Notes

-    BLUEPlease see these tech note articles for [mixed http/https
    content](http://www-01.ibm.com/support/docview.wss?uid=swg21653966)
    and [self-signed
    certificates](http://www-01.ibm.com/support/docview.wss?uid=swg21654984)
    which may result in content not being shown as expected. ENDCOLOR
-   The RRC and DOORS NG Graphical Editor is supported in 32-bit mode
    using Internet Explorer and Firefox on Windows (Only). Chrome and
    Safari browsers will show graphical artifacts in preview mode, but
    will not support editing.
-   Macromedia Flash Player 10,11\* and future releases, mods and
    fixpacks is supported for graphical view in Work Item Statistics
    dashboard viewlet

### B3. Eclipse IDE (RTC Eclipse Client)

| IES | Notes |
|:---|:---|
| **IBM Eclipse SDK 3.6.2.3** and future fixpacks | IES 3.6.2.3 is bundled with the RTC client |
| **IBM Eclipse SDK 3.7.2** and future fixpacks |  |
| **IBM Eclipse SDK 4.2.2** and future fixpacks | BLUENew for CLM v4.0.3. CLM v4.0.3 and later includes two RTC Client installs for IES 3.6.2.3 and 4.2.2. Note IES 4.2.2 is not supported on SLES 10ENDCOLOR. |

#### Eclipse IDE Notes

\* If you are installing the Rational Team Concert Client into an
existing instance of Eclipse IDE 3.6, please read [this
technote](https://www-304.ibm.com/support/docview.wss?rs=3488&uid=swg21502374&wv=1).\*

### B4. Runtime Enviroments (RTC Only)

| Runtime | Notes |
|:---|:---|
| **Microsoft Visual Studio 2005 SP1 with .NET 3.5 SP1** and future fixpacks | for RTC client for Visual Studio |
| **Microsoft Visual Studio 2010 with .NET 4.0** and future fixpacks | for RTC client for Visual Studio |

### B5. Java SDK (RTC Eclipse Client)

-   IBM Java SDK 6.0.13.1\* and future fixpacks New for 4.0.3 - The RTC
    client move to Java 6 SR13 FP1
-   IBM Java SDK 7.0 SR1\* and future fixpacks
-   Sun Java SDK/JRE/JDK 6.0 Update 23\* and future fixpacks
-   Oracle Java SDK/JRE/JDK 7\* and future fixpacks

#### Java Runtime Notes

\*FYI - the DOORS Client is based on C++ (and DXL) not Java based.

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
| Server | Compatible Clients |  | CLM 4.0.x Server | RTC Eclipse Client v4.0.y, (x\>=y)RTC Eclipse Client v3.0.y or Later |  |  | RTC VS.Net Client v.4.0.y, x\>=y VS.Net Client v.3.0.y or later |  |  | RTC SCM CLI v.4.0.y, x\>=y RTC SCM CLI v.3.0.y or later |
|  | RTC ISPF Client v.4.0.y, x\>=y RTC ISPF Client v.3.0.y or later |  |  |  |  |  |  |  |  |  |
|  | RTC Windows Shell Client v.4.0.y, x \>=y (this was introduced in 4.0) |  |  |  |  |  |  |  |  |  |
|  | RTC MSSCCI Provider v.4.0.y, x \>=y (this was introduced in 4.0) |  |  |  |  |  |  |  |  |  |

### C2. RTC Build System Toolkit

-   The Build System Toolkit is a client that can also be run on Server
    Operating Systems. It is supported on all CLM Server (Host Operating
    Systems) and all the RTC Eclipse Client platforms. For the RTC
    Eclipse client platforms there is an Installation Manager install.
    For all other platforms there are Plain Zips.

### C3. RTC SCM Command-Line Tool

-   The SCM Command-Line Tool is supported on all Server Platforms
    except for IBM i.

### C4. RTC ISPF Client and ISPF Gateway

-   The Rational Team Concert ISPF Client is supported on all zOS
    platforms as specified under Server Operating Systems.
-   The Rational Team Concert ISPF client requires cURL, an open source
    tool supplied through IBM Ported Tools Supplementary Toolkit for
    z/OS. Information on IBM Ported Tools can be found at: [IBM Ported
    Tools for z/OS Product and Feature
    Information](http://www.ibm.com/systems/z/os/zos/features/unix/ported/).
    If you already have IBM Ported Tools installed, cURL for z/OS is
    available by ordering the PTF for APAR OA22944. Information on the
    Supplementary Toolkit for z/OS can be found at [Supplement Toolkit
    for
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

### C5. Rational Team Concert (RTC) Shell Client (introduced in v4.0)

-   The RTC Shell is distributed as a downloadable file through IBM
    Installation Manager.
-   Only Windows XP (32-bit) and Windows 7 (both 32-bit and 64-bit)
    operating systems are supported.
-   RTC Shell requires Microsoft Visual C++ 2010 x64 Redistributable
    package for 64-bit systems or Microsoft Visual C++ 2010 x86
    Redistributable package for 32-bit systems. The .NET Framework 3.5,
    SP1 is also required.

### C6. Rational Team Concert (RTC) MSSCCI Provider (introduced in v4.0)

-   The RTC MSSCCI Provider is distributed as a downloadable file
    through IBM Installation Manager.
-   Only Windows XP (32-bit) and Windows 7 (both 32-bit and 64-bit)
    operating systems are supported. On Windows 7 (64-bit), MSSCCI
    provider only integrates with applications running in 32-bit mode.
-   RTC MSSCCI Provider requires that the Microsoft .NET framework
    version 3.5 SP1 and Microsoft Visual C++ 2010 x86 Redistributable
    package (32-bit) are pre-installed.

### C7. Rational ClearQuest (CQ) Synchronizer Gateway ---++++ C7.1 CQ Synchronizer Server Operating Systems (Non-Clustered Only)

The following application servers can be used to host the synchronizer
gateway:

| Server Operating System | Bits | Notes |
|:---|:---|:---|
| **Windows Server 2003 R2 Enterprise/Web Edition/Standard Edition** and future fixpacks | 64 bit |  |
| **Windows Server 2003 R2 SP2 Enterprise/Web Edition/Standard Edition** and future fixpacks | 64 bit |  |
| **Windows Server 2008 R2 Enterprise/Standard** and future fixpacks | 64 bit |  |
| **Windows Server 2008 R2 SP1/SP2 Enterprise/Standard** and future fixpacks | 64 bit |  |
| **Red Hat Enterprise Linux (RHEL) 5 Update 5 (RHEL) x86-64** and future fixpacks | 64 bit |  |
| **Red Hat Enterprise Linux (RHEL) Server 6 x86-64** and future fixpacks | 64 bit |  |
| **SUSE Linux Enterprise Server (SLES) 10 SP3 x86-64** and future fixpacks | 64 bit |  |
| **SUSE Linux Enterprise Server (SLES) 11 SP1 x86-64** and future fixpacks | 64 bit |  |

##### *CQ Synchronizer Gateway Server Host Operating System Notes*

-   The ClearQuest Synchronizer Setup Wizard is not supported on Linux.
-   The ClearQuest client is required to install the Sychronizer Gateway
    on the host server.
-   CQ must be 7.1.2 or later. Please consult the [system requirements
    for
    ClearQuest](http://www-01.ibm.com/support/docview.wss?uid=swg27023170)
    here.

#### C7.2 CQ Synchronizer Gateway Memory Requirements

-   Minimum of 4 GB. Recommend 8 GB RAM. More memory generally improves
    performance.

#### C7.3 CQ Sycnronizer Gateway Application Server(s) (Non-Clustered Only)

-   Apache Tomcat 7 \[Bundled\] New version for CLM 2012

#### C7.4 CQ Synchronizer Gateway Java Runtime Environment

-   IBM Java SDK 6.0 SR10 FP1 and future fixpacks \[Bundled\]

## D. CLM Integrations, Migrations and Adapters

CLM appliucations integrate with each of the products listed below.

### D1. CLM Products Integrating With One Another

-   For 4.0.x versions all CLM products must be at the same 4.0.x level.
    If one product is upgraded to a new 4.0.x then all products must be
    upgraded whether they share a JTS or not.
-   The 4.0.x products can be integrated with products in the 3.0.x
    release as shown in the following table. Note that this excludes DNG
    which only integrates with other 4.0.x products at the same version
    level as DNG.
-   CLM v3.0.1.6 included critical fixes for high priority security
    issues so that version is recommended but not required.

| Integration | RTC | RQM | RRC | DNG | Notes |
|:---|:---|:---|:---|:---|:---|
| **IBM Rational Team Concert 3.0.1** and future fix packs | NA | Supported | Supported | Not Supported |  |
| **IBM Quality Manager 3.0.1** and future fix packs | Supported | NA | Supported | Not Supported |  |
| **IBM Rational Requirements Composer 3.0.1** and future fix packs | Supported | Supported | NA | Not Supported |  |

### D2. Integrations

| Capability Group | Integration | with RTC | with RQM | with RRC | with DNG | Notes |
|:--:|---:|:--:|:--:|:--:|:--:|:--:|
| Architecture & Design | **IBM Rational Rhapsody 7.6** and future mod levels and their fix packs | Supported | Supported | NA | NA | Rhapsody integrates with RTC & RQM Only |
|  | **IBM Rational Rhapsody 8.0** and future fix packs | Supported | Supported | NA | NA | Rhapsody integrates with RTC, RQM |
|  | **IBM Rational Rhapsody Design Manager 4.0** and future mod levels and their fix packs | Supported | Supported | NA | Supported | Rhapsody DM integrates with RTC, RQM, RRC & DNG. DNG's rich client support is limited to viewing and navigating OSLC links. Use the web client for creating and deleting OSLC links. |
|  | **IBM Rational Software Architect Design Manager 4.0** and future mod levels and their fix packs | Supported | Supported | Supported | Supported | RSA DM integrates with RTC, RQM, RRC, DNG. Note: DNG only integrates with a clean (vs upgraded) install of Rhapsody DM 4.0.1 or 4.0.2. DNG's rich client support is limited to viewing and navigating OSLC links. Use the web client for creating and deleting OSLC links. |
|  | **IBM Rational Software Architect 8.5** and future mod levels and their fix packs | Supported | NA | NA | NA | RSA integrates with RTC only |
|  | **IBM Rational Software Architect for WebSphere Software 8.5** and future mod levels and their fix packs | Supported | NA | NA | NA | RSA integrates with RTC only |
|  | **IBM Rational Software Architect RealTime Edition 8.5** and future fix packs | Supported | NA | NA | NA | RSA integrates with RTC only |
| Asset Management | **IBM Rational Asset Manager Enterprise Edition 7.5.1** and future fix packs, mod levels and their fix packs | Supported | Supported | Supported | NA | RAM integrates with RTC, RQM, RRC |
|  | **IBM Rational Asset Manager Standard Edition 7.5.1** and future fix packs, mod levels and their fix packs | Supported | Supported | Supported | NA | RAM integrates with RTC, RQM, RRC |
| Change and Release Management | **Rational Change 5.3** and future mod levels and their fix packs | Supported | Supported | Supported | NA | Change and Synergy are closely linked and share the same repository. Change integrates with RTC, RQM, RRC. For RTC that integration is made via Rational Synchronization Server. For the RQM and RRC integrations Change uses OSLC.Note: DNG's rich client support is limited to viewing and navigating OSLC links. Use the web client for creating and deleting OSLC links |
|  | **Rational Synergy 7.2** and future mod levels and their fix packs | Supported | Supported | NA | NA | Synergy integrates with RTC and RQM. Synergy integrates with RTC via Rational Synergy For Rational Team Concert Interface. |
|  | **IBM Rational Clearquest 7.1.2\*** and future fix packs | Supported | Supported | Supported | NA | CQ 7.1.2 integrates with RTC, RQM, RRC |
|  | **IBM Rational Clearquest 8.0** and future mod levels and their fix packs | Supported | Supported | Supported | Supported | CQ 8.0 integrates with RTC, RQM, RRC, DNG.Note: DNG's rich client support is limited to viewing and navigating OSLC links. Use the web client for creating and deleting OSLC links |
| Collaboration | **Rational Lifecycle Integration Adapters 1.0** and future fix packs | Supported | Supported | Supported | Supported | RLIA enables integrations with Jira, GIT and HPQC. |
|  | **Atlassian JIRA 4.4.x** and future fix packs | Supported | Supported | Supported | NA | Jira integrates with RTC, RRC and RQM via RLIA. |
|  | **Git 1.7.1** and future fix packs | Supported | NA | NA | NA | GIT integrates with RTC via RLIA. |
|  | **HP Quality Center 11.0** and future fix packs | Supported | NA | Supported | Supported | HPQC integrates with RTC, RRC & DNG via RLIA. Note: DNG's rich client support is limited to viewing and navigating OSLC links. Use the web client for creating and deleting OSLC links. |
|  | **IBM Lotus Connections 3.0, 3.0.1** and future fix packs | Supported | NA | NA | NA | Lotus Connections integrates with RTC only |
|  | **IBM Lotus Connections 4.0, 4.5** and future fix packs | Supported | NA | NA | NA | Lotus Connections integrates with RTC only. Please note that this integration supports form based auth, but not OAuth which means that the integration is not supported on the IBM SmartCLoud |
| Configuration Management | **IBM Rational Build Forge Enterprise, Enterprise Plus & Standard Editions 7.1.1.4** and future fix packs | Supported | Supported | NA | NA | BF integrates with RTC only |
|  | **IBM Rational Build Forge Enterprise, Enterprise Plus & Standard Editions 7.1.2** and future fix packs, mod levels and their fix packs | Supported | Supported | NA | NA | BF integrates with RTC only |
|  | **IBM Rational ClearCase 7.1.2** and future fix packs | Supported | NA | NA | NA | CC integrates with RTC only |
|  | **IBM Rational ClearCase 8.0** and future fix packs, mod levels and their fix packs | Supported | NA | NA | NA | CC integrates with RTC only |
| Connectors | **IBM Rational Connector for SAP Solution Manager 4.0** and future fix packs | Supported | Supported | NA | NA | SAP Connector integrates with RTC, RQM |
| Development Tools | **Rational Application Developer for WebSphere Software 8.5** and future mod levels and their fix packs | Supported | NA | NA | NA | RAD integrates with RTC only |
|  | **Rational Application Developer for WebSphere Software 9** and future mod levels and their fix packs | Supported | NA | NA | NA | RAD 9 integrates with RTC 4.0.3 and future mod releases and fixpacks |
|  | **IBM Rational Business Developer 8.5** and future fix packs | Supported | NA | NA | NA | RBD integrates with RTC only |
|  | **IBM Rational Developer for Power System Software 8.5** and future mod levels and their fix packs | Supported | NA | NA | NA | The RD Power integration is specific to the EE features in RTC. |
|  | **IBM Rational Developer for System z 8.5** and future fix packs | Supported | NA | NA | NA | RDz integrates with RTC only |
|  | **IBM Rational Programming Patterns 8.5** and future mod levels and their fix packs | Supported | NA | NA | NA | RPP integrates with RTC only |
| Instant Messaging | **IBM Lotus Sametime Standard 8.0** and future mod levels and their fix packs | Supported | NA | NA | NA | Sametime integrates with RTC only |
|  | **IBM Lotus Sametime Standard 8.5** and future fix packs | Supported | NA | NA | NA | Sametime integrates with RTC only. |
|  | **Jabber Openfire 3.4.1** and future fix packs | Supported | NA | NA | NA | Jabber integrates with RTC only |
| Process Management | **IBM Rational Method Composer 7.5.2** and future fix packs | Supported | NA | NA | NA | RMC integrates wtih RTC only |
| Project Management | **IBM Rational Focal Point 6.5.2** and future fix packs, mod levels and their fix packs | Supported | NA | Supported | NA | Focal Point integrates with RTC, RRC |
| Reporting and Analysis | **IBM Rational Insight 1.1.1.2** and future fix packs | Supported | Supported | Supported | Supported | Note - A schema change was made in 1.1.1.2 for additional reporting in RQM so this new version of Insight is required for integrating with CLM 4.0.3 and later fixpacks and Mod releases |
|  | **IBM Rational Publishing Engine 1.1.1 and 1.2** and future fix packs, mod levels and their fix packs | Supported | Supported | Supported | Supported | RPE integrates with RTC, RQM, RRC, DNG |
| Requirements Management | **IBM Rational DOORS 9.3, 9.4, 9.5** and future mod levels and their fix packs | Supported | Supported | NA | NA | DOORS 9.3 & 9.4 integrate with RTC and RQM. FYI - DOORS 9.5 bundles the DNG app. DOORS 9.3 and earlier, you can integrate DOORS and RQM by using RQMi. For additional information see: <https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.rational.test.qm.doc/topics/t_ovw_int_rqm_doors.html&scope=null> Starting in DOORS 9.4, you can integrate DOORS and RQM by using the OSLC specification. For additional information see: <https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.rational.test.qm.doc/topics/t_ovw_int_rqm_doors.html&scope=null> |
|  | **IBM Rational DOORS Web Access 1.4.0.0 and 1.5.00** and future mod levels and their fix packs | Supported | Supported | NA | NA | DWA 1.4 and 1.5 integrate with RTC and RQM. RRC and DNG integrate with DWA 1.5 Only. FYI - DWA 1.4 ships with DOORS 9.3 and DWA 1.5 ships with DOORS 9.4 |
|  | **IBM Rational DOORS Web Access 9.5** and future mod levels and their fix packs | Supported | Supported | Supported | Supported | DWA 9.5 integrates with RTC, RQM, RRC & DNG. |
| Security Management | **IBM Rational AppScan Enterprise Edition 8.5** and future mod levels and their fix packs | Supported | Supported | NA | NA | AppScan Enterprise integrates with RTC,RQM |
|  | **IBM Security AppScan Enterprise Edition 8.6** and future mod levels and their fix packs | Supported | Supported | NA | NA | formerly Rational AppScan EnterpriseAppScan Enterprise integrates with RTC,RQM |
|  | **IBM Rational AppScan Source Edition 8.5** and future mod levels and their fix packs | Supported | NA | NA | NA | AppScan Source integrates with RTC only |
|  | **IBM Security AppScan Source Edition 8.5** and future mod levels and their fix packs | Supported | NA | NA | NA | formerly Rational AppScan SourceAppScan Source integrates with RTC only |
| Systems Engineering | **IBM Rational Engineering Lifecycle Manager 1.0** and future releases, mod levels and fix packs | Supported | Supported | NA | NA | RELM integrates with RTC, RQM |
| Test Tools | **Rational Functional Tester 8.5** and future fix packs, mod levels and their fix packs | Supported | Supported | NA | NA | RFT integrates with RTC, RQM |
|  | **IBM Rational Performance Tester 8.1.1.4 and 8.3** and and future mod levels and their fix packs | Supported | Supported | NA | NA | RPT integrates with RTC, RQM |
|  | **IBM Rational Service Tester for SOA Quality 8.2.1 and 8.3** and future fix packs | Supported | Supported | NA | NA | SOA Tester integrates with RTC, RQM |
|  | **IBM Rational Robot 7.0.3** and future fix packs, mod levels and their fix packs | NA | Supported | NA | NA | Robot integrates with RQM only |
|  | **IBM Rational Test RealTime 8.0** and future mod levels and their fix packs | Supported | Supported | NA | NA | TestRT integrates with RTC, RQM |

### D3. Migration Support

| Capability Group | Migration From | to RQM | to RRC | Notes |
|:---|:---|:---|:---|:---|
| Test Artifacts | **IBM Rational Clearquest 7.1.2** and future fix packs | CQ TM artifacts to RQM | NA |  |
|  | **IBM Rational Clearquest 8.0** and future mod levels and their fix packs | CQ TM artifacts to RQM | NA |  |
|  | **IBM Rational Manual Tester 7.0.1** and future fix packs | RMT aftifacts to RQM | NA |  |
|  | **IBM Rational Test Manager 7.0.2** and future fix packs | TM aftifacts to RQM | NA |  |
|  | **IBM Rational Test RealTime 8.0** and future fix packs | TestRT aftifacts to RQM | NA |  |
| Requirements | **IBM Rational RequisitePro 7.1.3** and future mod levels and fix packs | NA | ReqPro Requirements to RRC |  |

### D4. Test Tool Adapters

-   IBM Rational Functional Tester 8.2.2 and 8.3\* and future fix packs,
    mod levels and their fix packs
-   IBM Rational Performance Tester 8.2.1.4 and 8.3\* and future fix
    packs, mod levels and their fix packs
-   IBM Rational Service Tester for SOA Quality 8.2.1 and 8.3\* and
    future fix packs, mod levels and their fix packs
-   IBM Security AppScan Enterprise Edition 8.6\* and future mod levels
    and their fix packs
-   IBM Rational Robot 7.0.3\* and future fix packs, mod levels and
    their fix packs
-   IBM Rational Test RealTime 8.0\* and future mod levels and their fix
    packs

## E. Related Articles

-   [Collaborative Lifecycle Management 2012 Sizing
    Guide](https://jazz.net/wiki/bin/view/Deployment/SizingReportCLM2012)
-   [Rational Requirements Composer 4.0 performance and tuning
    guide](https://jazz.net/library/article/844)
-   [IBM Rational Doors Next Generation 4.0.1 Performance
    Report](https://jazz.net/library/article/1216)
-   [Performance comparison: Rational Requirements Composer versions 4.0
    and 4.0.1](https://jazz.net/library/article/1232)
-   [Rational Team Concert 4.x performance tuning guide for
    z/OS](https://jazz.net/library/article/817)

## F. Summary of Updates by Release

-   New for 4.0.2:
    -   Tomcat 7.0.32
    -   FireFox 17ESR
    -   VMWare ESXi 5.1

<!-- -->

-   New for 4.0.3:
    -   KVM SUSE 11
    -   WAS 8.5
    -   DB2 10.1
    -   Java 6 SR 13 FP1
    -   IES 4.2.2 (RTC Client Only)
    -   Install Manager 1.6.3
    -   Rational Licensing Server 8.1.3

<!-- -->

-   New for 4.0.4:
    -   Ubuntu 12.0.4
