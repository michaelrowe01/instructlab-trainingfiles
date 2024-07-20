META:TOPICINFO{author="lfrankel" date="1411441620" format="1.1"
version="1.15"} META:TOPICPARENT{name="ServerRename"}

# Planning for server rename DKGRAY Authors: Main.LisaFrankel Build basis: CLM products, version 4.0.1 and later [planning-for-server-rename-dkgray-authors-main.lisafrankel-build-basis-clm-products-version-4.0.1-and-later]

ENDCOLOR

TOC{title="Page contents"}

Before you perform a server rename, review the overview information on
this page, learn about supported and unsupported scenarios, and perform
the prerequisite rename steps.

RED **Important:** ENDCOLOR Server rename is a complex and potentially
disruptive operation because correcting the stored links to the server
from other applications and systems can be difficult or impossible.
Server rename is supported only for a specific set of scenarios and
requires careful planning. Use server rename only as a last resort when
other approaches are unworkable. To enable server rename, you must
obtain a feature key file from IBM Software Support. When you contact
IBM support, mention that you are requesting a "Server Rename feature
key file". The key file is named `ImportURLMappings.activate`. Once
received, copy the file to the `JazzInstallDir/server/conf` directory
for the applications that you will rename.

## Server rename A server rename is defined as changing the public URL for the Jazz Team Server and one or more of its registered applications, after those applications are deployed. The URL change can include any or all of the following components: protocol, hostname, domain, port, or context root. An example of a public URL for a Jazz Team Server would be the string `https://clm01.mycompany.com:9443/jts`.

The Jazz Team Server and CLM applications use links to store
relationships between stored artifacts that may span applications or
systems, and to communicate with each other and with non-CLM
applications. Server rename remaps existing URLs to new URLs to preserve
the integrity of most links. Without the remapping, those links would be
broken.

RED **Note:** ENDCOLOR There are many links that are outside the control
of the Jazz Team Server and the CLM applications. The following types of
links are not covered in the rename and would be broken:

-   URLs embedded in email, presentations, and documents
-   Bookmarks in browsers
-   Free text links that users paste or type into UI fields
-   Links from third-party applications

### Risks and precautions

Performing a server rename is not without risk, particularly if the CLM
deployment includes integrations to other non-CLM applications. Any
change to a host name has the potential to break links in the data or to
prevent CLM products from operating correctly.

If it is necessary to make changes to your topology, the preferred
approach is to always do so in a way that maintains a stable URL, such
as using DNS to route the host name to a different machine, or using a
reverse proxy or virtual hosts. See [Techniques for changing your
topology](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.2/com.ibm.jazz.install.doc/topics/c_techniques_changing_topology.html)
for details. Where this is not possible, you can use server rename.

The following precautionary steps are recommended before you perform a
server rename:

-   Plan your deployment carefully. See [Deployment and installation
    planning for the Rational solution for
    CLM](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.2/com.ibm.jazz.install.doc/topics/c_planning_install.html),
    particularly the topic [Planning your
    URIs](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.2/com.ibm.jazz.install.doc/topics/c_planning_URLs.html).
-   Be careful throughout the renaming process to enter URLs correctly,
    double-checking to avoid typos in host names, ports, or context
    roots. Some of these typos are not detectable by the rename process.
    To correct mistakes, you may need to perform another rename, or in
    extreme circumstances, you may need to restore from backups before
    performing another rename.
-   Prepare and thoroughly review the mapping file in advance of the
    actual rename.
-   It is imperative that you fully understand your deployment prior to
    a rename, specifically what external references and linkages you
    have to other production systems. Review the information in
    [Supported scenarios for using server
    rename](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.2/com.ibm.jazz.install.doc/topics/c_server_rename_sup_unsup.html)
    to understand the scenarios that are supported. Review the
    information in [Impact of server rename on the Rational solution for
    Collaborative Lifecycle
    Management](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.2/com.ibm.jazz.install.doc/topics/c_server_rename_limitations.html)
    and [Impact of server rename on integrated
    products](ServerRenameImpactOnRationalSolutionForCLM) to see if the
    integrations in your deployment are supported.
