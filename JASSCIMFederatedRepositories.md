META:TOPICINFO{author="shubjit" date="1680768245" format="1.1"
version="1.15"} META:TOPICPARENT{name="JazzAuthorizationServer"}

# Multiple User Registries with Jazz Authorization Server and SCIM DKGRAY Author: Main.ShubjitNaik Build basis: JAS and CLM Version 6.0.6.1 and higher [multiple-user-registries-with-jazz-authorization-server-and-scim-dkgray-author-main.shubjitnaik-build-basis-jas-and-clm-version-6.0.6.1-and-higher]

ENDCOLOR

TOC{title="Page contents"}

WebSphere Application Server Liberty Profile allows configuring Multiple
federated registries. User registry federation is used when user and
group information is spread across multiple registries. For example, the
information might be in two different LDAPs, in two subtrees of the same
LDAP, in a file, or the users are of a system. The information might
even be in a custom user data repository. With registries federated, you
can search and use these distributed user information in a unified
manner with continuous store of information. Using federated registry,
you can use the unified view for authentication and authorization of
users in Liberty. BR BR

Jazz Authorization Server (JAS) is based on WebSphere Liberty Profile
and can leverage the feature of configuring federated Registries.
However, for it work with CLM, you would have to configure JAS with
SCIM.

This article focuses on steps to configuring JAS for SCIM and with
federated registries.

## Important Notes and Pre-requisites

-   To configure Multiple Users Registries with JAS, enabling SCIM
    configuration is Mandatory
-   It is recommended to upgrade to CLM and JAS Version 6.0.6.1 (latest
    iFix) or higher to configure SCIM with JAS
-   To configure SCIM you must use Lightweight Directory Access Protocol
    (LDAP) for User registries
-   The screenshots on the SCIM configurations in CLM / ELM are from
    version 6.0.6.1

## Setup and Configure JAS for SCIM with a Single LDAP Registry

-   To configure SCIM you must use Lightweight Directory Access Protocol
    (LDAP)
-   The first step is to configure JAS for SCIM with a Single LDAP
    Registry and complete JTS setup with JAS and SCIM
-   Refer article **[Configuring Jazz Authorization Server for
    SCIM](JASAndSCIM)** for the complete steps

## Configure JAS for SCIM with Multiple LDAP Registries

### Enable federated registries features in Liberty

\* Enable the Jazz Authorization Server to support Federated Registries
\* Edit `JazzAuthServer_install_dir/wlp/usr/servers/jazzop/server.xml`
and include the following in the list of features \* scim-1.0
appSecurity-2.0 servlet-3.0 ldapRegistry-3.0

### Modify LDAP configuration to include multiple registries

-   We have included a few examples from different federated LDAP
    environments (MS Active Directory and ApacheDS) to help guide the
    configuration
-   Edit
    `JazzAuthServer_install_dir/wlp/usr/servers/jazzop/ldapUserRegistry.xml`
    and modify to match your environment, examples below

#### Microsoft Active Directory

\*

adadmin ad2admin

-   Users or Groups listed under == tag are SCIM Administrators
-   The configuration under `< attributeConfiguration >` is mandatory
    for each LDAP server configuration as the `displayName` SCIM
    property is mapped to Name attribute in CLM / ELM. You can change
    the LDAP attribute mapping from `cn` to as per your organization's
    requirement.

#### ApacheDS

\*

clmadmin1 clmadmin2

-   The above example is from an ApacheDS server setup with Anonymous
    Authentication. Include the BindDN if necessary
-   Users or Groups listed under == tag are SCIM Administrators
-   The configuration under `< attributeConfiguration >` is mandatory
    for each LDAP server configuration as the `displayName` SCIM
    property is mapped to Name attribute in CLM / ELM. You can change
    the LDAP attribute mapping from `cn` to as per your organization's
    requirement.

### Update Administrators for Jazz Authorization Server

Map Groups or Users as JAS Administrators who can perform JAS CLI
operations, register Applications to JAS and access WebSphere Liberty
AdminConsole

