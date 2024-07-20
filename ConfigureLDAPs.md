META:TOPICINFO{author="shubjit" date="1668000925" format="1.1"
version="1.17"} META:TOPICPARENT{name="DeploymentAdminstering"}

# Configure Secure LDAP with Liberty and WebSphere for ELM Applications DKGRAY Authors: Main.BharathRao, Main.ShradhaSrivastav Build basis: ELM 7.0.1 and higher [configure-secure-ldap-with-liberty-and-websphere-for-elm-applications-dkgray-authors-main.bharathrao-main.shradhasrivastav-build-basis-elm-7.0.1-and-higher]

ENDCOLOR

TOC{title="Page contents"}

LDAP directory servers, mainly used as an authentication repository, are
often used to store sensitive information like passwords and other
account details. If your ELM environment uses an external LDAP-based
user repository, such as IBM Tivoli Directory Server or Microsoft Active
Directory, you can configure it to communicate over a secure SSL
channel.

This article assumes that you have already an existing connection to an
LDAP server set up.

Your LDAP server, must be configured to accept SSL connections and be
running on secured port number (636). Refer to your LDAP server
documentation if you need to create a signer certificate, which as part
of this task, must be imported from your LDAP server into the trust
store of the application server.

This article provides step by step instructions on configuring ELM with
secure LDAP(LDAPS)

## Liberty Server

**NOTE: Ensure you have a working LDAP configuration with CLM before
enabling LDAP SSL.** Reference: ConfigureLDAPforLibertyProfile

### Configure secure LDAP in Liberty

\- Enable **Require SSL** and update the **LDAP Port** to secure port in
the ldapUserRegistry.xml file located in
\server\liberty\servers\clm\conf\\ **NOTE: Any changes to the group /
ldap properties if made had to be corrected in the application.xml file
located in \server\liberty\servers\clm\conf\\**

1.  Ensure to include the below features in the ldapUserRegistry.xml
2.  Edit the LDAP configuration in the Liberty server in
    ldapUserRegistry.xml file
3.  Proceed with the next section to add LDAP SSL certificate

### Add LDAP SSL certificate

1.  To configuration secure LDAP, obtain the SSL signer certificate from
    the LDAP server
2.  From the file explorer, navigate to \server\jre\bin and double click
    on ikeyman.exe
3.  To open an existing keystore file, Click on
4.  Choose the Key database type from the drop-down and click on Browse
    to select the key database file(kdb). Enter the password and click
    on Ok to open the file
5.  After the kdb is open, click on the drop-down and choose Signer
    Certificate
6.  Click on Add and browse the signer certificate file(.arm) obtained
    from the LDAP server, then click ok to add the certificate
7.  Proceed with the next section to configure secure LDAP in JTS server

Alternatively you can generate the certificate using the following
command line: =ikeycmd -cert -add -db -type kdb -file -pw =

### Configuring secure LDAP In JTS server

**NOTE: Any changes to the group / ldap properties if made has to be
corrected here**

1.  Login to https://clmexample.com:9443/jts/setup, proceed to the User
    Registry section
2.  In the User Registry section, edit the LDAP host configuration to
    update the LDAP port to secure port
3.  Perform a test connection and ensure the LDAP configuration succeeds
4.  Restart the Liberty server

## WebSphere Application Server

**NOTE: Ensure you have a working LDAP configuration with CLM before
enabling LDAP SSL.**

### Configure secure LDAP in WAS

1.  Enable Require SSL
2.  Change LDAP PORT to secure port

### Add LDAP SSL certificate

a\. Login to WebSphere Application Server Administration Console
Navigate to Security \> SSL certificate and key management a. Click on
Key stores and certificates a. Click on NodeDefaultTrustStore a. Click
on Signer certificates a. Click Retrieve from port to retrieve the LDAP
SSL certificate from the LDAP server a. Enter the LDAPS server details
and click on Retrieve signer information a. Confirm the SSL certificate
for LDAPS Server is retrieved and then click OK a. Click on Save a.
Proceed with the next section to configure secure LDAP in JTS Server

