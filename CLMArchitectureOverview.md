META:TOPICINFO{author="sbeard" date="1417903045" format="1.1"
version="1.10"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Collaborative Lifecycle Management architecture overview [collaborative-lifecycle-management-architecture-overview]

DKGRAY Authors: Main.TimFeeney Build basis: The Rational solution for
Collaborative Lifecycle Management (CLM) ENDCOLOR

TOC{title="Page contents"}

Application Lifecycle Management (ALM) is a broad Rational solution
category. ALM is also a market category, with vendors providing
solutions competing for market share in this space. Industry analysts
and tool vendors define it differently. Wikipedia uses the
[ALM](http://en.wikipedia.org/wiki/Application_lifecycle_management)
definition from an SD Times article by Jennifer Dedong:

*..a continuous process of managing the life of an application through
governance, development and maintenance. ALM is the marriage of business
management to software engineering made possible by tools that
facilitate and integrate requirements management, architecture, coding,
testing, tracking, and release management*

Forrester analyst Carey Schwaber, in The Changing Face of Application
Lifecycle Management (Forrester Research, August 18, 2006), states, ALM
is the thread that ties the development lifecycle together.

While the definitions vary, you can see that creation and management of
any asset used in the development of software is important to ALM.

IBM Rational has a broad set of tools supporting the development of
software that includes the core capabilities of change management,
project management, requirements definition and management, design
management, construction & software configuration management, deployment
management (software delivery automation) and quality management.

By assembling a solution that covers these core capabilities, software
development teams can focus on solving complex business problems.

For a 5-minute introduction to ALM, [watch this video on
Jazz.net](https://jazz.net/library/video/345). For a short introduction
to Open Services for Lifecycle Collaboration (OSLC), watch this [video
on open-services.net](http://open-services.net/about/).

## Overview

The lead ALM solution from IBM Rational software is the Rational
solution for Collaborative Lifecycle Management (CLM), which consists of
Rational Requirements Composer, Rational Team Concert, Rational Quality
Manager and Rational Software Architect with Design Management

The Jazz platform is strategic for implementing the Rational solution
for CLM. The Jazz platform is all about collaboration; it allows
individual products to integrate better and more easily, and allows the
users of those products who take on distinct roles to work more
effectively together than has historically been possible. The Jazz
platform supports a more collaborative approach to ALM tools and their
users.

That approach is open. It leverages the standards used by the Internet.
Just as the internet works with data spread around the world, the
approach is to allow development team data to be spread around an
organization, and yet be as easily accessible as surfing the
world-wide-web. Through the support for
[OSLC](http://open-services.net/html/Home.html), integrations can be
provided for both Jazz-based and classic products. Additionally, third
party vendors and customers can consume or provide their own OSLC
interfaces to support heterogeneous environments made up of Rational,
third party, and/or customer solutions. The combination of Jazz and OSLC
provides the ability to have unprecedented collaboration, transparency,
automation, and traceability.

Effective ALM can help address current business requirements, enhance
productivity with automation, and accelerate decision-making. The key
word here is effective. ALM is not a one-size-fits-all type of solution;
instead, to be effective, you should implement ALM in a way that best
suits your development environment and your companys culture. IBM
Rational software professionals have defined [Five ALM
Imperatives](https://jazz.net/library/article/637) that can help ensure
an effective ALM implementation. These imperatives have been developed
after more than 20 years of implementing ALM, have been used time and
time again, and can be applied to just about any implementation:

-   Maximize product value with **in-context collaboration**
-   Accelerate time to delivery with **real-time planning**
-   Improve quality with **lifecycle traceability**
-   Refine predictability with **development intelligence**
-   Reduce costs with **continuous improvement.**

In summary, "CLM" expresses the proper scope and differentiated value of
our solution. This approach leverages the value that Jazz brings across
both IT and systems delivery, delivered via five ALM imperatives.

## Solution components

The Rational solution for CLM , which is covered by this architecture
document, is comprised of the following applications running on a common
Jazz Team Server: Requirements Management (RM), Change and Configuration
Management (CCM), Quality Management (QM), and Design Management (DM).
These applications are used by a set of products, including the Rational
solution for CLM. These products are:

-   **Rational Requirements Composer (RRC):** helps teams define and use
    requirements effectively across the project lifecycle including rich
    editors for both textual and visual requirements capabilities for
    lean requirements definition, including the creation of use cases,
    sketches and storyboards.

<!-- -->

-   **Rational Team Concert (RTC):** integrates change management,
    source control management, continuous builds (software delivery
    automation), project planning and reporting/dashboard capabilities.

<!-- -->

-   **Rational Quality Manager (RQM):** provides a shared test
    management hub for test planning, creation, and execution as well as
    workflow control, tracking, and end-to-end traceability.

<!-- -->

-   **Rational Software Architect with Design Management (RSA-DM):**
    enables teams to share, collaborate and manage design information
    across the application development lifecycle.

In addition to these applications, the Rational solution for CLM
provides two types of reporting capabilities:

-   **Rational Reporting for Development Intelligence (RRDI):** allows
    creation and viewing of chart and dashboard style reports. It is an
    optional install in CLM 2012. When installed and configured it
    provides users with an additional set of predefined development
    intelligence reports, as well as the ability to author new reports.
    Rational Reporting for Development Intelligence is based on the
    Cognos Business Intelligence (BI) platform.

<!-- -->

-   **Rational Reporting for Document Generation (RRDG):** provides
    support for generation of document style reports. In CLM 2012,
    Rational Reporting for Document Generation is included as part of
    Rational Requirements Composer, Rational Team Concert, and Rational
    Quality Manager. Authoring functionality for document style reports
    is provided by a separate purchase of Rational Publishing Engine
    (RPE).

In addition to these applications, the Rational solution for CLM
includes a set of process and practices and supporting tool extensions,
all packaged in a **Rational Method Composer (RMC)** configuration. The
CLM processes and practices include everything the you need to run the
solution. They describe the context and usage model for the products
that support the solution -- step-by-step guidance on how to apply the
solution, including product guidance in tool mentors. The practices are
self-documenting and include Jazz process templates (including Rational
Team Concert process and work item templates) for enacting the solution.
A published version of the configuration for IBM internal consumption
and inline comments can be found
[here](http://rupository.svl.ibm.com:3000/wikis/clm_2012/index.htm).
Customers that have purchased the necessary Rational Method Composer
reader licenses can download the configuration from the [IBM Rational
Solution Process Assets
page](https://www.ibm.com/support/docview.wss?rs=2360&uid=swg24030663).

[Rational Team
Concert](https://jazz.net/projects/rational-team-concert), [Rational
Quality Manager](https://jazz.net/projects/rational-quality-manager) and
[Rational Requirements
Composer](https://jazz.net/projects/rational-requirements-composer)
share a common installer that deploys the shared Jazz Team Server plus
the Change and Configuration Management, Quality Management, and
Requirements Management applications. The trial licenses that are
installed in the Jazz Team Server provide access to the capabilities of
these products. This means that you can install *any of these products*
to enable the full set of [collaborative lifecycle
management](https://jazz.net/projects/clm) capabilities provided by all
the products. To learn more about applications, capabilities and product
license keys, read the [Building products from
applications](https://jazz.net/blog/index.php/2010/08/16/building-products-from-applications/#_blank)
blog post. Though it currently requires a separate installer, [Rational
Software Architect with Design
Management](https://jazz.net/products/design-management/), part of the
Rational solution for CLM, can be installed into the shared Jazz Team
Server to provide design management capabilities.

## Solution configurations

Any of the CLM products can be used individually or combined as an
organization's first step towards fully leveraging the power of
Collaborative Lifecycle Management. With each tool adopted, the
organization will see continual improvements in quality and efficiency.

## High level solution topology

The CLM product components are built on top of Jazz Team Server, which
provides the foundational services that enable a group of tools to work
together as a single logical server. The figure below shows a typical
departmental installation topology using the current product versions.
Each application shares an associated version of Jazz Team Server. The
deployment can leverage a single database server to host the individual
database instances. This helps to reduce administrative costs including
simplifying backup procedures, although is not required. The diagram
below shows the various product components or applications. These
applications represent capabilities and do not map 1:1 to the products.
For example, Rational Quality Manager contains capabilities that are
found in each of the applications (CCM, RM, QM, DM and JTS) shown below.
A Rational Quality Manager Quality Professional license has access to
defining textual requirements in the RM application, work items and
plans in the CCM application, and all capacities in the QM application
and Jazz Team Server.

Although the Rational solution for CLM supports a very wide variety of
deployment topologies and supporting operating systems and software,
start from a selected set of the most tested and understood
combinations. These standard topologies can be found in the [Deployment
planning and design](DeploymentPlanningAndDesign) section of this wiki.

## Product interfaces

The Jazz initiative aims to improve software & system lifecycle
integration. This initiative consists of three elements:

-   An **open architecture** for lifecycle tool integration
-   An **open community** working together to integrate and develop
    lifecycle tools
-   A **catalog of products** that support the Jazz initiative.

The Jazz project includes the following:

-   [Collaborative Application Lifecycle Management
    Scenarios](https://jazz.net/wiki/bin/view/Main/CALMHome) the
    scenarios work from the outside-in by providing real-world, role and
    task based user experiences that explore end-user goals and their
    needs to access data throughout the lifecycle. They are designed to
    validate the Jazz Integration Architecture, Jazz Foundation, and
    OSLC specifications.

<!-- -->

-   [OSLC](http://open-services.net/) to unlock the information buried
    within development tools, open and agreed upon interfaces are needed
    that allow different tools to share and exchange the data that they
    produce. By creating specifications that define common shapes, uses,
    and relations between software lifecycle data, the OSLC community
    helps us eliminate traditional barriers between tools and to open
    the door to new forms of collaboration. OSLC specifications are
    based on Internet standards, including a novel use of [Linked
    Data](http://www.w3.org/wiki/LinkedData) not only for reading, but
    also for creating and updating. OSLCs use of linked data to enable
    protocol-based integrations of software tools is often referred to
    as linked lifecycle data.

<!-- -->

-   [Jazz Integration Architecture
    (JIA)](http://jazz.net/projects/DevelopmentItem.jsp?href=content/project/plans/jia-overview/index.html)
    a set of inter-connected technologies and specifications, consisting
    of reference architecture, API specifications, a set of common
    services and tool building blocks. At the center of JIA is the Jazz
    Foundation Services, which provides services to enable groups of
    tools to work together. Powering much of JIA are standard RESTful
    APIs and standard resource definitions, which enable participating
    tools to easily share data.

<!-- -->

-   [Jazz Foundation](https://jazz.net/projects/jazz-foundation/) an
    implementation of the Jazz Foundation Services, and optional
    toolkits to aid in the construction of Jazz applications.

The Jazz Architecture is an **open architecture** for lifecycle tool
integration that supports a range of integration patterns, embracing
linked lifecycle data (OSLC) for sharing lifecycle resources, and
defines Jazz Integration Services for common capabilities like
administration, reporting, dashboards, etc.

The value of Jazz Integration Services:

-   Jazz integration services provide additional ways to help lifecycle
    tools work well together, for example, user administration, team
    collaboration, license administration, team process, traceability,
    and reporting
-   Individual Jazz integration services designed to be used
    independently
-   Each lifecycle tool can select those services that provide value for
    that tool's customers
-   Allows new and improved forms of integration to be added to the mix
    as they are developed.

The Jazz Integration Architecture implements OSLC specifications for
integration:

-   Open Services for Lifecycle Collaboration is an open community of
    developers and organizations who collaborate across many software
    lifecycle domains to help standardize how software lifecycle tools
    share data.
-   Jazz products maintain loose coupling between interacting lifecycle
    tools via domain-specific OSLC interfaces and are not tied to a
    particular tool
-   This allows Jazz products to be upgraded independently of one
    another
-   Ensures the architecture is open to new lifecycle tools, where any
    lifecycle tool written by a vendor, an open source project, or
    in-house development, can consume or provide the OSLC protocols.
    This enables customers to integrate lifecycle tools they already
    use.

For CLM, there are four important domains that must be integrated, and
four important OSLC specifications that define how: Change Management,
Design Management, Requirements Management, and Quality Management. This
classification of key concepts of ALM simplifies the integration points,
not only between the CLM components, but also for third-party, open
source, or in-house tools. Any product can act as a provider, a
consumer, or both, of linked lifecycle data, and integrate with any
other tool that does the same. This open and flexible approach is how
the integration of each customers unique set of software lifecycle tools
is made a practical reality.

The products covered in this architecture brief implement OSLC
specifications; as such, they are either a provider or a consumer of
linked lifecycle data. The key specifications are: change management,
requirements management, and quality management.

Source: <http://open-services.net/software>

Open Services for Lifecycle Collaboration provides open, public
descriptions of resources and formats for sharing artifacts across the
software lifecycle. The term *artifact* is commonly used to describe the
content the users interact with. In the programmable web, this is called
a resource. The strategy treats all development artifacts as resources
at the end of the URI, where both XML and JSON are supported formats.
RESTful interfaces are used to GET, PUT, POST or DELETE data in each of
the repositories. Each tool implements the OSLC specification for their
domain (for example, change management, requirements management, quality
management). In addition, tools that integrate the Jazz Foundation
provide the additional benefit of a common UI framework, link-types
describing cross-discipline relationships, rich hovers, queries,
dashboards that host cross-repository widgets, and much more.

For example, when a requirements user chooses to link to, or create an
artifact in Rational Team Concert, Rational Requirements Composer uses
the Rational Team Concert change management RESTful interface to send
the data defined by the public [OSLC change management
specification](http://open-services.net/bin/view/Main/CmHome). Per the
specification, Rational Requirements Composer delegates the user
interface to Rational Team Concert, meaning, the details and semantics
provided by Rational Team Concert are consumed by and displayed in a
Rational Requirements Composer dialog. When the user clicks OK, Rational
Requirements Composer sends a PUT request to the Rational Team Concert
change management service. Links are created between both artifacts
using link support provided by the Jazz Foundation. This same strategy
is employed when a tester in Rational Quality Manager chooses to link to
a work item in Rational Team Concert; Rational Quality Manager calls the
change management service using the OSLC specification.

OSLC Delegation (source: [OSLC Core
Specification](http://open-services.net/pub/Main/OSLCCoreSpecDRAFT/oslc-delegated.png))

This provides a powerful and resilient integration which supports
independent evolution of the products. The URL integrating the two tools
can stay the same with each new upgrade, and changes can be made to the
user interface (coming from the provider application) without
compromising the consumers integration. The delegating UI is helpful to
the end user but it is even more helpful to a developer. Without
delegating the UI the product developers would have to have in-depth
knowledge about how to create a particular artifact. For example,
creating a defect would require knowing which of the attributes are
required and this would require knowledge about the used process and so
on. This would increase the coupling between the products and increased
coupling has a negative impact on independent evolution. This
demonstrates two important architectural decisions to delegate complex
capabilities to the provider and provide a simple way to discover a
resource. Delegating the UI results in a coarse grained coupling only,
and it keeps the barrier of entry low for existing products.

The above diagram illustrates the associations between the core assets
of the Rational solution for CLM. The intra-product relationships (the
relationships that exist within a lifecycle application) are represented
by a dashed line, and the inter-application relationships (the
relationships that exist across applications) are represented by a solid
line. Those in blue were added in the CLM 2011 release. A few examples
of these relationships are listed here. However, the reader should study
the diagram to understand all of the relationships that exist.

An example of an intra-application relationship in the Requirements
Management application (RRC) is that of a Requirement to a Collection of
requirements. A requirement may be of many types, such as, declarative,
use-case, storyboard, UI sketch, etc. A collection is a logical grouping
of these requirements. Therefore, an analyst may choose to bundle a
collection of requirements that apply to a specific release, or possibly
group requirements that affect a specific bug-fix, allowing the team to
know exactly what is to be implemented.

Another example is the relationship between a Test Plan and Test Cases
in the Quality Management application (RQM). Test Plans define the
overall plan for a testing effort, and they generally include a number
of Test Cases that perform the various tests against the application.
Similarly, Test Cases are related to Test Executions, which in-turn
generate (and hence are related to) Test Results.

Lastly, the Change and Configuration Management application (RTC) also
has a number of intra-application relationships. For example, when doing
iterative development it is important to have a high-level Plan for a
release (such as Version 1.0) and several iteration Plans (Sprint 1,
Sprint 2, etc.), that identify the work to be done in each iteration,
and will be executed against the Release Plan, thus the Plan
relationship to itself in the diagram.

The inter-application relationships shown by the solid lines illustrate
the relationships between the applications. These relationships provide
for the Collaborative Lifecycle Management integrations.

An example of this is the relationship between a Requirements Collection
in RM and a Release Plan in CCM. The Requirements Collection defines the
requirements to be implemented in the release, and the Release Plan
indicates the work that needs to be done in order to implement the
appropriate requirements. In this instance, the Requirements Collection
is said to be implemented by the Release Plan, and the Release Plan
implements the Requirements Collection.

Similarly, the Requirements Collection may be linked to a Test Plan in
QM, which allows the quality team to ensure they are testing the
appropriate requirements. In this instance, the Requirements Collection
is said to be validated by the Test Plan and the Test Plan validates the
Requirements Collection.

To complete the traceability, Release Plans in CCM may be linked to Test
Plans in QM, such that RQM tests the work being performed per the
Release Plan.

The Jazz Architecture has enabled a diverse ecosystem of third party
tools to emerge based on the available interfaces. The [Jazz
Integrations Dashboard](https://jazz.net/extend/integrations/) provides
a list of all those IBM Business Partners and other vendors providing
value added integrations to the Rational solution for CLM. Further, the
internal, Jazz [Integration Management
Dashboard](https://jazzdev.torolab.ibm.com:9443/jazz/web/projects/Jazz Platform#action=com.ibm.team.dashboard.viewDashboard&team=Open20Integrations&tab=_8)
describes the work by the Gearbox team to develop additional
integrations. Lastly, the IBM Rational Integration Engineering Team has
developed a number of [salable commercial
assets](http://w3.ibm.com/software/xl/portal/content?synKey=H129094D43445O88)
(integrations, extensions, utilities, etc.) that are available to use
with customers.

## Strengths

The strengths for the Rational solution for CLM are primarily addressed
collectively by looking at the current state of the Jazz Team Server and
the individual products use of Jazz:

-   **Common technology and server platform:** The Rational solution for
    CLM constitutes products that are based on a common technology
    platform called Jazz. The CLM products all run on top of a Jazz Team
    Server and use Jazz Foundation Services. This provides the products
    with a basis for deploying, managing, and integrating separate
    deployments of products based on Jazz in a common way.

<!-- -->

-   **Open Services for Lifecycle Collaboration framework:** The Jazz
    Team Server that the core CLM products run on implement OSLC as a
    means for integrating and communicating with each other. This
    provides a common way for sharing, integrating, and tracing assets
    across the products that would otherwise not be possible. For
    example, work item queries in Rational Team Concert can be hosted on
    a dashboard in Rational Quality Manager. This is also true of
    products that are not Jazz based but implement the OSLC
    specification. For example, Rational ClearQuest (v7.1.0.2 and newer)
    implements the OSLC 2.0 Change Management specification allowing it
    to share and integrate change management data bi-directionally with
    other tools that also support this specification, like Rational Team
    Concert. IBM has committed to providing and improving product
    integrations between the Jazz based CLM products and the broader
    portfolio of products. Additionally, many IBM Business Partners and
    market leading software products are supporting OSLC to increase
    their product interoperability with these offerings and the industry
    as a whole.

<!-- -->

-   **Token licensing support:** The Rational solution for CLM supports
    a token licensing model enabling customers to flexibly use whichever
    token supported product in Rational they need at any given point in
    time. Tokens are a layer of abstraction above products allowing
    customers to flexibly shift their investment from one product or
    domain to another without having to make product by product license
    purchases that are mutually exclusive.

<!-- -->

-   **Open commercial development:** The Rational solution for CLM is
    developed by IBM employees fully committed to making a highly
    innovative offering. However, the Rational solution for CLM is
    developed openly in the community on Jazz.net. Customers can see the
    ongoing work and plans, status, enhancements, and defects from IBM
    as well as those submitted by others. Additionally, builds of the
    milestone, beta, and release candidate versions of the products are
    incrementally provided for anyone registered (free) to try out. The
    source code for these products is also available on Jazz.net as well
    as incubator/prototype offerings being explored. Unlike an open
    source project, the software that goes into the releases is solely
    developed by IBM and is subject to strict quality assurance and
    management.

<!-- -->

-   **Broad and deep lifecycle management solution portfolio:** The
    Rational solution for CLM has a broad scope covering all major
    lifecycle management activities and also is deep providing best in
    class support for domain/role specific activities in the software
    development lifecycle. This is supported, integrated, and provided
    completely from IBM Rational reducing the overhead in managing and
    supporting the solution while assuring greater overall quality and
    reducing the investment risk in the solution.

<!-- -->

-   **Scalability and globally distributed development support:** The
    Rational solution for CLM has been optimized to scale and support
    hundreds and even thousands of users. Additionally, it uses
    http/https as its communication protocol and has been optimized for
    usage over wide area networks enabling it to support distributed
    users and groups from multiple locations while preserving the
    intended user experience.

<!-- -->

-   **Rich web 2.0 user experience:** The Rational solution for CLM
    provides a rich web client experience with features such as drag and
    drop, rich hovers, etc. The web client is considered a first class
    client that enables customers to flexibly access and use the product
    without having to worry about installing software or compatibility.
    It supports industry leading browsers including Microsoft Internet
    Explorer and Mozilla Firefox.

<!-- -->

-   **Broad platform support:** The Rational solution for CLM has the
    broadest platform support in the industry today as described in the
    [CLM System
    Requirements](DeploymentInstallingUpgradingAndMigrating).

<!-- -->

-   **Enterprise class entitlements included with paid licenses:**
    Customers are entitled to use WebSphere Application Server, DB2, and
    Cognos for their CLM deployments. Cognos adds development
    intelligence style reporting to the Rational solution for CLM.

## Complementary products

Jazz enables the Rational solution for CLM to be open and complement an
existing customers software stack, both Rational and non Rational
offerings via OSLC. It should be noted that the products identified in
the "IBM Product Alternatives" section can also be considered
complementary if a customer already owns these products or requires
them. All of these "Product Alternatives" include one or more
integrations to the Rational solution for CLM. However, there are
notable Rational products that directly complement the core Rational
solution for CLM with minimal to no overlap as identified here. A
customer-facing [Extend your
tools](https://jazz.net/extend/integrations/) page has been created that
details all the integrations to Jazz and the Rational solution for CLM.
There include native IBM supported integrations planned to non-IBM based
products including HP Quality Center, Atlassian Jira, and open source
Git.

-   [Rational Method
    Composer](http://www.ibm.com/software/awdtools/rmc/) - IBM Rational
    Method Composer is solution for managing, tailoring, and
    communicating process descriptions. RMC consists of two
    components, (1) Process Assets in the form of the IBM Practice
    Library and the Rational Unified Process Library and (2) a tool to
    author, tailor, configure, and publish process descriptions. RMC
    process descriptions provide the human readable guidance team
    members need to work together effectively and efficiently as a team.
    RTC process templates provide the machine readable rules that
    configure the tool to support your process. Together, RMC and RTC
    provide a powerful solution for process management, process
    enactment, and measured capability improvement. The Rational
    solution for CLM includes practices and processes in RMC, which
    require an RMC reader license to access; to tailor those, a full
    license for RMC is required.

<!-- -->

-   [Rational Application
    Developer](http://www.ibm.com/developerworks/rational/products/rad/) -
    A highly enhanced eclipse IDE that helps Java developers rapidly
    design, develop, assemble, test, profile and deploy high quality
    Java/Java EE , Portal, Web/Web 2.0, OSGi, Web services and SOA
    applications. Rational Team Concert directly integrates into a RAD
    IDE and also provides specific integrations for collaborating on
    unit testing and profiling of applications.

<!-- -->

-   [Rational Software
    Architect](http://www.ibm.com/software/awdtools/swarchitect/) - A
    family of products that provides integrated design and development
    support for model-driven development with the UML. Rational Software
    Architect provides extensions for a variety of problem and industry
    domains, such as deployment planning, SOA or communication
    applications, RSA-DM, included in the Rational solution for CLM, is
    one of the product editions included in the RSA family.

<!-- -->

-   [Rational Asset
    Manager](http://www.ibm.com/software/rational/products/ram/) - IBM
    Rational Asset Manager (RAM) offers a definitive, standards based
    library to help organizations manage, collaborate, and govern the
    business and technical assets involved in software and systems
    delivery. Rational Asset Manager directly integrates with Rational
    Team Concert for the storing and versioning of software assets in
    the RAM library.

<!-- -->

-   [Rational Functional
    Tester](http://www.ibm.com/developerworks/rational/products/functionaltester/) -
    a testing tool with automated testing capabilities for functional
    testing, regression testing, GUI testing and data-driven testing.
    Rational Quality Manager can manage and automate the execution of
    automated tests developed with Rational Functional Tester.

<!-- -->

-   [Rational Performance
    Tester](https://www.ibm.com/developerworks/rational/products/performancetester/) -
    a performance testing tool for load and stress testing with
    automated performance testing capabilities to validate the
    scalability of web and server based applications. Rational Quality
    Manager can manage and automate the execution of automated tests
    developed with Rational Performance Tester.

<!-- -->

-   [Rational Publishing
    Engine](http://www.ibm.com/software/awdtools/pubengine/) - automate
    the generation of documents for ad-hoc use, formal reviews,
    contractual obligations, or regulatory compliance can help improve
    productivity and reduce risk and cost.

<!-- -->

-   [Rational
    Insight](http://www.ibm.com/software/rational/products/insight/) -
    delivers measurement best practices to help organizations reduce
    time to market, improve quality, and take greater control of
    software and systems development and delivery. It provides objective
    dashboards and measures for transparency and control into risks,
    status, and trends.

<!-- -->

-   [Rational
    ClearCase](http://www.ibm.com/software/awdtools/clearcase/index.html) -
    provides sophisticated version control, workspace management,
    parallel development support and build auditing to improve
    productivity.

<!-- -->

-   [Rational
    ClearQuest](http://www.ibm.com/software/awdtools/clearquest/index.html) -
    provides change tracking, process automation, reporting and
    lifecycle traceability for better visibility and control of the
    software development lifecycle.

<!-- -->

-   [Rational DOORS](http://www.ibm.com/software/awdtools/doors/) -
    reduce costs, increase efficiency and improve quality by enabling
    you to optimize requirements communication, collaboration and
    verification throughout your organization and across your supply
    chain.

<!-- -->

-   [Rational
    RequisitePro](http://www.ibm.com/software/awdtools/reqpro/) - helps
    project teams to manage their requirements, to write good use cases,
    to improve traceability, to strengthen collaboration, to reduce
    project rework, and to increase quality.

<!-- -->

-   [Rational Build
    Forge](http://www.ibm.com/software/awdtools/buildforge/) - an
    adaptive process execution framework that automates, orchestrates,
    manages, and tracks all the processes between each handoff within
    the assembly line of software development, creating an automated
    software factory.

<!-- -->

-   [Rational AppScan](http://www.ibm.com/software/awdtools/appscan/) -
    enables organizations to take a strategic approach for addressing
    Web application security.

<!-- -->

-   [IBM Tivoli Service Request Manager, Tivoli Application Dependency
    Manager, and Tivoli Provisioning
    Manager](https://jazz.net/help-dev/clm/index.jsp?topic=/com.ibm.rational.test.lm.doc/topics/t_int_tivoli.html)
    Both Rational Team Concert and Rational Quality Manager integrate
    with Tivoli Service Request Manager to provide
    Development-Operations collaboration and coordination. Rational
    Quality Manager further integrates with Tivoli Application
    Dependency Manager and Tivoli Provisioning Manager to provide test
    lab integration with technology operations management.

<!-- -->

-   [Lotus
    Connections](https://jazz.net/projects/rational-team-concert/features/social)
    Rational Team Concert integrates with Lotus Connections to improve
    and enable business and development collaboration and social
    networking.

For an up to date list of all product integrations from IBM and IBM
Business Partners, see the following jazz.net locations:

-   [Rational Requirements Composer
    Integrations](http://jazz.net/projects/rational-requirements-composer/integrations/)
-   [Rational Team Concert
    Integrations](http://jazz.net/projects/rational-team-concert/integrations/)
-   [Rational Quality Manager
    Integrations](http://jazz.net/projects/rational-quality-manager/).

##### Related topics: [Deployment planning: Where to start?](DeploymentPlanning) [related-topics-deployment-planning-where-to-start]

##### External links: \* None [external-links-none]

##### Additional contributors: Main.StevenBeard [additional-contributors-main.stevenbeard]

META:FILEATTACHMENT{name="Arch1.png" attachment="Arch1.png" attr="h"
comment="" date="1367954134" path="Arch1.png" size="56466" user="sbeard"
version="1"} META:FILEATTACHMENT{name="Arch2.jpg" attachment="Arch2.jpg"
attr="h" comment="" date="1367955806" path="Arch2.jpg" size="734085"
user="sbeard" version="1"} META:FILEATTACHMENT{name="Arch3.png"
attachment="Arch3.png" attr="h" comment="" date="1367955940"
path="Arch3.png" size="39575" user="sbeard" version="1"}
META:FILEATTACHMENT{name="Arch4.png" attachment="Arch4.png" attr="h"
comment="" date="1367957266" path="Arch4.png" size="52475" user="sbeard"
version="1"} META:FILEATTACHMENT{name="Arch5.png" attachment="Arch5.png"
attr="h" comment="" date="1367957949" path="Arch5.png" size="27766"
user="sbeard" version="1"} META:FILEATTACHMENT{name="Arch6.jpg"
attachment="Arch6.jpg" attr="h" comment="" date="1367958724"
path="Arch6.jpg" size="251166" user="sbeard" version="2"}
META:FILEATTACHMENT{name="Arch7.png" attachment="Arch7.png" attr="h"
comment="" date="1367958943" path="Arch7.png" size="62703" user="sbeard"
version="1"} META:FILEATTACHMENT{name="Arch8.png" attachment="Arch8.png"
attr="h" comment="" date="1367959313" path="Arch8.png" size="92348"
user="sbeard" version="1"}
