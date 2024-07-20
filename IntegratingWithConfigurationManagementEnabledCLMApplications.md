META:TOPICINFO{author="fryerk" date="1561420209" format="1.1"
version="1.8"} META:TOPICPARENT{name="DeploymentIntegrating"}

# Enabling your application to integrate with configuration-management-enabled CLM applications DKGRAY Authors: Main.KathrynFryer [enabling-your-application-to-integrate-with-configuration-management-enabled-clm-applications-dkgray-authors-main.kathrynfryer]

Build basis: Rational solution for Collaborative Lifecycle Management
(CLM) 6.x ENDCOLOR

TOC{title="Page contents"}

In version 6, Rational Collaborative Lifecycle Management (CLM)
introduced new configuration management capabilities in the
requirements, test, and design domains. These capabilities represent the
first implementation of the [OASIS OSLC Configuration Management
specification](http://open-services.net/specifications/configuration-management/)
(in draft as of December 2015), and include support for versioned
artifacts, streams and baselines, and global configurations for
lifecycle data.

Many third-party applications, including in-house client applications,
have developed integrations with the CLM products, often by using OSLC
linking. Because of the changes associated with configuration
management, described in this article, many of these integrations will
not work correctly in an environment that uses configurations until the
3rd-party application implements a basic level of support for
configuration management.

This document describes different integration scenarios and what an
application must implement to realize them. It is intended for the
application owners and developers of those 3rd-party applications. It
assumes:

-   You are already familiar with the CLM configuration management
    capabilities (see this article for more details), with a basic
    understanding of streams, versioned artifacts, and one-way
    directional linking.
-   Your third-party application already complies with the OSLC Core 2.0
    specification.
-   Your third-party application already supports a way to define
    friendships and project associations with the CLM application you
    integrate with. (If you are writing a new application, refer to the
    relevant OSLC specifications and CLM Knowledge Center to learn about
    defining server and project associations.)

Important references include:

-   [OASIS OSLC Configuration
    Management](http://open-services.net/specifications/configuration-management/)
    specification (draft as of December 2015)
-   [OSLC Tracked Resource
    Set](http://open-services.net/wiki/core/TrackedResourceSet-2.0/)
    specification
-   [OSLC Indexable Linked Data
    Provider](http://open-services.net/wiki/core/IndexableLinkedDataProvider-2.0/)
    specification
-   [Linked Data Platform 1.0](http://www.w3.org/TR/ldp/) specification
-   [Backlink index
    reference](https://jazz.net/wiki/bin/view/Main/BacklinkIndex) on
    jazz.net

## Impacts of configuration management

Configuration management changes how artifacts are managed, used, and
referenced in CLM:

-   How artifacts are stored: They are versioned, and associated with a
    configuration (stream or baseline).
-   How artifacts are referenced or requested: Their URIs are resolved
    using a specific configuration context.
-   How cross-application links are managed: Links are directional. The
    "owning" or source application stores the link details with the
    artifact and publishes to the Link Index Provider; the target
    application does not store the link details with the artifact, but
    queries the incoming links (or "back links") from the link index
    when needed. By comparison, in non-configuration-enabled
    environments, applications create and store physical back links with
    the artifact; any existing back links are removed when a project
    area is enabled for configuration management. For a list of links
    and owning/target applications (which correspond to OSLC domains),
    see the following table; you can use the list to determine which
    links your application would own. (Link types that are constrained
    to artifacts within an application, such as those between
    requirements in an RM project, might or might not be managed using
    the link index.)
-   How OSLC links are resolved: They resolve first within the context
    of a defined configuration, and then across providers through a
    global configuration that contains configurations from more than one
    application.

**Table 1. Link types and their owning domain/application.** In
alphabetical order by owning domain, target domain, and link
relationship. \#LinkTable

If your application already integrates with the CLM applications, those
integrations may not work correctly in a configuration-aware
environment. For example, if your non-configuration-enabled application
has existing links to artifacts that have been versioned (in an existing
CLM project area that enabled configuration management), those links
will always resolve to the artifact in the initial or default stream;
over time, as new branches of the stream are created, you cannot assume
the default stream contains the correct artifact version. You cannot
create new links from a CLM versioned artifact to artifacts in a
non-configuration-enabled application. If your application owns the
links, the CLM artifact will no longer show the incoming link.

To ensure your application's integrations to CLM continue to work in a
configuration-aware environment, you must implement an appropriate level
of support for configuration management. This document describes
multiple integration scenarios and what an application must implement to
realize them.

**Note:** The CLM applications provide various examples of how to
support configuration management. Rational DOORS Next Generation (DNG),
Rational Design Manager (RDM), and Rational Quality Manager (RQM)
include versioned artifacts and configurations; RDM is considered
"compatible" and allows some linking to non-versioned artifacts. The RTC
SCM component provides advanced change and configuration management
support for source code artifacts; these artifacts are not defined by an
OSLC domain and don't use OSLC to create links, but can contribute
baselines, snapshots, and streams to global configurations. The Rational
Team Concert (RTC) or CCM work item system does not provide
configurations or versioned artifacts, but supports linking to versioned
artifacts and setting configuration context. (Technically, the work item
system is provided by the CCM application within CLM, which is available
based on licensing, but we will refer to it as RTC for simplicity.)

## If you do nothing to your application

In general, **linking between artifacts in configuration-enabled
containers (project areas) and non-configuration-aware containers is not
supported, and does not work in a way that is useful**. If you do
nothing to your application, your integration use cases will not work as
expected with configuration-enabled CLM projects, with a few exceptions:

1.  **If you link or synchronize only with RTC plans or work items**,
    and those work items don't link to versioned artifacts in DNG, RQM,
    or RDM (or such links are ignored or deleted in the 3rd-party
    application), the integration should continue to work without
    changes to your application. RTC does not version work item or plan
    artifacts.
2.  **If you copy a static URL to link to requirement or test
    artifacts**, the URL will include the configuration context and will
    resolve correctly to display the CLM artifact in the correct
    context.
    -   Copying the artifact URL from a link attribute value
        (right-clicking the artifact identified in an existing OSLC link
        and selecting Copy Link Location) yields a URL you can use in a
        REST command or to display the artifact in a browser.
    -   Copying the URL from the browser address field gives you a
        different syntax; you would need to derive the correct URL to
        use it to access the artifact programmatically.
3.  **If you enable execution of RQM tests in a separate application,
    and you used the recommended APIs** from IBM to accept URLs from RQM
    for the test to run and the target location for test results, the
    integration should continue to work. RQM provides URLs with the
    correct version and configuration information, and the third-party
    application can treat them like any other URL. Contact your IBM
    representative for updated CLM v6 information to validate your
    implementation. If you do NOT use the APIs, you should modify your
    adapter to use the APIs, which are available under special agreement
    from IBM; contact your IBM Business Development or client rep.
4.  **If you use the Rational Design Manager SDK to publish model
    content as RDM resources, and followed the steps defined on
    [Jazz.net](https://jazz.net/wiki/bin/view/Main/Dm5Sdk_ExternalFileExample)**,
    you have already implemented a mechanism to request and select
    target RDM configurations (or to use the default) for publishing.
    This mechanism will continue to work in v6, although you should test
    and validate the integration. However, you cannot yet specify a
    global configuration, only a local RDM configuration - meaning that
    if you work in a global configuration context, you'll need to know
    which local RDM configuration contributes to that global
    configuration.
5.  **If you link to design artifacts in RDM, and expect those links to
    always resolve to the default configuration** (as specified in RDM),
    your integration should continue to work. You can create links
    between RDM and third-party applications that do not support
    configurations, but those links always resolve to the default
    configuration set in RDM. DNG and RQM configuration-enabled projects
    will not allow users to create new links to or from applications
    that do not support configurations.

If these exceptions do not apply to your application, you likely need to
take some action to ensure your integrations work correctly with
configuration-enabled projects.

## How to enable your application

What you must do to enable your application for configuration management
depends on the usage scenarios you want to support. In the next
sections, we explore the following scenarios, which build upon each
other:

[Scenario1](#ScenarioOne). Enable users to set a global configuration context to use with your application.
:   Your application doesn't need to have versioned artifacts or
    configurations. This support is required for all the following
    scenarios; in and of itself, it does not provide much practical
    functionality.

<!-- -->

[Scenario 2](#ScenarioTwo). Enable users to create OSLC links between artifacts in your application and versioned artifacts in DNG, RQM, or RDM
:   \- for example, to indicate that a test case in your application
    validates a requirement in DNG, or a task or work item implements a
    requirement in DNG. Your application doesn't need to have versioned
    artifacts or configurations.

<!-- -->

[Scenario 3](#ScenarioThree). Enable users to define configurations (streams and baselines), and potentially to version artifacts, in your own application.
:   The OASIS OSLC Configuration Management specification describes how
    to implement configurations and artifact versioning. Note that the
    specification does not mandate versioning of artifacts, and suggests
    that ChangeRequests in particular should not be versioned.

<!-- -->

[Scenario 4](#ScenarioFour). Enable users to contribute configurations from your application to global configurations,
:   to group a particular set or configuration of artifacts with
    artifacts from the CLM application(s). Your application must provide
    configurations as described in the scenario above.

<!-- -->

[Scenario 5](#ScenarioFive). Enable users to report on data from your application along with the CLM application data
:   using the Jazz Reporting Service Report Builder or Rational
    Engineering Lifecycle Manager (RELM, which requires additional
    licenses to CLM). Reporting doesn't require versioned artifacts or
    configurations, but does behave differently if your artifacts are
    not versioned.

Before implementing any of these scenarios, your application
administrator must take steps to enable your application and its users
to access the Global Configuration Management (GCM) server:

1.  **Your application administrator must set up a friend relationship**
    between your application and the global configuration provider (the
    CLM Global Configuration Management \[GCM\] server), to enable
    communication between them. This step is similar to how you
    establish friendships with the other CLM applications you integrate
    with.
2.  **Your application users need permission to access the GCM
    application** and the appropriate project areas within it. If they
    don't already have access, your GCM or CLM administrator needs to
    add them as users and project area members.

### Service provider properties for CLM integration

The CLM applications also check for certain properties in your service
provider documents when initiating an integration operation, to
determine your application's configuration management support. For
example, when a user tries to create a link from a DNG artifact to
another application, DNG checks the application's
`globalConfigurationAware` setting to ensure compatibility or support
for configurations before opening the artifact picker; the Global
Configuration Management (GCM) application also checks the
`globalConfigurationAware` setting when responding to requests. These
properties are not defined in the OASIS OSLC specification, but are
required to integrate with CLM.

Add the following properties to your application's service provider
documents, using the `http://jazz.net/xmlns/prod/jazz/process/1.0/`
namespace. (The following examples use the prefix `jfs_proc` to
represent that namespace):

-   `globalConfigurationAware`. The CLM applications check this value
    when establishing a connection to your application's provider, such
    as when creating a link or requesting an artifact. If the provider's
    value is `no`, DNG and RQM do not permit the user to create or
    modify a link to the provider; RTC and RDM simply treat the
    application as if it doesn't support configurations. If you don't
    specify this property, the value is assumed to be `no`. Set the
    value to:
    -   `yes` if your application supports configurations and versioned
        artifacts.
    -   `compatible` if your application does not support
        configurations, but it can still link to or interact with
        versioned artifacts (because you have implemented Scenarios 1
        and 2 above).
    -   `no` if you have no support for configurations or versioning.
    -   For example: `yes`

<!-- -->

-   `supportContributionsToLinkIndexProvider`. For links that your
    application "owns", indicate whether you provide a TRS feed that
    populates the Link Index Provider with information for the target
    application (`true`) or not (`false`). For example: `true`
    -   The Link Index Provider (LDX) stores information about the
        links; the target application artifact, which does not store any
        incoming link information, can then query LDX to request
        information about those links in order to display them.
    -   If you do not provide information to the link index, the target
        DNG and RQM artifacts cannot show the incoming link from your
        application artifact. For more details, see [Scenario
        2](#Scenario2) below.
    -   The CLM applications do not check this value today, but assume
        that if a provider has declared support or compatibility for
        configurations (in the `globalConfigurationAware` property), it
        provides information to the Link Index Provider.

<!-- -->

-   `supportLinkDiscoveryViaLinkIndexProvider`. For links that your
    application does not "own", indicate whether your application
    queries the Link Index Provider to get information about incoming
    links from other applications (`true`) or not (`false`). For
    example: `true`
    -   Of the CLM applications, only RTC checks this property. If the
        application supports link discovery, RTC provides link
        information to LDX; otherwise, RTC attempts to create incoming
        links (back links) in the application. The other CLM
        applications do not create incoming links in any application
        when configurations are enabled. Unless your application "owns"
        all link types it uses, when you support linking to versioned
        artifacts, you should adopt the link discovery mechanisms.

\#ScenarioOne

### Scenario 1: Enable users to set a configuration context for your application's artifacts.

With configuration management enabled, artifact references are resolved
in the context of a configuration; cross-project or cross-application
links require a global configuration context. Whether your application
defines its own configurations or not, your users will need to set or
select a configuration context when creating or referencing artifacts
using OSLC links, and your application needs to store that context. This
capability is necessary to support the linking use cases described in
the next scenario.

To ensure that users can select a configuration context:

1.  **Your application users need to be able to select the desired
    global configuration context to use**, from the appropriate GCM
    project area. Your application can locate and use URL for the global
    configuration "picker" or selection dialog box from the GCM
    application's service catalog, using the typical OSLC discovery
    mechanisms. When your application opens the dialog box, the GCM
    application lists the available configurations; the user can then
    select or change the configuration they want from the list.
2.  **Your application needs a way to store the selected configuration
    context for future use** - options include a property of the user's
    session setting (such as a session variable); a user preference; an
    attribute or property of an artifact or project area; potentially
    even as an additional property of a link to the artifact; or some
    combination of these. How you implement depends on your application
    and usage scenarios. The RTC work item system uses a somewhat
    complex combination of mappings and attributes; other implementers
    might use a simpler implementation of a session variable, or a
    user-container attribute. Your application will need to include this
    context when making requests of other configuration-enabled
    applications.
3.  **Your application users need to be able to determine the current
    configuration context.** Your application needs to display or
    communicate the context in some way. The CLM applications use the
    configuration context menu in the main menu bar.
4.  **Optional: Your application might allow an administrator to set a
    default configuration context**, so the user does not need to make
    that decision. If you choose to provide such an option, you'll need
    a mechanism for the administrator to select the configuration from
    the list of global configurations, and store and display it so the
    user knows which configuration they are using. You might also need
    to consider whether and how the user can override that default.

\#ScenarioTwo

### Scenario 2: Enable users to link between your application's artifacts and versioned CLM artifacts.

For configuration-enabled projects, links are directional: there is a
source or owner artifact and application, and a target (see the Link
Table above). As a result, there are multiple steps involved in
establishing links between your applications artifacts and the versioned
artifacts in CLM:

1.  **Enable users to create links from your applications artifacts to
    CLM artifacts** by passing and accepting the configuration context
    in all artifact requests.
2.  **Ensure that users can create links from CLM versioned artifacts to
    your application.**
3.  **Enable users to create, see, and maintain links between your
    applications artifacts and versioned CLM artifacts**, regardless of
    which side initiates the action or owns the links. This step
    requires adopting the Link Index Provider (LDX) so the target
    application artifact can resolve incoming links.

If your application owns all of the links to the CLM application (or
conversely, the CLM application owns all of the links), you could
conceivably implement steps 1 and 2, and adopt LDX in a second phase.
However, until you adopt LDX, the user can only see, modify, or follow
the link from the owner artifact to the target artifact; the target
artifact will not show any indication that the link exists. That level
of implementation might be sufficient for a small set of use cases. In
the long term, you should adopt LDX so the user can see incoming links
as well, and modify and traverse links between artifacts regardless of
which application owns them.

**Notes:**

-   One special case exists: a user creates a link from your application
    to an RTC artifact, where RTC "owns" the link. If your application
    does not use LDX (`supportLinkDiscoveryViaLinkIndexProvider` is
    `false`), RTC tries to create an incoming link in your application.
    None of the other CLM applications create incoming links when
    configuration management is enabled.
-   Because CLM artifacts no longer store incoming links (links they do
    not "own") as properties, when you request the artifact (using REST
    GET, for example), the resource returned does not include those
    incoming link values. If your application requires those properties,
    you need to make a second request to LDX to get them. Also be aware
    that LDX stores the link properties using the forward link property
    (for example, validatesRequirement), which might not be the same
    label your application would use to show the incoming link.

#### a) Enable the user to create links from your application to a versioned CLM artifact (new or existing)

**When the user creates the link:**

1.  If the configuration context is not already set, the user chooses
    the desired configuration context for the CLM artifact from the list
    of global configurations, using the GCM application's delegated
    selection dialog box, as described earlier. Save the selected
    configuration context.
2.  Include the configuration context in the header or URI of the CLM
    request to create the link (and the artifact, if appropriate), as
    described in the "Configuration Context" section of the [OASIS OSLC
    CM
    specification](http://open-services.net/specifications/configuration-management/).
3.  If your application "owns" the link, save the link values with your
    application's artifact. (If your application does not "own" the
    link, you need to adopt LDX so you can display the incoming link.
    See [step c](#StepCee) below.)

**When the user follows or modifies the link from your application to
the CLM artifact**, or when your application shows a preview (rich hover
text) on mouse-over, include the configuration context in the request
header or URI to ensure that you display the correct version of the
artifact, as described in the Configuration Context section of the
[OASIS OSLC CM
specification](http://open-services.net/specifications/configuration-management/).

#### b) Enable the user to create links from the versioned CLM artifact to a (non-versioned) artifact in your application

1.  Ensure that the CLM applications can determine that your application
    supports configuration management: Update your service provider
    document to set the property `globalConfigurationAware` to `yes` (if
    you fully support the configuration management specification, and
    can only integrate with enabled applications or service providers)
    or `compatible` (if your application is configuration-aware, and can
    support integrations with enabled and non-enabled providers). If you
    do not specify the property, or set its value to `no`, the DNG and
    RQM applications will give an error, and will not display your
    delegated artifact selection or creation UI. (RTC and RDM will
    display the delegated UI, but might not pass the configuration
    context.)
2.  Accept and process the configuration context passed with the link
    creation request.
3.  If the user is linking to an existing artifact, filter the available
    artifacts based on the configuration context, where appropriate. (If
    your application implements versioned artifacts, you must use the
    configuration context to filter and set the link to the correct
    artifact version.)
4.  If your application "owns" the link, save the link values with your
    application's artifact.
5.  If the CLM artifact "owns" the link, it will store the link value
    with the CLM artifact, and send information about the target to the
    Link Index Provider (LDX). In that case, your application must adopt
    LDX to display the incoming link to the user (see [step c](#StepCee)
    below).

\#StepCee

#### c) Enable users to see and manage links between artifacts regardless of link ownership

To ensure that users can create, modify, view, and traverse links
between your application and the CLM applications, regardless of link
ownership, you need to adopt the Link Index Provider (LDX). How you
adopt and use LDX differs depending on whether your application "owns"
the link or not. See the [Link Table](#LinkTable) above to determine
link ownership.

-   **For links your application "owns"**, the CLM application does not
    store any physical data with its artifact, but queries the link
    information from LDX. To ensure that the CLM artifact displays the
    incoming link, you need to populate LDX with the link data:
    1.  Create an OSLC TRS feed for the link properties for your
        resources, and define the feed in your application's
        rootservices document. Refer to the [OSLC Tracked Resource
        Set](http://open-services.net/wiki/core/TrackedResourceSet-2.0/)
        and [Indexable Linked Data
        Provider](http://open-services.net/wiki/core/IndexableLinkedDataProvider-2.0/)
        specifications for details on defining and publishing tracked
        resource sets.
    2.  After your application is installed, an administrator must
        manually register the TRS feed as a data source in the LDX
        administrator UI at
        `https://SERVER:PORT/ldx/web/admin/data-sources` (replacing
        `SERVER:PORT` with the server and port values). There might be a
        more automated registration mechanism in a future release.
    3.  Tell the CLM applications that you contribute to LDX by setting
        the `supportContributionsToLinkIndexProvider` property to `yes`
        in your application's service provider documents.
-   **For links that the CLM application "owns"**, the CLM application
    stores the link with its artifact and populates the target
    information to LDX. Although in the past, your application might
    have stored the other end of the link with the artifact, you should
    now query LDX for the link information when required. Otherwise,
    users of the CLM application might delete or modify the link without
    your application being updated, rendering the link data invalid. To
    query LDX for link information:
    1.  Discover the Link Index (ILinkIndexService) API endpoint, which
        is defined as a resource in the LinkProvider property in the CLM
        application's Service Contribution Resource (/scr) document.
    2.  Query LDX for the link information using that Link Index API
        endpoint and the `queryForLinks` API or `query` REST command.
        See the [Backlink Index
        article](https://jazz.net/wiki/bin/view/Main/BacklinkIndex) on
        Jazz.net for details on the API syntax. For example, to get all
        "Implemented By" and "Validated By" links for a DNG resource in
        a specific configuration context:
        `POST https://SERVER:PORT/qm/linkIndex/query Content-Type: text/json Accept: text/json ---Content--- { "targetURLs": [ "https://SERVER:PORT/rm/resources/_q6HmUnl7EeSIQetY5MAdvQ" ], "linkTypes": [ "http://open-services.net/ns/cm#implementsRequirement", "http://open-services.net/ns/qm#validatesRequirement" ], "gcURL": "https://SERVER:PORT/gc/configuration/4" }`
    3.  Tell the CLM applications that you query links from LDX by
        setting the `supportLinkDiscoveryViaLinkIndexProvider` property
        to `yes` in your application's service provider documents.

\#ScenarioThree

### Scenario 3: Enable users to define configurations in your own application.

You might choose to enable users to define different configurations and
potentially versioned artifacts within your own application, to increase
reuse, enable variants and parallel development, and participate more
fully in global configurations. Note that the [OASIS OSLC Configuration
Management
specification](http://open-services.net/specifications/configuration-management/)
does not mandate versioning for all artifact types, and suggests that
ChangeRequests in particular should not be versioned.

-   **You need to support the underlying capabilities and services:**
    1.  Implement support for components and configurations as defined
        in the [OASIS OSLC Configuration
        Management](https://tools.oasis-open.org/version-control/browse/wsvn/oslc-ccm/trunk/specs/config-mgt/config-resources.html) -
        Configuration Resources specification section.
    2.  Produce RDF resources compliant with the [OASIS OSLC
        Configuration Management
        specification](http://open-services.net/specifications/configuration-management/)
        (versioned resources, configurations, streams, and baselines).
        Refer to the spec for details.
    3.  Publish your RDF resources by using an OSLC TRS feed, including
        versioned resources and local configuration resources. Refer to
        the [OSLC Tracked Resource
        Set](http://open-services.net/wiki/core/TrackedResourceSet-2.0/)
        and [Indexable Linked Data
        Provider](http://open-services.net/wiki/core/IndexableLinkedDataProvider-2.0/)
        specifications for details on defining and publishing tracked
        resource sets.
    4.  Tell the CLM applications that you support configurations by
        setting the `globalConfigurationAware` property to `yes` in your
        application's service provider documents.
    5.  When integrating with other application providers, check their
        `globalConfigurationAware` property and take appropriate action
        based on the setting. (Note: "appropriate action" depends on
        whether your application is compatible with both providers that
        support configurations and those that don't; if you can only
        integrate with providers that support configurations, you need
        error handling to alert users that you cannot integrate with
        providers that don't support configurations.)
-   If you want users to be able to choose whether to enable
    configuration management in a particular application instance or
    container, **provide an option or "switch" to enable the support**
    (as DNG and RQM do for each project area).
-   **Enable users to set the local configuration in your application,
    as well as a global configuration context** (as described
    previously). See the Delegated UI section in the [OASIS OSLC
    Configuration Management - Configuration
    Resources](https://tools.oasis-open.org/version-control/browse/wsvn/oslc-ccm/trunk/specs/config-mgt/config-resources.html)
    specification section. Note: If you do not support global
    configuration protocols, your application must set a default
    configuration that will be used to resolve incoming links.
-   **When a user creates, displays, modifies, or deletes an artifact,
    ensure that your application passes the correct configuration
    context** information in the header of the request, as defined by
    the [OASIS OSLC Configuration
    Management](http://open-services.net/specifications/configuration-management/)
    specification.
-   If you want users of other third-party, non-configuration-enabled
    applications to link to your application artifacts, **consider
    explicitly defining a "default configuration"**, as RDM does.
    Otherwise, you can default to the initial configuration, as DNG and
    RQM do.
-   **Support directional linking**, as described in the [previous
    scenario](#ScenarioTwo) on linking:
    1.  Remove or ignore any incoming links (back links) in your
        application (links your application does not "own").
    2.  As described in [scenario 2](#ScenarioTwo), when a user creates
        an OSLC link that your application owns:
        1.  Register your TRS feed (that includes link resources) with
            the Link Index Provider (LDX) - either manually, or using
            the APIs and commands as described above.
        2.  When creating the link, store the link information with the
            artifact in your application; your TRS feed will publish the
            reverse link information to LDX for the CLM applications to
            query.
    3.  When displaying your own artifact (either in your application,
        or in a delegated UI like a rich hover preview), query LDX to
        get link information and display it in your application with any
        links that are physically stored there.
    4.  Tell the CLM applications that you use LDX by setting
        `supportContributionsToLinkIndexProvider` and
        `supportLinkDiscoveryViaLinkIndexProvider` properties to `yes`
        in your application's service provider documents.

**Important:** In most cases, if you are implementing configurations,
you will also want to contribute to global configurations, to enable
cross-application linking within the global context. If you are
implementing in stages and your application does not yet support global
configuration protocols, you must provide a default local configuration
to resolve links from other applications (namely CLM artifacts).

\#ScenarioFour

### Scenario 4: Enable users to add your application's configurations to a global configuration.

This usage scenario assumes that your application can represent
configurations and versioned artifacts, that can be contributed to a
global configuration, as described in [scenario 3](#ScenarioThree)
above, and per the [OASIS OSLC Configuration Management
specification](http://open-services.net/specifications/configuration-management/).

Note: At this time, you cannot contribute aggregate or composite
configurations to the CLM Global Configuration Management (GCM)
application; it expects that "local" configurations do not have any
sub-configurations. This does not apply to SCM configurations, since
references to the artifacts in SCM configurations are never resolved in
a GC context.

To enable a user to contribute your application's configurations to a
global configuration:

1.  **Indicate your configuration is a valid contribution** by giving it
    the `oslc_config:acceptedBy` property set to the value
    `oslc_config:Configuration`.
2.  **Define your available configuration service providers in a
    catalog**, and point to it from your rootservices document, for
    example: ==.
3.  **Allow the user to select from your available configurations** by
    providing a delegated "picker" UI that the GCM application can call
    to display and filter the list of available configurations.
4.  **When the user links to or from your application, use the global
    configuration context** to correctly resolve both incoming and
    outgoing references and resolve to the correct configuration and
    artifact.

\#ScenarioFive

### Scenario 5: Enable users to report on your artifacts with configuration-aware reports

RELM and Jazz Reporting Service and Report Builder can report against
projects with configurations using a special data source, the Lifecycle
Query Engine using Configurations. To include artifacts from your
applications in reports, your application must populate this data
source. (Note that RELM requires an additional license to the CLM
applications.)

To enable users to build and run reports on configurations that include
data from your applications:

1.  Publish your RDF resources using OSLC TRS feeds, as described in
    [Integrating external data sources with LQE and Report
    Builder](https://jazz.net/library/article/91450). Refer to the [OSLC
    Tracked Resource
    Set](http://open-services.net/wiki/core/TrackedResourceSet-2.0/) and
    [Indexable Linked Data
    Provider](http://open-services.net/wiki/core/IndexableLinkedDataProvider-2.0/)
    specifications for additional details on defining and publishing
    tracked resource sets.
2.  Register your TRS feeds with the LQE data source:
    -   If your application can register as a JTS extension (see
        <https://jazz.net/products/DevelopmentItem.jsp?href=content/project/plans/jia-overview/index.html>
        for details), its services can be queried from LQE. A CLM
        administrator can run setup on LQE, and it will find and add
        your application's TRS feeds.
    -   If your application does not register as a JTS extension, or if
        you want, a CLM administrator can manually add the TRS feeds
        from the LQE Data Sources administration page
        (`https://SERVER:PORT/lqe/web/admin/data-sources`), using the
        feed itself or the rootservices URL for your application.

**Notes:**

-   This process is the same for applications that don't support
    configurations but use LQE (without configurations) as a data source
    for reports.)
-   If you contribute non-versioned artifacts (that is, you do not
    support versioning or configurations, but populate LQE), those
    artifacts are considered part of all configurations, even if a user
    created links to or from them in the context of a specific CLM
    configuration. Those artifacts will then appear in reports against
    any configuration.

## Finalizing your implementation

After completing the steps required to support the integration scenarios
for your application, you'll need to validate them and publicize your
new configuration support.

As the CLM implementation of configuration management matures, there
might be other services where your application could participate, such
as the link validity service. Information on those special topics will
be addressed separately, as they are made available for external
consumption.

Please contact your IBM representative if you require assistance, and
also when you have validated support for configuration-enabled projects,
and the version you have tested with. If you have questions, or feedback
or helpful additions to this article, please post a comment here, or on
the [Jazz.net forum](https://jazz.net/forum).

##### Related topics: [related-topics]

-   [Deployment web home](DeploymentWebHome)

##### External links: [external-links]

-   [OASIS OSLC Configuration Management
    specification](http://open-services.net/specifications/configuration-management/)
    (in draft as of December 2015)
-   [OSLC Tracked Resource Set
    specification](http://open-services.net/wiki/core/TrackedResourceSet-2.0/)
-   [OSLC Indexable Linked Data Provider
    specification](http://open-services.net/wiki/core/IndexableLinkedDataProvider-2.0/)
-   [Linked Data Platform 1.0](http://www.w3.org/TR/ldp/)
-   [Backlink index
    article](https://jazz.net/wiki/bin/view/Main/BacklinkIndex) on
    Jazz.net

META:FILEATTACHMENT{name="directional_link_table1.png"
attachment="directional_link_table1.png" attr="" comment="This table
lists the link types and their owning domain/application In alphabetical
order by owning domain, target domain, and link relationship"
date="1450276515" path="directional_link_table1.png" size="60068"
user="fryerk" version="1"}
