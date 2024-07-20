META:TOPICINFO{author="lekandrade" date="1694625854" format="1.1"
reprev="1.24" version="1.24"} META:TOPICPARENT{name="SetupProjects"}

# Rational Team Concert process fundamentals DKGRAY Authors: [Ralph Schoon](Main.RalphSchoon) Build basis: RTC 2.0 and later [rational-team-concert-process-fundamentals-dkgray-authors-ralph-schoon-build-basis-rtc-2.0-and-later]

ENDCOLOR

TOC{title="Page contents"}

Various discussions with customers and questions in the forums indicate
that new projects starting to use Rational Team Concert often struggle
to understand how Work Items, Planning, Build, SCM and other concepts of
RTC integrate. These fundamentals of RTC however are needed to bootstrap
and customize a project. This page provides a basic introduction of the
underlying fundamental concepts of Rational Team Concert. The basic
concepts described in this article apply to all versions of RTC.

## Process configuration fundamentals

One basic task when setting up and administering a project is to
configure the basic process. This section introduces the basic concepts
to consider.

### Project Areas

In Rational Team Concert, **project areas** define the **process** used
by everything they include. Project areas have to be [created in the RTC
application](https://jazz.net/help-dev/clm/index.jsp?topic=/com.ibm.team.concert.nav.doc/topics/c_node_administering.html)
or are created while [creating a lifecycle
project](https://jazz.net/help-dev/clm/index.jsp?topic=/com.ibm.jazz.platform.doc/topics/t_logging_in_application_administration_page.html)

The initial process definition and description are provided by a
**process template** as described in the [Setting up Projects Landing
Page](SetupProjects). RTC ships with several [predefined process
templates](https://jazz.net/wiki/bin/view/Deployment/RTCProcessFundamentals)
that are a good starting point for various different project types.

The project area's **Process Configuration editor** is the main area for
[configuring and defining the process of the project
area](https://jazz.net/help-dev/clm/index.jsp?topic=/com.ibm.jazz.platform.doc/topics/t_projects_teams_process.html).
It allows you to define roles, the permissions and process behavior for
artifacts owned by the project area and it's enclosed teams. The editor
is available in the [Web
UI](https://jazz.net/help-dev/clm/index.jsp&topic=/com.ibm.jazz.platform.doc/topics/c_creating_managing_cross_application_projects.html)
as well as in the [Eclipse
client](https://jazz.net/help-dev/clm/index.jsp?topic=/com.ibm.jazz.platform.doc/topics/t_projects_teams_process.html).
Currently (RTC 5.x) some capabilities are only available in the RTC
Eclipse client.

### Project Area Templates / Process Templates

Project Area Templates and Process Templates provide a way to create new
project areas from predefined configurations. A set of "out of the box"
configurations are provided to enable various project and work flow
needs. In addition, after building a custom project area, the project
area can be exported as template and future new project areas can be
generated from the template. It is often a design decision whether to
create a fully configured project area based on a project template, or
if it is better to create a child project area that inherits the
behavior of a main project area.

Templates provide a wide range of capabilities, including defining the
types, attributes, default queries, plans and other configurations. Care
must be taken when defining project templates, such as when exporting a
project area as a template, that the artifacts included do not reference
id's from artifacts in the original project area. For example, a query
by work item type can be used by another project area with the same
configuration without concern. However a query that includes certain
attribute values such as the Unassigned value of the Filed Against
attribute would reference an artifact id (UUID) which does not exist in
the new project area so the query would not work properly if included in
a template. In addition, enumerations defined as "Database Enumerations"
are only included in the database so would not be exported when a
project area template is created. For this case the references such as
attribute definitions referencing the enumerations would reference an
enumeration id that does not exist; the workaround is to manually add
the database enumerations in to the new project area, using the same
enumeration and literal id's.

### Team Areas

A project area can contain **team areas**. [Team areas are
created](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.platform.doc/topics/c_add_mod_users_web.html)
within project areas or within team areas to further organize and
structure work within a project area. Team areas inherit the project
area's process, roles, permissions and operational behavior. **Users**
are defined as **members** of project and team areas and along with
their **roles**. This combination of membership and role [provides them
with permissions](https://jazz.net/library/article/291) and [defines the
behavior of RTC](https://jazz.net/library/article/292) when working with
artifacts owned by a project or team. Team areas may add new roles. They
can also modify the permissions and the operational behavior they
initially **inherit** from their parent's up to the project area.

### Members

[Users are added to project areas and team
areas](https://jazz.net/help-dev/clm/index.jsp?topic=/com.ibm.jazz.platform.doc/topics/c_add_mod_users_web.html)
as **members** of said area. Membership in a team- or project area is
used to control role based permissions and potentially access to the
data owned by the area.

A special membership is the project **administrator**. The user
[creating a project
area](https://jazz.net/help-dev/clm/index.jsp?topic=/com.ibm.team.concert.nav.doc/topics/c_node_administering.html)
is automatically entered as administrator in the project area. You can
add additional administrators later. This membership allows the user to
configure the process of the project area.

### Roles

Members of project and team areas have [roles
assigned](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.platform.doc/topics/c_add_mod_users_web.html).
Every member of an area has the **Everyone** or **default** role
assigned. Roles are used to control
[permissions](https://jazz.net/library/article/291) and [operational
behavior](https://jazz.net/library/article/292). A user can have
multiple roles. The roles are ordered and the order of the roles a user
has controls operational behavior. The initial roles and their
permissions and operational behavior configuration is provided by the
process template. The project and team area can modify, remove and
define additional roles that can be assigned to users.

Please note, users that are administrator of a project area or have
administrative permissions on repository level can only perform the
operations permitted by the roles they have in the project area,
however, they can always modify the process and grant themselves roles
and permissions if needed. It is possible to define a role like
"Administrator" that exclusively has all the serious permissions needed
to change the process. Administrators can then grant themselves this
role if they want to do administrative tasks. If the task is done the
administrator can remove the role again. This can help with avoiding
unplanned accidental changes to the process.

### Repository Roles

Permissions on repository level are granted by **repository roles**.
Repository roles are granted in the user administration section and
usually tied to groups in the LDAP system. Repository roles are provided
by the application, currently the following repository roles are
available

-   JazzAdmins - full administrative access
-   JazzGuests - guest users
-   JazzUsers - regular users with no repository wide administrative
    permissions, can be an administrator in a project area
-   JazzProjectAdmins - users with limited repository wide
    administrative permissions to perform repository level operations
    for project area members

Users with administrative permissions can see work items and project
area content that should be hidden due to visibility for a regular user.
Users with administrative permissions can also make themselves a member
and an administrator of a project area. The can grant themselves
permissions regardless of the permissions defined for the roles they
have in the context.

### Timelines

The project area defines one or more **timelines** which define how a
given **planned period of time** is **partitioned** into **iterations**
such as releases, milestones, sprints etc. A project area can be
assigned to **exactly one project timeline** to work against at any
instance in time. Team areas contained in a project can also each be
assigned to exactly one timeline to work against at any instance in
time. Only team areas on the top level of the team area hierarchy can
specify a different timeline, nested team areas **inherit** the timeline
from their parent. Please see the section [Timeline and iteration
fundamentals](#Timeline_and_Iteration_Fundament) for more details.

### Iterations

Iterations typically have a **start** and **end** date. Iterations can
be planned to deliver a result by marking them with the check box **"A
release is planned for this iteration"**. These iterations show up in
plans and can be selected in work items as "Planned for". The start and
end dates are used by the planning component to calculate **progress**,
**time available**, **load** and other information. Please see the
section [Timeline and iteration
fundamentals](#Timeline_and_Iteration_Fundament) for more details.

Iterations can have an iteration type. The iteration type can be used to
configure process behavior.

Iterations with no **"A release is planned for this iteration"** set and
with no dates configured can be used to control the process behavior
within a parent iteration.

### Work Item Types

The project area's process configuration is also used to define which
**types** of **work items** are available in this project area, which
workflow they follow, which attributes they provide, and how they are
displayed.

The project area configuration in the planning\>Work Item Type
Categorization section allows to categorize work item types as **plan
item** work item type. This controls how the planning component uses the
work items of these types for work breakdown and effort tracking. Work
items that don't belong to a plan item work item type are called
**execution items**.

Permissions can be configured for work item types to govern the process
and prevent deviating from the process.

### Work Items

**Work items** represent work that needs to be done, such as tasks or
defects. A work item has a work item type which defines the
**attributes** and the **workflow** of the work item. Special attributes
provided by default are used to provide mechanisms required to organize
many work items across teams. See the section [Work item
fundamentals](#Work_Item_Fundamentals) for more details.

Work Items are used in planning. The most basic data required for
planning is **which team area is the responsible owner of the work
item** and in **which iteration is the work item planned** to be
completed as described below.

### Categories

To allow users to assign a work item to a team, the project area
provides **categories**. A category is basically a human readable text.
Each category is associated to a project or team area.

It is possible to have multiple categories assigned to a team area. This
can help with planning, work balance and reporting. For example it is
possible to create a category "MyProduct" with subcategories "Core",
"User Interface" assigned to one team. These are also typical
categories.

### Releases

It is a common need to know for which **release** or version a work item
has been created. To support this, the project area provides a central
place to maintain releases. Releases such as "1.0", "2.0", "2.0 M3" to
track work against some general effort can be created and maintained
manually. It is also possible to create a release from a build result.
This is typically used to be able to pinpoint defects for a specific
release that has been shipped.

### Planning

The process of a project area provides available **Plan Types** to
create a new plan. The plan type determines what the plan will show.
Which plan types are available depends on the process template that was
used when creating the project. Please see the section [Planning
fundamentals](#Planning_Fundamentals) for more details.

### Permissions

**Permissions** can be configured on project area and on team area level
for various operations based on the roles a user has. See [Process
permissions lookup in Rational Team
Concert](https://jazz.net/library/article/291) for details on how
permissions work.

Permissions control which artifacts a user can create, modify and save.

Permissions can be configured not only for project and team areas, but
also for the temporal aspect represented by iterations and iteration
types.

### Operational Behavior

**Operational behavior** can be configured on project area and on team
area level for various operations based on the role a user has. See
[Process behavior lookup in Rational Team
Concert](https://jazz.net/library/article/292) for details on how
operational behavior works.

Operational behavior can be used to govern the process of a project or
team area using preconditions and follow up actions.

Operational behavior can be configured not only for project and team
areas, but also for the temporal aspect represented by iterations and
iteration types to allow the process to change over time.

### Source Control

RTC provides a fully integrated Jazz Source Control Management system.
Jazz Source control is integrated with work items and builds. Changes to
artifacts under source control are collected and organized in **change
sets** which can be associated to work items to track work or for
approval. Please see the section
[Source_Control_Fundamentals](#Source_Control_Fundamentals) for more
details.

### Builds

The build system in Rational Team Concert integrates the build process
with the work item based change management and the Jazz Source Control.

**Build definitions** control what is built and how it is built. **Build
Engines** do the build. The **Jazz Build Engine** or **JBE** is
available in the product. Other build engines can be used. The **Build
System Toolkit** and the ant tasks are used in build scripts and for
build publishing. RTC maintains the build results for each build
definition.

Build typically run on Jazz Source Control **streams**. During builds
the process creates relationships between the build result, the change
sets included and associated work items to help understanding what is
included in the build. Work items can be created against builds to track
the maturity and assign resources to fix problems. Please see the
section [Build Fundamentals](#Builds) for more details.

## Timeline and Iteration Fundamentals

When considering setting up timelines and iterations some best practices
have shown to be useful.

If a project performs parallel types of work, such as development for a
new release and maintenance of old releases and wants to do separate
planning for these kinds of activities, separate timelines and teams.
For example, the project and a couple of teams work on the project
timeline and develop for new releases. Some other maintenance teams work
against a maintenance timeline.

Planning needs an iteration for time-boxing. If something should show up
as a duration in planning create an iteration that represents the
time-box for this effort.

When defining iterations it is useful to have a consistent naming and
identifier schema. Some typical examples are below. The format used
"Iteration 1 (M1 R1) \[i1.m1.r1\]" can be interpreted as follows. The
first part is the **display name** "Iteration 1 (M1 R1)" and the text in
the brackets represents the **identifier** "i1.m1.r1".

### Timeline for a release based development:

### Timeline for quarterly maintenance:

When setting the start and end dates of iterations make sure the dates
of iterations don't overlap. The iterations on each level should be a
**partition** of the given time of the iterations on the next higher
level. If iterations overlap the progress information in plans gets
inaccurate. At the time of writing, the overlapping time of two
iterations is counted as available in plans including the iteration.
Effectively the overlapping time is counted as available twice. User
Allocation for the overlapping time counts in each iteration. so the
resources allocated are double booked.

When [creating
iterations](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.platform.doc/topics/c_creating_timelines_iterations_iteration_types.html)
it is possible to define a iteration type for the iteration. This can be
used to specify different operation behavior for different iteration
types. For example you can create iterations develop and endgame with
iteration types Develop and EndGame without the "A release is planned
for this iteration" checked. they would be invisible to the normal user
but can be set to active within the iteration. It is then possible to
specify at the iteration type that users always require an approval to
deliver code in the EndGame but can deliver without approvals in
Development.

Each timeline has a current iteration that controls the current process
behavior. The current iteration needs to be set manually e.g. by the
project lead.

## Work Item Fundamentals

Work items help to do a lot of things in RTC the following section
explains the basic building blocks of work items.

Work items live in the project area they are created. Since each project
area has its own process, the work item depends on that process and
lives within the project area. You can copy/move work items between
project areas, but essentially you get a new work item in the
destination project area. During the copy/move, work item attribute
values are mapped to the new values in the target project area.

You can link work items to other work items (and other elements) with
using various link types. Only Parent/Child and Tracks/Contributes To
have some business logic in planning or operational behavior out of the
box. There is no semantic or business logic implemented for most of the
link types. The tracks link is used in cross project planning.
Parent/Child links are used in planning for work items that are in the
same project area and show up in the same plan. For Parent/Child links
RTC provides some advisors/preconditions.

### Required Work Item Attributes

When creating work items it is necessary to provide some basic
information. Work items require to at least have a **type** and a
**summary**. It is possible to define which information is needed to be
present when saving a work item in the process configuration.

The work item type is selected when creating a work item. The type can
be changed later. Only the types available in the project the work item
is created for are available.

### Common Work Item Attributes

In an environment with multiple teams and multiple releases it is
necessary to provide ways to make the amount of work items more
manageable. The following work item attributes are used to do just that.

The work item's attribute **Filed against** allows to select and set the
work item's category. Setting the category also sets the team area
associated with it as the owner of the work item.

The work item's attribute **Found In** allows to select and set the
release the work item was created for.

The work item also has a **workflow state** which is driven by selecting
actions in the workflow.

A work item can have exactly one responsible person, the **Owner**.

Since this question comes up often, it is not possible to have multiple
owners in RTC. Experience shows, if you have multiple owner responsible
for one item, every one of them thinks the other owners should do
something with it. It is possible to customize the work items and add an
attribute, call it **Additional owners** of type user list. Other
mechanisms available are subscriptions, mentioning a user in comment.

A standard way of working if there is a big chunk of work that needs to
be broken up into work for multiple team members, is to create new work
items for each member and set the original work item as parent.

The image below shows the most important attributes used with work items
and how they relate to the fundamental concepts above.

### Custom Work Item Attributes

Work items can be [customized](EnactProcess) in various ways. The
easiest way is to add custom attributes to work item types. Various
types of attributes are provided to choose from. Custom attributes must
be added to the editor presentations so that users can see and change
them.

## Planning Fundamentals

The planning component is an important part of RTC. Plans provide a
specialized view on the work items in a project area. Please note, plans
show the real data on the work items. Plans do not contain the work
items as copy or some data that is unrelated to the reality of the
project. Changing a work item in the plan really changes the properties
of the work item.

In RTC 5.0.2 the **Quick Planner** was introduced. This is a special
page in the web UI to allow an agile developer to quickly create,
organize and plan work items. It can be configured with filters and
custom views and provide each individual with a support planning work
items planning component.

The classic planning component is also available. It provides shared
plans for members of the project area hierarchy.

Currently there are four "flavors" of planning available.

-   [Iteration/agile plans](https://jazz.net/library/article/594)
-   [Traditional/formal planning
    plans](https://jazz.net/library/article/657)
-   [Cross project plans](https://jazz.net/library/article/1152)
-   Quick planner

Dependent on the process template that was used to create the project
area, you have **agile planning** or **traditional/formal planning**
available.

Traditional planning is available in the "Formal Project Management
Process" template. It provides a scheduler that uses

-   Predecessor/successor relationships
-   Schedule constraints
-   Estimated effort, ranking
-   Resource availability

to calculate the schedule for the work items in the plan and show the
critical path.

Agile planning is available with the process template Scrum and Scaled
Agile Framework (SAFe) 3.0 (new in RTC 6.0). The example project also
uses an agile approach. The agile scheduler does not use any
relationships, it uses

-   Ranking
-   Estimated effort
-   Resource availability

to calculate durations and show the schedule.

Please note, regardless of the scheduler, the individual developer have
to order and execute their work items as prioritized or agreed to. The
plan does not order the work items for the developer e.g. in the my work
view.

### Plan types and plan views

The process configuration of the project area provides the available
**plan types** to choose from when creating a plan. Plans are
**configurable queries** on **life data** provided by **work items
selected by the plan**.

Each plan type provides some **Plan Views**. The Plan views configure
how the data will be presented on the planned items tab. Each plan can
have multiple plan views. New plan views can be created to present the
data in a convenient way. Plan views are global. Changing a plan view of
a plan changes it for all users.

Custom Plan views can be
[promoted](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.team.apt.doc/topics/t_associate_planmode_with_plantype.html)
and then configured to be used in the plan types to allow using them on
new plans. The Promotion operation is only available in the RTC Eclipse
client.

### Plan Details or Plan Scope

Creating and configuring a plan defines the scope of the plan, which
defines the data that is going to be presented in the plan. The plan's
scope is defined by configuring the following Plan Details:

-   The **owner of the plan** specifies which team area contributes to
    the plan. Since the team area is also assigned to one time line this
    specifies which iterations can be selected.

<!-- -->

-   The **iteration of the plan** specifies that only work items planned
    for this iteration are included into the plan. The iteration
    selected can only be part of the timeline the plan owner is working
    against. Also it is only possible to select iterations that are
    planned to deliver something. The latter is specified by setting the
    A release is planned for this iteration property for the iteration.

<!-- -->

-   The **plan type** that determines how the plan views, as well as
    which of the work items qualified by the above information, will be
    presented. The choice is to include only top level work items or all
    work item types.

### Attributes in plan views

All relevant built in attributes of the work item types are available to
be displayed in the plan views. Custom attributes are not available to
be selected in the plan view display. Custom attributes have to be added
to the **Attribute Mapping** in the process configuration section
**Project Configuration\>Configuration Data\>Planning\>Plan Attributes**
to make them available for selection in the plan view display section.

### Planned Items

Plans only show work items in their scope within the **Planned Items
tab**. Plans will only consider work items in scope that have the
**Planned For** attribute set to the iteration or nested iterations the
plan is configured for. Plans will also only consider work items that
are filed against the team area or one of its child team areas the plan
is configured for.

By default several plan types will also only show **top level work
items** to reduce the amount of details presented.

Plans that show only work items of types defined as **Plan Items** can
be configured to also show **execution items**. This can be done for
example in the Web UI. Edit the **Plan Details** and select the check
box **Include All Items** to include execution items in the view. The
impact of this is longer load times for the plans. The filter
**Execution Items** can be used to filter these work items out for a
better overview when the plan is configured to load execution items.

### Where is my work item?

If a work item disappears from a plan or one you expected is missing
from your plan it is probably filtered out or out of the plan's scope.
Check for the active filters and if execution items are included in the
plan. Carefully check the work items attributes, especially **Planned
For** and **Filed against**.

Work items that are not in the scope of the plan are **outplaced
items**. How outplaced items are handled has changed over time.

Up to RTC 3.x independent of its configuration a plan will only show and
consider work items that are planned for an iteration that belongs to
the the plans owners timeline. Although you can create work items on a
plan and plan them for a different timeline, the next time the plan is
loaded these work items will not be presented on the plan. In work
breakdown structures child work items planned for a different timeline
will also not be presented and their estimation and effort values will
not be calculated or rolled up by the plan. You can see outplaced parent
work items as greyed out in the plan.

In RTC 4.x and 5.x it was possible to see outplaced items on a work
breakdown plan for the relationship defined in the work breakdown. This
could have adverse impact on the plan performance. So this might change
in later releases.

In general the traditional and the agile scheduler doe not include
outplaced items, especially if owned by another project area for the
schedule. Their complexity, estimation and effort values will not be
calculated or rolled up by the plan.

## Source Control Fundamentals

The RTC Jazz Source Control Management provides the following
capabilities to support source control.

-   **Streams** - The RTC Jazz Source Control Management component
    provides streams to share source code under version control across
    all users.
-   **Components** - Streams contain components that are used to
    partition the source code e.g. across architectural boundaries.
-   **Repository workspaces** - Users have repository workspaces as
    their private sandbox. To work on the code it is **loaded** to a
    local disc. Changes in the local files are monitored. Users
    **check-in** local changes into the repository workspace.
-   **Flow Target** - Repository workspaces typically **flow** with one
    or more streams. The **current flow target** is the stream with
    which the source control component compares to the content of the
    repository workspace to analyze the changes on both ends. If a
    repository workspace has multiple flow target only one can be
    current.
-   **Change sets** - Local changes that get **checked-in** by a user
    are stored in **change sets**. Each change set represents the
    changes to **one or more files** in **one component**. Change sets
    can have **related work items** for documentation and approvals. It
    is possible to navigate between change sets and related work items.
-   **Baselines** - To create a reproducible unchangeable configuration
    for a component baselines can be created. Baselines are accessible
    as elements in the source control system to create and replace
    component content.
-   **Snapshots** - To create a reproducible unchangeable configuration
    for a stream and the components snapshots can be created. Snapshots
    create new baselines for components that are not selecting a
    baseline and can use baselines that exist. If requested to do so, a
    snapshot can create new baselines for each component. The snapshot
    is owned by a repository workspace or stream. It is possible to
    change the owner e.g. to collect important the snapshots. snapshots
    can be used to recreate the state of a stream or repository
    workspace. They can also be used to compare them to other states.
-   **Pending Changes** - The pending changes view shows the comparison
    of the local sandbox and the flow targets. Local changes on disk not
    yet in the repository workspace are **unresolved**. During check-in
    new change sets containing the local changes are created. New change
    sets in a repository workspace that are not yet in the current flow
    target are **outgoing**. They can be **delivered** to the flow
    target stream. Changes delivered by others to the current flow
    target not in the repository workspace are showing as **incoming**
    change sets. The owner of the repository workspace can **accept**
    the incoming changes to get them in the repository workspace and on
    disk.

### Integrating

To integrate changes from one stream to another, use a repository
workspace that has two streams as flow targets. When the repository
workspace is in sync with the first stream change the flow target to the
other stream. The source control system calculates the differences
between the repository workspace and the new flow target stream. It then
allows to deliver, accept and merge changes to bring the repository
workspace and the stream to the same state. If the repository workspace
was changed in this operation, changing the flow target to the original
stream allows to deliver integrations back to that stream.

### Promoting changes between streams

A stream can have another stream as a flow target. If there are no
conflicting changes the pending changes view can be used to accept and
deliver the changes between the streams. If there are conflicting
changes a repository workspace is required to solve the conflicts.

### SCM across project areas

Source Control Data is not confined to the project area. Streams and
components are only owned by project areas, team areas or users. The
ownership controls permissions and operational behavior. Ownership can
also be used to control visibility. However, it is possible to create a
stream based on a stream or component baselines owned by a different
project area. Data can also flow across project areas.

See the [Jazz Source Control FAQ](https://jazz.net/library/article/126)
for more information.

### Distributed SCM

The SCM data lives in a repositrory. Distrbuted SCM allows to make SCM
data available in multiple repositories. It makes it basically possible
to replicate SCM repository data from one repository into another one
and make it available there. See the article \* [Flow changes cross
repositories with Rational Team
Concert](https://jazz.net/library/article/535) for more information.

Also see the workshop [Rational Team Concert Workshop Distributed SCM
and Shipping RTC SCM Change Sets Across Disconnected
Networks](https://jazz.net/library/article/1399) for more details and
how to use this technique to ship data between disconnected sites.

## Build Fundamentals

This section will explain some of the fundamental concepts for
continuous engineering with builds. See the [Jazz Build
FAQ](https://jazz.net/wiki/bin/view/Main/BuildFAQ) for additional
information.

### Build engines

If you want to do a build, it has to be performed on some machine. This
is what a **build engine** does. There are several types of build
engines available that you can use with RTC

-   The Jazz Build Engine - JBE for short
-   Jenkins/Hudson
-   BuildForge

The Jazz Build Engine is a very basic build engine that is well
integrated with RTC. The build engine is built based on Eclipse and is
run as a headless process on one or many **build servers**. Each Jazz
build engine is called with parameters to define the RTC repository it
serves, the user that runs the build and the unique ID that identifies
this build engine. It is possible to run the Jazz Build Engine multiple
times on a build server.

Jenkins and BuildForge are more advanced build engines that can be used
with RTC. They need to be installed separately and can then be
integrated with the RTC build system.

### Build engine definitions

To be able to run any build engine needs a **build engine definition**
created in a RTC project area. This definition defines the unique engine
ID, the build engine type and can have properties to adjust for the
machine the engine runs on. For example you could need variable
properties, where the build tools are installed for different build
servers.

### Build definitions

A **build definition** is needed to be able to request builds. The build
definition specifies what tools to call to actually build. It also
specifies several steps you want to perform before or after a build.
There are several predefined types of build definition available in RTC.
Here just some few.

-   Using ANT with the JBE
-   Command Line with JBE
-   Generic
-   Jenkins
-   JBE with MS visual Studio
-   Maven with the JBE
-   Build Forge

The build definitions specify the build engines that execute the builds.

If you use one of the JBE based build definitions there are some
pre-build and post-build activities available to choose from. Load data
from the Jazz SCM (and create a snapshot if possible), before running
ANT, publish build results and deliver code somewhere else after the
build.

### Requesting and scheduling builds

Builds don't just happen by chance. They have to be requested by
someone. It is possible to define a schedule to create build requests.
In RTC users can request a build for a build definition. If a user
requests a build there are two choices of build requests available

-   Personal builds
-   Public builds

The user requests a personal build by providing his personal repository
workspace to be built. Otherwise the build is public.

### Build, permissions, licenses

The build engines like the Jazz Build Engine require users with
permissions and licenses configured to access the data and to publish
build results. Special **build system** licenses are available to assign
them to technical users.

The technical user performing the build must have access to the data
which usually means the user needs to be member of the project area and
have some role with the permissions to access the data.

All builds are run in the context and with the credentials of this user.

### JBE builds and Jazz SCM

To use the RTC SCM load capabilities in JBE based build definitions a
repository workspace is required to build. It must be owned by the build
user.

During a build, if the build user has the required permissions, a
snapshot is generated on the repository workspace. This snapshot is used
to compare it to the build before to determine the change sets that went
into the build compared to the one before. From this information the
build result also shows the work items related to this build.

In **personal builds**, the repository workspace of the user submitting
the request is used to load the SCM data. The repository workspace must
be visible to the build user for this to work. Regardless of being
visible to the build uder, the build user can not create a snapshot on
the repository workspace used during a personal build. Therefore no
snapshot can be created and this information is missing on personal
builds. The build user can however not create a snapshot on that
workspace and therefore the data can not be compared to previous builds.

### Build results

Each build definition creates a queue for build requests. The build
requests end in this queue and get picked up by the build engine to be
executed. The build engine runs the build somewhere and reports progress
and results back to RTC. Progress and results are collected and made
available in a **build result**.

It is possible to create work items for build results for example to
track progress of builds towards release.

It is possible to create a release from a build result, this also
protects the build result from being deleted. The release can then be
later used in the **Found In** attribute of work items to e.g. file
defects.

##### Related topics: [Deployment web home](DeploymentWebHome), [Set up projects](SetupProjects) [related-topics-deployment-web-home-set-up-projects]

##### External links: [external-links]

###### General \* [A good overview about the RTC features with links to more details.](https://jazz.net/projects/rational-team-concert/features/) [general-a-good-overview-about-the-rtc-features-with-links-to-more-details.]

-   [A Deployment Guide: Getting Started with Rational Team Concert
    3.x](https://jazz.net/library/article/542)

###### Planning [planning-1]

-   [Effective Planning with Rational Team
    Concert](https://jazz.net/library/article/1033)
-   [Understanding ranking in Rational Team Concert
    4.0](https://jazz.net/library/article/1033)
-   [Progress Bars, Load Bars, and the importance of estimating your
    work in Rational Team Concert](https://jazz.net/library/article/586)
-   [Cross-Project Tracking with Rational Team
    Concert](https://jazz.net/library/article/1152)
-   [Traditional planning: Managing formal projects in Rational Team
    Concert](https://jazz.net/library/article/657)
-   [Work Allocation and Planning - The Kate and William OpenUP
    Story](https://jazz.net/library/article/761)
-   [The traditional scheduler in IBM Rational Team Concert
    4.0](https://jazz.net/library/article/663)
-   [Planning with Rational Team Concert
    3.0](https://jazz.net/library/article/590)
-   [Progress Bars, Load Bars, and the importance of estimating your
    work in Rational Team Concert
    3.0](https://jazz.net/library/article/586)
-   [Using the My Work view in Rational Team
    Concert](https://jazz.net/library/article/588)
-   [Planning in the Web UI with Rational Team Concert
    2.0.0.2](https://jazz.net/library/article/382)

###### Customizing the process [customizing-the-process]

-   [Work Item Configuration and Shared Process in Rational Team
    Concert](https://jazz.net/library/article/1005)
-   [Fine-grained Customization of Configuration
    Data](https://jazz.net/wiki/bin/view/Main/ConfigurationDataDeltaUserDoc)
-   [Work Item and Foundation Articles, Wikis, and Tech Notes
    ](https://jazz.net/wiki/bin/view/Main/WorkItemArticlesAndTechNotes)
-   [Working with process
    templates](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.platform.doc/topics/t_work_process_templates.html)
-   [Migrating a project to a different process
    template](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.platform.doc/topics/t_migrate_dif_process.html)
-   [Exporting and importing process
    templates](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.platform.doc/topics/t_export_import_process_templates.html)
-   [Process
    templates](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.platform.doc/topics/c_process_template.html)
-   [Changing your Rational Team Concert Process Configuration - Best
    Practices](https://jazz.net/library/article/1002)
-   [Work Item Customization in Rational Team Concert
    3.0](https://jazz.net/library/article/565)
-   [Process Enactment Workshop for the Rational solution for
    Collaborative Lifecycle Management
    2012](https://jazz.net/library/article/1093)
-   [Customizing Attributes in Rational Team Concert
    3.0](https://jazz.net/library/article/537)
-   [Customizing the Agile Planning tools in Rational Team Concert
    3.0](https://jazz.net/library/article/587)
-   [Customizing a process template for formal project
    management](https://jazz.net/library/article/572)

###### Jazz Source Control [jazz-source-control]

-   [Jazz Source Control FAQ](https://jazz.net/library/article/126)
-   [Easing into Jazz Source
    Control](https://jazz.net/library/article/539)
-   [Update SCM Process Recipes](https://jazz.net/library/article/1468)
-   [Improved Gap Handling for
    SCM](https://jazz.net/library/article/1469)
-   [Flow changes cross repositories with Rational Team
    Concert](https://jazz.net/library/article/535)
-   [Rational Team Concert Workshop Distributed SCM and Shipping RTC SCM
    Change Sets Across Disconnected
    Networks](https://jazz.net/library/article/1399)
-   [Loading Content from a Jazz Source Control Repository in Rational
    Team Concert](https://jazz.net/library/article/1016)
-   [Controlling access to source control in Rational Team
    Control](https://jazz.net/library/article/215)
-   [How to keep your streams flowing smoothly in Rational Team
    Concert](https://jazz.net/library/article/649)
-   [Deleting Content From Source Control in Rational Team
    Concert](https://jazz.net/library/article/1006)

###### Build [build]

-   [Jazz Build FAQ](https://jazz.net/wiki/bin/view/Main/BuildFAQ)
-   [Getting Started with Setting up Jazz
    Builds](https://jazz.net/library/article/38)
-   [Getting started with Ant builds on the Jazz Build
    Engine](https://jazz.net/library/article/1287)
-   [Getting Started with Ant scripts and RTC Build Ant
    Tasks](https://jazz.net/library/article/1286)
-   [Build Artifacts Publishing Using HTTP Servers in Rational Team
    Concert](https://jazz.net/library/article/797)
-   [Automated Build Output Management Using the Plain Java Client
    Libraries](https://jazz.net/library/article/807)
-   [Using the SCM Command Line Interface in
    builds](https://jazz.net/library/article/195)
-   [Monitoring your build's progress with build
    activities](https://jazz.net/library/article/37)

##### Additional contributors: RalphSchoon -- Original content [additional-contributors-ralphschoon----original-content]

LawrenceSmith - Added Project Area Templates section.

META:FILEATTACHMENT{name="DevelopmentTimeline.png"
attachment="DevelopmentTimeline.png" attr="h" comment=""
date="1436195930" path="DevelopmentTimeline.png" size="17634"
user="rschoon" version="1"}
META:FILEATTACHMENT{name="Quarterly_Maintenance.png"
attachment="Quarterly_Maintenance.png" attr="h" comment=""
date="1436196101" path="Quarterly_Maintenance.png" size="10855"
user="rschoon" version="1"}
META:FILEATTACHMENT{name="Process-And-WorkItem.png"
attachment="Process-And-WorkItem.png" attr="h" comment=""
date="1436196181" path="Process-And-WorkItem.png" size="71834"
user="rschoon" version="1"} META:FILEATTACHMENT{name="ConfigurePlan.png"
attachment="ConfigurePlan.png" attr="h" comment="" date="1436257031"
path="ConfigurePlan.png" size="9459" user="rschoon" version="1"}
