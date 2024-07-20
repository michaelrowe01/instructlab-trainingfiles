META:TOPICINFO{author="sbagot" date="1432744881" format="1.1"
version="1.21"}
META:TOPICPARENT{name="IntegrationsTroubleshootingRTCandRationalAssetManager"}

# Why can't I link Rational Asset Manager assets and CLM artifacts? [why-cant-i-link-rational-asset-manager-assets-and-clm-artifacts]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: IBM
Rational Asset Manager 7.5.1.x and later as supported with CLM 4.0.x and
later ENDCOLOR

TOC{title="Page contents"}

This document describes common issues encountered while integrating
Rational Asset Manager with Rational solution for Collaborative
Lifecycle Management (CLM) applications.

## Initial assessment

-   In order to be able to integrate **Rational Asset Manager 7.5.1.1**
    and **the version 4.0.x CLM applications**, you need to have at
    least installed the **TestFix5** (testFix5e-70522) to Rational Asset
    Manager (contact [IBM Rational Client
    support](http://www.ibm.com/support/docview.wss?uid=swg27020747) to
    get the fix if you have not yet installed it).
-   There is no need to apply a test fix if you are using Rational Asset
    Manager 7.5.1.2

### Symptoms

-   When you link a Rational Asset Manager asset to a CLM artifact, only
    the ID of the CLM artifact or unintelligible characters are
    displayed in the asset.
-   When you link a Rational Asset Manager asset to a CLM artifact, the
    name or summary of the artifact is truncated.
-   When you link a Rational Asset Manager asset to a Rational Team
    Concert artifact, the related artifact backlink is not created.

## Data gathering and subsequent analysis steps

-   Does it affect all the linked CLM artifacts?
-   What characters are contained in the **summary** of the artifacts?
    -   Does the summary contain cyrillic characters or trailing spaces
        or characters?
    -   Does the summary contain special characters (like: " + \^ \~ \<
        \>) ?
-   Does it affect all the linked assets?
-   What characters have been used in the **name** of your assets?
    -   Does the name contain double quotes (")?
-   What are the hostnames of the servers running Rational Asset Manager
    and Rational Team Concert?

## Possible causes

-   Rational Asset Manager 7.5.1.1 APARs :
    -   [PM79565 - {wi 78059} Wrong characters for work item with
        cyrillic
        characters](http://www.ibm.com/support/docview.wss?uid=swg1PM79565)
    -   [PM80195 - {wi 78741} 7.5.1.1 backport: Wrong characters for
        Work Item with cyrillic
        characters](http://www.ibm.com/support/docview.wss?uid=swg1PM80195)
    -   [PM85690 - {wi 72678} Requirements management collection
        resource only shows ID in the
        asset](http://www.ibm.com/support/docview.wss?uid=swg1PM85690)
    -   [PM86177 - {wi 85372} The OSLC related artifact back link is not
        created if an asset name contains double
        quotes](http://www.ibm.com/support/docview.wss?crawler=1&uid=swg1PM86177)
-   Rational Asset Manager and Rational Team Concert are installed on
    servers that have the same hostname.

## Possible solutions

1 Upgrade to **Rational Asset Manager 7.5.1.2**. Here is the link to
[Rational Asset Manager Fix Pack 2 (7.5.1.2) for
7.5.1](http://www.ibm.com/support/docview.wss?uid=swg24034129) 1 If you
cannot upgrade to **Rational Asset Manager 7.5.1.2** at this time,
request the **TestFix 14** (testFix14b-79107) or higher for **Rational
Asset Manager 7.5.1.1** from [IBM Rational Client
support](http://www.ibm.com/support/docview.wss?uid=swg27020747) . 1
Avoid using specific characters, especially double quotes (") for your
asset names. 1 Review this technote for solving the issue if your
Rational Asset Manager and Rational team Concert have the same hostname:
[Unable to link an asset to a work item or post work item link in a
forum](http://www.ibm.com/support/docview.wss?uid=swg21516223)

##### Related topics: [related-topics]

-   Still need help troubleshooting your integrations issue? Refer to
    [Integrations troubleshooting](Integrationstroubleshooting) for
    additional topics.

##### External links: [external-links]

-   Rational Asset Manager Fix Pack 2 (7.5.1.2) for 7.5.1:
    <http://www.ibm.com/support/docview.wss?uid=swg24034129>
    -   PM79565 - {wi 78059} Wrong characters for Work Item with
        cyrillic characters:
        <http://www.ibm.com/support/docview.wss?uid=swg1PM79565>
    -   PM80195 - {wi 78741} 7.5.1.1 backport: Wrong characters for Work
        Item with cyrillic characters:
        <http://www.ibm.com/support/docview.wss?uid=swg1PM80195>
    -   PM85690 - {wi 72678} Requirements management collection resource
        only shows ID in the asset:
        <http://www.ibm.com/support/docview.wss?uid=swg1PM85690>
    -   PM86177 - {wi 85372} The OSLC related artifact back link is not
        created if an asset name contains double quotes:
        [http://www.ibm.com/support/docview.wss?uid=swg1PM86177](http://www.ibm.com/support/docview.wss?crawler=1&uid=swg1PM86177)
-   <http://www.ibm.com/support/docview.wss?uid=swg21516223>

##### Additional contributors: Main.FrancoisPanaget [additional-contributors-main.francoispanaget]

META:TOPICMOVED{by="fpanaget" date="1366107109"
from="Deployment.WhyAmINotAbleToLinkRAMArtifactsAndCLMArtifacts"
to="Deployment.WhyAmINotAbleToLinkRAMAssetsAndCLMArtifacts"}
