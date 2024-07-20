META:TOPICINFO{author="lekandrade" date="1702491057" format="1.1"
reprev="1.37" version="1.37"}
META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Planning for multiple Jazz application server instances [planning-for-multiple-jazz-application-server-instances]

DKGRAY Authors: Main.TimFeeney, Main.RalphSchoon, Main.MarianneHollier,
Main.DennisSchultz, Main.StevenBeard Build basis: The IBM solution for
Engineering Lifecycle Management (ELM) and the IBM solution for systems
and software engineering (Rhapsody) ENDCOLOR

TOC{title="Page contents"}

The Jazz architecture allows for multiple instances of specific
application servers, such as the Change and Configuration Management
(CCM) application (Engineering Workflow Management), Quality Management
(QM) application (Engineering Test Management) and Requirements
Management (RM) application (Engineering Requirements Management DOORS
Next). These application servers are registered to a common Jazz Team
Server (JTS) to form a ELM Instance. The architecture further allows
multiple ELM Instances to be formed. You should be aware of the
tradeoffs and architectural considerations when multiple instances are
needed in order to scale to support your user population/load.

The strategies described herein pre-date the availability of application
clustering, which, as of release 7.0, is available with the EWM, ETM,
and Architecture Management (AM) applications. Clustering provides for
increased user scalability. Multiple instances of an application may
still be needed in cases were clustering isn't available or for
increased data scale.

## Multiple Jazz Team Server considerations

It is possible to use multiple JTSes each with their own set of
registered applications (each referred to as ELM Instance).

It is possible to distribute load to separate ELM instances e.g. one ELM
instance per project or per department

Motivations

-   Maximize scalability
-   Prior to 5.0, JTS/RM shared storage leading to potential overtaxing
    of JTS due to RMs Jena queries thus limiting number of concurrent
    users a single JTS/RM could handle; in such cases, multiple JTS are
    required to add another RM.

Pro:

-   Useful if projects are independent e.g.: separating subcontractors,
    compliance

Con

-   Administrative cost increasing numbers need automation for
    deployment, administration and upgrade
-   More challenging to get a comprehensive view; if desired, would
    require Insight to report across multiple JTS

The image below shows multiple JTS and their registered applications.
The reporting is working a cross all these ELM instances.

### Functional differences to be aware when multiple JTS exist

Reporting

-   RRDI reports only on data for applications associated to one JTS;
    multiple JTS/ELM Instances require JRS (Jazz Reporting Services) or
    Insight to report across JTS boundaries

Linking between Artifacts

-   Applications are registered to one JTS and it is possible to link
    artifacts between applications
-   Multiple JTS require manual creation of friends relationships to
    connect artifacts
-   Only ELM link types are available across application boundaries
    limiting choices of link types between artifacts

**Cross-repository + cross-project link types**

| Link Name/Backlink Name                             | Remote provider type |
|:----------------------------------------------------|:---------------------|
| Related Change Request/Related Change Request       | CM                   |
| Affects Plan Item/Affected By Defect                | CM                   |
| Tracks/Contributes To                               | CM (CCM only)        |
| Tracks Change Set                                   | CM (CCM only)        |
| Blocks Execution Record/Blocked By Change Request   | QM                   |
| Affects Execution Result/Affected By Change Request | QM                   |
| Tested By Test Case/Tests Change Request            | QM                   |
| Related Test Case/Related Change Request            | QM                   |
| Related Execution Record/Related Change Request     | QM                   |
| Related Test Plan/Related Change Request            | QM                   |
| Implements Requirement/Implemented By               | RM                   |
| Affects Requirement/Affected By                     | RM                   |
| Tracks Requirement/Tracked By                       | RM                   |
| Elaborated By                                       | RM                   |

**Same project + Cross-project/Same repo link types**

| Link Name                  | Provider |
|:---------------------------|:---------|
| Related/Related            | CCM      |
| Duplicate Of/Duplicated By | CCM      |
| Copies/Copied From         | CCM      |
| Related Artifact/NA        | CCM      |
| Attachment/NA              | CCM      |
| Blocks/Depends On          | CCM      |
| Parent/Child               | EWM      |
| Predecessor/Successor      | CCM      |
| Resolves/Resolved By       | CCM      |
| Change Set/NA              | CCM      |
| Mentions/Mentioned By      | CCM      |
| Time Sheet Entry           | CCM      |

Lifecycle Projects and ELM Instances

