META:TOPICINFO{author="din" date="1704783900" format="1.1"
version="1.12"} META:TOPICPARENT{name="SecurityWhereToStart"}

# Configuring TLS Extended Master Secret for WebSphere Application Server and WebSphere Liberty DKGRAY Authors: Main.HongyanHuo Main.SentellaCystrunk Contributors: Main.JonAgnew Main.AlexBernstein Main.KelvinLow Main.SkyeBischoff Build basis: CLM 6.0.6 and above, ELM 7.x [configuring-tls-extended-master-secret-for-websphere-application-server-and-websphere-liberty-dkgray-authors-main.hongyanhuo-main.sentellacystrunk-contributors-main.jonagnew-main.alexbernstein-main.kelvinlow-main.skyebischoff-build-basis-clm-6.0.6-and-above-elm-7.x]

ENDCOLOR

TOC{title="Page contents"}

`Note: Support removed for IBM !WebSphere Application Server (Traditional WAS) starting with ELM version 7.0.3. Use !WebSphere Liberty, either embedded and installed with ELM applications, or separately installed`

## Introduction

The ELM release includes Java. Java Security enhancement related to 1.2
TLS protocol is the Extended Master Secret. Java Extended Master Secret
(EMS) requires a full handshake for each SSL/TLS connection between
Application Servers and Web Servers.

At this time, not all proxy and HTTP servers support EMS. If you enable
EMS on servers that don't support it, ELM products hosted on WebSphere
Application Server or WebSphere Liberty might experience performance
issues. This article outlines which environments are affected by this
problem, how to diagnosis it, and how to configure your server to
resolve it.

### Affected deployments

All CLM/ELM Product Versions deployed on WebSphere Application Server
and WebSphere Liberty are affected with these JDK levels:

-   V8 SR5 FP10 (8.0.5.10) and newer
-   7 SR10 FP20 (7.0.10.20) and newer
-   7 R1 SR4 FP20 (7.1.4.20) and newer

The deployments must also have a proxy or web server that does not
support or enable Extended Master Secret (EMS), but connects directly to
WebSphere Application Server or WebSphere Liberty with SSL.

For example, the default installation of WebSphere Liberty 18.0.0.1 with
one of the following configurations is affected:

-   HAProxy 1.5.18/OpenSSL 1.0.2: HAProxy is configured as SSL
    termination and connects to backend WebSphere Liberty servers using
    SSL only
-   A legacy web server with underlying SSL libraries or SSL modules
    that are not EMS-compatible (depending on the SSL configuration with
    backend WebSphere Liberty servers)

### Symptoms

You might see these symptoms after a ELM WebSphere Liberty upgrade or
2018 Java JDK upgrade on any platform:

-   Slow page loading or timeouts
-   Significantly decreased server throughput
-   Increased server CPU utilization on the WebSphere Application Server
    or WebSphere Liberty server
-   When SSL tracing is enabled on the WebSphere Application Server or
    WebSphere Liberty server, excessive messages are shown such as "
    Initialized: \[Session-, SSL_NULL_WITH_NULL_NULL\]", " Negotiating:
    \[Session-, \]"

### Cause

A full handshake (which is CPU intensive) is required for each SSL/TLS
connection between WebSphere Liberty and the proxy servers, when the new
EMS security feature is enabled by default on the WebSphere Liberty
server JVM, while the proxy server is not. For details, see the IBM APAR
IJ05598 at <https://www-01.ibm.com/support/docview.wss?uid=swg1IJ05598>.

### ELM Liberty Default for EMS

