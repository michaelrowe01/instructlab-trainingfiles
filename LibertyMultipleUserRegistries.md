META:TOPICINFO{author="shubjit" date="1647364632" format="1.1"
version="1.5"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Configuring Federated LDAP registries for Jazz Applications on WebSphere Liberty Profile DKGRAY Authors: Main.ShubjitNaik [configuring-federated-ldap-registries-for-jazz-applications-on-websphere-liberty-profile-dkgray-authors-main.shubjitnaik]

Build basis: IBM Collaborative Lifecycle Management 6.0.1 and higher
ENDCOLOR

TOC{title="Page contents"}

**Federation of user registries on WebSphere Liberty** BR

WebSphere Application Server Liberty Profile allows configuring Multiple
federated registries. User registry federation is used when user and
group information is spread across multiple registries. For example, the
information might be in two different LDAPs, in two subtrees of the same
LDAP, in a file, or the users are of a system. The information might
even be in a custom user data repository. With registries federated, you
can search and use these distributed user information in a unified
manner with continuous store of information. Using federated registry,
you can use the unified view for authentication and authorization of
users in Liberty.

There are 2 parts to setting up Federated User Registries for CLM.

-   Configuring WebSphere Liberty Profiles hosting Jazz Applications
    with Federated Registries
-   Configuring CLM to Import Users from Multiple User Registries

## Scenarios

-   Configuring Federated Registries on a departmental/ single server
    topology
-   Configuring Federated Registries on a Distributed setup
-   Federating LDAP registry with a Basic User Registry

## Enable federated registries in Liberty

### Including Features to support Federated Registries

\* Enable the Liberty Profile to support Federated Registries \* Edit
`Jazz_App_install_dir/server/liberty/servers/clm/server.xml` and include
the following in the list of features \* appSecurity-2.0 servlet-3.0
ldapRegistry-3.0

-   On a distributed setup, Configure each Liberty Profile hosting a
    Jazz Application with similar configurations

### Federate two or more LDAP registries

\* First ensure the Group Names planned to be used with Jazz are Unique
across all User registries (Example: JazzAdmin_host1, JazzAdmin_Host2)
\* Ensure the `ldapUserRegistry.xml` entry is enabled in
`Jazz_App_install_dir/server/liberty/servers/clm/server.xml`

\* Edit
`Jazz_App_install_dir/server/liberty/servers/clm/ldapUserRegistry.xml`
and modify to match your environment \* We have included a few examples
from different federated LDAP environments (MS Active Directory and
ApacheDS) to help guide the configuration

#### Microsoft Active Directory

\*

#### ApacheDS

\*

BR

-   The above example is from an ApacheDS server setup with Anonymous
    Authentication. Include the BindDN if necessary

### LDAP Registry federated with Basic

\* First ensure the Group Names planned to be used with Jazz are Unique
across the LDAP and Basic User registries (Example: JazzAdmin_host1,
JazzAdmin_Host2) \* Ensure the `ldapUserRegistry.xml` and
`basicUserRegistry.xml` entries are enabled in
`Jazz_App_install_dir/server/liberty/servers/clm/server.xml`

\* Edit
`Jazz_App_install_dir/server/liberty/servers/clm/conf/ldapUserRegistry.xml`
and modify to match your environment, you can include federate LDAP
registries as per the above example as well \* Edit
`Jazz_App_install_dir/server/liberty/servers/clm/conf/basicUserRegistry.xml`
and include Users and groups as per your requirement

-   You can either enter Plain Text Passwords or encrypt the passwords
    using the securityUtility

### Encrypt Passwords

-   To encrypt passwords, run the script
    `Jazz_App_install_dir/server/liberty/wlp/bin/securityUtility`
-   To run the securityUtility script, use the following syntax:
-   \$ securityUtility encode userPassword where *userPassword* is the
    password to encode
-   After the script completes, copy the output to the password
    attribute associated with the user ID (or bindPassword)

### Group to Role Mappings

\* Map Groups to the respective Jazz Roles \* Edit
`Jazz_App_install_dir/server/liberty/server/liberty/servers/clm/conf/application.xml`
and modify Group mapping for jts.war, ccm.war and qm.war

### Liberty server administration

\* Include Users/Groups for Liberty server administration \* These
Users/Groups would be able to access the Liberty server administration
page [https://SERVER:PORT/adminCenter](https://SERVER:PORT/adminCenter)
\* Edit
`Jazz_App_install_dir/server/liberty/server/liberty/servers/clm/server.xml`
and modify the section shown below

bclmadmin JazzAdmins_Host1

## Importing Users to Jazz Team Server (JTS)

### Importing Users from Federated LDAP Registries

`Note: You can only Synchronize users from one LDAP registry at a time into JTS.`

-   Configure your Jazz Team Server to your Primary LDAP server for
    Night Sync
-   To import from second LDAP registry to CLM, manually change the LDAP
    and group details in JTS \> Advanced Properties

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: \* [Federation of user registries - Liberty Profile](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/cwlp_repository_federation.html) [external-links-federation-of-user-registries---liberty-profile]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
