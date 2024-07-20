META:TOPICINFO{author="paulellis" date="1380882286" format="1.1"
reprev="1.2" version="1.2"}
META:TOPICPARENT{name="UpgradingRequirementsComposerFrom2To3"}

# Mapping RRC2 data to RRC3 data format [mapping-rrc2-data-to-rrc3-data-format]

DKGRAY Authors: Main.ShirleyHui Build basis: CLM 2011, Rational Team
Concert 3.0.1, Rational Requirements Composer 3.0.1ENDCOLOR

TOC{title="Page contents"}

This article explains differences between RRC2 and RRC3 data, and the
impact of those differences when migrating RRC2 data into RRC3 format.BR

Refer to [Upgrade Reference for CLM
2011](https://jazz.net/library/article/698) for overall guidance on
upgrading.BR

Rational Requirements Composer 3.0.1 was a large and significant
release, providing requirements management capability in addition to
requirements definition. It is fully aligned with Rational's CLM
solution. These changes have an impact on migrating data from RRC2. It
is important to understand how RRC2 data is mapped into RRC3 format.BR

One of the notables differences between RRC2 and RRC3 is the type
system. RRC3 introduces an administratively defined, reusable type
system which replaces the less structured RRC2 attribute groups.BR

## [Type system differences](#SectionA)

-   [Type Representation](#SectionA1)
-   [Type History](#SectionA2)
-   [Mapping Attribute Groups to Artifact Types](#SectionA3)

## [Other Differences](#SectionB)

-   [Saved Filters](#SectionB1)
-   [Content Links versus Traceability Links](#SectionB2)
-   [Project Archives and Project Templates](#SectionB3)

\#SectionA

## Type system differences

\#SectionA1

### Type Representation

The RRC2 type system was not designed to support attribute re-use.
Attributes with the same name and attribute type in different attribute
groups are not shared. The RRC3 type system supports attribute re-use.
While an RRC3 type system cannot be represented in RRC2, the RRC2 type
system can be transferred into RRC3. However, an RRC2 type system will
commonly contain multiple copies of a logical attribute - attributes
with the same name - but may or may not be the same type. In order to
handle all possible cases, we were forced to adopt a simplified strategy
for handling this multiplicity. The RRC2 type system is mapped into an
RRC3 type system with no attempt at attribute re-use. Some features of
this approach are:BR

-   the RRC2 type system is represented as-is in RRC3
-   an instance of every 'copy' of the RRC2 attribute is created
-   the type-system 'looks' very similar to that in RRC2

A side-effect of this approach is that because RRC2 allows multiple
copies of the same logical attribute definition to share the same title,
we have the potential of multiple RRC3 attribute definitions sharing the
same title. To disambiguate the titles of these type resources, we
introduced a naming convention derived from the attribute group and
attribute names. The project administrator may change the names after
the migration.

For example, in RRC2, if you have two AttributeGroups entitled
CommonAttributes and BetaReleaseAttributes which both define an
AttributeDefinition entitled Priority, the following type resources are
generated during the upgrade:

-   Two ArtifactTypes entitled CommonAttributes and
    BetaReleaseAttributes
-   Two AttributeDefintions entitled CommonAttributes / and
    BetaReleaseAttributes / Priority
-   Two AttributeTypes entitled CommonAttributes / PriorityType and
    BetaReleaseAttributes / PriorityType

BR

\#SectionA2

### Type history

A simple, unambiguous approach is employed to map types and resources of
each type from RRC2 to RRC3:

-   Type resources will have no historical revisions. Only the most
    recent representation of the type is created in RRC3.
-   All revisions of a resource will be represented using its underlying
    type.

The effect of this is that when a resource is viewed at a point-in-time
it will not necessarily display the same attributes that it would have
in RRC2 - this does not mean that there is data loss - only the
specification of the resource has changed and all the original data is
still retained.

This is also true for baselines.

Type system refactoring in RRC2 was not supported. However, changes to
attribute groups was allowed. New resources used the attributes defined
at that moment in the attribute group, but old resources were not
required to change. The old resources did not match the current
representation of the attribute group. The same will be true in RRC3.

BR \#SectionA3

### Mapping Attribute Groups to Artifact Types

The RRC2 type system is converted to RRC3 in the following way:BR

-   An RRC2 attribute group is converted to an RRC3 artifact type.
-   During migration an artifact is assigned an artifact type based on
    the attribute group(s) formerly associated with it. The mapping does
    **not** use the RRC2 type (e.g., Actor, Use Case, Use Case Diagram,
    Business Process Diagram, also known as the mime-type).
-   If there is one attribute group assigned to a resource, the RRC3
    resource is assigned the artifact type created based on the
    attribute group.
-   If an artifact does **not** have any attribute group assigned to it,
    it is assigned the default RRC3 **Requirement** artifact type.
    -   For example, RRC2 Actors and Use Cases without any attribute
        group will be assigned to the generic *Requirement* artifact
        type. BRIn RRC3 you cannot tell if the artifact was originally
        an RRC2 Actor or Use Case.
-   A RRC2 artifact may have multiple attribute groups applied to it.
    -   If a resource has multiple attribute groups assigned to it, an
        artifact type that represents the combination of the attribute
        groups is created and assigned to the resource.
    -   The name of the attribute group is a combination of the
        individual attribute groups.
        -   For example, artifact A has attribute groups AG1 and AG2. In
            RRC3, the project will have a new artifact type called
            AG1+AG2 and is applied to Resource
    -   Artifacts of the same mime type, for example, Actor, with
        different attribute groups assigned to different artifacts, will
        result in artifacts of different artifact types.BR
        -   For example, Actor A has attribute groups AG3 and AG4 and
            Actor B has attribute group AG4 and AG5. BR In RRC3, the
            project will have 2 new artifact types, AG3+AG4 and AG4+AG5.
            BR Actor A will have artifact type AG3+AG4 and Actor B will
            have artifact type AG4+AG5.

If you do not wish to see the default transforms, you may change the
migration behavior by changing the RRC2 data prior to migration. We
highly recommend that you perform a trial upgrade to understand the
attribute group to artifact type mappings.

There are 2 ways to modify the RRC2 data prior to migration:BR

-   If your artifacts do not have any attribute groups applied to them,
    and you wish to distinguish their original RRC2 type:
    -   For each RRC2 type, create an attribute group (e.g. an Actor
        attribute group, no attribute definitions) and apply it to all
        artifacts of that type.
    -   Accomplish this task by using the RRC2 ClientAPI to associate
        attribute groups with each resource by mapping from their Mime
        Type.
-   Use the AttributeGroupTool to modify the RRC2 data
    -   This tool creates an attribute group for each of the RRC2 types
        (also known as mime-types). If an attribute group is already
        present with the correct name, it uses it. It assigns the
        attribute group to all artifacts of that type.
    -   This tool is available on the Diagnostic Tool Portal. Contact
        IBM Support.
    -   After running this tool on the RRC2 data, proceed with the trial
        RRC3 upgrade.
    -   Confirm that artifacts have the expected artifact type.

\#SectionB

## Other Differences

\#SectionB1

### Saved Filters

#### Saved Filter Representation

A best-effort has been made to re-represent RRC2 Saved Filters using the
significantly more powerful RRC3 View mechanism. There are however a few
instances where the original intention of the RRC2 SavedFilter cannot be
represented:BR

-   when the filter refers to notions that are not represented in RRC3.
    For example, RRC2 mime types are not represented in RRC3. Filters
    depending on them will not work.
-   when the filter refers to a resource that may be mapped to a new
    representation. For example, attribute groups are changed to
    artifact types. The filters are not modified.

#### Saved Filter History

Only the current revision of the Saved Filter is migrated but this
revision should be visible in all baselines.

BR \#SectionB2

### Links

In RRC2 there are artifact-to-artifact links and content links. RRC2
does not support traceability links.BR

RRC3 supports content links and traceability links.BR

Trace links are created only for artifact-to-artifact links that existed
in RRC2, and only on the current revision (i.e. not for past
revisions).BR

Trace links are not created from content links. This includes embedded
links, and links created by drag and drop. Content links are migrated as
is.BR

Consider how did your users create links in RRC2? Did they use drag and
drop? The concept of traceability is formalized in RRC3. Some link
relationships that were created from drag and drop were considered
content links. In RRC3 they will be content links, not traceability
links.BR

If you require formalized links, use the FixLinks tool to convert
content links to traceability links.BR

The FixLinks tool is available via the IBM Support Diagnostic Tool
Portal. Contact IBM Support to request the tool.

BR

### Tool to convert content links to traceability links

Content links will be created if the following criteria are met:

1.  The target of the links is a resource within this repository 2. The
    target resource exists - i.e. it responds to HEAD or GET 3. A link
    to the resource does not already exist 4. The link type is simple -
    i.e. the upgrade hasn't identified it as being 'special'

Restrictions

1.  The FixLinks tool does not handle graphical content. 2. We don't
    create links to Terms

Notes

1.  The created, creator, modified, and contributor attributes will
    correspond to the resource in which the links are found. There is no
    way to determine who created the links and when they were
    created. 2. The tool will not create duplicate links. The tool can
    be run repeatedly.BR \*Note:there is a known problem that causes a
    Null Pointer Exception when there are a large number of links to
    create. You can re-run the tool repeatedly until all links are
    created. 3. We create .csv report containing all the newly created
    links; this can be used for further analysis

BR \#SectionB3

### Migrating RRC2 Project archives and RRC3 Project templates

In RRC2, users were able to use a project archive as a template for
other projects by uploading the archive into a new project. The ability
to create projects based on other projects has been formalized in RRC3
as project templates. During the RRC2 migration, the out-the-box RRC3
project templates are added.BR

In order to migrate RRC2 project archives:

1.  Prior to migration, the user should upload the project archives that
    are required to be migrated into temporary projects. 2. Perform the
    migration. 3. After migration, the user should review each of the
    uploaded projects that were derived from RRC2 project archives. 4.
    Use the create template feature from the Templates tab in Manage
    Project Properties to create RRC3 project templates. 5. The user may
    delete the temporary projects.

BR

## References

\* [Create a tool for converting content links to traceability links
(51637)](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=51637)
\* [Creating traceability and content links in
RRC3](http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/index.jsp?topic=2Fcom.ibm.rational.rrm.help.doc2Ftopics2Ft_work_links.html)

BR

##### Related topics: [Limitations](UpgradingRequirementsComposerFrom2To3#SectionR1), [Understanding the data transformations](UnderstandingTheDataTransformations), [Running a trial migration](UpgradingRRCRunningaTrialMigration), [Perform backups before offline and online migration steps](UpgradingRequirementsComposerFrom2To3#SectionR4), [Online migration error handling](UpgradingRequirementsComposerFrom2To3#SectionR5), [Review the migration results](UpgradingRRCReviewTheMigrationResults) [related-topics-limitations-understanding-the-data-transformations-running-a-trial-migration-perform-backups-before-offline-and-online-migration-steps-online-migration-error-handling-review-the-migration-results]

##### External links: [external-links]

-   [Upgrade Reference for CLM
    2011](https://jazz.net/library/article/698)

##### Additional contributors: Main.PaulEllis [additional-contributors-main.paulellis]

META:TOPICMOVED{by="paulellis" date="1380807425"
from="Deployment.Understandingthedatatransformations"
to="Deployment.UnderstandingTheDataTransformations"}
