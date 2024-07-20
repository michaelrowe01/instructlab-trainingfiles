META:TOPICINFO{author="tomp" date="1512311205" format="1.1"
version="1.1"} META:TOPICPARENT{name="WebPreferences"}

# Recommended Application Lifecycle Management (ALM) deployment topologies 6.x DKGRAY Authors: Main.StevenBeard, Main.DavidChadwick, Main.ThomasPiccoli Build basis: CLM and SSE 6.x [recommended-application-lifecycle-management-alm-deployment-topologies-6.x-dkgray-authors-main.stevenbeard-main.davidchadwick-main.thomaspiccoli-build-basis-clm-and-sse-6.x]

ENDCOLOR

TOC{title="Page contents"}

## Recommended topologies overview

This page describes the Recommended ALM Deployment Topologies for
version 6.x. Refer to [Standard deployment topologies
overview](StandardTopologiesOverview) for high-level description of the
standard topologies, how they are categorized and their key
characteristics.

These recommended deployment topologies for the Rational solution for
Application Lifecycle Management (ALM) are a subset of the standard ALM
deployment topologies. For the rest of the standard topologies, see
[Alternative ALM deployment topologies
6.x](AlternativeALMDeploymentTopologies6). Within this wiki, additional
guidance and best practices will be developed about how to best
instantiate these recommended topologies.

## Introduction and approach

These recommended topologies were chosen based on the following
criteria:

1.  Those that are most commonly and successfully deployed to date by
    customers and internally within IBM
2.  Those that are based upon the most commonly available platforms,
    operating systems and middleware
3.  Those that are based upon technologies that customers, partners and
    the IBM Rational Field have the most experience with
4.  Those that are the focus of testing within IBM Rational.

These recommended topologies represent only a few of the many
permutations for deploying the Rational solution for ALM. The [ALM
systems requirements](DeploymentInstallingUpgradingAndMigrating) capture
the full set of options for supported deployment permutations.

These topologies have been defined to capture good deployment patterns,
which include additional guidance on building in flexibility,
scalability, performance, and support for other non-functional
requirements, such as [high availability](HighAvailability), [disaster
recovery](DisasterRecovery), and [security](JTSAuthenticationExplained).

## Recommended topologies

### (ALM-E1) Enterprise - Distributed / Linux / DB2

This enterprise topology uses Linux for the server operating systems. It
includes both DNG and DOORS/DWA as the RM applications. The applications
are distributed across separate servers and WAS instances. A [reverse
proxy](InstallProxyServers) is used to ensure public URI stability. DB2
is used for the databases and is hosted on a separate server. Finally,
licenses are served by a floating license server and Tivoli Directory
Server provides the [LDAP](ConfigureCLMOnWASWithLDAP) based user
management, for all but DOORS/DWA, which uses Windows Active Directory
Server. Note that the VVC application is only present in release 6.0 and
has been incorporated in other applications in later releases.

|                            |                         |
|----------------------------|-------------------------|
| ***Metadata Variable***    | ***Value***             |
| Operating System           | Linux                   |
| Database Management System | DB2                     |
| Application Server         | WAS                     |
| License Management System  | Floating                |
| User Management System     | Tivoli Directory Server |
| Other technologies         | Reverse Proxy           |

-   ALM-E1 Topology Diagram for v6.x:

### (ALM-E3) Enterprise - Distributed / Linux / Oracle

This enterprise topology uses Linux for the server operating systems. It
includes both DNG and DOORS/DWA as the RM applications. The applications
are distributed across separate servers and WAS instances. A [reverse
proxy](InstallProxyServers) is used to ensure public URI stability.
Oracle is used for the databases and is hosted on a separate server.
Finally, licenses are served by a floating license server and Tivoli
Directory Server provides the [LDAP](ConfigureCLMOnWASWithLDAP) based
user management, for all but DOORS/DWA, which uses Windows Active
Directory Server. Note that the VVC application is only present in
release 6.0 and has been incorporated in other applications in later
releases.

|                            |                         |
|----------------------------|-------------------------|
| ***Metadata Variable***    | ***Value***             |
| Operating System           | Linux                   |
| Database Management System | Oracle                  |
| Application Server         | WAS                     |
| License Management System  | Floating                |
| User Management System     | Tivoli Directory Server |
| Other technologies         | Reverse Proxy           |

-   ALM-E3 Topology Diagram for v6.x:

### (ALM-E7) Enterprise - Distributed / Windows / Oracle

This enterprise topology uses Windows for the server operating systems.
It includes both DNG and DOORS/DWA as RM applications. The applications
are distributed across separate servers and WAS instances. A [reverse
proxy](InstallProxyServers) is used to ensure public URI stability.
Oracle is used for the databases and is hosted on a separate server.
Finally, licenses are served by a floating license server and Windows
Active Directory Server provides the [LDAP](ConfigureCLMOnWASWithLDAP)
based user management. Note that the VVC application is only present in
release 6.0 and has been incorporated in other applications in later
releases.

|                            |                                   |
|----------------------------|-----------------------------------|
| ***Metadata Variable***    | ***Value***                       |
| Operating System           | Microsoft Windows                 |
| Database Management System | Oracle                            |
| Application Server         | WAS                               |
| License Management System  | Floating                          |
| User Management System     | Microsoft Active Directory Server |
| Other technologies         | Reverse Proxy                     |

-   ALM-E7 Topology Diagram for v6.x:

## Applying the topologies

Every customer's environment is different with unique, necessary and
often immutable requirements and constraints. We recognize that these
standard topologies may not provide enough detail to make them
immediately implementable in some customer environments, but we wanted
to describe several topologies with enough variability to give an
indication of what is possible and where our recommendations start.

While we recommend customers start with a standard topology that is most
applicable to them, we recognize they will need to make changes and
customizations to support their own unique requirements and constraints.
IBM will support your own implementations, but may ask you to describe
which topology is most applicable to your deployment and ask you to
document what is unique in your environment to expedite any potential
support situation.

To aid you in documenting your chosen deployment topology, we have made
the following Rational Software Architect (RSA) model files available:

-   [ALM standard topologies
    6.x](ATTACHURL/com.ibm.alm.deployments.6.0.0.zip)

These may be imported into RSA then further modified or expanded to
represent your environment. Look at the Installation_Instructions.txt
file for information on how to import the models into RSA.

### Datasheets and sizing guidelines

Find ALM-specific performance datasheets, sizing guidelines and
performance-related case studies on the [Performance datasheets and
sizing guidelines page](PerformanceDatasheetsAndSizingGuidelines).

### Next steps

This topic is meant to briefly introduce these standard topologies and
describe how they might be applied. Work is already underway to build
upon and apply them. Subsequent updates to this topic and supporting
topics will provide additional insight into their usage.

Future updates to this topic or supporting topics may cover:

-   Deeper look at select topologies
-   Provide suggested tuning parameters
-   Consider high availability database topologies
-   Begin to expand this topology model into other domains
-   Discussion of strategic integrations with other IBM and non-IBM
    products.

##### Related topics: [Alternative ALM deployment topologies 6.x](AlternativeALMDeploymentTopologies6), [Standard deployment topologies overview](StandardTopologiesOverview) [related-topics-alternative-alm-deployment-topologies-6.x-standard-deployment-topologies-overview]

##### Additional contributors: Main.IanCompton [additional-contributors-main.iancompton]
