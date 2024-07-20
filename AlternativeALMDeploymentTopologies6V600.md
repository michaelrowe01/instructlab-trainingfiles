# Alternative Application Lifecycle Management (ALM) deployment topologies 6.x 
Main.StevenBeard, Main.DavidChadwick, Main.ThomasPiccoli 
Build basis: CLM and SSE 6.x 

## Alternative topologies overview

This page describes the Alternative ALM Deployment Topologies for
version 6.x. Refer to [Standard deployment topologies
overview](StandardTopologiesOverview) for high-level description of the
standard topologies, how they are categorized and their key
characteristics.

These alternative deployment topologies for the Rational solution for
Application Lifecycle Management (ALM) are a subset of the standard ALM
deployment topologies. For the rest of the standard topologies, see
[Recommended ALM deployment topologies
6.x](RecommendedALMDeploymentTopologies6).

## Alternate evaluation topology

### (ALM-V1) Evaluation - Single server / Tomcat / Derby

This is a simple, single server topology whose primary use is supporting
evaluations, demonstrations, proofs of concept and training. Given the
use of Derby and Tomcat, it can be stood up very quickly, especially
with the express install feature. Note that the VVC application is only
present in release 6.0 and has been incorporated in other applications
in later releases.

|                            |                   |
|----------------------------|-------------------|
| ***Metadata Variable***    | ***Value***       |
| Operating System           | Microsoft Windows |
| Database Management System | Derby             |
| Application Server         | Tomcat            |
| License Management System  | Trial             |
| User Management System     | Tomcat            |
| Other technologies         | None              |

-   ALM-V1 Topology Diagram for v6.x:

## Alternate departmental topologies

### (ALM-D1) Departmental - Single application server / Windows / DB2

This departmental topology uses Microsoft Windows for the server
operating systems. The ALM applications and JTS are deployed to a single
WAS instance. A [reverse proxy](InstallProxyServers) server is used to
ensure public URI stability. DB2 is used for the databases and is hosted
on a separate server. Jazz Reporting Service (JRS) is included in this
department configuration and the Data Collection Component (DCC) is
hosted on a separate server and WAS instance for performance reasons.
Finally, licenses are served by a floating license server and Active
Directory provides the [Lightweight Directory Access Protocol
(LDAP)](ConfigureCLMOnWASWithLDAP) based user management. Note that the
VVC application is only present in release 6.0 and has been incorporated
in other applications in later releases.

|                            |                            |
|----------------------------|----------------------------|
| ***Metadata Variable***    | ***Value***                |
| Operating System           | Microsoft Windows          |
| Database Management System | DB2                        |
| Application Server         | WebSphere                  |
| License Management System  | Floating                   |
| User Management System     | Microsoft Active Directory |
| Other technologies         | Reverse Proxy              |

-   ALM-D1 Topology Diagram for v6.x:

### (ALM-D2) Departmental - Single application server / Windows / Oracle

This departmental topology uses Microsoft Windows for the server
operating systems. The ALM applications and JTS are deployed to a single
WAS instance. A [reverse proxy](InstallProxyServers) server is used to
ensure public URI stability. Oracle is used for the databases and is
hosted on a separate server. Jazz Reporting Service (JRS) is included in
this department configuration and the Data Collection Component (DCC) is
hosted on a separate server and WAS instance for performance reasons.
Finally, licenses are served by a floating license server and Active
Directory provides the [LDAP](ConfigureCLMOnWASWithLDAP) based user
management. Note that the VVC application is only present in release 6.0
and has been incorporated in other applications in later releases.

|                            |                            |
|----------------------------|----------------------------|
| ***Metadata Variable***    | ***Value***                |
| Operating System           | Microsoft Windows          |
| Database Management System | Oracle                     |
| Application Server         | WebSphere                  |
| License Management System  | Floating                   |
| User Management System     | Microsoft Active Directory |
| Other technologies         | Reverse Proxy              |

-   ALM-D2 Topology Diagram for v6.x:

### (ALM-D3) Departmental - Single application server, Linux / Oracle

This departmental topology uses Red Hat Enterprise Linux for the server
operating systems. The ALM applications and JTS are deployed to a single
WAS instance. A [reverse proxy](InstallProxyServers) server is used to
ensure public URI stability. Oracle is used for the databases and is
hosted on a separate server. Jazz Reporting Service (JRS) is included in
this department configuration and the Data Collection Component (DCC) is
hosted on a separate server and WAS instance for performance reasons.
Finally, licenses are served by a floating license server and Tivoli
Directory Server provides the [LDAP](ConfigureCLMOnWASWithLDAP) based
user management. Note that the VVC application is only present in
release 6.0 and has been incorporated in other applications in later
releases.

|                            |                          |
|----------------------------|--------------------------|
| ***Metadata Variable***    | ***Value***              |
| Operating System           | Red Hat Enterprise Linux |
| Database Management System | Oracle                   |
| Application Server         | WebSphere                |
| License Management System  | Floating                 |
| User Management System     | Tivoli Directory Server  |
| Other technologies         | Reverse Proxy            |

-   ALM-D3 Topology Diagram for v6.x:

### (ALM-D4) Departmental - Single application server, Linux / DB2

