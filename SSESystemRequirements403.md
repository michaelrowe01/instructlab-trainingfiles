META:TOPICINFO{author="sbeard" date="1386849802" format="1.1"
version="1.9"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# System Requirements for Systems and Software Engineering 4.0.3 DKGRAY ***(Rational DOORS and DOORS Web Access, Rational DOORS Next Generation, Rational Team Concert, Rational Quality Manager, Rational Rhapsody, Rational Rhapsody Design Manager, Rational Engineering Lifecycle Manager)*** [system-requirements-for-systems-and-software-engineering-4.0.3-dkgray-rational-doors-and-doors-web-access-rational-doors-next-generation-rational-team-concert-rational-quality-manager-rational-rhapsody-rational-rhapsody-design-manager-rational-engineering-lifecycle-manager]

Authors: [Nancy Leduc](Main.NancyLeduc) Build basis: SSE 4.0.3 ENDCOLOR

TOC{title="Page contents"}

For a short list of track changes to this article please see the bottom
of this article.

-   This is the list of system requirements for **Rational systems and
    software engineering (SSE)** 4.0.3 incorporating:
    -   Rational DOORS and DOORS Web Access (DWA)
    -   Rational DOORS Next Generation (DNG)
    -   Rational Team Concert (RTC)
    -   Rational Quality Manager (RQM)
    -   Rational Rhapsody
    -   Rational Rhapsody Design Manager
    -   Rational Engineering Lifecycle Manager (RELM)
-   Questions? Please contact [Nancy Leduc](Main.NancyLeduc)

The system requirements are broken down into various components. These
are the most commonly supported platforms and middleware, for additional
options please refer to the individual product system requirements. For
recommended deployment topologies please refer to:
<https://jazz.net/wiki/bin/view/Deployment/RecommendedSSEDeploymentTopologies>

## A. Server Requirements

### A1. Server Host Operating Systems

#### A1.1 Server Support

The operating systems below may be used to host SSE applications.

| Server Operating System | Server Version | Notes |
|:---|:---|:---|
| **Red Hat Enterprise Linux (RHEL) Server 6** and future OS fixpacks | 64 bit |  |
| **SUSE Linux Enterprise Server (SLES) 11** and future OS fixpacks | 64 bit |  |
| **Windows Server 2008 R2 Enterprise Edition** and future OS fixpacks | 64 bit |  |
| **Windows Server 2008 R2 Standard Edition** and future OS fixpacks | 64 bit |  |

##### Server Host Operating System Notes

\* *"and future OS fixpacks" includes Service Releases (SR's) and
Updates (RHEL). Fix pack is IBM terminology for a minor release that
includes fixes (vs. features).*

### A2. Application Servers ---++++ A2.1 Application Server Support

The following application servers can be used to host CLM applications
(non-clustered):

| Application Servers | Server Version | Notes |
|:---|:---|:---|
| **WebSphere Application Server v8.5 x86-64** and future fixpacks | Supported | Please see "Bundling" Note below.Please also see Note below for BIRT issue. |
| **WebSphere Application Server Network Deployment v8.5** and future fixpacks | Supported | Non-clustered Only |
| Tomcat Apache Tomcat v7.0.3.2 and future fixpacks | Supported |  |

##### Application Server Notes

-   WAS and DB2 bundles are only available on Passport Advantage and via
    the CLM Media (not on Jazz.net). Customers upgrading from CLM 3.0.1
    and 4.0 are entitled to continue using WAS 7.0.x and WAS 8.0.x as
    long as CLM supports those versions.
-   WebSphere Application Server support for SSE is 64-bit only to align
    with 64-bit server platforms.
-   DOORS Web Access only supports Tomcat AppServer, no support for
    WebSphere Application Server is available
-   There is a known issue with BIRT reports running WAS 8.5.0.x please
    see this [Tech
    Note](http://www-01.ibm.com/support/docview.wss?uid=swg21616615) for
    WAS patch.

Note: CCM BIRT report issues running WAS 8.5.0.1 please see technote for
patch information.

### A3. Databases

The following databases can be used to host SSE applications:

| Database | Server | Notes |
|:---|:---|:---|
| **IBM Derby SDK 10.8.1.2** and future fixpacks | 64 bit | For Evaluation purposes only - for small teams of 10 users or less)CLM bundles Derby |
| **IBM DB2 Enterprise Server Edition v9.7** and future fixpacks | 64 bit |  |
| **IBM DB2 Workgroup Server Edition v9.7** and future fixpacks | 64 bit |  |
| **Oracle Database 11g Standard Edition Release 2** and future fixpacks | 64 bit |  |

##### Database Support Notes

-   Database support is 64-bit only to align with 64-bit server
    platforms.
-   WAS and DB2 bundles are only available on Passport Advantage and in
    the CLM Media (not on Jazz.net). Customers upgrading from CLM 3.0.1
    and 4.0.X are entitled to continue using DB2 9.7 as long as CLM
    supports that version.

### A4. Java Runtime Environment (Server)

| JRE                                           | CLM Server  | Notes |
|:----------------------------------------------|:------------|:------|
| **IBM Java SDK 6.0.13.1** and future fixpacks | Supported   |       |

### A5. Identity Management

-   Apache Directory Server 1.5.5
-   Microsoft Active Directory 2008
-   Microsoft Active Directory 2008 R2

### A6. Installation Manager

-   IBM Installation Manager 1.6.3

### A7. License Server

-   Rational License Server 8.1.3.3

## B. **Client Requirements**

-   **Reminder: The platforms listed below are the starting point for
    SSE support and unless otherwise indicated support includes this
    level and all future OS fixpacks. For RedHat Updates are equivalent
    to fix packs**

### B1. Client Operating Systems

| Client Operating System | DOORS Client | DNG Rich Client | Rhapsody | Web Clients (Browsers) | Notes |
|:---|:---|:---|:---|:---|:---|
| **Red Hat Enterprise Linux (RHEL) Client 6 x86-32, x86-64** and future OS fixpacks | Windows Only | Windows Only | Supported | Supported | Please see Client OS Notes below |
| **Red Hat Enterprise Linux (RHEL) Workstation 6 x86-32, x86-64** and future OS fixpacks | Windows Only | Windows Only | none | Supported | Please see Client OS Notes below |
| **SUSE Linux Enterprise Desktop (SLED) 10.0 SP3 x86-32, x86-64** and future OS fixpacks | Windows Only | Windows Only | Supported | Supported | Please see Client OS Notes below |
| **SUSE Linux Enterprise Desktop (SLED) 11.0 x86-32, x86-64** and future OS fixpacks | Windows Only | Windows Only | Supported | Supported | Please see Client OS Notes below |
| Windows XP Professional SP2 x86-32, x86-64 and future OS fixpacks | 32 bit | 32 bit only | 32 bit | Supported |  |
| Windows Vista SP2 Business x86-32, x86-64 and future OS fixpacks | 32 bit | 32 bit mode only | 32 bit | Supported |  |
| Windows Vista SP2 Enterprise x86-32, x86-64 and future OS fixpacks | 32 bit | 32 bit mode only | 32 bit | Supported |  |
| Windows Vista SP2 Ultimate x86-32, x86-64 and future OS fixpacks | none | 32 bit mode only | none | Supported |  |
| Windows 7 Business x86-32, x86-64 and future OS fixpacks | none | in 32 bit mode only | none | Supported |  |
| Windows 7 Enterprise x86-32, x86-64 and future OS fixpacks | 32 bit | in 32 bit mode only | 32 bit & 64 bit exploit | Supported |  |
| Windows 7 Ultimate x86-32, x86-64 and future OS fixpacks | none | in 32 bit mode only | 32 bit & 64 bit exploit | Supported |  |
| Windows 7 Professional x86-32, x86-64 and future OS fixpacks | 32 bit | in 32 bit mode only | 32 bit & 64 bit exploit | Supported |  |

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

|  |  |  |  |
|----|----|----|----|
| **Firefox 17 ESR** and future fixpacks | Supported | Supported |  |
| **Internet Explorer 8** and future fixpacks | Supported | Supported | Please note IE8 is not supported for the RTC Eclipse Client on 64-bit Windows please use IE9. |
| **Internet Explorer 9** and future fixpacks | Supported | Supported |  |

#### Browser Support Notes

-   DOORS NG Graphical Editor is supported in 32-bit mode using Internet
    Explorer and Firefox on Windows (Only).
-   Macromedia Flash Player 10,11\* and future releases, mods and
    fixpacks is supported for graphical view in Work Item Statistics
    dashboard viewlet

### B3. Java SDK

\* IBM Java SDK 6.0.13.1\* and future fixpacks

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
