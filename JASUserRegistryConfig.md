META:TOPICINFO{author="michaelrowe" date="1700243061" format="1.1"
version="1.23"} META:TOPICPARENT{name="JazzAuthorizationServer"}

# Configure JAS with a User Registry - LDAP or File Based DKGRAY Authors: Main.ShubjitNaik Build basis: JAS and ELM version 6.0.x, 7.x [configure-jas-with-a-user-registry---ldap-or-file-based-dkgray-authors-main.shubjitnaik-build-basis-jas-and-elm-version-6.0.x-7.x]

ENDCOLOR

TOC{title="Page contents"}

Jazz Authorization Server is based on the IBM WebSphere Liberty server.
Because Jazz Authorization Server authenticates users, it must be
configured with a user registry. WebSphere Liberty server has
capabilities similar to the full WebSphere Application Server; it can be
configured to use a Lightweight Directory Access Protocol (LDAP)
registry, or users can be defined in local files.

This article will focus on steps to help configure JAS with a File based
User Registry and LDAP User registry.

## Installation

**ELM** BR

-   To deploy JAS to an existing environment and migrate to JAS, visit
    this
    [Section](https://www.ibm.com/docs/en/elm/7.0.2?topic=management-enabling-jazz-security-architecture-sso-after-upgrade)
    on our Infocenter
-   For a new deployment of ELM, Install the applications via IBM
    Installation Manager and Select the option "Enable Jazz Security
    Architecture SSO" during the installationBRBR BR

**JAS** BR

-   Download Jazz Authorization Server install bit from
    [jazz.net](https://jazz.net/downloads/elm/releases/7.0.2?p=allDownloads),
    under All Downloads Section for the specific versionBRBR BRBR
-   Install Jazz Authorization Server application via Installation
    Manager, instructions available on our
    [Infocenter](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.2/com.ibm.jazz.install.doc/topics/t_s_server_installation_im.html)BRBR
    BR

## Setup and Configure JAS with a User Registry

### Configuration files

-   Copy the files from
    `JazzAuthServer_install_dir/wlp/usr/servers/jazzop/defaults` folder
    one level up to `JazzAuthServer_install_dir/wlp/usr/servers/jazzop/`
-   Files we would modify are `server.xml`, `appConfig.xml`,
    `ldapUserRegistry.xml` and `localUserRegistry.xml`
-   `appConfig.xml` - Contains Jazz Group/Role mappings and UserRegistry
    file information
-   `ldapUserRegistry.xml` - Configuring Liberty with an LDAP user
    registry
-   `localUserRegistry.xml` - Configuring Liberty file based registry

### To Configure JAS with Liberty file based registry

\* By default the bundled Liberty profile is configure with File based
user registry. \* Open the file
`JazzAuthServer_install_dir/wlp/usr/servers/jazzop/localUserRegistry.xml`
\* Add new Users or Groups and save the file

clmadmin

-   You can either enter *Plain Text Passwords* or encrypt the passwords
    using the
    [securityUtility](https://jazz.net/wiki/bin/view/Deployment/JASUserRegistryConfig#Encrypt_Passwords)

### To Configure JAS with LDAP registry

\* By default the bundled Liberty profile is configured with file based
user registry \* To change the configuration to LDAP registry, edit
`JazzAuthServer_install_dir/wlp/usr/servers/jazzop/appConfig.xml` file
\* Towards the end of the file change from \*

**TO** \* BR

-   To Configure the LDAP User Registry, guidance from LDAP
    administrators / Network admins may be necessary to complete the
    configuration Typical information needed from your LDAP Admin
    -   LDAP Server Name and Port (*LDAP Server hostname and Port*)
    -   The Base DN (LDAP Root Tree where Users/Groups can be queried
        from\_)
    -   bindDN and bindPassword (*User ID and password for the user who
        can query the LDAP directory*)
    -   Group and User filter (*inetOrgPerson, groupOfNames etc*)
    -   User ID and Group ID mappings (*sAMAccountName, cn etc*)

<!-- -->

-   Example configuration for different LDAPs information is available
    in our
    [Infocenter](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.3/com.ibm.jazz.install.doc/topics/t_config_ldap_connection_liberty.html)
-   We have included a few examples from different LDAP environments (MS
    Active Directory, Tivoli and ApacheDS) to help guide the
    configuration.
-   Edit
    `JazzAuthServer_install_dir/wlp/usr/servers/jazzop/ldapUserRegistry.xml`
    and modify the ldapRegistry configuration for your LDAP registry

#### Microsoft Active Directory

\*

#### IBM Tivoli Directory Server

\*

#### Apache DS

\*

#### Map Administrators for Jazz Authorization Server

Map Groups or Users as JAS Administrators who can perform JAS CLI
operations, register Applications to JAS and access WebSphere Liberty
AdminConsole JAS

#### Encrypt Passwords

-   To encrypt passwords, run the script
    `JazzAuthServer_install_dir/wlp/bin/securityUtility`
-   After the script completes, copy the output to the password
    attribute associated with the user ID (or bindPassword)
-   To run the securityUtility script, use the following syntax:
-   \$ securityUtility encode userPassword where *userPassword* is the
    password to encode

## Configure Database for JAS

When you first install JAS, it comes configured to use a local Derby
database for storing information. It is not recommended to use Derby
database for a production environment and note that Derby database won't
work in a clustered JAS environment, since that information won't be
available to all the instances.

The basic steps to configure the database are:

-   Create database tables on a database server which all JAS instances
    can access
-   Update the JAS configuration file (appConfig.xml) to use the
    database server

The following links provide information for both Oracle and DB2, and
sample SQL scripts are available that can create the necessary tables.
But note that you will need to customize these scripts for your own
environment.

-   [Configure IBM DB2
    Database](https://jazz.net/wiki/bin/view/Deployment/PerformanceClusteredJAS#DB2)
-   [Configure Oracle
    Database](https://jazz.net/wiki/bin/view/Deployment/PerformanceClusteredJAS#Oracle)
-   [Configure Microsoft SQL Server
    Database](https://jazz.net/wiki/bin/view/Deployment/PerformanceClusteredJAS#Microsoft_SQL_Server)

The JAS database is used to store client registration information (i.e.
all the applications that are configured to use the JAS for
authentication) and information about authentication tokens that have
been issued to clients. The client registration information is small and
static, so it takes very little space in the database, but the token
information is dynamic, and the space that it uses is proportional to
the number of times a client will authenticate with a CLM application.
Also, tokens have expiration periods; token information is retained
until it expires. Therefore, an environment in which there are many
authentications taking place and in which token expiration times are
fairly long will require more storage space in the database.

Also, the JAS will load all unexpired tokens for a particular user into
memory. If there are many tokens outstanding for a single user, more
Java heap memory may be required than in the default configuration. In
particular, since RTC build engines are usually configured to
authenticate as a single designated "build" user, lots of build activity
may result in the need to increase the Java heap size for the JAS.

Database storage size can be reduced by shortening the token expiration
periods. There are two of them, one for access tokens and one for
refresh tokens. The default access token expiration time is 6 hours, so
it generally won't cause a problem. But the default refresh token time
is 7 days, which can cause them to accumulate quite a bit. To reduce
that expiration time, adjust the value for the
"authorizationGrantLifetime" attribute of the element in the
`JazzAuthServer_install_dir/wlp/usr/servers/jazzop/appConfig.xml` file.
The default configuration is

client01

The value "604801" is 7 days plus 1 second, in seconds. It can be
reduced to make refresh tokens expire quicker and therefore not
accumulate as much in the database.

For more information, see [work item
471597](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/471597)

## JVM

The default JVM heap allocated to a WebSphere Liberty server is 60MB.
This applies to JAS as well and to increase the Java heap size, you can
create jvm.options file under
`JazzAuthServer_install_dir/wlp/usr/servers/jazzop/jvm.options` and
include the JVM memory parameters, one per line. For example, these
entries will increase the heap size to 2GB:

-Xms2G -Xmx2G

For more information see [Manually Customizing Liberty
Environment](https://www.ibm.com/docs/en/was-liberty/core?topic=manually-customizing-liberty-environment)

## Test JAS Configuration

-   Now that JAS is configured with a User registry, it is time to start
    the server and test the configuration
-   Start the server (Linux example) \$ cd JazzAuthServer_install_dir \$
    ./start-jazz
-   Access the following URLs to test JAS
    -   JAS Configuration URL BR
        [https://fully_qualified_domain_name_of_JAS_server:defined_port/oidc/endpoint/jazzop/.well-known/openid-configuration](https://fully_qualified_domain_name_of_JAS_server:defined_port/oidc/endpoint/jazzop/.well-known/openid-configuration)
        BR and
        [https://fully_qualified_domain_name_of_JAS_server:defined_port/oidc/endpoint/jazzop/registration](https://fully_qualified_domain_name_of_JAS_server:defined_port/oidc/endpoint/jazzop/registration)
        *default value for the registration URL is* `{"data":[]}`

## Jazz Team Server (JTS) Setup with JAS

-   For a new deployment, CLM installation should be enabled for Jazz
    Security Architecture SSO
-   Accessing the JTS setup page,
    [https://jtsserver:port/jts/setup](https://jtsserver:port/jts/setup)
    , would not prompt for a Username / Password
-   Express setup would be disabled for a CLM instance enabled for Jazz
    Security Architecture SSO BR BR

\* Run through the setup following the prompt until you reach "Register
Applications" Page \* Enter the Jazz Authentication Server details.
**The URL you enter should be accessible by all and is as important as
the Jazz Public URI** BR BR

### File based registry

-   In the Next step (Step 6), "Select a type of User Registry, select
    **Non-LDAP External Registry** BR BR

<!-- -->

-   Create a user with userID details from users configured in
    localUserRegistry.xml
-   Click on **Save and Log in** and Login as a User with JazzAdmin role
-   Assign a License to the User
-   Go back to Register Applications page (Step 5) and register all the
    applications
-   Complete the setup

### LDAP Registry

**User to Role Mappings**

-   Groups to Jazz Roles mappings are picked from JTS configuration when
    JAS is configured with LDAP or SCIM. More details on the next
    section.

Ensure pop-up blocker is disabled on the browser, or Pop-ups are allowed
for ELM and JAS URLs. Here are instructions to configure JTS with LDAP
User Registery

-   In the Next step (Step 6), "Select a type of User Registry, select
    **LDAP** BR BR
-   Enter the LDAP Details, there are 3 sections as mentioned below BR
    1 - LDAP Server and Bind User details BR BRBR 2 - Base USer DN and
    USer Properties mapping BR BRBR 3 - Group DN, Role and Property
    mapping BR BRBR
-   Assign a license and click Next
-   A Login window would be displayed, Login as a user with JazzAdmin
    role assigned
-   Go back to Register Applications page (Step 5) and register all the
    applications
-   Complete the setup

### ELM User group-to-role mapping

User Groups to Jazz Roles mappings (JazzAdmins, JazzUsers etc) are
picked from JTS configuration when JAS is configured with LDAP. When
Users accesses an ELM application URL, they are redirected to JAS for
Authentication. Post successful authentication JTS performs the
ldapsearch Query to fetch groups with LDAP details mentioned under JTS
\> Advanced Properties \>
**com.ibm.team.repository.service.jts.internal.userregistry.ldap.LDAPUserRegistryProvider**
for User group to Jazz role mappings.

`Note: We can only map direct LDAP groups in JTS. Special Subjects like ALL_AUTHENTICATED_USERS or NESTED_GROUPS would not work with JAS based deployments`

Here is an extract from JTS logs with debug enabled, where it is mapping
to the Jazz Groups configured in JTS.

DEBUG m.repository.servlet.internal.oidc.OidcAuthHandler \[TID:
37404299\] - Using group-to-role mapping
"{cn=MYJazzAdmins,CN=Groups,DC=clm,DC=com:\[JazzAdmins\],cn=MYJazzGuests,CN=Groups,DC=clm,DC=com:\[JazzGuests\],cn=MYJazzProjectAdmins,CN=Groups,DC=clm,DC=com:\[JazzProjectAdmins\],cn=MYJazzUsers,CN=Groups,DC=clm,DC=com=com:\[JazzUsers\]}"
for 300000 ms

/jts/service/com.ibm.team.repository.service.internal.IExternalUserRegistryRestService/externalUserRegistryConfiguration\]
DEBUG ce.jts.internal.userregistry.ldap.LDAPUserRegistry \[TID:
7FEA9AFC\] - Query to fetch group full names - ldapsearch -h
<ldap://ldapserver:389> -b "CN=Groups,DC=clm,DC=com" "(\|
(cn=MYJazzAdmins)(cn=MYJazzGuests)(cn=MYJazzProjectAdmins)(cn=MYJazzUsers))"

For new installations, during JTS/Setup select the User registry type as
LDAP and configure to the same LDAP registry that is configured with JAS
and enter the group mappings under the property *Jazz to LDAP Group
Mapping*

## Enable an Existing CLM setup for Jazz Security Architecture

-   Complete the Jazz Authorization Server Setup, Configuration and
    testing as per instructions within this article
-   Enable CLM applications for Jazz Security Architecture single
    sign-on following the instructions on our
    [InfoCenter](https://www.ibm.com/docs/en/elm/7.0.2?topic=management-enabling-jazz-security-architecture-sso-after-upgrade)

BR

##### Related topics: [Jazz Authorization Server](JazzAuthorizationServer), [Deployment web home](DeploymentWebHome) [related-topics-jazz-authorization-server-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

META:FILEATTACHMENT{name="JTS_Setup.png" attachment="JTS_Setup.png"
attr="h" comment="" date="1487341477" path="JTS_Setup.png" size="122103"
user="shubjit" version="1"} META:FILEATTACHMENT{name="JAS_Server.png"
attachment="JAS_Server.png" attr="h" comment="" date="1487341509"
path="JAS_Server.png" size="215084" user="shubjit" version="1"}
META:FILEATTACHMENT{name="Basic_Config.png"
attachment="Basic_Config.png" attr="h" comment="" date="1487341703"
path="Basic_Config.png" size="112657" user="shubjit" version="1"}
META:FILEATTACHMENT{name="LDAP_Config.png" attachment="LDAP_Config.png"
attr="h" comment="" date="1487430576" path="LDAP_Config.png"
size="161254" user="shubjit" version="1"}
META:FILEATTACHMENT{name="LDAP_Registry.png"
attachment="LDAP_Registry.png" attr="h" comment="" date="1487760441"
path="LDAP_Registry.png" size="180254" user="shubjit" version="1"}
META:FILEATTACHMENT{name="LDAP_User.png" attachment="LDAP_User.png"
attr="h" comment="" date="1487760463" path="LDAP_User.png" size="121541"
user="shubjit" version="1"} META:FILEATTACHMENT{name="LDAP_Group.png"
attachment="LDAP_Group.png" attr="h" comment="" date="1487760483"
path="LDAP_Group.png" size="304609" user="shubjit" version="1"}
