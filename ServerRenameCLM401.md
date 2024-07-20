META:TOPICINFO{author="lfrankel" date="1413992133" format="1.1"
reprev="1.7" version="1.7"} META:TOPICPARENT{name="ServerRename"}

# Renaming your Rational solution for Collaborative Lifecycle Management server (version 4.0.1) [renaming-your-rational-solution-for-collaborative-lifecycle-management-server-version-4.0.1]

DKGRAY Authors: Main.DavidChadwick Build basis: Rational solution for
Collaborative Lifecycle Management 2012 (product version 4.0.1) ENDCOLOR

TOC{title="Page contents"}

## Purpose

The purpose of this document is to provide the basic information for
customers to decide when and when not to use the Jazz server rename
feature introduced in version 4 of the Rational solution for
Collaborative Lifecycle Management products. These products include
Rational Team Concert, Rational Requirements Composer, and Rational
Quality Manager. With the additional functionality added in version
4.0.1, the full set of planned user scenarios are now supported for
server rename. These user scenarios have been thoroughly tested by IBM
and validated in partnership with our customers. This document has been
updated to include all of those user scenarios. Full support of server
rename for your production installation is now available with version
4.0.1 and later.

In addition, this document provides links to other related documents on
jazz.net. One such document, [Impact of server rename and integrated
products (version 4.0.1)](ServerRenameImpact401), provides more detailed
information on the various product integrations and which of these
provide support for the CLM server rename functionality. Over time,
most, if not all, of these products will accommodate CLM server rename.
As each of these integrations is made fully functional and thoroughly
tested, its status will be updated in that document.

## Definitions

### Renaming your CLM server

A CLM (or Jazz) server rename is defined as changing the public URL for
the Jazz Team Server and/or one or more of its registered applications.
The URL change can include any or all of the following components:
protocol, host name, domain, port, or context root. An example of a
public URL for a Jazz Team Server would be the string
`https://clm01.mycompany.com:9443/jts`.

### CLM Server

A CLM server is defined as a web application server hosting one or more
Jazz applications that are part of the IBM Rational solution for
Collaborative Lifecycle Management.

## Background on Public URL

One of the most challenging aspects of using the IBM Rational Jazz
products is dealing with linked artifacts which use absolute URL links
to access the encapsulated data. From the beginning, these links were
explicitly chosen to make use of the architecture of the web, which uses
URLs to reference objects and expects permanent (or at least long
lasting) addresses. The base part of the URL is called the public URL.
This is the part that must stay consistent to permit access to the
artifacts hosted by that Jazz application.

The advantage of this approach is that it gives you the ability to
access the artifact from any context, including a browser bookmark, a
hot link on a web page, or in an email message. The disadvantage is the
inability to move the artifact to a new server, change DNS host names or
domains, or freely update your IT infrastructure to support changes in
project or organizational structure.

Other traditional, monolithic, database server-based SDLC products in
the industry permit this freedom of movement, and users also expect that
freedom from the Collaborative Lifecycle Management solution.

Because the nature of software and systems development shops is dynamic
and constantly changing, there is a critical need for the CLM solution
to support these changing environments by allowing administrators to
rename their Jazz servers. Note, however, that changing the public URLs
of existing CLM deployments can be disruptive, so it is always best if
you can plan ahead and use stable URLs.

## Primary user scenarios for server rename

There are a number of reasons why server rename may be desired. Listed
here are a few representative user scenarios that are supported for
server rename.

1.  **Production to Staging**: This scenario involves copying a
    production server to a staging environment (also called a test
    sandbox) so that new or not yet used functionality can be checked
    before it is introduced into the production environment. Examples
    might include testing new project and process templates, work item
    customizations, integration with non-CLM tools, or trying out other
    CLM functions not yet used in the production environment. Note: Only
    a limited subset of integrations are currently supported.
2.  **Pilot to Production**: In this scenario, the CLM server was first
    used as a pilot implementation and now needs to be moved to the
    production IT environment. There are production rules that the
    current public URL in the pilot system do not meet. The IT
    department demands adherence to their standards. This may include
    moving to a secure connection or a different server
    name/domain/port.
3.  **Production to Production**: In this scenario, some aspect to the
    public URL is no longer usable and must be changed. For example, the
    server or domain name cannot remain the same. Perhaps the customer
    wants to standardize on a server name based on the products function
    rather than use the name of the host machine. Also the customer may
    want to move to a default port so non-local access is permitted
    without corporate firewall exceptions.

