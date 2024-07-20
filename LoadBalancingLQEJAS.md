META:TOPICINFO{author="shubjit" date="1686758778" format="1.1"
version="1.6"} META:TOPICPARENT{name="JazzAuthorizationServer"}

# Setup Load Balancing For Multiple LQEs on a JAS Based Deployment DKGRAY Authors: Main.ShubjitNaik, Main.ShradhaSrivastav, Main.MatthieuLeroux Build basis: Engineering Lifecycle Management and Jazz Authorization Server 7.0.2 or higher [setup-load-balancing-for-multiple-lqes-on-a-jas-based-deployment-dkgray-authors-main.shubjitnaik-main.shradhasrivastav-main.matthieuleroux-build-basis-engineering-lifecycle-management-and-jazz-authorization-server-7.0.2-or-higher]

ENDCOLOR

TOC{title="Page contents"}

The following article is an example of how you can configure Multiple
Lifecycle Query Engine (LQE) Nodes, deployed with Jazz Authorization
Server, with Load Balancing for Distributing query workload.

This examples assumes the ELM deployment is on IBM WebSphere Liberty
Profile with Jazz Authorization Server enabled and a Reverse Proxy
Server (IBM HTTP Server).

## High Level Instructions

Pre-Req: LQE deployed on its own IBM Liberty server and is setup with a
distributed deployment of ELM enabled with JAS.

-   Run a backup on the Primary LQE Server
-   Install and configure an additional LQE node
-   Add the new node URIs to JAS LQE registration
-   Test Individual LQE Nodes and change Node Names
-   Setup Apache HTTP Server or HAProxy as Load Balancer for the LQE
    nodes
-   Reconfigure LQE redirection in Reverse Proxy to point to the Load
    Balancer
-   Test Load Balanced LQE setup

## Run a Backup on the Primary LQE Server

You will need a backup from your original LQE server to configure
additional servers. A backup contains all the metadata in LQE and a copy
of the indexed data. You can use the backup files to install another LQE
server that has a copy of the indexed data.

