META:TOPICINFO{author="bhumikabalani" date="1386100759" format="1.1"
reprev="1.5" version="1.5"}
META:TOPICPARENT{name="DeploymentIntegrating"}

# Leveraging integration of Rational Focal Point with Collaborative Lifecycle Management [leveraging-integration-of-rational-focal-point-with-collaborative-lifecycle-management]

DKGRAY Authors: Main.VipinKAgrawal, Main.TWikiUser Build basis:
Products, editions, or versions that apply to the content. If no build
basis applies to this content, set the build basis to None. ENDCOLOR

TOC{title="Page contents"}

IBM Rational Focal Point (RFP) provides Collaborative Lifecycle
Management (CLM) integrations through its support of the Open Services
Lifecycle Collaboration (OSLC) change management and requirement
management specifications. Product manager (PM) captures and describes
high level stakeholders' requests (i.e. Business Requirements/Needs) in
RFP. PM does prioritization of captured high level stakeholders'
requests using RFP's prioritization feature. Then PM selects Business
Requirements/Needs, which need to be further analyzed by a Business
Analyst, and creates new requirements in IBM Rational Requirements
Composer (RRC) which are further elaborated in RRC and implemented in
IBM Rational Team Concert (RTC). The reporting capability implemented in
this release is really very useful for PM as PM can generate
Traceability report to find out whats the current status of a RFP
Requirement/Business Need to related Requirements in RRC(Elaboration) to
related Project status in RTC(Implementation) and Test Cases and
Execution Records with related defects in RQM(Testing) at any point of
time.

Introductory paragraph Introductory paragraph Introductory paragraph
Introductory paragraph Introductory paragraph Introductory paragraph
Introductory paragraph Introductory paragraph Introductory paragraph
Introductory paragraph Introductory paragraph Introductory paragraph
Introductory paragraph Introductory paragraph Introductory paragraph
Introductory paragraph Introductory paragraph Introductory paragraph
Introductory paragraph

## Configuration (use sentence-style capitalization)

I\) Register OAuth Consumer in CLM Server First step is to register IBM
Rational Focal Point as an incoming consumer in the CLM application
server. In CLM application consumer key is generated for each
application (RRC, RTC, RQM) which is used to identify IBM Rational Focal
Point to the CLM application server.

Procedure: \# Login to CLM sever with administrator credentials. \# Go
to CLM application server configuration page. e.g. for the Requirements
Management application for CLM, go to
<https://example.com:9443/jts/admin> and click Jazz Team Server - Server
Administration. \# In the navigation bar, click Consumers (Inbound). \#
Register the consumer by providing data for Consumer Name and Consumer
Secret. \# It will generate a consumer key. Make a note of the consumer
secret and consumer key as you need it to add the application server as
a friend in Rational Focal Point.

### II) Register Friend (Outbound) in CLM Server

Procedure: 1. This is required viewing Rich hover data in CLM server. 2.
In the navigation bar, click Friend (Outbound) and Click Add. 3.
Register the consumer by providing data for Name, Root Services URI
(e.g. <http://example.com:8080/fp/resources/rootservices>), OAuth Secret
and click Create Friend. 4. It will generate a consumer key. Make a note
of the consumer secret and consumer key as you need it to add the
application server as a friend in Rational Focal Point.

### III) Configure CLM Server as a friend in RFP using OAuth based Authentication Procedure:

1\. Go to Application \> Friends(Outbound) and Click Add Friend. 2.
Provide connection name, CLM Root Services URI (e.g. for RRC
<http://example.com>::9443/jts/rootservices) and OAuth consumer
key/secret you got from CLM. 3. Use Test Connection button to validate
CLM server credentials. 4. Save the connection. 5. More than one CLM
servers can be configured as friend.

Section text Section text Section text Section text Section text Section
text Section text Section text Section text Section text Section text
Section text Section text Section text Section text Section text Section
text Section text Section text Section text Section text Section text
Section text Section text Section text Section text Section text Section
text Section text Section text Section text Section text Section text
Section text Section text

### Heading 2 (use sentence-style capitalization)

Vipin Sub-Section text Sub-Section text Sub-Section text Sub-Section
text Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text

### Heading 2 (use sentence-style capitalization)

Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text

## Heading 1

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
