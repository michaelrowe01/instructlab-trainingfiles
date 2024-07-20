META:TOPICINFO{author="tadhara" date="1606372783" format="1.1"
version="1.11"} META:TOPICPARENT{name="JazzAuthorizationServer"}

# How to configure Jazz Authentication Server with App ID on IBM Cloud DKGRAY Authors: -- Main.TadahiroHara - 2020-11-26 Build basis: ELM 7.0.2 and higher ENDCOLOR [how-to-configure-jazz-authentication-server-with-app-id-on-ibm-cloud-dkgray-authors----main.tadahirohara---2020-11-26-build-basis-elm-7.0.2-and-higher-endcolor]

TOC{title="Page contents"}

Starting with the Collaborative Lifecycle Management Solution 6.0
software release, Jazz Security Architecture SSO is available as an
authentication option. Based on [OpenID
Connect](http://openid.net/connect/faq) , authentication is NOT
performed by the container hosting Jazz applications, but instead is
delegated to a separate Jazz Authorization Server (JAS), which performs
the role of an OpenID Connect provider (OP).

For further Information on Jazz Security Architecture you can visit our
jazz.net article [Jazz Server Authentication
Explained](https://jazz.net/library/article/75)

You can configure the Liberty OpenID Connect Provider to further
delegate the user authentication like [App
ID](https://cloud.ibm.com/catalog/services/app-id) on IBM cloud using
the Liberty "Social Login" feature. This article shows an example of
configuration with JAS and App ID.

The configuration information are extracted and modified for JAS from
[Liberty Topic: Configuring Social Login in
Liberty](https://www.ibm.com/support/knowledgecenter/SSD28V_liberty/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_sociallogin.html#twlp_sec_sociallogin__openid)
and [Configuring CLM Authentication with a 3rd Party OIDC
provider](JASandOIDCProvider)

## Limitations

In this approach the user authentication is further delegated from JAS
to App ID and this leads to redirections which some clients cannot do.
Following are the limitations

-   Authenticating with App ID works only for Browser based clients
-   Thick Clients (Eclipse, Visual Studio) and Command line utilities
    can be configured to authenticate via JAS and hence JAS needs to be
    connected to the own LDAP server or local directory as App ID does
    not provides LDAP access. Alternatively Client Certificate or Native
    Password can be considered.

## Deployment Pattern

The following diagram depicts the deployment topology and the
authentication flow.

## Overview of Configuration

Overview of the different steps involved in this configuration.

-   Configure on App ID
-   Configure OIDC Login in liberty in JAS
-   Set Redirect URL from JAS in App ID
-   Import certificate of App ID in a trust store in JAS
-   Add users to Cloud Directory in App ID ( Optional )

## Configure on App ID

### Create App ID instance on IBM cloud

You can deploy [App ID](https://cloud.ibm.com/catalog/services/app-id)
instance from catalog in IBM Cloud when you have an account of IBM
Cloud.

Deploying App ID instance.

### Add Application to App ID

you can add "Application" to get information for liberty OIDC settings.
please navigate Application from menu.

Adding an application in App ID.

You can get information for liberty OIDC settings after adding an
"Application".

{ "clientId": "xxxx1234-1234-1234-xxxx-e18890408990", "tenantId":
"xxxx1234-1234-1234-1234-206ad598442e", "secret":
"XXXXXXXXXXXXMDRkMC00ZTRjLTk1Y2MtYWU4MTIzNmQ2ZDZl", "name": "JAS",
"oAuthServerUrl":
"<https://au-syd.appid.cloud.ibm.com/oauth/v4/xxxx1234-1234-1234-1234-206ad598442e>",
"profilesUrl": "<https://au-syd.appid.cloud.ibm.com>",
"discoveryEndpoint":
"<https://au-syd.appid.cloud.ibm.com/oauth/v4/xxxx1234-1234-1234-1234-206ad598442e/.well-known/openid-configuration>",
"type": "regularwebapp", "scopes": \[ "myscope01" \] }

## Configure OIDC Login in liberty in JAS

You need to configure server.xml and appConfig.xml in liberty in JAS to
redirect authentication to App ID.

-   Open the `[JAS_HOME]\wlp\usr\servers\jazzop\server.xml`
    configuration file and add the socialLogin-1.0 , ssl-1.0
-   Add the `oidcLogin` element and configure the connection to App ID
    by referring "Application" information.

|                        |                                    |
|------------------------|------------------------------------|
| Attribute in oidcLogin | Value from Application Information |
| clientId               | {clientId}                         |
| clientSecret           | {secret}                           |
| authorizationEndpoint  | {oAuthServerUrl}/authorization     |
| tokenEndpoint          | {oAuthServerUrl}/token             |
| issuer                 | {oAuthServerUrl}                   |
| jwksUri                | {oAuthServerUrl}/publickeys        |
| scope                  | {scopes}                           |

##### 

Example of configuration.

socialLogin-1.0 appSecurity-2.0 ssl-1.0 ...

authFilterRef="myoidcAuthFilter" \>

##### 

Please see [OIDC discovery
document](https://cloud.ibm.com/docs/appid?topic=appid-discovery) and
[Liberty Topic: Configuring Social Login in
Liberty](https://www.ibm.com/support/knowledgecenter/SSD28V_liberty/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_sociallogin.html#twlp_sec_sociallogin__openid)
for details

## Set Redirect URL from JAS in App ID

You need to set "Redirect URL" of JAS to App ID. please navigate
Identity Providers \> Manage \> Authentication Settings.

For example, the redirect URL for the oidcLogin configuration example
has the following format:

<https://%5BJAS_Host%5D>:\[Port\]/ibm/api/social-login/redirect/oidclogin_id

The following error message shows when redirect URL is not set in App
ID.

Please see [Adding redirect
URIs](https://cloud.ibm.com/docs/appid?topic=appid-managing-idp#add-redirect-uri)
for details.

## Import a certificate of App ID in a trust store in JAS

You need to import a certificate of App ID in a trust store in JAS or
you can see the following error when http request is redirected from App
ID.

CWPKI0823E: SSL HANDSHAKE FAILURE: A signer with SubjectDN
\[CN=au-syd.appid.cloud.ibm.com, O=International Business Machines
Corporation, L=Armonk, ST=New York, C=US\] was sent from the host
\[au-syd.appid.cloud.ibm.com:443\]. The signer might need to be added to
local trust store \[ibm-team.keystore\], located in SSL configuration
alias \[defaultSSLConfig\]. The extended error message from the SSL
handshake exception is: \[PKIXCertPathBuilderImpl could not build a
valid CertPath.\].

-   import the certificate to the Liberty truststore
    `[JAS_HOME]\wlp\usr\servers\jazzop\ibm-team.keystore` file, in your
    browser, go to one of the endpoints specified by the oidcLogin
    element `au-syd.appid.cloud.ibm.com`, and export the certificate.
    Use a key management tool such as iKeyman or the Java keytool
    utility to add the certificate to the Liberty truststore file.

## Add users to Cloud Directory in App ID (Optional)

When you use Cloud Directory for user management you can add users by
referring [Add
Users](https://cloud.ibm.com/docs/appid?topic=appid-cd-users#add-users).
When you only use IBM ID for user management this is not needed.

## After configuration

After configuration, when you access to JTS application, your request
will be redirect to Login Form in App ID on IBM Cloud.

##### Related topics: [related-topics]

-   [Configuring CLM Authentication with a third Party OIDC provider
    ](JASandOIDCProvider)

##### External links: [external-links]

-   [App ID](https://cloud.ibm.com/catalog/services/app-id)
-   [Liberty Topic: Configuring Social Login in
    Liberty](https://www.ibm.com/support/knowledgecenter/SSD28V_liberty/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_sociallogin.html#twlp_sec_sociallogin__openid)

##### Additional contributors: [additional-contributors]

META:FILEATTACHMENT{name="Topology.png" attachment="Topology.png"
attr="h" comment="Topology Image for JAS and App ID integration"
date="1605251522" path="Topology.png" size="37190" user="tadhara"
version="1"} META:FILEATTACHMENT{name="AddApplication.png"
attachment="AddApplication.png" attr="h" comment="" date="1605585738"
path="AddApplication.png" size="16588" user="tadhara" version="1"}
META:FILEATTACHMENT{name="App_ID\_-\_IBM_Cloud.png"
attachment="App_ID\_-\_IBM_Cloud.png" attr="h" comment=""
date="1605585823" path="App_ID\_-\_IBM_Cloud.png" size="60906"
user="tadhara" version="1"}
META:FILEATTACHMENT{name="ApplicationInfo2.png"
attachment="ApplicationInfo2.png" attr="h" comment="" date="1605585932"
path="ApplicationInfo2.png" size="22191" user="tadhara" version="1"}
META:FILEATTACHMENT{name="Applicaion.png" attachment="Applicaion.png"
attr="h" comment="" date="1605586328" path="Applicaion.png" size="5848"
user="tadhara" version="1"}
META:FILEATTACHMENT{name="ErrorWhenNoRedirectURL.png"
attachment="ErrorWhenNoRedirectURL.png" attr="h" comment=""
date="1605591209" path="ErrorWhenNoRedirectURL.png" size="34830"
user="tadhara" version="1"} META:FILEATTACHMENT{name="RedirectURL.png"
attachment="RedirectURL.png" attr="h" comment="" date="1605591254"
path="RedirectURL.png" size="9968" user="tadhara" version="1"}
META:FILEATTACHMENT{name="LoginForm.png" attachment="LoginForm.png"
attr="h" comment="Login Form" date="1606205596" path="LoginForm.png"
size="19588" user="tadhara" version="1"}
