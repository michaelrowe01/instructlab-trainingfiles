META:TOPICINFO{author="michaelrowe" date="1695661716" format="1.1"
version="1.20"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Understanding reverse proxy [understanding-reverse-proxy]

DKGRAY Authors: Main.SeanGWilbur Build basis: The Rational solution for
Collaborative Lifecycle Management (CLM) and the Rational solution for
systems and software engineering (SSE) ENDCOLOR

TOC{title="Page contents"}

This topic outlines the rationale for configuring a reverse proxy, and
how this is used to support a consistent Public URL in a flexible
deployment topology. Follow-on articles in this series will provide
detailed deployment guidance for setting up reverse proxying.

## Other topics in this series

-   [Install Proxy Servers](InstallProxyServers)
-   [Configure a Reverse Proxy Server with WebSphere
    plugins](CreatingAProxyServerWithWebSpherePlugins)
-   [Configuring Enterprise CLM Reverse Proxies: WebSphere 8 and IHS
    8](ConfigureCLMEnterpriseReverseProxy)
-   [Configuring Enterprise CLM Reverse Proxies: Apache and
    mod_proxy](ConfigureCLMEnterpriseReverseProxyWithApache)
-   [Configuring Enterprise CLM Reverse Proxies: WebSphere 8.5 ND
    Proxy](ConfiguringEnterpriseCLMReverseProxiesWebSphere85NDProxy)

## Why use a reverse proxy?

One crucial piece to a successful deployment of the reverse proxy
configuration is understanding what you are going to accomplish and what
problems this will not solve for you. First and formost, the benefit of
using a reverse proxy is the ability to mask the complexity of the
underlying deployment from your end users.

Figure 1: Fully distributed CLM enterprise topology example

In order to fully distribute your deployment, complexity has been added
in that a user of the Rational solution for CLM must connect to 4+
different servers, as well as manage the different ports and context
roots involved. The benefit here is the simplicity of the deployment. A
fully distributed topology is allowed for, the deployment details are
transparent to the user, and there is a minimum amount of complexity in
how to connect the applications together. The big downside is that the
implementation details have become part of the deployment; this may
include ports and machine names that are not standard and with the
underlying requirement to never change the Public URL2 this can make
infrastructure level changes difficult tasks.

One alternative approach is to use a reverse proxy server to "listen" on
your public URL and allow for the underlying deployment to vary. This is
a common technique for hosting applications for security and load
balancing reasons and a standard feature of the IBM WebSphere and HTTP
Server plugin architecture that will be discussed a bit further on in
the article.

Figure 2: Using a reverse proxy in your topology

Now this approach gives the deployment more flexibility at the added
complexity of managing an additional system to host the reverse proxy
itself. The added complexity is has been the main stumbling point for
many people who have avoided this type of deployment. This series of
articles are intended to provide some additional to help overcome the
initial hurdles to a successful reverse proxy deployment.

## What a reverse proxy will and will not do

A reverse proxy here can help introduce a layer of abstraction between
the public URL and the underlying deployment, but this is not going to
solve any problems that require actually changing the public URL the
same requirements apply as covered in [You can't change the public
URL](https://jazz.net/wiki/bin/view/Deployment/YouCantChangeThePublicURI).
Below are a few common variations of the same questions:

RED **NO** ENDCOLOR - Change the server name, port, context root, or
protocol of the public URL. While it is possible for the server to
respond to different URLs, the application content and logic depend on
the public URL. It is possible to test the server and access the system
via the direct machine name or IP address in the browser address, but
the application navigation and content will contain the public URL.

GREEN **YES** ENDCOLOR - Allow for the current public URL or URLs to be
hosted while the underlying deployed server topology is changed. By
hosting the public URL via a web or proxy, the underlying deployment is
free to change while the external URL remains fixed.

GREEN **YES** ENDCOLOR - Consolidate multiple public URLs to be served
from a single location. This does not change the public URL, but
potentially provides the opportunity to unify your deployment and share
resources (the same physical machine, a web server, or transparent
caching server).

RED **NO** ENDCOLOR - Use existing web, proxy, and other network
infrastructure to rewrite URLs directly inside of content and header
responses. While there are various technologies that can handle this
functionality for you, this is unsupported with Jazz and may cause data
integrity issues for consumers and if invalid URL references are written
back to the Jazz system without the valid public URL.

GREEN **YES** ENDCOLOR - Use existing web, proxy, and other network
infrastructure to listen on various URLs to help direct users to the
correct system via forwarding. It is possible to listen on other URLs
that your users may request and forward the requests to the public URL.
For instance, a CCM server with a public URL of
https://clm.example.org:9443/ccm might have a fronting web/proxy to
listen on variation URLs such as https://clm.example.org/ccm to forward
traffic to the correct port of the public URL, simplifying the user
experience but not changing the public URL.

##### Related topics: [Deployment planning: Where to start?](DeploymentPlanning), [Maintaining the public URL](MaintainingThePublicURL), [Proxy server installation](InstallProxyServers), [Configuring Enterprise CLM Reverse Proxies: WebSphere 8 and IHS 8](ConfigureCLMEnterpriseReverseProxy), [Configuring Enterprise CLM Reverse Proxies: Apache and mod_proxy](ConfigureCLMEnterpriseReverseProxyWithApache), [Configuring Enterprise CLM Reverse Proxies: WebSphere 8.5 ND Proxy](ConfiguringEnterpriseCLMReverseProxiesWebSphere85NDProxy) [related-topics-deployment-planning-where-to-start-maintaining-the-public-url-proxy-server-installation-configuring-enterprise-clm-reverse-proxies-websphere-8-and-ihs-8-configuring-enterprise-clm-reverse-proxies-apache-and-mod_proxy-configuring-enterprise-clm-reverse-proxies-websphere-8.5-nd-proxy]

##### External links: [external-links]

-   [Rational solution for Collaborative Lifecycle Management
    Information Center](https://jazz.net/help-dev/clm/)
-   [Rational solution for systems and software engineering Information
    Center](http://pic.dhe.ibm.com/infocenter/rssehelp/v1r0m0/index.jsp)
-   [WebSphere Application Server 7 Information
    Center](http://pic.dhe.ibm.com/infocenter/wasinfo/v7r0/index.jsp)
-   [WebSphere Application Server 8.0 Information
    Center](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/index.jsp)
-   [WebSphere Application Server 8.5 Information
    Center](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r5/index.jsp)

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="topology_dist_clm_ent.gif"
attachment="topology_dist_clm_ent.gif" attr="h" comment=""
date="1367371396" path="topology_dist_clm_ent.gif" size="40548"
user="sbeard" version="1"}
META:FILEATTACHMENT{name="topology_RTC_proxy.png"
attachment="topology_RTC_proxy.png" attr="h" comment=""
date="1367371418" path="topology_RTC_proxy.png" size="77730"
user="sbeard" version="1"} META:TOPICMOVED{by="sbeard" date="1367370897"
from="Deployment.IncludeAReverseProxy"
to="Deployment.UnderstandingReverseProxy"}
