META:TOPICINFO{author="sbagot" date="1432664314" format="1.1"
reprev="1.7" version="1.7"}
META:TOPICPARENT{name="PerformanceTroubleshooting"}

# Why do some pages take two minutes to load? [why-do-some-pages-take-two-minutes-to-load]

DKGRAY Authors: PerformanceTroubleshootingTeam Build basis: CLM 3.x and
later ENDCOLOR

TOC{title="Page contents"}

This article explains why some pages take two minutes to load and
possible solutions to the problem.

## Symptoms and problem description

Using a web browser, users attempting to load Rational Team Concert
pages experience long delays lasting around two minutes. These delays
are not consistent, but always seem to occur the first time the users
attempt to use RTC within a fresh browser session. Subsequent loads of
the same page in the same browser session return much quicker as
expected.

This problem tends to occur in federated or isolated environments
(environments where the client and server are not connected to the
Internet but are behind a firewall and are secured from the outside).

This problem also tends to occur in Windows environments where Microsoft
Active Directory Server is used.

### Solution 1: Root hints are not disabled

If the environment is completely isolated from the outside world, it is
possible that a DNS server is still configured to use root hints. If a
network is connected to the Internet, a root hints file, or a cache
hints file contains the names and Internet addresses of root DNS servers
which in turn are used to resolve other Internet names and addresses.

If a network is not connected to the Internet, it is possible that a DNS
server is attempting to reach each external root server listed in the
root hints file and sequentially timing out for each request until it
tries a local DNS server within the isolated network. (The default
timeout is 20 seconds and some default root hints files have 6 entries
which can explain the approximate two-minute or 20-second x 6-tries
delay.)

To solve the problem, on the Active Directory server, open Microsoft DNS
Manager console. Right-click on the DNS server you need to configure.
Click Properties and then the Root Hints tab. Check the box to Disable
recursion (also disables forwarders). In some versions of Active
Directory the option is called Disable root hints.

Additionally, if your network is not connected to the Internet,
Microsoft suggests you replace the NS and A records in the cache hints
file with NS and A records for the DNS servers that are authoritative
for the root of your private TCP/IP network. See
<http://technet.microsoft.com/en-us/library/cc958982.aspx> for a further
discussion.

### Solution 2: Port 8880 or other WebSphere ports are blocked

Some ports including port 8880 which is the SOAP_CONNECTOR_ADDRESS for
WebSphere Application Server may be blocked. Unblocking ports can remove
the approximate two-minute delay. Refer to the specific firewall
instructions for your server. Generally you may need to grant WebSphere
firewall exceptions at the application level, but in some cases you may
need to explicitly open ports for specific application or ask the server
to leave them open permanently.

Refer to WebSphere Application Server documentation for other default
ports. For example, the Port number settings in WebSphere Application
Server ver 8 are at
<http://www.ibm.com/support/knowledgecenter/SS7JFU_8.0.0/com.ibm.websphere.migration.express.doc/info/exp/ae/rmig_portnumber.html>

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [Root Hints
    Files](http://technet.microsoft.com/en-us/library/cc958982.aspx)

##### Additional contributors: None [additional-contributors-none]
