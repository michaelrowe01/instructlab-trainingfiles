META:TOPICINFO{author="sbeard" date="1422039700" format="1.1"
reprev="1.22" version="1.22"} META:TOPICPARENT{name="WebHome"}

# Deployment wiki external linking guidelines [deployment-wiki-external-linking-guidelines]

DKGRAY Authors: Main.SusanYeshin Build basis: None ENDCOLOR

TOC{title="Page contents"}

Articles in the Deployment wiki often extend the basic product
information in the Rational solution for Collaborative Lifecycle
Management (CLM) Information Center (IC). When related information is
available, it is important to include links between the wiki articles
and IC topics. In addition, it is often beneficial to link from the wiki
to other sources of information, such as Jazz.net and developerWorks.
This article defines the linking policy.

## Linking responsibilities

-   Wiki authors, User Assistance (UA) content owners, and other
    contributors are expected to look for linking opportunities.
-   When a new link is required, open a work item against the location
    where the link is needed (IC or wiki page), or enter a comment in
    the IC Technical review (iDoc).
-   Both wiki authors and UA content owners are expected to ensure that
    links are current.

## What to link

-   Add links to wiki pages whenever content exists in another location
    that might extend the content of the wiki page, or be particularly
    useful to the reader.
-   Add links between the top-level page for each wiki subject area and
    highest-level topic in the IC for the same subject area. These links
    go in both directions, from the IC to the wiki, and from the wiki to
    the IC.
    -   Include links in both the Rational solution for CLM IC and the
        Rational solution for systems and software engineering (SSE) IC
        where necessary.
    -   The [cross-linking table](#CrossLinkingTable) identifies the
        high-level IC topics and wiki pages on which links are required.
    -   Because there are more IC topics than wiki sections, sometimes
        two or more high-level IC topics will link to one top-level wiki
        page. In that case, link the wiki page to only the first IC page
        listed in the cross-link table.

<!-- -->

-   Link between lower-level IC topics and wiki pages as needed, when
    information is closely related or complementary.
    -   Ensure that you are familiar with the content the IC provides
        about your subject area.
    -   These links are more likely to be from specific help topics to
        the wiki, not vice versa.
    -   If a wiki article extends information in the IC, include links
        in both the article and the help topic.

### Linking to the ICs

-   [Using the product information centers](InformationCenter) contains
    useful information and tips on the ICs for the various versions of
    Jazz products. You can link to this page to provide a general link
    to an IC, and your reader can choose which IC version to view.
-   To link from the wiki to a specific page in the IC, you have two
    options:
    -   Use the Jazz.net instance of the IC. The links will remain the
        same across releases, but you may expose your reader to
        unfinished content, or content not relevant to their own
        deployment. Example:
        [https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.install.doc/topics/c_install_overview.html](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.install.doc/topics/c_install_overview.html&scope=null).
    -   Use a version-specific IC. This gives you more control over the
        version and content, but requires you to update the link when
        the product version changes. Example:
        <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m3/index.jsp?re=1&topic=/com.ibm.jazz.install.doc/topics/c_install_overview.html>
-   On the wiki page, place the link at the bottom of the introductory
    section for the page (or at another point as needed).
-   Link wording: the following examples provide sample wording. Replace
    the words in brackets with the appropriate information, and add the
    link to the topic name. Depending on context, you have some leeway
    with the exact wording.
    -   You can also find base-level information about
        `[Sample activity]` in the `[Sample activity topic name]` in the
        `[CLM][SSE]` Information Center.
    -   For base-level information about `[Sample activity]`, see
        `[Sample activity topic name]` in the `[CLM][SSE]` Information
        Center.
    -   For product documentation about `[Sample activity]`, see
        `[Sample activity topic name]` in the `[CLM][SSE]` Information
        Center.

### Linking to Jazz.net

-   In general, Deployment articles and related content are being
    migrated from Jazz.net to the wiki. Previous versions remain on
    Jazz.net for now, with text to indicate that the wiki contains the
    latest content. For details, see [Migrating Jazz.net articles to the
    Deployment wiki](DeploymentGuidanceOnMigratingArticles).
-   For content that is not planned for migration, or for general
    product information, links might be appropriate. In this case, use
    linking conventions similar to those for linking to the ICs. A
    typical link to Jazz.net looks like this example: "For more
    information about `[this activity]`, see `[this content]` at
    Jazz.net."

### Linking to other information sources

-   Although the product ICs and Jazz.net are the primary link targets,
    from time to time it might be useful to link to additional material;
    for example, at developerWorks or third-party sites such as GitHub
    or Stack Overflow. There are no restrictions on third-party links;
    however, you should open them in a separate tab or window by using
    the `target="_blank"` attribute, so that the reader does not lose
    the wiki context:

For more information about \[this activity\], see Sample Content at
Sample Organization.

### Linking from the IC to the wiki

-   In the IC topic, place the link at the bottom of the text on the
    high-level page, directly above the RSS feed to Jazz.net and the
    child IC topics for the area.
-   Word the link as follows. Replace the words in brackets with the
    appropriate information, and add the link to the section title: "For
    advanced or deployment-specific information about
    `[Sample activity]`, see the `["xxxxxxxxx" section]` of the Jazz.net
    Deployment wiki."

## Link checking

As part of the periodic site reviews (associated with GA releases of the
Rational solution for CLM), a link-checking tool will be run against the
site. Jazz.net uses [Xenu Link
Sleuth](http://home.snafu.de/tilman/xenulink.html) for link checking on
the Deployment wiki. Link checking the IC is also part of the standard
UA quality process for each product release.

\#CrossLinkingTable

## Cross-linking table

\| **Wiki section** \| **Top-level IC topic** \| **Notes** \| \|
Deployment wiki home page \| Installing the Rational solution for CLM
(future topic) BRCLMUpgrading the Rational solution for CLM
(c_upgrade_overview) \| For now, substitute a link to c_planning_install
for the link to "Installing the Rational solution," which is not
currently available \| \| Deployment planning and design \| Deployment
topologies (c_deployment_topology_considerations BRInstallation process
and topology examples (c_topology_overview) \| Link the top-level page
of the wiki section to both the Upgrade and Installation planning pages.
You do not need to link the wiki to the "Deployment and Installation" or
"Deployment and Upgrade" topics, although those topics will link to the
wiki. \| \| Installing and upgrading \| Planning the deployment and
installation (c_planning_install) BRPlanning the deployment and upgrade
(c_planning_upgrade) BRDeployment and installation
(c_deployment_considerations) \| Link the top-level page of the wiki
section to both the Upgrade and Installation planning pages. You do not
need to link the wiki to the "Deployment and Installation" or
"Deployment and Upgrade" topics, although those topics will link to the
wiki. \|

|  |  |  |
|----|----|----|
| Migrating and evolving |  |  |
| Integrating | Overview of CLM Integrations (c_overview_clm_integrations.html) | The integrating wiki page can link to a proposed high-level conceptual introduction to "integrating" |

\| Administering \| Administering Rational solution for CLM servers
(tworkwithadminwebui) \| The main admin IC topic links to the main Admin
wiki page. Some of the wiki subpages can also link to the main admin
topic. \|

|  |  |  |
|----|----|----|
| Monitoring |  |  |
| Troubleshooting | rrm.help.doc/topics/c_troubleshooting_overview, BRteamconcert.doc/topics/c_troubleshooting, BRteamconcert.doc/topics/c_RTCi_trouble, web.admin.doc/topics/ttroubleshooting | The main troubleshooting topic is a common Rational topic and cannot be modified. Cross-links should be between the Troubleshooting wiki page and the product-level troubleshooting topics. The wiki page should identify the troubleshooting IC topics by product. |

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   None

##### Additional contributors: Main.AmyLaird, Main.LauraHinson [additional-contributors-main.amylaird-main.laurahinson]
