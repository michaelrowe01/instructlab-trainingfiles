META:TOPICINFO{author="lekandrade" date="1696509835" format="1.1"
version="1.13"} META:TOPICPARENT{name="ServerRename"}

# Verifying and troubleshooting server rename DKGRAY Authors: Main.LisaFrankel Build basis: CLM products, version 4.0.1 and later [verifying-and-troubleshooting-server-rename-dkgray-authors-main.lisafrankel-build-basis-clm-products-version-4.0.1-and-later]

ENDCOLOR

TOC{title="Page contents"}

This page describes verification and troubleshooting steps for server
rename. Perform the verification steps after the sever rename completes.

There are two primary parts to server rename verification:

-   Running the server rename verification wizard
-   Performing final verifications for the Jazz Team Server, the
    Rational solution for Collaborative Lifecycle Management (CLM)
    applications, and any common components and integrations

There is also a verification step that you perform earlier, after you
generate the mapping file. The earlier verification is performed on the
generated mapping file, before you perform the actual rename.

\#VerifyingURLsAndLinks

## Verifying URLs and links after a server rename

After you rename a server, you can verify the rename at the Server
Rename Status page, where you can visually inspect the key URLs for your
deployment. You can validate the public URL, friend URLs, project area
links, and so on. In addition, you can click on links to open the
application pages in a new browser tab and look for broken links and
incorrect URLs.

### Before you begin [before-you-begin]

To take advantage of the verification feature, you must upgrade the Jazz
Team Server and all CLM applications to version 4.0.1 or newer before
the rename. Older applications do not support this feature.

Perform one of the supported server rename scenarios that are described
at [Performing a server rename](ServerRenamePerforming). Then, start the
Jazz Team Server as described in Step 4 in the scenario topics.

### About this task [about-this-task]

During this verification process, the Jazz Team Server and all
registered applications are in read-only mode. Be sure to inform your
user community that the server will be in read-only mode during the
verification process and that it is highly recommended that they not log
on during that time.

### Procedure [procedure]

1.  Log into the Jazz Team Server at
    `https://new host:port/jts/serverRenameStatus` to view the Server
    Rename Status screen. This starts the actual renaming process as
    described in Step 5 in the scenario topics.
2.  Wait for the renames to complete and the status for all of the
    applications to reach 100. Any attempts to log in to the web UI for
    any of the CLM applications before the rename is complete will
    redirect you to this status page.
