META:TOPICINFO{author="rschoon" date="1704701441" format="1.1"
version="1.10"} META:TOPICPARENT{name="ConfigureCACertificates"}

# Configure CA and Self-Signed Certificates in Liberty or IHS for ELM Applications 7.0.3 DKGRAY Authors: Main.ShradhaSrivastav Build basis: ELM 7.0.3 [configure-ca-and-self-signed-certificates-in-liberty-or-ihs-for-elm-applications-7.0.3-dkgray-authors-main.shradhasrivastav-build-basis-elm-7.0.3]

ENDCOLOR

TOC{title="Page contents"}

ELM 703 is shipped with **Java 11 which no longer ship Ikeyman utility**
to manage certificate and keystore using GUI.

This article will share sample commands that can be used in place of
ikeyman to create or generate new keystore and manage CA certificates.

## **Understanding SSL Certificates**

All applications which run on HTTPS via the web require a Security
Certificate, or Public Key Certificate. This is used to validate that
the data is coming from a trusted source. The security certificate
bundled with the Jazz Team Server and ELM applications is signed to
localhost. As soon as the application is accessed with a URL other than
localhost (for example, hostname or IP address), the browser will
present the following errors: \* The security certificate presented by
this website was not issued by a trusted certificate authority. \* The
security certificate presented by this website was issued for a
different website's address.

These errors occur because:

-   The security certificate was self-signed, meaning that the server
    being accessed created the certificate, and
-   The security certificate was created for localhost, and you are
    accessing the server using a different hostname, IP address or the
    appropriate Public URI.

In order to resolve these errors, you can:

-   Purchase a certificate from a well-known trusted Certificate
    Authority and install it.
-   If you do not need encryption, configure the server for HTTP rather
    than HTTPS access.
-   Configure the browser to ignore or accept this invalid certificate

In this article we will provide a guide on how to configure CA
Certificate purchased from well-known Authority or internal CA
certificate.

## **Configure Liberty Profile**

