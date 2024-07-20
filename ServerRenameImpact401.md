META:TOPICINFO{author="lfrankel" date="1414007082" format="1.1"
reprev="1.6" version="1.6"} META:TOPICPARENT{name="ServerRename"}

# Impact of server rename on integrated products (version 4.0.1) DKGRAY Authors: Main.EricSolomon, Main.HeatherSterling [impact-of-server-rename-on-integrated-products-version-4.0.1-dkgray-authors-main.ericsolomon-main.heathersterling]

Build basis: Rational solution for Collaborative Lifecycle Management
4.0.1 ENDCOLOR

TOC{title="Page contents"}

Starting in the Rational solution for Collaborative Lifecycle Management
version 4.0.1, you can rename one or more server public URLs by using
the server rename feature. For more information about this feature, see
the "Changing the public URL by using server rename" topic in the Jazz
Team Server Installing book in the [IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

Changing server URLs is a complex and potentially disruptive operation
due to the linkages that may exist between multiple disparate products,
as well as 3rd party applications. Prior to attempting a rename, it is
imperative that you understand the supported scenarios (see the
"Supported scenarios for using server rename" topic in the Jazz Team
Server Installing book in the [IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html)),
the impact of performing a rename for your deployment scenario, and the
server rename procedure. If you haven't already done so, you should also
review [Renaming your Rational solution for Collaborative Lifecycle
Management server (version 4.0.1)](ServerRenameCLM401).

Before performing a server rename, it is important that you understand
the products that you integrate with.

-   If you are renaming a pilot or full production deployment and your
    deployment includes other integrations, verify that those
    integrations are supported. If your integration is not supported, do
    not perform a server rename. Your integrations will break.
-   If you are setting up a test staging environment, you must create
    "dummy mappings" in the mapping file for the URLs of any additional
    integrations in your deployment. This is to prevent contamination or
    linkages from the staging environment into production. For
    instructions on how to edit the mapping file for your deployment,
    see the "Mapping file for server rename" topic in the Jazz Team
    Server Installing book in the [IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

## Rational CLM product integrations

It is our intention to eventually support a CLM server rename in all of
the Rational integrated products. As one might expect, these products
are sometimes built on different technologies and architectures, and do
not all ship on the same release schedule as CLM. It is important to
understand that for most of these products, continued integration after
a CLM server rename will require you to either download a specific new
product release or iFix, or download and run a separate utility. When
new integrations are supported, the actions needed to repair the
integration points will vary by product but may include the following:

-   Changing repository connections to point to new servers
-   Editing configuration files with new server names and restarting
    software
-   Using an administration GUI to change server URLs
-   Running a tool to change URL references in product data repositories
    (some downtime would usually be required)

The following table lists the non-CLM product integrations that would be
impacted by a CLM server rename. Use this table to assess the impact on
your planned server rename. We are working hard to ensure that each
integration is thoroughly tested by IBM before we give it our seal of
approval and support. We will update these tables as new integrations
are supported, so check back as needed for the latest updates.

## Supported non-CLM products that would be impacted by a server rename of the JTS and CLM applications

Server rename support is now provided in this release for the following
non-CLM products. See the support statements for guidance about
reconfiguring the integrations after a server rename.

Non-CLM product Integrates With Support Statement and Documentation

Rational Application Developer for WebSphere Software 8.5 RTC

After the RTC server is renamed, you will be prompted to restart RAD and
connect to the renamed RTC server. Ensure that all RTC clients have
updated repository connections that point to the renamed RTC server. In
addition, be sure to update the hostname of the renamed RTC server in
the DNS lookup table.

Security AppScan Enterprise 8.6 RQMRTC After a server rename, RQM will
be unable to start AppScan. For the AppScan test adapter, rerun the
AppScan Adapter Setup and point to the new URL for the RQM server. For
defect submission from AppScan to RTC, log into Security AppScan
Enterprise and update the Defect Tracking Configuration in Enterprise to
point at the new URL for the RTC server. For details see Editing
integration details after a server rename. For additional details, see
Configuring the ASE adapter.

Security AppScan Source 8.6, 8.5

RTC

If you have enabled RTC defect tracking in Security AppScan Source for
Analysis, and the RTC server is renamed, any existing configuration for
project areas on that server will no longer be available. You will need
to connect to the server via its new repository URI and recreate the
configuration in the Defect Tracking System preferences. For details
about configuring a connection, see

Rational Team Concert preferences. For additional information, see

Integrating with Rational Team Concert.

Rational Build Forge 7.1.1.4 Rational Build Forge 7.1.2

RQM Not impacted by server rename

Rational Business Developer 8.5 Rational Developer for Power System
Software 8.5 Rational Developer for System z 8.5 Rational Programming
Patterns 8.5

RTC Server rename only impacts RTC client shell-sharing. Repository
connections for RTC need to be updated after a server rename to point to
the new server. See Verifying Change and Configuration Management,
specifically the sections on the Eclipse client and Enterprise
Extensions, for details. Note: Server rename has no impact on
integration with Rational Programming Patterns 8.5.

Rational Change 5.3.0.4, 5.3.0.3 iFix 001 RQM RTCRRC

Rational Change integrates with RTC, RQM, and RRC through Open Services
for Lifecycle Collaboration (OSLC). Rational Change also integrates with
RTC through Rational Synchronization Server. After a rename, RQM users
will not be able to navigate to test cases. RTC users will not be able
to navigate to work items, and RRC users will not be able to navigate to
requirements. To reestablish the integrations, use the Rational Synergy
7.2.0.2 or 7.2.0.3 command-line interface to update references to the
renamed server. With Rational Change 5.3.0.3, you will also need to
install the Change patch that includes the server rename support. For
details, see

Updating references to an an integration server that was renamed and
What to do when Rational Team Concert server is renamed.

Rational ClearCase Bridge v7.1.x, v7.1.2.x and v8.0.0.x

RTC

Requires execution of a ClearCase tool that is used to administer RTC
task URIs for certain situations. See Updating the ClearCase Bridge
after performing server rename on Jazz Team Server for details.

Rational ClearCase Synchronizer and Importer v7.1.x, v7.1.2.x and
v8.0.0.x

RTC

Stop and start the synchronization build engine after server rename. See
Updating the ClearCase Synchronizer environment after renaming the Jazz
Team Server for details.

Rational ClearQuest Bridge v7.1.2.07 or higher and v8.0.0.03 or higher

RTCRQMRRC

Requires running a tool several times that updates Jazz Team Server
public URI artifact links for the Rational solution for CLM.
Specifically, the tool updates the URIs that are stored in IBM Rational
ClearQuest Web server configuration files. The tool also updates the
URIs that are stored in OSLCLink records in the ClearQuest user
database. See

Remapping URIs after renaming a CLM server for details.

Rational ClearQuest Synchronizer v7.1.x, v7.1.2.x and v8.0.0.x

RTCRQM

Requires performing a set of steps to update the synchronizer properties
file and force a resynchronization from RTC/RQM to ClearQuest to repair
broken links after a CLM server renaming operation. See Preparing the
ClearQuest Synchronizer for renaming Jazz Team Server for details.

Rational DOORS 9.3, 9.4 Rational DOORS Web Access 1.4.0.0, 1.5.0.0

RQM RTC

Server rename impacts the requirements change management
feature. Proposed changes in progress will no longer be visible and
cannot be worked through the review/approval process. Before performing
any verifications after a CLM server rename, modify the URLs for the
Friend servers in the DOORS database properties with the new CLM server
hostname.

Rational DOORS Next Generation 4.0.1 RQMRTC Server rename impacts the
links between requirements, test cases, work items, and plans. See the
CLM Information Center at Changing the public URL by using server rename
for server rename guidelines. The instructions in the Information Center
for Requirements Management (RM) are also valid for DOORS Next
Generation. See

Verifying Requirements Management for specific instructions about
verification after a server rename.

Rational Focal Point 6.5.2 RTCRRC

After a rename, links to RTC and RRC artifacts will be broken. To
reestablish the integrations, you need to update the Server Friends List
in Focal Point, specifically the Root Services URI for RTC and RRC. See

Rational Focal Point and the Rational solution for Collaborative
Lifecycle Management and Connecting to the Rational solution for
Collaborative Lifecycle Management application server for details.

Rational Functional Tester 8.2.2 RQM After rename, RQM will not be able
to run RFT scripts, and the keyword view function will be disabled. To
reconnect, you must re-configure the adapter to point to the new URL and
update the URL in the Keyword view. For details, see

Configuring and running the Rational Functional Tester adapter for RQM
and

Viewing keywords created in IBM Rational Quality Manager.

Rational Functional Tester 8.2.2 RTC

After rename, repository connections to RTC will stop working. Work
items may have incorrect links. Repository connections need to be
updated to point to the new server. RTC plugins used by RFT may require
upgrading to 4.0.1. Rational Functional Tester projects managed by RTC
require reconfiguration. For more information, see

Sharing a project.

Hudson 2.2 Jenkins 1.4.5.8 RTC

Repository connections for RTC need to be updated after a server rename
to point to the new server. See Verifying Change and Configuration
Management for details.

Rational License Key Server 8.1.2

RTCRQMRRC

Not impacted by server rename

Rational Insight 1.1.1.1

RTCRQMRRC

The process of configuring Rational Insight after a rename of the Jazz
Team Server or the CLM applications is the same as the process of
configuring Rational Reporting for Development Intelligence (RRDI). See

Configuring RRDI after server rename for details. For instructions about
renaming the reporting server itself, see

Server rename and reporting.

Rational Method Composer 7.5.2 RTC

RMC generates an xml file that RTC imports as work item templates. Links
back to RMC-published pages, such as process descriptions from RTC work
items, can become broken in the following cases: A user specified a Jazz
server and port on the RMC export as part of the server path, and a CLM
administrator subsequently renamed the server and/or port. A user failed
to specify a server and port as part of the server path, but they opted
during the RMC generation/export to deploy RMC pages to the RTC server
context root, rather than using an RMC- specific root on the RTC server,
and a CLM admin subsequently renamed the Jazz server's context root.

To remedy the situation, work item templates can be re-exported and
imported to avoid links becoming broken for new work items. See

RMC with RTC tech note for details.

Rational Performance Tester 8.2.1 Rational Service Tester for SOA
Quality 8.2.1 RQM After rename, RQM cannot run RPT or RST scripts. You
will need to reconfigure the adapter to point to the new RQM server.
Verify that the adapter connects and that RPT and RST scripts run
successfully. For RPT details, see

Configuring the Rational Quality Manager adapter. For RST details, see
Configuring the Rational Quality Manager adapter.

Rational Performance Tester 8.2.1 Rational Service Tester for SOA
Quality 8.2.1

RTC

Connection records that point to RTC repositories will fail to open. For
RPT, you will need to update connection records to point to the new RTC
server.

Microsoft Project 2007, 2010

RTC

Not impacted by server rename. For details about the integration, see
Microsoft Project integration.

Rational Publishing Engine 1.1.2.2, 1.2 

RTC

If you included server URLs for RTC in your document specification and
template, and then change the server URL by doing a server rename,
document generation will be broken until you fix the references. For
details, see

Updating Rational Publishing Engine files after data source server
changes.

Rational Reporting for Development Intelligence 2.0 RTCRQMRRC

For instructions about the process of configuring Rational Reporting for
Development Intelligence after a rename of the Jazz Team Server or the
CLM applications, see 

Configuring RRDI after server rename. For instructions about renaming
the reporting server itself, see

Server rename and reporting.

Rational Reporting for Document Generation 1.1.2.2, 1.2 RTCRQMRRC
Rational Reporting for Document Generation (RRDG) is the document
generation component of Rational Publishing Engine (RPE). RRDG
dynamically computes the public URLs of the CLM applications and
provides substitutions for variables. If you author your document
specification to use these variables as the URLs for data sources, the
URLs will continue to work after a server rename. The only time that
server rename will cause a broken URL is if you hard-code a server URL
in your document specification or template.

Rational RequisitePro 7.1.3 RQM

Not impacted by server rename because RQM references are not stored on
the RequisitePro server.

Rational Rhapsody 7.6, 8.0 RQM After rename, RQM cannot run Rhapsody
TestConductor scripts. Re-configure the adapter to point to the new RQM
server.

Rational Rhapsody 7.6, 8.0 RTC Server rename only impacts RTC client
shell-sharing. Models that include URLs to CLM artifacts will have
broken links. Repository connections for RTC need to be updated after a
server rename to point to the new server. See Verifying Change and
Configuration Management for details.

Rational Robot 7.0.3

RQM

After rename, RQM cannot run Robot scripts. Re-configure the adapter to
point to the new RQM server. For details, see

Configuring the Robot adapter. Verify that the adapter connects and that
Robot scripts run successfully.

Selenium adapter 2.0

RQM

Selenium automates browsers, primarily for automating web applications
for testing purposes. You can use the JUnit Selenium adapter to run
Selenium version 2.0 WebDriver JUnit4 tests on the RQM server. After a
rename, change the URL of the RQM server in the Selenium adapter and
verify that Selenium scripts run successfully. For details, see Impact
of server rename on the Quality Management (QM) application.

Rational Software Architect 8.5 Rational Software Architect RealTime
Edition 8.5

Rational Software Architect for !WebSphere Software 8.5

RTC

Server rename only impacts RTC client shell-sharing. Models that include
URLs to CLM artifacts will have broken links. Repository connections for
RTC need to be updated after a server rename to point to the new server.
See Verifying Change and Configuration Management for details. In
addition, URLs in models must be updated manually.

Rational Software Architect Design Manager 4.0.1 Rational Rhapsody
Design Manager 4.0.1

RRC RQM RTC

After a CLM server rename, links to CLM artifacts will be broken until
server mapping is applied on the Design Manager (DM) server. The DM
server will use the same server mapping file as CLM. After CLM server
rename, verify as follows: Log in to DM in your web browser. Verify that
the links established before server rename are still functional and
navigable. Verify that the links in the Recent Links viewlet on the
dashboard are still navigable. Verify that new links from DM to CLM
servers can be created in DM without any issues. Verify that new links
from CLM to DM servers can be created in CLM without any issues.

See Design Manager for additional verification steps.

Rational Synergy 7.2.0.2, 7.2.0.3 RRC RQM RTC

Currently, Rational Synergy is not impacted by server rename. However,
you must use the Rational Synergy command line interface to reestablish
the integration between Rational Change and CLM. For details, see

Updating references to an an integration server that was renamed.

Rational System Architect RTC Only impacts RTC client shell-sharing.
Models that include URLs to CLM artifacts will have broken links.
Repository connections for RTC need to be updated after a server rename
to point to the new server. See Verifying Change and Configuration
Management for details. In addition, URLs in models must be updated
manually.

Rational Test RealTime 8.0.0.1 RQM RTC

After rename, RQM cannot run Test RT scripts. Reconfigure the adapter to
point to the new RQM server, using the -reconfigure option to set the
new server URL. For details, see

Initializing the Rational Quality Manager adapter. For RTC, server
rename only impacts RTC client shell-sharing. Repository connections for
RTC need to be updated after a server rename to point to the new server.
See Verifying Change and Configuration Management for details.

## Unsupported non-CLM products that would be impacted by a server rename of the JTS and CLM applications

Server rename support is not yet provided in this release for the
following non-CLM products.

Non-CLM product Integrates With Support Statement and Documentation

Rational Connector for SAP Solution Manager 4.0 RQM RTCRRC Not yet
supported for server rename

Rational Build Forge 7.1.1.4 Rational Build Forge 7.1.2, 7.1.3

RTC Not yet supported for server rename

Eclipse Lyo RQM RTC

Not yet supported for server rename

Lifecycle Query Engine 1.0.0.x RQM RTCRRC Not yet supported for server
rename

Rational Engineering Lifecycle Management 1.0.x RQM RTCRRC Not yet
supported for server rename

Git SCM 1.6.4.2 RTC

Not yet supported for server rename

JIRA 4.4.1

RTCRQM

Not yet supported for server rename

Rational Asset Manager Enterprise Edition 7.5.1 Rational Asset Manager
Standard Edition 7.5.1

RRC RQM RTC Not yet supported for server rename

Rational Publishing Engine 1.1.2.2, 1.2 RRC RQM

Not yet supported for server rename

Software Testing Automation Framework (STAF)Software Testing Automation
Framework Execution Engine (STAX) RQM Not yet supported for server
rename

Tivoli Provisioning Manager (TPM)Tivoli Application Dependency Manager
(TADM) RQM Not yet supported for server rename

##### Related topics: [ServerRename](ServerRename) [related-topics-serverrename]

##### Additional contributors: Main.RosaNaranjo [additional-contributors-main.rosanaranjo]
