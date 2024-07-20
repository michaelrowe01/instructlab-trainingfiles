META:TOPICINFO{author="zeech" date="1432796888" format="1.1"
version="1.5"}
META:TOPICPARENT{name="IntegrationsTroubleshootingDebugRTCVSClient"}

# How to Enable Debug Trace in Visual Studio DKGRAY Authors: Main.ZeeshanChoudhry Build basis: IBM Rational Team Concert Microsoft Visual Studio Client 3.x and later [how-to-enable-debug-trace-in-visual-studio-dkgray-authors-main.zeeshanchoudhry-build-basis-ibm-rational-team-concert-microsoft-visual-studio-client-3.x-and-later]

ENDCOLOR

TOC{title="Page contents"}

This article explains how you can enable the debug tracing for IBM
Rational Team Concert Visual Studio client to find out the details about
a reported error or unexpected results. There are two ways to enable the
debug tracing.

## Modifying the configuration file of the Microsoft Visual Studio executable.

You would want to use this approach if the problem is related to the
start up of the Rational Team Concert Visual Studio client.

To get the Rational Team Concert trace logs, modify the Visual Studio
config file named: "devenv.exe.config" following the steps below. This
config file can be found in the same folder as "devenv.exe". For example
"C:\Program Files\Microsoft Visual Studio
11.0\Common7\IDE\devenv.exe.config":

Please note: Path is different for different versions of Microsoft
Visual Studio installations.

1\. Close Visual Studio and then open the above config file in Notepad.

2\. Go to the end of the file, you should see similar codes like the
following:

..................

3\. Before the

tag, paste in the following lines

4\. Save the file and close it.(4 is the highest tracing level)

5\. Now start Microsoft Visual Studio, try to re-produce the problem.

Rational Team Concert should start logging, the trace files can be found
at location where pointed by the "APPDATA" environment variable, under
IBM\Rational\Team Concert Visual Studio Client subdirectory. For
example, if APPDATA points to "C:\Documents and
Settings\kkishore\Application Data" the location of Rational Team
Concert logs will be found under "C:\Documents and Settings\\Application
Data\IBM\Rational\Team Concert Visual Studio Client"

In latest release the trace file can be found at:

C:\Users\\AppData\Roaming\IBM\Rational\Team Concert Client

## Using Rational Team Concert Built-in verbose tracing option.

You would want to use this approach if the problem is related to a use
case in the Visual Studio client.

For example:

\- Connecting to the Team Concert Repository

\- Loading Workspace

\- Creating a Change set.

1\. Start Microsoft Visual Studio.

2\. Go to Menu \> Team Concert \> Windows \> Team Concert log.

3\. Set the Trace level to verbose.

4\. Now Reproduce the problem.

5\. Once the problem is reproduced, in "Team Concert log window" , click
"Save Log Files"

6\. You will be prompted to save a RTCNetLogs.zip file in a desired
location.

7\. Select the desired location and click "Save".

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: None [additional-contributors-none]