-   Cannot create lifecycle projects that include artifact containers
    registered with a different JTS

Dashboards live within one JTS

-   Can show widgets from applications with friends relationship

## Multiple Jazz application server considerations

You can also deploy multiple instances of a Jazz application, such as
the EWM application. If you deploy multiple instances of the same
application in the same application server, you must give each instance
a separate context root. For example, the context roots for two EWM
instances could be ccm1 and ccm2. To connect multiple instances of the
EWM application to a shared Jazz Team Server, the instances must all be
authenticated from the same authentication realm and thus share the same
set of users. In any deployment, the licenses are managed by Jazz Team
Server. For more information about licenses, see [Client access license
management
overview](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=c_license_mgmt_over.html&scope=null).

The image below shows multiple ELM applications registered to one JTS:

When you choose a topology for your deployment, carefully consider both
the present and future needs of your team. While it is possible to move
applications to a different application server later, this change
requires the use of a proxy server to maintain links to that
application.

Motivations

-   Capacity planning given the amount of users in the application
    instance and or usage model require multiple application servers
-   Funding model for projects requires segmentation (e.g. not a shared,
    joint/commonly funded resource)
-   Isolate a department or subcontractor; separate confidential from
    non-confidential data - when OOTB permissions settings are
    insufficient

Pros

-   Balance load on applications
-   Increased scalability

Cons

-   Side effects (functional differences)
-   Increased reporting complexity

[Multiple EWM Applications From a User
Perspective](MultipleCCMAppsUserPerspective) describes how this would
look like from a user perspective.

[Multiple EWM Applications Best Practices](MultipleCCMAppsBestPractices)
describes some best practices to be considered when working in this
environment.

### Functional differences to be aware when multiple instances of Jazz Applications exist

Reporting

-   JRS supports single or multiple DW sources thus supporting multiple
    JTS scenario. It can also handle reports that need to cross
    application boundaries.

Linking between Artifacts

-   Applications are all registered to one JTS and it is possible to
    link artifacts between applications
-   Only ELM link types available across application boundaries limiting
    choices of link types between artifacts

Lifecycle Projects and ELM Instances

-   Projects in all applications can take part in lifecycle projects
-   Lifecycle Project templates don't have means to distinguish between
    multiple registered application instances of the same type, which
    might require to manually add projects to the lifecycle project

### Installation considerations when deploying multiple instances of a Jazz application

Since each Jazz application instance must have a unique context root,
when installing multiple instances of an application, do so from the
[command
line](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.0/com.ibm.jazz.install.doc/topics/t_command-line_installation.html)
and follow the instructions to [Choosing a different context root than
default](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.0/com.ibm.jazz.install.doc/topics/t_choose_different_context_root.html)

## Multiple Change and Configuration Management application considerations

### Functional differences to be aware of when multiple EWM instances exist

#### Work Items

1.  Work Items can be created in any EWM repository and linked to any
    other work item in any other repository
    -   Selection dialog allows you to choose from repositories with a
        friends relationship to find or create work items
    -   The only link relationships between work items in different EWM
        repositories are Related Change Request and Tracks
    -   To link work items, repositories need to be Friends
        -   Automatic when registered to the same JTS
        -   Set manually between applications in different ELM Instances
2.  Copying/moving of Work Items to another Project Area is only
    possible within the same EWM repository (see
    [169824](https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.viewWorkItem&id=169824))
3.  The Eclipse current work item functionality doesnt work when the
    work item is in another repository

#### Planning

1.  Cross Project Planning
    -   Cross project plans allow one relationship type to show as a
        tree view and roll up plan data
    -   Must use the Tracks relationship to work across projects and
        repositories
    -   Parent/child relationships are not supported across EWM
        repositories
    -   Cross project plans show only the tracked work item and its
        rolled up plan data, parent child relationships underneath are
        hidden
2.  Work allocation
    -   Users working in multiple EWMs will need to maintain their work
        allocation and scheduled absences in each EWM where they have
        assigned work. Correct and complete allocation and time off
        entry ensures proper load and progress calculations in plan
        views.

#### SCM

