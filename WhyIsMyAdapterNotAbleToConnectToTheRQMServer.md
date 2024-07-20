META:TOPICINFO{author="sbagot" date="1432737694" format="1.1"
version="1.19"}
META:TOPICPARENT{name="IntegrationsTroubleshootingRQMandAdapters"}

# Why can't my adapter connect to the Rational Quality Manager server? [why-cant-my-adapter-connect-to-the-rational-quality-manager-server]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: Rational
Quality Manager 4.0.x and later ENDCOLOR

TOC{title="Page contents"}

This page describes how to troubleshoot issues where your adapter is not
connecting to your Rational Quality Manager server. The information in
this article applies to the Rational Functional Tester adapter, the
Rational Performance Tester adapter, and the command line adapter.

## Initial assessment

### Symptoms

-   The execution adapter is not listed as available in the Adapter
    Console view

### Impact / scope

-   Unable to run automate test scripts

### Environmental changes

-   Newly added firewall or security software

## Possible causes

### Lack of system connectivity

Network connection problems might prevent the system hosting the adapter
from accessing the Rational Quality Manager server.

### Mismatch in public URI

An incorrectly configured URL in the adapter might prevent the
connection.

### Mismatch in version of the adapter and version of Rational Quality Manager server

The adapter version might not be the one required by the Rational
Quality Manager server.

### Lack of permissions/licenses

The user that runs the test tool adapter might not have the right
permission or the right licenses to connect to the Rational Quality
Manager server.

## Possible solutions

### Verify system connectivity

-   Verify that the system hosting the adapter has connectivity to the
    Quality Management application.
-   One way to validate this is to simply bring up a browser and try
    connecting to Quality Manager (for example,
    `https://server_name:9443/qm/admin` for 3.x/4.x context root or
    `https://server_name:9443/jazz/admin` for 2.x context root).
-   Work with your network administrator to resolve the connectivity
    issue.

### Verify the public URI

-   Verify that the URL you are using for the adapter matches the
    configured public URI for the Quality Management application.
-   You can view the public URI for the server on the Quality Management
    application admin page (for example,
    `https://server_name:9443/qm/admin` for 3.x/4.x context root or
    `https://server_name:9443/jazz/admin` for 2.x context root).
-   You must configure the adapter to use this exact URL. This procedure
    is adapter-dependent. See the Information Center of your specific
    adapter for detailed information (see External Links below for
    examples).
-   Note that the public URI does not typically use a short name or an
    IP address.

### Verify the version of the adapter and the version of Rational Quality Manager server

-   Verify the version of the adapter (and or testing tool) meets the
    minimum version requirements for Rational Quality Manager version.
-   See [Rational Quality Manager system
    requirements](http://www.ibm.com/support/docview.wss?uid=swg27015934).

### Grant permissions and licenses

-   Verify that the CLM user profile for the user account that runs the
    test tool adapter has the appropriate repository permissions and
    licenses. 1 Open the Jazz Team Server admin page. 1 Select **Users
    \> Active Users** 1 Select the user in question. 1 Select
    **JazzUsers** in the Repository Permissions section. 1 Select
    **Rational Quality Manager - Quality Professional** or **Rational
    Quality Manager - Connector** in the Client Access Licenses section
-   If the user account has only a **Rational Quality Manager -
    Contributor** license, this will cause adapter connection issues.

##### Related topics: [related-topics]

\* Still need help troubleshooting your integrations issue? Refer to
[Integrations troubleshooting](IntegrationsTroubleshooting) for
additional topics.

##### External links: [external-links]

-   Rational Quality Manager System Requirements:
    <http://www.ibm.com/support/docview.wss?uid=swg27015934>
-   Configuring the RQM adapter - Rational Functional Tester 8.6:
    [http://www.ibm.com/support/knowledgecenter/SSBLQQ_8.6.0/com.ibm.rational.test.ft.doc/topics/t_configuring_rft_for_rqm.html](www.ibm.com/support/knowledgecenter/SSBLQQ_8.6.0/com.ibm.rational.test.ft.doc/topics/t_configuring_rft_for_rqm.html)
-   Configuring the RQM adapter - Rational Performance Tester 8.6:
    <http://www.ibm.com/support/knowledgecenter/SSMMM5_8.6.0/com.ibm.rational.test.lt.doc/topics/trqmadaptconfig.html>
-   Troubleshooting command-line adapter issues:
    <http://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.5/com.ibm.rational.test.qm.doc/topics/t_cmd_line_troubleshooting.html>

##### Additional contributors: Main.AraMasrof [additional-contributors-main.aramasrof]
