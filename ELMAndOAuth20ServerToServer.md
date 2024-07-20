META:TOPICINFO{author="shubjit" date="1629467045" format="1.1"
reprev="1.8" version="1.8"}
META:TOPICPARENT{name="JazzAuthorizationServer"}

# ELM and OAuth 2.0 Server to Server communication via Client Credentials Grant DKGRAY Authors: Main.ShubjitNaik Build basis: Engineering Lifecycle Management 7.x [elm-and-oauth-2.0-server-to-server-communication-via-client-credentials-grant-dkgray-authors-main.shubjitnaik-build-basis-engineering-lifecycle-management-7.x]

ENDCOLOR

TOC{title="Page contents"}

When deployed with Jazz Authorization Server (IBM Liberty OIDC feature)
Engineering Lifecycle Management solution supports OAuth 2.0. Refer the
article [ELM and OAuth 2.0](ELMAndOAuth20) to understand how to use
OAuth 2.0 protocol flow with ELM deployed with Jazz Authorization
Server. The article focuses on the context of a user login and then
perform an action on behalf of that user.

In some cases, applications may need an access token to act on behalf of
themselves rather than a user, which is more of server-to-server
communication. The [Client
Credentials](https://oauth.net/2/grant-types/client-credentials/) grant
is used when applications request an access token to access their own
resources, not on behalf of a user. In this case, the client can request
an access token using only its client credentials.

The focus of this article is on using the Client Credentials Grant OAuth
flow with ELM.

## OAuth 2.0 - A Quick Intro

[OAuth 2.0](https://oauth.net/2/) authorization framework enables a
third-party application to obtain limited access to an HTTP service,
either on behalf of a resource owner by orchestrating an approval
interaction between the resource owner and the HTTP service, or by
allowing the third-party application to obtain access on its own behalf.

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
](https://oauth.net/). In this article we will focus on the [Client
Credentials Grant
Type](https://oauth.net/2/grant-types/client-credentials/)

In the next section we will showcase how to register a new client to
Jazz Authorization Server and access ELM Protected resources via the
Client Credentials grant type.

## Accessing ELM Protected Resources via Client Credentials Grant Type

The Client Credentials grant type is used by clients to obtain an access
token outside of the context of a user.

### High Level Authorization Flow

Considering ELM deployed with Jazz Authorization Server, the Access flow
is as following

-   Pre-Req - Register a new Client with Jazz Authorization Server
    -   A functional user to associate with a request made on behalf of
        a client, who has the required access and license assigned
-   Request for Access Token with Client credentials
-   Access ELM Protected Resources via Access Token

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
trusted_uri_prefixes="<https:///>" \\ -P functional_user_id= \\ -P
functional_user_groupIds="JazzAdmins" \\ -P scope="openid profile email
general" \\ -P preauthorized_scope="openid profile email general" \\ -P
response_types="code","token" \\ -P
grant_types="password","authorization_code","client_credentials","refresh_token"
\\ -P introspect_tokens=true

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
    behalf of a client in a client_credentials grant type (Create a
    user, grant access to projects and assign licenses)
-   DONOT change values for `scope`, `preauthorized_scope`,
    `response types` and `grant types`

BR Here is an example command for registering a clientId to be used with
CURL commands \# ./mkclient -a
<https://jas.example.com/oidc/endpoint/jazzop> -u JazzUser:JazzPassword
\\ -P client_name="CURL Client" -P client_id="curlclientId" -P
client_secret="curlclientpassword" \\ -P functional_user_id=curl_user \\
-P functional_user_groupIds="JazzAdmins" \\ -P
redirect_uris="<https://jas.example.com/jazzop>","<https://localhost/jazzop>"
\\ -P
trusted_uri_prefixes="<https://jas.example.com/>","<https://localhost/>"
\\ -P scope="openid profile email general" -P
preauthorized_scope="openid profile email general" \\ -P
response_types="code","token" \\ -P
grant_types="password","authorization_code","client_credentials","refresh_token"
\\ -P introspect_tokens=true

-   You can review the registration details via the URL
    `https://jas.example.com/oidc/endpoint/jazzop/registration`

### Request for Access Token with Client credentials

In this example, we are using a Script (bash) to list out EWM/ETM/ERM
project areas and are using CURL commands. Once the Client is registered
with Jazz Authorization server, we can create a `POST` request to the
Token endpoint URL providing the Client Credentials (ClientID and
ClientSecret) using CURL as follows:

curl -k --location --request POST \\
'<https://jas.example.com/oidc/endpoint/jazzop/token>' \\ --header
'Content-Type: application/x-www-form-urlencoded' \\ --data-urlencode
'grant_type=client_credentials' \\ --data-urlencode
'client_id=curlclientId' \\ --data-urlencode
'client_secret=curlclientpassword' \\ --data-urlencode 'scope=openid
profile email general'

-   `jas.example.com` is your Jazz Authorization server
-   `client_Id`, `client_secret` are the values created earlier while
    registering the client

If the client credentials are valid, JAS will send a response containing
the Access token which is valid for 2 hours by default. A sample
response is shown below:

{"access_token":"nwc5fn9tDtqC2RDlTaG41ygNdAppOTvE2Trw1X4E","token_type":"Bearer","expires_in":7200,"scope":"general
openid profile email"}

Capture the value
`"access_token":"nwc5fn9tDtqC2RDlTaG41ygNdAppOTvE2Trw1X4E"`

### Access ELM Resources with the Access Token

Now that we have an access token using Client Credentials grant, we can
access ELM APIs using this Access Token as a Header on a `GET` request.
Here is a `GET` request with CURL to list ERM Project Areas, replace the
`Bearer` value with the Access Token. BR curl -k --location --request
GET '<https://elm.example.com/rm/process/project-areas>' \\ --header
'Authorization: Bearer nwc5fn9tDtqC2RDlTaG41ygNdAppOTvE2Trw1X4E'

Sample result of the command:

Money That Matters RM The purpose of this project is to specify and
manage the requirements of the JKE Business Recovery Matters project.
<https://elm.example.com/rm/process/project-areas/_F5xhQD-_EeuV6NBd2WfUvQ>
<https://elm.example.com/rm/process/project-areas/_F5xhQD-_EeuV6NBd2WfUvQ/roles>
<https://elm.example.com/rm/process/project-areas/_F5xhQD-_EeuV6NBd2WfUvQ/links>
<https://elm.example.com/rm/process/project-areas/_F5xhQD-_EeuV6NBd2WfUvQ/members>
<https://elm.example.com/rm/process/project-areas/_F5xhQD-_EeuV6NBd2WfUvQ/admins>
<https://elm.example.com/rm/process/project-areas/_F5xhQD-_EeuV6NBd2WfUvQ/team-areas>
<https://elm.example.com/rm/process/project-areas/_F5xhQD-_EeuV6NBd2WfUvQ/project-admins>
<https://elm.example.com/rm/process/project-areas/_F5xhQD-_EeuV6NBd2WfUvQ/read-access-list>
<https://elm.example.com/rm/process/project-areas/_F5xhQD-_EeuV6NBd2WfUvQ/timelines>
false false true Wed, 16 Dec 2020 17:07:19 GMT false
<https://elm.example.com/rm/process/project-areas/_F5xhQD-_EeuV6NBd2WfUvQ/history>
true SINGLE

\*Note: The response only contains the list of Projects that the
Functional User has access to.

##### Related topics: [JazzAuthorizationServer](JazzAuthorizationServer), [ELM and OAuth 2.0](ELMAndOAuth20), [OAuth 2.0](https://oauth.net/2/) [related-topics-jazzauthorizationserver-elm-and-oauth-2.0-oauth-2.0]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)
