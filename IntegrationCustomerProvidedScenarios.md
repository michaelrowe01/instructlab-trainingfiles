META:TOPICINFO{author="mariannehollier" date="1435776633" format="1.1"
reprev="1.6" version="1.6"}
META:TOPICPARENT{name="IntegrationHighPriorityScenarios"}

# Integration: Customer Scenarios [integration-customer-scenarios]

DKGRAY Cross-cutting theme technical leaders and senior editors:
Main.AmySilberbauer ENDCOLOR

TOC{title="Page contents"}

In this section we capture the scenarios developed through direct
collaboration with customers in the most recent Voice of the Customer
(VoiCE) sessions held in Orlando in June 2014. Thank you to all of the
participants that helped us develop these initial scenarios. You will
notice that we developed our **top** scenarios for integration focus
largely based on this content. You can see those high priority scenarios
here: [High Priority Scenarios](IntegrationHighPriorityScenarios).

In each of the scenarios, note the products involved, the integration
points, the activity flow, and the integration issues encountered. Also,
customers specified some key areas for improvement.

## Pre-Deployment (Install/Upgrade) Scenarios

This section illustrates the pre-deployment scenarios as described by
you, our customers. The key role in these scenarios is the **Tool
Administrator**.

### New Installation

This is a typical **New Installation** scenario. The key issue
identified here is the lack of information (documentation) available.
Further, it was noted that when information is available, it is either
incomplete or in some cases just plain wrong.

Among the thoughts for improvement are: \* Making integrations less
dependent on the sequence in which the installation of products occurs
\* Focusing on standards-based integrations, such as OSLC, which are
consistently used across the products \* Automating the more basic
steps, such as the gathering of information, generation of customized
steps as a result of using the Interactive Installation Guide, etc..

### Upgrade

This is a typical **Upgrade** scenario. The key issue identified here is
that there are often critical steps missing from the upgrade guidance.
Among the thoughts for improvement are:

-   Making integrations less dependent on the sequence in which the
    installation of products occurs
-   Focusing on standards-based integrations, such as OSLC, which are
    consistently used across the products
-   Automating the more basic steps, such as the gathering of
    information, generation of customized steps as a result of using the
    Interactive Installation Guide, etc..

As in the new installation scenario, best practices include use of the
Interactive Installation Guides, although because this is an upgrade
scenario, improvements to this process include the need to customize the
output from the installation guides with information from the existing
environment.

## Post-Deployment (Usage) Scenarios

Just as we describe the **Golden Topologies** supported and validated by
Rational, we also want to focus on the critical usage scenarios specific
to integrations. The high priority scenarios related to **usage**
scenarios are described below. These are our **Golden Integration
Scenarios** that will be our primary focus in the coming months. The key
roles in these scenarios vary, but they are essentially the
**Practitioners** in the target environment.

### **Requirements Management & Analysis**

This scenario describes the activity of managing and analyzing
requirements across the development lifecycle. The roles, activities,
products, and integrations are identified. Products include Rational
strategic and legacy products as well as third-party products. Key
issues include:

-   Problems importing into Rational's requirement management tooling
    from third-party products/formats
-   Performance and capability issues with the integrations that provide
    traceability between requirements and quality management artifacts
-   Lack of capabilities in producing reports

It is noted that some of these issues will be alleviated by moving off
Rational legacy tooling, such as RequisitePro, to the more strategic
tooling.

### **Development & Build**

This scenario describes a core activity supported by Rational:
**Development & Build**. The roles, activities, products, and
integrations are identified. Products include Rational strategic and
legacy products as well as third-party products. The significant issues
in this scenarios largely reflect the vast diversity of tools involved
for development, testing and build:

-   Integrations among the tools that are outside the boundaries of what
    we call Rational **ALM Core** are insufficient
-   Beyond **ALM Core** there are often performance and scalability
    issues
-   The lack of standard interfaces defined for the **ALM Core** tool
    set makes development of integrations difficult, costly and
    time-consuming

Among the key areas for improvement are standardization of process and
practices across the **ALM Core** tool set.

### **Migration**

This scenario is interesting in that, at first glance, it may seem to
have little to do with product-level integrations. In fact, the
**Migration** scenario does involve integrations in the sense that it is
typically a longer-term activity in which multiple systems co-exist at
least for some period of time. In addition, integration points must
address the mapping of attributes and other artifact characteristics
from the source system to the target system.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)
-   [IBM Software Product Compatibility
    Reports](http://publib.boulder.ibm.com/infocenter/prodguid/v1r0/clarity/index.jsp)

##### Additional contributors: Main.AllisonLynch, Main.IanCompton, Main.AnthonyKesterton, Main.MarianneHollier, Main.SherriMidyette [additional-contributors-main.allisonlynch-main.iancompton-main.anthonykesterton-main.mariannehollier-main.sherrimidyette]

META:FILEATTACHMENT{name="PlanExecuteNewInstall.png"
attachment="PlanExecuteNewInstall.png" attr="" comment="Customer version
of the Plan & Execute a New Install Scenario" date="1435776575"
path="PlanExecuteNewInstall.png" size="97729" user="mariannehollier"
version="4"} META:FILEATTACHMENT{name="PlanExecuteUpgrade.png"
attachment="PlanExecuteUpgrade.png" attr="" comment="Customer version of
the Plan & Execute an Upgrade Scenario" date="1435776632"
path="PlanExecuteUpgrade.png" size="108073" user="mariannehollier"
version="3"}
META:FILEATTACHMENT{name="RequirementsManagementAnalysis.png"
attachment="RequirementsManagementAnalysis.png" attr=""
comment="Customer version of the Requirements Analysis Scenario"
date="1407946099" path="RequirementsManagementAnalysis.png"
size="153961" user="asilber" version="3"}
META:FILEATTACHMENT{name="DevelopmentBuildRoleBased.png"
attachment="DevelopmentBuildRoleBased.png" attr="" comment="Customer
version of the Development & Build Scenario" date="1407946034"
path="DevelopmentBuildRoleBased.png" size="153016" user="asilber"
version="2"}
META:FILEATTACHMENT{name="MigrateTeamxfromVersionytoVersionz.png"
attachment="MigrateTeamxfromVersionytoVersionz.png" attr=""
comment="Customer version of the Migration Scenario" date="1407781428"
path="MigrateTeamxfromVersionytoVersionz.png" size="88252"
user="asilber" version="1"}
