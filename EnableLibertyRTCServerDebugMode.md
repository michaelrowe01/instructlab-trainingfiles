META:TOPICINFO{author="sbeard" date="1475147900" format="1.1"
version="1.3"} META:TOPICPARENT{name="WebPreferences"}

# How to enable RTC server in debug mode hosted on IBM Liberty profile DKGRAY Authors: Natarajan Thirumeni Build basis: Rational Team Concert, 6.0.1 runs on IBM WebSphere Liberty profile. [how-to-enable-rtc-server-in-debug-mode-hosted-on-ibm-liberty-profile-dkgray-authors-natarajan-thirumeni-build-basis-rational-team-concert-6.0.1-runs-on-ibm-websphere-liberty-profile.]

ENDCOLOR

TOC{title="Page contents"}

## Option used to enable DEBUG in RTC / Tomcat Server

In the past you've used Tomcat as application server and were able to
debug by using of the following options:

Option 1 Open the server.startup.bat Find the following line that starts
with the following. It is near the bottom of the file. set
JAVA_OPTS=JAVA_OPTS -Xdebug set JAVA_OPTS=JAVA_OPTS
-Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=8000

Option 2 /Tomcat/Bin Open startup.bat Change the second-last line from

call "EXECUTABLE" start CMD_LINE_ARGS to call "EXECUTABLE" jpda start
CMD_LINE_ARGS

None of these option is appears to be working in the RTC 601 WAS Liberty
server. They would work if you continue to use Tomcat as application
server in RTC 601.

### Steps to enable Liberty to listen DEBUG mode (LINUX)

Starting from RTC 6.0.1 version, IBM don't ship Tomcat Application
server (you're allowed to use Tomcat but isn't bundled within the
package) instead we ship IBM WAS Liberty application server. This is
light wight version of typical WAS application server.

Go to installation location of Jazz Team server 601 (path could be
different in every setup). In our case Jazz Team server is installed in
/opt/IBM/JazzTeamServer601/server

1\. Go to /opt/IBM/JazzTeamServer601/server

2\. Open liberty.server.sh in a editor

3\. Check WLP_DEBUG_ADDRESS port is set to a free port number.

JVM_ARGS="\$JAVA_OPTS" export JVM_ARGS WLP_DEBUG_ADDRESS=3388 export
WLP_DEBUG_ADDRESS 4. Make any changes required and save
liberty.server.sh

5\. Open server.startup.sh in a editor, check if iberty.server debug
option in the file. No changes required, close file.

if \[ "\$LIBERTY" = "true" \]; then if \[ "\$DEBUG" = "true" \]; then
./liberty.server debug; elif \[ "\$CREATE_ONLY" = "true" \]; then
./liberty.server create; else ./liberty.server start; fi; else if \[
"\$DEBUG" = "true" \]; then \$CATALINA_HOME/bin/catalina.sh jpda start;
else \$CATALINA_HOME/bin/startup.sh;

)

6\. Run the server with debug option

./liberty.server -debug

The print screen shows, the server is listening on port number 3399. At
this point, the server is not started, you need to attach to this
process to run the server. That's all on the server side.

Lets take a look at how to attach a remote debug process from the client
perspective. It can done on the client machine where it has access to
the RTC server.

1\. Open RTC Eclipse client (could also be done with a plain Eclipse
client for validation) 2. Switch to Java Perspective 3. From main menu
option, Run - Debug Configuration 4. Right Click on Remote Java
application 5. Choose New and provide the details of your RTC server
host and port number.

The print screen from our testing environment show, the RTC server is
running on myrts.demo.601.com and debug port number is 33388

6\. Click on Apply and hit on Debug button.

At this point you it will trigger a connection to your server, and start
the server in debug mode. You can monitor the server start activities in
the "message.log", which is located on the server side, Typically
opt/IBM/JazzTeamServer601/server/liberty/servers/clm/logs

## Heading 1

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]

-   Print screen shows, the remote host and port number of Jazz Team
    server:

META:FILEATTACHMENT{name="Eclipse_Remote_DebugOptions.jpg"
attachment="Eclipse_Remote_DebugOptions.jpg" attr="" comment="Print
screen shows, the remote host and port number of Jazz Team server"
date="1460559012" path="Eclipse_Remote_DebugOptions.jpg" size="72899"
user="natarajan_2ethirumeni" version="1"}
