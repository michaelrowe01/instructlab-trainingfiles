META:TOPICINFO{author="shubjit" date="1700039845" format="1.1"
reprev="1.9" version="1.9"}
META:TOPICPARENT{name="JazzAuthorizationServer"}

# Configure ELM Authentication with Multiple SAML Identity Providers DKGRAY Authors: Main.ShubjitNaik Build basis: Engineering Lifecycle Management / Jazz Authorization Server 7.0.2 or higher [configure-elm-authentication-with-multiple-saml-identity-providers-dkgray-authors-main.shubjitnaik-build-basis-engineering-lifecycle-management-jazz-authorization-server-7.0.2-or-higher]

ENDCOLOR

TOC{title="Page contents"}

There are requirements where ELM has to be deployed in an environment
for users from different companies to collaborate. And in this scenario
the end users would need to authenticate against different SAML IDPs
which could be their respective company owned IDPs. Can we configure
multiple Identity Providers with IBM Engineering Lifecycle Management
Solution?

You can setup ELM to authenticate via [Jazz Authorization
Server](JazzAuthorizationServer) (JAS) which is based on WebSphere
Liberty. And using the [SamlWeb
2.0](https://www.ibm.com/docs/en/was-liberty/nd?topic=liberty-configuring-saml-web-browser-sso-in)
feature Liberty can be configured to further delegate the user
authentication to a Third Party SAML IdP.

When JAS is configured with multiple OIDC Providers, Liberty presents a
[Social Media Selection
Form](https://www.ibm.com/docs/en/was-liberty/core?topic=liberty-social-media-selection-form)
to pick from a list of configured Providers. Although when configured
with Multiple SAML IdPs a similar list is not available, we can depend
on
[AuthFilters](https://www.ibm.com/docs/en/was-liberty/nd?topic=configuration-samlwebsso20#authFilter)
or we can modify the deployment to include another Liberty server and
create unique filters to configure Authentication against Multiple SAML
IdPs, and this is the focus of the article.

## Configuration Options

There are two Use Cases for configuring JAS with multiple SAML IdPs

-   `Use Case 1` : Utilize Liberty SAML config AuthFilters to redirect
    to multiple SAML IdPs
    -   Configure JAS with Multiple IdPs , example documentation
        available
        [Here](https://www.ibm.com/docs/en/opw/8.2.0?topic=server-configuring-multiple-ids-saml-identity-provider)
    -   Configure AuthFilters for each SAML configuration, documentation
        available in [IBM
        Docs](https://www.ibm.com/docs/en/was-liberty/nd?topic=configuration-samlwebsso20#authFilter)

<!-- -->

-   `Use Case 2` : When none of the available
    [AuthFilters](https://www.ibm.com/docs/en/was-liberty/nd?topic=configuration-samlwebsso20#authFilter)
    works for your deployment, install an additional Liberty server
    -   The rest of the article targets `Use Case 2`

## Deployment Overview

The high level instructions to configure ELM with SAML IdPs:

-   Configure JAS with multiple LDAP servers via SCIM or with one
    consolidated LDAP server (LDAP server should replicate ELM users
    from all SAML IdPs)
-   Configure CA Certificates for JAS
-   Setup ELM with JAS or Migrate and existing setup from container
    authentication to JAS
-   Configure JAS to redirect to Multiple OIDC Providers
-   Create a new Liberty server and configure
    -   Multiple OIDC Providers (OP1 and OP2)
    -   Multiple SAML Configurations (samlSP1 and samlSP2)
    -   Configure SAML AuthFilters to match incoming URL patterns from
        JAS
    -   Export SP Metadata for each SAML config
    -   Import SAML IdP metadata from each IDP

The instructions for configuring JAS with a SAML IdP and a Third Party
OIDC Provider are documented in the following articles

-   [Configure ELM Authentication with a Third Party OIDC
    provider](JASandOIDCProvider)
-   [Configure ELM Authentication with a SAML Identity
    Provider](JASandSAML).

*Sample* *Deployment*

### Limitations

-   Logout from ELM applications does not work

## Configure JAS and User Group Role Mapping

First step is to configure ELM and JAS. You would need to either
configure JAS with multiple LDAPs, one each for a SAML IDP, or a
consolidated LDAP server which has a copy of all the Users from multiple
SAML IDPs.

-   To configure multiple LDAPs in JAS you would need to enable SCIM.
    Visit [Configure Multiple User Registries with JAS and
    SCIM](JASSCIMFederatedRepositories)
-   To configure a single LDAP with JAS Visit [Configure JAS with an
    LDAP User Registry](JASUserRegistryConfig)

User Groups to Jazz Roles mappings (JazzAdmins, JazzUsers etc) are
picked from JTS configuration when configured with JAS. When Users
accesses an ELM application URL, they are redirected to JAS for
Authentication. Post successful authentication JTS performs one of the
following:

-   When configured with SCIM, JTS does the group lookup via the SCIM
    URL and groups provided under JTS Admin \> Advanced Properties \>
    -   `com.ibm.team.repository.service.jts.internal.userregistry.scim.SCIMUserRegistryProvider`
        for User group to Jazz role mappings
-   When configured with LDAP, JTS does a group lookup via an ldapsearch
    Query against the LDAP and group details mentioned under JTS Admin
    \> Advanced Properties \>
    -   `com.ibm.team.repository.service.jts.internal.userregistry.ldap.LDAPUserRegistryProvider`
        for User group to Jazz role mappings.

Note: Special Subjects like ALL_AUTHENTICATED_USERS or NESTED_GROUPS
would not work with JAS based deployments

## Create a new Liberty Server for SAML Configurations

Create a new Liberty Server using the JAS installation on port `9644`
for Multiple OpenId Connect Providers and SAML Configurations.

### Create server

The following examples uses JAS to create another server and copy over
LDAP and SSL keystore files

-   Create a new liberty Server on Jazz Authorization Server
    -   `cd [JAS_HOME]/wlp/bin`
    -   `./server create samlop`
-   Copy LDAP configuration from jazzop to samlop
    -   `cd [JAS_HOME]/wlp/usr/servers/samlop`
    -   `mkdir defaults`
    -   `cp ../jazzop/defaults/ldapUserRegistry.xml defaults/`
-   Copy the ssl keystore from jazzop to samlop
    -   `cd [JAS_HOME]/wlp/usr/servers/samlop`
    -   `cp ../jazzop/ibm-team.keystore .`
-   Update JVM Config , create a file `jvm.options` and set heap to 4GB
    -   `cd [JAS_HOME]/wlp/usr/servers/samlop`
    -   `vi jvm.options`
    -   -Xmx4G

-Xms4G -Xmn1G

### Update features, Port and SSL configurations

Change directory to `[JAS_HOME]/wlp/usr/servers/samlop` and edit
`server.xml` (delete old content). Enable features, LDAP, SSL
configurations and set port to `9644`

openidConnectServer-1.0 appSecurity-2.0 ldapRegistry-3.0 ssl-1.0
samlWeb-2.0

### Create openidConnectProvider configurations

Append `server.xml` file, create a `openidConnectProvider` config for
each SAML IDP. Following is an example for 2 SAML IdPs

-   `id` and `oauthProviderRef` are unique per OpenId Provider
    configuration
-   Client `name`, `secret` and `redirect` URL ID will be used in the
    Social Login config on JAS

### Create Multiple SAML configurations

Import each SAML IDP metadata by copying it to
`[JAS_HOME]/wlp/usr/servers/samlop/resources/security`

Append `server.xml` file, configure multiple SAML IdP redirect
configurations and set AuthFilters to incoming JAS URLs based on the
`id` created in the previous step. Following is an example for 2 SAML
configurations.

-   `op1` and `op2` used in `urlPattern` are the =id='s created in the
    openidConnectProvider configuration

### Export multiple SP metadata

Start the Liberty Server using the command `[JAS_HOME}/start-jazz`

Export SP metadata to be shared with each SAML IDP. `samlSP1` and
`samlSP2` are IDs created in the samlWebSso20 config.

-   Download samlSP1 metadata -
    `https://[Jazz_Auth_Server]:9644/ibm/saml20/samlSP1/samlmetadata`
-   Download samlSP2 metadata -
    `https://[Jazz_Auth_Server]:9644/ibm/saml20/samlSP2/samlmetadata`

\_These files need to imported as Relying Party on the respective SAML
IdPs\_

Note: If the server is to be configured behind Reverse Proxy, access the
above URLs with the Reverse Proxy URLs.

### Test Multiple SAML IDP redirection

In the Endpoint URLs below `op1` and `op2` are `ids` created in the
openidConnectProvider configuration. Test by accessing the following
URLs, if they are redirected to a different SAML Idp

-   SAML IDP 1 access URL -
    `https://[Jazz_Auth_server]:9644/oidc/endpoint/op1/authorize`
-   SAML IDP 2 access URL -
    `https://[Jazz_Auth_server]:9644/oidc/endpoint/op2/authorize`

Note: If the Liberty server is to be configured behind Reverse Proxy,
access the above URLs with the Reverse Proxy URLs.

## Enable Redirection in JAS to multiple SAML IDPs

Now that a Liberty Server is configured with multiple SAML
configurations and also multiple OpenId Connect Providers (OP), we will
redirect JAS to each OP by configure multiple Social Login
configurations, creating an `oidcLogin` config for each OP configured in
the new liberty server

-   Change directory to =\[JAS_HOME\]/wlp/usr/servers/jazzop
-   Edit `server.xml` file and add the following features within
    `featureManager` socialLogin-1.0

appSecurity-2.0

-   If you have the `samlWeb-2.0` feature enabled on JAS, it can be
    disabled

\* Edit appConfig.xml and add the following configurations

-   `id` is picked from the OP `redirect` URL configured in Liberty
    server, example /samlop1
-   `clientId` and `clientSecret` is picked from `name` and
    `secret parameters from =oauthProvider` on the Liberty Server
-   `displayName` is the name shown on the Liberty Social Media
    Selection form

Note: If the Liberty server is to be configured behind Reverse Proxy,
update the `discoveryEndpoint` URLs with the Reverse Proxy URLs.

## Test the Deployment

The Liberty server start and stop would be in parallel with JAS
(`jazzop` starts first followed by `samlop`).

-   Start - `[JAS_HOME}/start-jazz`
-   Stop - `[JAS_HOME}/stop-jazz`

On accessing the ELM Application URI you woould be presented with the
following Selection Form

## Reverse Proxy - IBM HTTP Server Plugin Configuration

Here is an example of a merged plugin config for IBM HTTP Server

## Configure Local Authentication along with SAML Identity Provider

You can configure [Socal Login Web
Application](https://www.ibm.com/docs/en/was-liberty/core?topic=SSD28V_liberty/com.ibm.websphere.liberty.autogen.nd.doc/ae/rwlp_config_socialLoginWebapp.htm)
to include Local Authentication in the Selection form.

Add the following configuration along with all the `oidcLogin`
configurations:

Here is the updated selection form when Local Authentication is included

##### Related topics: [Jazz Authorization Server Landing Page](JazzAuthorizationServer) [related-topics-jazz-authorization-server-landing-page]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

META:FILEATTACHMENT{name="deployment_multiple_saml_idps.png"
attachment="deployment_multiple_saml_idps.png" attr="h" comment=""
date="1646809716" path="deployment_multiple_saml_idps.png" size="752152"
user="shubjit" version="1"} META:FILEATTACHMENT{name="saml_picker.png"
attachment="saml_picker.png" attr="h" comment="" date="1646821481"
path="saml_picker.png" size="23364" user="shubjit" version="1"}
META:FILEATTACHMENT{name="SAML_Local_Auth.png"
attachment="SAML_Local_Auth.png" attr="h" comment="" date="1700039759"
path="SAML_Local_Auth.png" size="55740" user="shubjit" version="1"}
