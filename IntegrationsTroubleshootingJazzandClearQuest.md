META:TOPICINFO{author="atiacobo" date="1440108278" format="1.1"
reprev="1.13" version="1.13"}
META:TOPICPARENT{name="IntegrationsTroubleshooting"}

# Troubleshooting Jazz product integrations with ClearQuest [troubleshooting-jazz-product-integrations-with-clearquest]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: The
Rational solution for Collaborative Lifecycle Management (CLM) 4.x
ENDCOLOR

This page provides resources for troubleshooting Jazz product
integrations with IBM Rational ClearQuest.

-    **[Rational ClearQuest
    Synchronizer:](http://www.ibm.com/support/knowledgecenter/search/22ClearQuest20Synchronizer22)**
    Through synchronization operations, the ClearQuest Synchronizer maps
    ClearQuest records, such as defects, to Jazz work items. When a user
    creates or modifies a ClearQuest record, the ClearQuest Synchronizer
    creates or modifies a corresponding work item. The creation and
    modification changes also flow from work items to ClearQuest
    records. A ClearQuest Synchronizer has to be installed.

<!-- -->

-   **[Rational ClearQuest
    Bridge](http://www.ibm.com/support/knowledgecenter/search/22ClearQuest20Bridge22)**:
    With the ClearQuest Bridge ClearQuest records can get linked with
    Jazz work items by OSLC.

<!-- -->

-   **[Rational ClearQuest
    Importer](http://www.ibm.com/support/knowledgecenter/search/22ClearQuest20Importer22):**
    You can use the ClearQuest Import Wizard to import records from a
    ClearQuest user database into a project area. The imported records
    are stored as work items in the Jazz repository. The new work items
    are not synchronized or linked with the ClearQuest records upon
    which they are based. No configuration or extra installation is
    needed.

The troubleshooting situations on this page are divided into two groups:
situations that administrators are likely to encounter, and situations
that users are likely to encounter.

## User situations

### ClearQuest Bridge

-   [Why does the wrong Rational ClearQuest record type form pop up when
    I create a defect from a Jazz product, such as Rational Quality
    Manager or Rational Team Concert?](WhyWrongCqForm)
-   [Why is the ClearQuest Submit form blank when I go to create a
    defect from RQM or
    RTC?](WhyIsCQSubmitFormBlankWhenIGoToCreateADefectFromRQMOrRTC)
-   [Why do many ClearQuest record types appear when associating records
    and some do not even have the OSLC Links Package
    applied](WhyDoManyClearQuestRecordTypesAppear)

### ClearQuest Importer

-    [Why is my ClearQuest Import failing with error
    CRRTC0290E?](WhyIsMyClearQuestImportFailingWithErrorCRRTC0290E)

## Administrator situations

### ClearQuest Bridge

-   [Why can't I create a friendship between Rational ClearQuest and CLM
    applications, such as Rational Quality Manager, Rational Team
    Concert, and Rational Requirements
    Composer?](WhyAmINotAbleToCreateAFriendshipBetweenClearQuestAndCLMApplicationsSuchAsRQMRTCRRC)

<!-- -->

-   [Why can I not create an association between a ClearQuest database
    and a CLM Project Area (RQM, RTC,
    RRC)?](WhyCanINotCreateAnAssociationBetweenCQDbAndCLMPA)

### ClearQuest Synchronizer

-   [Troubleshooting Guide](TroubleshootingGuide)

--------------------

META:TOPICMOVED{by="dmmckinn" date="1382372494"
from="Deployment.IntegrationsTroubleshootingJazzProductIntegrations"
to="Deployment.IntegrationsTroubleshootingJazzandClearQuest"}
