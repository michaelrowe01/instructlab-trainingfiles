META:TOPICINFO{author="mariannehollier" date="1450380520" format="1.1"
version="1.27"} META:TOPICPARENT{name="WebHome"}

# Integration: Golden Integration Scenarios [integration-golden-integration-scenarios]

DKGRAY Cross-cutting theme technical leaders and senior editors:
Main.AmySilberbauer, Main.DaleHobill Build basis: Rational solution for
Collaborative Lifecycle Management (CLM) 6.0 ENDCOLOR

TOC{title="Page contents"}

## Introduction

In this section we document the **Golden Integration Scenarios** derived
through direct customer interaction and feedback. The original scenarios
developed with customers can be found here: [Customer
Scenarios](IntegrationCustomerProvidedScenarios). Just as we describe
the **Golden Topologies** for product and solution deployment that are
supported and validated, we also want to focus on the critical usage
scenarios specific to integrations. These scenarios will be our primary
focus in the coming months.

While we are currently focusing on these scenarios as documented, we
always appreciate feedback as well as thoughts on additional scenarios
going forward. Please provide feedback or pose questions in the
**Questions and comments** box at the bottom of the
[Integrating](DeploymentIntegrating) page.

## Top Integration Scenarios Scenarios help us understand the activities performed by various roles in an organization in the context of their day-to-day jobs. By collaborating with clients to define scenarios, we develop insight into how our solutions are used and where we must focus to ensure a valuable end-user experience. In the sections below, you can review the scenarios we will focus on to ensure an improved experience through the development of clear and concise documentation, validation plans, and the identification and ultimate closure of gaps in the integrations involved. Where we have gaps in the integrations for the scenarios below, we have highlighted those; where we have plans to validate but have not yet fully validated the scenarios, we have provided annotations.

### **Requirements Management & Analysis**

\* **Documentation:**

-   The **ALM Core** products in this scenario are RTC, RDNG, and RQM.
    These are all part of the Collaborative Lifecycle Management
    solution and integrations are fully documented. Links to the
    specific Knowledge Center topics can be found on the
    [Integrating](DeploymentIntegrating) page.
