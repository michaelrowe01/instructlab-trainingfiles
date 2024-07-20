META:TOPICINFO{author="michaelrowe" date="1709230059" format="1.1"
version="1.10"} META:TOPICPARENT{name="DeploymentPlanning"}

# Typical questions raised during a Technical Deployment Planning Workshop DKGRAY Authors: Main.MichaelRowe , Main.TimFeeney, Main.VaughnRokosz Build basis: N/A [typical-questions-raised-during-a-technical-deployment-planning-workshop-dkgray-authors-main.michaelrowe-main.timfeeney-main.vaughnrokosz-build-basis-na]

ENDCOLOR

TOC{title="Page contents"}

The following sample questions should be considered when beginning a new
ELM deployment or when evolving your existing deployment. We suggest
reviewing them with your IBM account team who can involve ELM deployment
SMEs as needed.

## Understanding your current environment

Note this is about your current software development lifecycle (SDLC)
environment, regardless of if it is already using IBMs Engineering
Lifecycle Management tools or not. Since your operational teams will be
supporting the ELM deployment too, the technology and tool choices that
you have made previously could have an impact on their ability to
support your new / upgraded environment. Having skilled resources who
understand the technology stack will improve your overall experience.

-   What is the current topology with detailed server specifications
    (cores, memory, disk, OS, etc.) of your SDLC?
-   What are the JVM settings for the ELM applications deployed? Are
    they sufficient and per IBM guidance?
-   What do the System Monitoring reports for a typical 24hr period
    indicate about the load and performance of the ELM deployment
    environment?

## Integration across software development lifecycle tool landscape

