META:TOPICINFO{author="yisu" date="1663706295" format="1.1"
version="1.11"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Migrating ELM to a New Environment DKGRAY Authors: Antoinette Lacobo, Susan Wu Build basis: None. [migrating-elm-to-a-new-environment-dkgray-authors-antoinette-lacobo-susan-wu-build-basis-none.]

ENDCOLOR

TOC{title="Page contents"}

## Introduction

This section will outline the process of migrating a ELM environment to
a new one. It does not provide step-by-step instructions on configuring
deployments, but that information can be found in the product
documentation (ELM Information Center) linked in the References Section.

For instruction on how to migrate JAS to a new hardware, see this
technote: <https://www.ibm.com/support/pages/node/6476864>

## Reasons Why You May Want to Move the Installation

-   To more robust hardware
-   To change the operating system
-   To a drive with more space
-   From an image system to a physical machine or vice-versa

## First Consideration is the Public URL

When you first installed ELM, you should have chosen a public URI that
is fully qualified and accessible from anywhere in the network where
users need to connect. That URI should have been based on a stable host
name that was rerouted through a domain name server (DNS). It should be
decoupled from the host names of the existing servers. If this is not
the case, you may have to consider going through a server rename after
the migration. You will also want to consider how you can restrict
access to the systems while migrating. If the source environment is
going to be removed from the network or de-commissioned after the
migration, you may not need the server rename.

This process is going to assume you have well-planned public URIs per
the product documentation.

## Server Timezone

For releases prior to 6.0.5, you cannot move applications to a server
running in a different timezone. Starting with 6.0.5, you can change the
timezone setting of an existing server (or migrate to a server in a
different timezone). If you are both upgrading from a pre-6.0.5 release
and migrating to a new environment, you should do the upgrade to 6.0.5
(or later) first. Otherwise, see the section below on migrating
configuration files for manual edits that must be applied.

## Summary of Migration

The steps for a migration are a combination of the following operations
listed below:

### 1. Backup/recovery

Before beginning any type of migration operation, you should ensure that
you have tested procedures to backup and restore your environment.

### 2. New Installation

You will need to perform many of the installation steps on the target
system as if you were creating a new one.

### 3. Upgrade

This procedure is only for migrating an environment, meaning move an
environment from one (the source) to another (the target), and not for
an upgrade (change of software version). However, since a ELM upgrade is
a side-by-side upgrade and not an in-place upgrade, the steps and the
commands in the upgrade scripts which copy specific configuration files
from the JAZZ_HOME environment to the target system are the same for a
migration. You can still use much of the interactive upgrade guide to
help document the migration plan.

You should already be very familiar with the first two operations. If
you are familiar with upgrading a ELM environment already, then you
understand most of what is needed to migrate to a new environment.

## Steps to Migrate

### 1. Preparation

-   Review the steps below and the corresponding product documentation.
-   Assemble documentation for any customizations you made to the start
    up scripts, WAS profiles, WAS Liberty etc.
-   Create a test environment to test out the migration.
-   Plan the backup and downtime for the migration.
-   Create procedure to disable access to the source environment.

### 2. Installation

Follow the installation instructions in the product documentation under
the topic "Installing the IBM Engineering Lifecycle Management (ELM) "
for these subtopics:

-   Hardware and software requirements
-   Installing the ELM software (Jazz Team Server and applications). Do
    not run setup.
-   Installing the database: You do not need to set up the database but
    you do need to configure the target environment for using the
    existing ELM databases. This will include installing the database
    driver and setting environment variables.
-   Deploying and configuring the application server including the user
    registry:

For WAS Liberty Profile: the application server will get installed with
the ELM software.

For Web Sphere Profile: follow the instructions to install and configure
the server including the user registry. Make any adjustments to the
settings that you had customized in the source environment.

### 3. Shut down the source system

Disable access to the source environment from the network.

Shut down and backup the source environment.

### 4. Migrate existing configuration files

Copy the existing configuration files from the source (old_install_dir)
to the target (new_install_dir) environment. Include the following:

-   Database files if vendor is Derby: cp -R
    old_install_dir/server/conf/jts/derby/repositoryDB
    new_install_dir/server/conf/jts/derby

cp -R old_install_dir/server/conf/ccm/derby/repositoryDB
new_install_dir/server/conf/ccm/derby cp -R
old_install_dir/server/conf/qm/derby/repositoryDB
new_install_dir/server/conf/qm/derby and similarly for any other
applications that have Derby databases

-   Application Server if WAS Liberty Profile:

Copy/replace the following configuration files and any files you may
have customized (e.g. server.startup.bat). Note: if you are migrating
across operating systems, best practice is to use the installed
configuration files and add your customizations manually:

server-install-dir/server/liberty/servers/elm/server.xml
server-install-dir/server/liberty/servers/elm/conf/ldapUserRegistry.xml
(Note: if ldap host name is change, this file need to be updated with
the correct host name)
server-install-dir/server/liberty/servers/elm/conf/application.xml

If you are using the built in local user authorization, also back up the
user registry file:
server-install-dir/server/liberty/servers/elm/conf/basicUserRegistry.xml

If you provide a server certificate, that also need to be transferred.
You can find information about the storage location of the used
certificate in the server.xml file. The element keyStore contains a
location property that contains the file location. If this shows a file
or a relative path the default location for the file is in the following
location:
server-install-dir/server/liberty/servers/elm/conf/resources/security/

\* ELM application related configuration files including the following.
Note: make sure to update the com.ibm.team.repository.db.jdbc.location
parameter to in each teamserver.properties file to reflect the new db
connection string. For teamserver.properties file in jts, also update
the com.ibm.team.datawarehouse.db.jdbc.location parameter to point to
the data warehouse db connection string.

old_install/server/conf/jts/teamserver**.properties
TargetJazzInstallDir/server/conf/jts
old_install/server/conf/ccm/teamserver**.properties
TargetJazzInstallDir/server/conf/ccm
old_install/server/conf/dcc/teamserver**.properties
TargetJazzInstallDir/server/conf/dcc
old_install/server/conf/gc/teamserver.properties
TargetJazzInstallDir/server/conf/gc
old_install/server/conf/qm/teamserver**.properties
TargetJazzInstallDir/server/conf/qm
old_install/server/conf/relm/teamserver.properties
TargetJazzInstallDir/server/conf/relm
old_install/server/conf/rm/teamserver.properties
TargetJazzInstallDir/server/conf/rm old_install/server/conf/rs/**.**
TargetJazzInstallDir/server/conf/rs (copy the entire conf/rs folder from
the old install to the new install, replace the existing files in
conf/rs folder under the new install)
old_install/server/conf/lqe/lqe.properties
TargetJazzInstallDir/server/conf/lqe
old_install/server/conf/lqe/dbconnection.properties
TargetJazzInstallDir/server/conf/lqe
old_install/server/conf/lqe/lqe.node.id
TargetJazzInstallDir/server/conf/lqe old_install/server/conf/lqe/lqe.key
TargetJazzInstallDir/server/conf/lqe
old_install/server/conf/ldx/lqe.properties
TargetJazzInstallDir/server/conf/ldx
old_install/server/conf/ldx/dbconnection.properties
TargetJazzInstallDir/server/conf/ldx
old_install/server/conf/ldx/lqe.node.id
TargetJazzInstallDir/server/conf/ldx old_install/server/conf/ldx/lqe.key
TargetJazzInstallDir/server/conf/ldx

If you are migrating to a server running in a different timezone, then
you must upgrade to version 6.0.5 or later. It is recommended to do the
server upgrade first, but if the move is done first, then this property
should be added to every `teamserver.properties` file after it is copied
to the new server:

com.ibm.team.repository.db.timezone=

where is replaced by the [timezone
identifier](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)
for the timezone that was used by the old server (such as
"America/New_York" for U. S. Eastern time, for example).

If a data warehouse database is being used, then this property should
also be added to `teamserver.properties` as well:

com.ibm.team.datawarehouse.db.timezone=

Note that the property is only recognized in ELM 6.0.3, 6.0.4, 6.0.5,
and 6.0.6 fixpacks (and subsequent releases) released after August 2018.
If using an older version, the data warehouse database must be
completely regenerated in order to avoid issues when changing a server's
timezone.

### 5. Copy or Rebuild Indexes

The index files are referenced in the teamserver.properties file with
relative path locations (e.g.
com.ibm.team.fulltext.indexLocation=conf/qm/indices/workitemindex,
com.ibm.team.jfs.index.root.directory=indices). So these entries should
not have to change when you create new install areas. But after a new
installation, the index files under these directories would not match.
So you must copy the following index files from the source to the
target:

old_install/server/conf/jts/indices old_install/server/conf/ccm/indices
old_install/server/conf/dcc/indices old_install/server/conf/qm/indices
old_install/server/conf/rm/indices old_install/server/conf/gc/indices
old_install/server/conf/relm/indices
old_install/server/conf/lqe/indexTdb old_install
/server/conf/lqe/textIndex old_install /server/conf/lqe/shapeText
old_install /server/conf/lqe/shapeTdb
old_install/server/conf/lqe/historyText
old_install/server/conf/lqe/historyTdb
old_install/server/conf/ldx/indexTdb
old_install/server/conf/ldx/textIndex

If the operating systems are different, you should rebuild the indexes
with repotools commands. This will take longer and must be done with the
database running and the server shut down.

## Post Migration

1\. Ensure the clocks for the server and database are in sync.

2\. Ensure the JAZZ_HOME environment variable is set.

3\. Start the server.

4\. Log in as a user with jazzadmins and import the licenses.

5\. Smoke test.

6\. Enable network access to the new server.

## References for Detailed Instructions

Interactive Upgrade and Installation Guides available in this product
documentation: <https://www.ibm.com/docs/en/elm>

<https://jazz.net/wiki/bin/view/Deployment/BackupCLM>

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
