META:TOPICINFO{author="din" date="1704364117" format="1.1"
version="1.3"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Configure IHS as reverse proxy on local or remote Linux or Windows machine with ELM using command line DKGRAY Author: Abdulhusain Hamid Build basis: ELM 7.0.2; WAS 9.0.5.1; IHS 9.0.5.1; Plugins 9.0.5.1; RHEL 7.9; Windows Server 2016. [configure-ihs-as-reverse-proxy-on-local-or-remote-linux-or-windows-machine-with-elm-using-command-line-dkgray-author-abdulhusain-hamid-build-basis-elm-7.0.2-was-9.0.5.1-ihs-9.0.5.1-plugins-9.0.5.1-rhel-7.9-windows-server-2016.]

ENDCOLOR

TOC{title="Configure IHS as reverse proxy on local or remote Linux or
Windows machine with ELM using command line"}

`Note: Support removed for IBM !WebSphere Application Server (Traditional WAS) starting with ELM version 7.0.3. Use !WebSphere Liberty, either embedded and installed with ELM applications, or separately installed`

This web page will assist configuring IHS as reverse proxy on local or
remote Linux or Windows machine with ELM using command line. This will
cover generating IHS kdb file, adding certificate into kdb file,
updating httpd.conf file, creating WAS profile, updating few properties
on WAS profile, creating IHS Web Server on WAS profile and merging
plugin-cfg.xml through command line.

## Windows:

### Install IHS (C:\IBM\WebSphere\HTTPServer) and WebSphere Plugin (C:\IBM\WebSphere\Plugins) on local or remote machine

Add below line in file
C:\IBM\WebSphere\HTTPServer\java\8.0\jre\lib\security\java.security

security.provider.10=com.ibm.security.cmskeystore.CMSProvider (This step
is required for ikeyman GUI tool)

### Generate IHS_key.kdb file on IHS machine

C:\IBM\WebSphere\HTTPServer\bin\>

gskcapicmd.bat -keydb -create -db IHS_key.kdb -pw secret -expire 365
-stash -type cms

### Add certificate to it

gskcapicmd.bat -cert -create -db IHS_key.kdb -label
winserv.test.clms.com -expire 365 -dn "CN=winserv.test.clms.com"
-default_cert yes -pw secret

### Update httpd.conf at C:\IBM\WebSphere\HTTPServer\conf on IHS machine

LoadModule ibm_ssl_module modules/mod_ibm_ssl.so

Listen 0.0.0.0:443

SSLEnable

KeyFile C:/IBM/WebSphere/HTTPServer/bin/IHS_key.kdb

SSLStashFile C:/IBM/WebSphere/HTTPServer/bin/IHS_key.sth

SSLDisable

### Install WAS and create WAS profile. Install ELM webapps.

C:\IBM\WebSphere\AppServer\bin\>manageprofiles.bat -create -profileName
ELMSrvr -templatePath
C:\IBM\WebSphere\AppServer\profileTemplates\default -profilePath
C:\IBM\WebSphere\AppServer\profiles\ELMSrvr -enableAdminSecurity true
-adminUserName wasadmin -adminPassword wasadmin -omitAction
samplesInstallAndConfig

C:\IBM\WebSphere\AppServer\profiles\ELMSrvr/bin\> wsadmin.bat -lang
jython -user wasadmin -password wasadmin -f
C:\IBM\JazzTeamServer\server\was\clm_was_config.py
C:\IBM\JazzTeamServer\server\conf

wsadmin.bat -lang jython -user wasadmin -password wasadmin -f
C:\IBM\JazzTeamServer\server\was\clm_deploy_distributed.py winservNode01
server1 C:\IBM\JazzTeamServer\server\webapps qm,rm -config
C:\IBM\JazzTeamServer\server\was

### Update few properties on WAS profile using following commands:

C:\IBM\WebSphere\AppServer\profiles\ELMSrvr\bin\>startServer.bat server1
-profileName ELMSrvr

C:\IBM\WebSphere\AppServer\profiles\ELMSrvr\bin\>wsadmin.bat -lang
jython -user wasadmin -password wasadmin -c
"AdminConfig.create('Property',
AdminConfig.list('WebContainer',AdminConfig.getid('/Server:server1/')),
'\[\[name trusthostheaderport\] \[value true\]\]')"

C:\IBM\WebSphere\AppServer\profiles\ELMSrvr\bin\>wsadmin.bat -lang
jython -user wasadmin -password wasadmin -c
"AdminConfig.create('Property',
AdminConfig.list('WebContainer',AdminConfig.getid('/Server:server1/')),
'\[\[name com.ibm.ws.webcontainer.extracthostheaderport\] \[value
true\]\]')"

