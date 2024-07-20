META:TOPICINFO{author="sbagot" date="1432737167" format="1.1"
version="1.6"}
META:TOPICPARENT{name="IntegrationsTroubleshootingRationalAdapterForHPALM"}

# General Troubleshooting Rational Adapter for HP ALM [general-troubleshooting-rational-adapter-for-hp-alm]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: Rational
Adapter for HP ALM Standard Edition v1.1, Rational Collaborative
Lifecycle Management version 4.0, 4.0.1, 4.0.2, 4.0.3 ENDCOLOR

TOC{title="Page contents"}

This page provides general troubleshooting information for Rational
Adapter for HP ALM Standard Edition v1.1.

### Project list is empty for some users

When logging into HP Adapter as an Administrator and clicking on
Projects to open the Projects page, no project is listed.

-   This issue was identified as a defect and is fixed in build
    1.1.0-HPQM11-I20130507_1738
-   The problem seems to occur only with some user IDs
-   Use the following REST call to confirm that no projects are returned
    from HP:
    -   **/qcbin/rest/domains/DEFAULT/projects?login-form-required=y**
-   The following REST API is available in v.11.5 and can be used as a
    work-around to get the project list:
    -   **/qcbin/rest/domains/?login-form-required=y&include-projects-info=y**

### Non-default browser is being used

When launching HP ALM, it sometimes launches Chrome even though
Microsoft Internet Explorer (IE) is set as a default browser

-   This seems to be a general issue with HP ALM and not specific to the
    adapter.
-   A work-around is to run this Microsoft Fixit at:
    <http://support.microsoft.com/kb/310049> after setting IE as a
    default browser.

### Clicking toolbar icons do not launch the adapter

-   Check for hidden windows new browser may open behind the current one
-   Verify the Action Name defined for the toolbar button exactly
    matches the function name (such as: Resource_Landing_Page_TP)

### Missing Parameter GB_BASE_URL

-   Verify the Adapter URL is defined as a Site Admin Parameter or the
    project GB_AdapterURL() function.

### Adapter page loads with errors

-   Check the URL call using the last entry in the
    **C:\GB_EventLog.txt** file. This log saves the URLs called for any
    adapter toolbar action in ALM.
-   Cut and Paste the URL into a browser to verify that the adapter is
    configured correctly.

### Missing Toolbar Icons

-   Adapter icons only exist for Requirements, Test Plan, Test Set and
    Defects. These icons do not show up in the other modules.
-   Verify that the toolbar modifications were completed correctly:
    **Tools \> customize \> workflow script \> toolbars**.

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   Troubleshooting the HP adapter
-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.KotTontranakwong [additional-contributors-main.kottontranakwong]
