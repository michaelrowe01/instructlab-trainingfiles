META:TOPICINFO{author="swijenay" date="1403641185" format="1.1"
version="1.6"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Configuring Ubuntu for Rational Team Concert clients [configuring-ubuntu-for-rational-team-concert-clients]

DKGRAY Authors: Main.MichaelAfshar, Main.StephenGiesbrecht,
Main.SudarshaWijenayake Build basis: Rational Team Concert clients 3.x
and higher ENDCOLOR

TOC{title="Page contents"}

You must configure your Ubuntu system before you can use Rational Team
Concert clients.

## Configuring Rational Team Concert Eclipse client

### Before you begin

For the supported versions of Ubuntu client, see the [System
Requirements page](DeploymentInstallingUpgradingAndMigrating).

For the Rational Team Concert Eclipse client to display correctly in
Ubuntu, you must have the Mozilla XULRunner plug-in installed. The
XULRunner plug-in is not included in the Rational Team Concert Eclipse
client installation, therefore, the plug-in must be manually installed
if it does not exist on your system. To determine if your system
includes the XULRunner plug-in, open the Rational Team Concert Eclipse
client. If the Welcome screen looks like figure 1, the XULRunner plug-in
is missing.

*Figure 1: Welcome page with missing XULRunner plug-in*

Not all versions of Eclipse are compatible with all versions of
XULRunner. For a complete list of compatible versions, see
<http://eclipse.org/swt/faq.php#browserlinux>.

### Downloading a compatible version of XULRunner

If your operating system is 32-bit, you can download a compatible
version of XULRunner from
<http://ftp.mozilla.org/pub/mozilla.org/xulrunner/releases/>.

If you have a 64-bit operating system, you must download 64-bit binaries
from one of the nightly builds, as only the 32-bit versions are
available from the official releases. The main directory for nightly
builds can be found at
<http://ftp.mozilla.org/pub/mozilla.org/xulrunner/nightly/>.

Both the 3.6 and 4.2 versions of Eclipse support all releases of version
1.9.x of XULRunner. XULRunner 1.9.1 can be downloaded from
<http://ftp.mozilla.org/pub/mozilla.org/xulrunner/nightly/2009/12/2009-12-08-03-mozilla-1.9.1/>.

Both releases and nightly builds include SDK archives and runtime
archives. Only the runtime archive is required for running the Rational
Team Concert clients.

### Procedure

1 After downloading the required version of the XULRunner plug-in
archive, extract it to a directory on your drive, for example,
`/opt/IBM/TeamConcert/XULRunner`. 1 Go to the installation directory of
Rational Team Concert Eclipse client. 1 Open the eclipse.ini file for
editing and enter the following line at the end of the
<file:-Dorg.eclipse.swt.browser.XULRunnerPath=/opt/IBM/TeamConcert/XULRunner>
1 Save the eclipse.ini file and launch the Rational Team Concert Eclipse
client. If the Welcome screen looks like figure 2, XULRunner is working
properly.

*Figure 2: Welcome page with XULRunner plug-in properly installed*

## Configuring Build System Toolkit

Because Build System Toolkit is only available as a 32-bit binary, you
might have difficulty installing it on a 64-bit version of Ubuntu. If
you encounter the `jbe: no such file or directory` error message, or the
Jazz Build Engine crashes because it cannot find `jre/bin/java`, even
though the file does exist, you will need to enable support for 32-bit
architecture.

### Procedure

1 To confirm the default architecture for your computer, open a terminal
and enter: dpkg --print-architecture If the output is `amd64`, then you
must install libraries that support a 32-bit foreign architecture. 1 To
install the 32-bit packages, you must be logged into your terminal
session as root or have permission to execute commands by using sudo. In
your terminal enter the following command: apt-get install ia32-libs
This initiates a long package installation process that installs the
32-bit versions of the core libraries. 1 After installation completes,
confirm that the installation was successful by typing the following
command: dpkg --print-foreign-architectures If the installation was
successful, the output should be `i386`.

*Figure 3: Terminal with i386 output*

You should now be able to run the Jazz Build Engine normally.

##### Related topics: [related-topics]

##### External links: ---+++++! Additional contributors: [external-links-----additional-contributors]

META:FILEATTACHMENT{name="welcomePageNoXULRunner.png"
attachment="welcomePageNoXULRunner.png" attr="h" comment=""
date="1386359836" path="welcomePageNoXULRunner.png" size="92000"
user="mafshar" version="1"}
META:FILEATTACHMENT{name="welcomePageXULRunner.png"
attachment="welcomePageXULRunner.png" attr="h" comment=""
date="1386366021" path="welcomePageXULRunner.png" size="230924"
user="mafshar" version="1"} META:FILEATTACHMENT{name="i386.png"
attachment="i386.png" attr="h" comment="" date="1386373290"
path="i386.png" size="13069" user="mafshar" version="1"}
