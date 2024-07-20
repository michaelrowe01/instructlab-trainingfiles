META:TOPICINFO{author="sbagot" date="1432743470" format="1.1"
version="1.9"}
META:TOPICPARENT{name="IntegrationsTroubleshootingSmartCard"}

# How to Read Debug logs of Eclipse Client and Team Concert server for Smart Card issues? DKGRAY Authors: Main.ZeeshanChoudhry Build basis: IBM Rational Team Concert 4.0.3 and later [how-to-read-debug-logs-of-eclipse-client-and-team-concert-server-for-smart-card-issues-dkgray-authors-main.zeeshanchoudhry-build-basis-ibm-rational-team-concert-4.0.3-and-later]

ENDCOLOR

TOC{title="Page contents"}

This article explains you how you interpret the log files of IBM
Rational Team Concert Eclipse client and IBM Rational Team Concert
server that have [Debug
Tracing](IntegrationsTroubleshootingSmartCardDebug) enabled.

## How to Navigate in Eclipse log?

You will notice there will be a lot of information in the .log file of
eclipse when you have enabled the [Debug
Tracing](IntegrationsTroubleshootingSmartCardDebug)

For instance this trace tells you what Key Store client is using at the
moment:

ENTRY org.apache.commons.httpclient.HttpClient 0 500 2014-10-20
08:28:06.380 MESSAGE IBMJCE 1.2: IBMJCE Provider implements the
following: HMAC-SHA1, MD2, MD5, MARS, SHA, MD2withRSA, MD5withRSA,
SHA1withRSA, RSA, Key factory : DiffieHellman, DSA, RSA Secret key
factory : Blowfish, AES, DES, TripleDES, Mars, RC2, RC4, Seal, ARCFOUR
PKCS5Key, PBKDF1 and PBKDF2(PKCS5Derived Key). Certificate : X.509
Secure random : IBMSecureRandom Key store : JCEKS, PKCS12KS (PKCS12),
JKS

And this tells you they have enabled the required settings for the Smart
Card log-in to work in java.security file which is

security.provider.1=com.ibm.security.capi.IBMCAC

ENTRY org.apache.commons.httpclient.HttpClient 0 500 2014-10-20
08:28:06.378 MESSAGE IBMCAC 1.0: IBM Crypto API for CAC JCE provider

While trying to debug the problem with Smart Card log-in, it is imported
to know what information we are sending to the server and what
information we get back from the server. To find that out in the log we
can extract the relevant part of the .log with two search strings.

-   **\>\>**
-   **\<\<**

When you open the .log file in the notepad++ you can enter the Search
string "\>\>" and click on "Find All in Current Document"

This will show you all the information we are sending to the server.

Example:

Line 657: MESSAGE \>\> "GET
/ccm/versionCompatibility?clientVersion=4.0.3 HTTP/1.1\[\r\]\[\n\]" Line
696: MESSAGE \>\> "http.useragent:
com.ibm.team.repository.transport.client.RestClientConnectionBase\[\r\]\[\n\]"
Line 708: MESSAGE \>\> "X-Requested-With:
com.ibm.team.repository.transport.client.RestClientConnectionBase\[\r\]\[\n\]"
Line 720: MESSAGE \>\> "Accept: text/xml\[\r\]\[\n\]" Line 732: MESSAGE
\>\> "Accept-Charset: UTF-8\[\r\]\[\n\]" Line 744: MESSAGE \>\>
"Accept-Language: en-US\[\r\]\[\n\]" Line 756: MESSAGE \>\>
"X-com-ibm-team-userid: \[\r\]\[\n\]" Line 768: MESSAGE \>\>
"Authorization: jauth user_token=\_jCfAMFhUEeSXYZuMs1YgCQ\[\r\]\[\n\]"
Line 780: MESSAGE \>\> "X-com-ibm-team-configuration-versions:
com.ibm.team.jazz.foundation=4.0.3,com.ibm.team.rtc=4.0.3\[\r\]\[\n\]"
Line 792: MESSAGE \>\> "User-Agent: Jakarta
Commons-HttpClient/3.1\[\r\]\[\n\]" Line 804: MESSAGE \>\> "Host:
HOST.DOMAIN\[\r\]\[\n\]" Line 825: MESSAGE \>\> "\[\r\]\[\n\]"

