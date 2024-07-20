META:TOPICINFO{author="lfrankel" date="1410980505" format="1.1"
version="1.7"} META:TOPICPARENT{name="ServerRename"}

# Impact of server rename on the Rational solution for Collaborative Lifecycle Management DKGRAY Authors: Main.LisaFrankel [impact-of-server-rename-on-the-rational-solution-for-collaborative-lifecycle-management-dkgray-authors-main.lisafrankel]

Build basis: CLM products, version 4.0.1 and later ENDCOLOR

TOC{title="Page contents"}

This page describes restrictions and limitations to evaluate before
proceeding with the steps of renaming a server.

## Impact of server rename on the Jazz Team Server

Review the Jazz Team Server-specific restrictions in this section
associated with server rename.

### Updating the teamserver.properties file

After performing a server rename operation, you might need to change the
`com.ibm.team.repository.web.helpuri` property in the
`teamserver.properties` file.

This property points to the help (`clmhelp/index.jsp`). If you are using
a single server for the Jazz Team Server and applications, the help URI
is a relative path and you do not need to update it unless the context
root has changed. If you have a distributed deployment, you might need
to adjust the help URI after the server rename operation is complete. Go
to the `teamserver.properties` file for each application and update the
value of this property. For details, see "Configuring the location of
the help in a distributed environment" in the Jazz Team Server
Installing book in the [IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html)
.

### Application names remain the same after a server rename operation

The server rename operation does not rename the content of the
application name. If an application name contains a URL or context root
which has been renamed, you must manually edit the **Application name
property** in the Registered Applications page. For details about
editing the Registered Applications page, see "Managing registered
applications" in the Jazz Team Server Administering book in the [IBM
Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

## Impact of server rename on the Change and Configuration Management (CCM) application

Review the following CCM-specific restrictions associated with server
rename.

### Restart all clients

After the server administrator renames a server, you must restart any
client that connects to that server. If you leave a client open during
the server rename operation, it is possible that artifacts that include
the previous server URL could be stored in the repository.

### Use 4.0.1 or higher clients and build engines for production scenarios

For the pilot-to-production scenario and the production-to-production
scenario, all user clients and build engines must be at version 4.0 or
higher prior to the rename operation

### Use staging workspace for test staging environment using production data scenario

For the preparing a test staging environment using production data
scenario, always use a staging workspace for connecting to the staging
server. Do not re-use an existing production workspace to connect to the
staging server.

### Check in changes into repository workspace before renaming server

If you use Rational Team Concert source control, check in all of your
changes into your repository workspace before you rename the server.
This ensures that your changes are safely stored in the repository and
no changes are lost during the rename operation.

### Deactivate non-Jazz Build Engine (JBE) build engines

Before performing a server rename operation, deactivate any build
engines of type Build Forge, Build Agent, and Hudson/Jenkins to prevent
builds from running on these external systems until you verify the
engine connection details. After the rename operation, verify the
connection details for these build engines. Verification is needed
especially in the preparing a test staging environment using production
data scenario to prevent builds in the staging environment from running
on production build servers. Verification might be needed for other
scenarios, depending on whether the target build servers are moving with
the renamed CCM server. If the connection details are correct after the
rename operation, you can reactivate the engines if appropriate for your
scenario. Other options are to leave these build engines deactivated;
change their connection details to something invalid (if this was not
done in the mapping); or delete them.

Because the JBE process is run with a given RTC server URL, it does not
have the same issue as non-JBE build engines. Production JBE instances
will continue to run against the production CCM server. However,
cross-contamination from the staging environment to the production
environment might be possible if JBE instances are run against the
staging environment, and build scripts or build properties refer to
production servers. Review for such cases before you perform the server
rename operation.

### Update server URLs in work item templates

The server rename operation does not update the server URL in work item
templates. For any work item templates that include the server URL in a
field, you must change the URL to the one used by the renamed server.

### Specify full URI of renamed server in full-text searches

To search for work items that contain the URI of the renamed server, you
must specify the full URI; searching for URI fragments is not supported.

### Query limitations

In a work item query, you cannot search for a renamed server URI in a
small or medium string/html attribute.

### Plan limitations

URLs within the **Notes** (wiki) tab of a plan do not get renamed as a
result of the server rename operation.

## Impact of server rename on the Quality Management (QM) application

The Quality Management application has specific restrictions that are
related a server rename.

### Command-line and Selenium adapters

After a server rename, update the Quality Management public URL in the
adapter configuration file for the RQM Command-Line or Selenium adapter.
Depending on the adapter version, the configuration file will be named
either `Config.ini` or `Config2.ini`.

1.  Stop the adapter process.
2.  Open the `Config.ini` or `Config2.ini` file in a text editor.
3.  Find the property named `rqm.repository` and modify the URL, port,
    and context to match the information for the renamed server.
4.  Save the `Config.ini` or `Config2.ini` file and restart the adapter.

For more information, see "Setting up and starting the command line
adapter" in the Rational Quality Manager Testing book in the [IBM
Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

### Shared Resource Locations for automated test tools

After a server rename, update the shared resource locations used for
automated test scripts at **Manage Project Properties \> Shared Resource
Locations**. For more information, see "Making shared test resources
available" in the Rational Quality Manager Administering book in the
[IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

### Embedded links in text fields

After a server rename, embedded links in plain and rich text fields may
require adjustment.

For example, test plans might feature descriptions that contain links in
free-form text to another server. If a server is renamed, those links
must be updated manually.

### Broken links in documents pre-dating server rename

Links in emails, bookmark collections, external web pages,
presentations, and documents that refer to a server will be broken when
that server is renamed. Update these resources as is necessary.

### Insight XML data configuration files

Insight customers use XML data configuration (`.xdc`) files provided
with CLM as part of a Cognos Data Manager ETL solution. These files
contain server names. After a server rename, these files must be
downloaded again and reinstalled as documented in "Importing the XML
data configuration file for live reporting" in the Rational Reporting
Installing book in the [IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

### Test tool adapter considerations

Reconfigure the RQM test tool adapters to use the new public URI for the
Jazz Team Server. For details about the adapters, see "Rational test
tools integration overview" in the Rational Quality Manager Integrating
book in the [IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
For specific details about configuring the adapter, see the
documentation for the product providing the Rational and/or third-party
test execution adapter.

For the AppScan test adapter, you will need to run the AppScan Adapter
Setup and point to the new URL if the server name has changed. For
details, see "Integrating with AppScan Enterprise" in the Rational
Quality Manager Integrating book in the [IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

For defect submission from AppScan to Change and Configuration
Management, log into AppScan Enterprise and update the Defect Tracking
Configuration to point at the new URL.

### Changes to advanced properties

For server rename, you can make changes to several of the advanced
properties in the Quality Management (QM) application. For instructions
to configure advanced properties, see Configuring advanced properties in
the Jazz Team Server Administering book in the [IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

#### Remap embedded anchored links that are non-navigable

By default, embedded anchored links that are navigable in the rich text
editor are remapped. However, embedded anchored links with XHTML-type or
HTML 4 URI-type attributes are remapped only by configuring the
`MappingContentService` property. This property is disabled by default
for performance reasons. To find the property, on the Application
Administration page, in the Advanced Property section, click **RQM
Process Component \>
com.ibm.rqm.common.service.internal.mapping.MappingContentService \>
Rewrite hidden links in XHTML**.

Table 1 lists the embedded anchored links that can be remapped by using
the `MappingContentService` property.

*Table 1.* *Link types*

\> \> \>

\> \> \>

\> \> \>

\> \> \>

\> \> \>

\> \> \>

\> \> \>

\> \>
