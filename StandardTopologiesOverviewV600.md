META:TOPICINFO{author="tomp" date="1512310944" format="1.1"
version="1.1"} META:TOPICPARENT{name="WebPreferences"}

# Standard deployment topologies overview [standard-deployment-topologies-overview]

DKGRAY Authors: Main.StevenBeard, Main.GrantCovell, Main.TimFeeney,
Main.DavidChadwick, Main.VaughnRokosz, Main.ThomasPiccoli Build basis:
CLM and SSE 3.x, 4.x, 5.x and ALM 6.x ENDCOLOR

TOC{title="Page contents"}

Many customers implement an Application Lifecycle Management (ALM)
solution for building software. In past releases we talked about using
the Collaborative Lifecycle Management (CLM) or Systems and Software
Engineering (SSE) solutions depending on whether the primary use case
was a software development shop or a more integrated hardware and
software product engineering use case. The common goal is to provide a
complete tool infrastructure for their software or systems development
organizations. With the 6.0 release, we have combined the installation
package into a single ALM Core package of tools to simplify the
installation and deployment of the solution to both audiences. To
simplify our discussion, we will present a single set of ALM topologies
that can be deployed in part or as a whole depending on what
capabilities the customer needs to purchase and supply to their software
or product development teams.

One of the most frequently asked questions is how to deploy the full ALM
solution so that it performs well, runs robustly, and evolves without
restriction. Customers ask about possible deployment strategies because
they must balance two sometimes opposing forces: the desire to build
what's right for their organizations and the desire to stay within the
mainstream of the ALM product evolution so they can easily and quickly
reap the benefits of the new technology.

The ALM [system requirements](DeploymentInstallingUpgradingAndMigrating)
permit a wide range of supported middleware platforms and topologies
upon which to host the solution. The ALM products run on several
commercial databases and two of the most popular web application
servers. It is also possible and recommended to introduce reverse proxy
servers in front of either a centralized or a distributed set of web
application servers.

To simplify the wide range of choices, this article outlines several
standard topologies which are the expected and most frequently chosen
deployment patterns over the past several years. Keeping in mind the
continual evolution of the ALM solution, these topologies can be used
with the ALM 3.X or later product versions.

Publishing these standard topologies represents tried and true examples
of how customers have successfully deployed the ALM solution.
Additionally, the ALM solution system testing organization uses these
topologies to perform deep customer simulation testing, which includes
installation, upgrade, functional, performance, and robustness testing.
By adhering closely to one of these standard topologies, customers will
have an easier time characterizing their deployment in the event of an
interaction with IBM software support. These topologies become a short
hand that can be used whenever an ALM deployment is discussed. For
example, when system performance testing results or a high availability
configuration is discussed, the appropriate standard topology can be
referenced.

Several different teams came together to define and document these
standard topologies. These teams design and execute system, performance
and reliability testing, develop and support the ALM products, and work
directly with customers to design and implement the ALM solution at
customer locations worldwide.

\#KeyTopologyVariants

## Key topology variants

The ALM applications, and Jazz Team Server can be installed on shared
application servers, or distributed across multiple application servers
for improved scalability. Although this flexibility allows you to design
a topology to best fit your needs, that flexibility also adds complexity
to the planning process. As a result, it is important to plan your
deployment topology carefully, as changing your topology later can be
very complex and require substantial application downtime. Potential
deployment topologies are divided into four key topology variants:
Evaluation, Department, Enterprise and Federated.

### Evaluation topologies

An evaluation topology is useful for demonstration or training
deployments only. In this type of installation, all the application and
database software is installed on the same server. You should not start
with this topology and then attempt to expand it into a Departmental or
Enterprise topology. If you have any intent to create production level
artifacts, you should consider either a Departmental or Enterprise
topology. The following diagram is a generic example of an evaluation
topology for the ALM v6.x solution. Note that the VVC application is
only present in release 6.0 and has been incorporated in other
applications in later releases.

-   Generic Evaluation Topology for ALM 6.x:

### Departmental topologies

Departmental topologies are useful for small team and single-server
deployments. Use a stable, company-approved host name and register it
with the domain name server (DNS) to keep the URLs of the data stable.
In this type of installation, databases are installed on a dedicated
database server, and one or more other applications are installed on an
application server. A key advantage of the departmental topologies is
that they require less hardware and are easier to deploy initially.
These topologies are best for smaller projects and smaller-sized teams.
Crucially, if you are fairly certain that your deployment will likely
expand, you should consider starting with an Enterprise topology. The
following diagram is a generic example of a departmental topology for
the ALM v6.x solution. Note that the VVC application is only present in
release 6.0 and has been incorporated in other applications in later
releases.

