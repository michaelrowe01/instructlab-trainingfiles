META:TOPICINFO{author="shubjit" date="1632379970" format="1.1"
version="1.19"} META:TOPICPARENT{name="JazzAuthorizationServer"}

# OAuth2.0 Access flow on ELM Configured with a SAML IDP or OIDC Provider DKGRAY Authors: Main.ShubjitNaik Build basis: Engineering Lifecycle Management Solution 7.0.2 and Higher [oauth2.0-access-flow-on-elm-configured-with-a-saml-idp-or-oidc-provider-dkgray-authors-main.shubjitnaik-build-basis-engineering-lifecycle-management-solution-7.0.2-and-higher]

ENDCOLOR

TOC{title="Page contents"}

When deployed with Jazz Authorization Server (IBM Liberty OIDC feature)
Engineering Lifecycle Management solution supports OAuth 2.0. Refer the
article [ELM and OAuth 2.0](ELMAndOAuth20) to understand how to use
OAuth2.0 protocol flow with ELM deployed with Jazz Authorization Server.

You can further configure the Jazz Authorization Server to delegate the
user authentication to your standard, corporate [SAML Identity
Provider](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.2/com.ibm.jazz.install.doc/topics/t_jsasso_jas_user_mgmt_saml.html)or
[OIDC Provider](JASandOIDCProvider).

Starting ELM and JAS version 7.0.2 when configured with a SAML IDP or
another OIDC Provider, Non-Web clients can work with [Liberty
Application Passwords.](EnableJASAppPasswords) The Liberty application
password feature is a way to circumvent the limitation by using a web
browser to handle an identity provider's authentication scheme and
producing a relatively long-lived token that can then be used by the
native client (non-browser) in a simpler protocol that does not depend
on the client being a web browser. The Application Passwords are
supported only when JAS is delegating authentication further to a SAML
IDP or an OIDC Provider. This feature also allows generating long-lived
app token that can be used as an Access token.

The focus of this article is on working with application passwords and
application tokens in an OAuth2.0 protocol flow to access ELM Protected
resources.

## OAuth 2.0 - A Quick Intro

OAuth 2.0 authorization framework enables a third-party application to
obtain limited access to an HTTP service, either on behalf of a resource
owner by orchestrating an approval interaction between the resource
owner and the HTTP service, or by allowing the third-party application
to obtain access on its own behalf.

