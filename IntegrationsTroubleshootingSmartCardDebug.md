META:TOPICINFO{author="michaelrowe" date="1659376213" format="1.1"
version="1.13"}
META:TOPICPARENT{name="IntegrationsTroubleshootingSmartCard"}

# How to Enable Debug Trace for Smart Card issues? DKGRAY Authors: Main.ZeeshanChoudhry Build basis: IBM Rational Team Concert 3.x, 4.x, 5.x, 6.x, and IBM Engineering Workflow Management 7.x [how-to-enable-debug-trace-for-smart-card-issues-dkgray-authors-main.zeeshanchoudhry-build-basis-ibm-rational-team-concert-3.x-4.x-5.x-6.x-and-ibm-engineering-workflow-management-7.x]

ENDCOLOR

TOC{title="Page contents"}

This article explains what debug trace you need to enable for the client
and server to troubleshoot the Smart Card log-in issues with IBM
Engineering Workflow Management (EWM). You are required to enable trace
for IBM EWM Eclipse client, IBM EWM server, and IBM WebSphere. After
enabling the below trace, user can reproduce the issue and then collect
all the logs so that support can analyze them and find the root cause of
the problem.

-   Eclipse .log
-   ccm.log
-   jts.log
-   SystemOut.log

Its is preferred you collect ISALITE data from the server machine so you
collect all the logs from the Rational Team Concert server including
configuration files and IBM WebSphere logs.

## **Please note, some debug options on this page are no longer supported. It is advisable to open a Support Case if you are having issues beyond what is described here.**

## Debug Trace for IBM Engineering Workflow Management Eclipse Client.

Enable the Eclipse client debugging as follows:

1\. Find **logging.properties** (located within the same directory as
the eclipse.ini). If not present, create one.

for 5.x Clients:

.level = INFO

handlers = java.util.logging.FileHandler,
java.util.logging.ConsoleHandler
java.util.logging.ConsoleHandler.formatter =
java.util.logging.SimpleFormatter java.util.logging.ConsoleHandler.level
= ALL com.ibm.team.repository.transport.auth.Tracer.level = ALL
com.ibm.team.repository.transport.client.ClientHttpUtil.level = ALL
httpclient.wire.header.level = FINEST httpclient.wire.content.level =
FINEST httpclient.wire.level = FINEST httpclient.level = FINEST
org.apache.commons.httpclient.level=FINEST

for 6.x Clients:

com.ibm.team.repository.transport.auth.Tracer.level=ALL
com.ibm.team.repository.transport.client.RemoteTeamServer.level=ALL
org.apache.http.level = FINEST

for 7.x Clients:

com.ibm.team.repository.transport.auth.Tracer.level=ALL
com.ibm.team.repository.transport.client.RemoteTeamServer.level=ALL
org.apache.http.level = FINEST

2\. In **eclipse.ini** modify the end of the file to include the
following debug settings:

-Djavax.net.debug=all -Djava.util.logging.config.file=logging.properties

-   **NOTE**: Where the "exact path to" is replaced with C:\Program
    Files\IBM\TeamConcert\\ or wherever the application is installed on
    your host that contains the logging.properties file.

<!-- -->

-   **NOTE**: If the path to the logging.properties file has spaces, you
    can try to change "Program Files" to "Progra1" or use (for example)
    C:\IBM\logging.properties

<!-- -->

-   **NOTE**: If the customer is using hardware keystores (crypto
    cards), please also add the following entry in addition to the debug
    settings above to the eclipse.ini:

-Djava.security.debug=pkcs11impl

3\. Restart Eclipse client so the Settings added can be taken into
effect.