### Create IHS Web Server on WAS profile (IHS must be installed on local or remote machine before creating IHS Web Server):

C:\IBM\WebSphere\AppServer\profiles\ELMSrvr\bin\>wsadmin.bat -lang
jython -user wasadmin -password wasadmin -c
"AdminTask.createWebServerByHostName('\[-webserverName ELMSrvr
-templateName IHS -webPort 80 -serviceName IBMHTTPServerV9.0
-webInstallRoot C:\IBM\WebSphere\HTTPServer -webProtocol HTTP
-configurationFile -errorLogfile -accessLogfile -pluginInstallRoot
c:\IBM\WebSphere\Plugins -webAppMapping ALL -hostName
winserv.test.clms.com -platform windows -adminPort 8008 -adminUserID
wasadmin -adminPasswd wasadmin -adminProtocol HTTP\]')"

### Update plugin-key.kdb pwd on WAS machine: (These steps can be carried out on IHS machine too)

C:\IBM\WebSphere\AppServer\profiles\ELMSrvr\config\cells\winservNode01Cell\nodes\winservNode01\servers\ELMSrvr\>C:\IBM\WebSphere\HTTPServer\bin\gskcapicmd.bat
-cert -list -db plugin-key.kdb -pw WebAS

C:\IBM\WebSphere\AppServer\profiles\ELMSrvr\config\cells\winservNode01Cell\nodes\winservNode01\servers\ELMSrvr\>C:\IBM\WebSphere\HTTPServer\bin\gskcapicmd.bat
-keydb -stashpw -db plugin-key.kdb -pw WebAS

C:\IBM\WebSphere\AppServer\profiles\ELMSrvr\config\cells\winservNode01Cell\nodes\winservNode01\servers\ELMSrvr\>C:\IBM\WebSphere\HTTPServer\bin\gskcapicmd.bat
-cert -list -db plugin-key.kdb -pw WebAS

### Copy files from WAS machine to IHS machine

Copy files from WAS machine
C:\IBM\WebSphere\AppServer\profiles\ELMSrvr\config\cells\winservNode01Cell\nodes\winservNode01\servers\ELMSrvr
to IHS machine C:\IBM\WebSphere\Plugins\config\ELMSrvr

### Update C:\IBM\WebSphere\HTTPServer\conf\httpd.conf file on IHS machine with below lines:

LoadModule was_ap24_module
"C:\IBM\WebSphere\Plugins\bin\32bits\mod_was_ap24_http.dll"

WebSpherePluginConfig
"C:\IBM\WebSphere\Plugins\config\ELMSrvr\plugin-cfg.xml"

### Restart IHS using Windows Service or command line tool.

### Verify, if IHS port 443 is listening and forwarding requests to respective ELM app.

If IHS is configured to forward requests to multiple WAS profiles, then,
follow above steps for 2nd and more profiles.

### Merge plugin-cfg.xml using following command.

C:\IBM\WebSphere\AppServer\bin\>pluginCfgMerge.bat
C:\IBM\WebSphere\Plugins\config\ELMSrvr\plugin-cfg.xml
C:\IBM\WebSphere\Plugins\config\ELMSrvr2\plugin-cfg.xml
C:\IBM\WebSphere\Plugins\config\merged_plugins\plugin-cfg.xml

### Update C:\IBM\WebSphere\HTTPServer\conf\httpd.conf file for merged profile.

LoadModule was_ap24_module
"C:\IBM\WebSphere\Plugins\bin\32bits\mod_was_ap24_http.dll"

WebSpherePluginConfig
"C:\IBM\WebSphere\Plugins\config\merged_plugins\plugin-cfg.xml"

