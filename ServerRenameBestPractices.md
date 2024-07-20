META:TOPICINFO{author="lfrankel" date="1412984343" format="1.1"
version="1.3"} META:TOPICPARENT{name="ServerRename"}

# Case studies and best practices for server rename and moving to the Rational solution for Collaborative Lifecycle Managment 2012 [case-studies-and-best-practices-for-server-rename-and-moving-to-the-rational-solution-for-collaborative-lifecycle-managment-2012]

DKGRAY Authors: Main.RobinYehle, Main.DavidChadwick Build basis:
Rational solution for Collaborative Lifecycle Management 2012 ENDCOLOR

TOC{title="Page contents"}

The purpose of this article is to provide insight into real server
rename experiences and scenarios and offer best practices and guidance
as more users take advantage of this new feature in the Rational
solution for Collaborative Lifecycle Management 2012. Keep checking back
for updates and new information as it becomes available.

## Scenario 1: Pilot-to-Production Server Rename with Upgrade, Migration, and Hardware Change

We just successfully completed a pilot-to-production rename with a
customer who was running a pilot 3.x CLM server on Windows with Tomcat
and DB2. Their requirement was to upgrade to 4.0, migrate to WebSphere
Application Server running on Linux for System z, and cut over to their
corporate LDAP for their user registry. Basically the only thing
remaining the same was the DB2 database. While the actual server rename
steps are few in number and rather straightforward, server rename in the
context of all of these other changes becomes a daunting task. Following
are the steps that were taken to accomplish the end result:

1.  Upgrade the pilot CLM server (pilot_clm.customer.com) to 4.0. See
    <http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m3/topic/com.ibm.jazz.install.doc/topics/c_upgrade_overview.html>.
    This includes all of the standard 3.x to 4.0 upgrade steps
    including:
    1.  Taking down the system.
    2.  Backing up the database and configuration files.
    3.  Installing the 4.0 product as a side-by-side install.
    4.  Copying over and updating the configuration files.
    5.  Upgrading the databases using repotools addTables.
    6.  Upgrading the data warehouse.
    7.  Verifying the repository data by checking the repotools logs.
    8.  Starting the 4.0 applications and activating your 4.0 licenses.
    9.  Validating / spot checking data in each of the applications.
    10. Pilot server is now open for business running 4.0 software.
2.  Upgrade all Jazz Build Engines and eclipse clients to 4.0. If you
    are using 3.x Rational Build Agents or the ISPF client on z/OS, it
    is not necessary to upgrade these components prior to the rename,
    but you will need to upgrade them to take advantage of the new
    features in V4.0.
3.  Install the new production CLM V4.0 server and deploy on WebSphere
    Application Server on Linux for System z.
4.  Configure the new production server (prod_clm.customer.com) by going
    through setup connecting to a throwaway Derby database. Verify
    proper authentication from the corporate LDAP and that the WAS
    configuration seems to be working properly. This is a recommended
    step in this case because of all of the moving parts involved in
    moving to a new application server and new authentication server.
    This step may not be necessary if you are not making significant
    environment changes while moving your application server. Consider
    your own situation and make the choice that is right for you.
5.  Verify that several of the user credentials have the proper
    permissions based on their LDAP group membership.
6.  Shutdown the new production server.
7.  Perform the server rename procedure as outlined here: [Moving a
    pilot or full production deployment using server
    rename](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m3/topic/com.ibm.jazz.install.doc/topics/t_change_server_name.html)
    1.  The preparation steps can be performed while the pilot system is
        on-line:
        1.  Request a feature key from IBM support if you have not
            already done so.
        2.  Generate a mapping file, update it with your new production
            URLs, and send it to IBM support for review.
    2.  The off-line steps for this scenario should be done with the
        pilot and production servers off-line:
        1.  Back-up the pilot databases including the data warehouse.
        2.  Restore the pilot databases into the production database
            server if you are changing (not the case in this scenario).
        3.  Copy the JFS/text indices from pilot server to production
            server.
        4.  Copy and edit the teamserver.properties files for each
            application config folder from the pilot server to
            production server, adjusting the database entries and the
            LDAP entries to point to the production database server and
            the corporate LDAP server (as tested before).
        5.  Copy the remaining properties and rdf files specified in the
            help from pilot to production.
        6.  Copy the mapping file into the /server directory.
        7.  Copy the server rename feature key file into the server
            directory as well.
        8.  Issue the repotools-jts.sh importURLMappings
            fromFile=./mappings.txt command.
        9.  Since this was an all in one install on a single server, the
            .mappingEvent file did not have to be copied to other
            application servers.
        10. Verify that the rename was successful by looking for errors
            in the repotools-jts_importURLMappings.log file after the
            repotools-jts operation completes.
    3.  The on-line steps for server rename are then done:
        1.  Start the production jts server followed by the other
            applications.
        2.  Go to the /serverRenameStatus to watch the progress of the
            server rename as it is propagated to each of the
            applications.
        3.  When the rename completes, verify the project area linkages
            between the repositories to make sure the rename was
            successful.
        4.  Do some of the other suggested manual validation steps in
            the help page such as running the data warehouse ETLs and
            checking dashboard widgets and reports.
    4.  Notify users that the server rename is complete and to begin
        using the new public URL for their access to the system. Their
        existing eclipse workspaces can be reused. Simply update the
        repository connection to point to the new production server URL.

## Scenario 2: In-Place Pilot-to-Production Server Rename

The instructions in the CLM Information Center for performing a
pilot-to-production server rename are written with the expectation that
you are working with two servers. However, it is possible to perform an
in-place server rename on your pilot machine. When referencing the help,
simply understand that your source and target servers are one and the
same. For the step where you copy the indices and application
configuration files from pilot to production, you should instead create
a backup copy of these files from your server before performing the
rename.

##### Related topics: [ServerRename](ServerRename) [related-topics-serverrename]

##### Additional contributors: Main.RosaNaranjo [additional-contributors-main.rosanaranjo]