ELM does not stand alone in your environment. Most customers already
have some set of tools in place for managing different parts of their
end-to-end development process. ELM is designed to be integrated with
your existing tool suites via [OSLC (Open-Services for Lifecycle
Collaboration)](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=integrating-oslc-integrations),
[third party
tools](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=integrating-engineering-integration-hub),
and custom integrations via a rich set of [public
APIs](https://jazz.net/wiki/bin/view/Deployment/CLMProductAPILanding).
As such, take an inventory of those products and integrations:

1.  Which ELM products have you already deployed, if any?
2.  What other IBM tools/versions will be / are integrated into your ELM
    environment?
3.  What 3rd party tools/versions will be / are integrated into your ELM
    environment?
4.  What open-source tools/versions will be / are integrated into your
    ELM environment?
5.  What custom tools and scripts will be / are integrated into your ELM
    environment?
    1.  If using EWM, what Eclipse/Visual Studio clients do you
        integrate with?
    2.  What difficulties do you experience keeping them in sync with a
        deployed/supported version of EWM/ELM?
    3.  Do you have or need a mixed client version environment (n-1
        compatibility)?

## Current deployment topology and characteristics

When you are switching between releases of ELM or adding new ELM
applications to your current deployment, you should have a good
understanding of your environment. This understanding may provide you
with insights as to where you can make changes to configuration, and
where you may need to add capacity.

You should also have current topology diagrams of your existing
development, staging and production environments. Ideally, your staging
environments, at minimum, should mirror your production environment
topology and sizing. Doing so allows you to validate environment changes
prior to modifying your production environment.

1.  Which standard topology is your topology closest to? see [Standard
    deployment topologies overview: Recommended and alternate
    topologies](https://jazz.net/wiki/bin/view/Deployment/StandardTopologiesOverview#RecommendedAndAlternateTopologies).
2.  How many instances do you have of each ELM application?
3.  Are you using a Reverse Proxy server? This is highly recommended for
    any enterprise deployment.
4.  Do you have a load balancer?
5.  Do you have a content caching proxy server setup for remote sites or
    your EWM build farm?
6.  What is the network bandwidth for each site?
    1.  Rule of thumb latency between servers 1-5ms, \<50ms to license
        server, server to client \<200ms 90 of time. See - [Impact of
        Network
        Latency](https://jazz.net/wiki/bin/view/Deployment/ImpactOfNetworkLatency).
7.  What other applications are running on the same server as the ELM
    applications?
8.  Do you have separate environments for Development, Staging and
    Production? How are they the same or different?

## Infrastructure technology choices

If you are creating a new ELM environment some of these choices should
be made now. If you are upgrading your environment, then you need to
validate if your prior choices are still appropriate and adjust
appropriately.

1.  How many cores for each server?
2.  How much RAM for each server?
3.  Are your servers virtual? see [Principles of good
    virtualization](https://jazz.net/wiki/bin/view/Deployment/PrinciplesOfGoodVirtualization)
    1.  What is your hypervisor technology?
    2.  What is affinity/entitlement for the VM resources? Are the CPU,
        memory, and network
        1.  Recommend having anti-affinity rules in place so no two
            servers (VM) are on same physical server else recovery is
            more difficult/complex
    3.  What are the overcommitment rules in place for the VM resources?
        1.  memory should never be overcommitted a.. Do the allocated
            CPUs for each VM correspond to an actual physical CPU?
4.  Which operating system / platform are you using for the application
    tier (servers hosting your ELM applications)?
5.  What browser(s) do you use? Are you on the latest Extended Support
    Release (ESR) of the browser?
6.  Which database and version are you using for ELM?
    1.  How long have you been using your ELM database? b. How large is
        your ELM database?
7.  Which application server edition/version are you using? [why
    liberty](https://jazz.net/wiki/bin/view/Deployment/LibertyVersusWASFullProfileForCLM).
    Note since the release of ELM 7.0.3, you will be required to move to
    WebSphere Liberty. What are the JVM heap min/max/nursery settings
    for each application server?
8.  What storage type/technology do you use? While ideal you should use
    SSD for any real-time database storage, this may not be an option
    for all customers. If you are not using SSD you may need to adjust
    caching.

## User and data scale needs and projections

Planning the rollout of your teams, across applications, roles, and
geographies, may have a direct impact on how you size your environment.
Make sure that you understand the steady state and peak demands of your
servers. Think about how your user ramp up will happen over time,
planning for capacity to be available as needed. This capacity sizing
should be able to address the peak requirements with acceptable
performance.

1.  What is the current/planned number of registered users, broken down
    by role and geography?
2.  What is the current/planned number of concurrent users, broken down
    by role and geography?
3.  What is the timeline/ramp up for the current and future state
    deployment? Consider two things:
    -   Youll need more CPUs as the number of concurrent users increases
        (or if you run automation that
    -   Youll need more memory as the amount of data increases.

## Understand ELM configuration and typical usage scenarios/patterns by role

ELM is a set of applications, each with their own unique requirements
and behaviors which may impact performance and scale. These application
[limits](https://jazz.net/wiki/bin/view/Deployment/EnvelopesRangesAndLimits)
can be impacted by how you have configured various processes. Revisiting
these questions periodically will also allow you to proactively adjust
your topology and other application settings. As such, you should
understand the following:

1.  In cases of multiple ELM application servers of a given kind (e.g.
    multiple CCM servers):
    1.  How are projects assigned to a given server?
    2.  Are there cross-server relationships between these projects?
2.  What traceability relationships exist between the application
    artifacts?
3.  Is EWM distributed SCM in use?
4.  Is EWM process sharing in use?
5.  What is your typical release pattern/schedule?
6.  Have you implemented a continuous integration practice?
7.  What is your volume of builds per day? week?
8.  Have you implemented a continuous deployment practice?
9.  What is your volume of deployments per day? week?
10. What are the typical application usage patterns by each ELM
    application and each role?

## Top end user issues and concerns

Your usage patterns may change after your initial deployment of ELM.
Understanding your users behaviors and concerns will allow you to stay
ahead of some issues. As we discussed earlier in this article, there are
various changes you can make in technologies, deployment topologies, and
process templates which may address your concerns. You should
periodically review these concerns and work with your IBM account team
to ensure your users are getting the most out of your ELM deployment.

1.  What performance concerns do you have currently?
2.  What are the primary end user issues and concerns now? Have you
    logged Support cases?
3.  What are the primary application administration issues and concerns
    now? Have you logged Support cases?

## High Availability and Disaster Recovery

While business operations may be considered the highest priority for any
infrastructure, building an appropriate plan for availability and
disaster recovery ensures that if unforeseen events do occur, your
engineering teams can be productive as quickly as possible.

We break this section up into two parts, first is the background, which
helps you think through the business requirement for uptime and
recovery. The second section provides a set of considerations for
approaching your recovery, should it be necessary. Throughout both
sections we will also share some best practices.

### Background

1.  What is your required level of availability for your ELM environment
    during supported hours? See [Availability - /"number of
    nines/"](https://jazz.net/wiki/bin/view/Deployment/HighAvailability#AvailabilityNumberOfNines).
    Typically, development environments should be 99.9.
2.  What are your supported business operating hours for your ELM
    environment?
3.  What is your current level of availability? See [Measuring
    Availability](https://jazz.net/wiki/bin/view/Deployment/HighAvailability#MeasuringAvailability).
4.  Do you have planned outages? How often/long? What do you do during
    those times?
5.  What is your requirement for Mean Time to Recovery (MTTR) for high
    availability scenarios? See [Mean Time to Recovery
    (MTTR).](https://jazz.net/wiki/bin/view/Deployment/HighAvailability#MeanTimetoRecovery)
    What is your typical/actual MTTR?
    1.  1 hour or more is reasonable. Anything less will be difficult to
        achieve
6.  What is your required Recovery Point Objective (RPO) for disaster
    recovery scenarios? See [Recovery point objective
    (RPO)](https://jazz.net/wiki/bin/view/Deployment/DisasterRecovery#RecoveryPointObjective).
    What is your typical/actual recovery point?
    1.  24 hours is the standard for most organizations. Less is very
        aggressive and difficult to achieve.
7.  What is your required Recovery Time Objective (RTO) for disaster
    recovery scenarios? See [Recovery time objective
    (RTO)](https://jazz.net/wiki/bin/view/Deployment/DisasterRecovery#RecoveryTimeObjective).
    What is your typical/actual recovery time?
    1.  2 days is reasonable

### Approach

1.  What is your strategy for backup?
    1.  What do you back-up? see [ELM
        Backup](https://jazz.net/wiki/bin/view/Deployment/BackupCLM)
        (databases, configuration files, proxy, virtual servers)
    2.  How often to you back-up your production environment?
    3.  How often do you test your approach to back-up (and restore)?
        How?
2.  Do you perform root cause analysis of your failures and what are
    they telling you?
3.  How are failures detected? How are you notified of your failures?
    How are they triaged?
4.  Do you monitor for failures? Which levels?
5.  How long do you try to recover from an HA failure before you decide
    to treat it as a DR failure?
6.  What approach and technology do you use to support application tier
    high availability?
7.  What approach and technology do you use to support application tier
    disaster recovery?
8.  How often do you test your approach to high availability? How? see
    [Chaos Monkey](https://netflix.github.io/chaosmonkey/).
9.  How often do you test your approach to disaster recovery? How?
10. Do you have a backup for every person involved in the process from
    failure to recovery?
11. Do you have the author, or another individual, test the procedures?
12. How do you verify that the environment has recovered properly?

Refer to [failure
scenarios](https://jazz.net/wiki/bin/view/Deployment/ApproachesToImplementingHAAndDR#Failure_scenarios_with_general_a)
for information on types of failures and reasonable recovery scenarios.

## Capacity planning, performance, and monitoring

To address capacity requirements and changes over time we recommend
taking a three-step approach: Measure -\> Analyze -\> Act, rinse, and
repeat. To enter this cycle, you initially plan on what your expected
performance expectations are, along with the infrastructure to support
it. Many of the prior sections of this document should help you pull
that plan together.

-   The Measure-\>Analyze-\>Act cycle: (see
    [Monitoring](https://jazz.net/wiki/bin/view/Deployment/DeploymentMonitoring))
    -   Monitoring a system provides insight into trends and behavior
        based on real production data
    -   Understanding what monitoring data tells you can enable capacity
        planning
    -   Performance capability and problems can be best analyzed by
        understanding the normal behavior of a system as documented
        through monitoring data
-   Different approaches to monitoring:
    -   Tactical or short-term monitoring, to alert on problems and to
        assist in problem resolution. Strategic or long-term monitoring,
        to track growth trends in the deployment to help with capacity
        planning

<!-- -->

-   What is being monitored today?
    -   Application, application server, system/OS, VM/LPAR, DB,
        Network, availability, end-user performance benchmarks, end to
        end user transaction performance, users/license, reverse proxy,
        caching proxy
-   What additional monitoring do you need?
    -   Application, application server, system/OS, VM/LPAR, DB,
        Network, availability, end-user performance benchmarks, end to
        end user transaction performance, users/license, reverse proxy,
        caching proxy

<!-- -->

-   How are you monitoring, and at what tiers?
    -   IBM tools, homegrown, 3rd-party?

<!-- -->

-   Why you monitor the data? Potential usage includes:
    -   Tactical (monitoring \> triggers)
        -   Detect issues early
            -   Are there triggers which cause alarms, e.g. JVM \> X GB,
                CPU \> 90, end-user ping \> 10sec, etc.?
        -   Get data from live systems to assist in problem
            determination and resolution
        -   Provide historical data to evaluate effectiveness of system
            changes
    -   Strategic (monitoring \> planning)
        -   Dashboard design and strategy
        -   Reporting design and strategy
        -   Data storage and retention strategy
        -   Trending and forecasting
    -   Insights for other teams across the enterprise:
        -   Capacity planning (servers)
        -   Finance for licensing and other costs
        -   Team Admins on feature usage

<!-- -->

-   Minimum things to monitor
    -   JVM size
    -   CPU
    -   license usage
    -   DB size
    -   data transferred to and from the app server and DB server
    -   Uptime
-   Are there any features missing from ELM tools regarding monitoring?

## Security, audit, and compliance

Another set of considerations to assess when planning your environment
is related to regulatory issues which may impact the location, access
methods, and reporting requirements. The following questions may have a
material impact to how you configure your deployment, by defining
location of servers, which project areas can be co-located on a specific
server, how you partition your databases, etc.

-   What security export regulations must you comply with?
    -   local, regional, national, international
    -   people, facility, corporate
    -   database, application, web tiers
-   Are there multiple levels of security to work within e.g.
    unclassified, restricted, confidential, secret, top secret?
-   What confidentiality standards must you comply with?
    -   teams within organization, between organization and with
        customer, between partners/subcontractors
    -   people, facility, corporate
    -   database, application, web tiers
-   Is there a need for multi-tenancy, e.g. host environment for
    multiple customers/contractors and need to segment them?
-   Are there any needs to restrict what a given role, project,
    application, etc. has access to?
-   Do you have any corporate, national, etc. audit requirements (e.g.
    UK FSA, SOX)? What impact does that have on data retention and
    access control?
-   Are there any other standards that impact the construction and use
    of your development environment?
-   What remote access/VPN/VDI requirements do you have?
-   Do you permit Bring Your Own Device (BYOD) or mobile devices? What
    standards/policies govern their use?
-   Do you have any corporate single sign-on (SSO) standards and
    preferred technologies?
-   What web tier security do you have in place?
-   Do you do SSL offloading at the web tier (HTTPS outside data center
    and HTTP inside)?

## Administration, configuring, tuning

Now that you have your topology deployed (or planned), monitoring in
place, and availability plan structured, make sure you have a good
administration process in place. Things you may wish to consider as you
integrate ELM administration into your larger admin process include:

-   Do you use your corporate help desk for capturing tickets against
    your environment?
-   Do you use EWM for your own infrastructure/tools team planning?
-   What are the administrative responsibilities of the ELM tools team?
-   What are the administrative responsibilities of the infrastructure
    team?
-   What are the administrative responsibilities of the project teams?
-   What are the support hours for the ELM tools team vs infrastructure
    team?
-   Do you have a regularly scheduled maintenance window?
-   What administrative procedures do you have documented in detail
    (e.g. backup, upgrade, maintenance)? How often are they reviewed or
    tested? Can they be performed by multiple team members?
-   Do you have a central knowledgebase (e.g. wiki) for capturing and
    publishing your procedures?
-   Where do your admins/end users go for documentation (external to IBM
    and/or internal to their site)?
-   Do you version control any part of your procedures or automation
    scripts?
-   For the responsibilities of the ELM tools team, do you have at least
    two administrators capable of performing each responsibility?
-   What approval process is required to make changes to the project,
    application, server, etc.?
-   What training do you provide? How? When?
-   What additional administrative or application skills does your team
    need?

##### Related topics: [Deployment Workshops and Reviews](DeploymentPlanning#Deployment_workshops_and_reviews), [Deployment web home](DeploymentWebHome) [related-topics-deployment-workshops-and-reviews-deployment-web-home]