### Restart IHS.

JTS and CCM are deployed on one WAS profile.

<https://winserv.test.clms.com:9443/jts>

<https://winserv.test.clms.com:9443/ccm>

RM and QM are deployed on second WAS profile on same machine.

<https://winserv.test.clms.com:9444/rm>

<https://winserv.test.clms.com:9444/qm>

Above ELM apps are configured with local IHS as reverse proxy and can be
accessible through below local IHS URLs too.

<https://winserv.test.clms.com:443/jts>

<https://winserv.test.clms.com:443/ccm>

<https://winserv.test.clms.com:443/rm>

<https://winserv.test.clms.com:443/qm>

Above ELM apps are configured with remote IHS as reverse proxy and can
be accessible through below remote IHS URLs

<https://winserv2.test.clms.com:443/jts>

<https://winserv2.test.clms.com:443/ccm>

<https://winserv2.test.clms.com:443/rm>

<https://winserv2.test.clms.com:443/qm>

### Configure WAS with ELM using repotools.

## Linux:

### Install IHS (/opt/IBM/WebSphere/HTTPServer) and WebSphere Plugin (/opt/IBM/WebSphere/Plugins) on local or remote machine

### Generate IHS_key.kdb file on IHS machine

/opt/IBM/WebSphere/HTTPServer/bin\]#

gskcapicmd -keydb -create -db IHS_key.kdb -pw secret -expire 365 -stash
-type cms

### Add certificate to it

gskcapicmd -cert -create -db IHS_key.kdb -label linserv.test.clms.com
-expire 365 -dn "CN=linserv.test.clms.com" -default_cert yes -pw secret

### Update httpd.conf at /opt/IBM/WebSphere/HTTPServer/conf on IHS machine

LoadModule ibm_ssl_module modules/mod_ibm_ssl.so

Listen 443

SSLEnable

KeyFile /opt/IBM/WebSphere/HTTPServer/bin/IHS_key.kdb

SSLStashFile /opt/IBM/WebSphere/HTTPServer/bin/IHS_key.sth

SSLDisable

### Install WAS and create WAS profile. Install ELM webapps.

/opt/IBM/WebSphere/AppServer/bin\]#

./manageprofiles.sh -create -profileName ELMSrvr -templatePath
/opt/IBM/WebSphere/AppServer/profileTemplates/default -profilePath
/opt/IBM/WebSphere/AppServer/profiles/ELMSrvr -enableAdminSecurity true
-adminUserName wasadmin -adminPassword wasadmin -omitAction
samplesInstallAndConfig

/opt/IBM/WebSphere/AppServer/profiles/ELMSrvr/bin\]#

./wsadmin.sh -lang jython -user wasadmin -password wasadmin -f
/opt/IBM/JazzTeamServer/server/was/clm_was_config.py
/opt/IBM/JazzTeamServer/server/conf

./wsadmin.sh -lang jython -user wasadmin -password wasadmin -f
/opt/IBM/JazzTeamServer/server/was/clm_deploy_distributed.py
linservNode01 server1 /opt/IBM/JazzTeamServer/server/webapps qm,rm
-config /opt/IBM/JazzTeamServer/server/was

### Update few properties on WAS profile using following commands.

/opt/IBM/WebSphere/AppServer/profiles/ELMSrvr/bin\]#

./startServer.sh server1 -profileName ELMSrvr

./wsadmin.sh -lang jython -user wasadmin -password wasadmin -c
"AdminConfig.create('Property',
AdminConfig.list('WebContainer',AdminConfig.getid('/Server:server1/')),
'\[\[name trusthostheaderport\] \[value true\]\]')"

./wsadmin.sh -lang jython -user wasadmin -password wasadmin -c
"AdminConfig.create('Property',
AdminConfig.list('WebContainer',AdminConfig.getid('/Server:server1/')),
'\[\[name com.ibm.ws.webcontainer.extracthostheaderport\] \[value
true\]\]')"

### Restart WAS profile.

### Create IHS Web Server on WAS profile (IHS must be installed on local or remote machine before creating IHS Web Server)

