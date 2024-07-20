META:TOPICINFO{author="shradha" date="1704704393" format="1.1"
reprev="1.16" version="1.16"}
META:TOPICPARENT{name="DeploymentAdminstering"}

# Configure CA and Self-Signed Certificates in Liberty and IHS for ELM Applications DKGRAY Authors: Main.ShradhaSrivastav, Main.BharathRao Build basis: ELM 6.x - 7.0.2 Sr1 [configure-ca-and-self-signed-certificates-in-liberty-and-ihs-for-elm-applications-dkgray-authors-main.shradhasrivastav-main.bharathrao-build-basis-elm-6.x---7.0.2-sr1]

ENDCOLOR

TOC{title="Page contents"}

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

## **Using IKEYMAN (Graphical User Interface)**

### Create Keystore (Optional, if existing keystore is not used)

1.  Open ikeyman.exe, Key Database File -\> New
2.  Select any Type
3.  Provide File name and path to the file

### Update server.xml (Only for Liberty) to point to new key store (Optional, only if new keystore is created)

1.  Update server.xml located at
    JazzTeamServer\server\liberty\servers\clm to point to new database
    file, type and password
2.  If type Selected while creating keystore is pk12 Type will be
    PKCS12, for jks Type will be JKCS
3.  Restart the server for changes to take effect

### To Create A Self-Signed Certificate a. Open ikeyman (GUI) utility located at JazzTeamServer\server\jre\bin

1.  Key Database File -\> Open -\> Browse to keystore file, enter
    password to open the file
2.  Click Create -\> New Self Signed Certificate and fill the required
    details
3.  Restart server for changes to take effect

### To Configure A CA Certificate

#### Generate certificate Request

a\. Open the Keystore database file using ikeyman a. Click Create -\>
New Certificate request and fill the necessary details a.

#### Send the certificate request generated to CA authority

#### Receive Certificate and Add it to Keystore

1.  Open the Keystore database file using ikeyman
2.  Select **Personal Certificates**
3.  Click Receive -\> Browse to the certificate received

#### Add Intermediate and Root certificate (*In case the Intermediate certificate is not included in the certificates received or CA is not a trusted (internal CA) , add them explicitly in Signers*) a. Open the Keystore database file using ikeyman

1.  Switch to **Signer Certificates**
2.  Click Add -\> Browse to Intermediate/Root certificate
3.  Enter a label in dialog box

## **Using IKEYCMD CLI**

ORANGE Installation Paths for each component will be: ENDCOLOR

For CLM Liberty use ikeycmd JazzTeamServerInstall\server\jre\bin IBM
HTTP Server use gskcmd IHSinstall_root\bin

### Create Keystore (Optional, if existing keystore is not used)

ikeycmd -keydb -create -db .kdb -pw -type cms -expire -stash .sth
./gskcmd -keydb -create -db ihskeys.kdb -pw secret -type cms -expire 365
-stash ihskeys.sth

Win:

Linux:

### Update server.xml (Only for Liberty) to point to new key store (Optional, only if new keystore is created)

### Create Self-Signed certificate

ikeycmd -cert -create -db -pw -label -dn -size -expire -sig_alg
-default_cert

Win:

Linux:

### Configure CA Certificate

1.  Generate certificate Request

ikeycmd -certreq -create -db .kdb -pw -label -dn -size -file .arm
-sig_alg

Win:

Linux:

1.  Send the certificate request generated to CA authority
2.  Receive Certificate and Add it to Keystore

ikeycmd -cert -receive -file -db .kdb -pw -format -default_cert

Win:

Linux:

**Note:** If the CA that issuing your CA-signed certificate is not a
trusted CA in the key database, store the CA certificate first and
designate the CA as a trusted CA. Then you can receive your CA-signed
certificate into the database. You cannot receive a CA-signed
certificate from a CA that is not a trusted CA. To add CA to trust
store, follow Intermediate and Root certificate section

### Intermediate and Root certificate In case of chain-intermediate certificate add then to Signers in keystore

ikeycmd -cert -add -db .kdb -pw -label -format -trust -file

**Additional commands**

To verify that the signer certificates were imported successfully, run
the following command:

./gskcmd -cert -list CA -db .kdb -pw

Display a list of certificates in a key database

./gskcmd -cert -list -db .kdb -pw

If the existing certificate in keystore is expired and new certificate
request needs to be created, you can use below command to recreate the
request which will use details from previously created certificate
request

./gskcmd -certreq -recreate -type cms -db .kdb -pw -label -target .arm

Note: The label needs to be same as original certificate request which
can be found using list command