The Application server needs to be configured to pick up a valid
certificate. For Liberty Profile, the certificate needs to be configured
in the file
\[ServerInstallDir\]\JazzTeamServer\server\liberty\servers\clm\server.xml
The entry
[keystore](https://openliberty.io/docs/latest/reference/config/keyStore.html)
is, where the certificate is configured. By default, the entry looks
like

The location defines the path and name of the keystore. The keystore
shipped with the product
\[ServerInstallDir\]\JazzTeamServer\server\liberty\servers\clm\resources\security\ibm-team-ssl.p12
Please see the [documentation for the keystore
entry](https://openliberty.io/docs/latest/reference/config/keyStore.html)
for more options. You can change the path to a different keystore file.
You can place your keystore file into the same folder and just rename
the location. The password is encrypted. The type of the keystore can be
different based on choice e.g. PKCS12 or JKCS. See the documentation. It
is best practice to always provide the keystore type when operation on
the keystore.

After changing the server.xml settings restart the server.

### Encrypt the password for a new key store

If you use a **new keystore**, the keystore is created with a password.
The password has to be provided in the keystore entry. You can encrypt
the password to be able to put it input the server.xml. See the
description [how to encrypt the
password](https://www.ibm.com/support/pages/how-encrypt-passwords-elm-configuration-files).
See the image below.

## **Server name for the certificate**

The certificate needs to contain the information about the server name.
The server name is usually a unique name containing the fully qualified
domain name. Examples would be

-   elmserv1.fyre.ibm.com
-   elm.example.com

To provide the server name as command line parameter **-dname** the
above examples are provided this way:

-   elmserv1.fyre.ibm.com equals to -dname
    CN=elmserv1,DC=fyre,DC=ibm,DC=com
-   elm.example.com equals to -dname CN=elm,DC=example,DC=com

## **keytool command**

The new tool for working with certificates is **keytool**. The keytool
can be found in a Java JRE folder. As an example it is shipped with ELM
server in the folder
\[ServerInstallDir\]\JazzTeamServer\server\jre\bin\\

Tip: To work with the keytool copy the path to the keytool and keep it
in an editor. Open a console in a folder you want to use to store your
work. You can now use
\[ServerInstallDir\]\JazzTeamServer\server\jre\bin\keytool
\[Parameters\]to run the keytool. The files involved in the work can all
be kept in the dedicated folder. See the next paragraphs for examples
how to use **keytool**

### Create a new keystore with self-signed Certificate It is possible to create a self signed certificate. Todays browser will not trust a self signed certificate, but accept it if asked to. A self signed certificate is interesting, because it can be locally created without depending on a Certificate Authority (CA). The command requires several parameters such as the keystore name and type to use. As an example the command below creates a new self signed certificate in the file keystore.p12.

\[ServerInstallDir\]\JazzTeamServer\server\jre\bin\keytool -genkey
-alias default -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore
keystore.p12 -validity 3650 You will be prompted for some information
such as a password and additional data. See an example below. The
parameters needed are the password and the name. All other entries can
be left blank. The password will be requested twice, if the keystore
does not exist.

Password: \*\*\*\*\*\***\*** What is your first and last name?
elmserv1.fyre.ibm.com What is the name of your organizational unit? SW
What is the name of your organization? IBM What is the name of your City
or Locality? Rochester What is the name of your State or Province?
Massachusetts

To avoid having to deal with the prompt, it is possible to provide the
parameters required in the command. The example below will perform the
creation without prompt.

\[ServerInstallDir\]\JazzTeamServer\server\jre\bin\keytool -genkey
-dname CN=elmserv1,DC=fyre,DC=ibm,DC=com -alias default -keyalg RSA
-keysize 2048 -validity 3650 -storetype PKCS12 -keystore keystore.p12
-storepass \*\*\*\*\*\***\***

This concludes the creation of the self signed certificate. The
certificate is now in the keystore **keystore.p12**. After creating (or
updating) the keystore, configure the application server to use it by
updating the server.xml file as suggested above.

### To Configure A CA Certificate

For a real certificate that is also trusted by servers and browsers, it
is necessary to request a certificate from a CA. Then this request is
sent to a CA and the CA provides the valid certificate to you.

#### Generate certificate Request

To get a CA Certificate you have to generate a certificate request from
your keystore. See an example below. The generated file certreq.csr is
later used with your CA to receive the final certificate. How the
process works is dependent on the CA.

\[ServerInstallDir\]\JazzTeamServer\server\jre\bin\keytool -certreq
-alias default -keyalg RSA -file certreq.csr -storetype PKCS12 -keystore
keystore.p12 -storepass \*\*\*\*\*\***\***

See more examples below.

keytool -keystore keystore.p12 -certreq -alias default -keyalg RSA -file
certreq.csr -storepass 123456

#### Use the certificate request with the CA authority

The generated file certreq.csr is used with your CA to receive the final
certificate. How the process works is dependent on the CA.

#### Import/Receive Certificate and Add it to Keystore

The CA provides with a **signed or CA certificate** for the server. The
**signed or CA certificate** is received or can be downloaded. Obtain
the **signed or CA certificate**. There can be different formats and
file names. In this case the certificate is a file named **cert.der**

The CA also provides with

-   A root certificate
-   An intermediate certificate.

The **signed or CA certificate**, the **root** and the **intermediate**
certificate need to be added to the keystore. This is done using an
import operation. Import the **Intermediate certificate first** --\>
then the **root certificate** --\> and then the **signed or CA
certificate**. See the example below.

\[ServerInstallDir\]\JazzTeamServer\server\jre\bin\keytool -import
-alias inter -file caintermediatecert.der -keystore keystore.p12
-storepass \*\*\*\*\*\***\***
\[ServerInstallDir\]\JazzTeamServer\server\jre\bin\keytool -import
-alias root -file carootcert.der -keystore keystore.p12 -storepass
\*\*\*\*\*\***\***
\[ServerInstallDir\]\JazzTeamServer\server\jre\bin\keytool -alias
default -file cert.der -keystore keystore.p12 -storepass
\*\*\*\*\*\***\***

**Note**:- The intermediate and root certificate should have different
alias name, but the **signed certificate should be imported with the
same alias** that was used while creating a certificate pair. After
importing all three certificates you should see : **"Certificate reply
was installed in keystore"** message.

## **Using IKEYCMD CLI**

As IBM HTTP Server (IHS) still bundles Java 8, you can use ikeyman(GUI)
or gskcmd (also known as iKeycmd) to manage certificate and keystores.

For more please refer to
[ConfigureCACertificates](https://jazz.net/wiki/bin/view/Deployment/ConfigureCACertificates)

##### Related topics: [Deployment web home](DeploymentWebHome), [Keytool Guide](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=guide-keytool) [related-topics-deployment-web-home-keytool-guide]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.ShradhaSrivastav, [Ralph Schoon](Main.RalphSchoon) [additional-contributors-main.shradhasrivastav-ralph-schoon]

META:FILEATTACHMENT{name="1.png" attachment="1.png" attr="h" comment=""
date="1701668608" path="1.png" size="80285" user="shradha" version="1"}
META:FILEATTACHMENT{name="2.png" attachment="2.png" attr="h" comment=""
date="1701668633" path="2.png" size="76623" user="shradha" version="1"}
META:FILEATTACHMENT{name="3.png" attachment="3.png" attr="h" comment=""
date="1701668651" path="3.png" size="28759" user="shradha" version="1"}
META:FILEATTACHMENT{name="4.png" attachment="4.png" attr="h" comment=""
date="1701668672" path="4.png" size="82482" user="shradha" version="1"}
META:FILEATTACHMENT{name="5.png" attachment="5.png" attr="h" comment=""
date="1701668687" path="5.png" size="34520" user="shradha" version="1"}
META:FILEATTACHMENT{name="6.png" attachment="6.png" attr="h" comment=""
date="1701668705" path="6.png" size="124195" user="shradha" version="1"}
META:FILEATTACHMENT{name="7.png" attachment="7.png" attr="h" comment=""
date="1701668720" path="7.png" size="69246" user="shradha" version="1"}
META:FILEATTACHMENT{name="SelfSigned1.png" attachment="SelfSigned1.png"
attr="h" comment="" date="1702295253" path="SelfSigned1.png"
size="20219" user="rschoon" version="1"}
