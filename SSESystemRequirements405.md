META:TOPICINFO{author="tcornell" date="1410469944" format="1.1"
reprev="1.15" version="1.15"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# System Requirements for Systems and Software Engineering 4.0.5 and 4.0.6 [system-requirements-for-systems-and-software-engineering-4.0.5-and-4.0.6]

DKGRAY ***(Rational DOORS and DOORS Web Access, Rational DOORS Next
Generation, Rational Team Concert, Rational Quality Manager, Rational
Rhapsody, Rational Rhapsody Design Manager, Rational Engineering
Lifecycle Manager)***

Authors: Main.CindyMcKeen Build basis: SSE 4.0.5, 4.0.6 ENDCOLOR

TOC{title="Page contents"}

For a short list of track changes to this article please see the bottom
of this article.

-   This is the list of system requirements for **Rational systems and
    software engineering (SSE)** 4.0.5 and 4.0.6 incorporating:
    -   Rational DOORS and DOORS Web Access (DWA)
    -   Rational DOORS Next Generation (DNG)
    -   Rational Team Concert (RTC)
    -   Rational Quality Manager (RQM)
    -   Rational Rhapsody
    -   Rational Rhapsody Design Manager
    -   Rational Engineering Lifecycle Manager (RELM)
-   Questions? Please contact Main.CindyMcKeen

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
| **SUSE Linux Enterprise Server (SLES) 10 SP2** and future OS fixpacks | 64 bit |  |
| **SUSE Linux Enterprise Server (SLES) 11** and future OS fixpacks | 64 bit |  |
| **Windows Server 2008 R2 Enterprise Edition** and future OS fixpacks | 64 bit |  |
| **Windows Server 2008 R2 Standard Edition** and future OS fixpacks | 64 bit |  |
| **Windows Server 2012 Standard Edition** and future OS fixpacks | 64 bit | BLUENew for v4.0.5ENDCOLOR |
| **Windows Server 2012 Datacenter Edition** and future OS fixpacks | 64 bit | BLUENew for v4.0.5ENDCOLOR |

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
| **WebSphere Application Server v8.5.5 x86-64** and future fixpacks | Supported | BLUENew for v4.0.5 - Non-clustered OnlyENDCOLORPlease see Note below for BIRT issue. |
| **WebSphere Application Server Network Deployment v8.5.5** and future fixpacks | Supported | BLUENew for CLM v4.0.5 - Non-clustered OnlyENDCOLOR |
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
| **IBM DB2 Enterprise Server Edition v10.1** and future fixpacks | 64 bit | BLUENew for v4.0.3 ENDCOLOR |
| **IBM DB2 Workgroup Server Edition v10.1** and future fixpacks | 64 bit | BLUENew for v4.0.3ENDCOLOR |
| **Oracle Database 11g Standard Edition Release 2** and future fixpacks | 64 bit |  |

##### Database Support Notes

-   Database support is 64-bit only to align with 64-bit server
    platforms.
-   WAS and DB2 bundles are only available on Passport Advantage and in
    the CLM Media (not on Jazz.net). Customers upgrading from CLM 3.0.1
    and 4.0.X are entitled to continue using DB2 9.7 as long as CLM
    supports that version.

### A4. Java Runtime Environment (Server)

| JRE | CLM Server | Notes |
|:---|:---|:---|
| **IBM Java SDK 6.0.14** and future fixpacks | Supported | BLUENew for 4.0.6 Java 6 SR15ENDCOLORBLUENew for v4.0.5 Java 6 SR14ENDCOLOR |

### A5. Identity Management

-   Apache Directory Server 1.5.5
-   Microsoft Active Directory 2008
-   Microsoft Active Directory 2008 R2

### A6. Installation Manager

-   IBM Installation Manager 1.7

### A7. License Server

-   Rational License Server 8.1.3.3

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
| **SUSE Linux Enterprise Desktop (SLED) 10.0 SP3 x86-32, x86-64** and future OS fixpacks | Windows Only | Supported | Supported | Please see Client OS Notes below |
| **SUSE Linux Enterprise Desktop (SLED) 11.0 x86-32, x86-64** and future OS fixpacks | Windows Only | Supported | Supported | Please see Client OS Notes below |
| Windows XP Professional SP2 x86-32, x86-64 and future OS fixpacks | 32 bit mode only | 32 bit mode only | Supported |  |
| Windows Vista SP2 Business x86-32, x86-64 and future OS fixpacks | 32 bit mode only | 32 bit mode only | Supported |  |
| Windows Vista SP2 Enterprise x86-32, x86-64 and future OS fixpacks | 32 bit mode only | 32 bit mode only | Supported |  |
| Windows Vista SP2 Ultimate x86-32, x86-64 and future OS fixpacks | none | none | Supported |  |
| Windows 7 Business x86-32, x86-64 and future OS fixpacks | none | none | Supported |  |
| Windows 7 Enterprise x86-32, x86-64 and future OS fixpacks | 32 bit mode only | 32 bit & 64 bit exploit | Supported |  |
| Windows 7 Ultimate x86-32, x86-64 and future OS fixpacks | none | 32 bit & 64 bit exploit | Supported |  |
| Windows 7 Professional x86-32, x86-64 and future OS fixpacks | 32 bit mode only | 32 bit & 64 bit exploit | Supported |  |

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
| **Firefox 17 ESR** and future fixpacks | Supported | BLUEDropped in 4.0.6 - Firefox 17ESR is out of service from MozillaENDCOLOR |
| **Firefox 24 ESR** and future fixpacks | Supported | BLUENew for v4.0.5ENDCOLOR |
| **Internet Explorer 8** and future fixpacks | Supported | Supported |
| **Internet Explorer 9** and future fixpacks | Supported | Supported |
| **Internet Explorer 10 for the Desktop** and future fixpacks | Supported | BLUENew for v4.0.5ENDCOLORRRDI supports IE10 in compatibility mode only (Cognos 10.2.x limitation) Note: Windows 7 only - Windows 8 is not yet supported |

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

## D. Summary of Updates by Release

### D1. Additions

-   New for v4.0.5:
    -   RRDI Server support moves to 64 bit (only) to align with new
        packaged Cognos v10.2.1
    -   Windows Server 2012
    -   IE 10
    -   Firefox 24
    -   WAS v8.5.5
    -   Java 6 SR14
    -   Installation Manager v1.7

<!-- -->

-   BLUENew for v4.0.6:
    -   Java 6 SR15

<!-- -->

-   BLUENew for CLM v4.0.7:ENDCOLOR
    -   Java 6 SR16
    -   Apache Tomcat 7.0.52
    -   Microsoft SQL Server Enterprise Edition 2012
    -   Microsoft SQL Server Standard Edition 2012

### D2. Planned Platform Drops for 2014

Dropped in 4.0.6

-   Firefox 17 (goes out of service end of 2013)

These platform drops are planned for 2014 and listed here to assist all
teams in platform planning:

-   DB2 9.7.x
-   Windows XP (which went out of service in 2010)
-   Windows Vista
-   Internet Explorer 8 (this browser has several known issues around
    performance and other areas see details and tech notes referenced
    above)

META:TOPICMOVED{by="sbeard" date="1386589711"
from="Deployment.SSESystemRequirements405406"
to="Deployment.SSESystemRequirements405"}