As you can see above there is a [JAuth Access
Token](https://jazz.net/wiki/bin/view/Main/JAuthOverview) used:
**\_jCfAMFhUEeSXYZuMs1YgCQ** for authentication request for the user
associated with this generated Token . This request is using a server
"Host: HOST.DOMAIN\[\r\]\[\n\]". The request is ending with
"\[\r\]\[\n\]" at line 825.

Now we want to know what was the response for this request client made
so we search now with string "\<\<"

Line 846: MESSAGE \<\< "HTTP/1.1 200 OK\[\r\]\[\n\]" Line 849: MESSAGE
\<\< "HTTP/1.1 200 OK\[\r\]\[\n\]" Line 867: MESSAGE \<\< "Date: Mon, 20
Oct 2014 08:25:08 GMT\[\r\]\[\n\]" Line 876: MESSAGE \<\< "X-Powered-By:
Servlet/3.0\[\r\]\[\n\]" Line 885: MESSAGE \<\< "Transfer-Encoding:
chunked\[\r\]\[\n\]" Line 894: MESSAGE \<\< "Content-Type:
text/json;charset=UTF-8\[\]\[\n\]" Line 903: MESSAGE \<\<
"Content-Language: en-US\[\r\]\[\n\]" Line 912: MESSAGE \<\<
"\[\r\]\[\n\]"

As you can see for the GET request above we have received a response 200
which is an OK transaction with time stamp as well. So the transaction
request for this user was completed with status code 200 for checking
the authentication. This is in normal conditions a token is sent to
server for authentication and server then sends a response to it since
the user [JAuth Access
Token](https://jazz.net/wiki/bin/view/Main/JAuthOverview) for
certificate is found and user continues to work on client.

In some cases you might see different status code like 302 or 401
depending on the nature of the problem. From which you can identify if
the server is not responding correctly to the request that was sent from
the client. Hence you would want to look at the server logs too.

**Note**: If you get a status **"302 Found"** in the response from
server then check what was the request that was sent to the server? Is
it trying to find a URL to get a token issued to certificate? Was there
a 401 code received just before the 302 Found. If yes what was the
response body of 401?

Below you will find the request to find the URL /ccm/jauth-issue-token
on the server was sent so client can present the authentication
challenge and the status code **302 Found** is showing that the URL is
found which is <https://HOST.PORT/ccm/jauth-issue-token> with a redirect
path which is
<https://HOST.PORT/ccm/authenticated/identity?redirectPath=2Fccm2Fjauth-issue-token>
which will be used later to generate a GET request to get an [JAuth
Access Token](https://jazz.net/wiki/bin/view/Main/JAuthOverview) issued
for the authentication for the user certificate so user can log-in.

MESSAGE \>\> "POST /ccm/jauth-issue-token HTTP/1.1\[\r\]\[\n\]" MESSAGE
\>\> "X-com-ibm-team-userid: \[\r\]\[\n\]" MESSAGE \>\>
"X-com-ibm-team-configuration-versions:
com.ibm.team.jazz.foundation=4.0.3,com.ibm.team.rtc=4.0.3\[\r\]\[\n\]"
MESSAGE \>\> "User-Agent: Jakarta Commons-HttpClient/3.1\[\r\]\[\n\]"
MESSAGE \>\> "Host: HOST.DOMAIN\[\r\]\[\n\]" MESSAGE \>\>
"Content-Length: 0\[\r\]\[\n\]" MESSAGE \>\> "\[\r\]\[\n\]"

MESSAGE \<\< "HTTP/1.1 302 Found\[\r\]\[\n\]" MESSAGE \<\< "HTTP/1.1 302
Found\[\r\]\[\n\]" MESSAGE \<\< "Date: Thu, 09 Oct 2014 14:27:19
GMT\[\r\]\[\n\]" MESSAGE \<\< "X-Powered-By: Servlet/3.0\[\r\]\[\n\]"
MESSAGE \<\< "X-com-ibm-team-repository-web-auth-msg:
authrequired\[\r\]\[\n\]" MESSAGE \<\< "Location:
[https://HOST.PORT/ccm/authenticated/identity?redirectPath=2Fccm2Fjauth-issue-token\[\r\]\[\n\]](https://HOST.PORT/ccm/authenticated/identity?redirectPath=2Fccm2Fjauth-issue-token%5B\r%5D%5B\n%5D)"
MESSAGE \<\< "Content-Length: 0\[\r\]\[\n\]" MESSAGE \<\<
"Content-Language: en-US\[\r\]\[\n\]" MESSAGE \<\< "\[\r\]\[\n\]"

Above The 302 Found response was following the Status code 401 which is
client was getting an unauthorized response from the server with the
link to jauth-issue-token from the server. So it tries to present a
authentication challenge to the URL received to get a token issued. 302
Found in this case is expected behavior.

Now what if , we see the status code for the authentication request is
200 at first but still user is failing to log-in to the IBM Rational
Team Concert Server? You have to look at the all the "\>\>" entries to
find out if its really the case. You need to focus on POST calls for the
authentication. What request client is sending to server and what
response it gets back for that POST request for authentication.

We will now discuss this in the below section of analyzing the server
logs.

## How to Navigate in Rational Team Concert server log?

After enabling the [Debug
Tracing](IntegrationsTroubleshootingSmartCardDebug) for the IBM Rational
Team Concert server you will start seeing information in the log for
authentication requests from the client using the JAuth Token they have
sent to the server for authentication.

A successful log-in looks like this in ccm.log:

USER.NAME.1234545
/ccm/service/com.ibm.team.repository.common.internal.IRepositoryRemoteService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Searching for
the JAuth token identified as "\_jCfAMFhUEeSXYZuMs1YgCQ"
USER.NAME.1234545
/ccm/service/com.ibm.team.repository.common.internal.IRepositoryRemoteService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Token handle
\_jCfAMFhUEeSXYZuMs1YgCQ not found in cache, trying to find by query
USER.NAME.1234545
/ccm/service/com.ibm.team.repository.common.internal.IRepositoryRemoteService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Token handle
\_jCfAMFhUEeSXYZuMs1YgCQ not found by query USER.NAME.1234545
/ccm/service/com.ibm.team.repository.common.internal.IRepositoryRemoteService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - unable to
find token identified by \_jCfAMFhUEeSXYZuMs1YgCQ USER.NAME.1234545
/ccm/service/com.ibm.team.repository.common.internal.IRepositoryRemoteService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Unauthorized:
unable to find a valid token identified by \_jCfAMFhUEeSXYZuMs1YgCQ
USER.NAME.1234545
/ccm/service/com.ibm.team.repository.common.internal.IRepositoryRemoteService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Value of
authenticate header: "jauth
realm="[https://HOST:PORT/ccm/](https://HOST:PORT/ccm/)",
token_uri="[https://HOST:PORT/ccm/jauth-issue-token](https://HOST:PORT/ccm/jauth-issue-token)""
USER.NAME.1234545 /ccm/jauth-issue-token\] DEBUG
pository.internal.service.auth.impl.IssueAuthToken - Searching for the
JAuth token identified as "USER.NAME.1234545" USER.NAME.1234545
/ccm/jauth-issue-token\] DEBUG
pository.internal.service.auth.impl.IssueAuthToken - Token not found
USER.NAME.1234545 /ccm/jauth-issue-token\] DEBUG
pository.internal.service.auth.impl.IssueAuthToken - Referenced
contributor is admin: "false" USER.NAME.1234545 /ccm/jauth-issue-token\]
DEBUG pository.internal.service.auth.impl.IssueAuthToken - Returning
contributor item for "User Name" USER.NAME.1234545
/ccm/jauth-issue-token\] DEBUG
pository.internal.service.auth.impl.IssueAuthToken - Creating new token
in database USER.NAME.1234545 /ccm/jauth-issue-token\] DEBUG
pository.internal.service.auth.impl.IssueAuthToken - Saved token to
database USER.NAME.1234545
/ccm/service/com.ibm.team.repository.common.internal.IRepositoryRemoteService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Searching for
the JAuth token identified as "6b40cc8b634947fd884771f9be53db85"
USER.NAME.1234545
/ccm/service/com.ibm.team.repository.common.internal.IRepositoryRemoteService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Token handle
6b40cc8b634947fd884771f9be53db85 not found in cache, trying to find by
query USER.NAME.1234545
/ccm/service/com.ibm.team.repository.common.internal.IRepositoryRemoteService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Token
6b40cc8b634947fd884771f9be53db85 found USER.NAME.1234545
/ccm/service/com.ibm.team.repository.common.internal.IRepositoryRemoteService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Searching for
the JAuth token identified as "6b40cc8b634947fd884771f9be53db85"
USER.NAME.1234545
/ccm/service/com.ibm.team.repository.common.internal.IRepositoryRemoteService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Token handle
6b40cc8b634947fd884771f9be53db85 found in cache USER.NAME.1234545
/ccm/service/com.ibm.team.repository.common.internal.IRepositoryRemoteService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Token
6b40cc8b634947fd884771f9be53db85 found