Example: ./gskcmd -certreq -recreate -type cms -db ihskeys.kdb -pw
secret -label caelm -target newreq.arm

Reference
<https://www.ibm.com/support/knowledgecenter/SSEQTJ_9.0.5/com.ibm.websphere.ihs.doc/ihs/rihs_ikeycmdsyn.html>

**For Chrome** In case of using Internal CA when accessing the
application in Chrome it still displays the certificate warning because
of stringent security feature added by chrome, to fix that follow the
steps from below link
<https://www.techrepublic.com/article/how-to-resolve-ssl-certificate-warnings-produced-by-the-latest-chrome-update/>

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.ShradhaSrivastav, Main.BharathRao [additional-contributors-main.shradhasrivastav-main.bharathrao]

META:FILEATTACHMENT{name="1.png" attachment="1.png" attr="h" comment=""
date="1582615181" path="1.png" size="30630" user="shradha" version="1"}
META:FILEATTACHMENT{name="3.png" attachment="3.png" attr="h" comment=""
date="1582617319" path="3.png" size="36783" user="shradha" version="1"}
META:FILEATTACHMENT{name="4.png" attachment="4.png" attr="h" comment=""
date="1582617340" path="4.png" size="14236" user="shradha" version="1"}
META:FILEATTACHMENT{name="5.png" attachment="5.png" attr="h" comment=""
date="1582617410" path="5.png" size="36561" user="shradha" version="1"}
META:FILEATTACHMENT{name="6.png" attachment="6.png" attr="h" comment=""
date="1582617430" path="6.png" size="14571" user="shradha" version="1"}
META:FILEATTACHMENT{name="7.png" attachment="7.png" attr="h" comment=""
date="1582617549" path="7.png" size="46097" user="shradha" version="1"}
META:FILEATTACHMENT{name="8.png" attachment="8.png" attr="h" comment=""
date="1582617766" path="8.png" size="34529" user="shradha" version="1"}
META:FILEATTACHMENT{name="9.png" attachment="9.png" attr="h" comment=""
date="1582617788" path="9.png" size="5972" user="shradha" version="1"}
META:FILEATTACHMENT{name="10.png" attachment="10.png" attr="h"
comment="" date="1582617807" path="10.png" size="3348" user="shradha"
version="1"} META:FILEATTACHMENT{name="cmd1.png" attachment="cmd1.png"
attr="h" comment="" date="1582617834" path="cmd1.png" size="16965"
user="shradha" version="1"} META:FILEATTACHMENT{name="cmd2.png"
attachment="cmd2.png" attr="h" comment="" date="1582617854"
path="cmd2.png" size="10135" user="shradha" version="1"}
META:FILEATTACHMENT{name="cmd3.png" attachment="cmd3.png" attr="h"
comment="" date="1582618319" path="cmd3.png" size="31605" user="shradha"
version="1"} META:FILEATTACHMENT{name="cmd4.png" attachment="cmd4.png"
attr="h" comment="" date="1582618343" path="cmd4.png" size="30617"
user="shradha" version="1"} META:FILEATTACHMENT{name="cmd5.png"
attachment="cmd5.png" attr="h" comment="" date="1582618363"
path="cmd5.png" size="36632" user="shradha" version="1"}
META:FILEATTACHMENT{name="2.png" attachment="2.png" attr="h" comment=""
date="1582783683" path="2.png" size="6401" user="shradha" version="1"}
META:FILEATTACHMENT{name="linux1.PNG" attachment="linux1.PNG" attr="h"
comment="" date="1586150512" path="linux1.PNG" size="2892"
user="shradha" version="1"} META:FILEATTACHMENT{name="linux2.PNG"
attachment="linux2.PNG" attr="h" comment="" date="1586150535"
path="linux2.PNG" size="8769" user="shradha" version="1"}
META:FILEATTACHMENT{name="linux3.PNG" attachment="linux3.PNG" attr="h"
comment="" date="1586150575" path="linux3.PNG" size="5390"
user="shradha" version="1"} META:FILEATTACHMENT{name="linux4.0.PNG"
attachment="linux4.0.PNG" attr="h" comment="" date="1586150604"
path="linux4.0.PNG" size="4493" user="shradha" version="1"}
META:FILEATTACHMENT{name="linux4.1.PNG" attachment="linux4.1.PNG"
attr="h" comment="" date="1586150680" path="linux4.1.PNG" size="4311"
user="shradha" version="1"} META:FILEATTACHMENT{name="linux5.1.PNG"
attachment="linux5.1.PNG" attr="h" comment="" date="1586150714"
path="linux5.1.PNG" size="9375" user="shradha" version="1"}
