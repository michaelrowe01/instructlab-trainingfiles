META:TOPICINFO{author="michaelrowe" date="1700076150" format="1.1"
version="1.9"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Planning your URIs [planning-your-uris]

DKGRAY Authors: Main.MichaelRowe Build basis: IBM Engineering Lifecycle
Management (ELM) ENDCOLOR

TOC{title="Page contents"}

Uniform Resource Identifiers (URIs) have an important role in Jazz
architecture. When you plan your deployment and installation of the IBM
Engineering Lifecycle Management (ELM) you must decide which URI to use
for the server.

## Overview

ELM applications and the Jazz Team Server generate absolute URIs to
resources that are used for the following purposes: stored artifacts,
mail notifications, feeds, copying items to the system clipboard, web
access, and for stable resource identification for all applications.
These URIs are rooted by a "Public URI" that is declared for the
application or Jazz Team Server.

In many instances, these generated URIs persist in the repository
databases because various stored resources contain URI links between
them and outbound links to resources on other applications and servers.
These URIs might also be referred to in contexts that are outside of the
local network. For example, a URI might be referred to from another
Internet domain or outside a corporate firewall.

You must choose a public URI that is fully qualified and accessible from
anywhere in the network where users need to connect. If necessary, a URI
that is based on a stable host name can be rerouted through a domain
name server (DNS).

**Note:** In a limited number of scenarios, you can change the server
URL later by using the server rename feature. For details, see [Changing
the public URL by using server
rename](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=rename-planning-server).
However, using server rename is a potentially disruptive procedure.
Correcting the stored links into the server from all other applications
and systems can be difficult or impossible. Also, server rename might
not be supported in your deployment, depending on the types of
integrations with other products being used. Therefore, be sure to plan
your deployment carefully so that a rename is not needed.

## Options for choosing a URI

The public URI must be configured while Jazz Team Server and the
applications are set up. The public URI can be set, validated, and
tested in the Jazz Team Server setup wizard.

When you choose a public URI, you make the following decisions:

-   Choose your protocol (HTTP or HTTPS): By default, Jazz Team Server
    and the applications require HTTPS for all protected resources. Use
    HTTPS for secure communications within your network.
-   Determine your host name: Choose a host name that is unlikely to
    change and that can be resolved through a DNS within your network.
    This choice gives you the option to move the server to a computer
    with a different IP address and maintain a stable URI. Ensure that
    the host name is fully qualified. If you are deploying all of the
    applications in one application server, you can use virtual host
    names to make the applications more portable while keeping a stable
    URI. For more information, see [DNS names in
    topologies](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=topology-dns-names-in-topologies).
-   Avoid using host names that cannot be resolved with a DNS: Avoid
    host names such as "localhost" or an IP address.
-   Determine the server port: By default, Jazz Team Server and the
    applications use the default port 9443 for HTTPS communications. If
    you prefer to use a different port, plan to do so early. For more
    information, see [Changing the port numbers for the application
    server](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=server-changing-port-numbers-application).
-   Decide whether to use the default HTTPS or HTTP ports: In this
    example, the port is not included in the public URI. For example:
    https://my.host.example.org/jts. This selection is common when you
    are using a reverse proxy to have a single host name for all
    applications that are deployed to separate physical computers. For
    more information, see [Reverse proxy servers in
    topologies](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=topology-reverse-proxy-servers-in-topologies)
    and [Changing the port numbers for the application
    server](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=server-changing-port-numbers-application).
-   Determine the context root: The context root is determined when web
    applications are deployed on the application server. The context
    root is the first segment after the host and port segment of the
    URI. A context root can have only a single segment. For example, in
    the URI https://u1.example.com:9443/ccm, the context root is "ccm".
    By default, the context roots for the CLM applications and Jazz Team
    Server are as follows for new installations:
    -   Change and Configuration Management (CCM): ccm
    -   Quality Management (QM): qm
    -   Requirements Management (RM): rm
    -   Jazz Team Server: jts
-   If you are upgrading from previous versions of IBM Rational Team
    Concert, IBM Rational Quality Manager, and IBM Rational Requirements
    Composer, the old context roots are used to preserve URI stability.
    If you are deploying up multiple instances of the CCM, QM, and RM
    applications to one logical host, choose context roots that have
    meaning within your organization. **Important:** The context root
    for the public URI must be the same as the context root for
    installing the application and deploying the application to its
    application server, even when a reverse proxy server is used in the
    topology. To choose a different context root for your installation,
    see [Choosing a different context root than
    default](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=line-choosing-different-context-root-than-default).
-   Use the public URI of the target application or server: When you
    connect applications to each other or to Jazz Team Server, always
    use the public URI of the target application or server.
-   Remember that clients can connect to the CCM application with an
    alias: This ability supports the case where a local caching proxy is
    set up for caching source-control content. For more information, see
    [Using content caching proxies for Jazz Source
    Control](http://jazz.net/library/article/325) on Jazz.net. If you
    connect with an alias, you might be redirected to the public URI
    when you follow URIs that the application provides.

##### Related topics: [You can't change the public URI](YouCantChangeThePublicURI), [Maintaining the public URL](MaintainingThePublicURL) [related-topics-you-cant-change-the-public-uri-maintaining-the-public-url]

##### External links: \* [Engineering Lifecycle Management Information Center](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management) [external-links-engineering-lifecycle-management-information-center]
