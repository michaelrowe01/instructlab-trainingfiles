META:TOPICINFO{author="ushanka4" date="1629880632" format="1.1"
version="1.6"} META:TOPICPARENT{name="ServerRename"}

# Additional documentation for server rename DKGRAY Authors: Main.VaughnRokosz [additional-documentation-for-server-rename-dkgray-authors-main.vaughnrokosz]

Build basis: 6.x ENDCOLOR

TOC{title="Page contents"}

This page expands on the server rename documentation found in the
Knowledge Center. It will cover:

-   How to do a server rename if the Jazz Authorization Server is in use
-   What do to when creating a staging environment that is a subset of a
    production environment
-   How to deal with the Report Builder component of the Jazz Reporting
    Server

## Server rename and the Jazz Authorization Server

[Jazz Security Architecture single
sign-on](https://www.ibm.com/docs/en/elm/7.0.2?topic=management-enabling-jazz-security-architecture-sso-after-upgrade)
(SSO) is an alternate single sign-mechanism that can be used instead of
Kerberos SSO, IBM WAS SSO, or Apache Tomcat server SSO. If you have
adopted the Jazz Security Architecture, then you need take some
additional steps during the server rename process:

-   You must disable the Jazz SSO feature before you import the mappings
    file
-   You must manually update URLs in the Jazz Authorization Server
    database
-   After the server rename verification process completes, you must
    re-enable the Jazz SSO feature and manually update references to the
    Jazz Authorization Server

### Scenario: Setting up a test staging environment with Jazz SSO

One of the supported server rename scenarios is to create a [staging
environment using production
data](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Ft_prepare_sandbox_server_rename.html).
If your production environment has adopted Jazz SSO, then you must do
the following if you plan to import your production data into a staging
environment:

-   Set up a new Jazz Authorization Server for use in your staging
    environment
-   Be sure you have configured your production Jazz Authorization
    Server to use a database server for persistent data, and not the
    local Derby database

You will not be able to share a single Jazz Authorization Server between
your staging and production environments.

The detailed step-by-step instructions for creating a [staging
environment using production
data](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Ft_prepare_sandbox_server_rename.html)
are in the on-line help. The changes to those instructions to account
for the Jazz Authorization server are listed below.

#### Additional steps to take in your production environment

When backing up your production databases (step 2), you will need to
back up the OAUTH database used by the Jazz Authorization Server. Copy
the OAUTH database to your staging database server along with the other
databases as described in [Moving the CLM
database](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fc_server_rename_movedb.html).

You will also need to export the JAS client configuration, using the
following procedure (on Linux):

Log in to the production JAS server cd /opt/IBM/JazzAuthServer/cli
./lsclient -u adminUser:adminPassword \>& prodjas.backup

Copy prodjas.backup to the /opt/IBM/JazzAuthServer/cli directory on your
staging Jazz Authorization Server.

#### Additional steps to take in your staging environment

When restoring the database backups in production (**step 3b**), you
will need to restore the configuration database for JAS. After
restoring, you will need to delete the entries in the "OAUTH20CACHE"
table. This table contains cached user information which is encrypted
using keys on the production JAS. These steps clear the cache and allow
the staging JAS to do its own encryption. On DB2, you would do this as
follows (if the JAS database was called "OAUTH2DB"):

db2 connect to OAUTH2DB db2 delete from OAUTHDBSCHEMA.OAUTH20CACHE

Prior to importing the mapping file in step 3e, you must temporarily
disable Jazz SSO on your staging systems. For jts, ccm, dcc, gc, qm,
relm and rm, edit (or add) the following line in teamserver.properties:

com.ibm.team.repository.servlet.sso_authenticationActivated=false

For rs, edit (or add) the following line in app.properties:

authenticationEnabled=false

In step 4, if you are using the IBM HTTP Server, remember to include the
staging Jazz Authorization Server in your other updates.

After you complete the server rename verification process (step 8), you
must re-enable the Jazz Authorization server and manually change any
host references to the production JAS so that they point to the staging
JAS.

To re-enable the Jazz SSO, first shut down all of your staging systems.
For jts, ccm, dcc, gc, qm, relm and rm, edit (or add) the following line
in teamserver.properties:

com.ibm.team.repository.servlet.sso_authenticationActivated=true

For rs, edit (or add) the following line in app.properties:

authenticationEnabled=true

Next, log into your staging JAS, and edit the client backup file
generated on the production JAS via lsclient. This file is in JSON
format, and will contain an entry for each production application. You
must change the host names in this file to reflect the new host names
which you have assigned to the applications in staging. This is a manual
step - the server rename process in 6.0.x does not automatically rename
these URLs. Be sure to update all of the URLs; there will be multiple
entries in each client section.

Here is an example client entry - this one is for the JTS. The entries
highlighted below are from a test production server, and would need to
be edited to point at the staging JTS. Repeat this for all client
entries.

After you have edited the client file to point to your staging URLs,
load it into the Jazz Authorization server as follows:

Log in to your staging JAS. Make sure JAS is running. cd
/opt/IBM/JazzAuthServer/cli ./ldclient -u adminUser:adminPassword
prodjas.backup

Finally, you must manually update application properties files to point
to your staging JAS. For jts, ccm, dcc, gc, qm, relm and rm, edit (or
add) the following line in teamserver.properties:

com.ibm.team.repository.servlet.sso_as=https\\//StagingJAS\\9643/oidc/endpoint/jazzop

For rs, edit (or add) the following line in app.properties:

jsa.auth.server.url=https\\//StagingJAS.com\\9643/oidc/endpoint/jazzop

(In the above examples, replace "StagingJAS.com" with the host name of
your staging JAS, and change to port to match your staging JAS
configuration).

Now you can start your staging CLM applications.

#### Other considerations

If your production JTS is configured as a license server, you will not
be able to see any information on the license page until you have
completed the server rename verification process and you have re-enabled
the Jazz Authorization Server. You may also see errors relating to the
license service in the jts.log during the server rename verification
process - this can be ignored.

If you are using token license, you can share a Rational Common License
server between your production and staging systems.

### Scenario: Moving a pilot or full production deployment with Jazz SSO

One of the supported server rename scenarios is to [move a pilot or
production
deployment](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Ft_change_server_name.html).
The detailed steps are provided in the on-line help. The changes to
those instructions to account for the Jazz Authorization server are
listed below.

#### Additional steps to take in your source environment

When backing up your source databases (step 2), you will need to back up
the configuration database used by the Jazz Authorization Server. Copy
that database to your target database server along with the other
databases as described in [Moving the CLM
database](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fc_server_rename_movedb.html).

You will also need to export the JAS client configuration, using the
following procedure (on Linux):

Log in to the JAS server cd /opt/IBM/JazzAuthServer/cli ./lsclient -u
adminUser:adminPassword \>& prodjas.backup

If you are moving to a new Jazz Authorization server, copy
prodjas.backup to the /opt/IBM/JazzAuthServer/cli directory on your new
Jazz Authorization Server. If you are going to use the same Jazz
Authorization server, save the prodjas.backup - you'll need it in a
later step.

#### Additional steps to take in your target environment

When restoring the database backups as part of moving your databases,
you will need to restore the configuration database for JAS. After
restoring, you will need to delete the entries in the "OAUTH20CACHE"
table. On DB2, you would do this as follows (if the JAS database was
called "OAUTH2DB"):

db2 connect to OAUTH2DB db2 delete from OAUTHDBSCHEMA.OAUTH20CACHE

This table contains cached user information which is encrypted using
keys on the source JAS. These steps are just clearing the cache and
allowing the target JAS to do its own encryption. This step is not
necessary if you are not moving to a new Jazz Authorization Server, but
it won't do any harm.

Prior to importing the mapping file in step 3a, you must temporarily
disable Jazz SSO on your staging systems. For jts, ccm, dcc, gc, qm,
relm and rm, edit (or add) the following line in teamserver.properties:

com.ibm.team.repository.servlet.sso_authenticationActivated=false

For rs, edit (or add) the following line in app.properties:

authenticationEnabled=false

After you complete the server rename verification process (step 8), you
must re-enable the Jazz Authorization server and manually change any
host references to the source JAS so that they point to the target JAS.
You can skip this step if you did not move to a new JAS.

To re-enable the Jazz SSO, first shut down all of your target systems.
For jts, ccm, dcc, gc, qm, relm and rm, edit (or add) the following line
in teamserver.properties:

com.ibm.team.repository.servlet.sso_authenticationActivated=true

For rs, edit (or add) the following line in app.properties:

authenticationEnabled=true

Next, log into your JAS, and edit the client backup file generated on
the source JAS via lsclient. This file is in JSON format, and will
contain an entry for each Jazz application. You must change the host
names in this file to reflect the new host names which you have assigned
to your target systems. This is a manual step - the server rename
process in 6.0.x does not automatically rename the JAS URLs. Be sure to
update all of the URLs; there will be multiple entries in each client
section.

Here is an example client entry - this one is for the JTS. The entries
highlighted below are from a source JTS, and would need to be edited to
point at the new JTS. Repeat this for all client entries.

After you have edited the client file to point to your new URLs, load it
into the Jazz Authorization server as follows:

Log in to your JAS. Make sure JAS is running. cd
/opt/IBM/JazzAuthServer/cli ./ldclient -u adminUser:adminPassword
prodjas.backup

Finally, if you changed the name of the Jazz Authorization Server as
part of the move, you must manually update application properties files
to point to your new JAS. For jts, ccm, dcc, gc, qm, relm and rm, edit
(or add) the following line in teamserver.properties:

com.ibm.team.repository.servlet.sso_as=https\\//NewJAS\\9643/oidc/endpoint/jazzop

For rs, edit (or add) the following line in app.properties:

jsa.auth.server.url=https\\//NewJAS.com\\9643/oidc/endpoint/jazzop

(In the above examples, replace "NewJAS.com" with the host name of your
new JAS, and change to port to match your JAS configuration).

Now you can start your moved CLM applications.

#### Other considerations

If your production JTS is configured as a license server, you will not
be able to see any information on the license page until you have
completed the server rename verification process and you have re-enabled
the Jazz Authorization Server. You may also see errors relating to the
license service in the jts.log during the server rename verification
process - this can be ignored.

## Additional steps when creating a staging environment that is a subset of a production environment

In the [example topologies for setting up a test staging
environment](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fc_server_rename_ex2_stage.html),
starting point 2 illustrates how you can create a staging environment
that only has a subset of the applications in production. When doing
this, you mask the URLs in staging so that they map to non-existent host
names.

In the case where the CLM applications in production are sharing a JTS,
there is one additional step you need to take before you import the
mapping file on the staging JTS. You need to [unregister any
applications](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fr_repotools_unregisterapp.html)
that are present in production but will not be present in staging. If
you don't do this, the server rename verification process will not
complete because it will be stuck trying to communicate with the missing
applications.

In the [example topology in starting point
2](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fc_server_rename_ex2_stage.html),
let's say you were going to create a staging environment that did not
include the production /rm application (rm1.production.example). In this
case, you would unregister the rm application on your staging JTS prior
to importing mapping file:

./repotools-jts.sh -unregisterApp appName=/rm
teamserver.properties=conf\jts\teamserver.properties

If you have configured one or more Data Collection Components (DCC) to
populate a data warehouse from your applications, you may also want to
remove the missing applications from the list of DCC data sources on
your staging system. The server rename process will map the URLs in the
Resource Group Configuration UI to dummy URLs, but you'll see errors in
on your staging system when you run the data collection jobs. This is
harmless, but you can remove the dummy data sources to eliminate the
errors.

When mapping production URLs to dummy staging URLs, do not use
underscores in the dummy host names. This causes the import of the
mappings file to fail.

Be aware that attempts to use the masked applications will generate
errors. You may see unexpected behavior in several cases:

-   You can see links to artifacts in masked applications, but you'll
    get an error if you click on those links.
-   The Report Builder will list masked applications, and reports
    against the data warehouse may return artifacts from the masked
    application. Note that the URLs for those artifacts will not be
    renamed, so if you click on those links, you will be directed to the
    production system (unless you have updated your client hosts file to
    prevent access to production systems)

## Clarifications when Report Builder is part of a server rename

The Report Builder stores its persistent information on the Report
Builder server, in the conf/rs/db directory. It does not use a
relational database, and so there is no database table on your database
server. Instead, you should copy the contents of the conf/rs/db
directory from your source server to your target server.

The Report Builder stores information about the data sources it reports
against in this local directory. That means if you have moved your data
warehouse from one database to another, as part of your server rename,
you will need to manually update the names of the database servers after
your complete the server rename verification process and your servers
are running again.

To do this, go to your Report Builder -\> Admin page and select "Data
Sources". Open each data source and update the host name for the new
database by editing the "Data source location" field. Test the
connection, and save your changes if the connection test succeeds.

## General documentation updates

In [Scenario: Setting up a test staging
environment](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Ft_prepare_sandbox_server_rename.html)

-   Step 2c left out DOORS Next Generation. Be sure to copy indices in
    \_SourceJazzInstallDir\_/server/conf/rm/indices
-   Step 5 is out of order. This step must happen after the server
    rename verification process is complete. You cannot access jts/admin
    in step 5.

##### Related topics: [related-topics]

-   [Changing the public URL by using server
    rename](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fc_redeploy_server.html)
-   <https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fc_jsasso_jas_deploy_start.html>\[Deploying
    and starting the Jazz Authorization Server\]\]
-   <https://jazz.net/wiki/bin/view/Deployment/PerformanceClusteredJAS>\[Implementing
    a cluster of Jazz Authorization Servers\]\]

META:FILEATTACHMENT{name="Client.png" attachment="Client.png" attr=""
comment="" date="1475098710" path="Client.png" size="56181"
user="vrokosz" version="1"} META:FILEATTACHMENT{name="ResourceGroup.png"
attachment="ResourceGroup.png" attr="" comment="" date="1475106277"
path="ResourceGroup.png" size="38670" user="vrokosz" version="1"}
META:FILEATTACHMENT{name="DataSource.png" attachment="DataSource.png"
attr="" comment="" date="1475107027" path="DataSource.png" size="42112"
user="vrokosz" version="1"}