1.  Versioning code across EWM applications requires [distributed
    SCM](https://jazz.net/library/article/535/) to replicate changes
    between EWM repositories
2.  Distributed SCM creates identical copies of change histories, change
    sets and changes made
    -   Only the current baseline is migrated to the target repository
    -   Select incoming baselines from the remote stream and accept the
        baselines to replicate them, if needed
    -   Work Item links on change sets are replicated with the change
        set, but the work item only links back to the original change
        set
3.  To be compatible between repositories Distributed SCM requires both
    repositories to have the same metadata model.
4.  Compatibility with previous versions is not supported in a
    distributed SCM setup. This means that there is no guarantee that
    distributed SCM works between different versions, as there could be
    comprehensive changes in how SCM manages its data between versions.
5.  It is recommended that all servers involved in a distributed SCM
    setup be at the same version level.
6.  Snapshots are local to a repository
    -   No snapshot across multiple EWM repositories
    -   Snapshots cant be transferred, selecting a snapshot owner in a
        different repository not possible
    -   Snapshots are not replicated
7.  It is possible to associate work items to change sets, regardless of
    the repository either side lives in
    -   Navigation to work items works as usual, once connection is made
    -   The link created using associate work item only works within one
        repository
    -   When associating a change set to a work item in another EWM
        repository, use drag and drop or the associate change request
        gesture to make the association rather than associate work item
8.  Preconditions
    -   Most out of the box deliver preconditions can only be satisfied
        by work item links. Some examples:
        -   The precondition requiring a change set to be associated to
            an approved work item only works for work items in same EWM
            repository as change set
        -   The precondition requiring a work item associated to the
            change set with its additional options only works for work
            items in same EWM repository as change set
        -   The Precondition requiring an associated work item to match
            a query only works for work items in same EWM repository as
            change set
9.  Other SCM capabilities
    -   The capability to locate change sets currently only works with
        local change set/work item relationships of the type associate
        work item

The image below shows distributed SCM across multiple EWM appliactions
where the client is connected to multiple EWM applications and can work
against multiple repositories:

#### Build

1.  The "Included In Build" and "Reported Against Build" links in a
    Build Result can only refer to work items in the same EWM. These
    link types use item links, not URI links, so the references are to
    same repository only (see
    [222103](https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.viewWorkItem&id=222103)).

## Multiple Quality Management application considerations

1.  ETM is intended to reuse as many test assets as possible, to reduce
    maintenance and improve productivity of the test teams.
    Specifically:
    -   Test cases
    -   Test scripts
    -   Test suites
    -   Keywords
    -   Test data
    -   Test environments platforms and parameters
    -   Test schedules timelines and iterations
    -   Quality objectives, entry criteria, exit criteria
    -   Categories and custom attributes
2.  This reuse is by reference and only within a ETM project area
3.  Unlike EWM, there is no notion of creating associations between
    assets in different ETM project areas, let alone ETM instances
4.  Copying any of the assets creates a separate, editable copy, meaning
    for the same asset, you have to maintain the original and the copies
    in two (or more) places
5.  Copying should be kept to a minimum to maximize reuse within
    projects on the same ETM instance

### Functional differences to be aware of when multiple ETM instances exist

1.  Duplicating test artifacts
    -   The Duplicate capability enables you to replicate a single test
        artifact or an entire collection of artifacts
    -   Only supports duplication within the source project area or to a
        project area on the same application instance.
    -   You cannot use Duplicate to copy artifacts to a project area on
        another server.
    -   However there is an as-is command line [RQM Copy
        Utility](https://jazz.net/wiki/bin/view/Main/RQMCopyUtility)
        allowing copying of artifacts across servers.
2.  Built-in reporting and IBM Reporting for Developer Intelligence
    reports are limited in scope to one application server.

## Multiple Requirements Management application considerations

As of 5.0, multiple DOORS Next instances per JTS is supported. In a 5.0
configuration with multiple DOORS Next instances, all JTS and DOORS Next
servers must be at 5.0, that is, mixing 4.0.x and 5.0 DOORS Next server
versions is not supported

### Functional differences to be aware of when multiple DOORS Next instances exist

1.  Linking of DOORS Next artifacts between DOORS Next instances is
    supported in 6.0.6 for configuration management enabled projects;
    otherwise, the only supported link type is OSLC References.
2.  Link constraints are not supported for cross-server linking
3.  When viewing the details of a change set, only DOORS Next links
    sourced on the local server are shown.
4.  Embedding of artifacts is only supported on the same DOORS Next
    instance
5.  Glossary terms can only be referenced between components on the same
    server
6.  DOORS Next views can be constructed that include links to artifacts
    from local and remote DOORS Next instances. The same performance
    considerations and caveats apply as when including information from
    EWM and ETM.
7.  When filtering a view based on artifact attributes on the target
    side of the link, this can only be performed on artifacts within the
    same server. When the artifact on the target side of the link is on
    another server, you are limited to filtering on the existence (or
    non-existence) of the link.
8.  Quick Search is limited to projects on the local DOORS Next instance
9.  For configuration management enabled projects:
    -   Types can only be imported from components on the same server
        (instead use ReqIF to update types between servers)
    -   Component templates are not shared across servers (You can
        download a project template from one server and upload it to
        another server)

## Strategies for distributing projects across application servers

IBM clients currently fall into three distinct groups when determining
their ELM application expansion approach or how to distribute projects
across their application instances:

-   Shopping Bag
-   Moving Van
-   Field of Dreams

### Shopping Bag

Overview create one to many servers and fill up the servers with similar
types of assets. If a server gets filled, then another server is
on-boarded. The 'shopping bag' reference comes from the idea that when
going to the market/grocery store, typically like things are put in the
same bag, e.g. canned foods, boxed goods, cleaning solutions, frozen
foods, tend to be kept separate from one another.

Projects organized/distributed by: Domain, Segment, Development Type,
etc.

Benefits: scientific/proactive approach since it requires monitoring,
logical since you are combining similar assets

### Moving Van

Overview an estimate is made at the beginning of the ELM deployment and
a server is sized, with the anticipation that all data will fit and
performance will continue to be good, no matter how ELM is used. The
'moving van' reference comes from the idea that when moving
goods/furnishings from one's home, you typically try to get the largest
moving van/truck possible to hold all your things with some room to
spare and all things are loaded together.

Projects organized by: ad hoc, smorgasbord (a large mixture of many
different things)

Benefits estimates are done once and that is all until performance
issues start

### Field of Dreams

Overview a hybrid of the other two approaches, plan for logical
groupings of projects across multiple servers sizing each to allow for
spare capacity, include monitoring to know when additional servers are
needed.

Projects organized/distributed by: Domain, Segment, Development Type,
etc.

Benefits logical organization combined with one time estimation

## Factors affecting Jazz application architecture

### EWM Application Architectural Considerations

1.  Organizations which require rolled up reports leveraging OOTB EWM
    reporting should reside in the same EWM.
2.  Organizations may leverage Insight to report across projects
    residing in separate EWMs.
3.  Organizations which require hierarchical work item relationships
    across project areas must reside in the same EWM.
4.  Consider separating areas which anticipate significant project area
    growth into different EWMs
5.  Logically organize EWMs to limit sprawl
6.  Minimize use of distributed SCM where possible and group project
    areas which share code base in the same EWM.
7.  Choose an approach that will provide the most flexibility and
    scalability

### ETM Application Architectural Considerations

Separating artifacts into multiple project areas provides the ability to
completely restrict access between testing teams. There is a place for
this with highly regulated teams, secure projects and so on. If you have
test artifacts that are highly sensitive and should only be viewable by
a small number of people, those test assets should be contained within a
separate ETM project area, regardless of the ETM server it is housed on.
But also consider that you will be trading reuse and commonality for
that independence.

We recommend that you partition your ETM project areas to take advantage
of the reuse capabilities by:

1.  Determine which of your systems are highly integrated and keep those
    test artifacts in a single project area. We recommend that you use a
    single ETM project area for all test artifacts that are pertinent to
    a given application domain. For example, all testing artifacts that
    are germane to testing System A and its related systems would be in
    a single ETM project area. Moving to this system-centric model will
    enable you to reuse system-centric test environments, test cases,
    test scripts, etc. across releases and projects. Collecting and
    managing artifacts by sub-system can be achieved with the use of
    Categories. You can create a standard set of shared (public) filters
    in order to provide views of artifacts at the sub-system level. This
    enables you to keep system related artifacts together in one project
    while still enabling you to filter and report at the sub-system
    level.
2.  Use team areas to separate test artifacts and govern security and
    permissions by role. Team areas enable you to set permissions on
    artifacts such that one team may have full permission over their
    artifacts but have only read permission to another teams artifacts.
    Again, this may be an option that enables you to manage permissions
    at the sub-system level yet share common assets across all
    sub-systems.
3.  Understand how non-functional requirements the most reusable
    requirements (usability, reliability, performance and
    supportability) and therefore the highly-reusable test cases
    associated with those non-functional requirements will be reused
    across multiple ETM project areas. Consider creating an enterprise
    catalog of non-functional tests from which you can derive
    system-specific non-functional tests.

If you believe you will need to copy test artifacts from one project
area to another, create those project areas on the same ETM server to
enable ease of copying. Copying from one ETM server to another ETM
server is not currently supported in the web interface and must be
accomplished via the copy utility.

In addition, if you believe you will want to report across project
areas, house those project areas on the same ETM server. IBM Insight
must be used for reports the cross ETM servers.

### DOORS Next Application Architectural Considerations

1.  Organize projects on DOORS Next instances along some common
    affinity, like with like, e.g. common domains, systems.
2.  Projects should share a common project template and to have a
    common/unified type system.
    -   Create a Primary Type System project from the template; leave
        unpopulated
    -   Create and populate multiple projects from the same template
    -   As changes to types occur, update the Primary Type System
        project then import updates to populated projects to keep types
        in sync
    -   Templates do not span DOORS Next instance boundaries, thus the
        recommendation to organize projects by affinity
3.  Projects requiring linking of artifacts using Built-in or Custom
    link types must be on same DOORS Next instance. Linking artifacts to
    projects across servers must be by Reference type. This restriction
    is removed in 6.0.6 for configuration management-enabled projects.

## When to add additional Jazz application servers

The decision to add additional ELM Instances or Jazz application servers
is dependent upon the following:

-   Monitor 5 key factors
    -   transaction of data between servers
    -   growth of the database
    -   license usage (concurrent usage & usage model)
    -   JVM memory, heap, threads, etc.
    -   CPU resources
-   Analyze and extrapolate trends from the collected data
    -   compare to published sizing/ranges data
-   Decide and implement new Jazz application server(s) as needed
-   See [Jazz Deployment
    Monitoring](https://jazz.net/wiki/bin/view/Deployment/DeploymentMonitoring)

### Typical number of users supported per application instance

It is very difficult to pinpoint exactly how many users can be supported
by a single instance of EWM or ETM. There are a number of factors to
consider such as the number of active users and what those users are
doing.

It is not all that helpful to look at the total number of registered
users. The number of actual concurrent users will typically be far lower
than the total number of registered users. Some anecdotal data from
internal IBM systems has indicated that only about 1 of registered users
are active on average with peak usage over a several week period
reaching about 3.

Another factor to consider is what those users are doing. In EWM, for
example, a developer clearly loads a system more than a contributor. SCM
and build operations are expensive where work item management typically
is not. ETM users typically load a system less than a developer,
although how much load a ETM user puts on the system can vary
considerably as well. A tester who is actively running tests, creating
test results and generating reports will tax the system much more than a
test manager creating and editing text in test plans.

IBM tests performance of each ELM release. To assist customers in their
topology planning, understanding how many application instances they
will need, we have documented our [CLM Sizing
Strategy](https://jazz.net/wiki/bin/view/Deployment/CLMSizingStrategy).
This strategy provides an expected range of concurrent users an
application instance can be expected to support given a particular
server configuration under a defined work load.

##### Related topics: [Deployment planning: Where to start?](DeploymentPlanning) [related-topics-deployment-planning-where-to-start]

-   [Multiple CCM Applications From a User
    Perspective](MultipleCCMAppsUserPerspective)
-   [Multiple CCM Applications Best
    Practices](MultipleCCMAppsBestPractices)

##### External links: [external-links]

##### Additional contributors: Main.RosaNaranjo [additional-contributors-main.rosanaranjo]

META:FILEATTACHMENT{name="Multiple_JTS.png"
attachment="Multiple_JTS.png" attr="h" comment="Multiple JTS and their
registered applications" date="1450345908" path="Multiple_JTS.png"
size="65902" user="rschoon" version="1"}
META:FILEATTACHMENT{name="Multiple_CLM_instances.png"
attachment="Multiple_CLM_instances.png" attr="h" comment="Multiple CLM
applications registered to one JTS" date="1450346193"
path="Multiple_CLM_instances.png" size="54174" user="rschoon"
version="1"} META:FILEATTACHMENT{name="Distributed_SCM.png"
attachment="Distributed_SCM.png" attr="h" comment="Distributed SCM
across multiple CCM appliactions" date="1450346404"
path="Distributed_SCM.png" size="25384" user="rschoon" version="1"}
META:TOPICMOVED{by="tfeeney" date="1402598618"
from="Deployment.PlanForMultipleJazzServerInstances"
to="Deployment.PlanForMultipleJazzAppInstances"}