\* To Map Groups and Users who would Administrate JAS \*

### Test SCIM with multiple registries

-   Now that JAS is configured with Federated Registries and SCIM, it is
    time to test if users from multiple registries are listed
-   Start the server (Linux example) \$ cd JazzAuthServer_install_dir \$
    ./start-jazz
-   Access the SCIM API for Users with this URL and confirm Users from
    multiple registries are listed BR
    [https://fully_qualified_domain_name_of_JAS_server:defined_port/ibm/api/scim/Users](https://fully_qualified_domain_name_of_JAS_server:defined_port/ibm/api/scim/Users)
-   Access the SCIM API for Groups with this URL and confirm Groups from
    multiple registries are listed BR
    [https://fully_qualified_domain_name_of_JAS_server:defined_port/ibm/api/scim/Groups](https://fully_qualified_domain_name_of_JAS_server:defined_port/ibm/api/scim/Groups)

BR

## JTS SCIM configuration to map to Multiple LDAP Registries

-   It is assumed that JTS Setup was completed earlier and was
    configured with JAS for SCIM with instructions from [Configuring
    Jazz Authorization Server for SCIM](JASAndSCIM)
-   Login to JTS admin page as a JazzAdmin User from the First LDAP
    registry
-   Click on **Server \> Advanced Properties** and search for SCIM
    Configuration
    **com.ibm.team.repository.service.jts.internal.userregistry.scim.SCIMUserRegistryProvider**
-   Edit **Jazz Groups to Registry Group Mapping** to include groups
    from Additional LDAPs BR One Jazz group can be mapped to multiple
    groups. The user registry groups must be separated by a semi colon.
    For example, JazzAdmins=LDAPAdmins1;LDAPAdmins2 maps JazzAdmins
    group to LDAPAdmins1 and LDAPAdmins2 BR BR BR BR
-   Save the Configuration
-   Confirm Users from different LDAP registries are able to Login with
    the Mapped Roles

## Import Users

-   By default User Synchronization operation picks
    **UserID=sAMAccountName** for Microsoft AD and **UserId=uid** for
    IBM Tivoli Directory Server and ApacheDS.
-   If you wish to change the User ID mapping, follow the instructions
    from JAS and SCIM Article [Configure SCIM Property To UserID
    Mapping](https://jazz.net/wiki/bin/view/Deployment/JASAndSCIM#Configure_SCIM_Property_To_UserI)
-   Test by importing a user from each LDAP server manually
-   Click on **Users \> Active Users \> Import Users**
-   Enter a search term, click on the User and Import the user
-   In the Active User Page, click on the newly imported user and
    confirm the UserId , Name and email maps to what you intended to
    configure
-   If the verification is complete, you can then "Synchronize the users
    from multiple LDAP User registries to CLM
    -   Navigate to <https:/jtsserver:port/jts/admin> page \> Home and
        Click on
        `Synchronize Jazz Team Server Users With External User Registry`

##### Related topics: [Jazz Authorization Server](JazzAuthorizationServer), [Configuring Jazz Authorization Server for SCIM](JASAndSCIM) [related-topics-jazz-authorization-server-configuring-jazz-authorization-server-for-scim]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

META:FILEATTACHMENT{name="SCIM_Groups_Multiple.png"
attachment="SCIM_Groups_Multiple.png" attr="h" comment=""
date="1487776068" path="SCIM_Groups_Multiple.png" size="198341"
user="shubjit" version="1"} META:FILEATTACHMENT{name="Nightly_Sync.png"
attachment="Nightly_Sync.png" attr="h" comment="" date="1488195756"
path="Nightly_Sync.png" size="46199" user="shubjit" version="1"}
META:FILEATTACHMENT{name="SCIM_Multiple_Groups.png"
attachment="SCIM_Multiple_Groups.png" attr="h" comment=""
date="1574083313" path="SCIM_Multiple_Groups.png" size="163137"
user="shubjit" version="1"}