## Non-supported data reorganization scenarios

There are other user scenarios that customers are very interested in
performing to modify the configuration of their production CLM
installations. A few of the most common are listed below. These user
scenarios are not in any way supported nor will they work. If any of
these scenarios is attempted, it will result in a non-functional
production environment. The development team will be reviewing these use
cases for possible solutions in the future.

1.  **CLM Consolidation Merging JTS servers**: In this scenario, the CLM
    products were implemented as multiple pilot or production
    installations and were originally hosted and managed separately. Now
    there is a desire to have the products integrated and centrally
    managed as a single CLM system. This would involve combining the
    multiple JTS instances and registering the applications with the
    combined JTS. (**Not supported** using server rename feature)
2.  **CLM server split**: In this scenario, the user population and/or
    number of projects has grown to the point where customer IT wants to
    split the projects across two CLM instances so that they can be
    separately administered and managed. Through some analysis of
    affinities, project areas are put on server A or server B with as
    few cross server linkages as can be managed for performance reasons.
    The strategy is to clone the production server and archive projects
    that are to be run from the other server. (**Not supported** using
    server rename feature)
3.  **Project Move from one CLM server to another**: In this scenario,
    the user wants to move project contents out of one CLM deployment
    and into the repositories of another. This is one of the top
    requests for enterprise deployments, but is also the most complex of
    the data reorganization scenarios. (**Not supported using server
    rename feature**)
4.  **CLM server cloning**: This scenario involves replicating servers
    so that you can reuse the existing system to seed a "ready to run"
    fully configured new system. (**Not supported** using server rename
    feature) However, there are new command line setup capabilities that
    may help build newly configured systems more efficiently.

## Server rename considerations

**Warning**: Before deciding to use the server rename feature, there are
some additional factors to consider. Because artifact links are used
externally to the CLM system, any existing externally-held links will no
longer be valid. This would include all links that were included in
email messages, web pages, and in integrated non-CLM products (unless
they explicitly support CLM server rename) that may be in use in the
customers environment.

Other integrated products storing URL references to CLM artifacts will
require an implementation of a rename feature that scans for these CLM
links and adjusts them based on source/target (old/new) public URL
pairs. However, you may have to upgrade those products or delay the
rename operation until all of the integrated products can handle the
renaming of the CLM system. For example, you must have Rational
ClearQuest version 8.0.0.3_2012B to apply the server rename function for
the bridged integration to the CLM system. Basically all of those links
must be updated so that the integrated applications can continue to work
properly and make use of the functionality afforded by the linked data
architecture of the CLM system and other applications using OSLC
linkages.

Consult [Impact of server rename and integrated products (version
4.0.1)](ServerRenameImpact401) to find the required version for each of
your integrated systems and verify that all are available before using
server rename.

## Server rename sequencing

A server rename is often accompanied by other complex operations. It is
recommended that each operation be validated individually prior to the
rename. This practice makes it easier to determine which operation
caused any problem introduced by that operation. Detailed instructions
for each of these operations can be found in the information center.

1.  Upgrade - An upgrade is considered a distinct action from a rename
    operation. In particular when rehearsing the upgrade to a version
    4.0.x product, this must be done using the production public URL
    (and server name) and thus must be done using an isolated network.
    The upgrade should be validated first before the server is renamed.
2.  Changing application servers - By setting up a second application
    server (usually this is done to host a staging environment or to
    replace the old production server), careful installation and
    configuration steps must be followed and validated before moving
    forward to perform the rename operation. This is the most frequent
    source of problems that are attributed to the server rename
    operation. Validating the application server installation and
    configuration using a temporary Derby repository is a recommended
    practice before attempting a rename operation on a copy of the
    production repository.
3.  Changing database servers - By setting up a second database server
    (for staging or infrastructure improvements), careful setup of the
    database, including granting the proper permissions to the
    connecting user ID, is important to validate with a database client
    program before connecting the Jazz applications to the restored copy
    of the production repository. This provides a high level of
    confidence that the rename operation will be able to connect and
    make the changes needed by the rename operation. Also, the rename
    process requires configuration files to be copied from the source
    CLM server to the target CLM server. If the database location
    changes, the `teamserver.properties` files must be updated to
    reflect the new location. Before proceeding with the rename,
    validate the target CLM server's configuration files to ensure that
    they contain correct information.
