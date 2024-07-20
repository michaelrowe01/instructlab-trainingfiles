# Jazz Security Architecture and Jazz Authorization Server

Authors: Main.ShubjitNaik 
Build basis: Jazz Authorization Server 6.x, 7.x 

Starting with the CLM 6.0 software release, Jazz Security Architecture
(JSA) SSO is available as an authentication option. Based on [OpenID
Connect](http://openid.net/connect/faq), the authentication is not
performed by the container hosting Jazz applications, but instead is
delegated to a separate Jazz Authorization Server (JAS), which performs
the role of an OpenID Connect provider (OP). JAS also provides Single
Sign On feature to the applications that are configured with it. BR
BRInformation related to Jazz Security Architecture is extracted from
our jazz.net article [Jazz Server Authentication
Explained](https://jazz.net/library/article/75)

## About OIDC, JSA and JAS

The [OpenID Connect (OIDC)](http://openid.net/connect) authentication
protocol was established in early 2015 as an extension of the [OAuth
2.0](https://oauth.net/2) protocol, designed to be easier to adopt
across a wide range of clients (native applications, browsers,
browser-based applications, and mobile devices). It is extensible and
configurable (with optional features). OpenID Connect is a simple
identity protocol and open standard that is built on top of the OAuth
2.0 protocol that enables client applications to rely on authentication
that is performed by an OpenID Connect Provider to verify the identity
of a user. OpenID is a protocol for authentication while OAuth is for
authorization. (Authentication is about making sure that the guy you are
talking to is indeed who he claims to be. Authorization is about
deciding what that guy should be allowed to do)

For additional information on OIDC and the authentication flow visits
our [Infocenter
page](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_openid_connect.html).

Jazz Security Architecture is a particular profile of OIDC, specifying
which optional features are included, and a few extensions.
Authentication is handled by a separate OpenID provider (OP, in our case
it would be our Jazz Authorization Server); Jazz applications delegate
to that provider instead of relying on the application server to handle
authentication. Jazz Authorization Server is based on the IBM WebSphere
Liberty server. Because Jazz Authorization Server authenticates users,
it must be configured with a user registry.

When a user logs into a Jazz application, JAS (OP) generates a token for
the user (known as a bearer token) that can then be used to authenticate
with any application that is configured with the same OP. Therefore,
Jazz Security Architecture provides a single sign-on experience that is
independent of the type of application container, unlike Kerberos,
WebSphere, and Tomcat single sign-on mechanisms. Single sign-on is
supported across all applications that are configured to use the same
JAS.

Configuring Jazz applications for Jazz Security Architecture SSO is
either done at install time, for new installations, or done as a
migration procedure, for existing installations that are using some
other form of authentication.

### Application To Application Authentication

In addition to authenticating end users that access Jazz applications,
applications also authenticate requests sent by other applications. In
particular, applications that participate in Open Services Lifecycle
Collaboration use linked data to share and connect resources across
application development domains. There are two forms of
application-to-application authentication implemented by Jazz
applications, OAuth 1.0a and OpenID Connect.

Up until the 6.0 software release, OAuth 1.0a was the only type of
inter-application authentication supported. It requires pair-wise
relationships between communicating applications - applications that are
registered as "friends" of each other can send requests to each other
that will be authenticated using OAuth 1.0a. For bi-directional
communications, each application must be a friend of each other. The
friending application is allocated a key and secret which it uses to
authenticate with the friend application.

When applications are configured with Jazz Security Architecture SSO
enabled, they can use OpenID Connect to authenticate with each other. In
that case, no pair-wise relationships are needed between applications
for authentication purposes; no "keys" or "secrets" are held by
applications in order to authenticate with each other. Instead, when a
user authenticates with an application that has Jazz Security
Architecture SSO enabled, that user is automatically authenticated with
all other applications that are registered with the same Jazz
Authorization Server as the first application. Therefore, applications
can invoke services in other applications on behalf of the user without
requiring additional logins.

## Advantages Of Using JAS

Jazz Security Architecture is one of our Authentication and Single
Sign-On (SSO) solution for Jazz Application starting CLM 6.x. JSA
eliminates the requirement for paired configuration of OAuth consumer
keys. All applications that are configured for Jazz Security
Architecture SSO can communicate with each other without a configuration
for every possible source and destination relationship.

**OAuth 2.0**

When deployed with Jazz Authorization Server (IBM Liberty OIDC feature)
ELM supports OAuth 2.0.

Up until the 6.0 software release, OAuth 1.0a was the only type of
inter-application authentication supported. Starting CLM version 6.0
Jazz Authorization Server was introduced and when applications are
configured with Jazz Security Architecture SSO enabled, they can use
OpenID Connect to authenticate with each other. OpenID Connect is a
simple identity protocol and open standard that is built on top of the
OAuth 2.0 protocol that enables client applications to rely on
authentication that is performed by an OpenID Connect Provider to verify
the identity of a user.

Here are the articles available on OAuth 2.0 and ELM.

-   [OAuth 2.0 and Accessing ELM Resources](ELMAndOAuth20)
-   [OAuth 2.0 Access flow with ELM Configured with Third Party OIDC
    Provider](ELMAndOAuth20WithOIDCProvider)
-   [ELM and OAuth 2.0 Server to Server communication via Client
    Credentials Grant](ELMAndOAuth20ServerToServer)

**SAML or OIDC Providers - Authentication and SSO via Third Party
Identity Providers**

As JAS is a Liberty OpenID Connect Provider, it can be configured to
further delegate authentication to a [SAML Identity
Provider](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.2/com.ibm.jazz.install.doc/topics/t_jsasso_jas_user_mgmt_saml.html)
or a [Third Party OIDC Provider](JASandOIDCProvider).

-   SSO is achieved across different vendor applications along with ELM
    applications connected to the SAML or OIDC Provider
-   Possibility to Leverage Multi-Factor Authentication via Third Party
    Identity Providers
-   Limitations
    -   Until version 7.0.1, Multi Factor Authentication Works only for
        Web Clients
-   Starting version 7.0.2 you can configure [Application
    Passwords](https://jazz.net/wiki/bin/view/Main/ApplicationPasswordsForNativeClients)
    for Non-Web Clients

**Reduced Maintenance**

-   JAS would be the only server to be configured for Authentication and
    JTS for User to group role mappings
    -   On a distributed setup without JAS, each application server
        (profile) hosting Jazz applications need to configured with LDAP
        and Group Mappings need to be setup
-   Changes to Group Mappings does not need a restart, reducing the
    maintenance time of restarting each Application server hosting Jazz
    applications

**Federated User Registries**

-   We can configure [JAS with SCIM](JASSCIMFederatedRepositories) for
    seamless Synchronization of Users from multiple user registries

##### Related topics:
- [Jazz Server Authentication Explained](https://jazz.net/library/article/75) [related-topics-jazz-server-authentication-explained]
