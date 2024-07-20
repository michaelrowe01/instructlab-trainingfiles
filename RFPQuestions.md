META:TOPICINFO{author="lekandrade" date="1694625191" format="1.1"
version="1.15"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Request for proposal (RFP) questions [request-for-proposal-rfp-questions]

DKGRAY Authors: [Dan Toczala](Main.DavidToczala) Build basis: 4.x and
later ENDCOLOR

TOC{title="Page contents"}

Customers often ask questions in a request for proposal (RFP) or in some
other fact-finding document. This page has a list of common RFP
questions and the answers to those questions. The page is divided into
the major sections that RFPs often contain.

## General / Technical

Question: What is the 3-year roadmap for your ALM solution?

-   We follow an agile continuous delivery process. Each release is
    planned and scoped based on our backlog of user submitted
    enhancements. We have an 'open commercial' model that stresses
    customer visibility to our current and upcoming plans. Access to our
    planning is available here:
    <https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.dashboard.viewDashboard&tab=_1>

Question: What software enhancements are currently planned for the next
released version of your product and when they will be available?

-   The current release we are working on is CLM 6.0.1 and it is
    scheduled to release in December 2015. Refer to our ALM Calendar:
    <https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.dashboard.viewDashboard&tab=_125>

Question: Who are your industry and technology partners?

-   We have a large ecosystem of business partners. On the page
    referenced below are listed partners with Ready for IBM Rational
    validated integrations to Jazz-based products. Visit our
    Integrations page to learn more about integrations between Rational
    products and Rational products, BP products, and third-party
    products.
    -   IBM Rational Business Partners:
        <https://jazz.net/community/partners/>

## Architecture and performance

Question: How is your solution is architected?

-   The Jazz solution has a basic three-tier web application
    architecture. For diagrams and explanations of this architecture,
    see the [Collaborative Lifecycle Management architecture
    overview](CLMArchitectureOverview), and the [Jazz standard
    topologies](https://jazz.net/library/article/820).

Question: How is your solution is designed to meet the best level of
performance through lowering response times?

-   The Jazz solution is based on the concept of "linked data." By
    having data accessible through REST-based mechanisms, the clients
    that access that data are able to use a standard HTTP protocol to
    address the various software development artifacts. This ability to
    directly address and manipulate these artifacts means that very
    little "control" information is passed along the network. The only
    data that is transmitted is the data that is essential to typical
    operations, thus optimizing network usage and solution performance.
    Calculations are done where they are needed and are able to be done
    most efficiently, either at the application server, or within the
    client or browser.

Question: Which mechanisms or approaches can help to reach adequate
performance level on a WAN architecture?

-   Because this is a REST-based architecture, static content (such as
    files or versions stored in the SCM system) can be "cached" for
    performance improvements using standard network acceleration
    technologies. While performance on a WAN does depend on the latency
    and throughput available on the WAN, use of content caching proxy
    servers or other network caching technologies can help improve end
    user performance.

Question: Does your solution use open source?

-   The Jazz solutions will *integrate* with many different open source
    solutions, and our products do utilize some open source code. This
    is highlighted in our certificates of originality (COO).

Question: What is the software life cycle and revision history of this
proposed solution?

-   The Jazz products are developed out on [Jazz.net](http://jazz.net).
    We currently use a continuous delivery process for delivering our
    products, and you can learn more about this process by reading about
    how we do [continuous delivery
    planning](https://jazz.net/wiki/bin/view/Main/RTCContinuousDeliveryPlanning).

Question: How secure is this product? What is the authentication
mechanism?

-   The Jazz solutions will typically be used in conjunction with the
    LDAP solution being used by the organization. User authentication is
    provided using OAuth. For more information, see the
    [security](https://jazz.net/wiki/bin/view/Deployment/JTSAuthenticationExplained)
    page.

Question: Are there limits on the scalability of the Jazz solution?

-   Everything has limits. As Jazz deployments need to scale to have
    additional capacity, additional instances of RTC (CCM) and RQM (QM)
    can be deployed under the same Jazz Team Server (JTS). This is not
    yet possible with the RRC (RM) component. In order to get an idea of
    how many users and projects can be hosted by a single Jazz instance,
    we suggest reviewing the [performance datasheets and sizing
    guidance](https://jazz.net/wiki/bin/view/Deployment/PerformanceDatasheetsAndSizingGuidelines)
    for your particular version of the solution.
-   We also **strongly suggest** that you put some type of [performance
    and service
    monitoring](https://jazz.net/wiki/bin/view/Deployment/DeploymentMonitoring)
    in place with your Jazz deployment.

Question: Are client-side components needed, such as Java applets, Java
applications, Flash, plug-ins or ActiveX controls? Indicate versions (if
applicable) and associated security controls.

Question: Are there documented procedures for performing stress or load
testing on your service or application? If so, what were the results?
How often are these tests performed and are the results retained?

-   See
    <https://jazz.net/wiki/bin/view/Deployment/PerformanceDatasheetsAndSizingGuidelines>

## Administration

Question: What operating systems does this work with?

-   Check out the Systems Requirements section of the [Installing,
    upgrading and
    migrating](https://jazz.net/wiki/bin/view/Deployment/DeploymentInstallingUpgradingAndMigrating)
    page on the deployment wiki, for the systems requirements
    appropriate for your specific release.

Question: What databases are supported?

-   Check out the Systems Requirements section of the [Installing,
    upgrading and
    migrating](https://jazz.net/wiki/bin/view/Deployment/DeploymentInstallingUpgradingAndMigrating)
    page on the deployment wiki, for the systems requirements
    appropriate for your specific release.

Question: What web browsers are supported?

-   Check out the Systems Requirements section of the [Installing,
    upgrading and
    migrating](https://jazz.net/wiki/bin/view/Deployment/DeploymentInstallingUpgradingAndMigrating)
    page on the deployment wiki, for the systems requirements
    appropriate for your specific release.

Question: Is there any additional hardware that should be purchased for
optimal performance?

-   For optimal performance in scenarios when Jazz SCM is being used, it
    is suggested that a caching proxy be utilized to improve end user
    response time, and to lighten the load on the Jazz infrastructure.
    For more information on this, read [Using content caching proxies
    for Jazz Source
    Control](https://jazz.net/wiki/bin/view/Deployment/ContentCachingProxyJazzSCM).

Question: What are the minimum processor speed and memory requirements
for the CLM applications?

-   Check out the Systems Requirements section of the [Installing,
    upgrading and
    migrating](https://jazz.net/wiki/bin/view/Deployment/DeploymentInstallingUpgradingAndMigrating)
    page on the deployment wiki, for the systems requirements
    appropriate for your specific release. In addition, we provide
    suggested hardware and architecture that is called out in our
    [standard topologies
    overview](https://jazz.net/wiki/bin/view/Deployment/StandardTopologiesOverview).

Question: What network connectivity speeds are needed for the ideal
operation of these products?

-   For ideal operation of the Jazz solutions, we would like to see the
    highest speeds, lowest latencies, and highest bandwidth possible.
    The faster you go, the better the end user experience will be. The
    network speed between the application servers and the database
    server should be at least 100 Mbit/s, with 1 Gbit/s preferred. In
    most cases a standard broadband connection to the client is
    sufficient.

Question: In terms of historical data archiving, how long does your
solution keep historical data for trending and analysis?

-   Data is never destroyed. Data is held in a data warehouse, which is
    used to provide historical data for reporting purposes.

## Integration

Question: Provide a list of all of the tools that your products
integrate with.

-   Any list of ALL of the tools that the Jazz products integrate with
    would be outdated soon after it was published. The current list of
    [supported integrations](https://jazz.net/extend/integrations/) is
    maintained out on [Jazz.net](http://jazz.net).
-   The Jazz based tools are all integrated with each other, providing a
    seamless user experience as the user navigates between the various
    capabilities provided by the tools. Jazz products utilize
    [OSLC](http://open-services.net/) to provide integrations with a
    large number of tools from both IBM, as well a other vendors. You
    can learn about OSLC by going through things like the [OSLC
    Workshop](https://jazz.net/library/article/635). There is also a
    [TRS workshop](http://wiki.eclipse.org/Lyo/TRSWorkshop) provided out
    on the [Eclipse website](http://wiki.eclipse.org/Main_Page), which
    covers the creation of a TRS (Tracked Resource Set) provider.

## Extensibility

Question: How is the product designed for future growth and changes in
technology?

-   Jazz is an initiative to transform software and systems delivery by
    making it more collaborative, productive and transparent, through
    integration of information and tasks across the phases of the
    lifecycle. The Jazz initiative consists of three elements: Platform,
    Products and Community. The Jazz platform is designed to support any
    industry participant who wants to improve the software and systems
    lifecycle and break down walls between tools. The platform is built
    on architectural principles that represent a key departure from
    approaches taken in the past. Unlike the way monolithic, closed
    products of the past are integrated, Jazz has an innovative approach
    to integration based on open, flexible services and Internet
    architecture. Jazz products are designed to put the team first.
    Rational is building a set of new Jazz products right here at
    Jazz.net. Other Rational products join the Jazz family through
    client or server integrations using the Jazz Architecture. And as
    part of IBM's "Ready for IBM Rational Software" partner program, IBM
    business partners offer extensions and complementary products that
    extend the value of the Jazz platform.

For more information on our visionary architecture please reference:

-   [About Jazz](https://jazz.net/story/about/)
-   [Jazz
    Foundation](https://jazz.net/wiki/bin/view/Main/JazzFoundation)
-   [Jazz Foundation
    Architecture](https://jazz.net/wiki/bin/view/Main/FoundationArchitecture)

## Customization

Question: Describe some of the typical customization that can be done.

-   Most Jazz implementations will have some level of customization.
    Many implement their own work item types and process flows. Adding
    work item types and customization of work items is relatively
    simple, and can be done using the guidance provided in the [Jazz
    deployment guide](https://jazz.net/library/article/542). For more
    complex customizations of the process and automation, some will
    extend the solution using Eclipse based extensions using the
    techniques found in the [extensions
    workshop](https://jazz.net/library/article/1000).
-   There are also some good blogs and other information both on this
    wiki, and out on [PlanetJazz](https://jazz.net/planet/).

## Release Process

Question: Please describe the release process for upgrades, bug fixes
and minor releases. Include standard deployment methods.

-   We follow a Continuous Delivery process to deliver value to
    end-users in short cycles. Please refer to:
    -   Continuous Delivery: How we plan and execute
        <https://jazz.net/wiki/bin/view/Main/RTCContinuousDeliveryPlanning>
    -   [CLM Maintenance For Continuous Delivery
        ](https://jazz.net/wiki/bin/view/Main/CLMMaintenanceForContinuousDelivery)
    -   [CLM Quarterly Mod Releases Schedule
        ](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.dashboard.viewDashboard&tab=_125)

Question: Does the entire system need to be upgraded for a bug fix
release?

-   No. We provide iFixes (i.e. bug fixes) that can easily be added to
    existing servers and just require a restart of the server. Please
    reference this article for a discussion of our iFix process:
    <https://jazz.net/blog/index.php/2014/08/28/devops-for-clm-maintenance-2/>

Question: At what point is support dropped for previous versions?

-   Historically, we've provided standard (defect and non-defect)
    product technical support for a minimum of three years from the date
    the product release was made generally available by IBM, with the
    option to get support extensions for at least an additional two
    years following a product's end of support (EOS) date for an extra
    charge set by IBM (so-called Standard '3+2' support). Over the past
    few years we have aggressively moved many of the 2000+ products in
    our software portfolio to Enhanced '5+3' Support a minimum of five
    full years of standard support from the date the product release was
    made generally available by IBM, with the option to get support
    extensions for at least an additional three years following a
    product's EOS date for an extra charge set by IBM. See the IBM
    Software Support Lifecycle Policy:
    <http://www-01.ibm.com/software/support/lifecycle/lc-policy.html>

Question: What is your approach to previous version compatibility?

-   We know that you want to exact the maximum value from your
    investment in the software you use to run your business. One of our
    new initiatives will be to support, on a going-forward basis for
    select IBM branded products that have not previously announced an
    EOS date, not only the 'current' version of the product, but also up
    to two previous versions, in an effort to limit disruptive
    technology transitions. In this context, a 'version' is a major
    functional enhancement level. While not every IBM software product
    will be subject to this new initiative, our initial focus is to
    support key products from all of our software brands, and expand the
    number of products over time. This initiative may help customers
    reduce the number of products for which they need to acquire
    extended support. The aim is to give you time to 'catch up' to the
    current version while being covered by support under an attractive
    pricing structure. See the IBM Software Support Lifecycle Policy:
    <http://www-01.ibm.com/software/support/lifecycle/lc-policy.html>

Question: How much time do we have to react when notification is
received that a version is losing support?

-   We'll continue to give customers at least 12 months notice prior to
    an IBM branded product release's EOS date and the availability of
    support extensions for an extra charge set by IBM. To make planning
    easier, we endeavor to coordinate most EOS dates to occur on 30
    April or 30 September. We also plan to make it easier to understand
    the support implications of changes to the portfolio. For example,
    when we combine products into a single offering, we'll work to
    explain how that affects the support you're counting on for the
    products you have installed. We want you to have time to put plans
    in place to upgrade to new versions or decide to purchase a support
    extension. See:
-   IBM Software Support Lifecycle Policy
    <http://www-01.ibm.com/software/support/lifecycle/lc-policy.html>
-   IBM Software End of Support
    <http://www-01.ibm.com/software/passportadvantage/endofsupport_ov.html>

Question: What is the frequency of product releases? Please comment on
major, minor, and bug fix releases.

-   We follow a Continuous Delivery process to deliver value to
    end-users in short cycles.

Please refer to:

-   Continuous Delivery: How we plan and execute
    <https://jazz.net/wiki/bin/view/Main/RTCContinuousDeliveryPlanning>
-   CLM Maintenance For Continuous Delivery
    <https://jazz.net/wiki/bin/view/Main/CLMMaintenanceForContinuousDelivery>
-   [CLM Quarterly Mod Releases Schedule
    ](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.dashboard.viewDashboard&tab=_125)

## Security

Question: Describe the location, encryption (as applicable) and contents
of any configuration files. Who has access to these files and are access
attempts logged? If encryption is used, describe the key storage
mechanism and key management process.

-   Application configuration files are located in the /server/conf
    folder and its sub folders. Files are not encrypted. See [CLM
    Backup](https://jazz.net/wiki/bin/view/Deployment/BackupCLM#Backing_up_the_Jazz_application)
    article for more information. The files must be accessible
    (read/write) to the user running the application server and backup.
    Protection and logging should be done using the Operating system
    mechanisms. The files are usually modified by the administration UI
    of the application and during setup. Only users with JazzAdmin
    repository role can modify the properties through the Admin UI.

Question: Describe the controls that are in place to ensure that data is
only accessible on a need-to-know basis and that a client/end-user can
access only the data to which they are authorized.

-   The Jazz solution provides the following controls: (1) Login. Only
    users with a user ID and password are able to access data., (2)
    Configuration of the Read Access permissions. It is possible to
    limit read access to a project area to a list of users e.g. members
    of that project area., (3) Visibility constraints e.g. on SCM
    objects such as streams and components that can be limited to a
    small number of users that are more fine grained than on the project
    level.
-   In general, the Jazz solution provides for increased productivity
    and is designed to support collaboration. It provides read access to
    all data that is not restricted using read access restriction or
    visibility.

Question: What session management methodology is used (e.g.
non-persistent cookies, session tokens stored in the database, by URL)?

-   The Jazz solution uses cookies to store the information of the
    logged-in user in the Web UI.

Question: How the session token is constructed (i.e. data elements)?
What steps have been taken to ensure that it is effectively
non-forgeable? If encryption is used, provide algorithm and key length.

-   A cookie is stored locally. The interfaces are REST based and
    therefore don't need session management, only the login needs to be
    tracked. No data is available for this as this is internal
    information. Different UI elements might store some data locally
    temporarily in the browser. This is information not exposed by the
    Jazz solution and it is really meant to be transparent to users.

Question: Describe controls on repeated attempts to log on including
account lockout (including duration of lockout) and logging/alerting?

Question: What audit trails does the system generate? Describe what
events and data is logged for application and system access and updates.
Describe storage location, length of storage, and security controls for
audit trail logs in online and offline storage. Does the application
allow for verbose logging which may result in sensitive data in the log
files? What mechanism is used for enabling logging? Describe any
separation of audit functionality from debug/trace logging if it exists.

Question: Describe controls in place to protect production systems and
data from unauthorized access within the corporate network.

Question: Does your product support role-based security, or a
combination of role and data based security?

-   The CLM applications define access levels, known as security roles,
    which determine whether a user is allowed to read, write, or
    administer various resources. When using Java EE container
    authentication (or Kerberos), the web container is responsible for
    mapping a user's group memberships to security roles. When using
    Jazz Security Architecture SSO, the applications themselves are
    responsible for performing the group-to-role mapping. During the
    processing of a request that has been authenticated with some user
    identity and security roles, the Jazz application servicing the
    request enforces any security role requirements.

Jazz applications use the following pre-defined security roles: \|
**Role Name** \| **Description** \| \| JazzAdmins \| Administrators of a
Jazz application with full read-write access \| \| JazzProjectAdmins \|
Administrators of a Jazz application with specific permissions to
control the creation and maintenance of Jazz Projects \| \| JazzUsers \|
Users with regular read-write access to the Jazz application \| \|
JazzGuests \| Users with read-only access to the Jazz application. \| \|
JazzDebug \| Users who are allowed to access the Jazz Repository Debug
service. \|

The roles are declared in application deployment descriptors for
applications that can be configured for container authentication
(described later). These roles map to group membership within the
authentication realm (i.e. LDAP) configured in the container. For
additional information please reference:
<https://jazz.net/library/article/75>

## Operation

Question: Are there any specific browser version or browser setting
requirements? Does the system utilize JavaScript if a customers browser
supports it? Does the system degrade gracefully to pure HTML if the
customers browser doesnt support it (or the customer has disabled it)?

Question: Is buffer overrun checking performed? Are other verification
performed on input data?

Question: How is the initial logon to the database or other backend
system performed? If an application-level authentication is used,
describe where and how the UserID and password is stored for the
application or what other authentication method is used.

Question:

##### Related topics: None [related-topics-none]

##### External links: [external-links]

-   None

##### Additional contributors: Main.RosaNaranjo [additional-contributors-main.rosanaranjo]
