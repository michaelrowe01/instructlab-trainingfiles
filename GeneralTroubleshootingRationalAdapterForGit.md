META:TOPICINFO{author="sbagot" date="1432737116" format="1.1"
version="1.14"}
META:TOPICPARENT{name="IntegrationsTroubleshootingRationalAdapterForGit"}

# General Troubleshooting Rational Adapter for Git [general-troubleshooting-rational-adapter-for-git]

DKGRAY Authors: Main.IntegrationsTroubleshootingTeam Build basis:
Rational Adapter for Git Standard Edition v1.1, Rational Collaborative
Lifecycle Management version 4.0, 4.0.1, 4.0.2, 4.0.3 ENDCOLOR

TOC{title="Page contents"}

This page provides general troubleshooting information for Rational
Adapter for Git Standard Edition v1.1.

## Gerrit patchset-created hook failure

Below are some possible sources of Gerrit patchset-created hook
failures:

-   Gerrit server cannot communicate with the IBM Jazz Team Server
    (JTS), or the Jazz Team server is down
-   Gerrit hook has not been completely configured (for example: no JTS,
    user, pw, or registered project URL)
-   Friend relationship between Git adapter and RTC has not been
    properly configured
-   Licenses have not been properly assigned to the RTC authorized key
    functional user or the Gerrit receive hook user

## Install and Setup

-   The banner will not display before running \***\_setup.sh -i**.

<!-- -->

-   Linking will not work before registering the site, running
    \***\_setup.sh -r**, and registering the project. Linking will only
    work for registered projects.

<!-- -->

-   The correct URLs need to be used when initializing, registering, and
    installing the hook with the \***\_setup.sh** scripts. The scripts
    can verify the URL is reachable but they do not verify that the URL
    points to the correct location.

<!-- -->

-   A common mistake is to enter the wrong URL when using \***\_setup.sh
    -r**. This should be the URL shown in the Git Adapter admin page
    after registering the Gitweb/Gerrit site, not after registering the
    project. The URL is also in the table on the Git Server Connections
    page.

<!-- -->

-   Similar to above, when using \***\_setup.sh hook**, the URL to enter
    is displayed in the Git Adapter admin page after registering the
    Gitweb/Gerrit project, not the URL after registering the
    Gitweb/Gerrit site. The URL is also on the Git Server Connection
    page in the Registered Git Projects table.

<!-- -->

-   The Gitweb and Gerrit pages need to be refreshed after initializing
    and registering using the \***\_setup.sh** scripts for the changes
    to take effect (such as: the Register project link to appear in the
    administration menu).

<!-- -->

-   The **Register Project** link does not go away after registering the
    project.

<!-- -->

-   There are restrictions on the name of a Git project before
    registering it with the adapter. Essentially, special characters are
    not allowed. See the following documentation topics for more
    information: \*
    <http://www.ibm.com/support/knowledgecenter/SSWMXJ_1.1.0/com.ibm.rational.rlia.git.install.doc/topics/t_register_git_project_git.html>
    \*
    <http://www.ibm.com/support/knowledgecenter/SSWMXJ_1.1.0/com.ibm.rational.rlia.git.install.doc/topics/t_register_gerrit_project_git.html>

## Configurations / Web

-   Banner does not shown for Gitweb or Gerrit
    -   This could be due to Firewall between Gitweb/Gerrit server and
        the Git Adapter server
    -   Gerrit needs a restart A restart is required for any
        configuration changes
-   Unable to register Gerrit projects
    -   Try to refresh the browser
    -   Gerrit needs a restart A restart is required for any
        configuration changes
-   Unable to add link from Gitweb or Gerrit web \* Try to refresh the
    browser and clear the browser cache \* Git Adapter and/or the Change
    and Configuration Management (CCM) server is down \* User does not
    have a Git Adapter license
    -   User does not have CCM license

## IBM WebSphere Cache/Configurations

-   Git Adapter still shows the old version after an upgrade
    -   Remove or rename the following folders, if they exist:
        -   **WAS Install
            Directory/profiles//temp/wscache/gitAdapter_war**
        -   **WAS Install Directory/profiles//temp///gitAdapter_war**
    -   Restart the Git Adapter war file
-   User is still logged on to the Git Adapter even though logout is
    performed on the JTS.
    -   Adding a custom session manager property.
        -   Click **Application servers \> \> Session management \>
            Custom properties** and add the
            **InvalidateOnUnauthorizedSessionRequestException = true**
            custom property.
        -   Restart the WebSphere Node
    -   Clear the browser cookies/cache. A restart of the browser may be
        required as well

## Command-line

-   Unable to add link using command-line interface (hook failure)
    -   See the Error message from Git and clear the error condition.

<!-- -->

-   If there is no Error message from Gerrit, check the Git Adapter log
-   Check your settings. Use the **Git config --list** command to list
    the configuration settings:
    -   Adapter project URL (rtc.adaptedprojecturl or
        rtc.gerritadaptedprojecturl)
    -   User (rtc.user)
    -   Password (rtc.password)
    -   JTS URL (rtc.jtsurl)
-   Git Adapter and/or CCM server is down
-   Friendship is not setup
-   User does not have access to the CCM project area
-   User does not have the license (Git Adapter and/or CCM)

## Reprocess

-   Gerrit reprocess capability is new in Git Adapter version 1.1
-   Admin should periodically check for errors to reprocess
-   Reprocess can be run repeatedly on the same log file until the link
    is successful
-   Error logs are created in the **gerrit_root/hooks/rtchookreprocess**
    directory when the hook fails
    -   Files named yyyymmdd-hh-mmssmicros-n.log, where
        yyyymmdd-hh-mmssmicros is a time stamp and n is the number of
        times commit processing failed
-   Is Reprocessing needed?
    -   Check the failure log and clear the error condition
        -   **git_project_repository/hooks/rtchookreprocess**
        -   **gerrit install directory/hooks/rtchookreprocess**
    -   Running reprocess command
        -   Safe to reprocess when in doubt. Reprocess can be run as
            many times as needed.
        -   Go to the **git project repository/hooks** directory and
            type **perl reprocess.pl**
        -   Go to the **gerrit install directory/hooks** directory and
            type **perl gerrit_reprocess.pl**
    -   Manual link creation in web UI

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   Troubleshooting the Git adapter
-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.KotTontranakwong [additional-contributors-main.kottontranakwong]

META:FILEATTACHMENT{name="CRIGT0488E.jpg" attachment="CRIGT0488E.jpg"
attr="h" comment="Screenshot of the CRIGT0488E error" date="1393252236"
path="CRIGT0488E.jpg" size="18887" user="kot" version="1"}
META:FILEATTACHMENT{name="CRIGT0434E.jpg" attachment="CRIGT0434E.jpg"
attr="h" comment="Screenshot of the CRIGT0434E error" date="1393253114"
path="CRIGT0434E.jpg" size="22033" user="kot" version="1"}
