META:TOPICINFO{author="shubjit" date="1686725025" format="1.1"
version="1.9"} META:TOPICPARENT{name="JazzAuthorizationServer"}

# Configuring Jazz Authorization Server with a SAML IdP DKGRAY Authors: Main.ShubjitNaik Build basis: IBM Engineering Lifecycle Management and Jazz Authorization Server Version 7.0.2 and higher [configuring-jazz-authorization-server-with-a-saml-idp-dkgray-authors-main.shubjitnaik-build-basis-ibm-engineering-lifecycle-management-and-jazz-authorization-server-version-7.0.2-and-higher]

ENDCOLOR

TOC{title="Page contents"}

[SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language)
(Security Assertion Markup Language) is an OASIS open standard for
representing and exchanging user identity, authentication, and attribute
information. A SAML assertion is an XML formatted token that is used to
transfer user identity and attribute information from the identity
provider (IdP) of a user to a trusted service provider (SP) as part of
completing an SSO request.

With the introduction of [Jazz Authorization
Server](JazzAuthorizationServer) (JAS), we can configure IBM Engineering
Lifecycle Management Solution to redirect authentication to a SAML
Identity Provider via JAS. For additional information on SAML and
WebSphere Liberty visit our [Infocenter
Page](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_saml_web_sso.html)