### Configuring secure LDAP In JTS server

**NOTE: Any changes to the group / ldap properties if made has to be
corrected here** a. Login to https://clmexample.com:9443/jts/setup,
proceed to the User Registry section a. In the User Registry section,
edit the LDAP host configuration to update the LDAP port to secure port
a. Perform a test connection and ensure the LDAP configuration succeeds
a. Proceed with the next section to remap group mappings in WAS

### Remap Security Group Mappings in WAS

1.  Login to WAS Administration Console
2.  Remove and re-add the user/group mappings under Security role to
    user/group mapping for each of the CLM/ELM applications [Remap war
    files](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.rational.pe.install.doc2Ftopics2Ft_auth_ldap_MS_ADS.html)
3.  Restart WAS

##### Related topics: [Configure LDAP for Liberty Profile](ConfigureLDAPforLibertyProfile), [Deployment web home](DeploymentWebHome) [related-topics-configure-ldap-for-liberty-profile-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

META:FILEATTACHMENT{name="Picture2.png" attachment="Picture2.png"
attr="h" comment="" date="1582625425" path="Picture2.png" size="75606"
user="shradha" version="1"} META:FILEATTACHMENT{name="Picture3.png"
attachment="Picture3.png" attr="h" comment="" date="1582625446"
path="Picture3.png" size="183049" user="shradha" version="1"}
META:FILEATTACHMENT{name="Picture4.png" attachment="Picture4.png"
attr="h" comment="" date="1582625512" path="Picture4.png" size="125539"
user="shradha" version="1"} META:FILEATTACHMENT{name="Picture5.png"
attachment="Picture5.png" attr="h" comment="" date="1582625534"
path="Picture5.png" size="63227" user="shradha" version="1"}
META:FILEATTACHMENT{name="Picture6.png" attachment="Picture6.png"
attr="h" comment="" date="1582625582" path="Picture6.png" size="51235"
user="shradha" version="1"} META:FILEATTACHMENT{name="Picture9.png"
attachment="Picture9.png" attr="h" comment="" date="1582625661"
path="Picture9.png" size="64905" user="shradha" version="1"}
META:FILEATTACHMENT{name="Picture15.png" attachment="Picture15.png"
attr="h" comment="" date="1582630542" path="Picture15.png" size="19016"
user="brao" version="1"} META:FILEATTACHMENT{name="Picture12.png"
attachment="Picture12.png" attr="h" comment="" date="1584445479"
path="Picture12.png" size="216585" user="brao" version="1"}
META:FILEATTACHMENT{name="Picture13.png" attachment="Picture13.png"
attr="h" comment="" date="1584445500" path="Picture13.png" size="242112"
user="brao" version="1"} META:FILEATTACHMENT{name="Picture1.png"
attachment="Picture1.png" attr="h" comment="" date="1584506736"
path="Picture1.png" size="410631" user="brao" version="1"}
META:FILEATTACHMENT{name="Picture7.png" attachment="Picture7.png"
attr="h" comment="" date="1584506827" path="Picture7.png" size="214855"
user="brao" version="1"} META:FILEATTACHMENT{name="Picture10.png"
attachment="Picture10.png" attr="h" comment="" date="1584509097"
path="Picture10.png" size="105083" user="brao" version="1"}
META:FILEATTACHMENT{name="Picture11.png" attachment="Picture11.png"
attr="h" comment="" date="1584509689" path="Picture11.png" size="31299"
user="brao" version="1"} META:FILEATTACHMENT{name="Picture14.png"
attachment="Picture14.png" attr="h" comment="" date="1585049511"
path="Picture14.png" size="308304" user="brao" version="1"}
META:FILEATTACHMENT{name="Picture16.png" attachment="Picture16.png"
attr="h" comment="" date="1585049536" path="Picture16.png" size="312874"
user="brao" version="1"}