-   Generic Departmental Topology for ALM 6.x:

### Enterprise topologies

Enterprise topologies are useful for production or medium-sized to
large-sized teams and multiple server (or distributed) deployments. Use
a stable, company-approved host name and register it with the domain
name server (DNS) to keep the URLs of the data stable. Enterprise
topologies distribute the ALM applications, Jazz Team Server, the
database software, etc, and are more flexible. These topologies enable
you to incrementally adopt applications into your deployment and
configure them to use the same Jazz Team Server. In this type of
installation, databases are installed on a single database server and
each application is usually installed on its own dedicated application
server. In addition, to connect multiple application instances to a
shared Jazz Team Server, the instances must all be authenticated from
the same authentication realm and thus share the same set of users. The
following diagram is a generic example of an enterprise topology for the
ALM v6.x solution. Note that the VVC application is only present in
release 6.0 and has been incorporated in other applications in later
releases.

-   Generic Enterprise Topology for ALM 6.x:

### Federated topologies

Federated topologies are useful to very large enterprises who tend to
deploy an ALM solution per product line or organizational division but
would still like to be able to pull together an enterprise-wide view of
their current status and report on a rolled up view of their entire
portfolio of software or product set. Often versions of products or
subsystems in one division are used as a part of a larger solution. By
coordinating the planning and monitoring the status across divisional
boundaries, the customer can manage these larger and more complex
solutions. The following diagram is a generic example of a federated
topology for the ALM v6.x solution. Note that the VVC application is
only present in release 6.0 and has been incorporated in other
applications in later releases.

-   Generic Federated Topology for ALM 6.x:

## Metadata variables

The following variables describe the key characteristics that provide
variation in the typical ALM deployment topologies. These, along with
the previously mentioned key topology variants are used to distinguish
the standard topologies.

1 Operating system (Windows, AIX, Linux, z/OS, etc.) 1 Database
management system (DB2, Oracle, SQL Server, Apache Derby) 1 Application
server (Apache Tomcat, WebSphere Application Server) 1 License
management systems (Evaluation, Floating, Token) 1 User management
system (Apache Tomcat, Active Directory, Tivoli Directory Server) 1
Other technologies such as proxy servers, virtual host names, WAN
accelerators

Although integrations are an important dimension, they are not addressed
in this article or included in the recommended or alternative deployment
topologies. Additionally, specific hardware architectures and
virtualization technologies are not included among these variables.
Hardware architecture and virtualization technologies are very important
considerations when defining a deployment architecture, however, more
from a performance and sizing perspective. Recommended hardware
architectures against these standard topologies will be discussed in a
follow-on article.

\#RecommendedAndAlternateTopologies

## Recommended and alternate topologies

### Versions 6.x

-   [Recommended ALM topologies, version
    6.x](RecommendedALMDeploymentTopologies6)
-   [Alternative ALM topologies, version
    6.x](AlternativeALMDeploymentTopologies6)

### Versions 5.x

-   [Recommended CLM topologies, version
    5.x](RecommendedCLMDeploymentTopologies5)
-   [Recommended SSE topologies, version
    5.x](RecommendedSSEDeploymentTopologies5)
-   [Alternative CLM topologies, version
    5.x](AlternativeCLMDeploymentTopologies5)
-   [Alternative SSE topologies, version
    5.x](AlternativeSSEDeploymentTopologies5)

### Versions 3.x, 4.x

-   [Recommended CLM topologies, versions 3.x,
    4.x](RecommendedCLMDeploymentTopologies)
-   [Recommended SSE topologies, versions 3.x,
    4.x](RecommendedSSEDeploymentTopologies)
-   [Alternative CLM topologies, versions 3.x,
    4.x](AlternativeCLMDeploymentTopologies)
-   [Alternative SSE topologies, versions 3.x,
    4.x](AlternativeSSEDeploymentTopologies)

## Datasheets and sizing guidelines

Find ALM-specific performance datasheets, sizing guidelines and
performance-related case studies on the [Performance datasheets and
sizing guidelines page](PerformanceDatasheetsAndSizingGuidelines).

##### Related topics: [related-topics]

-   [Deployment planning](Deployment.DeploymentPlanning)
-   [Deployment planning and
    design](Deployment.DeploymentPlanningAndDesign)

##### Additional contributors: Main.JoePesot [additional-contributors-main.joepesot]