The focus of this article is showcase configuring ELM and JAS with
[SimpleSAMLphp](https://simplesamlphp.org/) as the IdP.

## Limitations

When the user authentication is delegated from JAS to a SAML IdP there
are a few limitations:

-   ELM Version 7.0.1 and lower - Authenticating through a SAML IdP
    works for Browser based clients
    -   Thick Clients (Eclipse, Visual Studio) and Command line
        utilities can be configured to authenticate directly via JAS and
        LDAP.
-   ELM Version 7.0.2 and higher- Starting version 7.0.2 you can
    configure [Application Passwords](EnableJASAppPasswords) for Non-Web
    Clients
-   There is a requirement of an LDAP server (User Registry) for JAS for
    ID Token and Application Passwords mapping and for ELM for
    User-to-group role mapping (Or SCIM can be used)

## Overview of Configuration

Overview of the different steps involved in this configuration.

-   Configure JAS with an LDAP server (LDAP server should replicate ELM
    users from SAML IdP)
-   Configure [CA Certificates](ConfigureCACertificates) for JAS
-   Setup ELM with JAS or Migrate and existing setup from container
    authentication to JAS
-   Enable SAML feature and configurations in JAS
-   Export the Metadata from JAS to SAML IdP
-   Copy the SAML IdP
    [metadata](https://en.wikipedia.org/wiki/SAML_metadata) to JAS
-   Test Configurations

## Configure JAS with LDAP and ELM with JAS

Although the authentication is redirected and performed by the SAML IdP,
ELM still needs to connect to the LDAP (via Advanced Properties in JTS)
server for User-to-group role mapping (JazzAdmins, JazzUsers and so on)
and JAS as well needs to be configured with the same LDAP server for ID
Token and Application Passwords mapping. Most customers don't expose the
LDAP server working with the SAML IdP and instead create a replica with
limited attributes and passwords disabled.

As a pre-req , first configure JAS with the LDAP server and then setup
ELM [Configure JAS with
LDAP](https://jazz.net/wiki/bin/view/Deployment/JASUserRegistryConfig)

## Enable JAS to support SAML 2.0

Extracting the instructions from [ELM
Documentation](https://www.ibm.com/docs/en/elm/7.0.2?topic=server-enabling-saml-as-identity-provider)
and [Liberty
Documentation](https://www.ibm.com/docs/en/was-liberty/nd?topic=liberty-configuring-saml-web-browser-sso-in)

-   Edit `JazzAuthServer_install_dir/wlp/usr/servers/jazzop/server.xml`
    and uncomment the following features samlWeb-2.0

ssl-1.0

\* Edit
`JazzAuthServer_install_dir/wlp/usr/servers/jazzop/appConfig.xml` and
uncomment/update the `samlWebSso2.0` and `authFilter` elements

\* If you have a requirement to change the ID from `defaultSP` to a
custom ID then add the following section in `appConfig.xml`

-   For additional details on the SAML attributes and filters visit this
    [Liberty
    Documentation](https://www.ibm.com/docs/en/was-liberty/nd?topic=configuration-samlwebsso20)
-   With the above configuration JAS is now configured as a SAML Service
    Provider (SP)

## Export SP Metadata from JAS

For Jazz Authorization Server to communicate with the SAML IdP, the
server must be registered as a partner in the IdP. You can download /
export the SP metadata from JAS to register it as a partner. Registering
and enabling a partner depends on the SAML implementation in your IdP,
you can follow the SAML documentation or contact you Administrator.

When JAS is configured as a SAML Service Provider you can
download/export the metadata

-   Start Jazz Authorization Server
    `JazzAuthServer_install_dir/start_jazz`
-   Download the SP metadata by accessing the following URL
    <https://jas.example.org/ibm/saml20/defaultSP/samlmetadata>

<!-- -->

-   If you are not prompted to save the file, review your SAML
    configurations in the appConfig.xml and server.xml file on JAS
-   If you have changed the default ID in JAS SAML configurations,
    replace `defaultSP` in the URL with the ID that you have defined
-   Metadata from JAS needs to be generated again if there is a change
    in certificates

<!-- -->

-   Share the `spMetadata.xml` file with SAML IdP administrator

## Import SAML IdP Metadata into JAS

For the Jazz Authorization Server to communicate with the SAML IdP you
must import the SAML IdP metadata file

-   Request for the SAML IdP metadata file from your SAML administrator
-   Some of the SAML Identity Providers provide URLs to download
    metadata directly, example of ADFS and SimpleSAMLphp are given
    below.
-   Example Microsoft ADFS: You can download the metadata for Microsoft
    ADFS by accessing the URL
    <https://adfs.example.org/federationmetadata/2007-06/federationmetadata.xml>
-   Example SimpleSAMLphp: You can download the metadata for
    SimpleSAMLphp by accessing the URL
    <https://simplesamlphp.example.org/simplesaml/saml2/idp/metadata.php>
-   Rename the IdP metadata file to `idpMetadata.xml` (Case sensitive if
    JAS is running on UNIX based systems)
-   Copy the `idpMetadata.xml` to
    `JazzAuthServer_install_dir/wlp/usr/servers/jazzop/resources/security`

## SAML IdP Examples

### SimpleSAMLphp

[SimpleSAMLphp](https://simplesamlphp.org/) is a PHP-written application
that deals with authentication. Its main focus is to provide support for
SAML as a Service Provider (SP) or an Identity Provider (IdP). In this
example, SimpleSAMLphp is the Identity Provider (IdP).

The following steps demonstrate how to install and configure
SimpleSAMLphp.

-   Download and install the SimpleSAMLphp package from their
    [website](https://simplesamlphp.org/download/)
-   For prerequisites and details, see [SimpleSAMLphp Installation and
    Configuration](https://simplesamlphp.org/docs/latest/simplesamlphp-install.html)
-   To enable the IdP functionality, see the [SimpleSAMLphp Identity
    Provider
    QuickStart](https://simplesamlphp.org/docs/latest/simplesamlphp-idp.html)
-   Configure Authentication and metadata for the local Identity
    Provider and remote Service Provider, for instructions, see
    [SimpleSAMLphp Identity Provider
    QuickStart](https://simplesamlphp.org/docs/latest/simplesamlphp-idp.html)

<!-- -->

-   Here is an example of the file `saml20-idp-hosted.php`
    'simplesaml.example.org',

// X.509 key and certificate. Relative to the cert directory.
'privatekey' =\> 'simplesaml.key', 'certificate' =\> 'simplesaml.crt',

/\* Authentication source to use. Must be one that is configured in
'config/authsources.php'. \*/ 'auth' =\> 'example-userpass',
'userid.attribute' =\> 'uid', 'attributes.NameFormat' =\>
'<urn:oasis:names:tc:SAML:2.0:attrname-format:uri>' \];

#### Import JAS SP Metadata to SimpleSAMLphp

SimpleSAMLphp include a Metadata converter UI which can be used to
covert the metadata format that can be added to `saml20-sp-remote.php`

-   Access the URL sample
    `https://simplesaml.example.org/simplesaml/admin/metadata-converter.php`
-   Upload the JAS spMetadata.xml file and click Parse
-   Copy the converted data into `metadata/saml20-sp-remote.php`
-   Configure additional additional options required for your SP
    configuration, see [SP remote metadata
    reference](https://simplesamlphp.org/docs/latest/simplesamlphp-reference-sp-remote.html)
-   Test the Authentication Flow

### Microsoft ADFS

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
