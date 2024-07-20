META:TOPICINFO{author="din" date="1700723265" format="1.1"
version="1.18"} META:TOPICPARENT{name="JazzAuthorizationServer"}

# ELM Applications Authentication and Authorization via OAuth 2.0 Workflow DKGRAY Authors: Main.ShubjitNaik, Main.DineshKumar, Main.BharathRao, Main.SudarshanRao [elm-applications-authentication-and-authorization-via-oauth-2.0-workflow-dkgray-authors-main.shubjitnaik-main.dineshkumar-main.bharathrao-main.sudarshanrao]

Build basis: Engineering Lifecycle Management 7.x and higher ENDCOLOR

TOC{title="Page contents"}

[IBM Engineering Lifecycle Management](https://jazz.net/) (ELM)
applications use a number of authentication protocols: JEE container
authentication (Basic and FORM), OAuth 1.0a, OIDC and OAuth 2.0
(embedded in OpenID Connect/OIDC with extensions for the Jazz Security
Architecture/JSA profile), Kerberos/SPNEGO, etc.

There are two forms of application-to-application authentication
implemented by Jazz applications (ELM), [OAuth
1.0a](http://tools.ietf.org/html/rfc5849/)and [OpenID
Connect.](https://openid.net/connect/)

Up until the 6.0 software release, OAuth 1.0a was the only type of
inter-application authentication supported. It requires pair-wise
relationships between communicating applications applications that are
registered as "friends" of each other can send requests to each other
that will be authenticated using OAuth 1.0a. For bi-directional
communications, each application must be a friend of each other. The
friending application is allocated a key and secret which it uses to
authenticate with the friend application; they are the equivalent of a
username and password for the application itself.

Starting CLM version 6.0 [Jazz Authorization
Server](https://jazz.net/wiki/bin/view/Deployment/AboutJazzAuthorizationServer/)
was introduced and when applications are configured with Jazz Security
Architecture SSO enabled, they can use OpenID Connect to authenticate
with each other. OpenID Connect is a simple identity protocol and open
standard that is built on top of the OAuth 2.0 protocol that enables
client applications to rely on authentication that is performed by an
OpenID Connect Provider to verify the identity of a user.

Review the Jazz Security Architecture on the article
<https://jazz.net/library/article/75>

When deployed with Jazz Authorization Server (IBM Liberty OIDC feature)
ELM supports OAuth 2.0. The focus of this article is on accessing ELM
protected resources via the OAuth2.0 workflow.

## OAuth 2.0 - A Quick Intro

OAuth 2.0 authorization framework enables a third-party application to
obtain limited access to an HTTP service, either on behalf of a resource
owner by orchestrating an approval interaction between the resource
owner and the HTTP service, or by allowing the third-party application
to obtain access on its own behalf.

**OAuth 2.0 Protocol Flow** BR BR

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
specification defines four grant types

-   [Authorization
    code](https://tools.ietf.org/html/rfc6749#section-4.1)
-   [Implicit](https://tools.ietf.org/html/rfc6749#section-4.2,)
-   [Password](https://tools.ietf.org/html/rfc6749#section-4.3)
-   [Client
    credentials](https://tools.ietf.org/html/rfc6749#section-4.4)

For further details on the workflow on OAuth2.0 and different grant
types please review the OAuth 2.0 Framework at [OAuth 2.0
](https://oauth.net/).

In the next section we introduce how to register a new Client in Jazz
Authorization Server and Access ELM Protected resources via the
Authorization Code grant type.

## Accessing ELM Protected Resources via Authorization Code Grant Type

The authorization code grant type is most commonly used because it is
optimized for server-side applications and allows confidential and
public clients to exchange an authorization code for an access token.

### High Level Authorization Flow

OAuth 2.0 Framework Reference - [Authorization Code
Grant](https://tools.ietf.org/html/rfc6749#section-4.1)

Considering ELM deployed with Jazz Authorization Sevrer, the Resource
Owner is ELM and the authorization server is Jazz Authorization Server.
The Access flow is as following

1 Pre-Req - Register a new Client with Jazz Authorization Server 2
Authentication with Jazz Authorization Server 3 Request for
Authorization Code 4 Request for Access Token with the Authorization
Code

-   (Optional) Validate the Access Token by retrieving User credentials
    5 Access ELM Protected Resources via Access Token

### Application/Client Registration

Before using OAuth with your application, you must register your
application with Jazz Authorization Server. During registration you
would need to provide Application Name, Scope, Redirect URI or Callback
URL. The redirect URI is where the service will redirect the user after
they authorize (or deny) your application, and therefore the part of
your application that will handle authorization codes or access tokens.
Once your application is registered, the service will issue client
credentials in the form of a client identifier and a client secret.

In this example, we are using a Script to list out EWM/ERM project areas
and are using CURL commands. We will create our own ClientID and
ClientSecret and register a new client with JAS providing all the
details as follows \# cd /cli \# ./mkclient -a
<https:///oidc/endpoint/jazzop> \\ -u : \\ -P client_name="" \\ -P
client_id="" -P client_secret="" \\ -P
redirect_uris="<https:///auth/sso>","<https:///>" \\ -P
trusted_uri_prefixes="<https:///>" \\ -P scope="openid profile email
general" \\ -P functional_user_id="" \\ -P
functional_user_groupIds="JazzAdmins" \\ -P preauthorized_scope="openid
profile email general" \\ -P response_types="code","token","id_token
token" \\ -P
grant_types="authorization_code","client_credentials","implicit","refresh_token","<urn:ietf:params:oauth:grant-type:jwt-bearer>"

In the above example replace the following variables

-   JASURL - The Initial URL (and Port if present) to your Jazz
    Authorization Server
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
grant_types="authorization_code","client_credentials","implicit","refresh_token","<urn:ietf:params:oauth:grant-type:jwt-bearer>"
\\ -P response_types="code","token","id_token token"

You can review the registration details via the URL
`https://jas.example.com/oidc/endpoint/jazzop/registration`

### Authenticate to Jazz Authorization Server

In this example, we are using a Script (bash) to list out EWM/ERM
project areas and are using CURL commands. To generate cookies and
headers we make a `POST` request to /jazzop/j_security_check URL with a
valid ELM User

You can declare USER,PASSWORD,COOKIES and HEADERS as variables to begin
with:BR `# USER=JazzUser` BR `# PASSWD=JazzUserPassword` BR
`# COOKIES=cookies.txt` BR `# HEADERS=headers.txt` BR

Following is the command that needs to be run, You will receive a
`HTTP/1.1 302 Found` response with jazzop_sso_cookie value which would
be used as the Authenticated session for JazzUser. \# curl -X POST -d
"j_username=\$USER" -d "j_password=\$PASSWD" -k -c \$COOKIES -b
\$COOKIES -D \$HEADERS "<https://%5BJASURL%5D/jazzop/j_security_check>"

-   Replace `[JASURL]` with the Jazz Authorization Server URL, example
    `jas.example.com`

Sample headers.txt file created by running the CURL command above.

HTTP/1.1 302 Found Date: Mon, 30 Nov 2020 12:07:20 GMT Server:
IBM_HTTP_Server X-Powered-By: Servlet/3.0 Location:
<https://jas.example.com/jazzop/> Set-Cookie:
jazzop_sso_cookie=UxSR6K3lAKkOF/0cExEYjnVDTJiAlnyETZnUI4wqsoY3dla/RFXkut03WbzPLqLfimCSHsPKhHHCoDe0vP75uC/kznP1azyexmhvnOKWed7qmHRCiBHZLpkR1qnZ51JsJTrn8zCxtHxZaRWMEGH3N9s0JguH6HF0g8ASfILx68g/tEjErbGDf4S+kTGswP4jhdpn2JeNvtG8h4mKa2nPGT1aDjktNcAd0mdoHZkHq88FvDQ3SZmbSJgIgs+7ln5LyeEVA1ey+n/1yD5PKUxz2obmadjoa2lz0qqNBAdbtPB1288bm3+T4apKcv0THgP2lnFUqw496DlZcji+z4Qtc5+DrFfuFpCLYhBr899qNvsFXJPclp2IwnL2aPYibgKR;
Path=/ Set-Cookie: WASReqURL=""; Expires=Thu, 01 Dec 1994 16:00:00 GMT;
Path=/ Expires: Thu, 01 Dec 1994 16:00:00 GMT Cache-Control:
no-cache="set-cookie, set-cookie2" Content-Length: 0 Content-Language:
en-US

### Request for Authorization Code

To continue with the flow and request an authorization code , construct
a URL similar the following (Note we are requesting for
response_type=code via the Authorization Endpoint)
<https://jas.example.com/oidc/endpoint/jazzop/authorize?response_type=code&client_id=curlclientId&client_secret=curlclientpassword&redirect_uri=https3A2F2Fjas.example.com2Fjazzop>
&scope=openid20profile20email20general

-   `jas.example.com` is your Jazz Authorization server
-   `client_Id`, `client_secret`, `redirect_uri` and `scope` are the
    ones created earlier during registering a client

Once you have the URL constructed make a `GET` request to the URL
following the CURL command below including the `HEADERS` and `COOKIES`
from previous step curl -k -b \$COOKIES -c \$COOKIES -D \$HEADERS -X GET
\\
"<https://jas.example.com/oidc/endpoint/jazzop/authorize?response_type=code&client_id=curlclientId&client_secret=curlclientpassword&redirect_uri=https3A2F2Fjas.example.com2Fjazzop&scope=openid20profile20email20general>"

If the request is valid it redirects to the application redirect URI,
along with an authorization code generated by the authorization server.
This code is relatively short-lived depending on the OAuth service. The
`Location` value in `headers.txt` is updated with redirect_uri specified
adding a state and code to the query string. Here is a sample output of
headers.txt

HTTP/1.1 302 Found Date: Mon, 30 Nov 2020 13:14:48 GMT Server:
IBM_HTTP_Server X-Powered-By: Servlet/3.0 Pragma: no-cache Location:
<https://jas.example.com/jazzop?session_state=QQqRY8PLlilADmJZz8S6ZiU8NTbxY2B66THdCuDxQU8U3D.2201081ba070b&code=cb1wdJdAkoVrreyOY2T4B4r3XmHxvc>
Set-Cookie: oidc_bsc=PbAX7k8cpEKNCJhFvD6BrarEufBPcIiKF7I099IyG+M=;
Path=/ Expires: Thu, 01 Dec 1994 16:00:00 GMT Cache-Control: no-store,
no-cache=set-cookie Content-Length: 0 Content-Language: en-US

Capture the value `code=cb1wdJdAkoVrreyOY2T4B4r3XmHxvc` OR Run the
following command to extract the authorization code: cat headers.txt \|
grep Location \| cut -d '=' -f 3 Result:
`cb1wdJdAkoVrreyOY2T4B4r3XmHxvc`

### Request for Access Token

Now we will exchange the Authorization Code for an Access Token. To
request for an Access Token using the Authroziaton code from previous
setup , we can make a `POST` request to the Token endpoint URL using
CURL as shown below:

curl -k --location --request POST \\
'<https://jas.example.com/oidc/endpoint/jazzop/token>' \\ --header
'Content-Type: application/x-www-form-urlencoded' \\ --data-urlencode
'grant_type=authorization_code' \\ --data-urlencode 'code=' \\
--data-urlencode 'redirect_uri=<https://jas.example.com/jazzop>' \\
--data-urlencode 'client_id=curlclientId' \\ --data-urlencode
'client_secret=curlclientpassword'

\* `jas.example.com` is your Jazz Authorization server \* `code` Is the
Authorization code generated from the previous step \* `client_Id`,
`client_secret`, `redirect_uri` and `scope` are the ones created earlier
during registering a client

If the authorization is valid, JAS will send a response containing the
access token (and a refresh token) which is valid for 2 hours by
default. The entire response will look something like this:
{"access_token":"VQQSVldMW4cUtslwvKdCvC2eYKkq384BCxwsnFqV","token_type":"Bearer","expires_in":7200,"scope":"general
openid profile
email","refresh_token":"0ORqqbs0EuArYG9nLuFrQnpXxr659G5pSrIsyacDqLvhrGAiK8","id_token":"eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJzaHViaml0IiwiYXRfaGFzaCI6Il9WSEZZNU9wM3lmRmxzcGNpU0ppRVEiLCJyZWFsbU5hbWUiOiJlbG1jbHVzdGVyczEuZnlyZS5pYm0uY29tOjEwMzg5IiwidW5pcXVlU2VjdXJpdHlOYW1lIjoidWlkPXNodWJqaXQsb3U9VXNlcnMsZGM9bGRhcDMsZGM9Y29tIiwiZ3JvdXBJZHMiOlsiY249SmF6ekFkbWluczMsb3U9R3JvdXBzLGRjPWxkYXAzLGRjPWNvbSIsImNuPUphenpQcm9qZWN0QWRtaW5zMyxvdT1Hcm91cHMsZGM9bGRhcDMsZGM9Y29tIiwiY249SmF6elVzZXJzMyxvdT1Hcm91cHMsZGM9bGRhcDMsZGM9Y29tIl0sImlzcyI6Imh0dHBzOi8vZWxtY2x1c3RlcnMxLmZ5cmUuaWJtLmNvbTo0NDMvb2lkYy9lbmRwb2ludC9qYXp6b3AiLCJhdWQiOiJjdXJsY2xpZW50SWQiLCJleHAiOjE2MDY3NTAyMz

Capture the value
`"access_token":"VQQSVldMW4cUtslwvKdCvC2eYKkq384BCxwsnFqV"`

The Authorization Code flow is complete! We now have the `Access Token`
which can be used to make ELM API requests.

### Access ELM Protected Resources with Access Token

Note: this is the first time we would be accessing an ELM based URL

Now that we have an access token for the User `JazzUser` who has access
to ELM resources, we would be able to retrieve protected resources using
this Access Token as a Header on a `GET` request. Here is a `GET`
request with CURL to list ERM Project Areas using CURL, replace the
`Bearer` value with the Access Token. BR curl -k --location --request
GET '<https://elm.example.com/rm/process/project-areas>' \\ --header
'Authorization: Bearer VQQSVldMW4cUtslwvKdCvC2eYKkq384BCxwsnFqV'

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
false false true Wed, 25 Nov 2020 15:21:11 GMT false
<https://elm.example.com/rm/process/project-areas/_w-sawC8xEeu-5_iBQYQ_UQ/history>
true SINGLE

### List User Info from Access Token

We can send a `GET` request to the Userinfo endpoint on JAS to retrieve
details of the user to whom the Access Token belongs to. Replace
`Bearer` value with the Access Token curl -k --location --request GET
'<https://jas.example.com/oidc/endpoint/jazzop/userinfo>' \\ --header
'Authorization: Bearer VQQSVldMW4cUtslwvKdCvC2eYKkq384BCxwsnFqV'

Sample result of the command:

{"sub":"JazzUser","groupIds":\["cn=JazzUsers,ou=Groups,dc=example,dc=com"\],"iss":"[https:\\\\jas.example.com\\oidc\\endpoint\\jazzop](https:\/\/jas.example.com\/oidc\/endpoint\/jazzop)","email":"<jazzuser@jke.net>"}

## JAS with SAML IDP Or Third Party OIDC Providers

When JAS is further configured to delegate authentication to either a
SAML IDP or a Third Party OIDC Server the OAuth2.0 flow mentioned in
this article is `NOT Supported`.

Starting version 7.0.2 ELM and JAS when configured with a SAML IDP or
another OIDC Provider, Non-Web clients can work with [Liberty
Application
Passwords.](https://openliberty.io/blog/2019/09/13/microprofile-reactive-messaging-19009.html#oidc)
The Liberty application password feature is a way to circumvent the
limitation by using a web browser to handle an identity provider's
authentication scheme and producing a relatively long-lived token that
can then be used by the native client (non-browser) in a simpler
protocol that does not depend on the client being a web browser.

The OAuth 2.0 Password grant type can be used with Application passwords
to generate an access token from JAS, refer this Article [OAuth2.0
Access flow with ELM Configured with Third Party OIDC
Provider](ELMAndOAuth20WithOIDCProvider)

##### Related topics: [JazzAuthorizationServer](JazzAuthorizationServer), [OAuth 2.0](https://oauth.net/2/) [related-topics-jazzauthorizationserver-oauth-2.0]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="oauth20protocolflow.jpg"
attachment="oauth20protocolflow.jpg" attr="" comment="Source
<https://oauth.net/2/>" date="1606477360" path="oauth20protocolflow.jpg"
size="60748" user="shubjit" version="1"}
