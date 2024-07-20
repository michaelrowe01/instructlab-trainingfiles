META:TOPICINFO{author="lfrankel" date="1411442557" format="1.1"
version="1.12"} META:TOPICPARENT{name="ServerRename"}

# Performing a server rename DKGRAY Authors: Main.LisaFrankel Build basis: CLM products, version 4.0.1 and later [performing-a-server-rename-dkgray-authors-main.lisafrankel-build-basis-clm-products-version-4.0.1-and-later]

ENDCOLOR

TOC{title="Page contents"}

This page includes step-by-step procedures for performing a server
rename.

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

\#ServerRenamePreparingTheMappingFile

## Preparing the mapping file

Learn how to prepare the mapping file which you will later use when you
rename your Rational solution for Collaborative Lifecycle Management
(CLM) servers. You can prepare and review the mapping file in advance of
the actual rename while your servers are still online.

### About this task [about-this-task]

There are several steps that you need to take before you rename the
server. In large part, this involves preparing and reviewing the mapping
file that you will use to perform the rename operation. The mapping file
lists the existing source URLs and the renamed target URLs in your
deployment. These include the URLs for the Jazz Team Server, the CLM
applications, the CLM help WAR file, and any other applications that are
impacted. For sample topology diagrams and mapping files, see [Topology
diagrams and mapping file
examples](ServerRenamePlanningFor#TopologyDiagramsMappingFileEx).

You can perform these steps in both an all-in-one CLM deployment, where
the Jazz Team Server and the CLM applications are all installed on the
same computer, or in a distributed deployment, where the CLM
applications are installed on different computers. These preparatory
steps can be used with various scenarios, for example where a computer
is moved to a new physical location, when setting up a test sandbox on a
new computer, or the case of a data center consolidation that involves a
renamed environment on new computers.

RED **z/OS:** ENDCOLOR Renaming a server is supported on z/OS, but there
are several differences in the process for creating a mapping file. For
details, see [Server rename on
z/OS](ServerRenamePlanningFor#ServerRenameOnZOS).

### Procedure [procedure]

1.  After upgrading the Jazz Team Server (JTS) and all CLM applications,
    start the Jazz Team Server and verify that the applications have
    been registered correctly with the server.
    1.  Log in to the Administration page of the Jazz Team Server. Point
        your web browser to `https://hostname:port/jts/admin`.
    2.  Click the **Server** tab.
    3.  In the left pane, in the Configuration section, click
        **Registered Applications**.
    4.  Verify that all of your applications are registered. For further
        details, see the "Registering applications with Jazz Team
        Server" topic in the Jazz Team Server Administering book in the
        [IBM Knowledge
        Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
2.  Open a command prompt on the computer where the Jazz Team Server is
    installed and change to the `JazzInstallDir\server` directory. RED
    **Note:** ENDCOLOR Be sure to perform this step and the following
    steps on the original Jazz Team Server, even if you will be moving
    to new hardware.
3.  Use the `repotools-jts -generateURLMappings` command to generate an
    initial mapping file to use as a template for further editing, as
    shown next. If you have already run the command, or the file already
    exists, add the `overwrite=true` parameter.
    -   RED **Windows:** ENDCOLOR
        `repotools-jts.bat -generateURLMappings toFile=mappings.txt adminUserId=adminId adminPassword=adminPassword additionalURLFile=additionalurl.txt`
    -   RED **UNIX, Linux:** ENDCOLOR
        `./repotools-jts.sh -generateURLMappings toFile=mappings.txt adminUserId=adminId adminPassword=adminPassword additionalURLFile=additionalurl.txt`
        The output of this command is a mapping file that lists the
        existing source Public URL and a default target URL for the Jazz
        Team Server and each CLM application (CCM, QM, and RM) that is
        registered with the Jazz Team Server. It also identifies source
        and target URLs for the CLM help WAR file and any known affected
        external systems. In addition, a second file is created that
        contains a list of all of the URLs that may need to be mapped or
        that reference third-party integrations that may need to be
        considered. You can add these URLs to the mappings file. For
        simple deployments, it is not uncommon for this file to contain
        no additional URLs. If you include the
        `additionalURLFile=additionalurl.txt` parameter, you can specify
        a different name for this file. For further details about this
        parameter, see [Repository tools command to generate the server
        rename mappings
        file](ServerRenameRepositoryToolsCommandLineRef#ServerRenameRepoToolsCmdGenerateURLMappings).
        Verify that there are no errors in the log file at
        `JazzInstallDir/server/repotools-jts_generateURLMappings.log`.
4.  Review and edit the generated mapping file carefully. Look for typos
    in the host name, port or root contexts. Some of these typos are not
    detectable by the server rename tools and can lead to a
    nonfunctioning product. To familiarize yourself with the structure
    of the mapping file, see [Mapping file for server
    rename](ServerRenamePlanningFor#ServerRenameMappingFile).
    1.  Verify that a source-target pair exists for every application
        being renamed and for the CLM Help WAR file.
    2.  Edit the `target=` urls for the entries that you want to rename
        to be the correct targets. RED **Note:** ENDCOLOR If you are
        renaming a port number of the Jazz Team Server or any
        application, you will need to update the port information in the
        application server after the rename, but before the servers are
        restarted. For details, see the "Changing the port numbers for
        the application server" topic in the Jazz Team Server Installing
        book in the [IBM Knowledge
        Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
        If you are renaming a context root of the Jazz Team Server or
        any application, see Changing the context root.
    3.  Using a pound sign (#), comment out the source-target pair of
        any URLs that you do not want to be renamed.
    4.  Review the list of affected URLs. Although the command searches
        for all known URLs in the deployment, it is possible that some
        are missed. If any of these affected URLs need to be mapped,
        uncomment the source/target pair for the affected URL and
        provide the new target URL. If you have any doubts about the
        environment, talk to an administrator before proceeding with the
        rename.
    5.  Review the `additionalurls` file. For details, see [Repository
        tools command to generate the server rename mappings
        file](ServerRenameRepositoryToolsCommandLineRef#ServerRenameRepoToolsCmdGenerateURLMappings).
        RED **Note:** ENDCOLOR If any configuration changes are made to
        the CLM deployment before you proceed to the actual rename,
        including registering additional applications, you will need to
        regenerate the mapping file.
5.  Use the `repotools-jts -verifyURLMappings` command to verify the
    mapping file.
    -   RED **Windows:** ENDCOLOR
        `repotools-jts.bat -verifyURLMappings mappingFile=mappings.txt repositoryURL`
        adminUserId= adminPassword==
    -   RED **UNIX, Linux:** ENDCOLOR
        `./repotools-jts.sh -verifyURLMappings mappingFile=mappings.txt repositoryURL=serverURL adminUserId=adminId adminPassword=adminPassword`
        For further details about the types of verifications that this
        command performs, see [Repository tools command to verify a
        mapping
        file](ServerRenameRepositoryToolsCommandLineRef#ServerRenameVerifyMappingFile).
6.  If your scenario involves new hardware, install CLM on the new
    computers. Do not run the Jazz Setup wizard or start the Jazz Team
    Server. For details about supported software versions, see
    [Supported scenarios for using server
    rename](ServerRenamePlanningFor#ServerRenameSupportedScenarios). For
    details about the installation process, see the "Installing Jazz
    Team Server and the Rational solution for Collaborative Lifecycle
    Management applications" topic in the Jazz Team Server Installing
    book in the [IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

### What to do next [what-to-do-next]

Proceed to renaming the server. For details, see Moving a pilot or full
production deployment by using server rename or Setting up a test
staging environment with production data.

\#ServerRenameSettingUpTestStagingEnv

## Setting up a test staging environment with production data

Learn how to use the server rename feature to prepare a staging
environment with production data. A staging environment is a test
sandbox that is isolated from the production environment. It can be used
to try out new features or functions with real data without impacting
the production database.

### Before you begin [before-you-begin]

-   To enable server rename, you must obtain a feature key file from IBM
    Software Support. When contacting IBM support, mention that you are
    requesting a "Server rename feature key file". The key file is named
    `ImportURLMappings.activate`. Once received, copy the file to the
    `JazzInstallDir/server/conf` directory for the applications that you
    will rename.
-   Before you proceed with the rename, check that the required version
    of the CLM software is installed and that your environment meets the
    criteria for a server rename. For details, see [Software version
    requirements](ServerRenamePlanningFor#SwVersionReq) and [Supported
    scenarios for using server
    rename](ServerRenamePlanningFor#ServerRenameSupportedScenarios).
-   Decide whether you are going to move the deployment to new hardware
    or keep the same hardware (rename-in-place). In the following steps,
    your current server environment is called the source environment.
    The server environment that you are moving to is called the target
    environment. If you are performing a rename-in-place, the target
    environment refers to a new location on the same server, or set of
    servers in a distributed deployment.
-   Review [Impact of server rename on the Rational solution for
    Collaborative Lifecycle
    Management](ServerRenameImpactOnRationalSolutionForCLM) to
    understand the actions you will need to take when the Jazz Team
    Server and CLM applications are renamed.
-   Decide whether you are going to keep the existing application server
    or migrate to a new one. If you are planning to move to a new
    application server, see one of the following topics in the Jazz Team
    Server Upgrading and Migrating book of the [IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html)
    as appropriate to your environment: "Switching from Apache Tomcat to
    WebSphere Application Server" or "Changing WebSphere Application
    Server installations and instances".
-   Decide whether you are going to keep the existing database or move
    to a new one. If you are planning to move to a new database, see one
    of the following topics as appropriate to your environment: Moving
    CLM databases to a different database server or Changing CLM
    databases to a different database vendor.
-   Setting up server rename can take several attempts. If your setup
    takes more than one attempt, you will need to restore your
    environment to a clean state between attempts. For instructions on
    restoring to a clean state, see [Recovering from common
    problems](ServerRenameVerifyingAndTroubleshooting#RecoveringFromCommonProblems).

### About this task [about-this-task-1]

The server rename feature uses a mapping file to determine the URLs to
be renamed. A `repotools` command is provided to generate an initial
mapping file for you. The mapping file contains source-target pairs for
the Jazz Team Server and all applications, as well as any other URLs
contributed by applications. For details about the mapping file, see
[Mapping file for server
rename](ServerRenamePlanningFor#ServerRenameMappingFile). For
information sample topology diagrams and mapping files, see [Setting up
a test staging
environment](ServerRenamePlanningFor#SettingUpTestStagingEnvironment).

When you are planning a staging environment, you need to be especially
careful not to contaminate production data or vice versa. The staging
environment must be isolated with no connections to any part of the
production environment, including the production database. You
accomplish this two ways, by adding entries to the hosts file, if it is
allowed in your environment, and by creating mappings to mask the
servers that are not present in your staging environment. Be sure to
include in the mapping any additional CLM servers or non-CLM products
that might be connected to the production server. See substep d. of step
3 and [Mapping file for server
rename](ServerRenamePlanningFor#ServerRenameMappingFile) for details.

For example, you might have a Change and Configuration Management (CCM)
application in one production server with links to CCM in another
production server, and links to Quality Management (QM) in still another
production server. Furthermore, you might have integrations with non-CLM
products, such as Rational ClearQuest. In this case, first mask out the
URLs of the additional CCM and QM servers. Also ensure that the URL for
Rational ClearQuest is masked out or otherwise mapped to a staged
Rational ClearQuest gateway server.

RED **Important:** ENDCOLOR Do not connect a Rational Team Concert
client to both the production and staging repositories. Always use a
staging workspace for connecting to the staging server.

### Procedure [procedure-1]

1.  Prepare for the rename by following the steps that are described in
    Preparing the mapping file. Be sure to create dummy mappings for any
    of the affected URLs in the mapping file. This practice avoids
    cross-linking between the staging and production environments. For
    details, see [Mapping file for server
    rename](ServerRenamePlanningFor#ServerRenameMappingFile). The result
    of the preparatory phase is a mapping file that is generated on the
    original, source Jazz Team Server. After you carefully review and
    edit the mapping file, copy it to the `JazzInstallDir\server`
    directory on the target Jazz Team Server in the staging environment.
2.  Back up the production environment and copy text indexes and
    application configuration files to the target staging server. For
    distributed systems, go to the appropriate server to copy the files.
    RED **Note:** ENDCOLOR If you are performing a rename-in-place and
    not moving to new hardware, you are copying the environment from one
    installation to a second installation on the same system. Because
    you need to stop the production servers while you perform these
    steps, be sure to choose a convenient time to perform the backup,
    preferably right before you set up the staging environment. If any
    changes are made to the production environment before you proceed to
    the rename, you will need to regenerate the mapping file before you
    import it into the staging server. While the servers are down, users
    are unable to create or traverse links from any external systems
    that are integrated with the CLM deployment about to be renamed.
    1.  Stop the Jazz Team Server and any distributed CLM applications
        that are registered with the Jazz Team Server in the production
        environment.
    2.  Back up all of the databases in the CLM 4.0 production
        environment, including the Jazz Team Server database, the
        databases for the CCM and QM applications, the data warehouse
        database, and the RRDI content store database. Copy the
        databases from the production to the staging environment by
        following the steps in Configuring your deployment after a
        database server move.
    3.  Copy the `JFS/text` indexes from the source production server to
        the target staging server. The following examples for a Linux
        server assume that the drives for the staging computers are
        mounted on the network. If it is not possible to mount the
        drives for the staging computers on the network, use other file
        transfer methods to ensure that the files are copied.

cp -R SourceJazzInstallDir/server/conf/jts/indices
TargetJazzInstallDir/server/conf/jts cp -R
SourceJazzInstallDir/server/conf/ccm/indices
TargetJazzInstallDir/server/conf/ccm cp -R
SourceJazzInstallDir/server/conf/qm/indices
TargetJazzInstallDir/server/conf/qm

1.  Copy the application configuration files from the source production
    server to the target staging server. (For distributed systems, go to
    the appropriate server to copy the files.) As with the previous
    step, the next examples are for a Linux server and assume that the
    drives for the staging computers are mounted on the network. cp
    SourceJazzInstallDir/server/conf/jts/teamserver\*.properties
    TargetJazzInstallDir/server/conf/jts

cp SourceJazzInstallDir/server/conf/ccm/teamserver**.properties
TargetJazzInstallDir/server/conf/ccm cp
SourceJazzInstallDir/server/conf/qm/teamserver**.properties
TargetJazzInstallDir/server/conf/qm cp
SourceJazzInstallDir/server/conf/admin/admin.properties\*
TargetJazzInstallDir/server/conf/admin cp
SourceJazzInstallDir/server/conf/admin/friends.rdf\*
TargetJazzInstallDir/server/conf/admin cp
SourceJazzInstallDir/server/conf/rm/teamserver.properties
TargetJazzInstallDir/server/conf/rm a. Copy the mapping file to the
`TargetJazzInstallDir\server` directory on the staging server. For
details about the mapping file, see Preparing the mapping file. RED
**Note:** ENDCOLOR If any configuration changes are made to the CLM
deployment before you perform the next step, you will need to regenerate
the mapping file. a. Restart all of the CLM servers, and allow users to
continue to use the production environment. The remaining steps apply to
the staging test environment. 1. Perform the following steps in the
staging test environment. a. Optional: Differentiate the staging servers
from the production servers by uploading a theme. RED **Learn more about
themes:** ENDCOLOR Because the staging and production servers have the
same data, it can be difficult to distinguish between the two. To help
differentiate the staging servers from the production servers, you can
use a theme on the staging servers to make it easy to see which server
you are working on. To upload a new theme on the Jazz Team Server, type
`https://fully.qualified.hostname:9443/jts/admin`, click **Servers**,
and then click **Themes**. To upload a new theme for Change and
Configuration Management, type
`https://fully.qualified.hostname:9443/ccm/admin` and click **Themes**.
To upload a new theme for Quality Management, type
`https://fully.qualified.hostname:9443/qm/admin` and click **Themes**.
In all cases, click **Browse** and select a `themes.zip` file. You can
find sample themes at [Uploading a new
theme](https://jazz.net/wiki/bin/view/Main/WebUITheming#Uploading_a_New_Theme).
For more information about themes, see "Configuring themes" in the Jazz
Team Server Administering book in the [IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
a. Restore the database backups from the production environment to the
staging environment. It is a best practice to use a separate database
server in the staging environment to avoid stressing the production
database server. a. Replace the database connection parameters in the
`JazzInstallDir/server/conf/applicationName/teamserver.properties` files
so that they point to the connection parameters for the staging copy of
the database in the test environment. These parameters include the
entries for the `jts` database, the `ccm` and `qm` application
databases, the data warehouse database, and updated passwords. RED
**Attention:** ENDCOLOR This step is important to complete before you
continue with the next steps in the task. Before you run the
`repotools-jts -importURLMappings` command, it is important that you
verify the `teamserver.properties` files are pointing to the staging
copy of the database in the test environment. Otherwise, if the
`teamserver.properties` files specify connection parameters to the
database in the production environment, running the `-importURLMappings`
command will corrupt the production database. RED **Important:**
ENDCOLOR You must update only the database connection parameters in the
`teamserver.properties` files. Do not update any other entries in these
`teamserver.properties` files as these properties are reserved and
modified by the server rename process. For example, the public URI
property: `com.ibm.team.repository.server.webapp.url` a. As an extra
precaution to the dummy mappings in the mapping file, if it is allowed
in your environment, update your hosts file to prevent access to the
production system URLs and to prevent accidental edits to artifacts in
the production server. The goal here is to resolve the host names to a
false IP address that is not being used by any of the CLM servers in the
production environment. Thus, if a server in the staging environment
tries to establish a connection to a production server, the connection
will fail. Make a list of all of the distinct host names that appear in
your mapping file. These host names might be source URLs or affected
URLs. For each host name, create an entry in the hosts file that maps
the host name to a false IP address. You need to edit the hosts file for
all of the servers in your staging environment, including third-party
servers and client workstations. The following host file shows sample
entries for your staging server: \# 10.10.10.10 refers to an IP address
that does not host a clm application. 10.10.10.10 ProductionServerP1
10.10.10.10 ProductionServerP2 10.10.10.10 ProductionServerP3

1.  Open a command prompt window in the `JazzInstallDir\server`
    directory and import the mappings file into the target Jazz Team
    Server by using the `repotools-jts -importURLMappings` command. RED
    **Attention:** ENDCOLOR Before you run the
    `repotools-jts -importURLMappings` command, it is important that you
    verify the `teamserver.properties` files are pointing to the staging
    copy of the database in the test environment. Otherwise, if the
    `teamserver.properties` files specify connection parameters to the
    database in the production environment, running the
    `-importURLMappings` command will corrupt the production database.
    -   If you have an all-in-one deployment, import the mappings file
        by using the `repotools-jts -importURLMappings` command: RED
        **Windows:** ENDCOLOR
        `repotools-jts.bat -importURLMappings fromFile="C:\mappings.txt"`
        RED **UNIX, Linux:** ENDCOLOR
        `./repotools-jts.sh -importURLMappings fromFile="opt/mappings.txt"`
        The rename begins offline on the Jazz Team Server, before the
        server is restarted.
    -   If you have a distributed deployment and are allowed to map
        network drives, map a network drive from the Jazz Team Server
        host to each of the application hosts. Then, create a file (for
        example, `serverConfFile.txt`) that contains a list of the
        remote `server/conf` directories in your deployment in the
        following format:

\# Remote CCM server x:/JazzTeamServer/server/conf \# Remote QM server
y:/JazzTeamServer/server/conf \# Remote RM server
z:/JazzTeamServer/server/conf

Finally, proceed with the `repotools-jts -importURLMappings` command and
add the `serverConfFile=` parameter as shown next. RED **Windows:**
ENDCOLOR
`repotools-jts.bat -importURLMappings fromFile="C:\mappings.txt" serverConfFile="C:\serverConf.txt"`
RED **UNIX, Linux:** ENDCOLOR
`./repotools-jts.sh -importURLMappings fromFile="/opt/mappings.txt" serverConfFile="/opt/serverConf.txt"`

-   If you have a distributed CLM deployment and are not allowed to
    remap network drives, proceed with the
    `repotools-jts -importURLMappings` command as shown next. RED
    **Windows:** ENDCOLOR
    `repotools-jts.bat -importURLMappings fromFile="C:\mappings.txt"`
    RED **UNIX, Linux:** ENDCOLOR
    `./repotools-jts.sh -importURLMappings fromFile="opt/mappings.txt"`
    Then, copy the `server/conf/jts/.mappingEvent` file to the remote
    application configuration directories
    (`server/conf/application_name`), that is, `ccm`, `qm`, and `rm`.
    You must copy the `.mappingEvent` file after you import the mapping
    file but before you start the server. The `.mappingEvent` file
    contains information that the applications need to contact the Jazz
    Team Server at its new location. The `.mappingEvent` file contents
    are the same for a Jazz Team Server and its registered applications.
    Verify that the rename is successful by checking the console output
    and the `server/repotools-jts_importURLMappings.log` file. If any
    errors are displayed, or if you realize that you made a mistake in
    your mapping file, see [Troubleshooting server
    rename](ServerRenameVerifyingAndTroubleshooting#ServerRenameTroubleshooting)
    to pinpoint and fix the problem. RED **Note:** ENDCOLOR Rename
    servers running on z/OS by using sample JCL member
    `HLQ.SBLZSAMP(BLZRENAM)`. For detailed customization instructions,
    see the comment header of `BLZRENAM`. 4. Start the Jazz Team Server
    and any distributed CLM applications that are registered with the
    Jazz Team Server. The CLM applications will synchronize with the
    Jazz Team Server to apply the URL mappings and update their data
    warehouse data. This process generally takes about 5 minutes for a
    small data set and up to 30 minutes or more for a large data set. 5.
    Log in to the Jazz Team Server at
    `https://new host:port/jts/serverRenameStatus.Logging` starts the
    renaming process. When the rename is complete, you can verify the
    rename and take any corrective action that is necessary. For
    details, see [Verifying URLs and links after a server
    rename](ServerRenameVerifyingAndTroubleshooting#VerifyingURLsAndLinks). 6.
    Before you complete the verification process, ensure that you have
    performed any additional product-specific verifications that are
    described in [Completing the server rename verification
    process](ServerRenameVerifyingAndTroubleshooting#ServerRenameCompletingVerification).
    When you are confident that the renamed data is correct, click the
    **I have verified the server rename** check box and click
    **Finish**. The Jazz Team Server and all registered applications
    exit read-only mode and normal product use can resume. RED **Note:**
    ENDCOLOR If you introduced dummy mappings to protect the production
    environment, you will see errors about these URLs in the
    Applications and Friends section of the Application Diagnostics page
    on the staged server. If you have multiple linked deployments, do
    not complete the wizard until you have validated the data in all
    deployments. 7. Optional: Configure Rational Reporting for
    Development Intelligence (RRDI) in the target staging environment.
    For details, see Configuring RRDI after server rename. 8. If you are
    including other components in your staging environment, see [Impact
    of server rename on the Rational solution for Collaborative
    Lifecycle Management](ServerRenameImpactOnRationalSolutionForCLM)
    and [Impact of server rename on integrated products (versions 4.0.1
    and later)](ServerRenameImpact401).

\#ServerRenameMovingPilotOrFullProdDeployment

## Moving a pilot or full production deployment by using server rename

Learn how to use the server rename feature to move a pilot or full
production deployment.

### Before you begin [before-you-begin-1]

-   To enable server rename, you must obtain a feature key file from IBM
    Software Support. When contacting IBM support, mention that you are
    requesting a "Server rename feature key file". The key file is named
    `ImportURLMappings.activate`. Once received, copy the file to the
    `JazzInstallDir/server/conf` directory for the applications that you
    will rename.
-   Before you proceed with the rename, check that the required version
    of the CLM software is installed and that your environment meets the
    criteria for a server rename. For details, see [Software version
    requirements](ServerRenamePlanningFor#SwVersionReq) and [Supported
    scenarios for using server
    rename](ServerRenamePlanningFor#ServerRenameSupportedScenarios).
-   Decide whether you are going to move the deployment to new hardware
    or keep the same hardware (rename-in-place). In the following steps,
    your current server environment is called the source environment.
    The server environment that you are moving to is called the target
    environment. If you are performing a rename-in-place, the target
    environment refers to a new location on the same server, or set of
    servers in a distributed deployment.
-   Review [Impact of server rename on the Rational solution for
    Collaborative Lifecycle
    Management](ServerRenameImpactOnRationalSolutionForCLM) to
    understand the actions you will need to take when the Jazz Team
    Server and CLM applications are renamed.
-   Decide whether you are going to keep the existing application server
    or migrate to a new one. If you are planning to move to a new
    application server, see one of the following topics in the Jazz Team
    Server Upgrading and Migrating book of the [IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html)
    as appropriate to your environment: "Switching from Apache Tomcat to
    WebSphere Application Server" or "Changing WebSphere Application
    Server installations and instances".
-   Decide whether you are going to keep the existing database or move
    to a new one. If you are planning to move to a new database, see one
    of the following topics as appropriate to your environment: Moving
    CLM databases to a different database server or Changing CLM
    databases to a different database vendor.
-   Setting up server rename can take several attempts. If your setup
    takes more than one attempt, you will need to restore your
    environment to a clean state between attempts. For instructions on
    restoring to a clean state, see [Recovering from common
    problems](ServerRenameVerifyingAndTroubleshooting#RecoveringFromCommonProblems).
    RED **Note:** ENDCOLOR After the rename, the source CLM servers must
    be permanently taken out of service to avoid contamination of the
    production environment.

### About this task [about-this-task-2]

The server rename feature uses a mapping file to determine the URLs to
rename. A `repotools` command is provided to generate an initial mapping
file. The mapping file contains source-target pairs for the Jazz Team
Server and all applications, and any other URLs contributed by
applications. For details about the mapping file, see [Mapping file for
server rename](ServerRenamePlanningFor#ServerRenameMappingFile). For
sample topology diagrams and mapping files, see [Topologies and mapping
files for the pilot-to-production
scenario](ServerRenamePlanningFor#PilotToProdScenario).

### Procedure [procedure-2]

1.  Prepare and review the mapping file in advance of the actual rename
    while your servers are still online, following the steps described
    in Preparing the mapping file. The result of the preparatory phase
    is a mapping file that is generated on the source Jazz Team Server.
    The mapping file contains source-target pairs for the Jazz Team
    Server and all applications, and any other URLs contributed by
    applications.
2.  Back up the existing source environment and copy text indexes and
    application configuration files to the new target installation. For
    distributed systems, go to the appropriate server to copy the files.
    RED **Note:** ENDCOLOR If you are performing a rename-in-place and
    not moving to new hardware, you are copying the environment from one
    installation to a second installation on the same system.
    1.  Stop the Jazz Team Server and any distributed CLM applications
        that are registered with the Jazz Team Server. In addition, stop
        any other applications that are affected by the server rename,
        such as the Jazz Build Engine, or any affected, supported
        integrations, such as Rational Reporting for Development
        Intelligence (RRDI), Rational ClearCase, or Rational ClearQuest.
        RED **Note:** ENDCOLOR While the servers are down, users are
        unable to create or traverse links from any external systems
        that are integrated with the CLM deployment about to be renamed.
    2.  Back up the databases for the source environment, including the
        Jazz Team Server database, the databases for the CCM and QM
        applications, the data warehouse database, and the RRDI content
        store database, if you are using RRDI. If you are changing the
        database server or vendor, see Configuring your deployment after
        a database server move for additional steps.
    3.  Copy the `JFS/text` indexes from the source installation to the
        target installation. The following examples for a Linux server
        assume that the drives for the target production computers are
        mounted on the network. If you cannot mount the drives on the
        network in your environment, use other file transfer methods to
        ensure that the files are copied.

cp -R SourceJazzInstallDir/server/conf/jts/indices
TargetJazzInstallDir/server/conf/jts cp -R
SourceJazzInstallDir/server/conf/ccm/indices
TargetJazzInstallDir/server/conf/ccm cp -R
SourceJazzInstallDir/server/conf/qm/indices
TargetJazzInstallDir/server/conf/qm cp -R
SourceJazzInstallDir/server/conf/rm/indices
TargetJazzInstallDir/server/conf/rm

1.  Copy the application configuration files from the source
    installation to the target production installation. As with the
    previous step, the next examples are for a Linux server and assume
    that the drives for the target production computers are mounted on
    the network.

cp SourceJazzInstallDir/server/conf/jts/teamserver**.properties
TargetJazzInstallDir/server/conf/jts cp
SourceJazzInstallDir/server/conf/ccm/teamserver**.properties
TargetJazzInstallDir/server/conf/ccm cp
SourceJazzInstallDir/server/conf/qm/teamserver**.properties
TargetJazzInstallDir/server/conf/qm cp
SourceJazzInstallDir/server/conf/admin/admin.properties**
TargetJazzInstallDir/server/conf/admin cp
SourceJazzInstallDir/server/conf/admin/friends.rdf\*
TargetJazzInstallDir/server/conf/admin cp
SourceJazzInstallDir/server/conf/rm/teamserver.properties
TargetJazzInstallDir/server/conf/rm

1.  Copy the mapping file to the `TargetJazzInstallDir\server` directory
    on the target production server. 1. Perform the offline portion of
    server rename by importing the mapping file into the target
    production Jazz Team Server. Use the
    `repotools-jts -importURLMappings` command.
2.  If you have an all-in-one deployment, import the mappings file by
    using the `repotools-jts -importURLMappings` command as follows:
    -   RED **Windows:** ENDCOLOR
        `repotools-jts.bat -importURLMappings fromFile=".\mappings.txt" serverConfFile=".\serverConf.txt"`
    -   RED **UNIX, Linux:** ENDCOLOR
        `./repotools-jts.sh -importURLMappings fromFile="./mappings.txt" serverConfFile="./serverConf.txt"`
        The rename will begin offline on the Jazz Team Server before the
        server is restarted.
3.  If you have a distributed deployment and are allowed to map network
    drives, map a network drive from the Jazz Team Server host to each
    of the application hosts. Then, create a file (for example,
    `serverConfFile.txt`) that contains a list of the remote
    `server/conf` directories in your deployment in the following
    format:

\# Remote CCM server x:/JazzTeamServer/server/conf \# Remote QM server
y:/JazzTeamServer/server/conf \# Remote RM server
z:/JazzTeamServer/server/conf

Finally, proceed with the `repotools-jts -importURLMappings` command and
add the `serverConfFile` parameter as shown next.

-   RED **Windows:** ENDCOLOR
    `repotools-jts.bat -importURLMappings fromFile=".\mappings.txt" serverConfFile=".\serverConf.txt"`
-   \* RED **UNIX, Linux:** ENDCOLOR
    `./repotools-jts.sh -importURLMappings fromFile="./mappings.txt" serverConfFile="./serverConf.txt"` a.
    If you have a distributed CLM deployment and are not allowed to
    remap network drives, proceed with the
    `repotools-jts -importURLMappings` command (without the
    `serverConfFile` parameter). Then, copy the
    `server/conf/jts/.mappingEvent` file to the remote application
    configuration directories (`server/conf/application_name`), that is,
    `ccm`, `qm`, and `rm`. The event file is generated when you import
    the mappings. You must copy the `.mappingEvent` file after you
    import the mapping file but before you start the server. The
    `.mappingEvent` file contains information that the applications must
    contact the Jazz Team Server at its new location. The
    `.mappingEvent` file contents are the same for a Jazz Team Server
    and its registered applications. RED **Note:** ENDCOLOR Rename
    servers that are running on z/OS by using sample JCL member
    HLQ.SBLZSAMP(BLZRENAM). See the comment header of BLZRENAM for
    detailed customization instructions. Verify that the rename is
    successful by checking the console output and the
    `JazzInstallDir/server/repotools-jts_importURLMappings.log` file. If
    any errors are displayed, or if you realize that you made a mistake
    in your mapping file, see [Troubleshooting server
    rename](ServerRenameVerifyingAndTroubleshooting#ServerRenameTroubleshooting)
    to pinpoint and fix the problem. 1. Start the Jazz Team Server and
    any distributed CLM applications that are installed. The CLM
    applications will synchronize with the Jazz Team Server to apply the
    URL mappings and update their data warehouse data. The
    synchronization should take about 5 minutes for a small data set and
    up to 30 minutes or more for a large data set. 1. Log in to the Jazz
    Team Server. \* If you are renaming the Jazz Team Server, log in to
    the target server at `https://new host:port/jts/serverRenameStatus`.
    \* If you are renaming one or more of the CLM applications but not
    the Jazz Team Server, log in to the source server at
    `https://source host:port/jts/serverRenameStatus.` Logging in to the
    Jazz Team Server starts the actual renaming process. When the rename
    is complete, you can verify the rename and take any corrective
    action that is necessary. During the verification process, the Jazz
    Team Server and all applications are placed in read-only mode, but
    you are able to browse data, and look for broken links and unmapped
    URLs. For details, see [Verifying URLs and links after a server
    rename](ServerRenameVerifyingAndTroubleshooting#VerifyingURLsAndLinks). 1.
    Before you complete the verification process, ensure that you have
    performed any additional product-specific verifications that are
    described at Completing the server rename verification process. When
    you are confident that the renamed data is correct, click the **I
    have verified the server rename** check box and click **Finish**.
    The Jazz Team Server and all registered applications will exit
    read-only mode and normal product use can resume. 1. Optional:
    Configure Rational Reporting for Development Intelligence (RRDI) in
    the target production environment. For details, see Configuring RRDI
    after server rename. 1. Perform any additional post-server rename
    steps that are required for integration with other components and
    products such as the Jazz Build Engines, Rational Reporting,
    Rational Team Concert clients, Rational ClearQuest, or Rational
    ClearCase. For details, see [Impact of server rename on the Rational
    solution for Collaborative Lifecycle
    Management](ServerRenameImpactOnRationalSolutionForCLM). 1. Full
    production only: If you have a second Jazz Team Server or additional
    CLM applications that are linked to the renamed Jazz Team Server,
    you must run `repotools-jts -importURLMappings` on the second Jazz
    Team Server. This step is necessary to update the links from the
    second server to the renamed server. RED **Important:** ENDCOLOR Do
    not generate a new mapping file. You must use the same mapping file
    that you used for the first renamed server. a. Copy the edited
    mappings file from the first server to the second server. Be sure to
    include any corrective mappings that you applied from the
    verification process. a. Review the mapping file and if necessary,
    remove any source-target pairs that you do not want to apply to the
    second server. a. Perform the rename on the second server by
    repeating Steps 3 through 6 on the second Jazz Team Server.

\#ConfiguringRRDIAfterServerRename

## Configuring RRDI after server rename

After a rename of the Jazz Team Server or any of the CLM applications,
you will need to configure Rational Reporting for Development
Intelligence (RRDI) to work in the new production or staging
environment.

### Procedure [procedure-3]

1.  Back up the following databases from the source environment and
    restore them on a new database server for the new installation of
    RRDI in the target environment.
    -   The content store database (for example, RICM, if it has not
        already been backed up and restored)
    -   The data warehouse (for example, RIDW, if it has not already
        been backed up and restored)
2.  If this is a new installation of RRDI, complete the following steps.
    1.  Install Rational Reporting for Development Intelligence version
        2.0 or higher in the target environment. For details, see
        "Installing Rational Reporting for Development Intelligence
        using Installation Manager" in the Rational Reporting Installing
        book in the [IBM Knowledge
        Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
    2.  Configure the report server by running the RRDI Setup
        application. For details, see "Configuring and integrating
        Rational Report Server after the installation" in the Rational
        Reporting Installing book in the [IBM Knowledge
        Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
        Remember to perform these actions:
        -   In the Configure Content Store Database page, specify the
            connection properties for the content store database (for
            example, RICM) that you restored.
        -   In the Configure Data Warehouse page, specify the connection
            properties for the data warehouse database (for example,
            RIDW) that you restored.
    3.  Log on to the Jazz Team Server and verify that the report server
        URLs stored in Advanced Properties of the Jazz Team Server and
        the CCM and QM Administration pages point to the production RRDI
        report server. If they do not point to the production system,
        update them accordingly. RED **Note:** ENDCOLOR If your mapping
        file contained mappings for the report server URL, this should
        have been updated automatically.
    4.  Verify that all previously imported reports from the pilot RRDI
        report server continue to work.
    5.  Any Cognos reports or report views with action set to View most
        recent report, must be rerun after a CLM server rename to have
        the cached HTML report updated.
        1.  Log on to the RRDI report server.
        2.  Look for reports or report views with cached output
            versions. RED **Note:** ENDCOLOR If a cached output version
            exists for a report or report view, you can click **View the
            output versions** for this report to view the cached
            reports. If the reports or report views were generated
            before the CLM server rename, you must rerun the reports or
            report views to update them. Otherwise, users running the
            reports or report views will see stale links pointing to the
            old CLM server.
        3.  Click **Run with Options** to rerun the reports or report
            views.
        4.  In the report viewer, click **Keep this version \> Save
            Report** to update the cached output versions associated
            with the reports or report views.
    6.  Import a new report from the target RRDI report server. Verify
        that the import is successful and that the imported report runs
        without issue.
    7.  If you have configured Rational Quality Manager live reports in
        RRDI, follow the steps to generate the `xdc` file for the new
        server and configure it in the 32-bit ODBC manager. For details,
        see "Setting up live reporting" in the Rational Reporting
        Installing book in the [IBM Knowledge
        Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
3.  If this is an existing installation of Rational Reporting for
    Development Intelligence, complete the following steps to update the
    `jazzns_config.xml` file with the new Jazz Team Server.
    1.  Start the Tomcat-based Rational Reporting for Development
        Intelligence setup server that runs the Setup application. For
        information on starting the setup server, see "Initializing the
        server for the Rational Reporting setup wizard" in the Rational
        Reporting Installing book in the [IBM Knowledge
        Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
    2.  Start the setup application by opening
        `https://localhost:10443/rrdi/setup` in your browser.
    3.  In the Common Task list, select **Configure Rational Reporting
        User Authentication**. The Configure Rational Reporting User
        Authentication wizard opens.
    4.  In the **Jazz Team Server URI** field, update the URI with the
        new URI for your Jazz Team Server. Then, click **Validate**. RED
        **Note:** ENDCOLOR You may be asked to enter your OAuth consumer
        secret before proceeding to the next step.
    5.  After the URI is validated, click **Configure**. The setup
        application restarts your web application.
    6.  Click \*Next\*; then, click **Finish**.
    7.  Open the report server in your browser to verify that the Jazz
        Team Server authentication is successful.

\#ServerRenameChangingTheContextRoot

## Changing the context root

Although it is most common to change the host name during a server
rename, it is also possible to change the context root. Doing so
requires a new server installation that mirrors the old installation,
but with new context roots. Make sure that you generate a mapping file
against the original server, as detailed in Preparing the mapping file.
Change the necessary context roots in this mapping file. For more
information about changing the context root, see [Case study: Server
rename (version 4.0.1)](ServerRenameCaseStudy)

### Before you begin [before-you-begin-2]

-   To enable server rename, you must obtain a feature key file from IBM
    Software Support. When contacting IBM support, mention that you are
    requesting a "Server Rename Feature Key File". The key file is named
    `ImportURLMappings.activate`. Once received, copy the file to the
    `JazzInstallDir/server/conf directory` for the applications that you
    will rename.
-   Before you proceed with the rename, check that the required version
    of the CLM software is installed and that your environment meets the
    criteria for a server rename. See [Software version
    requirements](ServerRenamePlanningFor#SwVersionReq) and [Supported
    scenarios for using server
    rename](ServerRenamePlanningFor#ServerRenameSupportedScenarios) for
    details.

### Procedure [procedure-4]

1.  Use Installation Manager to install a separate, Jazz Team Server.
    When you get to the Context Root Options panel, click **Select
    custom context root values** and enter your custom context root
    values. Even if you are renaming only the context root for a single
    application, you must install all of the applications that you
    intend to run. For further installation instructions, see
    "Installing the Rational solution for Collaborative Lifecycle
    Management by using IBM Installation Manager" in the Jazz Team
    Server Installing book in the [IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
2.  Copy the following configuration files from the old installation
    `server/conf/oldContextRoot` to the new installation
    `server/conf/newContextRoot`. Copy all of these configuration files,
    even if you are not renaming a particular application's context
    root. RED **Note:** ENDCOLOR If you changed the context roots in the
    old installation, replace these default examples with your own
    customized versions.
    -   From `server/conf/admin`, copy `admin.properties` and
        `friends.rdf`.
    -   From `server/conf/jts`, copy `teamserver.properties` and the
        `indices` directory.
    -   From `server/conf/ccm`, copy t`eamserver.properties` and the
        `indices` directory.
    -   From `server/conf/qm`, copy `teamserver.properties` and the
        `indices` directory.
    -   From `server/conf/rm`, copy `teamserver.properties` and the
        `indices` directory.
3.  Ensure that the following database properties in the
    `teamserver.properties` files for CCM, RM, QM, and JTS are pointed
    at the correct database locations.
    -   `com.ibm.team.repository.db.jdbc.location`
    -   `com.ibm.team.datawarehouse.db.jdbc.location` Finally, fix the
        relative text indices location to use the new location. Be sure
        to include the new context root in the path.
        com.ibm.team.fulltext.indexLocation=conf/new_context_root/indices/workitemindex 4.
        If you are using WebSphere Application Server, uninstall the
        applications from the old installation and install them in the
        new installation. Also, update JAZZ_HOME to point to the new
        installation. For details about deploying applications to
        WebSphere Application Server, see "Deploying applications for
        the Rational solution for Collaborative Lifecycle Management on
        WebSphere Application Server" in the Jazz Team Server Installing
        book in the [IBM Knowledge
        Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html). 5.
        If you are using the Tomcat user registry, to sync the existing
        users, copy the
        `OldJazzInstallDir/server/tomcat/conf/tomcat-users.xml` file to
        the `NewJazzInstallLocation/server/tomcat/conf` directory. 6.
        Follow the standard rename instructions, starting at the
        `importURLMappings` step. You must run the `importURLMappings`
        command against the new installation by using the generated
        mapping file from the old installation. Do not perform any
        additional steps against the old installation, which serves only
        as a backup until you are sure that the new installation is
        working correctly. RED **Note:** ENDCOLOR It is possible that
        the old application context root will appear in the server
        rename status UI. The UI displays the registered application
        name. By default, the name is the context root. Therefore, if
        you never changed the name from the default, the old context
        root is shown.
4.  Optional: Update the name of all renamed applications.
    1.  Log in to the Jazz Team Server administrative UI and go to the
        **Configuration \> Registered Applications**.
    2.  Click **Edit** and rename each application to its new context
        root or to any other name that you choose.

\#ServerRenameConfiguringDeploymentAfterDBMove

## Configuring your deployment after a database server move

Learn how to reconfigure your CLM deployment when a database moves or a
database vendor changes.

\#ServerRenameMovingCLMDBsToDiffSvr

### Moving CLM databases to a different database server

Learn how to reconfigure your CLM deployment when the database server
moves to new hardware.

#### About this task [about-this-task-3]

You might need to move your CLM databases in the following scenarios.

-   When moving a pilot deployment to production, if the database server
    being used in the pilot deployment is different from the server that
    will be used in production.
-   When a staging environment is being set up that uses its own
    database server and a copy of the production data.

#### Procedure [procedure-5]

1.  Back up the old database.
2.  Use database vendor-specific tools to migrate the data from the old
    database to the new database.
3.  For the Jazz Team Server, CCM, RM, and QM databases, update the
    following properties in the
    `server/conf/applicationName/teamserver.properties` file to point to
    the new CLM database location.
    -   `com.ibm.team.repository.db.vendor`
    -   `com.ibm.team.repository.db.jdbc.location`
    -   `com.ibm.team.repository.db.jdbc.password`
4.  For the Jazz Team Server, CCM, RM, and QM databases, update the
    following properties in the
    `server/conf/applicationName/teamserver.properties` file to point to
    the new data warehouse database location.
    -   `com.ibm.team.datawarehouse.db.jdbc.vendor`
    -   `com.ibm.team.datawarehouse.db.jdbc.location`
    -   `com.ibm.team.datawarehouse.db.jdbc.password`
    -   `com.ibm.team.datawarehouse.db.base.folder`
5.  For the Jazz Team Server, CCM, RM, and QM databases, run
    `repotools-applicationName -verify` to ensure that the new CLM
    database connection is successful.

\#ServerRenameChangingCLMDBsToDiffDBVendor

### Changing CLM databases to a different database vendor

You must change your CLM databases if you are using a different vendor
in production deployment than the one used in the pilot deployment. For
example, a small pilot deployment using Derby is being moved into
production using DB2.

#### Procedure [procedure-6]

1.  For the Jazz Team Server, CCM, RM, and QM databases, run
    `repotools-applicationName -export toFile=export.tar` to export the
    data from the old database.
2.  Copy the tar file from the old database server to the new database
    server if they reside on separate systems.
3.  For the Jazz Team Server, CCM, RM, and QM databases, update the
    following properties in the
    `server/conf/applicationName/teamserver.properties` file to point to
    the new location.
    -   `com.ibm.team.repository.db.vendor`
    -   `com.ibm.team.repository.db.jdbc.location`
    -   `com.ibm.team.repository.db.jdbc.password`
4.  For the Jazz Team Server, CCM, RM, and QM databases, run
    `repotools-applicationName -import fromFile=export.tar` to import
    the data in the new database.
5.  For the Jazz Team Server, CCM, RM, and QM databases, run
    `repotools-applicationName -verify` to ensure that the new database
    connection is successful.
6.  For the data warehouse database, rebuild the database on the new
    database platform.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: None [additional-contributors-none]
