META:TOPICINFO{author="daviddl" date="1708005859" format="1.1"
version="1.177"} META:TOPICPARENT{name="WebHome"}

# Deployment Planning and Design DKGRAY Authors: Main.MichaelRowe, Main.TimFeeney, Main.VaughnRokosz, Main.PaulEllis, Main.ShubjitNaik, Main.RichardRakich Build basis: 7.0.3 ENDCOLOR [deployment-planning-and-design-dkgray-authors-main.michaelrowe-main.timfeeney-main.vaughnrokosz-main.paulellis-main.shubjitnaik-main.richardrakich-build-basis-7.0.3-endcolor]

TOC{title="Page contents"}

The planning and design of your new or evolving IBM Engineering
Lifecycle Management (ELM) environment requires understanding of your
existing and future business and technical needs. There likely are other
applications which will need to be integrated with ELM to provide
practitioners workflows and data flows needed for their productivity and
corporate / regulatory standards which must be met. This document will
focus on how you can build a technical deployment that meets your needs,
while being flexible enough to grow as your needs change.

## Gathering the basics

To begin with you should have detailed and documented understanding of
your current technical and operational environment. The goal is to
understand your organizational standards and capabilities which may
influence your deployment of ELM choices:

-   Current topology supporting engineering teams and its
    characteristics
    -   Infrastructure technology choices (e.g., OS, DB, identity
        management, etc.)
    -   Hosting (on prem, cloud based, etc.)
-   Software tool landscape
-   Availability and uptime requirements

Additional considerations and requirements, which could impact topology
flexibility include:

-   Typical ELM usage scenarios / patterns by job role and location
-   Planned usage model, growth projections, and performance
    requirements
-   Security, audit, and compliance requirements which may have impacts
    to your deployment topology, i.e., separating projects, users, or
    servers

A more detailed set of questions to consider can be found at [typical
questions](https://jazz.net/wiki/bin/view/Deployment/DeploymentPlanningTypicalQuestions).
These questions are not exhaustive; they are designed to provide
guidance in gathering the information which may impact your deployment
topology.

Key Links:

-   [Engineering Lifecycle Management Architecture
    Overview](https://jazz.net/wiki/bin/view/Deployment/CLMArchitectureOverview)
-   [ELM Sizing
    Strategy](https://jazz.net/wiki/bin/view/Deployment/PerformanceCLMSizingCenter)
-   [Blog Getting to a right sized Jazz
    environment](https://trfeeney.wordpress.com/2019/06/20/getting-to-a-right-sized-engineering-lifecycle-management-environment/)

## Define deployment topology

After you have defined your technical choices, usage requirements, and
growth projections, reviewing these
\[\[<https://jazz.net/wiki/bin/view/Deployment/StandardTopologiesOverview>\]\[standard
topologies\] will allow help identify patterns which are appropriate for
addressing your needs. A detailed assessment of matching your
requirements to these topologies can be provided by IBM or Business
Partner services teams. These topologies are designed to be customized
to meet your middleware, scale, availability, and other non-functional
requirements.

Deployment examples:

-   [Standard deployment topologies
    overview](https://jazz.net/wiki/bin/view/Deployment/StandardTopologiesOverview)
-   [IBM Jazz.net
    example](https://jazz.net/wiki/bin/view/Deployment/DeploymentExampleIBMJazznetEnvironment)
-   [IBM Hursely DevOps
    environment](https://jazz.net/wiki/bin/view/Deployment/DeploymentExampleIBMHursleyDevOps)

## Validating deployment

A key aspect of managing your ELM environment is having an appropriate
testing / staging environment, this environment should match your
production environment as closely as possible. You can use this
environment to:

-   Validate your topology choices
-   Develop training assets, and train new employees on ELM usage
-   Test application configuration changes before enabling in production
-   Execute performance stress tests
-   Perform test upgrades and migrations

Exercising this environment allows for upskilling your operational team,
while giving you baseline expectations for managing your production
deployment. Balancing the flexibility of your potential topology with
the operational support required to administer the environment is one
item to assess when establishing your test environment.

Key links:

-   [Planning your
    URIs](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=installation-planning-your-uris)
-   [Understanding Reverse
    Proxy](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=topology-reverse-proxy-servers-in-topologies)
-   [Reverse Proxies and Load Balancers in an IBM ELM
    Deployment](https://jazz.net/wiki/bin/view/Deployment/CompareProxyServers)
-   [Planning for multiple Jazz Application Server
    Instances](https://jazz.net/wiki/bin/view/Deployment/PlanForMultipleJazzAppInstances)

## Deploy to production and proactively monitor

After you have defined your requirements, established your projections,
customized your topology, and validated it in a test environment, its
time to deploy to production.

The process doesnt end there, you will need to monitor the environment
and adjust it to ensure that your enterprise can achieve the ongoing
benefits of utilizing ELM. A detailed article on what you should monitor
and how to respond to it can be found at the
[monitoring](https://jazz.net/wiki/bin/view/Deployment/DeploymentMonitoring)
article.

Key Links:

-   [Approaches to implementing high availability and disaster recovery
    for
    Jazz](https://jazz.net/wiki/bin/view/Deployment/ApproachesToImplementingHAAndDR)
-   [Jazz Team Server Authentication
    Explained](https://jazz.net/wiki/bin/view/Deployment/JTSAuthenticationExplained)
-   [Deployment
    Monitoring](https://jazz.net/wiki/bin/view/Deployment/DeploymentMonitoring)
-   [Performance sizing guides and
    datasheets](https://jazz.net/wiki/bin/view/Deployment/PerformanceDatasheetsAndSizingGuidelines)
-   [ELM Licensing
    Explained](https://jazz.net/wiki/bin/view/Deployment/DeploymentLicensingELM)
-   [Ranges and
    Limits](https://jazz.net/wiki/bin/view/Deployment/EnvelopesRangesAndLimits)

META:TOPICMOVED{by="sbeard" date="1367597914"
from="Deployment.DeploymentScenarios"
to="Deployment.DeploymentPlanningAndDesign"}
