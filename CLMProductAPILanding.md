META:TOPICINFO{author="michaelrowe" date="1708036322" format="1.1"
version="1.46"} META:TOPICPARENT{name="DeploymentIntegrating"}

# API Landing page DKGRAY Authors: Main.RosaNaranjo, Main.JimRuehlin [api-landing-page-dkgray-authors-main.rosanaranjo-main.jimruehlin]

Build basis: 7.0.x ENDCOLOR

TOC{title="Page contents"}

Please note, as of release 7.0.3 this page is deprecated. Please book
mark [ELM API Landing
Page](https://jazz.net/wiki/bin/view/Deployment/ELMProductAPILanding)
for future updates.

This is a landing page for the various API wiki pages that exist on the
Jazz.net development wiki as well as a central collective page of the
known APIs that are available for integrating programmatically with our
CE/ELM products. It serves as a convenience for accessing API
information about CE/ELM products and is not guaranteed to have
up-to-the-minute information. See the official API specifications for
each CE/ELM component for complete information.

Please see the [IBM Support Statement for ELM
APIs](https://www.ibm.com/support/pages/node/284221). APIs are supported
differently than ELM products. ------- RED IBM strongly advises that any
scripts that customers develop using APIs be tested in a staging
environment prior to use in a production environment. Scripts can have
unintended performance or other consequences and thus should be highly
scrutinized prior to deployment on production systems. ENDCOLOR

[API Automation Best
Practices](https://jazz.net/wiki/bin/view/Deployment/AutomationsBestPractices)
------- **NOTE:** [Renaming the IBM Continuous Engineering
Portfolio](https://jazz.net/blog/index.php/2019/04/23/renaming-the-ibm-continuous-engineering-portfolio/)

## General OSLC and CLM API information

[OSLC Workshop](https://jazz.net/library/article/635)

[Guide for writing OSLC
integrations](https://oslc.github.io/developing-oslc-applications)

[OSLC and REST API "cheat
sheet"](https://clmpractice.org/2014/12/03/oslc-and-rest-apis-cheat-sheets-how-to-for-querying-rtc-and-dng-resources)

[ELM-CLM Root Services
Specification](https://jazz.net/wiki/bin/view/Main/RootServicesSpec)

[OSLC GitHub repository](https://github.com/OSLC)

[Eclipse Lyo](https://www.eclipse.org/lyo) is an improved Java framework
with sample libraries and reference implementations for creating OSLC
integrations

[IoT Connector](https://github.com/OSLC/iotp-adaptor) is a working
sample of an OSLC adapter for IBM Watson IoT Platform created using Lyo
Designer. It's a working example and source code for integrating with
ELM and includes common operations such as authenticating with ELM using
OAuth. It works with non-configuration management-enabled CLM systems
(aka "opt-out" DNG and RQM).

## Jazz Foundation

Foundation APIs are available in ELM applications that support those
Foundation services.

[Jazz REST Services
home](https://jazz.net/wiki/bin/view/Main/JazzRESTServicesMain)

[Jazz Foundation Process
API](https://jazz.net/wiki/bin/view/Main/DraftTeamProcessRestApi)

[JAF SDK Main Page](https://jazz.net/wiki/bin/view/Main/JAFSdk)

[Jazz Foundation SDK download
page](https://jazz.net/downloads/jazz-foundation/)

[Authentication of a native client with a Jazz-based
application](https://jazz.net/wiki/bin/view/Main/NativeClientAuthentication)

[Fetch User
Profile](https://jazz.net/wiki/bin/view/Main/FetchUserProfile)

### Global Configuration Management

GCM is a provider of global configurations as defined by the OSLC
Configuration Management draft specification; EWM SCM, Doors Next, and
ETM are providers of local configurations. These applications implement
the appropriate APIs from that specification.

Drafts of the OSLC Configuration Management Specification can be found
on the [OSLC Specifications
page](https://open-services.net/specifications/).

[Global Configuration Management REST
API](https://jazz.net/gc/doc/scenarios) - Documents extensions beyond
the OSLC specification for the current release. The same
release-specific documentation of these REST APIs can be found in your
local ELM installation at
<https://%5Bserver%5D>:\[port\]/gc/doc/scenarios.

[GCM Client Extension
API](https://jazz.net/wiki/bin/view/Main/GcmExtensionApi)

## DOORS Next Generation

Global Configuration Management REST API Documentation for the Global
Configuration Management REST API can be found at
<https://%5Bserver%5D>:\[port\]/gc/doc/scenarios. You must have the GC
application installed to access this link. This API is a collection of
REST services that client applications use to create and update
components, create new streams, create baselines, update a stream to
match a baseline, and other operations. REST client applications can use
the API to programmatically perform many of the operations that are
usually done through the GCM web user interface. See [RM Enhancement
384433](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/384433).

[RM as an OSLC service
provider](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.2?topic=services-rm-as-oslc-service-provider)

[Using OSLC capabilities in the Requirements Management
application](https://jazz.net/library/article/1197)

[DNG Server API
Documentation](https://jazz.net/wiki/bin/view/Main/DNGServerAPI)

[DNG Client Extension
API](https://jazz.net/wiki/bin/view/Main/RMExtensionsMain)

[DNG Module API](https://jazz.net/wiki/bin/view/Main/DNGModuleAPI)

[DNG Reportable REST API - v6.0 or
higher](https://jazz.net/wiki/bin/view/Main/DNGReportableRestAPI)

[RRC Reportable REST API - v4.0.x thru
v5.0.2](https://jazz.net/wiki/bin/view/Main/RRCReportableRestAPI)

[Extending requirements functionality
(video)](https://jazz.net/library/article/87230)

[RM Extensions Examples version
6.0.5](https://jazz.net/wiki/bin/view/Main/RMExtensionsExamples605)

[ReqIF API v1.0](https://jazz.net/wiki/bin/view/Main/DNGReqIF) New for
6.0.6.1

[Readiness REST API - v7.0.2 or
higher](https://jazz.net/wiki/bin/view/Main/ReadinessProbe)

## Rational Team Concert (EWM)

[Resource Oriented Work Item
API](https://jazz.net/wiki/bin/view/Main/ResourceOrientedWorkItemAPIv2)

[What APIs are available for RTC and what can you
extend?](https://rsjazz.wordpress.com/2013/03/14/what-apis-are-available-for-rtc-and-what-can-you-extend/)

[EWM SDK](https://jazz.net/wiki/bin/view/Main/EwmSdk703)

[6.0.1: OSLC API Changes for Enumerations ](CLMOSLCAPIChangesFor601)

[RTC SDK changes for RTC
6.0.3](https://rsjazz.wordpress.com/2016/11/07/the-rtc-sdk-is-about-to-change-in-6-0-3/)

[RTC Plain Java APIs](https://jazz.net/library/article/1229)

[Consuming Rational Team Concerts OSLC Change Management V2
Services](https://jazz.net/library/article/1001)

[Resource Oriented Work Item
API](https://jazz.net/wiki/bin/view/Main/ResourceOrientedWorkItemAPIv2)

[Programmatic Link Creation and new link type
contribution](https://jazz.net/wiki/bin/view/Main/ProgrammaticLinkCreation)

[Programmatic Link Creation and new link type
contribution](https://jazz.net/wiki/bin/view/Main/ProgrammaticWorkItemCreation)

[Programmatic Workitem Creation](https://jazz.net/library/article/782/)

[Extension Points and Operation
IDs](https://jazz.net/wiki/bin/view/Main/CustomPreconditionsTable#operations)

[Rational Team Concert plain Java APIs
Article](https://jazz.net/library/article/1229)

[SCM Participant for Integrating Rational Team Concert with an Activity
Stream Service](https://jazz.net/library/article/758)

[Source control process recipes for Rational Team Concert Source Control
Operations with
Preconditions](https://jazz.net/library/article/1075#operations)

[Rational Team Concert Creating Custom Operation
Advisors](https://jazz.net/library/article/495)

[Consuming Rational Team Concerts OSLC Change Management V2
Services](https://jazz.net/library/article/1001)

[RTC Automation OSLC
Prototype](https://jazz.net/wiki/bin/view/Main/RTCAutomationOSLCPrototype)

[Work Items Service provider for OSLC 2.0 CM
Specification](https://jazz.net/wiki/bin/view/Main/WorkItemAPIsForOSLCCM20)

[Reportable REST
API](https://jazz.net/wiki/bin/view/Main/ReportsRESTAPI#Reportable_REST_API)

[How consume Jazz Reportable REST API programmatically using
Java](https://jazz.net/forum/questions/211156/how-consume-jazz-reportable-rest-api-programmatically-using-java/211320)

[Rational Team Concert Extensions
Workshop](https://jazz.net/library/article/1000)

## Rhapsody Model Manager

[Reportable REST API for
RMM](https://jazz.net/wiki/bin/view/Main/RMMReportableRestAPI)

## Rational Quality Manager (ETM)

[RQM Test Automation Adapter
API](https://jazz.net/wiki/bin/view/Main/RQMTestAutomationAdapterAPI)

[RQM Reportable REST API ](https://jazz.net/wiki/bin/view/Main/RqmApi)

[OSLC QM V2 API](https://jazz.net/wiki/bin/view/Main/RqmOslcQmV2Api)

[Readiness REST API](https://jazz.net/wiki/bin/view/Main/ReadinessProbe)

## Reporting

[A look inside LQE and Report
Builder](https://jazz.net/library/article/91481)

[Integrating external data sources with LQE and Report
Builder](https://jazz.net/library/article/91450)

[RTC Reportable REST
API](https://jazz.net/wiki/bin/view/Main/ReportsRESTAPI)

[RQM Reportable REST API](https://jazz.net/wiki/bin/view/Main/RqmApi)

[DNG Reportable REST
API](https://jazz.net/wiki/bin/view/Main/DNGReportableRestAPI)

## Plain Java Client or Jazz APIs

The "official" Jazz API is available for download on the downloads page,
in the Plain Zips section, under Plain Java Client Libraries and Plain
Java Client Libraries API Documentation. The article [Rational Team
Concert plain Java API's](https://jazz.net/library/article/1229) is an
introduction into how they work. Customers wishing to write process
extensions for their Jazz implementation should begin with the [EWM/RTC
extensions workshop](https://jazz.net/library/article/1000), the
[Process enactment workshop](https://jazz.net/library/article/1093), and
the [OSLC workshop](https://jazz.net/library/article/635). This will
help them better understand the various different options for extending
and enhancing the Jazz solution, and will provide valuable insight into
how to implement the needed customizations.

## Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

## External links: [external-links]

-   [OSLC community pages](http://open-services.net/)
-   [OSLC RM Spec
    v2](http://open-services.net/bin/view/Main/RmSpecificationV2)
-   [OSLC QM Spec
    v2](http://open-services.net/bin/view/Main/QmSpecificationV2)
-   [OSLC Configuration Management domain: OASIS working
    draft](https://tools.oasis-open.org/version-control/browse/wsvn/oslc-ccm/branches/2q2015/specs/config-mgt.html)
-   [W3C: Resource Description Framework](http://www.w3.org./RDF/)
-   [W3C: Linked Data](http://www.w3.org/standards/semanticweb/data)
-   [RSJazz - What APIs are Available for RTC and What Can You
    Extend?](https://rsjazz.wordpress.com/2013/03/14/what-apis-are-available-for-rtc-and-what-can-you-extend/)
-   [RSJazz - Setting up Rational Team Concert for API
    Development](https://rsjazz.wordpress.com/2013/02/28/setting-up-rational-team-concert-for-api-development/)
-   [RSJazz - Understanding and Using the RTC Java Client
    API](https://rsjazz.wordpress.com/2013/03/20/understanding-and-using-the-rtc-java-client-api/)
-   [RSJazz - Links to other API related
    sources](https://rsjazz.wordpress.com/interesting-links/)

##### Additional contributors: Main.ThomasPoulin, Main.GeoffClemm, [Ralph Schoon](Main.RalphSchoon), Main.ToddDunnavant, Main.MichaelRowe [additional-contributors-main.thomaspoulin-main.geoffclemm-ralph-schoon-main.todddunnavant-main.michaelrowe]
