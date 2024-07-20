META:TOPICINFO{author="shubjit" date="1705414895" format="1.1"
version="1.22"} META:TOPICPARENT{name="InstallProxyServers"}

# Reverse Proxies and Load Balancers in an IBM Engineering Lifecycle Management (ELM) Deployment DKGRAY Authors: Main.ShubjitNaik, Main.DineshKumar, Main.JimRuehlin Build basis: CLM 6.0.6, 6.0.6.1, ELM 7.x [reverse-proxies-and-load-balancers-in-an-ibm-engineering-lifecycle-management-elm-deployment-dkgray-authors-main.shubjitnaik-main.dineshkumar-main.jimruehlin-build-basis-clm-6.0.6-6.0.6.1-elm-7.x]

ENDCOLOR

TOC{title="Page contents"}

This article focuses on the benefits and limitations of different
Reverse Proxy and Load Balancer Servers used in standard deployment
topologies of IBM Engineering Lifecycle Management and Continuous
Engineering Solutions.

## DNS Aliasing

URIs have an important role in Jazz architecture. When you plan your
deployment and installation of the Rational solution for Engineering
Lifecycle Management (ELM), you must decide which URI to use for the
server. This is referred to as the Public URI.

The standard deployment of ELM Solution has multiple application servers
and in most production deployments each application runs on its own
application server/host.

You can configure your deployment using DNS aliasing, however, this will
result in separate DNS names for each application, example
jts.example.com, ccm.example.com, etc. This could be an administrative
overhead on a production deployment when they are to be scaled, migrated
or replicated. From an end-user perspective, they will have to remember
multiple URIs. Securing such a deployment will incur additional cost as
each DNS Name would require distinct SSL Certificates (CA). For more
information visit [this
link](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.install.doc/topics/c_virtual_host.html).

The recommended approach is to deploy a **Reverse proxy**. This way you
can refactor the physical topology and still maintain the URIs. You can
maintain a common source URL, for example, clm.example.com and reach
each application via its context root, example /ccm, /rm, etc. This will
give much more flexibility during scenarios of scaling and migrations.
With a reverse proxy in place, securing the deployment will be simpler
with one SSL Certificate (CA) for the reverse proxy.

## Reverse Proxy Server

A Reverse Proxy is a gateway for servers and enables one web server to
provide content from other servers transparently. It can redirect the
traffic to specific applications based on the configuration related to
the context root in the URL. Example /ccm, /rm etc. For a distributed
deployment, where each application from the stack within the ELM/CLM
deployment is deployed on its own server, to maintain a single Public
URL and hide the underlying deployment you should use a Reverse Proxy
Server.

