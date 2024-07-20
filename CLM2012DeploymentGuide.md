# Rational Solution for Collaborative Lifecycle Management 4.x deployment guide

Author: Main.RickMaludzinski 

Build basis: Rational solution for Collaborative Lifecycle Management 4.x 


This guide provides a roadmap to assist you with your deployment of
Rational Collaborative Lifecycle Management (CLM) 4.x. It is intended to
help you navigate to pertinent documentation on Jazz.net, the
Infocenter, and other resources that are essential for successfully
deploying a new CLM 4.x (also known as CLM 2012) solution or upgrading
to CLM 4.x from a current installed base. It will also answer questions
that typically arise during a deployment scenario with pointers to
additional information should the reader require it. As this guide is
not intended to replace existing documentation available elsewhere you
will note the heavy use of links to tutorials, articles, videos, and
product documentation created by multiple contributors from across the
Jazz development organization.

The intended deployment scenario should guide you through the material
below. If you are not familiar with CLM basics, you should start with
the first section [Introduction to CLM](#IntroCLM). If you are already
familiar with CLM, and will be installing CLM for the first time, then
proceed with [New CLM 4.x Installation](#NewInstall). If you are
upgrading an existing deployment to CLM 4.x, then you should read
[Upgrade to CLM 4.x](#UpgradeCLM).

Disclaimer: This guide is an evolving document and incremental
improvements will be published on a regular basis. For additional
information about the topic presented in this article add your comments
or questions directly in the discussion part, or visit the [Jazz.net
Forum](https://jazz.net/forum/).

## Finding information

The following table lists some good sources for information with a brief
description of each and links to RSS feeds where appropriate:

| Useful Links | Description |
|:---|:---|
| Jazz.net [library](https://jazz.net/library/#q=), [Jazz Library RSS feed](http://jazz.net/library/rss/) | The jazz.net library contains articles, videos, tips, documentation, and more. All library items have tags associated with them to help you find what you are looking for. For example the tag SCM will get you all the source control topics. |
| [Jazz Team Blog](https://jazz.net/blog/) and [Planet Jazz](https://jazz.net/planet) on jazz.net,[Jazz Team Blog RSS feed](http://jazz.net/blog/index.php/feed) | Go to the Jazz Team blog for bogs from the Jazz development team. Planet Jazz is a new page on jazz.net that aggregates blogs from the broader community of experts, users, and fans of Jazz and related technologies. |
| Jazz.net [Forum](https://jazz.net/forum), [Jazz Forum RSS feed](https://jazz.net/forum/feeds/rss) | The forum allows your to ask questions, get answers from the Jazz experts and post your own answers. |
| [CLM Information Center](InformationCenter) | Information centers (infocenters) provide a powerful online interface for finding technical information on a particular product, offering, or product solution. |

For the latest news, blogs, and tidbits about Jazz from around the Web,
you may want to subscribe to the [Jazz Community
News](http://jazz.net/pub/community/news/feed.rss) RSS feed.

As well, several sections within this article contain links to
additional material under "Further Reading" and "Advanced Topics" to
facilitate more in-depth study.

\#IntroCLM

## Introduction to CLM

This section answers the question:

"What are the basics I need to know before I get started with deploying
and configuring CLM?"

This section briefly explains the basics and provides you with links to
more in-depth information and useful tutorials.

If you would like to experiment with some of the features and
capabilities of Rational's solution for Collaborative Lifecycle
Management (CLM) and the Jazz platform, you can [create a CLM
sandbox](https://jazz.net/products/sandbox/). This is a temporary,
hosted environment, where you can create your own sandbox project and
explore and evaluate the capabilities of RTC, RQM and RRC.

### What is CLM?

CLM stands for Collaborative Lifecycle Management. It is an integrated
solution for effective Application Lifecycle Management
([ALM](http://www.ibm.com/software/products/us/en/category/SW860)).
Essentially, it provides integrations between the three core processes
at the foundation of an organization's Software Development Lifecycle
([SDLC](http://en.wikipedia.org/wiki/Software_development_process)):

-   Change and Configuration Management (CCM)
-   Quality Management (QM)
-   Requirements Management (RM)

CCM, QM, and RM are applications that provide capabilities accessible by
product licenses. They are not products - you cannot purchase QM for
example, but you can purchase RQM which gives you capabilities that are
drawn from all three applications. [Building products from
applications](https://jazz.net/blog/index.php/2010/08/16/building-products-from-applications/)
is a good reference that explains the difference between applications
and products.

CLM comprises three products - [Rational Team
Concert](https://jazz.net/projects/rational-team-concert/) (RTC) ,
[Rational Quality
Manager](https://jazz.net/projects/rational-quality-manager/) (RQM), and
[Rational Requirements
Composer](https://jazz.net/projects/rational-requirements-composer/)
(RRC) - that provide the capabilities needed by developers, quality
professionals, and requirements analysts, respectively. One or more
role-based license keys for each product permit access to capabilities
provided by deployed applications. More information on roles and
licensing is provided later in this document in the section Roles and
Licensing in CLM. For an overview of CLM 2012, refer to [Overview of the
CLM
solution](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.help.common.jazz.calm.doc/topics/c_capabilities.html)
in the Infocenter.

The products in CLM 2012 are Rational Team Concert 4.0, Rational Quality
Manager 4.0 and Rational Requirements Composer 4.0.

With the exception of the RM application, which uses the Jazz Team
Server repository for persisting data, each of the applications has its
own data store. The cross-product integrations in CLM support
traceability, web-like navigation, review, commenting, and status
tracking across project repositories with the intent to better
coordinate the flow of people, processes and information. As an example,
a developer can link an enhancement created in CCM to requirements that
were created by an analyst in RM. Additionally, a tester may link one or
more test cases created in QM to the same requirements in RM as well as
the enhancement in CCM. For readers new to CLM, the [Money that Matters
lifecycle](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.clm.tutorial.doc/topics/tut_alm_introduction.html)
scenario in the Infocenter is a excellent tutorial for exploring these
capabilities (here is a [welcome page for the
scenario](https://jazz.net/rm/web#action=com.ibm.rdm.web.pages.showArtifact&artifactURI=https://jazz.net/rm/resources/_-QrUATKjEeGFPKPBgbKpsA)).

### Components of CLM ---++++1. Jazz Team Server

The Jazz Team Server (JTS) is a separately deployed web application that
provides common services to enable applications to work together.
Services include user and project administration, security,
collaboration, query, presentation, process and other generic cross-tool
capabilities. An installed instance of an application is affiliated with
an installed instance of a JTS by registering it as a Jazz Team Server
Extension. Application integration is enabled when multiple applications
share the same JTS.

Note: While a single JTS can support multiple instances of Jazz
applications such as CCM, and QM, only one instance of RM is permitted.

Further reading:

\* Jazz Team Server
[article](https://jazz.net/projects/jazz-foundation/jazz-team-server/) -
a brief description. \* JTS is based on [RESTful web
services](http://www.ibm.com/developerworks/webservices/library/ws-restful/)
and is considered the center of the [Jazz Integration
Architecture(JIA)](https://jazz.net/projects/jazz-foundation/jazz-integration-architecture/)
\* Lifecycle resources (test cases, work items, requirements, etc) that
are exposed by these RESTful services comply with the [Open Services for
Lifecycle Collaboration](http://open-services.net/) standard.

Advanced Topics:

\* If you want to see how OSLC works, you can do a hands-on workshop
called the [OSLC Workshop](https://jazz.net/library/article/635). \* If
you want to learn how to extend the capabilities of Jazz, you can do a
hands-on workshop called the [RTC Extensions
Workshop](https://jazz.net/library/article/634).

#### 2. Jazz applications

We discussed applications in What is CLM above. A Jazz application is
any application that is deployed to provide some type of service within
a family of Jazz tools and is registered as an extension to JTS.

#### 3. Reporting

CLM 2012 offers two main reporting capabilities:

-   [Development Intelligence
    Reports](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.reporting.overview.doc/topics/c_ovr_rrdi.html)
    are used to communicate status, monitor progress, diagnose problems,
    identify corrective actions, etc. for the purpose of managing
    projects and programs. A pie chart that shows defects categorized by
    customer or a graph depicting test case execution over time are
    examples of this report type.

CLM ships with a set of predefined reports where you can set runtime
parameters for your specific need. However, in order to author new
reports or customize existing reports Rational Reporting for Development
Intelligence (RRDI) is required.

-   [Document-style Reports typically constitute a deliverable
    used](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.reporting.overview.doc/topics/c_ovr_rrdg.html)
    in subsequent phases of a project. An example is a requirements
    specification which is a compilation of requirements into document
    format that can be circulated for review and approval.

RRC, RTC, and RQM users can generate and view document style reports but
the ability to author new report templates requires that Rational
Publishing Engine (RPE) be installed.

[Rational Insight](https://jazz.net/products/rational-insight/) is
required if you want to include data from multiple JTS deployments,
other Rational applications, and third party tools, or if you need to
customize the underlying reporting data warehouse and schema. Note that
CLM 2012 requires Insight 1.1.1 or later.

Further Reading:

-   [What's New in Rational solution for Collaborative Lifecycle
    Management reporting](https://jazz.net/library/article/835)
-   [Introduction to Rational
    Reporting](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.reporting.overview.doc/topics/c_ovr_overview.html)
-   [What's New in Rational Reporting For Development Intelligence
    2.0](https://jazz.net/library/article/836)
-   [Setting up
    Reporting](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.rrdi.admin.doc/topics/t_deploying_vega.html) -
    this link provides steps to install and configure RRDI for CLM 2012
-   [Using RPE with
    CLM](https://jazz.net/wiki/bin/view/Main/CALMReportingRPE) -
    contains tutorials for using RPE with RTC, RRC, and RQM.
-   [Tips for Deploying Rational Insight in a large
    Enterprise](http://www.ibm.com/developerworks/rational/library/rational-insight-large-enterprise/index.html?ca=drs-) -
    this developerWorks article walks the reader through installing a
    version 1.0.1.1 of Insight that is currently available.
-   [Get things clear about CLM 2011 reporting
    capabilities](https://sleroyblog.wordpress.com/2011/09/21/reporting/) -
    A mind map that summarizes the basic reporting capabilities in CLM.

Advanced Topics:

-   [CLM 2011 Reporting
    Workshop](https://jazz.net/library/article/675) - a hands-on
    workshop that guides you through some of the basics of using the CLM
    reporting capabilities.
-   [CLM Framework Manager Data Model
    Details](https://jazz.net/wiki/bin/view/Main/CALMReportingDataModelDetails) -
    for the low level details and data dictionary associated with each
    of the CLM capabilities.

## Roles and licensing in CLM

A license (also known as a Client Access License or CAL) is associated
with products - RQM Quality Professional, RTC Developer, or RRC Analyst.
These licenses are installed in the JTS and then assigned to the user.
Based on the license assigned, the user has access to certain
capabilities.

A license (also known as a Client Access License or CAL) permits access
to capabilities provided by an application. Role-based licenses are
associated with products. For example, the CCM, QM, and RM applications
each have an author-class license that permits full read-write access to
their capabilities and typically only read access to capabilities
provided by other applications. The three author licenses for CLM 2012
are RTC Developer, RQM Quality Professional, and RRC Analyst. Licenses
are installed in the JTS and then assigned to a user ID. A user ID may
have more than one license assigned to it and any user using that user
ID will have access to the union of capabilities provided by all the
assigned licenses.

Most licenses are available as different types. For example, Authorized
User licenses are permanently assigned to a single user ID until they
are explicitly reassigned. Floating User licenses are acquired
dynamically from a license server when an operation is attempted and
released after an inactivity timeout or explicit logout. Token licenses
are acquired in a similar manner to Floating User licenses but each
license has a token cost and the token pool is managed by a Rational
License Server.

Further Reading:

-   For a good discussion of the types of licenses and roles, and the
    functionality available, read [Client access license management
    overview](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.repository.web.admin.doc/topics/c_license_mgmt_over.html)
    and [Floating client access license management
    overview](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.repository.web.admin.doc/topics/c_floating_licenses.html)
    in the Infocenter.
-   [Licensing in the Rational Solution for CLM
    2012](https://jazz.net/library/article/825) - Jazz.net article for
    What's new in Licensing for CLM 2012
-   [Licensing in the Rational Solution for CLM
    2011](https://jazz.net/library/article/548) - Jazz.net article with
    some discussion of licensing, as well as some how-to for setting up
    your CLM licensing.
-   [Jazz Licensing in Ten Minutes with RTC
    3.0](https://jazz.net/library/video/571) - An older video on
    Jazz.net, but a lot of the concepts still hold true.

\#NewInstall

## New CLM 2012 installation

### Planning the installation

The process for a new installation is relatively straight forward and
has been made easier with the use of the [Interactive Installation
Guide](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/roadmap_form.html).
Before you get started, you should get familiar with the [CLM
installation
process](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_example_flow_clm.html)
by reviewing the installlation process example.

It is important to note that CLM is an integrated installation - one
download contains all 3 applications and the JTS. During install you can
select what to install so that you have the flexibility to install all
applications on one application server or you can choose to spread the
applications across systems.

#### Supported topologies

There are 3 basic topologies - for details see [Topology
examples](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_topology_overview.html).

-   [Evaluation
    Topology](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_topology_evaluation_examples.html) -
    A single server install used for evaluation purposes only and then
    discarded. If you are planning to create production level artifacts
    you should start with either a departmental or enterprise topology.
-   [Departmental
    Topology](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_topology_departmental_examples.html) -
    This is a good production topology for a group or department when
    there may be limited hardware resources, or the projects and teams
    are relatively small in scope and size and unlikely to expand
    significantly.
-   [Enterprise
    Topology](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_topology_enterprise_examples.html) -
    Suitable for medium- to large-sized teams, this is a distributed
    deployment of Jazz applications meant to scale to support an
    Enterprise.

The article [Standard Collaborative Lifecycle Management
Topologies](https://jazz.net/library/article/820) on jazz.net details
standard topologies to assist you with planning your deployment.

##### Single Sign-On

Single sign-on (SSO) allows users to sign on once to gain access to all
servers without having to re-authenticate for each server. Although
Tomcat supports SSO, it limits SSO to applications that are installed on
a single server. WebSphere Application Server is more flexible where SSO
can be configured in a distributed environment. The Infocenter article
[deploying with single
sign-on](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_deploy_single_sign-on.html)
provides steps for each of the supported application servers. Here is a
[tip for deploying SSO on WAS](https://jazz.net/library/article/413).

##### Server rename

[Server
Rename](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_server_rename_overview.html),
new in CLM 2012, can be useful where you want to prepare a test staging
environment using production data or when moving a pilot deployment into
production. See [supported
scenarios](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_server_rename_sup_unsup.html)
for details. It allows you to update the Scheme/Protocol, Host name,
Port, and Context Root components of the URI. Server rename is complex,
potentially disruptive, and should only be used as a last resort when
other approaches to reconfiguring your topology are unworkable. Often
the use of DNS aliases or a reverse proxy can accomplish your goals. To
enable server rename you must obtain a feature key file from IBM
Software Support. It is called a "Server Rename Feature Key File".

Renaming the application server may require that you [update the port
number](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_ports_change.html)
on the application server. There are additional steps for [changing the
context
root](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_change_context_root.html).

Before proceeding you need to [plan for server
rename](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_server_rename_plan.html)
and review [risks and
limitations](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_server_rename_limitations.html).
The following links provide the step-by-step procedure for each of the
supported scenarios:

-   [Renaming your Rational solution for Collaborative Lifecycle
    Management server](https://jazz.net/library/article/818)
-   [Setting up a test staging environment using production
    data](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_prepare_sandbox_server_rename.html)
-   [Moving a pilot deployment into production using server
    rename](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_change_server_name.html)

\#UriPlanning

#### URI planning

Choosing a public URI for long-term stability is very important as the
applications and JTS generate absolute URIs to resources that are used
for stable resource identification across all applications. In many
cases the URIs are persisted in the repository databases and stored
resources may contain links between them as well as to resources in
other applications. Once resources have been stored in the repository,
changing the URI will have serious consequences.

The absolute URI is rooted by a public URI that is declared for the
applications and JTS. Therefore it is imperative that you choose a
public URI that is [fully
qualified](http://en.wikipedia.org/wiki/Fully_qualified_domain_name),
likely to remain stable over time, and is accessible from anywhere in
the network where users need to connect. Here are some additional
considerations:

-   Use hostnames that can be resolved via DNS (NEVER USE 'localhost' or
    an IP address).
-   Moving a Jazz application from one server to another (even one with
    a different IP address) will maintain any links to the data in the
    repository as long as the domain name remains unchanged and is
    mapped to the new IP address.
-   You must specify a context root for web applications that are
    deployed within the application server. The context root appears
    immediately after the host and port segment of the URL. Default
    context roots are listed below:

| Default Context Root | Description |
|:---|:---|
| /jts | the Jazz Team Server |
| /ccm | Change and Configuration Management capability (provided by RTC) |
| /qm | Quality Management capability (provided by RQM) |
| /rm | Requirements Management capability (provided by RRC) |
| /admin | Jazz Project Administration capability |
| /clmhelp | Help resources |

Example: for a server named jazz_ccm.demo.test, with the /ccm capability
running on it, the base URI for the CCM resource would be
<https://jazz_ccm.demo.test:9443/ccm>.

-   When planning a new installation, if you do not want to use the
    default port numbers (9443) for the application servers you can
    change them. Changing the port numbers for the application server
    explains how.
-   Consider using a reverse proxy or DNS aliases (see the next section)

##### Reverse Proxy and DNS alias

Using a reverse proxy or DNS aliases will help ensure you have the
flexibility to update your topology in the future.

-   A [reverse proxy](http://en.wikipedia.org/wiki/Reverse_proxy) is a
    type of proxy server that retrieves resources on behalf of a client
    from the application servers sitting 'behind' the reverse proxy
    server. For more information see [Using a reverse proxy in your
    topology](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_reverse_proxy.html)
    and a recent blog with additional links to articles explaining
    reverse proxy servers and how to configure them. Here are
    [instructions](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_config_reverse_proxy_ihs.html)
    for configuring the IBM HTTP server as a reverse proxy for IBM
    Websphere Application Server.

<!-- -->

-   Another option is to use a [DNS
    alias](http://en.wikipedia.org/wiki/CNAME_record) for each
    application in your topology so that the public URI can remain
    stable in the event you need to change the configuration.

Further Reading:

-   [Moving Jazz Servers and URI Stability with CLM
    2011](https://jazz.net/library/article/686) - A Jazz.net article on
    the topic of URI stability.
-   [You Can't Change the Public URI. Really. You
    can't](http://jazzpractices.wordpress.com/2011/07/21/you-cant-change-the-public-uri-really-you-cant/) -
    Another perspective on URI stability from the Jumpstart team.
-   [What's the Deal with the CLM Public
    URI?](http://blog.boriskuschel.com/2012/03/whats-deal-with-clm-public-uri.html) -
    blog about the importance of selecting an appropriate public URI
-   [Solving Real World Problems using Rational
    Technologies](https://www.ibm.com/developerworks/mydeveloperworks/blogs/dchadwick/entry/public_urls_are_casted_in_stone_how_do_i_plan_for_the_future4?lang=en_us) -
    developerWorks article that provides some guidance on selecting a
    public URL.
-   [Understanding reverse proxy](UnderstandingReverseProxy)
-   [Configuring Enterprise CLM Reverse Proxies: WebSphere 8 and IHS
    8](ConfigureCLMEnterpriseReverseProxy)
-   [Configuring Enterprise CLM Reverse Proxies: Apache and
    mod_proxy](ConfigureCLMEnterpriseReverseProxyWithApache)
-   [Configuring Enterprise CLM Reverse Proxies: WebSphere 8.5 ND
    Proxy](ConfiguringEnterpriseCLMReverseProxiesWebSphere85NDProxy)

#### Client / server compatibility

In release 4.0, client N-1 compatibility is supported, which means that
you can upgrade a server to the next release without the need to upgrade
the clients. This backward compatibility applies to the following
clients and is illustrated in the table below:

-   Client for Eclipse IDE
-   Client for Microsoft Visual Studio IDE
-   SCM command line
-   ISPF client

\|\*Eclipse & Visual Studio Client \*\|**Jazz Team Server**\|\|\|\|

|           |         |             |         |         |
|-----------|---------|-------------|---------|---------|
| \^        | **4.0** | **3.0.1.x** | **3.0** | **2.x** |
| **4.0**   | yes     | no          | no      | no      |
| **3.0.1** | yes     | yes         | no      | no      |
| **3.0**   | yes     | yes         | yes     | no      |
| **2.x**   | no      | no          | no      | yes     |

When a server/client mismatch occurs, a friendly dialog explains the
version mismatch. An option is available for customizing the message to
direct users to the location where they can download new clients. How to
do this is explained in [this
article](https://jazz.net/library/article/524) on jazz.net (in the
article, search for the string 'Set the client version mismatch
messages').

As per the above table, RTC users who require access to both v3.x and
v4.0 servers must use a v3.x RTC Eclipse client. If users need to access
both v2.x and v3.x (or v4.0) servers they must use separate RTC Eclipse
clients for each since no single client will work with both servers.

**Notes:**

1.  RTC 4.0 eclipse client can run in Eclipse 3.6 and 3.7 (3.6.2.2 is
    bundled) and supports shell sharing.
2.  RTC repository workspace compatible from v2.x or v3.x to v4.0
    client.
3.  RQM and RRC 4.0 clients are web-browser based. There is no Eclipse
    client for these products.
4.  CLM 4.0 Server Rename feature: you must upgrade all RTC clients
    (including build engines) to version 4.0 prior to the rename.

#### Performing the installation

For an understanding of the key concepts that are involved in performing
the installation, refer to [Understanding the deployment and
installation
process](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_what_to_install.html).

For a new CLM installation you will perform the following:

-   Prepare for the installation - see [Preparing the
    installation](#PrepInstall).
-   [Use the Interactive Installation Guide](#UseIUG) to guide you
    through the installation steps. You can choose various options to
    define your topology including whether you want to install RRDI.
-   [Run the setup wizard](#RunSetup) to connect the applications and
    database to JTS v4.0.
-   You probably don't have a build system installed so refer to
    [Install and configure the build system](#InstallBuildsys).
-   If you plan to use floating CALs or Token services for your
    licensing scheme then you must [install and configure a license
    server](#InstallLIC).
-   If you want the ability to author new document style report
    templates you will need to [install and configure RPE](#InstallRPE).

\#PrepInstall

##### Preparing the installation

Before starting:

-   Be sure to have properly selected your URI's for your Jazz
    capabilities. See [URI Planning](#UriPlanning) for more information.
-   Read the release notes available on the product downloads pages.
-   Verify that the [system
    requirements](https://jazz.net/library/article/811) are met.
-   Decide on the user registry to be used. Your options will depend on
    the application server you are using. Tomcat has a default user
    registry whereas WebSphere offers a range of possible configurations
    for user registry as described in [Selecting a registry or
    repository](http://pic.dhe.ibm.com/infocenter/wasinfo/v7r0/topic/com.ibm.websphere.base.doc/info/aes/ae/tsec_useregistry.html).
    Both application servers can be configured to use LDAP. Refer to
    [setting up user
    management](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_plan_user_management.html)
    for details.
-   Decide on the database vendor to be used and review the installation
    instructions in [Setting up the
    database](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_s_server_installation_setup_db.html).
    Instructions are provided for DB2, Oracle, and SQL server.

For an enterprise deployment you will need to install a database server
and configure a database for each of the following:

-   Data warehouse database (optional)
-   Jazz Team Server database
-   CCM database (if the CCM application will be installed)
-   QM database (if the QM application will be installed)
-   RRDI content store (if RRDI is installed)

Note: RM does not require its own database as it uses the JTS database.

\* If installing RRDI, make sure that the RRDI application is installed
on a separate server instance. This will ensure that heavy reporting
loads on the system do not impact the performance of the CLM tools. \*
Review the [Collaborative Lifecycle Management 2012 Sizing Report
(Standard Topology E1)](SizingReportCLM2012) to assist you with
maximizing system performance. Also review [factors that can affect
performance](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Ft_max_perf.html).
\* Have your instructions handy. It is strongly recommended that you use
the [Interactive Installation
Guide](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/roadmap_form.html)
available from the Infocenter as it compiles installation instructions
specific to your scenario.

-   New for CLM 2012: If you are using Websphere Application Server, you
    now have the option to configure a cluster of app servers.
-   If you need to be able to author new reports or customize existing
    reports be sure to select 'yes' to install Rational Reporting for
    Development Intelligence.

If you want to install the product as a non-root user on UNIX systems or
as a non-administrator on Windows, in the Select user mode for
Installation Manager, select Non-Administrator.

\#UseIUG

##### Use the interactive installation guide

The [Interactive Installation
Guide](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/roadmap_form.html)
takes you through the following main steps:

**Planning checklist**

\* [Installing the server using IBM Installation
Manager](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_s_server_installation_im.html) -
you have 2 options - a web based install or a local install.

-   Install and configure databases. You can use Derby which is included
    with the installer but its use should be limited to trial and demo
    deployments. And note that RRDI does not support Derby - although
    you can configure a data warehouse on Derby, you will not be able to
    migrate your data to another database vendor.

For any other deployment, instructions are provided for
[DB2](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_s_server_installation_setup_db2.html),
[Oracle](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_s_server_installation_setup_oracle.html),
and [SQL
Server](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_s_server_installation_setup_sql.html).

-   Install, set up, and start the Application Server(s) - Tomcat
    Application Server v7.0 comes with the installation but if you are
    planning to use Websphere Application Server then you should not
    install Tomcat. During installation, you will be asked to provide
    the directory where the webbapps are to be placed (the default
    location is JazzInstallDir/server/webapps). Later in the install
    process you will deploy these web apps to the application server.

<!-- -->

-   If you selected to install Tomcat v7.0 you are good to go. To start
    the server(s) refer to [Starting the Apache Tomcat
    Server](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/m_s_server_installation_start_tomcat.html).
    Websphere Application Server (WAS) is a separate install - you can
    set up WAS using the [Integrated Solutions
    Console](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_s_server_installation_setup_WAS.html)
    or using [Jython
    scripting](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_configure_was_jython.html).
    Depending on your desired topology, you may be installing one or
    more application servers (eg. one app server for each of JTS, CCM,
    QM, RM).

<!-- -->

-   WAS includes some addition steps to [configure the server to use
    LDAP](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_instl_config_ldap_on_was.html)
    (this is optional) and to [deploy the web applications and start the
    server](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_deploy_was.html).
    In addition to the web archives for JTS, CCM, QM, and RM, you will
    also be deploying web archives for the following applications:
    -   Lifecycle Project Administration (LPA) - admin.war
    -   Information Center (IC) - clmhelp.war
    -   RM view mode version of the graphical artifacts - converter.war

<!-- -->

-   Install the RTC client for Eclipse IDE. Refer to [Install the
    Eclipse Client](#InstallEclipse) later in this article.

<!-- -->

-   If you selected to install RRDI, the installation package consists
    of Rational Report Server and optional sample reports (the samples
    are not related to CLM data). [Review the planning
    checklist](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.rrdi.admin.doc/topics/c_planning_tasks_checklist.html),
    [installation
    requirements](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.rrdi.admin.doc/topics/c_install_req_overview.html),
    and [deployment
    scenarios](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.rrdi.admin.doc/topics/c_install_topology_overview.html)-
    for a departmental or enterprise deployment, RRDI is installed on a
    separate application server with its content store created on the
    database server. The installation procedure is described in
    installing
    [RRDI](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.rrdi.admin.doc/topics/t_install.html).

<!-- -->

-   Once RRDI has been installed, you will need to [create the database
    for content
    store](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.rrdi.admin.doc/topics/t_configure_content_store_combine.html),[
    Initialize the reporting
    server](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.rrdi.admin.doc/topics/t_postinstall_config_setup_app.html)
    and then run the [RRDI set up
    wizard](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.rrdi.admin.doc/topics/t_postinstall_start_setup_app.html)
    to configure RRDI. Finally integrating RRDI with CLM data requires
    that you load the Cognos archive files from the JTS as described in
    [Integrating RRDI with CLM data
    sources](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.rrdi.admin.doc/topics/t_postinstall_integrate_rrdi_clm.html).

<!-- -->

-   Now that the servers are started run the setup wizard as described
    next.

\#RunSetup

##### Run the setup wizard

The Setup Wizard walks you through some final configuration steps to
connect the applications and database to JTS v4.0. The Setup Wizard
helps you to:

-   Configure the public URI
-   Configure database connections
-   Configure email settings
-   Register applications
-   Configure the user registry
-   Configure the data warehouse
-   Finalize Setup for each application

After ensuring the application server(s) have been started launch the
wizard. In a browser window type:

**\[fully qualified hostname\]:\[port number\]/jts/setup**

The default port number for the application servers is 9443. It is
recommended that each of the application servers and applications have
their own unique port numbers. This makes it easier to debug any
potential performance issues and allows for implementation of a [reverse
proxy
server](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_reverse_proxy.html)
at a later time. You can change the port number by referring to the
following procedure: [Changing the port number for the application
server](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_ports_change.html).
You should also select a unique context root. Note that you should
change the port number and context root ***before*** setting the public
URI for your applications.

The JTS, along with the applications registered to the JTS, is called an
application group. In a single server configuration, the applications
that need to be registered are found automatically. In a distributed
system, where the applications are installed on different machines from
the JTS (we call these 'remote' applications), registering the
applications with the JTS can be done when you initially set up your CLM
environment by [running the setup
wizard](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_s_server_installation_setup_wizard.html)
for enterprise deployments or you can [run the setup on the
command-line](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_running_setup_command_line.html).

If you have an existing Jazz CLM environment, and you are adding a new
server and/or capability, then you will need to register the new
application with the JTS by following to these
[instructions](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.repository.web.admin.doc/topics/t_register.html).

\#InstallBuildsys

##### Install and configure the build system The Jazz Build System Toolkit contains the Jazz Build Engine (JBE) and a toolkit of Ant tasks that processes manual and scheduled build requests, executes builds, and publishes logs. You can use any build engine to run Jazz Team Builds (such as the Build Forge build engine). For details on variations refer to [Jazz Team Build setup variations](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.team.build.doc/topics/csetupwithexistingtools.html).

The Build System Toolkit can be be installed [using the IBM Installation
Manager](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/t_install_build_toolkit_im.html)
or it can be installed from a .zip file. If you will be using the Build
Forge build engine, refer to [Installing the Rational Build
Agent](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/BF_install_buildagent_overview.html).

For an overview of the steps involved in setting up and running a
typical Jazz Team Build, refer to [A typical Jazz Team Build
setup](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.team.build.doc/topics/c_buildsetup.html).
The detailed procedure for performing the build tasks can be done [using
the Eclipse
client](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.team.build.doc/topics/c_working_in_eclipse.html)
or using the Web client. If you intend to use the Eclipse client, refer
to [Install the Eclipse Client below](#InstallEclipse).

Further Reading:

\* Getting Started with Setting up Jazz Builds \* Continuous Integration
Best Practices with RTC \* Using the Hudson Build Integration with RTC
\* How To Do Maven Releases with Jazz SCM \* RTC Plugin for Jenkins

\#InstallLIC

##### Install and configure a license server

If you plan to use floating CALs or Token services for your licensing
scheme then you will need to install and configure a license server.

Floating CALs are managed as a pool that are shared by multiple users
who acquire a license when they need it and return it to the pool when
they are done. You can either have a dedicated JTS that serves floating
CALs or you can use an existing JTS. See [Installing and managing
floating client access license
keys](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.repository.web.admin.doc/topics/tmanagefloatinglic.html)
for instructions on configuring a floating license server and to point
other jazz team servers to the license server.

A floating CAL server can also distribute Rational Common Licensing
(RCL) tokens. Jazz services have a predetermined 'token cost' associated
with them and when a user invokes the service, the required number of
tokens are checked out from the license server. Token services requires
an additional license server called the IBM Rational License Key Server.
Please refer to the [RCL
information](http://publib.boulder.ibm.com/infocenter/rational/v0r0m0/index.jsp)
center for installation instructions.

For more information on Jazz Licensing and some background on how it
works, check out the [CLM 2011 Licensing
Article](https://jazz.net/library/article/548). Some of it may be out of
date, but the core concepts hold true.

\#InstallRPE

##### Install and configure RPE

Refer to the Rational Publishing Engine 1.1.2.2 Infocenter for
instructions on [Installing
RPE](http://publib.boulder.ibm.com/infocenter/rpehelp/v1r1m1/topic/com.ibm.rational.pe.install.doc/topics/t_installing_rpe_1.1.2.html)
and integrating CLM data sources ([integrating
RTC](http://publib.boulder.ibm.com/infocenter/rpehelp/v1r1m1/topic/com.ibm.rational.pe.integration.doc/topics/c_rtc_integrate.html),
[ integrating
RQM](http://publib.boulder.ibm.com/infocenter/rpehelp/v1r1m1/topic/com.ibm.rational.pe.integration.doc/topics/c_rqm_integrate.html),
and [integrating
RRC](http://publib.boulder.ibm.com/infocenter/rpehelp/v1r1m1/topic/com.ibm.rational.pe.integration.doc/topics/c_rrc_integrate.html))
with RPE.

\#InstallEclipse

##### Install the Eclipse Client

There are three ways to install the client. Refer to [Client
Installation
Overview](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_client_installation_overview.html)
for details.

\#UpgradeCLM

## Upgrade to CLM 2012

**Before proceeding**: If you have Insight in your current deployment,
you will require Insight version 1.1.1 or higher along with the upgrade
to CLM 2012. Check the latest system requirements of the CLM version you
are upgrading to for complete details. If you are upgrading from CLM
2010, you can proceed with the first step (upgrade to CLM 2011) and then
proceed with the upgrade to Insight 1.1.1or higher.

If you have RRDI in your current deployment, upgrade to CLM 2012 first
then proceed with the upgrade to RRDI. **Note**: This suggested order is
the latest recommendation as of June 2013

For more information on the reporting considerations during an upgrade,
please see [Reporting
Considerations](https://jazz.net/wiki/bin/view/Deployment/UpgradePlanning#Reporting_considerations)
section in Upgrade Planning deployment wiki page.

CLM 2012 is backward compatible with the 3.0.x clients and servers
providing you with more flexibility in planning and executing your
upgrade. You can execute the upgrade in stages, say by starting with the
JTS and one application, such as CCM, and upgrading those applications
first. Then, at a later time you can upgrade the remaining applications
as well as the Eclipse and Visual Studio clients.

Although a mixed 3.x and 4.0 environment is supported, for compatibility
with JTS 4.0 you will need RQM 3.0.1.3 and RRC 3.0.1.4.

If you are upgrading from CLM 2010, you will need to perform a 2-step
upgrade process by first upgrading to CLM 3.0.1.x (also known as CLM
2011) and then finally to CLM 2012.

### Two-step upgrade from CLM 2010 to CLM 2012

Upgrading from CLM 2010 to CLM 2012 is a 2-step process:

1.  Upgrade from CLM 2010 to CLM 2011: refer to [Understanding the
    deployment and upgrade
    process](http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.install.doc/topics/c_understand_upgrade.html)
    in the 3.0.1 Information Center. As well, review the [Upgrade
    process
    examples](http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.install.doc/topics/c_upgrade_process_overview.html)
    and [Upgrade topolgy
    example](http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.install.doc/topics/c_upgrade_topology_overview.html)
    and then use the [Interactive upgrade
    guide](http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html)
    to perform the upgrade to CLM 2011. Note all these links are on the
    3.0.1 Information Center. For a summary of the tasks you should
    complete in preparation for the upgrade, read the article [Upgrade
    reference for CLM 2011](https://jazz.net/library/article/698). The
    [CLM 2011 Upgrade Workshop](https://jazz.net/library/article/662)
    provides a hands-on walk through of the CLM 2011 upgrade process.
    The [CLM 2011 Upgrade FAQ](https://jazz.net/library/article/679) is
    also a great source of information. 2. Upgrade from CLM 2011 to CLM
    2012 - see the next section below.

If the upgrade is planned such that step 2 is to be done at a later
time, the eclipse and visual studio clients should be upgraded to be
compatible with the 3.0.1 server at the same time step1 is done. If it
is acceptable that the client upgrades can wait until the upgrade is
complete, it would be wise to inform users that only the web client
should be used in the interim. Here are [instructions for upgrading the
clients](http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.install.doc/topics/c_upgrade_client_vs_eclipse.html)
to v3.x.

### Upgrade from CLM 3.0.1 to CLM 4.0

For an understanding of the key concepts that are involved in performing
an upgrade, refer to [Understanding the deployment and upgrade
process](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_understand_upgrade.html).
You should also review [Deployment and upgrade
considerations](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_upgrade_consideration.html),
[Upgrade process
example](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_upgrade_flow_clm.html),
[Upgrade topology
example](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_upgrade_topology_ex_dist_clm_ent.html),
and the [CLM 2012 Upgrade Guide](https://jazz.net/library/article/819).

A CLM 3.0.1 to CLM 4.0 upgrade requires a full installation of CLM 4.0
followed by an upgrade script (one for each application) which migrates
and updates configuration files, adds tables to the various database
repositories in place, and upgrades the data warehouse. The upgrade
should be staged with the JTS being upgraded first, followed by the
applications, which can be done in any order. Use the interactive guide,
[Upgrading to version
4.0](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html),
to generate upgrade instructions specific to your deployment topology,
application and database servers, data warehouse configuration, product
integrations, etc. It is important to note that you should not run the
setup wizard during the upgrade process.

An upgrade in a Tomcat environment is straight-forward and essentially
involves shutting down each of the servers hosting the JTS or CLM
application, installing the JTS or CLM application, running an upgrade
script on each server to update configuration files and tables (and the
data warehouse in the case of JTS), and lastly, starting the servers.
Note that for the RM application, there is an online migration phase
after the server has been started.

An upgrade in a WAS deployment involves additional steps to backup the
server profile, uninstall the 3.0.1 JTS/CLM apps from WAS, clean up some
directories, update properties, etc. and then running an upgrade script
on each server to update configuration files and tables (and the data
warehouse in the case of JTS). After starting the server, the last step
is to deploy the 4.0 war files and start the applications. Note that for
the RM application, there is an online migration phase after the server
has been started.

To review an upgrade scenario in a fully distributed WAS deployment
refer to the article [CLM 2012 Upgrade
Guide](https://jazz.net/library/article/819) on jazz.net. The CLM 4.0
upgrade guide also provides troubleshooting and FAQ sections as well as
other information to help guide you through the upgrade process.

Notes:

1.  3.0.1 did not require 64bit OS - whereas a 64 bit OS is a
    requirement for 4.0
2.  The 2011 Eclipse and Visual Studio clients are compatible with CLM
    2012 and can therefore be upgraded at a later time. Here are
    [instructions for upgrading the
    clients](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/c_upgrade_client_vs_eclipse.html).
3.  For RRC you still need to perform an online migration. Instructions
    are provided in the interactive upgrade guide [Upgrading to version
    4.0](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html).

### Upgrade an existing Jazz environment to CLM 2012

In this scenario you already have a Jazz-based product (RTC, RQM, RRC)
in your network and now you would like to upgrade to CLM 2012.

If you are starting with a 2.x product, you will have to upgrade the
product to 3.0.1 first by following the [Interactive upgrade
guide](http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html)
in the 3.0.1 Information Center. As you select the options that describe
your environment, you will choose your deployment topology. This is
where you can specify that you want to begin distributing your
applications on multiple machines if you have not already installed a
separate JTS.

If you are starting with 3.0.1 products or have just finished upgrading
to 3.0.1, the next step is to upgrade to version 4.0 using the
[Interactive upgrade
guide](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html)
in the 4.0 Information Center.

Now that you have upgraded to version 4.0, the next step is to install
the remaining applications to make up a full CLM 2012 offering. For
this, use the [Interactive installation
guide](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.install.doc/topics/roadmap_form.html).

### Administration

Before we start, a few definitions would be useful. A
[repository](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.repository.web.admin.doc/topics/c_repository.html)
is a central location for tool-specific information. It is a data store
containing top level objects called items that have a Universally Unique
Identifier (UUID). Some item types maintain a history of changes for
audit purposes, while other item types do not. APIs are provided for
creating, retrieving, updating and deleting items as well as running
queries on the repository.

Each CLM application (CCM, QM, RM) uses a [project
area](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/c_project_area.html)
to organize a software project. A project area is a top level or root
item in a repository that defines the project's deliverables, team
structure, process, and schedule. There can be many project areas in a
repository. In a CLM deployment, artifacts across application projects
can be linked to support cross-application traceability.

A project area can contain multiple teams and [team
areas](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/c_team_area.html)
are the mechanism for organizing them. A team area includes team
members, the timeline to which the team is assigned, and the process to
which the team has subscribed. Team areas are optional - they may not be
needed for small projects or project teams.

In CLM, each of the applications has their own project area. A
[lifecycle
project](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.team.concert.doc/topics/c_getting_started_project_areas_and_lifecycle_projects.html)
groups multiple project areas so that the project areas can be managed
from a central location. The application that is used to administer
project areas is called Lifecycle Project Administration (LPA). In [Run
the Setup Wizard](#RunSetup) during a new CLM installation you may
recall registering LPA with the server.

#### Common project administration

There are several administrative tasks that are common to CCM, QM, and
RM such as creating project areas and team areas, creating timelines and
iterations, adding users to a project area, and adding and modifying
roles and permissions. These common administration tasks are described
in [Administering project areas: Tasks for all applications (web
client)](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/c_common_project_admin_tasks.html).
Alternatively, you can use the Lifecycle Project Administration (LPA)
application to create and manage project areas across applications,
which is what we will be doing in the next section.

##### Setting up projects

To create a lifecycle project and project areas, [log into Lifecycle
Project
Administration](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/t_starting_project_administration_application.html)
and either [create a lifecycle project from a
template](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/t_creating_aggregate_projects_from_template.html)
or, if you have existing project areas, then you can
\[<http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/t_creating_aggregate_project_and_adding_project_areas.html>\[\]\[create
a lifecycle project and add existing project areas\]\].

When you create a project area you will need to specify a process
template to use.
[Process](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/c_process.html)
specifies the roles, practices, rules, and guidelines that are used to
organize and control the flow of work in a project. It defines
permissions for performing operations within the project, and can be
used to define project reports, queries, and work item types. Jazz
includes [process
templates](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/c_process_template.html)
for common processes that you can use as-is or customize to suit your
organization.

If users have not yet been created, follow the [instructions to create
users](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.repository.web.admin.doc/topics/taddnewuser.html)
in the Jazz Team Server repository. Once created, users can be added to
projects (see [add members to
projects](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/t_adding_members_to_projects.html))
and assigned roles (see [assigning
roles](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/t_assigning_roles_lpa.html)).
[Roles](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/c_roles.html)
identify the functions of team members and determines which operations a
user can perform. If email notification has been enabled, the newly
added user will receive a team invitation with instructions on how to
accept it.

Once you have your project areas created and have added members the next
steps are to [create timelines, iterations, and iteration
types](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/c_creating_timelines_iterations_iteration_types.html)
and optionally [create team
areas](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/c_creating_team_areas_associating_categories.html)
for organizing project teams. For a complete set of common
administrative tasks refer to [Administering project areas: Tasks for
all applications (web
client](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/c_common_project_admin_tasks.html)).

##### Enabling email notification 
You can modify the server configuration properties such as database connections, feed settings, OAuth consumers, etc. from the admin page of the JTS or the admin page of an application registered with the server. See [Configuring the Server](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.repository.web.admin.doc/topics/tconfigserver.html) for a complete list but for now, if you want to send email notifications to work item owners and subscribers to inform them of changes then you need to [configure e-mail settings](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.repository.web.admin.doc/topics/tconfigemail.html) since the default is that email notifications are disabled.

##### Managing users

User information is stored in the JTS database where it is shared by the
server and by all applications registered with the JTS. User information
is also stored in an external registry such as LDAP. A task can be
scheduled to run regularly to synchronize data in the two locations. For
details refer to [Managing
users](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.repository.web.admin.doc/topics/tmanageusers.html) -
when getting started with CLM 2012, the key user administration
functions are [creating
users](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.repository.web.admin.doc/topics/taddnewuser.html)
and [assigning
licenses](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.repository.web.admin.doc/topics/tmanageusercal.html).

#### Additional administrative tasks

The above description focused on the administrative tasks that are
common to CCM, QM, and RM. Additional administration tasks specific to
these applications can be found in [Administering change and
configuration management project
areas](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.jazz.platform.doc/topics/t_projects_teams_process.html),
[Administering quality management project
areas](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.test.qm.doc/topics/c_admin_test_projects.html),
and [Administering requirements
projects](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.rational.rrm.help.doc/topics/t_admin_rrc.html).

##### Related topics: 
-   None

##### External links: 
-   [Jazz Administration Guide (3.x)](https://jazz.net/library/article/543) - While this was written for 3.x, it provides a template for the important information and tasks that you need to be aware of as a jazz Administrator. 

##### Additional contributors:
-   None