-   Carefully consider clients, such as the Rational Team Concert
    Eclipse or Visual Studio client, that rely on the CLM deployment to
    be renamed. To prevent any disruption and to preserve availability,
    notify end users of those clients in advance that you are going to
    change the URLs of the CLM servers used by those clients. Encourage
    end users to perform backups and to complete tasks in progress, such
    as code deliveries, before you start the rename procedure.
-   During the online portion of the rename, users may be able to log in
    to the server while the administrator is validating the renamed
    data. At this time, any operation that is not a read-only operation
    will result in an error. Ensure that users are aware of this
    behavior in case they log in before the online rename is complete.

\#SwVersionReq

### Software version requirements

Before you can perform a server rename, you must upgrade to the required
version of the CLM software. The following table lists the software
version requirements for performing a server rename:

Table 1. Required software versions

\###Add table here

For a complete list of system requirements for the current release, see
[System requirements](DeploymentInstallingUpgradingAndMigrating).

### What parts of the URL can be renamed?

Renaming a Jazz Team Server and/or the CLM applications requires a
remapping of the URLs that are stored in CLM resources. You can rename
the entire URL prefix, which includes all parts of the URL through the
context root, but does not include the context path of a resource.
Specifically, you can rename the scheme (or protocol), host, domain,
port, and context root.

For example, suppose you want to rename the following old URL in a pilot
deployment, which is moving to a centrally managed data center:

-   Old URL: `http://bad.host.example.org:9443/ccm` This URL uses an
    unsecure protocol (http), the default port configuration (9443), and
    a default context root (ccm).

<!-- -->

-   New URL: `https://good.host.example.org/ccm14` This URL uses a
    secure protocol (`https`), changes the host name, uses the default
    port (unspecified in the URL), and a custom context root (`ccm14`).

Table 2. Parts of the URL that can be remapped in a server rename

\###Add table here

\#ServerRenameSupportedScenarios

## Supported scenarios

You can rename the server to move a pilot deployment into production or
to move an existing production deployment to new hardware. The server
rename operation moves all existing projects and artifacts from one
deployment to another. The operation does not support a selected project
move function; that is, you cannot move only selected projects when you
rename a server.

Read the description of the supported and unsupported scenarios below.
See [Server rename process example]( ) for the high-level steps in
performing a server rename. See Software version requirements for
information about the requirements for each scenario.

### Setting up a test staging environment with production data

This scenario allows you to create a copy of an existing CLM deployment
for test purposes only. In this scenario, when version 4 is running in
production, you can also install version 4 in the test staging
environment and copy the data and configuration files from production to
the staging environment. You then use server rename to change the URLs
in the staging environment.

This is useful for trying out new features or functions with real data
without impacting the production database. One such example might be
trying out a change to your process configuration or Rational Team
Concert work item type definitions. This scenario requires that the
production server and the copied test server must never cross-link.

In addition, it is important not to connect a Rational Team Concert
client to both the production and staging repositories. Always use a
staging workspace for connecting to the staging server.

For additional details, see [Topologies and mapping files for setting up
a test staging environment]( ) and [Setting up a test staging
environment with production data]( ).

RED **Important:** ENDCOLOR This scenario cannot be used to stage an
upgrade from version 3 to version 4, which requires an isolated network
where the URLs remain constant before and during the upgrade procedure.
For details about this upgrade scenario, see [Staging a test environment
for the upgrade process]( ).

### Moving a pilot deployment to production

This scenario starts out as a small, pilot deployment that has been set
up for evaluation purposes. The pilot has a limited number of users, who
test-drive product features and create data. After the evaluation
period, the goal is to scale up, add more users and data, and not lose
any existing data that was created during the pilot.

For several reasons, such as a need to move the pilot to more robust
hardware or a need to comply with corporate naming standards, a server
rename is required. The pilot-to-production scenario must meet the
following requirements:

-   The pilot must be a single CLM deployment (Jazz Team Server with the
    registered CLM applications) with no linkages to other CLM
    deployments.
-   All user clients and build engines must be at version 4 or higher
    prior to the rename.
-   After performing the server rename, the pilot deployment must be
    permanently taken out of service.
-   No integrations to Rational or third-party products are allowed,
    except for integrations to Rational ClearQuest, Rational ClearCase,
    and Rational Reporting for Development Intelligence (RRDI). RRDI can
    be moved from the pilot environment to a separate system in the
    production environment. Rational ClearQuest and Rational ClearCase
    must be production systems that can communicate with the CLM
    deployment in the pilot environment. At this time, moving Rational
    ClearQuest or Rational ClearCase from a pilot system to a production
    system is an unsupported scenario.
-   You must not be using the Derby database, or must migrate off of the
    Derby database prior to the rename.

For additional details, see [Topologies and mapping files for the
pilot-to-production scenario]( ) and [Moving a pilot or full production
deployment by using server rename]( ).

### Moving an existing production deployment

Starting from version 4.0.1, you can perform a server rename on a CLM
deployment that is in full production. You can move your deployment to
new hardware or perform a rename in place on the existing hardware. This
production-to-production scenario must meet the following requirements:

-   Unlike the pilot-to-production scenario, multiple CLM deployments,
    such as two linked Jazz Team Servers, are now supported.
-   If you are switching to new hardware, the old hardware must be
    permanently taken out of service.
-   More integrations to Rational and third-party products are allowed
    than was allowed previously. For information about supported
    integrations, see [Impact of server rename on the Rational solution
    for Collaborative Lifecycle
    Management](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.2/com.ibm.jazz.install.doc/topics/c_server_rename_limitations.html)
    and [Impact of server rename on integrated products (version 4.0.1
    and later)](ServerRenameImpactOnRationalSolutionForCLM).
-   It is assumed that you are using an enterprise database and not
    using the Derby database.

\#ServerRenameMappingFile

## Mapping file for server rename

### Description of a sample mapping file

### Dummy mappings to protect production data

### Using a simplified mapping file

### URLs with default ports

### Case sensitivity

### Additional URLs file

### Errors during mapping file generation

### Verifying a mappings file

\#ServerRenameOnZOS

### Server rename on z/OS

## Server rename process example

\#TopologyDiagramsMappingFileEx

## Topology diagrams and mapping file examples

This section provides example topologies and mapping files to help you
perform a server rename. Use the example that closely matches your
deployment environment.

\#SettingUpTestStagingEnvironment

### Setting up a test staging environment

A staging environment is a test sandbox that includes a snapshot of
production data isolated from the production environment. When planning
a test staging environment, you need to be especially careful not to
contaminate production data or vice-versa. You accomplish this by
masking out production servers in the mapping file. Be sure to consider
any additional CLM servers, or any integrated servers, that might be
connected to the production server.

#### Starting Point 1: Single-server CLM production deployment

##### Copying the production environment

#### Starting Point 2: Production environment with two linked CLM deployments

##### Copying a single, distributed deployment to a staging environment

##### Copying both distributed deployments to a staging environment

\#PilotToProdScenario

### Pilot-to-production scenario

#### Starting Point 1: Single-server CLM pilot deployment

##### Moving to a single-server CLM production deployment

##### Moving to a distributed production deployment

#### Starting Point 2: Single-server CLM pilot deployment with integrations

##### Moving to a single-server CLM production deployment with integrations

\#ProdToProdScenario

### Production-to-production scenario

#### Starting Point 1: Single-server CLM deployment

##### Copying the single-server production deployment

#### Starting Point 2: Distributed production deployment with integrations

##### Renaming the distributed production deployment

##### Moving a single application in a distributed deployment to a new server

#### Starting Point 3: Two distributed deployments that are linked together

##### Renaming one of the linked deployments

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: None [additional-contributors-none]