3.  Click Next to start the verification wizard. The wizard will guide
    you through a visual inspection of the important URLs in your
    deployment. During the verification process, the Jazz Team Server
    and all applications will be placed in read-only mode, but you will
    be able to browse data, and look for broken links and unmapped URLs.
    RED **Note:** ENDCOLOR Do not exit read-only mode until you have
    confirmed that the URLS are correct, that you can successfully
    browse through your application data, and that the links work. To
    learn more about read-only mode, including read-only mode
    restrictions, see [Server rename read-only mode
    limitation](https://jazz.net/library/article/1124).
4.  If all of the URLs are correct, ensure that you have performed any
    additional product-specific verifications described at Completing
    the server rename verification process. When you are confident that
    the renamed data is correct, click the **I have verified the server
    rename** check box and click **Finish**. At this point, the Jazz
    Team Server and all registered applications will exit read-only mode
    and normal product use can resume.
5.  If any of the URLs are incorrect or still need to be renamed,
    perform the following steps:
    1.  Click the flag icon next to the URL. On the final step of the
        wizard, any flagged URLs will be included in a mapping template.
        RED **Note:** ENDCOLOR Do not check the **I have verified the
        server rename** box or click **Finish** at this point.
    2.  Stop the Jazz Team Server and create a new mappings file by
        using the template that is provided. The template can be used to
        fix URLs that were mapped incorrectly due to typographical
        errors or missed mappings. RED **Note:** ENDCOLOR Do not append
        the template to the original mappings file. The new mappings
        file will fix the errors that were found. Do not use the
        original mapping file because those renames have already been
        performed. To fix any problems, you have to rerun the
        `repotools -importURLMappings` command. See Recovering from
        importURLMappings errors for a list of common mapping errors and
        corrective actions.
    3.  Rerun the `repotools -importURLMappings` command to perform
        another rename.
    4.  Restart the Jazz Team Server.
    5.  Repeat the verification process starting at Step 1.

\#ServerRenameCompletingVerification

## Completing the server rename verification process

After you run the server rename verification wizard, you must perform
the verifications that are described in this section.

The verification wizard displays the renamed URLs in your deployment and
allows you to flag any incorrect URLs. These incorrect URLs must be
corrected before you complete the rename. The wizard will instruct you
to stop the server, create a new mapping file with the supplied
template, and rerun the `repotools importUrlMappings` command to perform
another rename.

### Verifying the Jazz Team Server

Complete the final verification steps for the Jazz Team Server and
associated common components, described next, after a successful server
rename and after you have completed the steps in the server rename
verification wizard.

#### General verifications for server rename in a staging environment

-   You should never see a production URL surface as a hyperlink
    anywhere in the Rational Team Concert Eclipse client, the Rational
    Team Concert client for Microsoft Visual Studio IDE, the web client
    UI, or the SCM Command Line Interface clients, nor should navigation
    cause you to traverse from the staging environment to an external
    production system.
-   If you have introduced dummy mappings to protect the production
    environment, you should see broken links to these dummy URLs in the
    Applications and Friends section of the Application Diagnostics page
    for any production system outside of the staging environment. RED
    **Note:** ENDCOLOR URLs in plain text, as contrasted with navigable
    hyperlinks, are not mapped.

#### General Jazz Team Server administration \* Log in to the Jazz Team Server Administration UI, for example `https://clmhost.production.example.org:9443/jts/admin)`.

-   Review the home page and scan for obvious errors.
-   Hover over various links and look at the browser status bar to
    verify that the URLs show the new mapped URLs. \* Verify the home
    menu.
-   Open the home menu at the upper left of the page banner and verify
    that there are no errors showing or missing entries.
-   Hover over each menu entry and verify the URLs in the browser status
    bar.
-   Navigate to some of the home menu entries and validate the page that
    you navigate to. \* Verify the Administration pages for the Jazz
    Team Server, Change and Configuration Management (CCM), and Quality
    Management (QM). For the Jazz Team Server, go to
    `server/jts/admin and click Manage Server`. For the applications, go
    to `server/ccm/admin and server/qm/admin`.
-   In the Status Summary page, verify the text and URL links for the
    Public URI of the Jazz Team Server and the floating license client.
-   In the Diagnostics page, if you are renaming a staging environment,
    you should see errors for the Application and Friends diagnostic, if
    there are any servers outside the staging environment.
-   In the Registered Applications page (Jazz Team Server only), verify
    the discovery URLs and application status. For the application
    status, you should see a green check and a status of Installed.
-   In the Advanced Properties page, search for url, http:, or https://.
    Ensure that there are no URLs that point to production systems.
-   In the Friends (Outbound) page, verify the root services URI for
    each friend.
-   In the Allowlist (Outbound) page, verify the allowlist URLs \* If
    you had a web UI theme installed, verify that it still appears
    correctly.

#### Dashboards

-   Navigate to your dashboards and verify that they load successfully,
    including all widgets coming from other servers that were renamed.
-   Verify that the different types of dashboards load properly,
    including personal dashboards on the Jazz Team Server, mini
    dashboard, project and team dashboards in Change and Configuration
    Management (CCM), Quality Management (QM), and Requirements
    Management (RM).
-   Verify that the drop-down menu for the home button shows your list
    of personal dashboards.
-   Verify that widgets with URL preferences show the updated URL if you
    open settings.
-   Verify News Feed (for external RSS/Atom feeds) and the External
    Content widget (for embedding other pages).
-   Verify that links in widgets have updated URLs, bookmarks, HTML, and
    headlines widgets.
-   (Optional) Add a widget to a project or team dashboard and click
    **Save**. Then, refresh the browser and verify that the modification
    is remembered and loads correctly.

#### Process and process authoring in the web UI

-   Verify all project area links in the Associations section of the
    **Overview** tab of any project area editor.
-   Verify all hyper links in the process description under the
    **Process Description** tab.
-   If process sharing is used, check in the consuming project area the
    link to the project area that provides the shared process.

#### Reports

-   After a server rename, start the ETLs (data collection jobs) by
    clicking the **Run all data warehouse collection jobs for all
    applications** from the Reports Admin page in the Jazz Team Server.
-   Run a few out-of-the-box reports under Reports Shared Reports and
    ensure that they still work.
-   If RRDI is installed, run a few RRDI reports and ensure that they
    still work. Run the reports in RRDI and from the dashboards. Run the
    reports both before and after the rename to be sure that the server
    rename had not caused any failures.
-    Verify the Reporting Server URL for Quality Management and Jazz
    Team Server.
    1.  Type `https://host:port/qm/admin` or
        `https://host:port/jts/admin`.
    2.  Click **Reports**.
    3.  Under **Configuration**, click **Custom Reports Connection**.
    4.  View the Reporting Server URL.

#### Lifecycle Project Administration (LPA)

1.  Log on to the Lifecycle Project Administration application as a user
    with JazzAdmins repository permissions. For details, see "Accessing
    the Lifecycle Project Administration application" in the Rational
    solution for Collaborative Lifecycle Management Administering book
    in the [IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
2.  For existing lifecycle projects, verify that URLs in hyperlinks for
    artifact containers and their associations use the new server URL.
3.  Click on an existing lifecycle project to edit it. Download the
    **Recommended Role Assignments** resource and verify that the URLs
    are as expected.
4.  Verify that templates are listed in the **Templates** tab.

### Verifying Change and Configuration Management

#### Rational Team Concert Eclipse and Microsoft Visual Studio clients

#### Rational Team Concert web client

#### SCM Command Line Interface (CLI) client

#### Rational Team Concert ISPF client

#### Jazz Team Build

#### Planning

#### Work items

#### Enterprise Extensions

### Verifying Quality Management

### Verifying Requirements Management

### Verifying Design Management and its associated components

#### Rational Software Architect (RSA) Design Management Eclipse client

#### Design Management web client

\#VerifyingCQAndCC

### Verifying Rational ClearQuest and Rational ClearCase

#### Rational ClearQuest Bridge

#### Rational ClearQuest Synchronizer

#### Rational ClearCase Bridge

#### Rational ClearCase Synchronizer

\#ServerRenameTroubleshooting

## Troubleshooting server rename

\#RecoveringFromCommonProblems

### Recovering from common problems

### Recovering from generateURLMappings errors

### Recovering from importURLMappings errors

#### You missed a mapping entry in your mappings file ---++++! You made a mistake in the target url of a mapping [you-missed-a-mapping-entry-in-your-mappings-file-----you-made-a-mistake-in-the-target-url-of-a-mapping]

#### You made a mistake in the source url of a mapping ---++++! You accidentally reversed the source and target in the mapping file [you-made-a-mistake-in-the-source-url-of-a-mapping-----you-accidentally-reversed-the-source-and-target-in-the-mapping-file]

#### You made a syntax error in the mapping [you-made-a-syntax-error-in-the-mapping]

#### Command fails with CRJAZ2449E ---++++! Command gives warning CRJAZ2425W [command-fails-with-crjaz2449e-----command-gives-warning-crjaz2425w]

#### Command shows CRJAZ2197E message [command-shows-crjaz2197e-message]

### Responding to server rename status errors

### Reviewing a history of server renames

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: None [additional-contributors-none]
