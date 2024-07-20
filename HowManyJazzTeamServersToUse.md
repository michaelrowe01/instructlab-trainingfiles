META:TOPICINFO{author="sbeard" date="1394678124" format="1.1"
version="1.9"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Determining how many Jazz Team Servers to use DKGRAY Authors: Main.MichelleDeArmas Build basis: The Rational solution for Collaborative Lifecycle Management (CLM) and the Rational solution for systems and software engineering (SSE) [determining-how-many-jazz-team-servers-to-use-dkgray-authors-main.michelledearmas-build-basis-the-rational-solution-for-collaborative-lifecycle-management-clm-and-the-rational-solution-for-systems-and-software-engineering-sse]

ENDCOLOR

TOC{title="Page contents"}

This topic will help you decide how many Jazz Team Servers to deploy and
how to distribute applications among them.

## Jazz Team Server options

A Jazz Team Server that has more than one application connected to it is
considered to be a shared server. Using a shared Jazz Team Server for
multiple applications has these advantages:

-   Central user and license administration
-   Lifecycle project administration
-   Improved web-application navigation between applications
-   A common data warehouse
-   Fewer administration and configuration duties

Use a single, shared Jazz Team Server in these circumstances:

-   When all users and groups are aligned in a single authentication
    realm.
-   When all applications are centrally managed.

All of the example departmental and enterprise topologies illustrate the
use of a single, shared Jazz Team Server for multiple distributed
applications. However, in some conditions, the use of more than one Jazz
Team Server might be preferable.

Use separate Jazz Team Servers in these circumstances:

-   When users of different applications must be isolated
-   When separate authentication realms are used. Each authentication
    realm must have its own Jazz Team Server because user identities are
    based on the user accounts in an authentication realm.
-   When applications would otherwise be widely distributed from the
    Jazz Team Server, thus resulting in performance degradation.

**Restrictions:**

-   After an application is connected to a Jazz Team Server, the
    application cannot be connected to a different Jazz Team Server.
-   Two instances of the Requirements Management (RM) application cannot
    share the same Jazz Team Server. If you have multiple instances of
    the RM application, deploy them on separate application servers,
    each with its own Jazz Team Server.

##### Related topics: [Deployment planning: Where to start?](DeploymentPlanning) [related-topics-deployment-planning-where-to-start]

##### External links: \* None [external-links-none]

##### Additional contributors: None [additional-contributors-none]
