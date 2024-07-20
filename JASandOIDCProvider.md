META:TOPICINFO{author="shubjit" date="1673448566" format="1.1"
version="1.16"} META:TOPICPARENT{name="JazzAuthorizationServer"}

# Configuring ELM Authentication with a third Party OIDC provider DKGRAY Authors: Main.ShubjitNaik [configuring-elm-authentication-with-a-third-party-oidc-provider-dkgray-authors-main.shubjitnaik]

Build basis: Engineering Lifecycle Management and Jazz Authorization
Server 7.x ENDCOLOR

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
delegate the user authentication to your standard, corporate OpenID
Connect provider using the Liberty "Social Login" feature. Using this
method we can delegate authentication from JAS to another OIDC provider.
This is the focus of the article.

The configuration information are extracted and modified for JAS from
[Liberty Topic: Configuring Social Login in
Liberty](https://www.ibm.com/docs/en/was-liberty/core?topic=liberty-configuring-social-login-in#twlp_sec_sociallogin__openid)

## Limitations

In this approach the user authentication is further delegated from JAS
to another OIDC provider and this leads to redirections which some
clients cannot do. Following are the limitations

-   ELM Version 7.0.2 and higher- Starting version 7.0.2 you can
    configure [Application Passwords](EnableJASAppPasswords) for Non-Web
    Clients
-   ELM Version 7.0.1 and lower - Authenticating through a 3rd Party
    OIDC provider works only for Browser based clients
    -   Thick Clients (Eclipse, Visual Studio) and Command line
        utilities can be configured to authenticate via JAS.
-   There is a requirement of an LDAP server (User Registry) for JAS for
    ID Token and Application Passwords mapping and for ELM for
    User-to-group role mapping (Or SCIM can be used)

## Deployment Pattern

The following diagram depicts the deployment topology and the
authentication flow.

BR

## Overview of Configuration

Overview of the different steps involved in this configuration.

-   Configure JAS with LDAP and ELM with JAS
-   Configure CA Certificates for JAS
-   Configure Social Login in JAS to Redirect to 3rd Party OIDC Provider
-   Create ClientId and Secret for JAS on the 3rd Party OIDC Provider
-   Configure Filters for Non-Web Clients

## Configure JAS with LDAP and ELM with JAS

Although the authentication is redirected and performed by the Third
Party OIDC Provider, JAS and ELM still needs to connect to the LDAP
server for User-to-group role mapping (JazzAdmins, JazzUsers and so on)
and JAS as well needs to be configured with the same LDAP server for ID
Token and Application Passwords mapping. Most customers don't expose the
LDAP server working with the Third Party OIDC Provider and instead
create a replica with limited attributes and passwords disabled.

As a pre-req , first configure JAS with the LDAP server and then setup
ELM [Configure JAS with
LDAP](https://jazz.net/wiki/bin/view/Deployment/JASUserRegistryConfig)

## Configure CA Certificates for JAS

The default certificate generated is a self-signed certificate for
common Name `localhost`. While this works for JAS and ELM with warnings,
it would fail when configuring with another OIDC Provider. You would
need to generate a CA certificate for JAS where CA is your Enterprise
Certificate provider.

You could also generate an updated Self-Signed certificate with Common
Name matching your JAS URL. You would then need to import the new
certificate generated for JAS to the truststore of your OIDC Server and
also import the certificate from discovery endpoint into JAS truststore.

By default the Social Login configuration uses the RS256 signature
algorithm.

## Configure Social Login in JAS to Redirect to 3rd Party OIDC Provider

You can configure a Liberty server so that users can authenticate to
websites that are hosted on the Liberty server by logging in with their
social media accounts. For JAS to connect to a different OIDC server we
define our own social login configuration that is based on the OAuth 2.0
or OpenID Connect 1.0 standards.

In Liberty, social login is enabled by the socialLogin-1.0 feature. Here
are instructions to configure Social Login for a 3rd Party OIDC server.

-   Open the `[JAS_HOME]\wlp\usr\servers\jazzop\server.xml`
    configuration file and add the socialLogin-1.0 , ssl-1.0 and
    appSecurity-2.0 features.

socialLogin-1.0 appSecurity-2.0 ssl-1.0 ...

-   Add the `oidcLogin` element and configure the connection to your
    OIDC provider
-   Define the OIDC server endpoints on the `authorizationEndpoint` ,
    `tokenEndpoint` , `jwksUri` and `issuer` attributes The Liberty
    server first redirects the user to the authorization endpoint to
    authenticate the user and obtain the OAuth authorization code. Then,
    it invokes the token endpoint to exchange the OAuth authorization
    code for an OAuth token.

<!-- -->

-   The endpoints data required in the configuration can be obtained
    from the discovery endpoint URL of the OIDC provider. Lets take an
    example of Google OIDC provider, the discovery endpoint URL is
    `https://accounts.google.com/.well-known/openid-configuration`

<!-- -->

-   The configuration with data from the discovery endpoint is as seen
    below and needs to be included in
    `[JAS_HOME]\wlp\usr\servers\jazzop\appConfig.xml` after
    `oauthProvider` section

<!-- -->

-   The `clientId` and `clientSecret` are to be generated by your OIDC
    provider (In the next step)
-   The redirect URL points to the ID of your configured oidcLogin
    element in the following format

[https://liberty_host:SSL_port/ibm/api/social-login/redirect/oidclogin_id](https://liberty_host:SSL_port/ibm/api/social-login/redirect/oidclogin_id)

-   For example, the redirect URL for the oidcLogin configuration
    example has the following format:

<https://%5BJAS_HOST%5D>:\[Port\]/ibm/api/social-login/redirect/myoidcserver

## Create ClientId and Secret for JAS on the 3rd Party OIDC Provider

Create an application for JAS in your corporate OIDC provider and
register the server with the application by providing a redirect URL of
JAS as mentioned in the previous step.

For example, the redirect URL for the oidcLogin configuration example
has the following format:

<https://%5BJAS_Host%5D>:\[Port\]/ibm/api/social-login/redirect/myoidcserver

After you create the application, note the Client ID and Client Secret.
Update them in the JAS configuration created in step 3, the attributes
to be updated are `clientId="[my_client_Id]"` and
`clientSecret="[my_client_password]"`

## Configure Filters for Non-Web Clients

Starting version 7.0.2 you can configure [Application
Passwords](https://jazz.net/wiki/bin/view/Main/ApplicationPasswordsForNativeClients)
for Non-Web Clients. The filters are different when JAS is configured
with App passwords.

In 7.0.1 and below, The OIDC authentication flow works for Web Clients
only. We need to add a filter to redirect only the browser based clients
to the 3rd party OIDC server. This way the Thick clients like Eclipse,
VS and command line utilities would directly authenticate with the
underlying LDAP configured with JAS.

The filter configuration is as follows:

Include this filter configuration id within the oidcLogin section that
was configured earlier.

For further information on using filters review [this
page](https://www.ibm.com/support/knowledgecenter/SSD28V_liberty/com.ibm.websphere.liberty.autogen.nd.doc/ae/rwlp_config_oidcLogin.html)

## Configure Logout

With ELM authentication is configured with a Third Party OIDC Provider,
the Logout operations from ELM does not complete. We have documented a
Workaround (link below) where ELM uses a custom *Web Logout URI*. This
workaround would work if you can directly access to the OIDC Logout URL.

[Configure Logout for ELM when configured with Third Party OIDC
Provider](https://jazz.net/wiki/bin/view/Deployment/LogoutJASSAMLOIDC#JAS_configured_with_a_Third_Part)

##### Related topics: [Deployment web home](DeploymentWebHome), [Jazz Authorization Server Landing Page](JazzAuthorizationServer) [related-topics-deployment-web-home-jazz-authorization-server-landing-page]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

META:FILEATTACHMENT{name="topology_oidc.png"
attachment="topology_oidc.png" attr="h" comment="" date="1566212277"
path="topology_oidc.png" size="67022" user="shubjit" version="1"}