-   To create a One Time Backup see [Backing up and restoring Lifecycle
    Query
    Engine](https://www.ibm.com/docs/en/elm/7.0.2?topic=performance-backing-up-restoring-lqe-ldx)
-   Or if Backups are scheduled, review the backup location
-   Copy over the latest backup to the new server identified for the
    second or additional LQE Node
-   In addition Copy the `lqe.key`, `lqe.node.id` and
    `dbconnection.properties` files from the conf/lqe directory to the
    new server

## Install and Configure additional LQE node

\* Install LQE on a new application server. You do not need to install a
new Jazz Team Server. \* Create a new relational database for the new
LQE server, [Click for
Instructions](https://www.ibm.com/docs/en/elm/7.0.2?topic=management-setting-up-database)
\* Copy the following folders from the LQE backup to the new
installation:

-   Copy the /datasets directory into the conf/lqe directory in the new
    installation.
-   Copy the /metadata directory into the conf/lqe directory in the new
    installation. \* Copy the `lqe.key`, `lqe.node.id` and
    `dbconnection.properties` files from the original server to the
    conf/lqe directory in the new installation \* Edit
    `dbconnection.properties` file in the conf/lqe directory and update
    the **db.location** and **db.password** \* Edit `lqe.properties`
    file in the conf/lqe directory and set the LQE restore property to
    true: lqe.restore=true \* Edit `[LQE_HOME]/server/server.startup`
    file to update any of the required configurations like Java Heap
    memory allocation to match the primary server \* Edit
    `[LQE_HOME]/server/liberty/servers/clm/server.xml` file to add clone
    Id to **httpSession** element as show below \* Start the new LQE
    Node

## Update JAS Registration with new LQE Node URL

We have included scripts to add new URLs to JAS registrations which is
primarily used for setting up clustering. We can reuse these scripts for
this task.

On the LQE Server

-   Directory - \[LQE_HOME\]/server/clustering
-   Copy over the files `addNodeReg.sh` and `JASConfig.params` files to
    the server hosting Jazz Authorization Server

On the Jazz Authorization Server

-   Copy the `addNodeReg.sh` and `JASConfig.params` files to
    \[JAS_HOME\] directory
-   Edit `JASConfig.params` file and modify the **JASPATH** to set it to
    JAS install directory and **JASCREDENTIALS** to add an Admin user
    and password JASPATH=/opt/IBM/JazzAuthServer

JASCREDENTIALS=elmadmin:elmadminpassword

-   Find the ClientId of LQE Application
    -   Access JAS URL
        `https://JazzAuthServerURI/oidc/endpoint/jazzop/clientManagement`
        and login as an Admin User
    -   Search for Client name `/lqe` and copy the respective Client ID

\* Run the following command to add original (behind Reverse Proxy) and
new LQE Node URL (Update the clientId and URL) \# ./addNodeReg.sh
[https://LQEPrimaryNodeURL:PORT/lqe](https://LQEPrimaryNodeURL:PORT/lqe)
\# ./addNodeReg.sh
[https://LQENEWNodeURL:PORT/lqe](https://LQENEWNodeURL:PORT/lqe)

## Test Individual LQE Nodes and change Node Names

Test by accessing individual LQE Node URLs

Primary LQE Node:

-   Access the URL
    [https://LQEPrimaryNodeURL:PORT/lqe/web/admin/nodes](https://LQEPrimaryNodeURL:PORT/lqe/web/admin/nodes)
-   Click on the Node Name, Change name to example `LQE_Primary_Node_1`
    and click **Save**

New LQE Node:

-   Access the URL
    [https://LQENEWNodeURL:PORT/lqe/web/admin/nodes](https://LQENEWNodeURL:PORT/lqe/web/admin/nodes)
-   Click on the Node Name, Change name to example `LQE_New_Node_2` and
    click **Save**

## Setup Apache HTTP Server or HAProxy as Load Balancer for the LQE nodes

We have performed minimal testing of Load Balancing of LQE nodes using
HAProxy and Apache HTTP Server and have documented our findings below.

For open-source software, including Apache HTTP Server and HAProxy, the
following IBM Policy applies: [IBM Open Source and Third-party software
policy](https://www.ibm.com/support/pages/node/737271)

We have documented instructions to setup [Load Balancing for LQE using
Apache HTTP
Server](https://jazz.net/wiki/bin/view/Main/LQEClusterApache)

[HAProxy](http://www.haproxy.org/) is a free and open source software
that provides a high availability load balancer and reverse proxy. It
supports a rich set of [Load Balancing
algorithms](http://cbonte.github.io/haproxy-dconv/1.9/configuration.html#4.2-balance)
and the default is Leastconn. We have tested the use of HAProxy with
EWM/ETM Clustering and hence are documenting the setup of HAProxy for
LQE load balancing. HAProxy is not supported on Microsoft Windows
Operating System. You can continue to the next step if your environment
is Linux based.

The steps provided in the next section is a simple setup of HAProxy. For
detailed instructions please visit <http://www.haproxy.org/>

### Install HAProxy

You need a Linux based server in your environment to install and
configure HAProxy. Run the following commands

\# yum update \# yum install haproxy

### Create Open SSL Certificates for HAProxy

Generate SSL Certificates to be used with HAProxy via OpenSSL

\# mkdir /etc/haproxy/ssl \# cd /etc/haproxy/ssl \# openssl req -newkey
rsa:3072 -sha256 -new -x509 -days 3652 -nodes -out haproxy.crt -keyout
haproxy.key \# cat haproxy.crt haproxy.key \> haproxy.pem \# chmod +rx
haproxy.\*

Import this certificate and key file into IBM HTTP Server certificate
kdb file and the Plugin kdb file.

### Edit/Create HAProxy config file

Here is a sample `haproxy.cfg` file for load balancing 2 LQE nodes. You
could change the ports (8080, 8443, 1936) to the ports of your choice
and the user/group as well. In addition, change the path to the SSL
certificate to the one created in the previous step.

-   \# vi /etc/haproxy/haproxy.cfg

global log 127.0.0.1:514 local0 chroot /var/lib/haproxy pidfile
/var/run/haproxy.pid maxconn 4000 user haproxy group haproxy daemon

stats socket /var/lib/haproxy/stats tune.ssl.default-dh-param 2048

defaults mode http log global option http-keep-alive option dontlognull
option http-server-close option forwardfor except 127.0.0.0/8 option
redispatch retries 3 timeout http-request 10s timeout queue 1m timeout
connect 10s timeout client 2h timeout server 2h timeout http-keep-alive
10s timeout check 10s maxconn 4000

\# Connect to LQE cluster frontend lqe-proxy bind \*:8080 bind \*:8443
ssl crt /etc/haproxy/ssl/haproxy.pem no-sslv3 log global option httplog
mode http capture cookie SERVERID len 32 redirect scheme https if {
ssl_fc } maxconn 1000 \# The expected number of the users of the system.

default_backend lqe

backend lqe option forwardfor http-request set-header X-Forwarded-Port
\[dst_port\] http-request add-header X-Forwarded-Proto https if { ssl_fc
} fullconn 1000 \# if not specified, HAProxy will set this to 10 of
'maxconn' specified on the frontend balance leastconn cookie SERVERID
insert indirect nocache

\# Edit the LQE Node URLs, and change Minimum and Maximum connections as
per you need. For another node, add server lqenode1 : minconn 100
maxconn 500 ssl check cookie lqenode1 verify none server lqenode2 :
minconn 100 maxconn 500 ssl check cookie lqenode2 verify none

\# The following configuration opens the Load Balancing Statistics
Page,, change user password per your requirement listen statistics bind
\*:1936 stats uri / stats admin if TRUE stats enable stats hide-version
stats auth admin:password stats refresh 5s

### Enable and start HAProxy server

Run the following commands to start the HAProxy Server, enable it to
auto start during machine startup and to check status of the HAProxy
server

\# systemctl start haproxy \# systemctl enable haproxy \# systemctl
status haproxy

### Update JAS Registration with HAProxy URL

Find the ClientId of LQE Application (This was also done in an earlier
step)

-   Access JAS URL
    `https://JazzAuthServerURI/oidc/endpoint/jazzop/clientManagement`
    and login as an Admin User
-   Search for Client name `/lqe` and copy the respective Client ID

On the JAS Server machine, switch to \[JAS_HOME\] directory

-   Run the following command to add original (behind Reverse Proxy) and
    new LQE Node URL (Update the clientId and URL) \# ./addNodeReg.sh
    [https://HAProxyServer:PORT/lqe](https://HAProxyServer:PORT/lqe)

### Test HAProxy Load Balancer URL

Access LQE via HAProxy URL `https://HAProxyServer:PORT/lqe`

-   Review the Cookies via Browser tools, find the LQE node the request
    was redirected to, example cookie `SERVERID: "lqenode1"`
-   Access LQE via HAproxy URL on another browser or another machine and
    review the cookies to find the LQE node
-   Access the URL
    [https://HAProxyServer:PORT/lqe/web/admin/nodes](https://HAProxyServer:PORT/lqe/web/admin/nodes)
    and check the node name
-   Access the Load Balancer statistics URL `http://HAProxyServer:1936`
    (Default user and password as per the haproxy.cfg file above is
    `admin` and `password` )

## Reconfigure LQE redirection in Reverse Proxy to point to the Load Balancer

As the landing ELM and LQE URL is IHS or your configured Reverse Proxy,
you would have to change the redirection of /lqe to the HAProxy server
and port. Example of IHS plugin URL below

## Test Load Balanced LQE

Access the original LQE URL via the Revers

-   Review the Cookies via Browser tools, find the LQE node the request
    was redirected to, example cookie `SERVERID: "lqenode1"` Proxy
-   Refresh Meta model for LQE data source, review technote
    <https://www.ibm.com/support/pages/how-refresh-meta-model-data-source>
-   Review Query Statistics by Access URL
    `https://LQE_IHS_URL/lqe/web/health/query-stats`

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