In combination with above settings , You should also enable the [debug
tracing for the IBM Engineering Workflow Management
Server](https://jazz.net/wiki/bin/view/Deployment/IntegrationsTroubleshootingSmartCardDebug#Debug_Trace_for_IBM_Rational_AN2)
and if needed [debug tracing for IBM
WebSphere](https://jazz.net/wiki/bin/view/Deployment/IntegrationsTroubleshootingSmartCardDebug#Debug_Trace_for_IBM_WebSphere)

## Debug Trace for IBM Engineering Workflow Management Eclipse Client SSL Handshake.

Enable the below tracing to get information about SSL Handshake between
IBM Rational Team Concert (RTC) Eclipse client and RTC server. It will
give you more information when you need to know which one of the smart
card's certificates is being used for authentication.

1\. Inside your \workspace\\metadata folder rename the existing .log
file to get a clean file. If at all possible use a new Eclipse Workspace
for this test.

2\. Launch the EWM Eclipse client.

3\. In Eclipse menu bar go to Windows \> Preferences \> Run/Debug \>
Console \> Make sure that 'Limit console output' is unchecked. ( This is
Important).

4\. Close the "Preferences" window using "Apply" and then click OK.

5\. In the Eclipse menu bar, go to Run -\> Run Configurations

6\. Select "Eclipse Application" form the list and then press the "New"
button.

7\. In the next window, click the "Arguments" tab and inside the "VM
Arguments" box, append the following option:

-Djavax.net.debug=true

Make sure you have a white space between each of the options in "VM
Arguments" box.

8\. If that line has -Djavax.net.debug=all in there, remove this option.

9\. Press "Apply" and then "Run" to start the new Eclipse instance to
reproduce the problem. If you get an error about a port being in use,
close all the windows and start over from step 1.

10\. In the runtime Eclipse environment that you launched in step 9,
Create a new RTC Repository connection.

11\. Log in using that new RTC repository connection created in step 10,
selecting your desired certificate from smart card and note the name of
the certificate you selected.

12\. When you see the login has failed you can close/exit the runtime
Eclipse environment you launched in step 9.

13\. In the first Eclipse window select all the text from the "Console
view" using a right click on Console view -\> Select All and Paste this
into a new text file. The "Console view" output is captured from the
first Eclipse instance which you used to launch the new runtime Eclipse
environment.

14\. Inside your \workspace\\metadata folder get the newly created .log
file for investigation.

You can correlate the above trace and .log information with all the
other traces for a complete picture.

## Debug Trace for IBM Engineering Workflow Management Server.

Enable the debug trace for the following for server: ( CCM and JTS
application)

Prior to versions 7.0.1 SR1 / 7.0.2 SR2:

1\. In the **log4j.properties** file of the CCM application, add the
following lines:

log4j.properties file is location in \server\conf\ccm

log4j.logger.com.ibm.team.repository.internal.service.auth.impl.IssueAuthToken=DEBUG
log4j.logger.com.ibm.team.repository.internal.service.auth.impl.JAuthHandler=DEBUG

2\. In the **log4j.properties** file of the JTS application, add the
following lines:

log4j.properties file is location in\server\conf\jts

log4j.logger.com.ibm.team.repository.internal.service.auth.impl.IssueAuthToken=DEBUG
log4j.logger.com.ibm.team.repository.internal.service.auth.impl.JAuthHandler=DEBUG

For versions 7.0.1 SR1 / 7.0.2 SR2 and beyond:

1\. In the **log4j2.xml** file of the CCM application, add the following
lines:

log4j2.xml file is location in \server\conf\ccm

2\. In the **log4j2.xml** file of the JTS application, add the following
lines:

log4j2.xml file is location in\server\conf\jts

3\. Reload the log4j properties using ?internal=true so the log4j
properties are taken into account.

<https://:/ccm/admin?internal=true#action=com.ibm.team.repository.admin.reloadLoggingSettings>
<https://:/jts/admin?internal=true#action=com.ibm.team.repository.admin.reloadLoggingSettings>

## Debug Trace for IBM WebSphere

**CAUTION**: These traces that you enable should be removed as soon as
you have reproduced the problem and collected the trace. This debug
trace cause a lot of noise in the WebSphere logs.

1\. In the WebSphere Application Server (WAS) Admin Console, navigate to

"Servers" -\> "Server Types" -\> "WebSphere application servers" -\>

2\. Under "Server Infrastructure", expand

"Java and Process Management" -\> "Process definition" -\> "Java Virtual
Machine"

3\. Add the following to the end of the Generic JVM Arguments box, save
to the master config, and restart the server for it to take hold

-Djavax.net.debug=ssl,handshake,data,trustmanager

4\. This will add debug trace of the SSL handshake to

//profiles//logs//SystemOut.log

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
