META:TOPICINFO{author="sbeard" date="1380282189" format="1.1"
version="1.6"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Data sheet for upgrading to the CLM environment [data-sheet-for-upgrading-to-the-clm-environment]

DKGRAY Authors: Main.CatherineBurrows Build basis: The Rational solution
for Collaborative Lifecycle Management (CLM) ENDCOLOR

TOC{title="Page contents"}

The following tables contain data items that you will need to have
available during the upgrade process. Let us know if there are any
additions or changes that you would like to see on the data sheet.

## 2.x to 3.0.1 context root mappings

You will need to know the actual URL including context root when you
upgrade from 2.x to 3.x. Do NOT change your context root when upgrading
to 3.x. For more information, consult the documentation at:
<http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.install.doc/topics/c_understand_upgrade.html>
CLM application

2.x default context root

Your actual 2.x context root, if different than the default

Rational Team Concert /CCM

[https://rtc.hostname.example.com:port/jazz](https://rtc.hostname.example.com:port/jazz)

Rational Quality Manager/QM

[https://rqm.hostname.example.com:port/jazz](https://rqm.hostname.example.com:port/jazz)

Rational Requirements Composer/RM

[https://rrc.hostname.example.com:port/rdm](https://rrc.hostname.example.com:port/rdm)

Jazz Team Server/JTS

A separate web application at
[https://rrc.hostname.example.com:port/jazz](https://rrc.hostname.example.com:port/jazz)
for Rational Requirements Composer. Included with the other products.

Note: When you upgrade from 3.0.1 to 4.0, the context roots stay the
same for all applications.

## 3.0 to 3.0.1 Rational Team Concert context root mapping

CLM application

3.0 default context root

Your actual 3.0 context root, if different than the default Jazz Team
Server
[https://jts.hostname.example.com:port/jts](https://jts.hostname.example.com:port/jts)

## Topology touch points

When performing an upgrade, you will need to have information and access
available as it relates to your database, application server, proxy
server, CLM applications, user management system, and license management
system. The following table depicts what information and/or access you
will need to these tools in order to perfom the upgrade. Database

Data items needed

Description

Data

Comments

DB2

Names of databases

Path

URL including port number

Found in the teamserver.properties file typically as:
com.ibm.team.repository.db.vendor,
com.ibm.team.repository.db.jdbc.location and
com.ibm.team.repository.db.jdbc.password

Admin user account privilege and password for all databases

On UNIX systems, get the password for the DB2 instance owner, which is
typically the db2inst1 user.

Location of where you can create a backup database

If you are using the data warehouse, you will need the path name for
database table space folder.

If you are using the data warehouse, type the login information for a
functional user that will run the data collection jobs.

This user ID must exist in your user registry. Note: The user ID that
you enter for the functional user must be a different ID than the
administrative user that you are currently using to configure the
application.

Oracle

Names of databases

Path

URL including port number

Admin authority for user account privilege and password for all
databases

Must have database administration authority over the database and that
the database, table space storage, and appropriate storage configuration
is created by a user with system administration authority.

You must create a separate table space and database user who is
associated with that table space for each application.

\* CCM DB user ID \* RQM DB user ID \* RRC DB user ID

If you are using the data warehouse, you will need the path name for
database table space folder.

If you are using the data warehouse, type the login information for a
functional user that will run the data collection jobs.

This user ID must exist in your user registry. Note: The user ID that
you enter for the functional user must be a different ID than the
administrative user that you are currently using to configure the
application. Microsoft SQL Server User ID and password for creating
databases

The user who creates the database table must be a member in the sysadmin
fixed server role, or an owner of the database (dbo).

Names of databases

Paths

URLs including port number

Admin authority for user account privilege and password for all
databases

You must create a separate table space and database user who is
associated with that table space for each application.

\* CCM DB user ID \* RQM DB user ID \* RRC DB user ID

If you are using the data warehouse, you will need the path name for
database table space folder. If you are using the data warehouse, type
the login information for a functional user that will run the data
collection jobs. This user ID must exist in your user registry. Note:
The user ID that you enter for the functional user must be a different
ID than the administrative user that you are currently using to
configure the application.

Application server

WebSphere Application Server

URL, admin user account privilege, and password.

Path name to location of WAR files Found in
WebSphereInstall/AppServer/profiles/profile/bin

User name and password with admin authority in the Integrated Solutions
Console

Name of application server that contain the WAR files before the upgrade

Name of application server to contain the WAR files after the upgrade is
deployed

Security roles mapped to jts_war

Security roles mapped to ccm_war

Security roles mapped to qm_war JAZZ_HOME To locate the information,
complete these steps in the Integrated Solutions Console: 1. Servers \>
Server Types \> WebSphere application servers. 2. Click the server name
to open it. The default server name is *server1*. 3. In the Server
Infrastructure section, click Java and Process Management \> Process
definition. 4. Under Additional Properties, click Java Virtual Machine.
5. Under Additional Properties, click Custom properties. Tomcat Public
URI As defined in the teamserver.properties file for
com.ibm.team.repository.server.webapp.url Database vendor As defined in
the teamserver.properties file for com.ibm.team.repository.db.vendor
Database location As defined in the teamserver.properties file for
com.ibm.team.repository.db.jdbc.location Application home Full path to
the Rational Team Concert version 2 or CCM application version 3 server
configuration directory. The path **must** not contain any spaces. The
default is /server/conf

Port numbers for Jazz Team Server and CLM applications May be found in
the server.xml file located at the path
*InstallDirectory/server/tomcat/conf*

Administrative ID and password This ID and password must work in the
previous version from which you are upgrading and reside in the
tomcat-users.xml file.

User ID, name, password, and e-mail address of the user who will have
administrative access to the Jazz Team Server after the upgrade This
user must reside in the registry. Reverse proxy server Rational solution
for CLM URL, port number, context roots for all CLM applications

See the following for more information: [Understanding reverse
proxy](UnderstandingReverseProxy), [Configuring Enterprise CLM Reverse
Proxies: WebSphere 8 and IHS 8](ConfigureCLMEnterpriseReverseProxy),
[Configuring Enterprise CLM Reverse Proxies: Apache and
mod_proxy](ConfigureCLMEnterpriseReverseProxyWithApache), [Configuring
Enterprise CLM Reverse Proxies: WebSphere 8.5 ND
Proxy](ConfiguringEnterpriseCLMReverseProxiesWebSphere85NDProxy) CCM
Inbound client request URL to proxy server for CCM

Forwarded client request URL from proxy server for CCM RM Inbound client
request URL to proxy server for RM

Forwarded client request URL from proxy server for RM QM Inbound client
request URL to proxy server for QM

Forwarded client request URL from proxy server for QM JTS Inbound client
request URL to proxy server for Jazz Team Server

Forwarded client request URL from proxy server for Jazz Team Server

CLM applications

Jazz Team Server

Path for the installation directory of the Jazz Team Server package

Path for the new installation directory of the Jazz Team Server package

URLs for the server and each application, including port numbers and
context root

Value found in teamserver.properties file for
"com.ibm.team.repository.server.webapp.url". If this value is not set,
it must be set using the administrative web interface.

ID and password with admin privileges (JazzAdmin)

Provide the user ID, name, password, and e-mail address of the user who
will have administrative access to Jazz Team Server

Name

Email

Configuration file locations: \* teamserver.properties \* services.xml
\* log4j.properties \* provision_profiles

Found in the path: *Install Directory/conf/application* CM URL including
port numbers and context root

ID and password with admin privileges RM URL including port numbers and
context root

ID and password with admin privileges QM URL including port numbers and
context root

ID and password with admin privileges RRDI URL including port numbers
and context root

ID and password with admin privileges

User management LDAP (General) LDAP registry location See:
<http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.install.doc/topics/c_plan_identity_management.html>
for more information on LDAP parameters.

LDAP user name

LDAP password

Base user DN

User property names mapping

Base group DN

Group name property

Group member property Jazz to LDAP group mapping

-    **JazzAdmins** =\[LDAP group for Jazz admins\]
-    **JazzUsers** =\[LDAP group for Jazz users\]
-    **JazzDWAdmins** =\[LDAP group for Jazz Data Warehouse admin\]
-    **JazzGuests** =\[LDAP group for Jazz guest\] (Not used by Rational
    Quality Manager)
-    **JazzProjectAdmins** =\[LDAP group for Jazz project admins\]

See
<http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.install.doc/topics/c_plan_identity_management.html>
for more information. LDAP local group realm for Tomcat Path name and
location of LDAP local file Connection URL Obtain these three values
from your LDAP administrator. These values are from your LDAP directory.
See
<http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.install.doc/topics/t_config_ldaplicalgroup.html>
for more information.

User base

User search

License management

Floating license Administrative user with a license If your Jazz Team
Server application acted as a floating license server for multiple
version 2 servers, you must reinstall your license keys. Jazz Team
Server that is the floating license server and has the client access
license (CAL) keys installed. You will need the URL containing the fully
qualified DNS host name and port number. For example:
<http://floating-license-server:9443/jts> where
"floating-license-server" contains the DNS domain of the machine. For
more information:
<http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.repository.web.admin.doc/topics/tmanagefloatinglic.html>

Jazz Team Server that assigns the floating client access license (CAL)
This server points to the floating server. Client access license keys
URL with a fully qualified DNS host name including port number. The
fully qualified host name includes the DNS domain reference of the
machine on which Jazz Team Server is installed. Example:
<https://%5Bfully> qualified hostname\]:9443/jts/admin For more
information:
<http://pic.dhe.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.repository.web.admin.doc/topics/tmanagelicensekey.html>

License activation key location

The number of purchased licenses

Email settings

SMTP server

SMTP port

SMTP user name and password

Name and email address for the **From** field on email

-   [Data sheet in printable PDF
    format](ATTACHURL/Upgrade_Datasheet.pdf)

##### Related topics: None [related-topics-none]

##### External links: \* None [external-links-none]

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="Upgrade_Datasheet.pdf"
attachment="Upgrade_Datasheet.pdf" attr="h" comment="" date="1367510328"
path="Upgrade_Datasheet.pdf" size="107201" user="sbeard" version="1"}