**NOTE**: The timestamps are removed from the above example for easy
reading.

Above you see the automatically generated [JAuth Access
Token](https://jazz.net/wiki/bin/view/Main/JAuthOverview)
**\_jCfAMFhUEeSXYZuMs1YgCQby** by client was received by the server with
an associated certificate **USER.NAME.1234545** which server was able to
map correctly to a particular user **"User Name"**. But this JAuth Token
was not found by the server. **IssueAuthToken** issued a new JAuth Token
to the user certificate and saved it in the database. The new Token
**6b40cc8b634947fd884771f9be53db85** is now associated with the user
certificate for this session and will be used again for future
authentication requests until the token expires (usually within 24
hours) or revoked. [JAuth Access
Token](https://jazz.net/wiki/bin/view/Main/JAuthOverview) is only
assigned to an authenticated user.

Now that we know how the successful log-in looks like , what if the user
was getting an error while logging-in selecting the right certificate in
the Eclipse client? The selected certificate is loaded in the Smart Card
and name of the certificate is displayed as USER.NAME.1234545 in Eclipse
client.

IBM Rational Team Concert Eclipse log-in window:

Error reported while trying to log-in is:

MESSAGE CRJAZ0053I The identifier for the repository identified by
"[https://HOST:PORT/ccm](https://HOST:PORT/ccm)" could not be contacted:
Received fatal alert: bad_certificate STACK 0
javax.net.ssl.SSLHandshakeException: Received fatal alert:
bad_certificate at com.ibm.jsse2.o.a(o.java:15) at
com.ibm.jsse2.o.a(o.java:11) at
com.ibm.jsse2.SSLSocketImpl.b(SSLSocketImpl.java:252) at
com.ibm.jsse2.SSLSocketImpl.a(SSLSocketImpl.java:392) at
com.ibm.jsse2.SSLSocketImpl.h(SSLSocketImpl.java:496) at
com.ibm.jsse2.SSLSocketImpl.a(SSLSocketImpl.java:528) at
com.ibm.jsse2.SSLSocketImpl.startHandshake(SSLSocketImpl.java:505) at
com.ibm.net.ssl.www2.protocol.https.c.afterConnect(c.java:83) at
com.ibm.net.ssl.www2.protocol.https.d.connect(d.java:31) at
com.ibm.net.ssl.www2.protocol.https.b.connect(b.java:31) at
com.ibm.team.repository.client.util.RepositoryUtil.getRepositoryId2(RepositoryUtil.java:115)
at
com.ibm.team.repository.client.internal.TeamRepositoryService.connectToAndUpdateTeamRepository(TeamRepositoryService.java:401)
at
com.ibm.team.repository.client.internal.TeamRepositoryService.getTeamRepositoryWithOverride(TeamRepositoryService.java:179)
at
com.ibm.team.process.rcp.ui.RepositoryCreationPage.createNewRepository(RepositoryCreationPage.java:233)
at
com.ibm.team.process.rcp.ui.RepositoryCreationPage.create(RepositoryCreationPage.java:200)
at
com.ibm.team.process.rcp.ui.RepositoryCreationPage\$1.run(RepositoryCreationPage.java:129)
at
org.eclipse.jface.operation.ModalContext\$ModalContextThread.run(ModalContext.java:121)

If we investigate the .log file of Eclipse we will notice that we sent
this [JAuth Access
Token](https://jazz.net/wiki/bin/view/Main/JAuthOverview) to server:
**\_GKvY0FhUEeSsnMfoOEZbww**

Line 593: MESSAGE \>\> "POST
/ccm/service/com.ibm.team.repository.common.service.IQueryService
HTTP/1.1\[\r\]\[\n\]" Line 596: MESSAGE \>\> "http.useragent:
com.ibm.team.repository.transport.client.RemoteTeamService\[\r\]\[\n\]"
Line 599: MESSAGE \>\> "Accept-Language: en-US\[\r\]\[\n\]" Line 602:
MESSAGE \>\> "Accept: text/xml\[\r\]\[\n\]" Line 605: MESSAGE \>\>
"Accept-Charset: UTF-8\[\r\]\[\n\]" Line 608: MESSAGE \>\>
"X-com-ibm-team-userid: \[\r\]\[\n\]" Line 611: MESSAGE \>\>
"X-com-ibm-team-marshaller-version: 0.2\[\r\]\[\n\]" Line 614: MESSAGE
\>\> "X-com-ibm-team-service-version: 1\[\r\]\[\n\]" Line 617: MESSAGE
\>\> "Accept-Encoding: gzip\[\r\]\[\n\]" Line 620: MESSAGE \>\>
"Authorization: jauth user_token=\_GKvY0FhUEeSsnMfoOEZbww\[\r\]\[\n\]"
Line 623: MESSAGE \>\> "X-com-ibm-team-configuration-versions:
com.ibm.team.jazz.foundation=4.0.3,com.ibm.team.rtc=4.0.3\[\r\]\[\n\]"
Line 626: MESSAGE \>\> "User-Agent: Jakarta
Commons-HttpClient/3.1\[\r\]\[\n\]" Line 629: MESSAGE \>\> "Host:
HOST.DOMAINl\[\r\]\[\n\]" Line 632: MESSAGE \>\> "Content-Length:
1045\[\r\]\[\n\]" Line 635: MESSAGE \>\> "Content-Type:
text/xml\[\r\]\[\n\]" Line 638: MESSAGE \>\> "\[\r\]\[\n\]"

And we received the response from the server in eclipse log file:

Line 722: MESSAGE \<\< "HTTP/1.1 401 Unauthorized\[\r\]\[\n\]" Line 725:
MESSAGE \<\< "HTTP/1.1 401 Unauthorized\[\r\]\[\n\]" Line 728: MESSAGE
\<\< "Date: Thu, 09 Oct 2014 14:27:19 GMT\[\r\]\[\n\]" Line 731: MESSAGE
\<\< "WWW-Authenticate: jauth
realm="[https://HOST:PORT/ccm/](https://HOST:PORT/ccm/)",
token_uri="https://HOST:PORT/ccm/jauth- issue-token"\[\r\]\[\n\]" Line
734: MESSAGE \<\< "Transfer-Encoding: chunked\[\r\]\[\n\]" Line 737:
MESSAGE \<\< "Content-Type: text/plain;charset=UTF-8\[\r\]\[\n\]" Line
740: MESSAGE \<\< "Content-Language: en-US\[\r\]\[\n\]" Line 743:
MESSAGE \<\< "\[\r\]\[\n\]"

As you notice we get a status 401 from the server for the authentication
request sent to server. Its also sending a link in response to contact
"https://HOST:PORT/ccm/jauth- issue-token" and get [JAuth Access
Token](https://jazz.net/wiki/bin/view/Main/JAuthOverview) issued. So now
we look at the server side what happened to this [JAuth Access
Token](https://jazz.net/wiki/bin/view/Main/JAuthOverview) :
**\_GKvY0FhUEeSsnMfoOEZbww** when server received it for certificate
USER.NAME.1234545:

/ccm/service/com.ibm.team.repository.common.service.IQueryService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Searching for
the JAuth token identified as "\_GKvY0FhUEeSsnMfoOEZbww"
/ccm/service/com.ibm.team.repository.common.service.IQueryService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Token handle
\_GKvY0FhUEeSsnMfoOEZbww not found in cache, trying to find by query
/ccm/service/com.ibm.team.repository.common.service.IQueryService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Token handle
\_GKvY0FhUEeSsnMfoOEZbww not found by query
/ccm/service/com.ibm.team.repository.common.service.IQueryService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - unable to
find token identified by \_GKvY0FhUEeSsnMfoOEZbww
/ccm/service/com.ibm.team.repository.common.service.IQueryService\]
DEBUG repository.internal.service.auth.impl.JAuthHandler - Unauthorized:
unable to find a valid token identified by \_GKvY0FhUEeSsnMfoOEZbww

Compared to the successful log-in, you will notice that when server is
receiving the [JAuth Access
Token](https://jazz.net/wiki/bin/view/Main/JAuthOverview)
**\_GKvY0FhUEeSsnMfoOEZbww** to be identified , its unable to accept the
certificate associated with it. Server is registering that certificate
as **unauthenticated** certificate and tries to find the [JAuth Access
Token](https://jazz.net/wiki/bin/view/Main/JAuthOverview) in cache or in
data base. There was no new JAuth token issued to the
**unauthenticated** certificate. The user certificate hence was not
valid for the server and user was not able to log-in to the CCM server.

One possible root cause is that the signer certificate for the user
certificate USER.NAME.1234545 is not present as a Trusted Root
certificate in NodeDefaultTrustStore of IBM WebSphere. Hence the
certificate is registered as **unauthenticated** by server and user can
not log-in to the Server via Eclipse client.

For information on how to add the signer certificate (Trusted Root
Certificate) to WebSphere , Refer to settings: [Configuring certificate
authentication in Rational Team Concert 3.0 using WebSphere Application
Server 7.0](https://jazz.net/library/article/606)

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: [additional-contributors]

META:FILEATTACHMENT{name="login.jpg" attachment="login.jpg" attr="h"
comment="Repository login Eclipse" date="1415607500" path="login.jpg"
size="88495" user="zeech" version="1"}