-   Outside of **ALM Core**, documentation is provided for:
    -   Integration between CQ and RTC, as part of the RTC product
        documentation.
    -   Import of requirements from external documents, including MS
        Word documents, in the Knowledge Center topic [Importing and
        extracting requirement artifacts from
        documents](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_6.0.0/com.ibm.rational.rrm.help.doc/topics/t_import_reqs_from_docs.html?lang=en).
    -   Integration between the CLM solution and Rational Insight in the
        Rational Insight Knowledge Center Topic [Integrating with the
        Rational solution for Collaborative Lifecycle Management
        (CLM)](http://www-01.ibm.com/support/knowledgecenter/SSRL5J_1.1.1/com.ibm.rational.raer.integration.doc/topics/c_integrate_clm_ovr.html?lang=en).
    -   [Help with Global
        Configurations](https://jazz.net/servlet/clm-cm/request-key)

\* **Known Issues:**

-   Global Configuration (GC) and Integrations:
    -   DOORS 9 works with CLM 6.0, but not with GC management
        capabilities.
    -   Requirement reconcile operation in RQM is NOT supported.
    -   In traceability views, you cannot filter by Development Item or
        Development Plan links.
    -   You cannot link RTC plans to versioned test plans; links will
        resolve to the default configurations.
    -   Even if you link to the default RQM configuration, the RTC plan
        traceability filter will show no results.
-   In RQM 6.0, the following are **not** supported when working with
    GC-management enabled project areas:
    -   RQM Execution Tool, Copy Utility, URL Utility, OSLC Cleaner
        Utility, API Utility
    -   RQM Excel/Word Importer
    -   RQM mobile application for offline test execution

\* **Validation:**

-   The **ALM Core** integrated behavior captured in this scenario is
    well-covered by our solution testing.

\* **Notes:** \* RequisitePro integration has been removed in CLM 6.0 \*
You can migrate from RequisitePro to RDNG, including all QM links \* You
can upgrade to CLM 6.0 and then migrate ReqPro to RDNG but you cannot
use Global Configuration management (GC) until you do this

### **Development & Build**

\* **Documentation:**

-   The **ALM Core** products in this scenario are RTC and Rhapsody.
    Integrations are fully documented. Links to the specific Knowledge
    Center topics can be found on the
    [Integrating](DeploymentIntegrating) page.
-   Outside of **ALM Core**, documentation is provided for:
    -   Integration between RTC and RDz, CC and UC Deploy, as part of
        the RTC product documentation.
    -   Integration between RTC and third-party tools, as part of the
        RTC product documentation.

\* **Known Issues:**

-   Rhapsody build configurations and code generation do not currently
    support all targets
-   Better guidance must be provided with respect to shell-sharing
    between **ALM Core** and other Rational and non-Rational products
-   Version compatibility for both clients and servers for Rational
    **ALM Core** products in the context of this scenario must be
    clarified

\* **Validation:** \* The **ALM Core** integrated behavior captured in
this scenario is well-covered by our solution testing. \* We do not
currently validate the RTC - UC Deploy integrations. This is on our
"gaps" list. \* We do not validate integration with third-party tooling
as part of solution testing in the context of this scenario. Generally,
these integrations are tested by the third-party organization that
develops and delivers the integrations.

#### **Development & Build (Tool-Based View)**

The visualization below supplements the Development & Build scenario to
capture the wide variety of tooling that may be involved in a typical
customer's heterogeneous environment.

\* **Documentation:**

-   The **ALM Core** products in this scenario are RTC and RQM and
    include the various RTC clients and build components. Links to the
    specific Knowledge Center topics can be found on the
    [Integrating](DeploymentIntegrating) page.
-   Outside of **ALM Core**, documentation is provided for:
    -   Integration between RTC and the IDEs (RAD, RDz, RDi) and UC
        Deploy, as part of the RTC product documentation.
    -   Integration between RTC and third-party tools (except Endevor
        and ChangeMan), as part of the RTC product documentation.
    -   Integration between RQM and third-party tools, as part of the
        RQM product documentation.
    -   Integration between RDz and the CA Endevor SCM is document in
        the RDz Knowledge Center topic [Accessing the CA Endevor
        Software Change Manager
        (SCM)](http://www-01.ibm.com/support/knowledgecenter/SSQ2R2_9.1.1/com.ibm.etools.carma.endevor.doc/concepts/accessingthecaendevorscmusingcarma.html?lang=en)

\* **Known Issues:**

-   Incomplete documentation for some IDEs: WDT, Data Architect, Data
    Stage, Mobile First Platform
-   Artifactory integration does not exist
-   Better guidance must be provided with respect to shell-sharing
    between **ALM Core** and other Rational and non-Rational products
-   Integration between RDz and ChangeMan has little documented details

\* **Validation:** \* Solution testing in the context of this scenario
is focused on the most common clients: Web UI and Eclipse UI \*
Individual development organizations provide function testing for ISPF
and Windows Shell clients. \* Validation of the Visual Studio client is
performed on an as-needed basis. \* Outside of **ALM Core**, we rely on
a large number of internal IBM development organizations to self-host,
specifically for integration with UC Deploy and RTW.

### **Source Code Management**

\* **Documentation:**

-   The **ALM Core** product in this scenario is RTC. Outside of **ALM
    Core**, documentation is provided for:
    -   Integration between RTC and some of the IDEs (RAD, RDz), as part
        of the RTC product documentation.

\* **Known Issues:**

-   Incomplete documentation for some IDEs: WDT, Data Architect, Data
    Stage, Mobile First Platform
-   Better guidance must be provided with respect to shell-sharing
    between **ALM Core** and other Rational and non-Rational products
-   We need to do a better job articulating the SCM usage scenario with
    RTC as the centralized SCM tool

\* **Validation:** \* Solution testing for SCM activities in a scenario
context focuses on the basic SCM activities; we rely on a large number
of internal IBM development organizations to self-host and develop
across the variety of platforms and clients that require SCM support.

## Future Areas of Focus

### Integrations in the Context of [IBM DevOps](http://www.ibm.com/ibm/devops/us/en/community/)

As we look beyond the **ALM Core** tool set to the end-to-end [IBM
DevOps](http://www.ibm.com/ibm/devops/us/en/community/) lifecycle, we
will be focusing on the documentation and validation of the tools that
must be integrated to support Plan, Development & Test, Deploy and
Operate activities. These integrations must also work seamlessly in
on-premise, cloud and hybrid development and deployment environments.

### Integrations in the Context of a Heterogeneous Environment

It is almost never the case that the Rational Collaborative Lifecycle
Management (CLM) and Systems and Software Engineering (SSE) solutions
are deployed in an environment that does not require, or could not
benefit from, integrations with other tools, Jazz-based or not. This
includes other IBM tools, as well as third-party and homegrown tools.
The most typical tools that must be integrated in such an environment,
based on customer feedback, are directly aligned with our **Golden
Integration Scenarios** described above.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)
-   [IBM Software Product Compatibility
    Reports](http://publib.boulder.ibm.com/infocenter/prodguid/v1r0/clarity/index.jsp)

##### Additional contributors: Main.AllisonLynch, Main.IanCompton, Main.AnthonyKesterton, Main.MarianneHollier, Main.SherriMidyette, Main.RosaNaranjo [additional-contributors-main.allisonlynch-main.iancompton-main.anthonykesterton-main.mariannehollier-main.sherrimidyette-main.rosanaranjo]

META:FILEATTACHMENT{name="ScenarioDesigns_DevelopmentBuildRoleBased_2.png"
attachment="ScenarioDesigns_DevelopmentBuildRoleBased_2.png" attr=""
comment="Top Scenario - Development & Build (Role-based)"
date="1438982564" path="ScenarioDesigns_DevelopmentBuildRoleBased_2.png"
size="142386" user="mariannehollier" version="2"}
META:FILEATTACHMENT{name="ScenarioDesigns_DevelopmentBuildToolBased_1.png"
attachment="ScenarioDesigns_DevelopmentBuildToolBased_1.png" attr=""
comment="Top Scenario - Development & Build (Tool-based)"
date="1438982665" path="ScenarioDesigns_DevelopmentBuildToolBased_1.png"
size="134137" user="mariannehollier" version="2"}
META:FILEATTACHMENT{name="ScenarioDesigns_RequirementsManagementAnalysis_2.png"
attachment="ScenarioDesigns_RequirementsManagementAnalysis_2.png"
attr="" comment="Top Scenario - Requirements Management"
date="1438982450"
path="ScenarioDesigns_RequirementsManagementAnalysis_2.png"
size="153735" user="mariannehollier" version="3"}
META:FILEATTACHMENT{name="ScenarioDesigns_SourceCodeManagement.png"
attachment="ScenarioDesigns_SourceCodeManagement.png" attr=""
comment="Top Scenario - Source Code Management" date="1438982795"
path="ScenarioDesigns_SourceCodeManagement.png" size="106395"
user="mariannehollier" version="2"}
