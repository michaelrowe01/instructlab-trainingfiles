META:TOPICINFO{author="sbagot" date="1432737601" format="1.1"
reprev="1.6" version="1.6"}
META:TOPICPARENT{name="IntegrationTroubleshootingRationalRequirementsComposer"}

# Full selection list of Link Types are not displayed when linking RRC to RTC Artifacts [full-selection-list-of-link-types-are-not-displayed-when-linking-rrc-to-rtc-artifacts]

DKGRAY Authors: Main.TamishaThompson Build basis: Rational Requirements
Composer 4.x, Rational Team Concert 4.x ENDCOLOR

TOC{title="Page contents"}

This topic provides information to help troubleshoot the issue seen
where the expected list of link options are not available when linking
artifacts from Rational Requirements Composer (RRC) to Rational Team
Concert (RTC).

## Symptoms In RRC, when attempting to create a link to an artifact in RTC, you do not see the full list of available link types to select from. For example, "Tracked by" is not available.

## Possible Causes

One possible cause may be that the RRC project is not associated with an
RTC project.

## Troubleshooting Steps

Verify the association exists between the RRC project and the RTC
project:

To verify:

1.  In your browser, open the RRC project (for example:
    <https://:/rm/web>)
2.  In the upper right corner, select the drop down for **Administration
    \> Manage This Project Area**
3.  Look in the section labelled **Associations** and confirm that an
    RTC project area is listed
4.  Repeat these same steps when viewing the project area of the RTC
    project (from ccm/admin), confirming that an RRC project area is
    listed for the Association.

If the association does not exist between the RRC project and RTC
project, the association must be created.

1.  Review the documentation on Creating a lifecycle project that
    includes only existing project areas
2.  Then create the Associations

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)
