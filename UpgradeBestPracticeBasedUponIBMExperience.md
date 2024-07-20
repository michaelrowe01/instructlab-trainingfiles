META:TOPICINFO{author="paulellis" date="1419250621" format="1.1"
version="1.10"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Upgrade best practice based upon IBM experience [upgrade-best-practice-based-upon-ibm-experience]

DKGRAY Authors: Main.ChristopheElek, Main.SudarshaWijenayake,
Main.JamesHewitt, Main.JohnOwen, Main.SamSultana, Main.CarlGirouard,
Main.GeraldMitchell, Main.StevenBeard, Main.RosaNaranjo,
Main.RichardForziati, Main.TracyChen Build basis: None ENDCOLOR

TOC{title="Page contents"}

This article is a summary of the process used by three different IBM
teams to upgrade their CLM systems. Consider this document as a best
practice for upgrading CLM from version 4 to another version 4. Times
are approximate and do not reflect a supported performance standard by
IBM.

The three teams are the following:

1 The Functional Verification Test Team (FVT) tests the upgrade process
before IBM ships the product. They perform upgrades from one Sprint
milestone to another Sprint milestone. 1 The Rational Engineering
Service (RES) team manages the self host server, *jazz.net*, where most
CLM developers work. The upgrade occurs every sprint. They manage 30
other CLM systems. In some systems, the upgrade occurs daily, using the
latest build. 1 The Hursley team manages just over one hundred CLM
production systems which support development teams including WebSphere,
MQ and CICS

In this document, we are listing the set of high level steps each of the
previously named teams use. We also give an estimate on how long each
task takes.

## Preconditions

Before one can upgrade, there must be an environment to upgrade. This
article does not explain how to install a new server. The RES/Hursley
teams have existing systems in staging and production. To test the
upgrade process, FVT first installs an environment on a cloud system.

All three teams based their best practices out of the existing
documentation to upgrade a CLM system. We highly suggest you become
familiar with such documentation before exploring the best practices.
[Understand the Upgrade Process (IBM
InfoCenter)](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m4/topic/com.ibm.jazz.install.doc/topics/c_upgrade_overview.html)

## Retrieve the installable binaries from the server 1 hour

The FVT team retrieves the build to download based on the build ID. They
download the binaries from an internal site. The Hursley team uses the
official external link and downloads the binary on a staging server.
They perform 3 manual installations in a local staging server; they
install a server in three different context root setup. This step is
manual, there is no response file. The RES team downloads the ZIP file
for a certain build identifier from an internal website.

## Generate a response file 15 minutes

The FVT team has a GUI application that generates a specific response
file. The Hursley Team generates a new migration script for each
version. Each script contains the hardcoded location of the local
staging server. RES does not use IBM Installation Manager (IIM) and thus
does not have a response file. Instead, a set of configurable arguments
are stored in a configuration file and referenced by the script.

## Lay out files on the file system 5 minutes

The RES team unzips the zip file in a directory based on BUILD ID. The
script uses a configuration file/response file. The FVT team uses IBM
install Manager (IIM) and installs the new CLM in a location specified
by the user response file. The Hursley script copies files from the
local staging server to the instance server using the generated script
with hardcoded path. The files are copied to a new location, preserving
the files associated with the original CLM release in case the upgrade
needs to be backed out.

## Massaging extracted files 5 minutes

The FVT team does not modify any files. The Hursley team runs a script
to combine the configuration files, modify the tomcat LDAP realm, and
change some log properties. They created this script. The RES team uses
a script to setup the context root links, rename the WAR files, and
create links for the renamed WAR files. This is done to easily track
which specific build/version is deployed on which application server in
WebSphere at a glance. They also open and update the WAR files with a
custom theme and modify the default authentication method. They also
created the script themselves.

## Pre-upgrade before outage 5 minutes

This step is to prepare the migration process as much as possible
without starting any server outage to the current production system. The
RES team runs their CLMTOOLS script, that mimics the upgrade wrapper
migration part of the script but does not run any addTables script. They
also validate the online backup of the database is running.

## Outage start 5 minutes

At this point, each team stops the Application server to be upgraded.

## Backup 10 minutes

After the server is down, the HURSLEY and RES team do a validation of
the incremental online backup and then execute the indexes backup. For
the RES team, the index backup is a disk copy of indices to a different
location. For the Hursley team, the index backup is a filesystem backup
to Tivoli Storage Manager.

## Upgrade - 25 minutes

The FVT team runs the upgrade wrapper script. This performs all the
tasks in silent mode: Migrate, re-index (if required) and addTables. The
Hursley team changes the database userid permissions to allow changes to
the structure of the database, which is not permitted under day-to-day
conditions, and then runs the update wrapper script to migrate the
server. The RES team executes the install and addTable part of their
CLMTOOLS script. This runs a script to remove old War files and install
news ones, and then executes all addTables.

## Post upgrade cleanup 5 minutes

Hursley runs a script to cleanup their tomcat work directory. RES also
runs a script to clean up all temporary directories for WebSphere.

## Outage stop 10 minutes

At this point, the Hursley team copies the upgrade logs and application
server logs to a safe place. They clean all system logs and start the
Application server.

## Manual steps to finalize upgrade 20 minutes

All teams manually migrate Requirement Manager (RM) application. If
needed, they manually install the licenses and do a quick validation of
the system.

##### Related topics: [Deployment web home](DeploymentWebHome), [Installing, upgrading and migrating](DeploymentInstallingUpgradingAndMigrating) [related-topics-deployment-web-home-installing-upgrading-and-migrating]

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]