ELM packaged Liberty install will have Extended Master Secret set to
disabled by default. We decided disabling EMS is the best initial option
for users migrating to the new Liberty version or Java versions. This
allows users to migrate to the new installations without issues, and
gives Administrators time to decide on the best security options for
their application server and connected proxy/http server. If you desire
to enable EMS in your Liberty environment you should read [Solution
2](#EnableEMS) below on how to properly enable EMS.

### Solution 1 - Disable EMS

The simplest way to avoid EMS performance or compatibility problems is
to disable EMS. For many environments this is an acceptable solution and
avoids complex compatibility problems the new EMS setting can cause
between the application server and different proxies. Likewise you may
want to disable EMS temporarily while your admin and security team
determine the correct proxy/http server upgrades required to fully
support EMS.

#### Disabling EMS on Websphere Liberty

To disable EMS in WebSphere Liberty you can add the following JVM
argument to the server startup script. In start-jazz on the Jazz
Authorization Server WebSphere Liberty server, you add the following
argument to the existing ones: export JVM_ARGS="...
-Djdk.tls.useExtendedMasterSecret=false"

In the server.startup file on the remaining CLM/ELM WebSphere Liberty
servers, you add the following argument: JAVA_OPTS="\$JAVA_OPTS
-Djdk.tls.useExtendedMasterSecret=false"

#### Disabling EMS on WebSphere Application Server

To disable EMS in WebSphere Application Server you can add the following
argument to the server's generic JVM arguments. Go to **Application
servers \> server1 \> Process definition \> Java Virtual Machine** and
add the following argument: Add
"-Djdk.tls.useExtendedMasterSecret=false" to the Generic JVM Arguments

\#EnableEMS

### Solution 2 - Enable EMS and Upgrade the proxy

For WebSphere Liberty or WebSphere Application Server, you might choose
to leave the jdk.tls.useExtendedMasterSecret=true setting (the default)
and ensure that your front-end proxy or HTTP server is up to date with
the latest SSL libraries and Java instead. For the WebSphere IHS or
proxy server, you must upgrade to the latest 8.x or 9.x version that
matches your WebSphere Application Server, and upgrade your Java JDK on
both your IHS or proxy server and WebSphere Application Server. For
other solutions, such as HAProxy, you must download and install the
latest version of OpenSSL, or wait for an updated HAProxy for your Linux
distribution. Other proxy solutions also require updates to their core
product or underlining SSL libraries. After upgrading your proxy/http
server you should also check your application server JVM arguments and
ensure useExtendedMasterSecret is enabled as highlighted below. Note if
useExtendedMasterSecret is not present in your configurations it will
default to enabled.

#### Enabling EMS on Websphere Liberty

To enable EMS in WebSphere Liberty you can add the following JVM
argument to the server startup script. In start-jazz on the Jazz
Authorization Server WebSphere Liberty server, you add the following
argument to the existing ones: export JVM_ARGS="...
-Djdk.tls.useExtendedMasterSecret=true"

In the server.startup file on the remaining CLM WebSphere Liberty
servers, you add the following argument: JAVA_OPTS="\$JAVA_OPTS
-Djdk.tls.useExtendedMasterSecret=true"

#### Enabling EMS on WebSphere Application Server

To enable EMS in WebSphere Application Server you can add the following
argument to the server's generic JVM arguments. Go to **Application
servers \> server1 \> Process definition \> Java Virtual Machine** and
add the following argument: Add "-Djdk.tls.useExtendedMasterSecret=true"
to the Generic JVM Arguments

### Diagnosis

#### Option 1 - Support check

To demonstrate the change in behavior without enabling Java SSL
debugging, you can run the OpenSSL s_client with the -reconnect option,
using a version of OpenSSL that does not support the Extended Master
Secret extension. For example, install an older version of OpenSSL such
as 1.0.2k-fips from 26 January 2017.

\$ openssl version OpenSSL 1.0.2k-fips 26 Jan 2017

\# Against the old Java, or a new Java with
-Djdk.tls.useExtendedMasterSecret=false, you can reuse the session ID to
resume the session. \$ openssl s_client -reconnect -connect
jontestvm.rtp.raleigh.ibm.com:9643 \< /dev/null 2\>&1 \| grep 'Cipher
is' New, TLSv1/SSLv3, Cipher is ECDHE-RSA-AES256-GCM-SHA384 Reused,
TLSv1/SSLv3, Cipher is ECDHE-RSA-AES256-GCM-SHA384 Reused, TLSv1/SSLv3,
Cipher is ECDHE-RSA-AES256-GCM-SHA384 Reused, TLSv1/SSLv3, Cipher is
ECDHE-RSA-AES256-GCM-SHA384 Reused, TLSv1/SSLv3, Cipher is
ECDHE-RSA-AES256-GCM-SHA384 Reused, TLSv1/SSLv3, Cipher is
ECDHE-RSA-AES256-GCM-SHA384

\# Against a new Java that supports the Extended Master Secret
extension, the server rejects the client's attempt to resume using the
session ID, which forces a full handshake each time. \$ openssl s_client
-reconnect -connect jontestvm.rtp.raleigh.ibm.com:9644 \< /dev/null
2\>&1 \| grep 'Cipher is' New, TLSv1/SSLv3, Cipher is
ECDHE-RSA-AES256-GCM-SHA384 New, TLSv1/SSLv3, Cipher is
ECDHE-RSA-AES256-GCM-SHA384 New, TLSv1/SSLv3, Cipher is
ECDHE-RSA-AES256-GCM-SHA384 New, TLSv1/SSLv3, Cipher is
ECDHE-RSA-AES256-GCM-SHA384 New, TLSv1/SSLv3, Cipher is
ECDHE-RSA-AES256-GCM-SHA384 New, TLSv1/SSLv3, Cipher is
ECDHE-RSA-AES256-GCM-SHA384

#### Option 2 - Debug check

When SSL tracing or SSL debugging is enabled, in every ClientHello
initiated by a proxy server, an attribute called "Extension
extended_master_secret" is **not** present, followed by messages that
indicate new key generation and negotiation start and complete before
ServerHello. To enable SSL debugging, you can set this JVM argument:
-Djavax.net.debug=ssl. Start the server and observe the log.

If excessive handshaking occurs, you will see repetitive messages like
the following one and no "Extension extended_master_secret"
notification:

**\*** ClientHello, TLSv1.2 ... **\*** Initialized: \[Session-10387,
SSL_NULL_WITH_NULL_NULL\] ssl: ServerHandshaker.setupPrivateKeyAndChain
RSA matching alias: default ssl:
ServerHandshaker.setupPrivateKeyAndChain, chooseEngineServerAlias
default ssl: ServerHandshaker.setupPrivateKeyAndChain, return true
JsseJCE: Using KeyPairGenerator EC from provider TBD via init JsseJCE:
Using SecureRandom SHA2DRBG from provider IBMJCE version 1.8 JsseJCE:
Using KeyPairGenerator EC from provider TBD via init ECDHCrypt: ECDH
KeyPairGenerator from provider from init IBMJCE version 1.8 Negotiating:
\[Session-10387, SSL_ECDHE_RSA_WITH_AES_128_CBC_SHA256\] JsseJCE: Using
MessageDigest SHA-256 from provider IBMJCE version 1.8 **\***
ServerHello, TLSv1.2

If the configuration is correct with the newer JDK, after the first full
handshake, you will see the "Extension extended_master_secret"
notification:

**\*** ClientHello, TLSv1.2 ... Compression Methods: { 0 } Extension
elliptic_curves, curve names: {secp256r1, secp384r1, secp521r1,
secp256k1} Extension ec_point_formats, formats: \[uncompressed\]
Extension signature_algorithms, signature_algorithms: SHA512withECDSA,
SHA512withRSA, SHA384withECDSA, SHA384withRSA, SHA256withECDSA,
SHA256withRSA, SHA224withECDSA, SHA224withRSA, SHA1withECDSA,
SHA1withRSA, SHA256withDSA, SHA1withDSA Extension extended_master_secret
Extension server_name, server_name: \[type=host_name (0),
value=v-6c26c0cb-ihs.rtp.raleigh.ibm.com\] **\*** qm:
AsynchronousTaskRunner-3 @@ 09:35, WRITE: TLSv1.2 Handshake, length =
260 qm: AsynchronousTaskRunner-3 @@ 09:35, READ: TLSv1.2 Handshake,
length = 91 **\*** ServerHello, TLSv1.2 RandomCookie: ...

Note: If EMS is disabled, the extension is not shown regardless of the
SSL configuration.