[Access tokens ](https://tools.ietf.org/html/rfc6749#section-1.4)are
credentials used to access protected resources. An access token is a
string representing an authorization issued to the client. The string is
usually opaque to the client. Tokens represent specific scopes and
durations of access, granted by the resource owner, and enforced by the
resource server and authorization server.

An [authorization grant
](https://tools.ietf.org/html/rfc6749#section-1.3)is a credential
representing the resource owner's authorization (to access its protected
resources) used by the client to obtain an access token. This
specification defines four grant types and for further details on the
grant types review the OAuth 2.0 Framework at [OAuth 2.0
](https://oauth.net/). In this article we will focus on the
[Password](https://tools.ietf.org/html/rfc6749#section-4.3)Grant Type.

In the next section we introduce how to register a new client in Jazz
Authorization Server which is configured with a Third Party OIDC
Provider and access ELM Protected resources via the Password grant type.

## Configuring Application Passwords in JAS

A pre-requisite is to configure application passwords with ELM and JAS.
The instructions are covered in the following wiki Article

-   [Enable Application Passwords for Native
    Clients](https://jazz.net/wiki/bin/view/Deployment/EnableJASAppPasswords)

## Accessing ELM Protected Resources via Password Grant Type

The resource owner password credentials grant type is suitable in cases
where the resource owner has a trust relationship with the client. Since
application passwords are enabled on the Jazz Authorization Server the
regular LDAP password will not work with this grant type.

### High Level Authorization Flow

Considering ELM deployed with Jazz Authorization Server which is
delegating Authentication to a another OIDC Provider. The Access flow is
as following

-   Pre-Req - Generate an app password for the User
-   Pre-Req - Register a new Client with Jazz Authorization Server
-   Request for Access Token using app password
    -   (Optional) Validate the Access Token by retrieving User
        credentials
-   Access ELM Protected Resources via Access Token

### Generate app password for the user

Once JAS is configured for Application passwords, users will be able to
generate app passwords for their userId via the URL
`https://[JASURL]/oidc/endpoint/jazzop/personalTokenManagement`. We will
generate an application password for the userId JazzUser and use it in
our example in the next step. \* Click on Add New, Select app-password
and click Generate

-   UserId : `JazzUser`
-   App Password : `u5RFiMZzrWJMCHtzf69DELLbF3Wc7h3V7okOcnNozF`

The application password is valid for 90 days by default. You can modify
the App password Lifetime by adding the parameter
[appPasswordLifetime](https://www.ibm.com/support/knowledgecenter/SSAW57_liberty/com.ibm.websphere.liberty.autogen.nd.doc/ae/rwlp_config_oauthProvider.html)

### Register Client with Jazz Authorization Server

Before using OAuth with your application, you must register your
application with Jazz Authorization Server. During registration you
would need to provide Application Name, Scope, Redirect URI or Callback
URL and Grant types. In this example, we are using a Script to list out
EWM/ERM project areas and are using CURL commands. We will register a
client with JAS mentioning ClientID, ClientSecret and other details as
follows

\# cd /cli \# ./mkclient -a
<https://jas.example.com/oidc/endpoint/jazzop> \\ -u : \\ -P
client_name="" \\ -P client_id="" -P client_secret="" \\ -P
redirect_uris="<https:///auth/sso>","<https:///>" \\ -P
trusted_uri_prefixes="<https:///>" \\ -P scope="openid profile email
general" \\ -P functional_user_id="" \\ -P
functional_user_groupIds="JazzAdmins" \\ -P preauthorized_scope="openid
profile email general" \\ -P response_types="code","token","id_token
token" \\ -P
grant_types="password","authorization_code","client_credentials","implicit","refresh_token","<urn:ietf:params:oauth:grant-type:jwt-bearer>"

In the above example replace the following variables

-   `jas.example.com` - The URL to your Jazz Authorization Server
-   JAS_ADMIN and PASSWORD - Jazz Authorization Server Administrator
    User and password
-   CLIENTNAME - Name to uniquely identify your Client
-   CLIENT_ID and CLIENT_SECRET (You can create your own)
-   Redirect URI Application Redirect URIs
-   Trusted URI - Trusted URIs of Application acessing Jazz
    Authorization Server
-   FUNCTIONAL USER - The user ID to associate with a request made on
    behalf of a client (Create a user, grant access to projects and
    assign licenses)
-   DONOT change values for `scope`, `preauthorized_scope`,
    `response types` and `grant types`

BR Here is an example command for registering a clientId to be used with
CURL commands \# ./mkclient -a
<https://jas.example.com/oidc/endpoint/jazzop> -u JazzUser:JazzPassword
\\ -P client_name="CURL Client" -P client_id="curlclientId" -P
client_secret="curlclientpassword" \\ -P
redirect_uris="<https://jas.example.com/jazzop>","<https://localhost/jazzop>"
\\ -P
trusted_uri_prefixes="<https://jas.example.com/>","<https://localhost/>"
\\ -P functional_user_id="JazzUser" \\ -P
functional_user_groupIds="JazzAdmins" \\ -P scope="openid profile email
general" -P preauthorized_scope="openid profile email general" \\ -P
response_types="code","token","id_token token" \\ -P
grant_types="password","authorization_code","client_credentials","implicit","refresh_token","<urn:ietf:params:oauth:grant-type:jwt-bearer>"

-   You can review the registration details via the URL
    `https://jas.example.com/oidc/endpoint/jazzop/registration`

#### Update appPasswordAllowed to true

There are two variables `appPasswordAllowed` and `appTokenAllowed` that
needs to be set to `true` as during registration the `mkclient` command
does not accept these parameters. We will use the following commands to
export and import the registration details:

-   Export the client metadata, the Client Id in our example above is
    `curlclientId` \# cd /cli

\# ./lsclient -a <https://jas.example.com/oidc/endpoint/jazzop> -u
\[UserName\]:\[Password\] curlclientId \> curl.json

-   Edit the exported file curl.json and change `appPasswordAllowed` and
    `appTokenAllowed` values from: "appPasswordAllowed" : false,

"appTokenAllowed" : false,

-   TO "appPasswordAllowed" : true,

"appTokenAllowed" : true,

-   Import the updated metadata to JAS \# ./ldclient -a
    <https://jas.example.com/oidc/endpoint/jazzop> -u
    \[UserName\]:\[Password\] curl.json

### Request for Access Token using app password

In this example, we are using a Script (bash) to list out EWM/ERM
project areas and are using CURL commands. Once the user has generated
an app-password, along with the ClientID and ClientSecret we can make a
`POST` request to the Token endpoint URL using CURL as follows:

curl -k --location --request POST \\
'<https://jas.example.com/oidc/endpoint/jazzop/token>' \\ --header
'Content-Type: application/x-www-form-urlencoded' \\ --data-urlencode
'grant_type=password' \\ --data-urlencode 'client_id=curlclientId'
--data-urlencode 'client_secret=curlclientpassword' \\ --data-urlencode
'scope=openid profile email general' \\ --data-urlencode
'username=JazzUser' \\ --data-urlencode
'password=u5RFiMZzrWJMCHtzf69DELLbF3Wc7h3V7okOcnNozF'

-   `jas.example.com` is your Jazz Authorization server
-   `password` Is the **app password** generated by JazzUser earlier
-   `client_Id`, `client_secret` are the ones created earlier during
    registering a client

If the authentication is valid, JAS will send a response containing the
Access token (and a refresh token) which is valid for 2 hours by
default. The entire response will look something like this:

{"access_token":"8zOuhLoiChkDMVVay1WNwVOracfXZzp8ecnZtRvs","token_type":"Bearer","expires_in":7200,"scope":"general
openid profile
email","refresh_token":"g87QlO9FKendCs9k46eF0W1MuW2jZaeV8MedUR0fhIVqyRKuua"}

Capture the value
`"access_token":"8zOuhLoiChkDMVVay1WNwVOracfXZzp8ecnZtRvs"`

### Access ELM Protected Resources with Access Token

`Note`: This is the first time we would be accessing an ELM based URL

Now that we have an access token for the User `JazzUser` who has access
to ELM resources, we would be able to retrieve protected resources using
this Access Token as a Header on a `GET` request. Here is a `GET`
request with CURL to list ERM Project Areas, replace the `Bearer` value
with the Access Token. BR curl -k --location --request GET
'<https://elm.example.com/rm/process/project-areas>' \\ --header
'Authorization: Bearer 8zOuhLoiChkDMVVay1WNwVOracfXZzp8ecnZtRvs'

Sample result of the command:

JKE (Requirements Management) The purpose of this project is to specify
and manage the requirements of the JKE Business Recovery Matters
project.
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/roles>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/links>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/members>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/admins>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/team-areas>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/project-admins>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/read-access-list>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/timelines>
false false true Wed, 03 Dec 2020 15:21:11 GMT false
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/history>
true SINGLE

### List User Info from Access Token

We can send a `GET` request to the Userinfo endpoint on JAS to retrieve
details of the user to whom the Access Token belongs to. Replace
`Bearer` value with the Access Token curl -k --location --request GET
'<https://jas.example.com/oidc/endpoint/jazzop/userinfo>' \\ --header
'Authorization: Bearer 8zOuhLoiChkDMVVay1WNwVOracfXZzp8ecnZtRvs'

Sample result of the command:

{"sub":"JazzUser","groupIds":\["cn=JazzUsers,ou=Groups,dc=example,dc=com"\],"iss":"[https:\\\\jas.example.com\\oidc\\endpoint\\jazzop](https:\/\/jas.example.com\/oidc\/endpoint\/jazzop)","email":"<jazzuser@jke.net>"}

## Accessing ELM Protected Resources using App-Token

Once JAS is configured for Application passwords, users will be able to
generate `app tokens` for a specific `userId` via the URL
`https://[JASURL]/oidc/endpoint/jazzop/personalTokenManagement`

\* Click on Add New and select app-token and Generate

**Limitations**

-   app-tokens are locked to the first application it is used against,
    example if the token is used to access protected resources of ERM,
    it cannot be used to access APIs of EWM, ETM etc.
-   Each ELM application needs a different app-token

**Advantage**

-   While Access Tokens generated by different OAuth2.0 types are valid
    for 2 hours similar to a user session, app-token are long lived and
    can be configured for custom lifetime, default being 90 days. You
    can modify the Token Lifetime by adding the parameter
    [appTokenLifetime](https://www.ibm.com/support/knowledgecenter/SSAW57_liberty/com.ibm.websphere.liberty.autogen.nd.doc/ae/rwlp_config_oauthProvider.html)

### Use App Token to access ELM Application Protected Resources

Now that we have an app-token for a user who has access to ELM
resources, we would be able to retrieve protected resources using this
as an Access Token on a `GET` request. Here is a `GET` request with CURL
to list ERM Project Areas, replace the `Bearer` value with the App
Token. BR curl -k --location --request GET
'<https://elm.example.com/rm/process/project-areas>' \\ --header
'Authorization: Bearer YuZ5H9QtrCv2HBgqlz6UifZ4ZGXA8Wc6IXFZvkHoVf'

Sample result of the command:

JKE (Requirements Management) The purpose of this project is to specify
and manage the requirements of the JKE Business Recovery Matters
project.
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/roles>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/links>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/members>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/admins>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/team-areas>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/project-admins>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/read-access-list>
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/timelines>
false false true Wed, 03 Dec 2020 15:21:11 GMT false
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/history>
true SINGLE

`Note: This app token used to list ERM project areas, can only be used with ERM application APIS going forward and will not work for other applications. If you intend to generate a single Access token for all ELM Applications similar to an SSO, use the Password Grant type OAUth2.0 access flow mentioned in the previous section`

##### Related topics: [JazzAuthorizationServer](JazzAuthorizationServer), [ELM and OAuth 2.0](ELMAndOAuth20), [OAuth 2.0](https://oauth.net/2/) [related-topics-jazzauthorizationserver-elm-and-oauth-2.0-oauth-2.0]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

META:FILEATTACHMENT{name="app-token.png" attachment="app-token.png"
attr="h" comment="" date="1611034979" path="app-token.png" size="84838"
user="shubjit" version="1"} META:FILEATTACHMENT{name="app-password.png"
attachment="app-password.png" attr="h" comment="" date="1611035936"
path="app-password.png" size="76370" user="shubjit" version="1"}