This departmental topology uses Red Hat Enterprise Linux for the server
operating systems. The ALM applications and JTS are deployed to a single
WAS instance. A [reverse proxy](InstallProxyServers) server is used to
ensure public URI stability. DB2 is used for the databases and is hosted
on a separate server. Jazz Reporting Service (JRS) is included in this
department configuration and the Data Collection Component (DCC) is
hosted on a separate server and WAS instance for performance reasons.
Finally, licenses are served by a floating license server and Tivoli
Directory Server provides the [LDAP](ConfigureCLMOnWASWithLDAP) based
user management. Note that the VVC application is only present in
release 6.0 and has been incorporated in other applications in later
releases.

|                            |                          |
|----------------------------|--------------------------|
| ***Metadata Variable***    | ***Value***              |
| Operating System           | Red Hat Enterprise Linux |
| Database Management System | DB2                      |
| Application Server         | WebSphere                |
| License Management System  | Floating                 |
| User Management System     | Tivoli Directory Server  |
| Other technologies         | Reverse Proxy            |

-   ALM-D4 Topology Diagram for v6.x:

## Alternate enterprise topologies

### (ALM-E2) Enterprise - Distributed / Windows / SQL Server

This enterprise topology uses Microsoft Windows for the server operating
systems. It includes both DNG and DOORS/DWA as RM applications. The
applications are distributed across separate servers and WAS instances.
A [reverse proxy](InstallProxyServers) is used to ensure public URI
stability. Microsoft SQL Server is used for the databases and is hosted
on a separate server. Finally, licenses are served by a floating license
server and Windows Active Directory Server provides the
[LDAP](ConfigureCLMOnWASWithLDAP) based user management. Note that the
VVC application is only present in release 6.0 and has been incorporated
in other applications in later releases.

|                            |                            |
|----------------------------|----------------------------|
| ***Metadata Variable***    | ***Value***                |
| Operating System           | Microsoft Windows          |
| Database Management System | Microsoft SQL Server       |
| Application Server         | WebSphere                  |
| License Management System  | Floating                   |
| User Management System     | Microsoft Active Directory |
| Other technologies         | Reverse Proxy              |

-   ALM-E2 Topology Diagram for v6.x:

### (ALM-E4) Enterprise - Power Server / AIX / DB2

This enterprise topology uses AIX for the server operating systems. The
applications share a single WAS instance except for LQE and DCC which
are split out on individual LPARs for performance reasons. A [reverse
proxy](InstallProxyServers) is used to ensure public URI stability. DB2
is used for the databases and is hosted on a separate AIX LPAR. Finally,
licenses are served by a floating license server and Tivoli Directory
Server provides the [LDAP](ConfigureCLMOnWASWithLDAP) based user
management.

|                            |                         |
|----------------------------|-------------------------|
| ***Metadata Variable***    | ***Value***             |
| Operating System           | AIX                     |
| Database Management System | DB2                     |
| Application Server         | WebSphere               |
| License Management System  | Floating                |
| User Management System     | Tivoli Directory Server |
| Other technologies         | Reverse Proxy           |

-   ALM-E4 Topology Diagram for v6.x:

### (ALM-E5) Enterprise - Mainframe / zLinux / DB2

This enterprise topology uses Linux for System z for the server
operating systems. The applications are run in separate profiles on a
single WAS instance. A [reverse proxy](InstallProxyServers) is used to
ensure public URI stability. DB2 for z/OS is used for the databases and
is hosted on a separate z/OS based LPAR. Finally, licenses are served by
a floating license server and Tivoli Directory Server provides the LDAP
based user management.

|                            |                         |
|----------------------------|-------------------------|
| ***Metadata Variable***    | ***Value***             |
| Operating System           | Linux on System z       |
| Database Management System | DB2 for z/OS            |
| Application Server         | WebSphere               |
| License Management System  | Floating                |
| User Management System     | Tivoli Directory Server |
| Other technologies         | Reverse Proxy           |

-   ALM-E5 Topology Diagram for v6.x:

### (ALM-E6) Enterprise - Mainframe / zOS / DB2

This enterprise topology uses IBM z/OS for the server operating systems.
The applications are run in separate profiles on a single WAS instance.
A [reverse proxy](InstallProxyServers) is used to ensure public URI
stability. DB2 for z/OS is used for the databases and is hosted on a
separate LPAR. Finally, licenses are served by a floating license server
and RACF provides the user management.

|                            |               |
|----------------------------|---------------|
| ***Metadata Variable***    | ***Value***   |
| Operating System           | IBM z/OS      |
| Database Management System | DB2 for z/OS  |
| Application Server         | WebSphere     |
| License Management System  | Floating      |
| User Management System     | RACF          |
| Other technologies         | Reverse Proxy |

-   ALM-E6 Topology Diagram for v6.x:

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

##### Related topics: 
* [Recommended ALM deployment topologies 6.x](RecommendedALMDeploymentTopologies6), 
* [Standard deployment topologies overview](StandardTopologiesOverview) [related-topics-recommended-alm-deployment-topologies-6.x-standard-deployment-topologies-overview]

##### Additional contributors: 
* Main.IanCompton [additional-contributors-main.iancompton]
