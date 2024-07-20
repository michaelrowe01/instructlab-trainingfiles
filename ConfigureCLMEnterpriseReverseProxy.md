META:TOPICINFO{author="shubjit" date="1701962173" format="1.1"
reprev="1.16" version="1.16"}
META:TOPICPARENT{name="InstallProxyServers"}

# Configuring Enterprise CLM Reverse Proxies: WebSphere 8 and IHS 8 [configuring-enterprise-clm-reverse-proxies-websphere-8-and-ihs-8]

DKGRAY Authors: Main.SudhakarFrederick Build basis: Rational solution
for Collaborative Lifecycle Management 4.0.1, Websphere Application
Server (Base) 8.0.0.2, IBM HTTP Server 8.0.0.2 ENDCOLOR

TOC{title="Page contents"}

`note: Support removed for IBM !WebSphere Application Server (Traditional WAS) with ELM version 7.0.3. Use !WebSphere Liberty, either embedded and installed with ELM applications, or separately installed`

This guide will explain how to setup and configure an example CLM
environment using [WebSphere Application
Server](http://www-01.ibm.com/software/webservers/appserv/was/) (WAS),
[IBM HTTP
Server](http://www-01.ibm.com/software/webservers/httpservers/) (IHS)
and the [WAS web server
plugins](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.nd.doc/info/ae/ae/twsv_plugin.html)
for IHS, such that users will be able to access the various CLM
applications simply by changing the context root of a central URL which
is processed by IHS. IHS will take care of sending the requests to the
appropriate JTS/CCM/QM/RM application servers operating behind the
proxy.

Note that [Configuring Enterprise CLM Reverse Proxies: WebSphere 7 and
IHS 7](ConfigureCLMEnterpriseReverseProxywithWAS7) covers this same
ground with Websphere 7 and IHS 7. There have been some changes in the
installation and configuration processes in Websphere 8 and IHS 8 which
are covered here.

If you are running WebSphere855, please refer to [Configuring Enterprise
CLM Reverse Proxies: WebSphere 8.5.5 and IHS
8.5.5](ConfigureCLMEnterpriseReverseProxy855)

## Other topics in this series

-   [Understanding reverse proxy](UnderstandingReverseProxy)
-   [Configuring Enterprise CLM Reverse Proxies: Apache and
    mod_proxy](ConfigureCLMEnterpriseReverseProxyWithApache)
-   [Configuring Enterprise CLM Reverse Proxies: WebSphere 8.5 ND
    Proxy](ConfiguringEnterpriseCLMReverseProxiesWebSphere85NDProxy)

## Configuring the WAS Web Server plugins with WAS 8 and IHS 8

There are two methods used to deploy the WAS Web Server plugins
depending on whether IHS and the WAS profiles are
[local](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.nd.doc/info/ae/ae/tins_webplugins_local.html)
or
[remote](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.nd.doc/info/ae/ae/tins_webplugins_remotesa.html).
To demonstrate both methods, we will assume that the JTS, RM application
server profiles are co-located with the IHS server (local), with the QM
and CCM applications each on their own servers (remote).

The user accessible Public URIs (and the actual servers they redirect
to) will be:BR https://clm.example.org/qm
(https://qmserver01.example.org:9443/qm)BR https://clm.example.org/jts
(https://clm.example.org:9447/jts)BR https://clm.example.org/rm
(https://clm.example.org:9448/rm)BR https://clm.example.org/ccm
(https://ccmserver01.example.org:9449/ccm)

We will also configure single sign-on with WAS such that a user only
needs to log into one of the products and subsequent access to the other
applications will not require re-authentication.BR Experienced WAS
administrators will be aware that the WAS configuration steps in this
guide can be carried out in different ways using "wsadmin" or the WAS
Integrated Solutions console.

N.B. Note that all of the setup and configuration documented here MUST
be done **before** running the JTS setup wizard to ensure that the
public URIs are set correctly to the external URIs.

#### Example server configuration

For the purposes of this article we use three separate servers
configured as follows:

-   Server 1 (Host-name: clm.example.org):
    -   IBM HTTP Server already installed, listening on port 80 with the
        IHS Administrative console on port 8008
    -   WAS profile with JTS, Admin and CLMHelp applications deployed
        (HTTPS port : 9447)
    -   WAS profile with RM WAR deployed (HTTPS port : 9448)
-   Server 2 (Host-name: qmserver01.example.org):
    -   WAS profile hosting QM (HTTPS port: 9443)
-   Server 3 (Host-name:ccmserver01.example.org):
    -   WAS profile hosting CCM (HTTPS port: 9449)

#### Prerequisites and assumptions

-   Base Websphere Application Server profiles are used (ie. not
    Websphere ND, which is covered by [this
    article](https://jazz.net/library/article/1123))
-   Use the instructions provided in the [CLM
    Infocenter](https://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/index.jsp)
    to deploy the different applications
-   Each of the WAS profiles is configured to use LDAP domain
    **"example.org"** for authentication
-   A separate database server is available
-   The [WebSphere Plug-ins for WebSphere Application Server Version 8.0
    have been
    installed](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.nd.doc/info/ae/ae/tins_installation_plugins.html)
    on server 1 to
-   Administrative console access to each WAS profile is available
-   [Username and password available for access to IHS Administrative
    console](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.ihs.doc/info/ihs/ihs/tihs_protconfigas.html)
-   Firewalls on the two servers are configured appropriate, allowing
    access to the internal ports only between the three servers. In
    other words ports 9443, 9447, 9448, 9449, 8008 are not visible to
    the outside world
-   The firewall on Server 1 allows access to port 443 from the outside
    world
-   Though the steps here were carried out in a Linux enviroment, their
    Windows equivalents will work as well.

## Procedure

\#CreateKey

### 1. Create a key database and self-signed certificate for IHS

In this step we create a [CMS](http://tools.ietf.org/html/rfc3852)
keystore database file and a self-signed certificate which are needed to
authenticate IHS during an SSL handshake. Note that Self-signed
certificates should only be used for test/development scenarios. In
production environments use the appropriate organizational certificates
provided by a trusted certificate authority. We will later add the WAS
certificates to this same keystore database.

Make sure the IHS Server is stopped. Run the
["gsk7cmd"](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.ihs.doc/info/ihs/ihs/cihs_ikeycmdline.html)
utility (alternatively use the
[ikeyman](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.ihs.doc/info/ihs/ihs/welc_ikeymangui.html)
GUI) to create a new keystore database (ihskeys.kdb) and password stash
file (ihskeys.sth) both of which will be created in the current
directory. gskcmd -keydb -create -db ihskeys.kdb -pw secret -expire 365
-stash -type cms

Create a self-signed certificate and add it to the the new keystore db

gskcmd -cert -create -db ihskeys.kdb -label clm.example.org -expire 365
-dn "CN=clm.example.org" -default_cert yes -pw secret

### 2. Enable SSL directives within the IBM HTTP Server's configuration file (httpd.conf)

In this step we need to first direct IHS to load the SSL support module
(mod_ibm_ssl.so) and then direct IHS to listen for secure requests (on
port 443 in this example). We also need to point IHS to the key database
file (**ihskeys.kdb**) and password stash file (**ihskeys.sth**) that
were created earlier. Add (or uncomment) the following lines in
httpd.conf, making sure that the values for the KeyFile and SSLStashFile
directives match the names (and paths) of the files generated in the
previous section:

LoadModule ibm_ssl_module modules/mod_ibm_ssl.so

Listen 0.0.0.0:443 \## Uncomment for IPv6 support: \#Listen \[::\]:443

SSLEnable

KeyFile /opt/IBM/HTTPServer/bin/ihskeys.kdb SSLStashFile
/opt/IBM/HTTPServer/bin/ihskeys.sth SSLDisable

\#SetupSSLHandshake

### 3. Setup SSL Handshake between the WAS profiles and IHS

Now we need to proxy SSL requests from IHS to the WAS servers by
exporting the WAS keys and importing them into the IHS keystore database
previously created.

1.  Login to the WAS Integration Solutions Console for the JTS profile.
2.  Navigate to **Security -\> SSL certificate and key management -\>
    Key Stores and Certificates**, create a new Key store with the
    following values:BR **Name:** jtswaskeysBR **Path:**
    jtswaskeys.kdbBR **Type:** CMSKSBR **Password:** secretBR BR
3.  Click **OK** then **Save**. This will create the file ENCODE{
    "/etc/jtswaskeys.kdb" type="entity" }.
4.  Navigate to \*SSL certificate and key management -\> Key stores and
    certificates -\> NodeDefaultKeyStore\*
5.  Choose "\*Personal certificates\*" from the right sidebar
6.  Check the default certificate and click **Export**.
7.  Specify the following values in the Export certificates pane:BR
    **Key Store Password:** WebAS (unless this has been changed)BR
    Select the **"Key Store File"** radio buttonBR **Key File Name:**
    ENCODE{ "/etc/jtswaskeys.kdb" type="entity" }BR **Type:** CMSKSBR
    **Password:** secretBR BR
8.  Click **OK**. This will export the default WAS personal certificates
    into **`/etc/jtswaskeys.kdb`**.
9.  Add the certificates from the exported keystore (jtswaskeys.kdb)
    into the previously created IHS keystore(ihskeys.kdb).

gskcmd -cert -import -db /etc/jtswaskeys.kdb -pw secret -type cms
-target ihskeys.kdb -target_pw secret -target_type cms -label default
-new_label default_jtswasBR

Repeat the above steps, changing the value of Key File Name as
appropriate for each of the CCM(ccmwaskeys.kdb), RM (rmwaskeys.kdb)and
QM profiles (qmwaskeys.kdb). Note that since the CCM and QM WAS profiles
are **not** co-located with the IHS server, we first need to copy
"qmwaskeys.kdb" and "ccmwaskeys.kdb" to the IHS server. \#ForceWAS

### 4. Force WAS to honor host headers

To avoid a problem with Jazz redirecting to :9443 ports on the IHS
Server we need to set a couple of Web Container custom properties in
WAS. Failure to set these properties can also result in the "Finalize"
button in the last step of the JTS setup wizard to be greyed out.

1.  Login to the WAS Integration Solutions Console for each WAS profile
    and navigate to **Servers -\> Server Types -\> WebSphere application
    servers -\> server1**
2.  Under **"Container Settings"** expand Web Container Settings. Choose
    **"Web Container"**.BR BR
3.  Add the following custom properties: trusthostheaderport = true

com.ibm.ws.webcontainer.extracthostheaderport = true

\#SSOWithWAS

### 5. Single Sign-On (SSO) with WAS

To allow sharing of authentication tokens between the different WAS
profiles, we need to enable the SSO property in each WAS profile, export
the LTPA (Lightweight Third Party Authentication) keys from one profile
and import them into each of the other profiles.

#### 5.1Setup JTS profile for SSO and export keys [setup-jts-profile-for-sso-and-export-keys]

1\. Login to the WAS Integration Solutions Console for the JTS WAS
profile. 1. Navigate to **Global Security -\> Web and SIP Security -\>
Single sign-on (SSO)** and set the following properties:BR **Enabled**
BR **Domain name**: example.orgBR **Requires SSL** BR BR 1. Click **OK**
then **Save**. 1. Navigate to **Global Security**, select **LTPA** and
enter the following values:BR **Password:** secretBR **Confirm
Password:** secret BR **Fully qualified key file name:**
ENCODE{"/etc/jtsssokey" type="entity"}BR 1. Click **Export keys**.BR

1.  Click **OK** then **Save**. This will create a file
    ENCODE{"/etc/jtsssokey" type="entity"} which we will import into the
    other WAS profiles.
2.  Stop and restart the JTS profile.

#### 5.2Setup RM, QM and CCM for SSO and import JTS keys [setup-rm-qm-and-ccm-for-sso-and-import-jts-keys]

1.  Copy the jtssokey generated above from ENCODE{"/etc" type="entity"}
    to ENCODE{"/etc/jtsssokey" type="entity"}
2.  Login to the WAS Integration Solutions Console for the **RM** WAS
    profile.
3.  Navigate to **Global Security -\> Web and SIP Security -\> Single
    sign-on (SSO)** and set the following properties:BR **Enabled** BR
    **Domain name:** example.orgBR **Requires SSL** BR BR
4.  Click **OK** then **Save**.
5.  Navigate to Global Security,select LTPA and enter the following
    values:BR **Password** : secretBR **Confirm Password:** secretBR
    **Fully qualified key file name:** ENCODE{"/etc/jtsssokey"
    type="entity"}BR
6.  Click **Import keys**.
7.  Click **OK** then **Save**.
8.  Stop and restart the RM profile.

Repeat the above steps for each of the CCM and QM profiles, copying the
jtsssokey file to the and respectively. \#ConfiguringAndTuningTheJTS

### 6. Configure WAS IHS Plug-in for JTS (Server 1)

We will now use the WAS Web Server Plug-ins Configuration Tool to
configure IHS such that all requests to https://clm.example.org/jts are
redirected to https://clm.example.org:9447/jts. As noted before, for the
purposes of this example,the WAS profile to which the JTS application
has been deployed is co-located on the same server as IHS. We therefore
use the procedure described in [Configuring a Web server and an
application server profile on the same
machine](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.base.doc/info/aes/ae/tins_webplugins_local.html).

The following steps are performed on "Server 1' which hosts both IHS and
the WAS profile hosting the JTS, Admin and CLMHelp applications.
\#GenerateJTS

#### 6.1Generate the plugin configuration file [generate-the-plugin-configuration-file]

1\. Stop the JTS WAS profile. 1. Stop IHS. 1. Launch the Plug-ins
Configuration Tool.BR

1\. Click **Add....** 1. Enter **"webserver1"** for Name and "/Plugins"
for **Location**. Click **Finish**. 1. Click create and choose **"IBM
HTTP Server V8"** for Web server type and click **Next**.BR

1\. Click **Browse** to select the configuration file for IHS, verify
that the Web server port is correct, and then click **Next** when you
are finished.BR

1\. Optionally configure access to the IBM HTTP Administration Server.
This not required but makes it easy to propagate the plugin
configuration file from the application server to the web server. 1.
Specify a unique nickname for the Web server. Click Next.BR 1. Select
**WebSphere Application Server machine (local)**, browse to the
installation directory and click **Next**.BR

1\. Select the profile that the JTS application is deployed to and click
**Next**.BR

1\. Click **Configure** on the Plug-in Configuration Summary panel. The
wizard begins configuring the Web server and the application server.
Note the path of the **Plug-in configuration file**, which we will use
later.BR

1.  Verify the success on the Plug-in Configuration Summary panel and
    click **Finish** to exit the wizard.

#### 6.2Modify keyring and stashfile properties [modify-keyring-and-stashfile-properties]

1.  Open the generated plugin configuration file
    (C:\IBM\HTTPServer\Plugins\config\webserver1\plugin-cfg.xml in this
    case) and modify the keyring and stashfile properties of the HTTPS
    Transport attributes to use the IHS keyfile and SSL Stashfile.

<!-- -->

1.  Start IHS and the JTS WAS profile.BR

First verify that you can access the JTS page using the "internal" URL:
https://clm.example.org:9447/jts. Next verify that the IHS URL
https://clm.example.org/jts displays the same page. \#ConfigureRM

### 7. Configure WAS IHS Plug-in for RM application (Server 1)

As noted before, for the purposes of this example, the WAS profile to
which the RM application has been deployed is co-located on the same
server as IHS and the JTS profile.BR This is similar to the procedure
used for the JTS with the exception that we will need to merge some of
the content from the plugin configuration file generated for the RM
profile into the plugin configuration file already created for the JTS.

The following steps are performed on "Server 1' which hosts both IHS and
the WAS profiles hosting the RM and JTS applications. \#GenerateRM

#### 7.1 Generate plugin configuration file [generate-plugin-configuration-file]

1.  Stop the RM WAS profile.
2.  Stop IHS.
3.  Copy the previously generated
    ENCODE{"/config/webserver1/plugin-cfg.xml" type="entity"} to another
    file such as ENCODE{"/config/webserver/jts-plugin-cfg.xml"
    type="entity"}.
4.  Launch the Plug-ins Configuration Tool on server1. Since the httpd
    file for the IHS server already contains the plugin entries for the
    JTS, the Plug-in configuration tool will balk at the Web Server
    Configuration File Selection pane (see Step 7 in Section 6.1). To
    get around this we first delete the previous configration (making
    sure we copied the config file in the previous step).BR BR
5.  Once the reference has been deleted , click Create and follow the
    same process as beforeBR \* choose the same httpd.conf file \* do
    not configure the HTTP Administration server as it has already been
    done \* specify "webserver1" for the web server definition \* choose
    WebSphere Application Server machine (local), browse to the
    installation directory and select the "RM" profile
6.  When the wizard completes, modify the keyring and stashfile
    properties as in Section 6.4, and copy the newly generated
    ENCODE{"/config/webserver1/plugin-cfg.xml" type="entity"} to
    ENCODE{"/config/webserver/rm-plugin-cfg.xml" type="entity"}

#### 7.2 Merge plugin directives [merge-plugin-directives]

We now need to merge in the appropriate sections from the plugin
configuration generated for the RM profile into the plugin configuration
generated for the JTS using the pluginCfgMerge tool.
wasinstall_root/bin/pluginCfgMerge.sh rm-plugin-cfg.xml jts-plugin-xml
plugin-cfg.xml

#### 7.3 Edit httpd.conf [edit-httpd.conf]

Open the IHS httpd.conf file in a text editor and change the
WebSpherePluginConfig directive to point to the merged plugin
configuration file. WebSpherePluginConfig
/config/webserver/plugin-cfg.xml Restart IHS.BR First verify that you
can still access the JTS page using the IHS URL
https://clm.example.org/jts.BR Next, verify that you can access the RM
page using the "internal" URL: https://clm.example.org:9448/rm. Next
verify that the IHS URL https://clm.example.org/rm displays the same
page. \#ConfigureQM

### 8. Configure WAS IHS Plug-in for the QM application (Server 2)

We will now use the WAS Web Server Plug-ins Configuration Tool to
configure IHS such that all requests to https://clm.example.org/qm are
redirected to https://qmserver01.example.org:9443/qm and. As noted
before, for the purposes of this example, the WAS profile to which the
QM application has been deployed is **not** co-located on the same
server as IHS. We therefore use the procedure in [Configuring a Web
server and an application server on separate machines
(remote)](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.nd.doc/info/ae/ae/tins_webplugins_remotesa.html).

The following steps are performed on "Server 1' which hosts IHS.

#### 8.1 Generate manual plugin configuration script [generate-manual-plugin-configuration-script]

1\. Stop IHS. 1. Copy the previously generated
ENCODE{"/config/webserver/plugin-cfg.xml" type="entity"} to another file
such as ENCODE{"/config/webserver/rm-jts-plugin-cfg.xml"
type="entity"}. 1. Launch the Plug-ins Configuration Tool on server1.
Again we first remove the reference to the previous file from the
Configuration tool.BR

1\. Once the reference has been deleted , click Create and follow the
same process as beforeBR \* choose the same httpd.conf file \* do not
configure the HTTP Administration server as it has already been done \*
specify "webserver1" for the web server definition \* choose (Remote)
application server and enter the host name of the QM ServerBR

1\. Once the installation completes, the wizard generates a manual
configuration script which must be run on the QM server. The path to the
script is displayed in the installation summary panel.BR

The following steps are performed on "Server 2' which hosts the WAS
profile hosting the QM application.

#### 8.2 Run manual configuration script on Server 2 [run-manual-configuration-script-on-server-2]

We now copy the manual configuration script generated above to the /bin
directory on Server 2.BR If the WAS profile hosting the QM application
isn't already running start it.BR Run the configurewebserver1.sh
script.BR If it runs successfully, a web server definition will have
been created in the QM application server profile. \#GenerateQM

#### 8.3 Propagate the QM plugin configuration file to the IHS server [propagate-the-qm-plugin-configuration-file-to-the-ihs-server]

1\. Login to the WAS Integration Solutions Console for the QM WAS
profile. 1. Navigate to Servers -\> Server Types -\> Web Servers 1.
Select "webserver_qm" and click "Generate Plug-in".BR

1\. Once the plugin file has been generated, select "webserver1" and
click "Propagate Plug-in".BR

If successful WAS will generate a message such as:InformationPLGC0048I:
The propagation of the plug-in configuration file is complete for the
Web server. qm.clm.example.org-node.webserver1.BR Note the path
displayed for the generated plugin configuration file on Server 1 which
is the IHS Server.

The following steps are performed on "Server1' which hosts IHS.

#### 8.4 Merge plugin directives [merge-plugin-directives-1]

We now need to merge in the appropriate sections from the plugin
configuration generated for the QM profile into the plugin configuration
that contains the merged directives for the JTS and RM profiles.BR
Remember that in step 8.1 we copied the /config/webserver/plugin-cfg.xml
to /config/webserver/rm-jts-plugin-cfg.xml. Run the pluginCfgMerge tool
to merge the contents of the new plugin-cfg.xml propagated from the QMBR
server.wasinstall_root/bin/pluginCfgMerge.sh
/config/webserver1/plugin-cfg.xml
/config/webserver/rm-jts-plugin-cfg.xml /config/webserver/plugin-cfg.xml

#### 8.5 Edit httpd.conf [edit-httpd.conf-1]

Open the IHS httpd.conf file in a text editor and change the
WebSpherePluginConfig directive to point to the merged plugin
configuration file. WebSpherePluginConfig
/config/webserver/plugin-cfg.xml" Restart IHS.BR First verify that you
can still access the JTS and RM pages using the IHS URL
https://clm.example.org/jts and https://clm.example.org:9448/rm.BR Next
verify that you can access the QM page using the "internal" URL:
https://qmserver01.example.org:9443/qm. and then verify that the IHS URL
https://clm.example.org/qm displays the same page.BR Copy the
ENCODE{"/config/webserver/plugin-cfg.xml" type="entity"} to another file
such as ENCODE{"/config/webserver/rm-jts-qm-plugin-cfg.xml"
type="entity"}. \#ConfigureCCM

### 9. Configure WAS IHS Plug-in for the CCM application (Server 3)

We will now configure IHS such that all requests to
https://clm.example.org/ccm are redirected to
https://ccmserver01.example.org:9443/ccm. As noted before, for the
purposes of this example, the WAS profile to which the QM application
has been deployed is **not** co-located on the same server as IHS. We
therefore use the procedure in [Configuring a Web server and an
application server on separate machines
(remote)](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.nd.doc/info/ae/ae/tins_webplugins_remotesa.html).
However we have already generated the manual configuration script for
the QM profile in Section 7. Since the script is designed to accept the
WAS profile name, administrative username and password as parameters we
can simply reuse it.

#### 9.1 Run manual configuration script generated for QM on Server 3 [run-manual-configuration-script-generated-for-qm-on-server-3]

The following steps are performed on "Server3' which hosts the CCM
profile.

1.  Copy the previously generated cofigurewebserver1.sh from Server 1 to
    the ENCODE{"/bin" type="entity"} directory.
2.  Run the script:BR wasinstall_root/bin/cofigurewebserver1.sh CCM
    username passwordBR If it runs successfully, a web server definition
    will have been created in the CCM application server profile.BR

\#PropagateCCM

#### 9.2 Propagate the CCM plugin configuration file to the IHS server [propagate-the-ccm-plugin-configuration-file-to-the-ihs-server]

1.  Login to the WAS Integration Solutions Console for the CCM WAS
    profile.
2.  Navigate to **Servers -\> Server Types -\> Web Servers**
3.  Select "webserver1" and click "Generate Plug-in".
4.  Once the plugin file has been generated, select "webserver1" and
    click "Propagate Plug-in".BR If successful, WAS will generate a
    message such as:BR InformationPLGC0048I: The propagation of the
    plug-in configuration file is complete for the Web server.
    ccm.clm.example.org-node.webserver1.BR

The following steps are performed on "Server1' which hosts IHS.
\#MergePluginDirectives

#### 9.3 Merge plugin directives [merge-plugin-directives-2]

We now need to merge in the appropriate sections from the plugin
configuration generated for the CCM profile into the plugin
configuration that contains the merged directives for the JTS, RM and QM
profiles.BR Remember that in step 8.5 we copied
ENCODE{"/config/webserver/plugin-cfg.xml" type="entity"} to
ENCODE{"/config/webserver/rm-jts-qm-plugin-cfg.xml type="entity"}. Run
the pluginCfgMerge tool to merge the contents of the new plugin-cfg.xml
propagated from the CCM server.BR wasinstall_root/bin/pluginCfgMerge.sh
/config/webserver1/plugin-cfg.xml
"/config/webserver/rm-jts-qm-plugin-cfg.xml
/config/webserver/plugin-cfg.xml

#### 9.4 Edit httpd.conf [edit-httpd.conf-2]

Open the IHS httpd.conf file in a text editor and change the
WebSpherePluginConfig directive to point to the merged plugin
configuration file.BR WebSpherePluginConfig
/config/webserver/plugin-cfg.xml" Restart IHS.BR First verify that you
can still access the JTS, QM and RM pages using the IHS URL
https://clm.example.org/jts, https://clm.example.org/rm and
https://clm.example.org/qm.BR Next verify that you can access the CCM
page using the "internal" URL: https://ccmserver01.example.org:9449/ccm.
and then verify that the IHS URL https://clm.example.org/ccm displays
the same page.

## Running the JTS setup wizard

Now that we have URLs that are server agnostic we can run the [JTS setup
wizard](https://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/topic/com.ibm.jazz.install.doc/topics/t_s_server_installation_setup_wizard.html)
and use these URLs when registering the applications. Here are the
discovery URLs that will be used:BR Requirements Management:
https://clm.example.org/rm/scrBR Quality Management:
https://clm.example.org/qm/scrBR Change and Configuration Management:
https://clm.example.org/ccm/scrBR Lifecycle Project Administration:
https://clm.example.org/admin/scrBR

## Moving an application

Now suppose that we wish to redeploy the RM application to it's own
separate server (for example, rmserver01.example.org) without affecting
users' ability to access it through https://clm.example.org/rm. Here is
a summary of the steps, previously detailed, to be repeated:

1.  Deploy the RM application to WAS on rmserver01.example.org
2.  Follow the instructions in the [CLM
    Infocenter](https://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/topic/com.ibm.jazz.install.doc/topics/c_deploying_was.html),
    making sure to copy over the directory that contains the indexes and
    configuration files, located at /server/conf/rm for the RM
    application from the original server.
3.  Setup SSL Handshake Between WAS profile on rmserver01.example.org
    and IHS on clm.example.org
4.  Follow the procedure detailed in [Setup SSL Handshake between the
    WAS profiles and
    IHS](ConfigureCLMEnterpriseReverseProxy#SetupSSLHandshake), creating
    a new "rmwaskeys.kdb" keystore from the new WAS profile, copying
    this keystore over to the IHS server and using gscmd to import it
    into the IHS keystore (ihskeys.kdb).
5.  Force WAS To Honor Host Headers
6.  Follow the procedure in [Force WAS to honor host
    headers](ConfigureCLMEnterpriseReverseProxy#ForceWAS) on the new WAS
    profile hosting the RM application.
7.  Setup Single Sign-On(SSO) with WAS and import JTS keys
8.  Follow the procedure in [Single Sign-On (SSO) with
    WAS](ConfigureCLMEnterpriseReverseProxy#SSOWithWAS) to set the
    domain name and import the keys from the jtsssokey key file.
9.  Configure WAS IHS Plug-in for the RM application
10. Follow the procedure in [Configure WAS IHS Plug-in for the CCM
    application (Server
    3)](ConfigureCLMEnterpriseReverseProxy#ConfigureCCM) to run the
    plugin configuration script for the RM profile and propagate the
    plugin configuration back to the IHS server
11. Replace plugin directives and edit the httpd.conf
12. Finally follow the procedure in [Merge plugin
    directives](ConfigureCLMEnterpriseReverseProxy#MergePluginDirectives),
    edit the httpd.conf file and restart IHS.

## Using the command line

Many of the steps documented carried out via the GUI or the WAS Admin
Console also have command line or wasadmin equivalents listed below
against the relevant section.

[Section 1](#CreateKey): wsadmin
[AdminTask.createKeyStore](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.base.doc/info/aes/ae/rxml_atkeystore.html)
and
[AdminTask.exportCertificate](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.base.doc/info/aes/ae/rxml_atpersonalcert.html)BR
[Section 4](#ForceWAS): wsadmin
[AdminConfig.list](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.base.doc/info/aes/ae/rxml_adminconfig1.html)
and
[AdminConfig.create](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.base.doc/info/aes/ae/rxml_adminconfig1.html)BR
[Section 5](#SSOWithWAS): wsadmin
[AdminTask.configureSingleSignon](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.base.doc/info/aes/ae/rxml_7securityconfig.html)
and
[AdminTask.exportLTPAKeys](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.base.doc/info/aes/ae/rxml_7securityconfig.html)BR
Sections [6](#ConfiguringAndTuningTheJTS), [7](#ConfigureRM),
[8](#ConfigureQM), [9](#ConfigureCCM) : [Configuring a web server
plug-in using the pct
tool](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.base.doc/info/aes/ae/tins_pctcl_using.html)BR
Sections [6.1](#GenerateJTS), [7.1](#GenerateRM) , [8.3](#GenerateQM) ,
[9.2](#PropagateCCM) : [GenPluginCfg
command](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/topic/com.ibm.websphere.base.doc/info/aes/ae/rxml_genplugincfg1.html)

## References

-   [Collaborative Lifecycle Management 4.0.1 Information Center:
    Installation process and topology
    examples](https://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/topic/com.ibm.jazz.install.doc/topics/c_topology_overview.html)
-   [jazz.net: Moving Jazz Servers and URI Stability with CLM
    2011](https://jazz.net/library/article/686)
-   [Collaborative Lifecycle Management 4.0.1 Information Center:
    Reverse proxy servers in
    topologies](https://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/topic/com.ibm.jazz.install.doc/topics/c_reverse_proxy.html)
-   [WebSphere 8 Information
    Center](http://pic.dhe.ibm.com/infocenter/wasinfo/v8r0/index.jsp)
-   [Tip: Single Sign-on using WebSphere Application
    Server](https://jazz.net/library/article/413/)

##### Related topics: [Proxy server installation](InstallProxyServers), [Understanding reverse proxy](UnderstandingReverseProxy), [Configuring Enterprise CLM Reverse Proxies: Apache and mod_proxy](ConfigureCLMEnterpriseReverseProxyWithApache), [Configuring Enterprise CLM Reverse Proxies: WebSphere 8.5 ND Proxy](ConfiguringEnterpriseCLMReverseProxiesWebSphere85NDProxy) [related-topics-proxy-server-installation-understanding-reverse-proxy-configuring-enterprise-clm-reverse-proxies-apache-and-mod_proxy-configuring-enterprise-clm-reverse-proxies-websphere-8.5-nd-proxy]

##### Additional contributors: Main.RosaNaranjo [additional-contributors-main.rosanaranjo]

##### Questions and comments: [questions-and-comments]

COMMENT{type="below" target="ConfigureCLMEnterpriseReverseProxyComments"
button="Submit"}

INCLUDE{"ConfigureCLMEnterpriseReverseProxyComments"}

META:FILEATTACHMENT{name="LTPAexport.png" attachment="LTPAexport.png"
attr="h" comment="" date="1380036718" path="LTPAexport.png" size="12761"
user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="createjtswaskeys.png"
attachment="createjtswaskeys.png" attr="h" comment="" date="1380036750"
path="createjtswaskeys.png" size="12775" user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="exportjtswaskeys.png"
attachment="exportjtswaskeys.png" attr="h" comment="" date="1380036780"
path="exportjtswaskeys.png" size="10813" user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="qm_webgenerate.png"
attachment="qm_webgenerate.png" attr="h" comment="" date="1380044157"
path="qm_webgenerate.png" size="12607" user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="qm_webgpropagate.png"
attachment="qm_webgpropagate.png" attr="h" comment="" date="1380044175"
path="qm_webgpropagate.png" size="12451" user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="selectwebcontainer.png"
attachment="selectwebcontainer.png" attr="h" comment=""
date="1380045257" path="selectwebcontainer.png" size="17896"
user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="webcontainercustom.png"
attachment="webcontainercustom.png" attr="h" comment=""
date="1380045311" path="webcontainercustom.png" size="8843"
user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="websipssosetting.png"
attachment="websipssosetting.png" attr="h" comment="" date="1380045750"
path="websipssosetting.png" size="16607" user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="webserverplugininstall01.png"
attachment="webserverplugininstall01.png" attr="h" comment=""
date="1380048644" path="webserverplugininstall01.png" size="30839"
user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="webserverplugininstall03.png"
attachment="webserverplugininstall03.png" attr="h" comment=""
date="1380048657" path="webserverplugininstall03.png" size="28978"
user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="webserverplugininstall04.png"
attachment="webserverplugininstall04.png" attr="h" comment=""
date="1380048671" path="webserverplugininstall04.png" size="41051"
user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="webserverplugininstall07.png"
attachment="webserverplugininstall07.png" attr="h" comment=""
date="1380048794" path="webserverplugininstall07.png" size="22960"
user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="webserverplugininstall09.png"
attachment="webserverplugininstall09.png" attr="h" comment=""
date="1380050910" path="webserverplugininstall09.png" size="37184"
user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="webserverplugininstall08.png"
attachment="webserverplugininstall08.png" attr="h" comment=""
date="1380050939" path="webserverplugininstall08.png" size="28797"
user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="webserverplugininstall11.png"
attachment="webserverplugininstall11.png" attr="h" comment=""
date="1380050957" path="webserverplugininstall11.png" size="37725"
user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="webserverplugininstall12.png"
attachment="webserverplugininstall12.png" attr="h" comment=""
date="1380053152" path="webserverplugininstall12.png" size="37815"
user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="webserverplugininstall13.png"
attachment="webserverplugininstall13.png" attr="h" comment=""
date="1380053171" path="webserverplugininstall13.png" size="38907"
user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="webserverplugininstall14.png"
attachment="webserverplugininstall14.png" attr="h" comment=""
date="1380053188" path="webserverplugininstall14.png" size="37985"
user="rnaranjo" version="1"}
