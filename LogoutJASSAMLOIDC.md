META:TOPICINFO{author="shubjit" date="1694174449" format="1.1"
version="1.19"} META:TOPICPARENT{name="JazzAuthorizationServer"}

# Configure Single Sign-On and Single Sign-Out for ELM configured with a SAML or OIDC Provider DKGRAY Authors: Main.ShubjitNaik Build basis: Engineering Lifecycle Management and Jazz Authorization Server 7.0.2 and Higher [configure-single-sign-on-and-single-sign-out-for-elm-configured-with-a-saml-or-oidc-provider-dkgray-authors-main.shubjitnaik-build-basis-engineering-lifecycle-management-and-jazz-authorization-server-7.0.2-and-higher]

ENDCOLOR

TOC{title="Page contents"}

Jazz Authorization Server (JAS) is a Liberty OpenID Connect Provider and
it can be configured to further delegate authentication to a [SAML
Identity Provider](JASandSAML) or a [Third Party OIDC
Provider](JASandOIDCProvider). The expectation is for Single Sign-On and
Sign-Out to work between ELM and non-ELM applications that are both
configured to use the same Provider.

The focus on this Article is on Single Sign-On and Logout. It is assumed
that you have configured JAS with either a SAML IdP or a Third Party
OIDC Provider.

## JAS configured with a SAML IdP

### Configuring Single Sign-On

The default configuration of JAS configured with SAML IdP indicates the
IdP to force the user to re-authenticate. We would need to change this
configuration for SSO to work between ELM and Non-ELM applications.

Steps to update the configuration: \* Edit `appConfig.xml` file located
at `[JAS_HOME]\wlp\usr\server\jazzop\appConfig.xml` \* Search for
`samlWebSso20` section and update the parameter *forceAuthn* to
`forceAuthn="false"` and add parameter *spLogout="true"*

-   Test Single Sign-On between ELM and Non-ELM applications

### Configuring Single Sign-Out

You would need to perform the following additional configuration changes
in JAS.

\* First confirm if the SAML `idpMetadata.xml` file contains `HTTP-POST`
binding for `SingleLogoutService`. IBM Liberty only supports SAML SSO
with `HTTP-POST` Bindings and not `HTTP-Redirect` Binding. \* [IBM
WebSphere Liberty SAML
Documentation](https://www.ibm.com/docs/en/was-liberty/nd?topic=authentication-saml-20-web-browser-single-sign)
\* An example entry looks like this

-   Next Upgrade the Liberty profile for JAS to 23.0.0.6 or higher
    -   Download Liberty version 23.0.0.6
        <https://www.ibm.com/support/pages/fix-list-ibm-websphere-application-server-liberty>
    -   Upgrade Jazz Authorization Server -
        <https://www.ibm.com/support/pages/node/6445491>

\* Edit `appConfig.xml` file located at
`[JAS_HOME]\wlp\usr\server\jazzop\appConfig.xml` \* Search for
`samlWebSso20` section and change the `spCookieName` parameter value
from `jazzop_sso_cookie_idp` to example `liberty_saml_idp_sso_cookie` or
to any name of your choice.

\* Add `/end_session` to the Authentication Filter `requestUrl`

### Configuring Single Sign-Out when SAML IdP does not support HTTP-POST

`This workaround would work if you can directly access the SAML !IdP Logout URL`
There are instances where SAML IdP does not support HTTP-POST for
`SingleLogoutService` and/or the above instructions does not work. You
could follow the workaround mentioned below, which are additional
configuration in ELM.

-   Request your Administrator to share the SAML IdP Logout URL that can
    be accessed directly
    -   Sample logout URL for example Microsoft ADFS
        `https://adfs.example.org/adfs/ls/?wa=wsignout1.0`
-   In each ELM application `jts, ccm, qm, rm, gc and dcc` perform the
    following:
    -   Access Advanced Properties
        `https://[ELM_URL]/[app]/admin#action=com.ibm.team.repository.admin.configureAdvanced`
    -   Search for the property `Web Logout URI` and update the value
        with the Logout URL received
    -   Search for the property
        `Trusted URIs for client authorization and redirection` and
        update the value with the Logout URL received
-   Test Logout from ELM Applications

## JAS configured with a Third Party OIDC Provider

### Configuring Single Sign-On

When ELM is configured with a Third Party OIDC Provider , no changes are
needed.

### Configuring Single Sign-Out

With the default configurations the Logout operations from ELM does not
complete. You would need to perform the following additional
configuration in ELM.
`This workaround would work if you can directly access the OIDC Logout URL`

-   Request your Administrator to share the OIDC Logout URL
    -   Sample logout URL from a customer
        `https://preprod.example.com/ui/oidcclient/logout`
-   In each ELM application `jts, ccm, qm, rm, gc and dcc` perform the
    following:
    -   Access Advanced Properties
        `https://[ELM_URL]/[app]/admin#action=com.ibm.team.repository.admin.configureAdvanced`
    -   Search for the property `Web Logout URI` and update the value to
        the Logout URL received
    -   Search for the property
        `Trusted URIs for client authorization and redirection` and
        update the value with the Logout URL received
-   Test Logout from ELM Applications

## Testing

After applying the Single Sign-On and Sign Out configurations mentioned
in the previous steps, following are the results

-   Single Sign-On is achieved between ELM and Non-ELM applications
-   Logout from an ELM Application will logout via the IdP logout URL
    and all other ELM Applications are logged out

<!-- -->

-   Logout from a Non-ELM application - ELM applications are NOT logged
    out immediately
    -   Post the SSO timeout which is set to 2 hours by default (can be
        changed), the applications are redirected to the IdP and
        existing sessions are logged out

##### Related topics: [Jazz Authorization Server Landing Page](JazzAuthorizationServer), [Configure ELM with a Third Party OIDC provider](JASandOIDCProvider) [related-topics-jazz-authorization-server-landing-page-configure-elm-with-a-third-party-oidc-provider]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

META:FILEATTACHMENT{name="bad_request.png" attachment="bad_request.png"
attr="h" comment="" date="1628229220" path="bad_request.png"
size="321438" user="shubjit" version="1"}