./wsadmin.sh -lang jython -user wasadmin -password wasadmin -c
"AdminTask.createWebServerByHostName('\[-webserverName ELMSrvr
-templateName IHS -webPort 80 -webInstallRoot
/opt/IBM/WebSphere/HTTPServer -webProtocol HTTP -configurationFile
-errorLogfile -accessLogfile -pluginInstallRoot
/opt/IBM/WebSphere/Plugins -webAppMapping ALL -hostName
linserv.test.clms.com -platform linux -adminPort 8008 -adminUserID
wasadmin -adminPasswd wasadmin -adminProtocol HTTP\]')"

### Update plugin-key.kdb pwd on WAS machine: (These steps can be carried out on IHS machine too)

/opt/IBM/WebSphere/AppServer/profiles/ELMSrvr/config/cells/linservNode01Cell/nodes/linservNode01/servers/ELMSrvr\]#

/opt/IBM/WebSphere/HTTPServer/bin/gskcapicmd -cert -list -db
plugin-key.kdb -pw WebAS

/opt/IBM/WebSphere/HTTPServer/bin/gskcapicmd -keydb -stashpw -db
plugin-key.kdb -pw WebAS

/opt/IBM/WebSphere/HTTPServer/bin/gskcapicmd -cert -list -db
plugin-key.kdb -pw WebAS

### Copy files from WAS machine to IHS machine

Copy files from WAS machine
/opt/IBM/WebSphere/AppServer/profiles/ELMSrvr/config/cells/linservNode01Cell/nodes/linservNode01/servers/ELMSrvr
to IHS machine /opt/IBM/WebSphere/Plugins/config/ELMSrvr

### Update /opt/IBM/WebSphere/HTTPServer/conf/httpd.conf file on IHS machine with below lines:

LoadModule was_ap24_module
"/opt/IBM/WebSphere/Plugins/bin/64bits/mod_was_ap24_http.so"

WebSpherePluginConfig
"/opt/IBM/WebSphere/Plugins/config/ELMSrvr/plugin-cfg.xml"

### Restart IHS.

/opt/IBM/WebSphere/HTTPServer/bin\]#

./apachectl stop

./apachectl start

### Verify, if IHS port 443 is listening and forwarding requests to respective ELM app.

If IHS is configured to forward requests to multiple WAS profiles, then,
follow above steps for 2nd and more profiles.

### Merge plugin-cfg.xml using following command.

/opt/IBM/WebSphere/AppServer/bin\]#

./pluginCfgMerge
/opt/IBM/WebSphere/Plugins/config/ELMSrvr/plugin-cfg.xml
/opt/IBM/WebSphere/Plugins/config/ELMSrvr2/plugin-cfg.xml
/opt/IBM/WebSphere/Plugins/config/merged_plugins/plugin-cfg.xml

### Update /opt/IBM/WebSphere/HTTPServer/conf/httpd.conf file for merged profile.

LoadModule was_ap24_module
"/opt/IBM/WebSphere/Plugins/bin/64bits/mod_was_ap24_http.so"

WebSpherePluginConfig
"/opt/IBM/WebSphere/Plugins/config/merged_plugins/plugin-cfg.xml"

### Restart IHS.

JTS and CCM are deployed on one WAS profile.

<https://linserv.test.clms.com:9444/jts>

<https://linserv.test.clms.com:9444/ccm>

RM and QM are deployed on second WAS profile on same machine.

<https://linserv.test.clms.com:9445/rm>

<https://linserv.test.clms.com:9445/qm>

Above ELM apps are configured with local IHS as reverse proxy and can be
accessible through below local IHS URLs too.

<https://linserv.test.clms.com:443/jts>

<https://linserv.test.clms.com:443/ccm>

<https://linserv.test.clms.com:443/rm>

<https://linserv.test.clms.com:443/qm>

Above ELM apps are configured with remote IHS as reverse proxy and can
be accessible through below remote IHS URLs

<https://linserv2.test.clms.com:443/jts>

<https://linserv2.test.clms.com:443/ccm>

<https://linserv2.test.clms.com:443/rm>

<https://linserv2.test.clms.com:443/qm>

### Configure WAS with ELM using repotools.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