4.  WebSphere considerations - If you are using WebSphere Application
    Server, it is important that the Jazz Team Server and applications
    start at the appropriate times. It is a good idea to disable
    auto-start during the rename process since there are various offline
    and online steps, and the application server or applications
    themselves might need to be restarted. It is a best practice to
    start the applications before the Jazz Team Server. The Jazz Team
    Server polls the applications and requires them to be online for the
    rename to complete.

## Impact of a server rename

Once you determine that your use case for the server rename feature is
supported, review the "Changing the public URL by using server rename"
topic in the Jazz Team Server Installing book in the [IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
This section of the CLM help explains how to perform a server rename
operation. Following are the high-level steps in the rename process:

1.  Generating and editing the mapping file that contains all of the
    source/target URL mappings. This must be performed while the CLM
    servers are still online. This step does not impact product
    functionality. Also run the **verifyURLmappings** command to check
    for any reported errors.(**preparation step**)
2.  Running an offline command to import the URL mappings into the JTS.
    All CLM servers in the topology must be shutdown prior to running
    this command. You will need to plan appropriately for the outage.
    (offline step)
3.  Bringing up all CLM servers so that the applications can contact the
    JTS to synchronize their mappings. During this time, the JTS is in a
    special mode that blocks user access. All requests made to the JTS
    or any of its registered applications are redirected to a
    centralized server rename status page. (**online/readonly step**)
4.  When the rename completes on all applications and components, the
    JTS and applications will enter a read-only mode of operation so
    that you can perform addition manual data validation steps. One of
    these steps is running the server rename validation wizard.
    (**online/readonly step**)
5.  Once you are satisfied that the server rename operation has
    completed successfully, you can switch the servers to full
    production mode. (**online step**)

There are integrations with some subsystems within the CLM system that
contain the CLM servers public URL or at least the host name of the
server. While most of these are handled directly by the server rename
operation, there are some that require manual updates. These include
build engines and test adapters as well as some linkages such as live
CLM data source feeds used by reporting tools. Instructions for updating
these are included in the server rename instructions. Some of these
steps can be manually intensive and require verification after the
server rename operation.

If an error occurs during the second or third step of the server rename,
or you made a mistake in the mapping input file, consult the product
documentation to determine if the error is correctable. If it is not
correctable, you will need to restore all of your databases and
configuration files from your backups. Contact IBM Support to determine
how to rectify the problem.

## Decision process

Once you have evaluated your server topology, integrations, and impact
on your user community, you must make a decision whether to use server
rename to accomplish your goal or whether to maintain the current public
URL. Through the use of DNS mapping and host name aliasing, perhaps with
a reverse proxy server, you may be able to maintain the current public
URL. Leaving the public URL constant is certainly a preferred solution
because it preserves all of the external references as well as those
that you can update through the server rename process. The linked data
architecture used by the Jazz architecture (and the CLM system) expects
the links to be stable and supported for a long period of time.
Maintaining those links should be a high priority in setting up the CLM
system.

## Enabling server rename

If maintaining the public URL is simply not an option for your CLM
system, and you fit into one of the supported use cases, you must
contact IBM Support to obtain a server rename feature key file to unlock
the server rename feature.

IBM Support will help you confirm that your rename usage pattern is
consistent with a supported use of the server rename feature. They can
also help you determine if IBM assistance is needed to help you perform
the rename operation or if you need any additional fixes. The goal is to
ensure that you are informed of the process details. If you are not sure
whether you have a pilot to production scenario or a production to
production scenario, contact IBM Support.

## Server rename checklist

When you call IBM Support, be prepared to answer the following
questions. You must answer "yes" to all the questions to use the server
rename feature.

1.  Is the user scenario supported -- production to staging, pilot to
    production, or production server rename?BRIBM only supports renaming
    a production server by using the server rename feature with v4.0.1
    or later version.BR
2.  Are you sure that you are not attempting a different data
    reorganization scenario by using the server rename feature?BRThis
    feature does not permit the migration of project areas associated
    with one JTS to another, moving project areas from one application
    repository to another, or provide a way to create two production
    environments.BR
3.  Are all CLM applications and their JTS running version 4.0.1 or
    later? Is RRDI included and running version 2.0 or later?BR\*\*If
    not, all applications must be upgraded to v4.0.1 before attempting a
    pilot to production or a production to production rename. For a
    production to staging rename version 4.0 is required and version
    4.0.1 is strongly recommended.BR\*\*Note that ***you cannot use
    server rename for staging a v3 to v4 upgrade***.BR\*\*Upgrading to
    version 4.0.1 is a separate activity and requires stable URLs and an
    isolated network.BR\*\*Once you are running version 4, you can use
    server rename to rename your staging environment for further
    testing.BR
4.  Are all RTC client programs that will access the renamed system
    running a versopm 4.0 or later product version?BR\*\*If not, you
    must upgrade all clients to version 4 (or install separate version 4
    client instances) that will be used to access the renamed
    system.BRThis is of primary importance for the pilot to production
    and production to production use cases, so your users are warned
    when accessing a newly renamed CLM system.BR\*\*For the production
    to staging use case, the users of the staging (or test) system
    should use a separate client workspace and a separate version 4
    client to protect the production data against contamination from
    client interactions with the test system.
5.  If used as a staging (or test) environment, is the renamed CLM
    system isolated from all integrated production applications?
    Integrations that not available as part of the renamed staging
    environment should be stubbed out (that is, set to a null system
    name) so that these links from the production system are not active
    or usable. This guarantees that the newly renamed test system is
    isolated from those integrated systems. For details, see the
    "Mapping file for server rename" topic in the Jazz Team Server
    Installing book in the [IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).BRFor
    the production to staging user scenario, as a best practice, the
    `/etc/hosts` file on the renamed test server should redirect those
    previously integrated production system names to a bogus IP address
    so that there is no communication between the renamed test system
    and the integrated production systems.BRThe RQM Lab Management
    functionality supports server rename in version 4.0.1 and later.
6.  If you are using a Derby database in your pilot to production use
    case, do you understand the need to migrate the existing data
    repositories to a production database server?BRAll production CLM
    systems are expected to use production quality databases that handle
    the scalability, robustness, and maintainability required in a
    production environment. This means that the pilot Derby database
    must be migrated to an enterprise database during the server rename
    to the new production CLM system. You will need to run the
    **repotools export** and **repotools import** commands to migrate
    your data to the production database server as part of the CLM
    server rename procedure. For instructions for re-configuring your
    CLM deployment when the database vendor changes, see the "Changing
    the Rational solution for Collaborative Lifecycle Management
    databases to a different database vendor" topic in the Jazz Team
    Server Installing book in the [IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
7.  Will only one of these systems ever be used in the production
    environment?BRIn the pilot to production use case, you are expected
    to NEVER restore to production service the original server image
    from before the CLM server rename. It has been replaced by the
    renamed CLM server.BRIn the production to staging use case, you are
    expected to run both the staging and production versions of the
    system, but the staging version will not be integrated with
    production applications nor be used as a production system. It
    should remain in an isolated staging (or test) environment.BRBecause
    of expected technical design limitations, the staging system and the
    production system can never be linked through a Jazz friend
    relationship or have linked data between the systems.
8.  There can be no linked data between the renamed system and the
    original system. Is this acceptable to you and for your intended use
    of the CLM servers?BRIn the pilot to production or production to
    production user scenario, the initial system with the original
    public URL is decommissioned.BRIn the production to staging user
    scenario, the staging system will never integrate with production
    applications but both environments will remain active.BRBy walking
    through the intended purposes for both the original and renamed CLM
    servers, it should be clear that the systems will not be linked nor
    used together in any way.
9.  If you are performing a production rename and have multiple
    deployments, have you identified all affected deployments?BR If
    deployment A is being renamed and any application in A is linked to
    any application in deployment B, B must also be renamed. This is
    because B contains links to A.BR\*\*The rename for A and B MUST be
    performed simultaneously. Administrators must validate A and B and
    complete the renames at the same time. If any corrective mappings
    are needed, they must be applied to both A and B. Administrators
    must plan for outage time for all linked deployments.BR\*\*If an
    administrator is not certain of all of the deployment linkages, the
    **generateURLMappings** command should be run against all of the
    Jazz Team Servers in production. Inbound friends do not show up in
    the generated mapping file and it is easy to miss these linkages.
    Scan for occurrences of any of A's URLs in B's generated mapping
    file. If deployment A is being renamed and an application in
    deployment B has a one-way friendship with an application in
    deployment A, the application in B will not show up in A's mapping
    file. However, the application in A will show up in B's mapping
    file. In this case, the rename must be performed against B as well,
    since B contains links to A.BR\*\*Consult the additional URLs file
    that is generated after running the **generateURLMappings** command.
    This file contains URLs that were not contributed to the generated
    mapping file. The list could contain URLs that need to be added to
    the generated mapping file or that represent integrations that need
    to be considered.BR\*\*Many integrations do not show up in the
    generated mapping file. Ensure that administrators go through the
    list of integrations in [Impact of server rename and integrated
    products (version 4.0.1)](ServerRenameImpact401) to identify any
    integrations that they might have.BR\*\*In some cases, backlink
    creation may fail during the rename read-only mode period. Consider
    the scenario in the first bullet where a third deployment C exists.
    C has linkages to B but not A. In this scenario, C does not need to
    be renamed but it should also be taken down because backlink
    creation from C to B will fail when B is in read-only mode. For some
    operations, the user is warned that the backlink creation failed; in
    other cases, it may not be obvious. There is currently no mechanism
    that will automatically repair missed backlinks.
10. Have you requested a server rename feature key to unlock the server
    rename feature from IBM Support?BRThe server rename will fail if it
    cannot find the feature key file in the directory specified in the
    email from IBM Support.
11. Have you reviewed [Workarounds for Server Rename problems in CLM
    4.0.1](https://jazz.net/library/article/1165) to see if there are
    posted solutions to any of your problems?

## Server rename outage planning

It is critical to identify and plan for the amount of outage time that
is needed. This is especially true for pilot-production or production
renames where user productivity is impacted. Here are some best
practices:

1.  Do not underestimate verification time. Administrators should
    perform the following before completing a rename:BRVerify that all
    of the URLs in the verification wizard are correct and that all of
    the links can be followed.BRVerify that all links and URL data in
    all of the applications and project areas are correct.BRPerform any
    product-specific verification, including client verification, as
    described in the information center.
2.  By having multiple people verify things simultaneously, the overall
    outage time is reduced.
3.  Plan outage time for recoverable mistakes. It is possible that you
    might miss a mapping or make a typo in a mapping. In this case, a
    corrective mapping must be applied and an additional server rename
    must be performed.
4.  Plan outage time for the worst case scenario. The rename feature is
    solid, however there is always a chance something could go wrong. In
    this case, a full backup and restore is required before normal
    server operation can resume.
5.  In the case of multiple linked deployments, outage time must be
    considered for all deployments. The renames must be done
    simultaneously and completed at the same time.
6.  If an upgrade is required beforehand, plan outage time for that as
    well.
7.  Instruct users that it is a best practice to check in their
    outstanding source code changes before the rename occurs. Include
    instructions for updating their connection strings for the new
    server location. For the version 4 clients, users do not have to
    start with a fresh workspace after the rename operation because the
    clients support server rename.

## Summary

Renaming a server can be accomplished with proper planning and by
carefully following the server rename instructions. Remember that there
will be external links to CLM artifacts that will be broken after
performing a server rename. Before performing a server rename, confirm
that you have a supported use case. Assessment of integrations with
other applications is crucial to prevent a loss of integrated system
functionality. There are a number of CLM subsystems depend on the public
URL. These subsystems might not be obvious and must be updated to
accommodate the rename operation. Communication of the server rename
with the CLM user community is very important and should be planned
ahead of time. Performing a server rename operation should be done
carefully to reduce lost work and productivity.

## For more information

-   [CLM Knowledge Collection in the IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html)
    -- Provides instructions on server rename
-   [Impact of server rename and integrated products (version
    4.0.1)](ServerRenameImpact401) -- Discusses CLM server rename
    integration support
-   [Workaround: Server Rename Read-only Mode
    Limitations](https://jazz.net/library/article/1124) -- Explains the
    limitations of the post server rename read-only mode

##### Related topics: [ServerRename](ServerRename) [related-topics-serverrename]

##### Additional contributors: Main.RitchieSchacher, Main.HeatherSterling, Main.EricSolomon, Main.AraMasrof, Main.RosaNaranjo [additional-contributors-main.ritchieschacher-main.heathersterling-main.ericsolomon-main.aramasrof-main.rosanaranjo]
