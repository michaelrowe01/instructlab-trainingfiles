META:TOPICINFO{author="gcovell" date="1403814301" format="1.1"
reprev="1.10" version="1.10"}
META:TOPICPARENT{name="PerformanceDatasheetsAndSizingGuidelines"}

# Web caching performance improvements in Rational Team Concert 5.0 [web-caching-performance-improvements-in-rational-team-concert-5.0]

DKGRAY Authors: Main.JohnCox Date: June 2, 2014 Build basis: Rational
Team Concert 5.0 ENDCOLOR

TOC{title="Page contents"}

## Overview

Rational Team Concert (RTC) version 5.0 provides new Web caching
technology that can improve application performance and scalability. The
new technology stores cachable information locally on the client. Each
Web browser request to an RTC service is made up of many individual URL
GETs performed by the browser to fill in the page. Some of the
information that is requested does not change over the lifetime of the
user's browser session. For example, images that make up the icons on
the Web page are static. They do not change during an open session with
the server. It is safe to cache this type of information on the client
side. This reduces the number of individual GET requests for each page.
RTC 5.0 uses a technology called browser local storage to store the
cached information on the client. JavaScript then executes within each
page to pull the information from local storage.

## Performance project

A project was created to measure the 5.0 Web caching performance
improvements. RTC 4.0.6 and 5.0 configurations were deployed using the
E1 topology. This enterprise topology uses Linux for the server
operating systems. The CLM applications, RRDI and JTS are distributed
across separate servers and WAS instances. A reverse proxy is used to
ensure public URI stability. DB2 is used for the databases and is hosted
on a separate server. Finally, licenses are served by a floating license
server and Tivoli Directory Server provides the LDAP based user
management.

The workload used in the test was created from the JKE Banking sample
application. The application was deployed and Rational Performance
Tester (RPT) was used to create a script for performance load driving.
To create the script RPT acts as a proxy and records each of the
individual URL GETs that are requested for each page. The tests were
created individually for 4.0.6 and 5.0. 5.0 is caching some of the GET
requests and therefore RPT recorded fewer for each full page request.
For this project 10 individual work item pages were requested and
recorded.

The first advantage shown by the new Web caching technology in 5.0 is
seen by looking at the individual URL GETs that make up a request for a
single work item. In 4.0.6 this consists of around 54 individual GET
requests. The caching technology in 5.0 reduces this to 39 individual
GET requests. **This is close to a 25 reduction in the number of GET
requests made to the server**. It is important to note though that the
recorded requests for each work item perform a load of the full page for
that work item. Typically, once a work item has been opened, further
work items will be loaded by using REST services to request the
information for that work item and filling in the page. Therefore, this
test measures the improvement for the scenarios that leverage the Web
caching technology in 5.0.

The reduction in GET requests also improves the performance of the
server under load. A test was conducted where 10 simulated users
accessed the 10 recorded work items in a loop with zero think time. This
test loosely models a busy server environment and measures the response
time for each page. Results for 4.0.6 and 5.0 are shown the following
figure.

### Web caching results

Results for 4.0.6 and 5.0 are shown in the following figure.

Response times measured show a significant advantage for the 5.0 Web
caching technology. Response times display improvement in a range of 8
to 2x. This is a wider than expected range. However, the mix of the load
on the servers for these tests can be complex. Many of the URL GETs are
requested in parallel. The results show a waterfall pattern with periods
of higher concurrency (detailed below).

## WAN environment simulation

It is common in enterprise environments to have users spread out over
the globe in a wide-area network (WAN) environment. Remote users can
experience a significant delay introduced by network congestion over the
WAN. These delays can range from milliseconds to several seconds.
Therefore, reducing the number of requests and improving response time
can be even more critical in a WAN environment.

The tests described previously were performed again in a WAN simulated
environment. For this test an artificial delay of 1 second was added to
all network requests between the RPT load drivers and the CLM HTTP
servers. This was achieved using the netem technology that is built into
Linux. The command line used was:

tc qdisc add dev eth0 root netem delay 1000ms

### WAN environment results

Results for the WAN environment tests are shown in the following figure.

These results show the dramatic effect network delays can have on
overall response time. In the prior data all response times for the work
items tested were less than 1 second. In the WAN emulation test cases
response times ranged from around 12 seconds to as high as 28 seconds.
As mentioned earlier, each work item request results in a number of GET
requests to the server, thus amplifying the effect of the WAN network
delay.

### Waterfall flow of concurrent requests

Once again response times measured show a significant advantage for the
5.0 Web caching technology. Response times in the WAN tests show
improvement in a range of 16 to 2x for 5.0 over 4.0.6. This is
comparable to the 8 to 2x difference measured in the prior performance
test.

Version 4.0.6 produces more GET requests for each work item and each
network request is delayed in the WAN test. Therefore, logically you
might expect for the Web caching introduced in 5.0 to have a greater
impact on performance improvement in the WAN environment. This is not
the case however. This is due to the waterfall pattern of GET requests
to the server. The waterfall pattern is produced by a mix of serial and
concurrent GET requests. Serial requests are dependent on the results of
a former request in the page. Once the response is received further
requests can then be made. Once these responses are received, additional
requests are produced, and so on until the full page is loaded. The
figure to the left shows the waterfall GET request pattern in a graphic
format. The figure on the right is a capture of the pattern for an
actual request used in this testing. Red lines are drawn to show groups
of requests that are conducted concurrently by the browser for this
page.

## Summary

RTC 5.0 introduces a new Web caching technology that improves
performance and scalability. RTC 5.0 reduces the GET requests by caching
safe information on the client side. A technology called browser local
storage to store the cached information on the client. JavaScript then
executes within each page to pull the information from local storage. A
reduction of close to 25 GET requests per work item was measured in
tests described in this paper. The reduced number of GET requests
resulted in average response time improvements of 8 to 2x.

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

META:FILEATTACHMENT{name="Enterprise_Distributed_Linux_DB2.png"
attachment="Enterprise_Distributed_Linux_DB2.png" attr="h" comment="CCM
Enterprise Distribution Pattern for CCM" date="1398993777"
path="Enterprise_Distributed_Linux_DB2.png" size="63660" user="stancox"
version="1"} META:FILEATTACHMENT{name="4.06vs5.0.png"
attachment="4.06vs5.0.png" attr="h" comment="4.06 vs 5.0 Response Time"
date="1403813830" path="4.06vs5.0.png" size="15799" user="stancox"
version="4"} META:FILEATTACHMENT{name="4.06vs5.0-WAN.png"
attachment="4.06vs5.0-WAN.png" attr="h" comment="4.06 vs 5.0 Response
Time WAN" date="1403813884" path="4.06vs5.0-WAN.png" size="15925"
user="stancox" version="3"} META:FILEATTACHMENT{name="waterfall.png"
attachment="waterfall.png" attr="h" comment="Waterfall request pattern"
date="1398994779" path="waterfall.png" size="75113" user="stancox"
version="1"} META:FILEATTACHMENT{name="4.06vs5.0-WANa.png"
attachment="4.06vs5.0-WANa.png" attr="h" comment="4.06 vs 5.0 Response
Time WAN" date="1403812526" path="4.06vs5.0-WANa.png" size="15906"
user="stancox" version="2"}
META:FILEATTACHMENT{name="waterfall-graph.png"
attachment="waterfall-graph.png" attr="h" comment="" date="1400007344"
path="waterfall-graph.png" size="21152" user="stancox" version="1"}
