META:TOPICINFO{author="fryerk" date="1580152182" format="1.1"
version="1.16"} META:TOPICPARENT{name="DeploymentAdminstering"}

# Frequently-asked questions (FAQ) about CLM configuration management DKGRAY Authors: Main.KathrynFryer Build basis: Rational solution for Collaborative Lifecycle Management (CLM) 6.x [frequently-asked-questions-faq-about-clm-configuration-management-dkgray-authors-main.kathrynfryer-build-basis-rational-solution-for-collaborative-lifecycle-management-clm-6.x]

ENDCOLOR

TOC{title="Page contents"}

This page answers common questions about the configuration management
capabilities that were introduced in version 6 of the IBM Engineering
Lifecycle Management (ELM) solution (formerly known as IBM Rational
Collaborative Lifecycle Management (CLM) - for more details on product
names, please see
[Jazz.net](https://jazz.net/blog/index.php/2019/04/23/renaming-the-ibm-continuous-engineering-portfolio/)).
The suite includes:

-   Engineering Requirements Management DOORS Next Generation (DOORS
    Next) - also referred to as RM
-   Engineering Systems Design Rhapsody - Model Manager (RMM) - also
    referred to as AM
-   Engineering Test Management (ETM) - also referred to as QM
-   Engineering Workflow Management (EWM) - which includes both change
    management and source code configuration management (SCM)

If you have a question that isnt answered here, please ask it in the
[Jazz.net forum](https://jazz.net/forum/). We might add it to our list!

A growing series of articles on Jazz.net provides a deeper exploration
of practices around specific aspects of configuration management. Find
the complete list of available articles in [Best practices for CLM Usage
Models: Global configuration
management](CLMUsageModelBestPractices#Global_Configuration_Management).

## List of questions

\#TopOfList

The questions are organized by topic area, and listed here so you can
more easily locate a specific question.

Enabling configuration management

-   [What benefits do I get from enabling configuration management for
    requirements and quality management domains?](#BenefitsFromCfgM)
-   [Where can I learn more about configuration management
    capabilities?](#LearnMore)
-   [What extra ELM applications do I need to install for configuration
    management? If I dont install them, does it limit any other
    capabilities?](#AppsRequiredForCfgM)
-   [How do I enable configuration management in the ELM
    applications?](#HowToEnable)
-   [Do I have to enable all my projects for configuration
    management?](#EnableAllOrNone)
-   [What happens if I enable only one of my linked RM or QM
    projects?](#EnableOnlyOneLinkedProject)
-   [What if I only want to use configuration management in one ELM
    application?](#OnlyOneAppForCfgM)
-   [If I want multiple components in a single project RM or QM project
    area, do I need to enable configuration
    management?](#FineGrainedComponentsEnablement)
-   [Do I have to define multiple components in my configuration-enabled
    RM or QM project area?](#MultipleFGCsRequiredOrNot)
-   [Why do I see a configuration context menu in my non-enabled RM
    project?](#NonEnabledDNGConfigContext)
-   [What happens to my ClearQuest (CQ) integration if I enable
    Configuration Management in ELM?](#IntegrationWithCQ)

Definitions and concepts

-   [What is a component?](#WhatIsComponent)
-   [What is a configuration?](#WhatIsConfiguration)
-   [What is a local configuration compared to a global
    configuration?](#WhatIsLocalVsGlobalConfig)
-   [Whats the difference between a version and a
    variant?](#WhatIsVersionVsVariant)
-   [What is the default stream?](#WhatIsDefaultStream)
-   [What is a personal stream and why do I need
    one?](#WhatIsPersonalStream)
-   [What is a global baseline?](#WhatIsGlobalBaseline)
-   [What is a baseline staging stream and what is it
    for?](#WhatIsBaselineStagingStream)

Global configurations

-   [When should I work in a local or a global configuration
    context?](#WorkInLocalVsGlobalContext)
-   [Can a global configuration include multiple versions of the same
    local configuration (for example, two different streams from the
    same RM project)?](#GCMultipleVersionsOfLocalConfig)
-   [When do I create a new component instead of a new
    configuration?](#NewComponentVsNewConfig)
-   [Can I write business rules for global
    configurations?](#GCBusinessRules)
-   [Can I modify or update a global baseline?](#ModifyGlobalBaseline)
-   [How do I stabilize my global working stream leading up to a release
    milestone?](#StabilizeWorkingStream)

Managing streams and baselines

-   [When do I create a new stream?](#CreateNewStream)
-   [Are the artifacts in each stream copies of each
    other?](#StreamsCopyOrReference)
-   [When I go to a historical baseline, do I need to use a previous
    version of the application to view it?](#ViewHistoricalBaseline)

Linking artifacts and resolving links

-   [What does directional linking or no back links
    mean?](#DirectionalLinkingExplained)
-   [What happens when my artifact links to an artifact that is not
    included in my current global
    configuration?](#ExistingLinkToArtifactOutsideGC)
-   [What happens when I try to link to an artifact in a component not
    included in my current global
    configuration?](#AddLinkToArtifactOutsideGC)
-   [Can I create a link from a versioned artifact to a non-ELM
    application?](#LinkToNonCLMApp)
-   [What happens to existing links to a non-ELM application that does
    not support global configurations (e.g. IBM Rational DOORS
    9.x)?](#ExistingNonCLMLinkWOCfgM)
-   [When I create a new local configuration, will the existing links
    become inconsistent or
    unresolvable?](#ExistingLinksInNewLocalConfig)
-   [If I delete a link and then link to another artifact, what happens
    to the history of the link to the previous artifact?](#LinkHistory)
-   [I cannot link from a baseline. This seems like a limitation. Is
    there a way around this?](#CreateLinksFromBaseline)
-   [If baselines are not editable, why do links and link validity
    indicators sometimes change in my
    baseline?](#WhyLinksChangeInBaselines)
-   [What attributes are used to determine link
    validity?](#AttributesForLinkValidity)
-   [Can I create links between files under EWM source control to other
    versioned artifacts (like requirements and test
    artifacts)?](#TraceabilityLinksSCM)

Managing and delivering change

-   [When I merge or deliver changes across streams, are the change sets
    physically copied to the receiving
    stream?](#ChangeSetsCopiedOnDelivery)
-   [How can I improve change management of my
    requirements?](#ChangeMgmtForReqts)
-   [Do I have to create a change set to make a change in DOORS
    Next?](#DoINeedChangeSets)
-   [When should I use explicit change sets in DOORS
    Next?](#WhenExplicitChangeSets)

Reporting on configurations

-   [How is reporting on configuration-enabled projects different from
    reporting on non-enabled projects?](#HowIsReportingDifferent)

### Questions: Enabling configuration management

\#BenefitsFromCfgM

#### Q: What benefits do I get from enabling configuration management for requirements and quality management domains? [q-what-benefits-do-i-get-from-enabling-configuration-management-for-requirements-and-quality-management-domains]

A: Configuration management across the lifecycle provides many benefits:

-   Reproduce past results, because you can reliably recreate all
    artifacts associated with a particular milestone or release.
-   Improve collaboration and reuse, better supporting parallel
    development as well as product line variants.
-   Insulate and manage change to the current development work using
    change sets (DOORS Next) or branched streams (ETM)

Increased reuse can lead to reduced costs and faster delivery, while
improving change management and reliability can enhance quality.
\#LearnMore

#### Q: Where can I learn more about configuration management capabilities? [q-where-can-i-learn-more-about-configuration-management-capabilities]

A: Read the Jazz.net article [Welcome to configuration
management](https://jazz.net/library/article/1492) for an overview of
configuration management. Youll find links to many other resources
including educational videos, practice guidance, other articles, and IBM
Knowledge Center topics. \#AppsRequiredForCfgM

#### Q: What extra CLM applications do I need to install for configuration management? If I dont install them, does it limit any other capabilities? [q-what-extra-clm-applications-do-i-need-to-install-for-configuration-management-if-i-dont-install-them-does-it-limit-any-other-capabilities]

A: The following ELM applications are required if you enable
configuration management across the suite:

1.  Global Configuration Management (GCM) application - to group and
    link configurations together
2.  Link Index Provider (LDX) application - to manage links across
    configurations
3.  Lifecycle Query Index (LQE) application - for reporting

If you are not using configuration management (other than EWM SCM for
source control), you do not need the GCM or LDX applications. Omitting
them has no other impact on the CLM applications. You can also
optionally use LQE as a data source for reporting against projects that
are not enabled for configuration management, in addition to the data
warehouse; otherwise, the LQE application is not required.

Ensure that you consider these applications when planning your
infrastructure, and allocate adequate resources. For more information on
the applications and recommended topologies, see [Recommended ALM
deployment topologies for 6.x](RecommendedALMDeploymentTopologies6).
\#HowToEnable

#### Q: How do I enable configuration management in the ELM applications? [q-how-do-i-enable-configuration-management-in-the-elm-applications]

A: RMM and EWM are enabled to work with configuration management by
default; no additional steps are required. (Note: if you are using
Rhapsody - Design Manager v6.0 or v6.0.1, see [this tech
note](http://g01zciwas018.ahe.pok.ibm.com/support/dcf/preview.wss?host=g01zcidbs003.ahe.pok.ibm.com&db=support/swg/rattech.nsf&unid=2487D935C1097C3D85257F6300680F95&taxOC=SSCMKMZ&MD=2016/02/242014:02:16&sid=).)
For DOORS Next and ETM, an administrator must enter an activation key in
the application's setting for Local Versioning Component (under Advanced
Settings); project administrators can then enable individual projects in
the project settings. To request an activation key, contact [IBM
Support](http://www.ibm.com/software/rational/support/contact.html) or
visit [Jazz.net](https://jazz.net/products/clm/cm/get-key).
\#EnableAllOrNone

#### Q: Do I have to enable all my projects for configuration management? [q-do-i-have-to-enable-all-my-projects-for-configuration-management]

A: You can enable configuration management for individual DOORS Next,
ETM, and RMM project areas in the project area settings; you do not have
to enable all project areas. However, if you have links between project
areas, you must enable all of those projects, or none of them, to ensure
that cross-project linking continues to resolve correctly. For example,
if you have an ETM project that links to a DOORS Next project, and that
DOORS Next project links to another DOORS Next project, you must enable
all three of those project areas to ensure that all the cross-project
linking works correctly, and also define a global configuration that
includes the configurations from all three project areas. You do not
need to enable configuration management in EWM project areas, but you do
need to configure them correctly to participate in global
configurations; see [this Jazz.net
article](https://jazz.net/library/article/92499) for details. **Note:**
For EWM and RMM project areas, enabling configuration management refers
to enabling the ability to contribute to global configurations and
participate in configuration management across the lifecycle. All EWM
and RMM projects can create streams and baselines in EWM SCM to manage
source code and models in the context of the individual application.
\#EnableOnlyOneLinkedProject

#### Q: What happens if I enable only one of my linked DOORS Next or ETM projects? [q-what-happens-if-i-enable-only-one-of-my-linked-doors-next-or-etm-projects]

A: If your projects link to each other, enabling only one of them for
configuration management severely compromises your ability to continue
to link between them. For that reason, you should enable all of your
linked project areas, or none of them. Because linking is directional,
the specific behavior depends on which project you enable. Read on for
more details, but in general:

-   You cannot create any new links between the enabled and non-enabled
    projects.
-   Existing links might or might not be displayed, and might or might
    not resolve.
-   If the existing links do resolve, they always go to the artifact in
    the default stream.

If you enable only the DOORS Next project:

-   Links between DOORS Next and ETM will no longer appear (because back
    links are removed).
-   Links from ETM will continue to resolve to the artifact in the
    default stream.
-   You can delete the existing links from ETM (where they appear), but
    you cannot create any new links between the DOORS Next and ETM
    project artifacts.

If you enable only the ETM project:

-   Links between DOORS Next and ETM continue to appear in both
    applications (since ETM owns the links).
-   Clicking the link in DOORS Next opens the ETM artifact in the
    default stream,
-   Clicking the link in ETM gives an error, although preview continues
    to work.
-   You cannot create any new links between the DOORS Next and ETM
    project artifacts
-   You can only delete the existing links from the DOORS Next side.

The outcome is similar when multiple DOORS Next projects link to each
other. \#OnlyOneAppForCfgM

#### Q: What if I only want to use configuration management in one ELM application? A: If your configuration-enabled projects will link to other projects, even to projects in the same ELM application, you still need global configurations to support the cross-project linking. If you only use one application, and you never link across project areas or components, then you do not need to use global configurations or the Global Configuration Management (GCM) application. You might still need the Link Index Provider (LDX) application to ensure that directional links within your project resolve correctly. If you plan to use interactive reports, you also need the Lifecycle Query Index (LQE) application for configuration-enabled reporting. \#FineGrainedComponentsEnablement [q-what-if-i-only-want-to-use-configuration-management-in-one-elm-application-a-if-your-configuration-enabled-projects-will-link-to-other-projects-even-to-projects-in-the-same-elm-application-you-still-need-global-configurations-to-support-the-cross-project-linking.-if-you-only-use-one-application-and-you-never-link-across-project-areas-or-components-then-you-do-not-need-to-use-global-configurations-or-the-global-configuration-management-gcm-application.-you-might-still-need-the-link-index-provider-ldx-application-to-ensure-that-directional-links-within-your-project-resolve-correctly.-if-you-plan-to-use-interactive-reports-you-also-need-the-lifecycle-query-index-lqe-application-for-configuration-enabled-reporting.-finegrainedcomponentsenablement]

#### Q: If I want multiple components in a single RM or QM project area, do I need to enable configuration management? A: Yes, the capability to "subdivide" a QM or RM project area into multiple components is only available if the project is enabled for configuration management. Each component then has its own set of streams and baselines. There are no other specific settings to enable multiple components in a project area. [q-if-i-want-multiple-components-in-a-single-rm-or-qm-project-area-do-i-need-to-enable-configuration-management-a-yes-the-capability-to-subdivide-a-qm-or-rm-project-area-into-multiple-components-is-only-available-if-the-project-is-enabled-for-configuration-management.-each-component-then-has-its-own-set-of-streams-and-baselines.-there-are-no-other-specific-settings-to-enable-multiple-components-in-a-project-area.]

\#MultipleFGCsRequiredOrNot

#### Q: Do I have to define multiple components in my configuration-enabled RM or QM project area? [q-do-i-have-to-define-multiple-components-in-my-configuration-enabled-rm-or-qm-project-area]

A: Enabling configuration management for your RM or QM project
automatically enables having multiple components in that project area,
and defines an initial component that includes any existing artifacts in
the project area. It is your choice whether to define additional
components. \#NonEnabledDNGConfigContext

#### Q: Why do I see a configuration context menu in my non-enabled DNG project? A: Even if your DOORS Next project is not enabled for configuration management, you can make baselines of the artifacts at important milestones. You can then use the configuration context menu to select a particular baseline or the current artifacts, and determine what set of artifacts you are exploring. Non-enabled ETM project areas do not show a configuration context menu because they use different mechanisms to manage snapshots. \#IntegrationWithCQ [q-why-do-i-see-a-configuration-context-menu-in-my-non-enabled-dng-project-a-even-if-your-doors-next-project-is-not-enabled-for-configuration-management-you-can-make-baselines-of-the-artifacts-at-important-milestones.-you-can-then-use-the-configuration-context-menu-to-select-a-particular-baseline-or-the-current-artifacts-and-determine-what-set-of-artifacts-you-are-exploring.-non-enabled-etm-project-areas-do-not-show-a-configuration-context-menu-because-they-use-different-mechanisms-to-manage-snapshots.-integrationwithcq]

#### Q: If I want to enable configuration management, can I still integrate with IBM ClearQuest? Will it work? [q-if-i-want-to-enable-configuration-management-can-i-still-integrate-with-ibm-clearquest-will-it-work]

A: For details on IBM ClearQuest integration, see [ClearQuest support
for OSLC Configuration Management and Global
Configurations](http://www-01.ibm.com/support/docview.wss?uid=swg27047205)

[ *Back to top* ](#TopOfList)

### Questions: Definitions and concepts

\#WhatIsComponent

#### Q: What is a component? [q-what-is-a-component]

A: A *component* is part of your system a unit of organization for a
reusable set of engineering artifacts. The granularity of a component
varies between providers, but typically it contains the set of artifacts
used in some product, project, or a subdivision of such a set. As of
version 6.0.3, you can create multiple components within a single DOORS
Next or ETM project area; in earlier versions, a component corresponds
to an entire project area. In EWM SCM and RMM, you can define components
to the level of granularity you desire. A global component groups
related components across the lifecycle, and optionally other global
components, into a hierarchy like a product line. \#WhatIsConfiguration

#### Q: What is a configuration? [q-what-is-a-configuration]

A *configuration* identifies a subset of the artifacts in a component,
and selects one version of each of those identified artifacts. A single
component can have multiple configurations. A configuration can be
either a stream, where artifacts can be modified, or a baseline, where
artifacts are captured at a particular point of time and can't be
changed. \#WhatIsLocalVsGlobalConfig

#### Q: What is a local configuration compared to a global configuration? [q-what-is-a-local-configuration-compared-to-a-global-configuration]

A: A *local configuration* is defined in a single application for
example, a stream in ETM. Local configurations can be assembled into, or
*contribute to*, a *global configuration* in the Global Configuration
Management (GCM) application. To link artifacts across local
configurations, the local configurations must be included in the same
global configuration. \#WhatIsVersionVsVariant

#### Q: Whats the difference between a version and a variant? [q-whats-the-difference-between-a-version-and-a-variant]

A: In our terminology, a *variant* is a *version* of an artifact that is
identified by a specific set of characteristics that distinguish it from
other versions of the same artifact, where each variant can exist at the
same time as other variants of the artifact; think about models of a car
or phone. There will, of course, often be several time-based versions of
a given variant. \#WhatIsDefaultStream

#### Q: What is the default stream? [q-what-is-the-default-stream]

A: For DOORS Next and ETM, the *default stream* (also called *default
configuration*) is the initial stream created when you first enable your
project area for configuration management. If you never created another
branch stream, all your work in that project area would be in the
default stream. When an incoming link doesnt specify version information
for an artifact, the link resolves to the artifact in the default stream
(if it exists). If the artifact isnt in the default stream, the link
fails to resolve. \#WhatIsPersonalStream

#### Q: What is a personal stream and why do I need one? [q-what-is-a-personal-stream-and-why-do-i-need-one]

A: A *personal stream* is a global configuration owned by and visible to
a single user. When a DOORS Next user creates a change set in the
context of a global configuration, a personal stream is automatically
created and associated with that change set and the original global
configuration. The personal stream is effectively a personal override
for the global configuration, allowing the changes made in the change
set to be seen in the global context but only by the user making the
changes. Other users in the same global configuration context will not
see the changes until they are delivered. For a more detailed
explanation, see [this blog
post](https://fryerk.wordpress.com/2018/01/24/what-is-a-personal-stream-anyways/).
\#WhatIsGlobalBaseline

#### Q: What is a global baseline? [q-what-is-a-global-baseline]

A: A *global baseline* is a baseline of a global configuration. Like all
baselines, it is immutable, and that means all of the configurations it
includes must also be baselines. A global stream can include both stream
and baseline contributions. When you create a global baseline, the
system can automatically recurse through the configuration hierarchy and
create baselines for the stream contributions. Alternatively, you can
create a [baseline staging stream](#WhatIsBaselineStagingStream) to
manually replace the stream contributions with the appropriate
baselines. \#WhatIsBaselineStagingStream

#### Q: What is a baseline staging stream and what is it for? [q-what-is-a-baseline-staging-stream-and-what-is-it-for]

A: A *baseline staging stream* is a special kind of global configuration
for the Configuration Lead to assemble a global baseline. As described
[above](#WhatIsGlobalBaseline), creating a global baseline automatically
creates baselines for any and all stream contributions in the global
configuration. That is not always feasible, especially in more complex
environments or hierarchies; the Configuration Lead might not have
permission to create all the baselines, and might not know whether every
stream is ready for baseline or has been baselined already.

The alternative is to create a baseline staging stream, which serves as
a temporary assembly area. The Configuration Lead can then coordinate
with contributing teams to locate or create the appropriate baselines to
replace each of the stream contributions. Once all baselines are in
place, the Lead can fully commit the global baseline. You can also
create a baseline staging stream from an existing global baseline, if
you need to replace one or more of its contributions with different
baselines due to error or recent changes. See also [Can I modify or
update a global baseline?](#ModifyGlobalBaseline).

**Note**: A baseline staging stream is **not** a working configuration
context for engineering teams to perform work or make changes. You might
set your configuration context to a baseline staging stream, for
example, to verify it includes the correct combination of baselines and
the cross-application links resolve as expected. However, the only type
of change that should occur in a baseline staging stream is to replace a
stream contribution with a corresponding baseline.

[ *Back to top* ](#TopOfList)

### Questions: Global configurations

\#WorkInLocalVsGlobalContext

#### Q: When should I work in a local or a global configuration context? [q-when-should-i-work-in-a-local-or-a-global-configuration-context]

A: If you are working in the context of a single project area in a
single ELM application, without any need to link to other project areas
or applications, you can work in a local configuration context. If you
need to link to artifacts in other project areas, in the same or other
ELM applications, you should work in the context of a global
configuration to ensure that those links resolve to the correct versions
of the artifacts. \#GCMultipleVersionsOfLocalConfig

#### Q: Can a global configuration include multiple versions of the same local configuration (for example, two different streams from the same RM project)? A: Yes, a global configuration can have multiple instances of a local configuration. However, including multiple instances that are different versions of the same configuration introduces component skew, which you typically would want to avoid. This is more likely to happen in nested product hierarchies, where the same configuration is used by more than one component in some larger assembly, but at different versions. [q-can-a-global-configuration-include-multiple-versions-of-the-same-local-configuration-for-example-two-different-streams-from-the-same-rm-project-a-yes-a-global-configuration-can-have-multiple-instances-of-a-local-configuration.-however-including-multiple-instances-that-are-different-versions-of-the-same-configuration-introduces-component-skew-which-you-typically-would-want-to-avoid.-this-is-more-likely-to-happen-in-nested-product-hierarchies-where-the-same-configuration-is-used-by-more-than-one-component-in-some-larger-assembly-but-at-different-versions.]

For example, the global configuration example below includes two
different versions of the `RM Stream` local configuration:

Global Configuration Prime RM Stream 2.0 QM Prime Stream Reusable
Component Global Configuration RM Stream 1.0 QM Stream 1.0

The system handles component skew by using the first instance of the
local configuration that it encounters in the global configuration
hierarchy (working down from the top). In the example above, when you
open DNG in the `Global Configuration Prime` context, the
`RM Stream 2.0` local configuration will load, since it is higher in the
hierarchy. To use a different local configuration, like `RM Stream 1.0`
in this example, reorder the hierarchy to make that configuration appear
first; in the example, you could move
`Reusable Component Global Configuration` above `RM Stream 2.0`. If
changing the hierarchy would impact other users, you could also choose
to work in a global configuration stream or baseline of the lower-level
component, for example, in the context of
`Reusable Component Global Configuration`, assuming that configuration
includes the artifacts you need.

The GCM application provides a utility to identify component skew. For
more information on troubleshooting component skew, see the topic
[Unexpected local configuration in the Current Configuration
menu](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.2/com.ibm.rational.gcapp.doc/topics/c_order_in_gc_hiers.html?lang=en)
in [IBM Knowledge
Center](http://www.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
\#NewComponentVsNewConfig

#### Q: When do I create a new component instead of a new configuration? [q-when-do-i-create-a-new-component-instead-of-a-new-configuration]

A: Create a new component when you are creating a new physical or
logical piece of your system: system a new part, module, or whatever.
Create a new configuration to revise or extend an existing part of your
system, such as a new version or variant.

For example, say you have an Automated Meter Reader offering for the US
market, defined by a global configuration, and you need a similar
offering for the UK market; you would create a new global configuration
from the US baseline and customize it for the new market. However, if
you wanted to add a new braille or audio interface to your Meter Reader,
you would likely need to create new components or project areas in each
local application (requirements, design, code, tests), with a
corresponding global configuration (component) that assembles those new
local contributions. You might still use that UK variant of your
Automated Meter Reader configuration, and add the new global component
to that configuration. You would then add the stream from that global
component to the appropriate variant stream of your Automated Meter
Reader component. \#GCBusinessRules

#### Q: Can I write business rules for global configurations? [q-can-i-write-business-rules-for-global-configurations]

A: Currently, global configurations have only one business rule: a
global baseline can only consist of global or tool-specific baselines
(that is, global baselines cannot include streams). Other than that,
there are no rules for creating global configurations.

The user must have a designated role to create a global configuration.
There is a separate permission for creating baselines, since this might
be given to a wider group of users involved in building the system. As
of version 6.0.1, you can define custom attributes, including tags, for
global configurations. Using the custom attributes and other
configuration data in LQE, you could write reports to validate business
logic. \#ModifyGlobalBaseline

#### Q: Can I modify or update a global baseline? [q-can-i-modify-or-update-a-global-baseline]

A: By definition, a baseline is immutable (unchangeable). You can't
change the content of a baseline, or the contributions included in a
global baseline. If you have appropriate permissions, you can modify the
name and some attributes of the global baseline. To change the content,
you must create a new baseline.

If you need to replace only a handful of contributions, for example due
to error or recent changes, it can be expedient to generate a [baseline
staging stream](#WhatIsBaselineStagingStream) from an existing global
baseline. You can then simply substitute the desired baseline
contributions for the existing contributions, and commit the new global
baseline.

**Note:** The only changes made in the baseline staging stream are to
substitute the baseline contributions. Engineering teams should never
make changes in the context a baseline staging stream. Instead, they
would make changes in a working configuration context, and then generate
the appropriate baselines to be substituted into the baseline staging
stream. \#StabilizeWorkingStream

#### Q: How do I stabilize my global working stream leading up to a release milestone? [q-how-do-i-stabilize-my-global-working-stream-leading-up-to-a-release-milestone]

A: As you get closer to a milestone or release boundary in your
development lifecycle, It is common practice to stabilize the delivery
stream by progressively freezing components as they complete. Because
global configuration streams can include both baseline and stream
contributions, you can easily replace the stream contributions in your
working configuration context with baselines as each component freezes.
For example, you might replace a requirements stream contribution with a
baseline, while users continue to work in their testing stream in that
global configuation; your requirements team could work ahead either in a
local configuration or a parallel global configuration for the next
iteration.

Alternatively, you could create a stabilization global configuration for
continuing work on the upcoming milestone, while teams that are finished
continue to work in the original configuration context. If appropriate,
you can assign the stabilization or work-ahead global configuration to a
dedicated team area for the specific subset of users who will work in
it.

**Note:** You should never use a [baseline staging
stream](#WhatIsBaselineStagingStream) in place of a stabilization
stream. Engineering teams should never make changes in the context of a
baseline staging stream.

[ *Back to top* ](#TopOfList)

### Questions: Managing streams and baselines

\#CreateNewStream

#### Q: When do I create a new stream? [q-when-do-i-create-a-new-stream]

A: Your organization should define an overall strategy for when to
branch a new stream, as well as when to take baselines, at both the
local and global configuration level. Your strategy will depend on your
development practices and your goals. For example:

-   To enable parallel development of future items before your current
    release is complete, you could create a new stream based on the most
    recent baseline of your current stream. You continue to work on the
    current stream until that release is complete, and determine which
    changes to deliver across the current and future streams.
-   Alternatively, to avoid parallel development and merging, you could
    wait until the current release is complete before creating the new
    stream for the next release, although that might slow ongoing
    development.
-   You could even baseline the current stream when the release is
    complete, and then rename it to continue using it for your new
    current release; in this case, ensure you are very clear on naming
    conventions and usage so that teams are always clear on which stream
    to use.

You might also need to consider when to create new branches for
maintenance releases, depending on when that work needs to start. If you
start before the current release is complete, you will need to deliver
changes from the current stream to the maintenance stream. During
maintenance, you would need to determine which changes should be
delivered back to the new current release. You might have one or
multiple maintenance streams, again depending on whether you work on
maintenance releases sequentially or in parallel with each other. In
general, create a new stream only when necessary and when you are ready
to start working in it; minimizing the number of concurrent work streams
reduces the complexity of delivering across multiple streams.
\#StreamsCopyOrReference

#### Q: Are the artifacts in each stream copies of each other? [q-are-the-artifacts-in-each-stream-copies-of-each-other]

A: No, they are either true parallel variants, or different time-based
versions, or the same versions reused by reference.
\#ViewHistoricalBaseline

#### Q: When I go to a historical baseline, do I need to use a previous version of the application to view it? [q-when-i-go-to-a-historical-baseline-do-i-need-to-use-a-previous-version-of-the-application-to-view-it]

A: When you upgrade the ELM applications, your baselines are migrated
along with your other data, so you can view them in your current product
version.

[ *Back to top* ](#TopOfList)

### Questions: Linking artifacts and resolving links

\#DirectionalLinkingExplained

#### Q: What does directional linking or no back links mean? A: In projects that do not enable configuration management, when you create a link between artifacts, both artifacts store a link property: a link and a back link, if you will, although it is not explicitly stated which is the link and which is the back link. With configuration management and versioned artifacts, maintaining both link and back link becomes extremely challenging, especially across applications. [q-what-does-directional-linking-or-no-back-links-mean-a-in-projects-that-do-not-enable-configuration-management-when-you-create-a-link-between-artifacts-both-artifacts-store-a-link-property-a-link-and-a-back-link-if-you-will-although-it-is-not-explicitly-stated-which-is-the-link-and-which-is-the-back-link.-with-configuration-management-and-versioned-artifacts-maintaining-both-link-and-back-link-becomes-extremely-challenging-especially-across-applications.]

As a result, the linking model for configuration-management-enabled
projects has changed: for each link type, there is a source or owner
application or artifact, and a target. The source artifact stores the
link as a property, and its application feeds the link information to
the Link Index Provider (LDX). The target artifact does not store or
modify any property for the link (no back link); its application queries
LDX for incoming links for the artifact, and displays them in the UI as
if they were properties. This is true for all OSLC link types; for a few
link types that are internal to an application, the application may
continue to store back links. For more details on directional linking,
see [this blog
post](https://fryerk.wordpress.com/2020/01/13/elm-directional-linking-with-cm-enabled/).

For the ELM application user, these changes should be transparent. She
can create links to and from artifacts as before, and the links continue
to display as before; whether the link information is stored with the
artifact or retrieved from the link index provider is not material. What
might affect the end user is when a link resolves correctly in one
configuration, but not in another because an artifact is missing. That
scenario is addressed in the questions below.
\#ExistingLinkToArtifactOutsideGC

#### Q: What happens when my artifact links to an artifact that is not included in my current global configuration? A: For the link to exist, it must have been created either before configuration management was enabled in the project, or at a time when both artifacts were included in a global configuration. The scenario could occur for several reasons: [q-what-happens-when-my-artifact-links-to-an-artifact-that-is-not-included-in-my-current-global-configuration-a-for-the-link-to-exist-it-must-have-been-created-either-before-configuration-management-was-enabled-in-the-project-or-at-a-time-when-both-artifacts-were-included-in-a-global-configuration.-the-scenario-could-occur-for-several-reasons]

1.  Your global configuration is missing the configuration or component
    the artifact belongs to.
2.  The missing artifact is included in a different version or variant
    of the global configuration where the link was created (for example,
    a previous release), but is not in the current version of the
    configuration.
3.  The missing artifact is in a project area or application that does
    not enable configuration management. Linking behavior between
    enabled and non-enabled containers is described in [What happens if
    I enable only one of my linked DOORS Next or ETM
    projects?](#EnableOnlyOneLinkedProject).

You can only observe this scenario from a source artifact (one that owns
the link in question). If the artifact that is not part of the
configuration is the target of the link, it shows no indication that the
link exists. The source artifact shows some version of the link text,
but you cannot preview or open a linked artifact that is not in the
configuration; an error occurs or the link does not resolve correctly.
In RTC, if the configuration context is not defined (the attribute
mapping or release association is missing), the link resolves to the
artifact in the [default stream](#WhatIsDefaultStream) if it exists in
that stream; otherwise, it gives an error.

To correct this problem, delete the link if it isnt needed, or ensure
that the artifact is included in the referenced configurations, and the
correct set of configurations are included in the global configurations.
\#AddLinkToArtifactOutsideGC

#### Q: What happens when I try to link to an artifact in a component not included in my current global configuration? [q-what-happens-when-i-try-to-link-to-an-artifact-in-a-component-not-included-in-my-current-global-configuration]

A: For DOORS Next, ETM, and RMM, if you are in a configuration-enabled
project, you can only create links to artifacts within your current
configuration context. If you try to link to an artifact outside your
current global configuration, you will get an error.

When you create link from artifacts in those applications to work items
in EWM, you can clear the check box that shows only work items within
the global configuration context and then link to any work item;
however, these links may not resolve correctly in future. When you
create a link from EWM, if the global configuration context isnt
specified (the attribute or release mapping is missing), you can link to
artifacts outside of the configuration context, but only to artifacts in
the [default stream](#WhatIsDefaultStream). For more information on
linking between work items and versioned artifacts, see [this Jazz.net
article](https://jazz.net/library/article/92499). \#LinkToNonCLMApp

#### Q: Can I create a link from a versioned artifact to a non-ELM application? [q-can-i-create-a-link-from-a-versioned-artifact-to-a-non-elm-application]

A: Yes, if the other application provides some level of support for
configuration management. The application must register as an OSLC
provider or consumer, and set the globalConfigurationAware property in
its service provider document; if that property is not set, the ELM
applications assume no support for configuration management. If the
application has no support for configuration management, you cannot
create links from configuration-enabled DOORS Next, ETM, or RMM project
areas to that application.

Because EWM work items are not versioned, you can create links between
work items and other applications that support OSLC, whether or not they
support configurations. To determine whether your non-CLM application
supports configuration management, contact the application provider.
More information on enabling applications is included in the
\[\[<http://open-services.net/specifications/configuration-management/>\]\[OASIS
OSLC Configuration Management specification\] (draft) and the Jazz.net
article on [Enabling your application to integrate with
configuration-management-enabled CLM
applications](https://jazz.net/wiki/bin/view/Deployment/IntegratingWithConfigurationManagementEnabledCLMApplications).
\#ExistingNonCLMLinkWOCfgM

#### Q: What happens to existing links to a non-ELM application that does not support global configurations (e.g. earlier versions of DOORS)? A: This situation happens if you enable an existing ELM project area that has links to the non-ELM application. The link to the ELM artifact continues to appear in the non-ELM application; the link resolves to the version of the artifact in the default configuration. [q-what-happens-to-existing-links-to-a-non-elm-application-that-does-not-support-global-configurations-e.g.-earlier-versions-of-doors-a-this-situation-happens-if-you-enable-an-existing-elm-project-area-that-has-links-to-the-non-elm-application.-the-link-to-the-elm-artifact-continues-to-appear-in-the-non-elm-application-the-link-resolves-to-the-version-of-the-artifact-in-the-default-configuration.]

If the ELM artifact owns the link, the link also continues to appear in
the ELM application. When you follow that link, it continues to resolve
as it did before, to the single non-versioned artifact in the non-ELM
application.

As mentioned in [the previous question](#LinkToNonCLMApp), you cannot
create new links between versioned artifacts (in DOORS Next or ETM) and
artifacts in applications that do not support configurations. You can
still link from those applications to artifacts in non-enabled project
areas and to EWM work items. Note: As of DOORS 9.7, you can link from
versioned ELM artifacts to DOORS requirements; those links are visible
only on the ELM artifact. In a coming DOORS release, those links will
also be visible in the DOORS artifact. DOORS does not contribute to
global configurations. \#ExistingLinksInNewLocalConfig

#### Q: When I create a new local configuration, will the existing links become inconsistent or unresolvable? [q-when-i-create-a-new-local-configuration-will-the-existing-links-become-inconsistent-or-unresolvable]

A: The new local configuration inherits the set of artifact links from
the baseline from which the stream was created; that is, the new stream
will use the same set of versions of the artifacts as the baseline,
including their existing links.

However, these links will not resolve (and if the artifacts do not own
the links, the links will not even display) if the new local
configuration is not part of a global configuration that includes the
artifacts on the other end of the links. To resolve the links, you need
to include the new configuration, as well as configurations containing
the linked artifacts, in a global configuration, and set your context to
that global configuration.

It is the configuration leads responsibility to ensure that each global
configuration has meaningful contributions from each component, and it
is the users responsibility to ensure that links are meaningful in that
context. \#LinkHistory

#### Q: If I delete a link and then link to another artifact, what happens to the history of the link to the previous artifact? [q-if-i-delete-a-link-and-then-link-to-another-artifact-what-happens-to-the-history-of-the-link-to-the-previous-artifact]

A: Links are part of the versioned state of an artifact, so previous
links can be seen in previous versions of the artifact. You can use
previous global baselines to navigate through links as they were at the
time of that baseline. Individual tools may also offer ways to visualize
the history of artifacts and the changes made to them.
\#CreateLinksFromBaseline

#### Q: I cannot link from a baseline. This seems like a limitation. Is there a way around this? [q-i-cannot-link-from-a-baseline.-this-seems-like-a-limitation.-is-there-a-way-around-this]

A: Many kinds of links, such as traceability links, are an important
part of the semantic content of an artifact. Baselines are intended to
be non-editable, so you arent able to change the content of the artifact
in the baseline.

However, with directional links, only the source (or link owning
artifact) stores the link information; the target artifact does not
store the link as an attribute, but queries the link index provider on
request (see [What does directional linking or no back links
mean?](#DirectionalLinkingExplained) for details on directional
linking). The defined link directions take into account the likely order
of artifact baselines: for example, requirements are typically baselined
before test development and execution, so ETM artifacts own and store
links to DOORS Next artifacts. Thus, you can create a new link from an
ETM test artifact in a stream to a DOORS Next artifact in a baseline,
without modifying the DOORS Next artifact resource representation. If
the ETM artifact is part of a baseline, you could not save the new link
property. \#WhyLinksChangeInBaselines

#### Q: If baselines are not editable, why do links and link validity indicators sometimes change in my baseline? [q-if-baselines-are-not-editable-why-do-links-and-link-validity-indicators-sometimes-change-in-my-baseline]

A: See the [answer above](#CreateLinksFromBaseline): Because links are
directional, only the source (or owning) artifact stores the link
information. The target artifact does not change, but uses the link
index provider to determine relationships. Link directions take into
account the likely order of baselines, so that artifacts that tend to
complete later in the lifecycle (like test artifacts) store the links to
artifacts that tend to be baselined earlier (like requirements). Thus,
you can link from an ETM test artifact to a DOORS Next baselined
requirement because the DOORS Next artifact does not store the link
relationship and does not change. For more details on directional
linking, see [What does "directional linking" or "no back links"
mean?](#DirectionalLinkingExplained).

Similarly, link validity is determined by a service. Validity is not
stored as a property of the artifact resource; when the application
renders the artifact, it queries the link validity service for the
appropriate values to display. The baselined artifact does not change.
\#AttributesForLinkValidity

#### Q: What attributes are used to determine link validity? [q-what-attributes-are-used-to-determine-link-validity]

A: For DOORS Next, any change to predefined or custom properties
(including the primary artifact content) causes the links to and from
that artifact to become suspect. For ETM, a few attributes do not affect
link validity (between ETM and DOORS Next artifacts), since they do not
inherently change the test artifact content: Priority, Risk, Review
State, Weight, Lock, Estimate, Owner, Creator, and test script content.
At this time, you cannot select which attributes to use when determining
link validity. The validity service currently applies only to link types
used between requirements; between requirements, models, and test
artifacts; and between source code files. \#TraceabilityLinksSCM

#### Q: Can I create links between files under EWM source control to other versioned artifacts (like requirements and test artifacts)? [q-can-i-create-links-between-files-under-ewm-source-control-to-other-versioned-artifacts-like-requirements-and-test-artifacts]

A: As of version 6.0.3, you can create a link from a file under EWM
source control to another versioned artifact, including other source
files, requirements in DOORS Next, and test artifacts in ETM. To create
the link, you must use the EWM client and set the configuration context
to a global configuration that includes configurations for both source
and target artifacts, as described in the IBM Knowledge Centre topic
[https://www.ibm.com/support/knowledgecenter/en/SSYMRC_6.0.6.1/com.ibm.team.scm.doc/topics/t_scm_eclipse_trace.html](Linking EWM source files to ELM artifacts).
The links resolve only in the correct configuration context. Currently,
ETM artifacts display the links to source files, but DOORS Next
artifacts do not.

[ *Back to top* ](#TopOfList)

### Questions: Managing and delivering change

\#ChangeSetsCopiedOnDelivery

#### Q: When I merge or deliver changes across streams, are the change sets physically copied to the receiving stream? [q-when-i-merge-or-deliver-changes-across-streams-are-the-change-sets-physically-copied-to-the-receiving-stream]

A: Artifacts are used by reference, not by copy. Delivering change sets
(in DOORS Next) or merging changes across streams (in ETM) does not copy
artifacts, but instead updates the target configuration to point to
different versions of the affected artifacts. \#ChangeMgmtForReqts

#### Q: How can I improve change management of my requirements? [q-how-can-i-improve-change-management-of-my-requirements]

A: DOORS Next offers several capabilities to better manage changes to
requirements, including change sets, linking change sets to change
requests, and user roles and permissions.

Create change sets (from the configuration context menu or Manage
Configurations view) to group or separate sets of related changes for
better tracking and easier delivery across streams, and to isolate
changes from the main stream until they are ready to deliver. You can
mandate that all changes be made inside a change set by setting an
option for each stream.

You can also require that users associate change sets with an approved
change request before allowing delivery. This option is also set for
each stream. If you set this option, if a change set is not linked to a
change request, or the change request is not approved, the change set
cannot be delivered. The change request can reside in any system (there
is no restriction on configuration management support in this isolated
case), and the change request system defines the criteria for approval.

Users must have the appropriate permissions to create and deliver change
sets their own, as well as those of other users. You can limit those
permissions as needed, for example, restricting the ability to deliver
changes to a small group, or only the team lead. \#DoINeedChangeSets

#### Q: Do I have to create a change set to make a change in DOORS Next? [q-do-i-have-to-create-a-change-set-to-make-a-change-in-doors-next]

A: Not necessarily, but we recommend using explicit change sets in most
cases. If you do not explicitly create a change set from the
configuration context menu or Manage Configurations view, each change
that you make creates its own implicit change set, which is delivered to
the stream immediately when you save. For example, deleting or moving an
artifact creates an implicit change set; editing an artifact creates an
implicit change set with whatever changes you made in that edit session.
The creation and delivery of the implicit change sets is transparent to
the user. When you deliver change sets across streams, you can see the
implicit change sets and deliver those changes. The drawback is that the
list of implicit change sets can be very long, since the changes are
very granular, and the names generated by the system are not very
descriptive (for example, Edit artifact 916). You can set an option for
each stream to mandate creating a change set for any changes.
\#WhenExplicitChangeSets

#### Q: When should I use explicit change sets in DOORS Next? [q-when-should-i-use-explicit-change-sets-in-doors-next]

A: Use explicit change sets to better track and manage requirements
change, as well as to group (or separate) sets of related changes, and
especially if you expect to deliver changes across configurations. In
most cases, using explicit change sets, with a well-defined naming
convention, is a good idea. If you want to enforce explicit change sets,
you can set an option for the individual stream that prevents any change
outside of a change set.

If you do not explicitly create a change set, each change you make
creates its own implicit change set, with a very simple system-generated
name, as described in the question above. When you deliver across
streams, you then see a long list of change sets and it is difficult to
determine which changes you want to deliver.

Creating a change set allows you to group a set of changes together, as
well as to keep your changes separate from the main stream until you are
ready to share them. In a team environment, several members might have
their own change set in order to work in parallel (there are merge
capabilities should conflict arise). When you need to deliver across
configurations, your naming convention and grouping strategy should make
it easier to identify the required change sets.

You might choose NOT to use explicit change sets if you are starting a
new project, if changes are minimal and will be discarded or never
reused, or if you know ALL changes will be delivered across
configurations and you dont need to track them individually.

[ *Back to top* ](#TopOfList)

### Questions: Reporting on configurations

\#HowIsReportingDifferent

#### Q: How is reporting on configuration-enabled projects different from reporting on non-enabled projects? [q-how-is-reporting-on-configuration-enabled-projects-different-from-reporting-on-non-enabled-projects]

A: For interactive reporting on configuration-enabled projects, use the
Report Builder in Jazz Reporting Service with the "Lifecycle Query
Engine scoped by a Configuration" data source. (In some versions, this
data source is called "Lifecycle Query Engine using Configurations".)
The LQE data source recognizes versioned data, but the ELM data
warehouse does not. With configuration-enabled reporting, reports are
run in the context of a configuration, usually a global configuration,
which determines which versions of artifacts to include in the report.
You can also use the Lifecycle Query Engine scoped by a Configuration
data source with IBM Engineering Lifecycle Optimization - Engineering
Insights (ENI, formerly known as RELM).

For DOORS Next and ETM project areas, enabling configuration management
stops all feeds to the ELM data warehouse, and archives the existing
project data in the warehouse. Business Intelligence and Reporting Tools
(BIRT), Rational Reporting for Development Intelligence, and dashboard
reports or widgets that use the data warehouse will not work for enabled
DOORS Next or ETM project areas.

EWM does populate the data warehouse, but that data does not include
configuration-related information. For versioned data, you must replace
existing reports with new ones that use the Lifecycle Query Engine data
source. RMM contributes data only to LQE.

To generate documents, you can continue to access versioned data by
reportable REST APIs, using built-in, template-based reporting in the
ELM application or by using IBM Engineering Lifecycle Optimization -
Publishing (PUB, formerly known as RPE). You can add configuration
context to existing PUB templates. The built-in document generation uses
the current configuration context. You can also export reports from
Report Builder to PUB. For more information on reporting, see the
Jazz.net article on [Getting started with reporting by using LQE data
sources 6.0.6.1](https://jazz.net/library/article/92649). (Previous
articles exist for eariler ELM versions.)

[ *Back to top* ](#TopOfList)

##### Related topics: \* [Recommended ALM deployment topologies for 6.x](RecommendedALMDeploymentTopologies6) [related-topics-recommended-alm-deployment-topologies-for-6.x]

-   [Best practices for CLM Usage Models: Global configuration
    management](CLMUsageModelBestPractices#Global_Configuration_Management)
-   [Enabling your application to integrate with
    configuration-management-enabled CLM
    applications](IntegratingWithConfigurationManagementEnabledCLMApplications)

##### External links: [external-links]

-   [Welcome to configuration
    management](https://jazz.net/library/article/1492)
-   [IBM ELM Knowledge
    Center](http://www.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html)
-   [OASIS OSLC Configuration Management specification
    (draft)](http://open-services.net/specifications/configuration-management/)

##### Additional contributors: Main.NickCrossley, Main.RosaNaranjo [additional-contributors-main.nickcrossley-main.rosanaranjo]
