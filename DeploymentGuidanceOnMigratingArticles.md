META:TOPICINFO{author="sbeard" date="1384899899" format="1.1"
reprev="1.25" version="1.25"} META:TOPICPARENT{name="WebHome"}

# Migrating Jazz.net articles to the Deployment wiki [migrating-jazz.net-articles-to-the-deployment-wiki]

DKGRAY Authors: Main.RalphEarle, Main.StevenBeard Build basis: None
ENDCOLOR

TOC{title="Page contents"}

This article provides guidance on how to migrate Jazz.net articles into
the Deployment wiki.

## Migration procedure

Identify a candidate deployment related Jazz.net article that should be
migrated, migrated and updated (this might include refactoring) or just
superseded by a topic page in the wiki. If the article just needs to be
superseded by an existing topic page in the wiki, follow step 8. below
to request a banner to be added to the original article stating, 'The
content of this article has been superseded by the ... topic page'.

Check with the section lead that they are happy for the article to be
migrated to their section and agree it's location (link location(s) and
parent topic page).

We are managing much of the article migration using [Migrate current and
relevant Jazz.net deployment related articles into the
wiki](https://jazz.net/jazz02/web/projects/Deployment20Wiki#action=com.ibm.team.workitem.viewWorkItem&id=94658),
with a child Story WI for the actual migration of each individual or
small group of related article pages. As usual a peer and editors review
of the new topic page should be performed against the Story once the
article has been migrated.

Steps to migrate or migrate and update a Jazz.net article to the wiki:

1.  Select the article on Jazz.net. Verify that the article source
    originates on Jazz.net and is not linked from developerWorks or
    another external source.
2.  Open the article on Jazz.net.
3.  Copy the article text to the clipboard. **Note:** Copy only the
    text, and not the HTML tagging. If you copy the HTML tagging, you
    might introduce inconsistent styles or markup that the wiki does not
    support.
4.  Create a new topic page on the Deployment wiki with the name of the
    article converted to a WikiWord.
5.  Paste the article text onto the new topic page.
6.  If the article contains graphics, follow the steps in [Migrating
    graphics](#MigratingGraphics).
7.  Format the topic page for the wiki. Basic wiki formatting help is
    shown at the bottom of the page when editing. For details on
    formatting topic pages and a full list of wiki shorthand, see
    [Deployment wiki formatting guidance](DeploymentFormattingGuidance).
    You must add wiki shorthand for the following items in an article:
    -   Headings
    -   Lists
    -   Bold, italic, or fixed font
    -   Tables
    -   Separators
8.  After your article is migrated to the wiki, the original Jazz.net
    article requires a migration banner similar to:The first hyperlink
    will be to the new topic page where the content of the jazz.net
    article has been migrated to.Please raise a new task within the
    [JazzCS](https://jazz.net/jazz02/web/projects/JazzCS#action=com.ibm.team.workitem.newWorkItem&type=task&ts=1380069013000)
    RTC project to request a banner to be added to the migrated Jazz.net
    article:
    -   Set the 'Owned By' field to 'Reuben Varzea'
    -   Set the 'Summary' field to 'Add migration banner to Jazz.net
        article:' with the article's name
    -   Include in the 'Description' field the hyperlink to original
        article and the new wiki topic page where the content of the
        article has been migrated to e.g.Jazz.net article [Version
        Compatibility Matrix for RRDI, CLM, and Rational
        Insight](https://jazz.net/library/article/1199) migrate to
        [Deployment wiki: Version Compatibility Matrix for RRDI, CLM,
        and Rational
        Insight](https://jazz.net/wiki/bin/view/Deployment/VersionCompatibilityCLMRRDIAndInsight)
    -   Explicitly include the full wording of the migration banner as
        the introductory text can change:
        -   'The content of this article has been migrated to the ...
            topic page.', for straight forward migration
        -   'The content of this article has been migrated and updated
            to the ... topic page.', for migration and update
        -   'The content of this article has been migrated and
            refactored to ... and ... topic pages.', for migration and
            refactoring
        -   'The content of this article has been superseded by ...
            topic page.', for articles that have been superseded
        -   'There is a more recent version of this content relating to
            more recent versions of the related products on the ...
            topic page.', for articles that are not going to be
            migrated, where there is a more recent version of the
            content relating to more recent versions of the products
9.  Change all the links in the Deployment wiki that pointed to the old
    Jazz.net article to the new wiki topic page. The easiest way of
    finding the links that need to be changed is to search the wiki for
    the article number. **This is critical to maintain the consistency
    of the Deployment wiki.**
10.  Check to see if the article has any good comments that should be
    part of the new wiki page. Sometimes these comments can be added to
    the wiki page as a Q&A section.
11. Please add the migrated article and new topic page to the table at
    the bottom of this page.

### Formatting notes

-   The heading styles are different between the Jazz.net articles and
    wiki topic pages. Use the wiki template topic page styles rather
    than trying to retrofit the Jazz.net styles to maintain consistency
    in the wiki.
-   The wiki converts any words that look like a WikiWord to a link to a
    potential wiki page. Common examples are WikiWord, WebSphere,
    SmartCloud, and DevOps. You can disable this behavior in two ways:
    -   To disable individual instances, prefix the unintended WikiWord
        with an exclamation point (example: `!WebSphere`).
    -   To disable all automatic linking ofWikiWords, surround any
        portion of the page text withand tags.
-   To exclude a heading from the TOC, put ! after the heading notation
    (---+!).
-   The wiki link notation opens the linked page in the same window as
    the current page. To open a link on a new tab or page, use a
    standard anchor tag with the target="\_blank" attribute: link text.

\#MigratingGraphics

### Migrating graphics

1.  Right-click the graphic.
2.  Save the graphic on your hard drive.
3.  In the upper-right corner of your new wiki page, click **Attach**.
    (This link is not available when the page is in edit mode.)
4.  Select the file that you saved on your hard drive.
5.  In the Properties section, select **Create a link to the attached
    file** and **Do not show attachment in table**. A new `img` link is
    created at the bottom of the wiki page.
6.  Open the wiki page for editing. Copy the new `img` link from the
    bottom of the page to the clipboard. Paste the link where you want
    the graphic to be displayed. Delete the link and its accompanying
    code from the bottom of the page.
7.  To align the new `img` centrally and have an associated caption, use
    the following format:

***Caption***

## Jazz.net articles that have already been migrated to the Deployment wiki

| Jazz.net article | Deployment wiki topic page |
|:---|:---|
| [Version Compatibility Matrix for RRDI, CLM, and Rational Insight](https://jazz.net/library/article/1199) | [Version Compatibility Matrix for RRDI, CLM, and Rational Insight](VersionCompatibilityCLMRRDIAndInsight) |
| [Configuring Enterprise CLM Reverse Proxies, Part 1: Understanding Reverse Proxy](https://jazz.net/library/article/744) | [Understanding reverse proxy](UnderstandingReverseProxy) |
| [Configuring Enterprise CLM Reverse Proxies: WebSphere 8 and IHS 8](https://jazz.net/library/article/745) | [Configuring Enterprise CLM Reverse Proxies: WebSphere 8 and IHS 8](https://jazz.net/library/article/745) |
| [Part 3: Configuring Enterprise CLM Reverse Proxies: Apache and mod_proxy](https://jazz.net/library/article/1066) | [Configuring Enterprise CLM Reverse Proxies: Apache and mod_proxy](ConfigureCLMEnterpriseReverseProxyWithApache) |
| [Best Practices for Server Rename and Moving to the Rational solution for Collaborative Lifecycle Managment 2012](https://jazz.net/library/article/1116) | [Best Practices for Server Rename and Moving to the Rational solution for Collaborative Lifecycle Managment 2012](https://jazz.net/wiki/bin/view/Deployment/ServerRenameBestPractices) |
| [Case study: Server rename (version 4.0.1)](https://jazz.net/library/article/1148) | [Case study: Server rename (version 4.0.1)](https://jazz.net/wiki/bin/view/Deployment/ServerRenameCaseStudy) |
| [Impact of Server Rename and Integrated Products (Version 4.0.1)](https://jazz.net/library/article/1120) | [Impact of Server Rename and Integrated Products (Version 4.0.1)](https://jazz.net/wiki/bin/view/Deployment/ServerRenameImpact401) |
| [Standard Collaborative Lifecycle Management Topologies](https://jazz.net/library/article/820) | [Standard topologies overview ](https://jazz.net/wiki/bin/view/Deployment/StandardTopologiesOverview) |
| [Renaming your Rational solution for Collaborative Lifecycle Management server (version 4.0.1 and later)](https://jazz.net/library/article/1081) | [Renaming your Rational solution for Collaborative Lifecycle Management server (version 4.0.1 and later)](https://jazz.net/wiki/bin/view/Deployment/ServerRenameCLM401) |
| [Rational Solution for Collaborative Lifecycle Management 2012 Deployment Guide](https://jazz.net/library/article/832) | [Rational Solution for Collaborative Lifecycle Management 2012 deployment guide](https://jazz.net/wiki/bin/view/Deployment/CLM2012DeploymentGuide) |

##### Related topics: [Deployment formatting guidance](DeploymentFormattingGuidance), [Writing guidelines](DeploymentWritingGuidelines) [related-topics-deployment-formatting-guidance-writing-guidelines]

##### External links: None [external-links-none]

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="Migration_Banner.png"
attachment="Migration_Banner.png" attr="h" comment="" date="1384777329"
path="Migration_Banner.png" size="36446" user="sbeard" version="1"}
