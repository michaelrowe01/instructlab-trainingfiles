META:TOPICINFO{author="lekandrade" date="1694625513" format="1.1"
version="1.24"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Deployment options for IBM Engineering Workflow Management with Architecture Management Extension DKGRAY Authors: Main.TimFeeney, Main.RazYerulshalmi, Main.SashaRekhter, Main.GeoffClemm [deployment-options-for-ibm-engineering-workflow-management-with-architecture-management-extension-dkgray-authors-main.timfeeney-main.razyerulshalmi-main.sasharekhter-main.geoffclemm]

Build basis: 7.0+ ENDCOLOR

TOC{title="Page contents"}

As of 7.0, [Rhapsody Model Manager (RMM) is now provided as an extension
for an Engineering Workflow Management (EWM) server, rather than as a
separate Architecture Management (AM)
application](https://jazz.net/pub/new-noteworthy/rmm/7.0/7.0/index.html).
This article describes the options and tradeoffs for choosing separate
or combined Change and Configuration Management (CCM) and AM servers
whether starting with a new deployment or migrating from an existing 6.x
deployment.

## New 7.x deployment of CCM and AM applications

When both the CCM and AM capabilities are needed, ***the preferred
option for new deployments is a single EWM server with the CCM and RMM
applications installed together*** (thus making the AM extension
available to enable on projects). The additional load from AM workflows
on the CCM application have [little impact on CCM service
times](https://jazz.net/wiki/bin/view/Deployment/PerformanceImpactOfCombiningRMMandRTCServers).
Thus, combining the two applications, assuming the server is properly
sized and the applications are within [known sizing
limits](https://jazz.net/wiki/bin/view/Deployment/CLMSizingStrategy60#Rational_Team_Concert_RTC_Exampl),
is completely viable and recommended. Sizing limits can be mitigated by
[CCM
clustering](https://jazz.net/wiki/bin/view/Deployment/ChangeAndConfigurationManagementClusteredEnvironmentVersion605).

The benefits of a single/combined server are:

-   Simplifies infrastructure and reduces administration and resource
    costs
-   Local configurations can be used to create affinity between model,
    code, and other related files (no global configuration needed)
-   Common local baseline can capture models and code together
-   Simplified and more robust capability to associate RMM change sets
    with EWM work items (most preconditions for work item delivery are
    only valid only for work items in the same CCM instance)
-   Single shared process template used in common between CCM and AM
    applications (don't need to keep separate AM and CCM process
    templates up to date and in sync)

In some cases, it may be desirable to deploy separate CCM and AM
application servers. Primary motivations would be:

-   Capacity planning given the amount of users in the CCM application
    and/or usage model require multiple CCM servers
-   Funding model for projects requires segmentation (e.g. not a shared,
    joint/commonly funded resource)
-   AM application servers can be [configured in one of two ways ("Model
    Management Server" or "Model and Code Management
    Server")](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_c_licensing_for_rmm.html).
    If the server is set up to only manage models (Model Management
    Server) this reduces the overall licenses cost compared to if RMM is
    set up to manage both models and code.
-   Isolate a department or subcontractor; separate confidential from
    non-confidential data - when OOTB permissions settings are
    insufficient

## Migration use cases from 6.x to 7.x

As with new deployments, ***the recommendation when migrating existing
deployments with RTC, RMM and/or Rhapsody Design Manager (RDM) 6.x to
EWM/RMM 7.x is to target a topology that combines both EWM/RMM on a
single server***, that is, the EWM application with AM extension.
However, there are different use cases to consider based on the
applications currently deployed, which may make separate servers the
more appealing choice, especially if a model migration would be needed.
Each of these have their benefits, challenges and data migration
considerations.

There is an additional use case, not covered in this article, for when
you have Rational Team Concert (RTC) only in the current 6.x environment
and want to add RMM when upgrading RTC to 7.0 or some time later. This
case and other planning considerations is covered in [Planning for the
upgrade or migration of Rhapsody Model Manager to version
7.0](https://www.ibm.com/support/pages/node/6223296).

|  |  |  |  |  |
|----|----|----|----|----|
| BLUE **Table 1: RDM/RMM migration use cases to combined or separate EWM/RMM servers** ENDCOLOR |  |  |  |  |
| \* Source Topology \* | \* EWM\[4\] ***(Combined)*** \* | \* EWM/CCM\[5\] / EWM/AM\[6\] ***(Separate)*** \* |  |  |
| RDM\[2\] (externally managed mode (EMM) via RTC SCM), RTC\[1\] | [UC-1](#UC_1_RDM_EMM_RTC_server_to_Combi) | N/A |  |  |
| RDM\[2\] (actively managed mode (AMM)), RTC\[1\] | [UC-2](#UC_2_RDM_AMM_RTC_server_to_Combi) | [UC-4](#UC_4_RDM_AMM_RTC_server_to_Separ) |  |  |
| RMM\[3\], RTC\[1\] | [UC-3](#UC_3_RMM_RTC_server_to_Combined) | [UC-5](#UC_5_RMM_RTC_server_to_Separate) |  |  |
| RMM\[3\] | [UC-6](#UC_6_RMM_server_to_Combined_CCM) | N/A |  |  |

BLUE *Table 1 footnotes* ENDCOLOR 1 *RTC 6.x* 1 *RDM 6.x* 1 *RMM 6.x* 1
*EWM 7.x (CCM with AM extension) - used for managing code and models* 1
*EWM/CCM 7.x (CCM only) - used for managing code only* 1 *EWM/AM 7.x
(CCM with AM extension) - used for managing models only*

There is one exception to the combined server recommendation and that is
for UC3 in which case we would recommend UC5, thus targeting separate
servers so as to avoid a complex migration process that requires
extensive guidance from IBM. A hybrid approach would be to manage old
models on the EWM/AM server and code/new models on the EWM/CCM server.

### UC-1: RDM EMM, RTC server to Combined CCM/AM server

This use case starts with an existing RDM 6.x server configured to
'externally managed mode' for managing its models with RTC 6.x and
migrates to a configuration that consists of an EWM 7.x server (CCM with
AM extension enabled).

ATTACHURL/UC1.png

#### High level steps [high-level-steps]

1 Upgrade RTC server to EWM 7.x with AM extension installed and in Model
and Code Management Server Deployment Mode. 1 Follow steps in [Migration
from Rational Rhapsody Design Manager to Rhapsody Model
Manager](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_c_import_dm_models_to_rmm.html)
to import existing RDM models into RMM.

#### Key benefits [key-benefits]

1 This use case will retain:

-   SCM history of models
-   Work item links to model artifacts 1 Able to import all OSLC links

#### Key challenges [key-challenges]

1 Contributions in a global configuration (GC) that formerly referenced
an RDM configuration will need to be updated to reference an EWM
configuration. 1 In order to re-create incoming OSLC links (AM/QM), you
will need to provide an editable QM configuration (i.e. a stream). 1
Consider adopting a [multiple stream
strategy](https://jazz.net/library/article/93878) for managing your RMM
models. 1 RDM models must be exported one stream at a time and imported
into RMM.

#### Best practices/recommendations [best-practicesrecommendations]

1 [Model Migration: Importing Rhapsody models into Rhapsody Model
Manager to migrate from Rhapsody Design
Manager](https://jazz.net/library/article/92282) 1 [Migration from
Rational Rhapsody Design Manager to Rhapsody Model
Manager](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_c_import_dm_models_to_rmm.html)
1 [Guidelines for working with multi-stream projects with Rhapsody Model
Manager](https://jazz.net/library/article/93878)

### UC-2: RDM AMM, RTC server to Combined CCM/AM server

This use case starts with an existing RDM 6.x server configured in
'actively managed mode' for managing its models and migrates to a
configuration that consists of a single EWM 7.x server (CCM with AM
extension enabled).

ATTACHURL/UC2.png

#### High level steps [high-level-steps-1]

1 Upgrade RTC server to EWM 7.x with AM extension installed and in Model
and Code Management Server Deployment Mode. 1 Follow steps in [Migration
from Rational Rhapsody Design Manager to Rhapsody Model
Manager](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_c_import_dm_models_to_rmm.html)
to import existing RDM models into RMM.

#### Key benefits [key-benefits-1]

1 Able to import all OSLC links

#### Key challenges [key-challenges-1]

1 SCM history of model artifacts is not retained 1 Contributions in a
global configuration (GC) that formerly referenced an RDM configuration
will need to be updated to reference an EWM configuration. 1 In order to
re-create incoming OSLC links (AM/CCM, AM/QM), you will need to provide
editable configurations (i.e. a stream). 1 Will need to publish all
views
([Diagrams](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_c_view_diagrams_in_rmm_web_interface.html),
[Tables,
Matrices](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_t_view_tables_in_rmm_web_interface.html))
1 Consider adopting a [multiple stream
strategy](https://jazz.net/library/article/93878) for managing your RMM
models.

#### Best practices/recommendations [best-practicesrecommendations-1]

1 [Model Migration: Importing Rhapsody models into Rhapsody Model
Manager to migrate from Rhapsody Design
Manager](https://jazz.net/library/article/92282) 1 [Migration from
Rational Rhapsody Design Manager to Rhapsody Model
Manager](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_c_import_dm_models_to_rmm.html)
1 [Guidelines for working with multi-stream projects with Rhapsody Model
Manager](https://jazz.net/library/article/93878)

### UC-3: RMM, RTC server to Combined CCM/AM server

This use case starts with an existing RMM 6.x server that
version-controlled its models and an RTC server for version-control of
code (and other non-modeling artifacts), work items, plans and builds
and migrates to a configuration that consists of an EWM 7.x server (CCM
with AM extension enabled).

While it is understandable why customers would want to pursue this use
case in order to gain the benefits of a single/combined server topology,
the complexity of a model migration may warrant the hybrid approach
discussed earlier. That is, to a two server topology so that no model
migration is needed, but use the EWM server for all new model work. It's
possible that the amount of data on the source RMM server is little
enough that a model migration with all the history and links intact is
not needed and thus the challenges described for this use case do not
apply or are of less concern thus making this a combined server option
more achievable.

ATTACHURL/UC3.png

#### High level steps [high-level-steps-2]

1 Upgrade RTC server to EWM 7.x with AM extension installed and in Model
and Code Management Server Deployment Mode. 1 Perform a one time
migration of model artifacts with history from RMM to EWM. This is not a
supported out of the box operation. Please contact your IBM
representative to arrange a discussion with IBM architects on how best
to accomplish this task. At a high level, this will involve the
following steps: 1 Use [distributed source
control](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.jazz.repository.web.admin.doc/topics/tenabledistribscm.html)
to deliver versioned model content in RMM to the EWM repository. 1
Re-populate the RMM index table for all project areas. 1 Will need to
publish all views
([Diagrams](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_c_view_diagrams_in_rmm_web_interface.html),
[Tables,
Matrices](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_t_view_tables_in_rmm_web_interface.html))

#### Key benefits [key-benefits-2]

1 This use case will retain:

-   SCM history of models
-   Work item links to model artifacts
-   Outgoing links (AM/RM)

#### Key challenges [key-challenges-2]

1 Merging of RMM and RTC servers is not supported; however, may be
accomplished manually with help from IBM Services (or development??) 1
Incoming OSLC links (AM/CCM, AM/QM) are not retained 1 RMM streams will
need to be recreated in EWM 1 Contributions in a global configuration
(GC) that formerly referenced an RMM configuration will need to be
updated to reference an EWM configuration. 1 Will need to publish all
views
([Diagrams](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_c_view_diagrams_in_rmm_web_interface.html),
[Tables,
Matrices](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_t_view_tables_in_rmm_web_interface.html))

#### Best practices/recommendations [best-practicesrecommendations-2]

1 Engage IBM for a guided discussion on the most appropriate option

### UC-4: RDM AMM, RTC server to Separate CCM/AM servers

This use case starts with an existing RDM 6.x server configured to
'actively managed mode' for managing its models and migrates to a
configuration that consists of an EWM/CCM 7.x server (CCM only), used
for managing code only and an EWM/AM 7.x server (CCM with AM extension),
used for managing models only.

ATTACHURL/UC4.png

#### High level steps [high-level-steps-3]

1 Upgrade RTC server to EWM 7.x without enabling AM extension 1 Deploy
an EWM/AM 7.x server and enable AM extension and in Model Management
Server Deployment Mode 1 Follow steps in [Migration from Rational
Rhapsody Design Manager to Rhapsody Model
Manager](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_c_import_dm_models_to_rmm.html)
to import existing RDM models into RMM on the EWM/AM server.

#### Key benefits [key-benefits-3]

1 Able to import all OSLC links

#### Key challenges [key-challenges-3]

1 SCM history of model artifacts is not retained 1 Contributions in a
global configuration (GC) that formerly referenced an RDM configuration
will need to be updated to reference an EWM configuration. 1 In order to
re-create incoming OSLC links (AM/CCM, AM/QM), you will need to provide
editable configurations (i.e. a stream). 1 Will need to publish all
views
([Diagrams](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_c_view_diagrams_in_rmm_web_interface.html),
[Tables,
Matrices](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_t_view_tables_in_rmm_web_interface.html))
1 Consider adopting a [multiple stream
strategy](https://jazz.net/library/article/93878) for managing your RMM
models. 1 The topology remains with two servers for managing CCM and AM
content rather than taking advantage of a combined CCM/AM server that
can manage code and models in one repository.

#### Best practices/recommendations [best-practicesrecommendations-3]

1 [Model Migration: Importing Rhapsody models into Rhapsody Model
Manager to migrate from Rhapsody Design
Manager](https://jazz.net/library/article/92282) 1 [Migration from
Rational Rhapsody Design Manager to Rhapsody Model
Manager](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.1/com.ibm.rational.rmm.overview.doc/topics/rhp_c_import_dm_models_to_rmm.html)
1 [Guidelines for working with multi-stream projects with Rhapsody Model
Manager](https://jazz.net/library/article/93878)

### UC-5: RMM, RTC server to Separate CCM/AM servers

This use case starts with an existing RMM 6.x server that
version-controlled its models and an RTC server for version-control of
code (and other non-modeling artifacts), work items, plans and builds
and migrates to a configuration that consists of an EWM/CCM 7.x server
(CCM only), used for managing code only and an EWM/AM 7.x server (CCM
with AM extension), used for managing models only.

ATTACHURL/UC5.png

#### High level steps [high-level-steps-4]

1 Upgrade RTC server to EWM 7.x without enabling AM extension 1 Upgrade
RMM server to EWM 7.x and enable AM extension and in Model Management
Server Deployment Mode 1 Follow steps in the interactive upgrade guide

#### Key benefits [key-benefits-4]

1 This use case will retain:

-   SCM history of models
-   Work item links to model artifacts
-   Outgoing links (AM/RM)
-   Incoming links (AM/CCM, AM/QM)
-   Global configuration contributions, e.g. RMM local configuration can
    continue to be used in existing GCs.

#### Key challenges [key-challenges-4]

1 The topology remains with two servers for managing CCM and AM content
rather than taking advantage of a combined CCM/AM server that can manage
code and models in one repository. 1 If RMM and RTC were on the same
server, they likely were installed in the same package group. If so, be
sure to see [Planning for the upgrade or migration of Rhapsody Model
Manager to version 7.0](https://www.ibm.com/support/pages/node/6223296)

#### Best practices/recommendations [best-practicesrecommendations-4]

1 Follow steps in the interactive upgrade guide

### UC-6: RMM server to Combined CCM/AM server

This use case starts with an existing RMM 6.x server that
version-controlled its models and migrates to a configuration that
consists of an EWM 7.x server (CCM with AM extension enabled).

ATTACHURL/UC6.png

#### High level steps [high-level-steps-5]

1 Upgrade RMM server to EWM 7.x and enable AM extension and in Model
Management Server Deployment Mode 1 Follow steps in the interactive
upgrade guide

#### Key benefits [key-benefits-5]

1 This use case will retain:

-   SCM history of models
-   Work item links to model artifacts
-   Outgoing links (AM/RM)
-   Incoming OSLC links (AM/CCM, AM/QM)
-   Global configuration contributions, e.g. RMM local configuration can
    continue to be used in existing GCs. 1 The EWM server will be able
    to manage both models and code.

#### Key challenges [key-challenges-5]

1 none at this time

#### Best practices/recommendations [best-practicesrecommendations-5]

1 Follow steps in the interactive upgrade guide.

META:FILEATTACHMENT{name="UC6.png" attachment="UC6.png" attr="h"
comment="" date="1595536103" path="UC6.png" size="20527" user="tfeeney"
version="2"} META:FILEATTACHMENT{name="UC5.png" attachment="UC5.png"
attr="h" comment="" date="1593698192" path="UC5.png" size="35926"
user="tfeeney" version="3"} META:FILEATTACHMENT{name="UC4.png"
attachment="UC4.png" attr="h" comment="" date="1595536083"
path="UC4.png" size="38284" user="tfeeney" version="3"}
META:FILEATTACHMENT{name="UC3.png" attachment="UC3.png" attr="h"
comment="" date="1593542628" path="UC3.png" size="28135" user="tfeeney"
version="1"} META:FILEATTACHMENT{name="UC2.png" attachment="UC2.png"
attr="h" comment="" date="1593542643" path="UC2.png" size="30461"
user="tfeeney" version="1"} META:FILEATTACHMENT{name="UC1.png"
attachment="UC1.png" attr="h" comment="" date="1593542663"
path="UC1.png" size="30410" user="tfeeney" version="1"}
