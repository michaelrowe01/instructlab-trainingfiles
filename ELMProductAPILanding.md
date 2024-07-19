# Engineering Lifecycle Management API Landing page 

Authors: Main.RosaNaranjo, Main.JimRuehlin, Main.MichaelRowe

Build basis: 7.0.x 

## Overview

This is a landing page for the various API wiki pages that exist on
Jazz.net as well as a central collective page of the known APIs that are
available for integrating programmatically with our Engineering
Lifecycle Management (ELM) products. It serves as a convenience for
accessing API information about ELM products and is not guaranteed to
have up-to-the-minute information. See the official API specifications
for each ELM component for complete information.

Please see the [IBM Support Statement for ELM
APIs](https://www.ibm.com/support/pages/node/284221). APIs are supported
differently than ELM products. ------- RED IBM strongly advises that any
scripts that customers develop using APIs be tested in a staging
environment prior to use in a production environment. Scripts can have
unintended performance or other consequences and thus should be highly
scrutinized prior to deployment on production systems. ENDCOLOR See [API
Automation Best
Practices](https://jazz.net/wiki/bin/view/Deployment/AutomationsBestPractices)
-------

## General OSLC and ELM API information

**Note all ELM servers have some level of API documentation located at
<https://://doc>**

TABLE{id="Server" sort="on" initsort="1" headerrows="1" tableborder="3"
cellpadding="5" cellspacing="2" columnwidth="15, 30, 45, 10"
tablewidth="80"}

|  |  |  |  |
|----|----|----|----|
| Application-Context | Links | Additional Details | Last Updated |
| 1 - Overview | [/jts/doc](https://jazz.net/jts/doc) | JTS Documentation Root | Release specific |
| JTS | [/jts/doc/services](https://jazz.net/jts/doc/services) | JTS Services Documentation | Release specific |
| CCM | [/ccm/doc/services](https://jazz.net/jazz/doc/services) | CCM Services Documentation (override this link with our own servers root) | Release specific |
| DCC | [/dcc/doc/services](https://jazz.net/dcc/doc/services) | DCC Services Documentation | Release specific |
| GC | [/gc/doc/services](https://jazz.net/gc/doc/services) | GC Services Documentation | Release specific |
| QM | [/qm/doc/services](https://jazz.net/qm/doc/services) | QM Services Documentation (override this link with our own servers root) | Release specific |
| RM | [/rm/doc/services](https://jazz.net/rm/doc/services) | RM Services Documentation | Release specific |

The following table contains key concepts you should become familiar
with when working with ELM and OSLC based applications' APIs.

TABLE{id="General" sort="on" initsort="1" headerrows="1" tableborder="3"
cellpadding="5" cellspacing="2" columnwidth="15, 30, 45, 10"
tablewidth="90"}

|  |  |  |  |
|----|----|----|----|
| Component | Key links | Additional Details | Last Updated |
| Workshop | [OSLC Workshop](https://jazz.net/library/article/635) | Covers CM and RM 2.0 specifications, Build basis 3.0-6.0 | April 1, 2016 |
| Guide | [Guide for writing OSLC integrations](https://oslc.github.io/developing-oslc-applications) | OSLC application development guide |  |
| Cheat Sheet | [OSLC and REST API "cheat sheet"](https://clmpractice.org/2014/12/03/oslc-and-rest-apis-cheat-sheets-how-to-for-querying-rtc-and-dng-resources) | External Blog | March 12, 2014 |
| Specification | [ELM Root Services Specification](https://jazz.net/wiki/bin/view/Main/RootServicesSpec) | Key details document to understand API discovery process | May 25, 2011 |
| OSLC | [OSLC GitHub repository](https://github.com/OSLC) | GitRepo | Ongoing |
| Eclipse | [Eclipse Lyo](https://www.eclipse.org/lyo) | Eclipse Lyo is an improved Java framework with sample libraries and reference implementations for creating OSLC integrations | June 22, 2023 |
| OSLC | [IoT Connector](https://github.com/OSLC/iotp-adaptor) | IoT Connector is a working sample of an OSLC adapter for IBM Watson IoT Platform created using Lyo Designer. It's a working example and source code for integrating with ELM and includes common operations such as authenticating with ELM using OAuth. It works with non-configuration management-enabled CLM systems (aka "opt-out" DN and ETM). | 2021 |

## Jazz Foundation

Foundation APIs are available in ELM applications that support those
Foundation services.

TABLE{id="JAF" sort="on" initsort="1" headerrows="1" tableborder="3"
cellpadding="5" cellspacing="2" columnwidth="15, 30, 45, 10"
tablewidth="90"}

|  |  |  |  |
|----|----|----|----|
| Component | Key links | Additional Details | Last Updated |
| Jazz Rest Services | [Jazz REST Services home](https://jazz.net/wiki/bin/view/Main/JazzRESTServicesMain) | Landing apge for key services details | September 26, 2009 |
| Process API | [Jazz Foundation Process API](https://jazz.net/wiki/bin/view/Main/DraftTeamProcessRestApi) | Build basis 4.0.3 | December 15, 2023 |
| Foundation SDK | [Documentation](https://jazz.net/wiki/bin/view/Main/JAFSdk) | Build basis 4.x | August 29, 2012 |
| \^ | [Download](https://jazz.net/downloads/jazz-foundation/) | Download to match your server | Ongiong |
| Authentication | [Authentication of a native client with a Jazz-based application](https://jazz.net/wiki/bin/view/Main/NativeClientAuthentication) | Details on authentication techniques across all APIs. | June 11, 2018 |
| User Profile | [Fetch User Profile](https://jazz.net/wiki/bin/view/Main/FetchUserProfile) | **NEW API** | Jauary 9, 2024 |
| Readiness API | [Documentation](https://jazz.net/wiki/bin/view/Main/ReadinessProbe) | Build basis: 7.0.2 | September 30, 2021 |
| Rest API | [JTS Scenarios](https://jazz.net/jts/doc/scenarios) | This document provides a number of scenario based examples of common uses of the API. |  |

## Global Configuration Management

GCM is a provider of global configurations as defined by the OSLC
Configuration Management specification; EWM SCM, DOORS Next, and ETM are
providers of local configurations. These applications implement the
appropriate APIs from that specification.

Documentation for the Global Configuration Management REST API can be
found at <https://%5Bserver%5D>:\[port\]/gc/doc/scenarios. You must have
the GC application installed to access this link.

TABLE{id="GCM" sort="on" initsort="1" headerrows="1" tableborder="3"
cellpadding="5" cellspacing="2" columnwidth="15, 30, 45, 10"
tablewidth="90"}

|  |  |  |  |
|----|----|----|----|
| Component | Key links | Additional Details | Last Updated |
| OSLC Configuration Management Specification | [Specifications page](https://docs.oasis-open-projects.org/oslc-op/config/v1.0/os/oslc-config-mgt.html) | Release 1.0 GCM Specifications | July 23, 2023 |
| Rest API | [Global Configuration Management Scenarios](https://jazz.net/gc/doc/scenarios) | This document provides a number of scenario based examples of common uses of the API. |  |
| Client Extention | [GCM Client Extension API](https://jazz.net/wiki/bin/view/Main/GcmExtensionApi) |  |  |

## Engineering Requirements Management DOORS Next (DN)

This API is a collection of REST services that client applications use
to create and update components, create new streams, create baselines,
update a stream to match a baseline, and other operations. REST client
applications can use the API to programmatically perform many of the
operations that are usually done through the GCM web user interface.

TABLE{id="DN" sort="on" initsort="1" headerrows="1" tableborder="3"
cellpadding="5" cellspacing="2" columnwidth="15, 30, 45, 10"
tablewidth="90"}

|  |  |  |  |
|----|----|----|----|
| Component | Key links | Additional Details | Last Updated |
| RM Service Provider | [RM as an OSLC service provider](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/doors-next/7.0.3?topic=services-rm-as-oslc-service-provider) | Documentation in IBM Docs | Release Dependent |
| OSLC Article | [Using OSLC capabilities in the RM application](https://jazz.net/library/article/1197) | Describes OSLC | January 17, 2013 |
| Server API | [Documentation](https://jazz.net/wiki/bin/view/Main/DNGServerAPI) | Supporting version 6.X and newer | February 13, 2024 |
| Client API | [Extension API Documentation](https://jazz.net/wiki/bin/view/Main/RMExtensionsMain) |  | February 13, 2024 |
| Module API | [Documentation](https://jazz.net/wiki/bin/view/Main/DNGModuleAPI) |  | December 5, 2017 |
| Reportable Rest API | [DN Reportable REST API - v6.0 or higher](https://jazz.net/wiki/bin/view/Main/DNGReportableRestAPI) | No significant changes for 7.X | March 17, 2023 |
| Reportable Rest API | [RRC Reportable REST API - v4.0.x thru v5.0.2](https://jazz.net/wiki/bin/view/Main/RRCReportableRestAPI) | No longer supported | August 6, 2018 |
| Video Tutorial | [Extending requirements functionality](https://jazz.net/library/article/87230) | Demo from DN 4.0.5 | March 09, 2017 |
| Extension Examples | [Version 7.0.3](https://jazz.net/wiki/bin/view/Main/RMExtensionsExamples703) |  | February 13, 2024 |
| ReqIF API | [ReqIF API v1.0](https://jazz.net/wiki/bin/view/Main/DNGReqIF) | New for 6.0.6.1 | October 31, 2019 |
| Rest API | [DN Scenarios](https://jazz.net/rm/doc/scenarios) | This document will provide scenario based examples of common uses of the API. |  |
| DNG Change Set Contents | [API Overview](https://jazz.net/wiki/bin/view/Main/DNGChangesetContentsApiOverview) | This document will provide scenario based examples of common uses of the API. | 02-15-2024 |

## Engineering Workflow Management (EWM / Formerly RTC)

TABLE{id="EWM" sort="on" initsort="1" headerrows="1" tableborder="3"
cellpadding="5" cellspacing="2" columnwidth="15, 30, 45, 10"
tablewidth="90"}

|  |  |  |  |
|----|----|----|----|
| Component | Key links | Additional Details | Last Updated |
| WorkItem (Resource Oriented) | [Documentation](https://jazz.net/wiki/bin/view/Main/ResourceOrientedWorkItemAPIv2) | This API allows you to get, create, modify and query work items and other resources using standard HTTP methods, allowing integrations with minimal requirements for the clients. | Feburary 2, 2021 |
| Blog post | \[<https://rsjazz.wordpress.com/2021/09/29/using-the-ewm-rest-and-oslc-apis/>\]\] | Using EWM Rest and OSLC APIs | September 29, 2021 |
| Blog post | [What APIs are available for EWM and what can you extend?](https://rsjazz.wordpress.com/2013/03/14/what-apis-are-available-for-rtc-and-what-can-you-extend/) | https://rsjazz.wordpress.com has a large number of articles available on EWM APIs and SDK usage | March 14, 2013 |
| SDK | [Document](https://jazz.net/wiki/bin/view/Main/EwmSdk703) | 7.0.3 Release | October 26, 2023 |
| OSLC - Enumerations | [API Changes for Enumerations ](CLMOSLCAPIChangesFor601) | 6.0.1: OSLC | January 5, 2017 |
| Blog post | [RTC SDK changes for RTC 6.0.3](https://rsjazz.wordpress.com/2016/11/07/the-rtc-sdk-is-about-to-change-in-6-0-3/) | https://rsjazz.wordpress.com has a large number of articles available on EWM APIs and SDK usage | November 7, 2016 |
| Java SDK | [Plain Java APIs](https://jazz.net/library/article/1229) | Article for RTC 4.0.1 | January 20, 2013 |
| OSLC | [Consuming EWM OSLC Change Management V2 Services](https://jazz.net/library/article/1001) | Introductory article on using EWM via OSLC | July 10, 2012 |
| Java | [Programmatic Link Creation and new link type contribution](https://jazz.net/wiki/bin/view/Main/ProgrammaticLinkCreation) | Introductory artcle on creating new links in EWM with Sample source code (RTC 1.x/2.x) | September 9, 2009 |
| Java | [Programmatic WorkItem Creation](https://jazz.net/wiki/bin/view/Main/ProgrammaticWorkItemCreation) | Introductory article on creating new workitems in EWM with Sample source code (RTC 1.x/2.x) | June 6, 2009 |
| Java | [Programmatic Defect Creation](https://jazz.net/library/article/782/) | Introductory article on creating a linked defect from a work item (RTC 3.x) | December 23, 2011 |
| SDK | [Extension Points and Operation IDs](https://jazz.net/wiki/bin/view/Main/CustomPreconditionsTable#operations) | Build basis RTC 3.0.1.2 | September 9th, 2019 |
| Java | [Plain Java APIs Article](https://jazz.net/library/article/1229) | Build basis RTC 4.0.1 | January 30, 2013 |
| Configuration | [Source control process recipes for Rational Team Concert Source Control Operations with Preconditions](https://jazz.net/library/article/1075#operations) | An article on how to configure preconditions and operations in EWM's source control | June 9, 2017 |
| SDK | [Creating Custom Operation Advisors](https://jazz.net/library/article/495) | Build basis RTC 2.0.0.2 | August 25, 2010 |
| OSLC | [Consuming EWMs OSLC Change Management V2 Services](https://jazz.net/library/article/1001) | Build basis RTC 4.0 | July 10, 2012 |
| OSLC | [Automation OSLC Prototype](https://jazz.net/wiki/bin/view/Main/RTCAutomationOSLCPrototype) | Prototype of services automation API | June 10, 2010 |
| OSLC | [Work Items Service provider for OSLC 2.0 CM Specification](https://jazz.net/wiki/bin/view/Main/WorkItemAPIsForOSLCCM20) | Build basis RTC 3.0.1 | May 24, 2018 |
| Reportable API | [Documentation](https://jazz.net/wiki/bin/view/Main/ReportsRESTAPI#Reportable_REST_API) | Build basis RTC 3.0.1 | August 4, 2015 |
| Reportable API | [Forum Question/Answer](https://jazz.net/forum/questions/211156/how-consume-jazz-reportable-rest-api-programmatically-using-java/211320) | How to consume Reportable REST API programmatically using Java | November 18, 2015 |
| Workshop | [Extensions Workshop](https://jazz.net/library/article/1000) | EWM Extentions Workshop material | May 7, 2021 |

## Rhapsody Model Manager

TABLE{id="RMM" sort="on" initsort="1" headerrows="1" tableborder="3"
cellpadding="5" cellspacing="2" columnwidth="15, 30, 45, 10"
tablewidth="90"}

|  |  |  |  |
|----|----|----|----|
| Component | Key links | Additional Details | Last Updated |
| Reportable API | [Documentation](https://jazz.net/wiki/bin/view/Main/RMMReportableRestAPI) | The Rhapsody Model Manager server provides REST APIs for accessing information about Architecture Management artifacts for reporting, traceability, and coverage metrics. | January 11, 2024 |

## Engineering Test Management (ETM / Formerly RQM)

TABLE{id="ETM" sort="on" initsort="1" headerrows="1" tableborder="3"
cellpadding="5" cellspacing="2" columnwidth="15, 30, 45, 10"
tablewidth="90"}

|  |  |  |  |
|----|----|----|----|
| Component | Key links | Additional Details | Last Updated |
| Test Automation Adapter | [Documentation](https://jazz.net/wiki/bin/view/Main/RQMTestAutomationAdapterAPI) | Build basis 7.0 | May 27, 2020 |
| Reportable API | [Documentation](https://jazz.net/wiki/bin/view/Main/RqmApi) | The ETM Reportable Rest API provides full CRUD capabilities | October 23, 2023 |
| OSLC | [QM V2 API](https://jazz.net/wiki/bin/view/Main/RqmOslcQmV2Api) | Supported OSLC QM V2 API as supported by ETM | August 10, 2023 |
| Rest API | [QM Scenarios](https://jazz.net/qm/doc/scenarios) | This document will provide scenario based examples of common uses of the API. |  |

## Reporting

TABLE{id="JRS" sort="on" initsort="1" headerrows="1" tableborder="3"
cellpadding="5" cellspacing="2" columnwidth="15, 30, 45, 10"
tablewidth="90"}

|  |  |  |  |
|----|----|----|----|
| Component | Key links | Additional Details | Last Updated |
| Article | [A look inside LQE and Report Builder](https://jazz.net/library/article/91481) | Describes how Lifecycle Query Engine and Report Builder process metadata from application to support reporting in ELM | February 2018 |
| Article | [Integrating external data sources with LQE and Report Builder](https://jazz.net/library/article/91450) | This article is intended for developers who want to contribute data from 3rd-party applications or external data sources to the LQE data source for reporting. It includes references and links to a companion article that describes how LQE and Report Builder process the metadata to support reporting. | March 2022 |
| Reportable API | [EWM Documetation](https://jazz.net/wiki/bin/view/Main/ReportsRESTAPI) | EWM Reportable Rest API | August 4, 2015 |
| Reportable API | [ETM Documenation](https://jazz.net/wiki/bin/view/Main/RqmApi) | ETM Reportable Rest API | October 3, 2023 |
| Reportable API | [DN Documentation](https://jazz.net/wiki/bin/view/Main/DNGReportableRestAPI) | DN Reportable Rest API | March 17, 2023 |

## Plain Java Client or Jazz APIs

The "official" Jazz API is available for download on the downloads page,
in the Plain Zips section, under Plain Java Client Libraries and Plain
Java Client Libraries API Documentation. The article [Rational Team
Concert plain Java API's](https://jazz.net/library/article/1229) is an
introduction into how they work. Customers wishing to write process
extensions for their Jazz implementation should begin with the [RTC
extensions workshop](https://jazz.net/library/article/1000), the
[Process enactment workshop](https://jazz.net/library/article/1093), and
the [OSLC workshop](https://jazz.net/library/article/635). This will
help them better understand the various different options for extending
and enhancing the Jazz solution, and will provide valuable insight into
how to implement the needed customizations.

## Related topics: 
-   [Deployment web home](DeploymentWebHome)

## External links: 

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
-   [michaelrowe01 - Beginning API
    Discovery](https://michaelrowe01.com/index.php/day-job/ibm-elm/beginning-api-discovery-or-understanding-the-rootservices-document/)
-   [michaelrowe01 - ELM Oauth 1.0a
    Example](https://michaelrowe01.com/index.php/day-job/ibm-elm/api-authentication-method-in-elm-oauth-1-0a/)
-   [michaelrowe01 - ELM OIDC
    Example](https://michaelrowe01.com/index.php/day-job/ibm-elm/api-authentication-method-in-elm-oidc/)

##### Additional contributors: 
-   [Ralph Schoon](Main.RalphSchoon), 
-   Main.ToddDunnavant
