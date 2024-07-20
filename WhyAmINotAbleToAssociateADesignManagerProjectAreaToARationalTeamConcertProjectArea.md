META:TOPICINFO{author="sbagot" date="1432735933" format="1.1"
version="1.17"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandSoftwareArchitectExtforDesignMgt"}

# Why can't I associate a Design Manager project area to a Rational Team Concert or Rational Quality Manager project area? DKGRAY Authors: IntegrationsTroubleshootingTeam [why-cant-i-associate-a-design-manager-project-area-to-a-rational-team-concert-or-rational-quality-manager-project-area-dkgray-authors-integrationstroubleshootingteam]

Build basis: IBM Rational Team Concert or Rational Qualitiy Manager
4.0.x and later, IBM Rational Software Architect Extension for Design
Management 4.0.x and later ENDCOLOR

TOC{title="Page contents"}

This page describes what to do if you cannot add an association to a
Rational Software Architect Extension for Design Management project from
a Rational Team Concert or Rational Quality Manager project area.

## Initial assessment

### Symptoms

-   When you try to add an association to a Rational Software Architect
    Extension for Design Management project from a Rational Team Concert
    or Rational Quality Manager project area, you receive the error:
    Failed to read matching artifact container catalog resource.

### Impact/scope

-   Does it affect all the administrators of Rational Team Concert or
    Rational Quality Manager project areas who want to associate their
    project to an existing Design Manager project area?

## Data gathering and subsequent analysis steps

-   Verify the friendship information in the Jazz Team Server admin and
    Change and Configuration Management (CCM) admin page, or in the Jazz
    Team Server and Rational Quality Manager admin page.
    -   Jazz Team Server admin:
        `https://HostName:PortNumber/jts/admin#action=jazz.viewPage&id=com.ibm.team.repository.server`
        -   **Consumers (inbound):**
            `https://HostName:PortNumber/jts/admin#action=com.ibm.team.repository.admin.configureOAuth`
            -   Note the consumer name (ccm rootservices) key
                information
            -   Note the consumer name (qm rootservices) key information
    -   CCM admin:
        `https://HostName:PortNumber/ccm/admin#action=jazz.viewPage&id=com.ibm.team.repository.server`
        -   **Friends (outbound):**
            `https://HostName:PortNumber/ccm/admin#action=com.ibm.team.repository.admin.friends`
            -   Note the Design Management (/dm) friend - OAuth Consumer
                Key information
    -   Quality Management (QM) admin:
        `https://HostName:PortNumber/qm/admin#action=jazz.viewPage&id=com.ibm.team.repository.server`
        -   **Friends (outbound):**
            `https://HostName:PortNumber/qm/admin#action=com.ibm.team.repository.admin.friends`
            -   Note the Design Management (/dm) friend - OAuth Consumer
                Key information

## Possible causes

-   One of the CCM or Rational Quality Manager rootservice consumer keys
    in the Jazz Team Server inbound consumers list does not correspond
    to the Design Management OAuth Consumer Key in the CCM or QM friends
    list.

<!-- -->

-   The secret key of the CCM or Rational Quality Manager rootservice
    consumer key does not correspond to the secret key of the Design
    Management friend.

## Possible solutions

-   Make sure that the consumer key information (Key ID and Key Secret)
    between the Jazz Team Server inbound consumers and the CCM or
    Rational Quality Manager friends are matching perfectly.
-   The following technote provides further information on this problem
    and the detailed steps to resolve it for CCM:
    -   [Failed to read matching artifact container catalog resource
        adding an association from a project
        area](http://www.ibm.com/support/docview.wss?uid=swg21626622).

##### Related topics: [related-topics]

-   Still need help troubleshooting your integrations issue? Refer to
    [Integrations Troubleshooting](IntegrationsTroubleshooting) for
    additional topics.

##### External links: [external-links]

\* Failed to read matching artifact container catalog resource adding an
association from a project area:
<http://www.ibm.com/support/docview.wss?uid=swg21626622>

##### Additional contributors: Main.FrancoisPanaget [additional-contributors-main.francoispanaget]

META:TOPICMOVED{by="fpanaget" date="1366990034"
from="Deployment.WhyCannotIAssociateADesignManagerProjectAreaToARationalTeamConcertProjectArea"
to="Deployment.WhyAmINotAbleToAssociateADesignManagerProjectAreaToARationalTeamConcertProjectArea"}