For more Information visit [Understanding Reverse
Proxy](https://jazz.net/wiki/bin/view/Deployment/UnderstandingReverseProxy)
and [Reverse Proxy in
Topologies](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=topology-reverse-proxy-servers-in-topologies)

The only supported and tested Reverse Proxy Server for ELM/CLM
deployments is:

-   [IBM HTTP
    SERVER](https://www.ibm.com/support/knowledgecenter/en/SSEQTJ/mapfiles/product_welcome_ihs.html)

However, we have customers who have worked with other Reverse Proxy
Servers for ELM/CLM deployments and we have listed them below:

-   [Apache HTTP Server](https://httpd.apache.org/)
-   [F5](https://www.f5.com/)

## Load Balancer Server

A Web server that takes care of redirecting and balancing incoming
traffic, based on configured algorithms, between different nodes in a
clustered setup. A load balancer is a requirement for a clustered setup:
multiple instances of the same application are running connecting to the
same database. As of the publication date, EWM is the only application
that can be set up in clustered mode. The supported and tested Load
Balancers with Engineering Workflow Management (EWM) and Engineering
Test Management (ETM) Clustered Setup are:

-   [IBM HTTP
    Server](https://www.ibm.com/support/knowledgecenter/en/SSEQTJ/mapfiles/product_welcome_ihs.html)
-   [HAProxy](http://www.haproxy.org/)

In general, if the software is included or bundled with our IBM
offerings, IBM does testing to ensure the Third Party products will work
with IBM programs and function appropriately. Based on this, IBM
Software support will diagnose problems concerning customer problems
utilizing the knowledge of how our IBM offerings work with the
Third-Party software. Once we have concluded that the IBM program is
working correctly, but the issue still exists, IBM must refer you, the
customer, to the Third Party vendor for further diagnosis. For
open-source software, including HAProxy, the following IBM Policy
applies:

[IBM Open Source and Third-party software
policy](https://www.ibm.com/support/pages/node/737271)

While HAProxy is not included or bundled with the ELM offerings, IBM
does testing to ensure HAProxy will work with the ELM applications and
function appropriately. Based on this, IBM Software support will
diagnose problems concerning customer problems utilizing the knowledge
of how our IBM offerings work with HAProxy--including cases in which
custom load rules [load balancing
algorithm](http://cbonte.github.io/haproxy-dconv/1.9/configuration.html#4-balance)
have been defined. Once we have concluded that the IBM program is
working correctly, but the issue still exists, IBM must refer you, the
customer, to the HAProxy community for further diagnosis."

IBM Support does not provide advice related to defining, testing, or
optimizing custom load rules. IBM or business partner services could
assist you with these matters.

The following tables list the key differences between IHS and HAProxy

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

|  |  |  |
|----|----|----|
|  | IBM HTTP SERVER | HAPROXY |
|  |  |  |
| Support | IBM Support | Forum Support (Community Edition), [IBM Support Policy on Third-party and Open Source software](https://www.ibm.com/support/pages/node/737271)IBM has documented instructions on installation and configuration of HAProxy in the context of deploying a Clustered Setup of EWM and ETM |
| Operating Systems | Can be installed on Windows, Linux and AIX Platforms | Can be installed on Linux platforms only |
| CLM Versions | Supported as a Load Balancer from ELM/CLM version 6.0.5 onwards | Supported as a Load Balancer from ELM/CLM 6.0.4 onwards |
| Config Instructions | [Configure IHS for Load Balancing](https://jazz.net/wiki/bin/view/Deployment/ChangeAndConfigurationManagementClusteredEnvironmentVersion605#Configure_IHS_for_load_balancing) | [Configure HAProxy for Load Balancing](https://jazz.net/wiki/bin/view/Deployment/ChangeAndConfigurationManagementClusteredEnvironmentVersion605#Configure_HAProxy_server_as_load) |
| Load Balancing | The following Load Balancing Policies are supported by IHS, the default load balancing type is Round Robin. Round Robin The Round Robin implementation has a random starting point. The first application server is picked randomly. Round Robin is then used to pick application servers from that point forward. This implementation ensures that in multiple process-based web servers, all of the processes do not start by sending the first request to the same Application Server.Random The Random implementation also has a random starting point. However, with this implementation all subsequent servers are also randomly selected. Therefore, the same server might get selected repeatedly while other servers remain idle. | HAProxy supports a rich set of [Load Balancing algorithms](http://cbonte.github.io/haproxy-dconv/1.9/configuration.html#4.2-balance) and the default is Leastconn. Following are a few examples: Round Robin Each server is used in turns, according to their weights. This algorithm is dynamic, which means that server weights may be adjusted on the fly for slow starts for instance. Note that in some large farms, when a server goes up after having been down for a very short time, it may sometimes take a few hundred requests for it to be re-integrated into the farm and start receiving traffic. This is normal, though very rare. It is indicated here in case you would have the chance to observe it so that you don't worry. Static Round Robin Each server is used in turns, according to their weights. This algorithm is similar to round-robin except that it is static, which means that changing a server's weight on the fly will have no effect. On the other hand, when a server goes up, it is always immediately reintroduced into the farm, once the full map is recomputed. It also uses slightly less CPU to run (around -1). Leastconn The server with the lowest number of connections receives the connection. Round-robin is performed within groups of servers of the same load to ensure that all servers will be used. This algorithm is dynamic, which means that server weights may be adjusted on the fly for slow starts for instance. Source The source IP address is hashed and divided by the total weight of the running servers to designate which server will receive the request. This ensures that the same client IP address will always reach the same server as long as no server goes down or up. This algorithm is static by default, which means that changing a server's weight on the fly will have no effect, but this can be changed using "hash-type". |
| Monitoring | External Tools can be used | Statistics Reports is Bundled with HAProxy UI. External Tools can be used as well |
| As a Reverse Proxy | Supported and Tested - The major advantage of using IBM HTTP Server is that a single server can be used as a Reverse Proxy and as the Load Balancer | Not Tested or Supported as a Reverse Proxy - HAProxy is tested as a Load Balancer ONLY for EWM and ETM clustered setup in combination with IBM HTTP Server as a Reverse proxy |

-   HAProxy's additional options for load balancing makes it an
    attractive option for deployments in which the admin team value this
    flexibility and can accept the cost of another proxy specifically
    for load balancing.

##### Related topics: [Deployment web home](DeploymentWebHome), [Installing Proxy Servers](https://jazz.net/wiki/bin/view/Deployment/InstallProxyServers) [related-topics-deployment-web-home-installing-proxy-servers]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.PaulEllis, Main.DanielMoul [additional-contributors-main.paulellis-main.danielmoul]
