META:TOPICINFO{author="sbagot" date="1432743194" format="1.1"
reprev="1.13" version="1.13"}
META:TOPICPARENT{name="IntegrationsTroubleshootingRTCandIntegratedDevelopmentEnvironments"}

# Troubleshooting the installation of the Rational Team Concert Client on version 9 of IBM IDEs [troubleshooting-the-installation-of-the-rational-team-concert-client-on-version-9-of-ibm-ides]

DKGRAY Authors: Main.IntegrationsTroubleshootingTeam Build basis: RTC
4.0.3 and later, Rational Application Developer 9, Rational Software
Architect 9, Rational Developer for Z 9, Rational Business Developer 9,
Rational Developer for i 9 ENDCOLOR

TOC{title="Page contents"}

The version 9 of the IBM integrated development environments (IDEs) is
based on Eclipse 4.2. The first version of Rational Team Concert Client
that supports Eclipse 4.2 is version 4.0.3. Depending on the Operating
System, there are different ways of installing the Rational Team Concert
Client on Rational Application Developer 9, Rational Software Architect
9, Rational Developer for Z 9, Rational Business Developer 9, Rational
Developer for i 9. There are also different packages of the Rational
Team Concert Client for Eclipse that must be used in the different
cases. This document explains common error messages and the successful
installation procedure for different Operating Systems.

## How to verify that two products are compatible

Before you start the installation, review this page to verify that the
versions you have selected are compatible with each other: [How To
Verify That Two Products Are
Compatible](https://jazz.net/wiki/bin/view/Deployment/HowToVerifyThatTwoProductsAreCompatible)

## How to verify that a product supports a given operating system

Not all IDEs listed in this document support all Operating Systems
mentioned in this article. You can check to see if your IDE supports a
given Operating System using this form: [Operating systems for a
specific
product](http://www.ibm.com/software/reports/compatibility/clarity/osForProduct.html)

## Windows/Linux operating systems

On Microsoft Windows/Linux operating systems, you can install Rational
Team Concert Client for Eclipse using IBM Installation Manager.

### Problem

If you download the package called:

Client for Eclipse IDE (Extension Install)

and attempt to install it, you will get the following error:

Rational Team Concert - Client Extension for Eclipse 3.x 4.0.4 cannot be
installed into any package group. CRIMA1071E: The installation package
'Rational Team Concert - Client Extension for Eclipse 3.x' requires
components supplied by other packages. - No installation package
information provided.

This is due to the fact that the Extension is only compatible with
Eclipse 3.x.

### Resolution

You need to download the following package instead:

Client for Eclipse 4.2.x IDE

After installing the desired IDE, install the above package in the same
package group as the IDE, as follows.

1 Unzip the file: RTC-Client-Eclipse4.2-repo-4.0.4.zip (your version
number might differ) 1 Open **IBM Installation Manager** 1 Open **File
\> Preferences \> Repositories** 1 Click on **Add Repository** and
browse to the location of the extracted repository:

\[PATH\]\im\repo\rtc-client-ext-offering\offering-repo\repository.config

1 Click **OK** 1 Click **Install** 1 Select: **Rational Team Concert -
Cient for Eclipse IDE 4.2** and the desired version:

1 If desired, click on: **Check for other Versions, Fixes and
Extensions** 1 Click **Next** 1 Select **Accept the Terms in the License
Agreement** 1 Click **Next** 1 Select the existing package group where
the IDE is installed. In the screenshot below, you see an example where
**IBM Rational Software Architect for WebSphere Software** was installed
in the directory: C:\IBM\SDP, but your installation may differ:

1 Click **Next** 1 Select the desired features to install (Note: IBM
Sametime is a messaging system):

1 Click **Next** 1 Select how you want to access the Help system. The
default option is: **Access help from the Web** 1 Click **Next** 1 Click
on **Install**

1 At the end of the installation, you will see this screen:

1 Click on **Finish** 1 Exit **Installation Manager** 1 Launch the IDE
and activate Rational Team Concert Client by opening: **Windows \> Open
Perspective \> Other \> Work Items**

Note: If you have installed Rational Application Developer 9, Rational
Software Architect 9, Rational Developer for Z 9, Rational Business
Developer 9, Rational Developer for i 9 as an administrator into an
existing Eclipse 4.2.2 instance, review the following technical document
to see if it applies to your environment: [Non-administrator user cannot
install software by using Eclipse Software Installer in
V9.0](http://www-01.ibm.com/support/docview.wss?uid=swg21640442)

## MacOS operating system

On MacOS, you cannot install Rational Team Concert Client for Eclipse
using IBM Installation Manager.

### Problem

If you attempt to install the package:

Client for Eclipse 4.2.x IDE

with Installation Manager, you will see the error:

In plain text:

Package Rational Team Concert - Client for Eclipse 4.2.x IDE cannot be
installed on the current platform (operating system: macosx,
architecture: x86).

### Resolution

For a successful installation, proceed as follows:

1 Install the IDE first 1 Download the package called: p2 Install
Repository 1 Install the RTC Client plugin with the Eclipse p2 Installer
1 Go to the menu **Help \> Install New Software** to launch the
Installation wizard.

1 Click on the **Add** button to be able to enter the details of the
location of the RTC client p2 zip (**RTC-Client-p2Repo-4.0.x.zip**) 1
Enter the name of your choosing for the software site in the **Name**
field 1 Click on the **Archive** button to browse to the **location**
were you stored the RTC-Client-p2Repo-4.0.x.zip 1 Click **Ok**

1 Once you have created your installation repository site, the entry
**Rational Team Concert Client (extend an Eclipse installation)** will
be listed. Select the **Rational Team Concert Client Feature** entry and
click **Next**.

1 Verify in the **Installation Details** that the Name, Version and Id
matches the information shown in the screenshot below.

1 **Review the Licenses** and **accept** the **licenses agreement
terms**

1 Click **Ok** when prompted with the **Security Warning** dialog

1 Click **Yes** when prompted to **restart** the **IDE**

## Related Information

##### Related topics: [Integrations Troubleshooting](IntegrationsTroubleshooting) [Troubleshooting Rational Team Concert integration with Integrated Development Environments](IntegrationsTroubleshootingRTCandIntegratedDevelopmentEnvironments) [related-topics-integrations-troubleshooting-troubleshooting-rational-team-concert-integration-with-integrated-development-environments]

##### External links: [external-links]

-   [Products and prerequisites
    matrix](http://www.ibm.com/software/reports/compatibility/clarity/softwarePrereqsMatrix.html)
-   [Operating systems for a specific
    product](http://www.ibm.com/software/reports/compatibility/clarity/osForProduct.html)
-   [Non-administrator user cannot install software by using Eclipse
    Software Installer in
    V9.0](http://www.ibm.com/support/docview.wss?uid=swg21640442)
-   [Rational Team Concert 4.0.4 client for Eclipse 4.2 crashes when
    Rational Software Architect 9.0 is installed in the same IBM
    Installation Manager](https://jazz.net/library/article/1337#00001)
-   [Rational Team Concert 4.0.4 client for Eclipse 4.2 crashes with JVM
    segmentation error on SLES
    10](https://jazz.net/library/article/1337#00000)

##### Additional contributors: Main.LaraZiosi, Main.FrancoisPanaget [additional-contributors-main.laraziosi-main.francoispanaget]

META:FILEATTACHMENT{name="RTC403ClientInstalOnMacOSError.png"
attachment="RTC403ClientInstalOnMacOSError.png" attr="h" comment="Error
installing RTC client 4.0.3 or higher using Installation Manager on
MacOS" date="1386168150" path="RTC403ClientInstalOnMacOSError.png"
size="91846" user="fpanaget" version="1"}
META:FILEATTACHMENT{name="ErrorInstallingExtension.jpg"
attachment="ErrorInstallingExtension.jpg" attr="h" comment=""
date="1389623026" path="ErrorInstallingExtension.jpg" size="79466"
user="dmmckinn" version="2"}
META:FILEATTACHMENT{name="ConfigureRepository.jpg"
attachment="ConfigureRepository.jpg" attr="h" comment=""
date="1389629962" path="ConfigureRepository.jpg" size="67030"
user="dmmckinn" version="2"} META:FILEATTACHMENT{name="InstallRTC.jpg"
attachment="InstallRTC.jpg" attr="h" comment="" date="1386519837"
path="InstallRTC.jpg" size="154889" user="lziosi" version="1"}
META:FILEATTACHMENT{name="SelectExistingPackageGroup.jpg"
attachment="SelectExistingPackageGroup.jpg" attr="h" comment=""
date="1386520342" path="SelectExistingPackageGroup.jpg" size="178210"
user="lziosi" version="1"}
META:FILEATTACHMENT{name="SelectRTCFeatures.jpg"
attachment="SelectRTCFeatures.jpg" attr="h" comment="" date="1386520579"
path="SelectRTCFeatures.jpg" size="166009" user="lziosi" version="1"}
META:FILEATTACHMENT{name="InstallRTCFinal.jpg"
attachment="InstallRTCFinal.jpg" attr="h" comment="" date="1386520941"
path="InstallRTCFinal.jpg" size="133309" user="lziosi" version="1"}
META:FILEATTACHMENT{name="RTCInstallationConfirmation.jpg"
attachment="RTCInstallationConfirmation.jpg" attr="h" comment=""
date="1386521546" path="RTCInstallationConfirmation.jpg" size="110595"
user="lziosi" version="1"}
META:FILEATTACHMENT{name="OpenRTCPerspective.jpg"
attachment="OpenRTCPerspective.jpg" attr="h" comment=""
date="1386521928" path="OpenRTCPerspective.jpg" size="189434"
user="lziosi" version="1"}
META:FILEATTACHMENT{name="RTC404Clientp2Install1.png"
attachment="RTC404Clientp2Install1.png" attr="h" comment=""
date="1386695429" path="RTC404Clientp2Install1.png" size="71574"
user="fpanaget" version="1"}
META:FILEATTACHMENT{name="RTC404Clientp2Install2.png"
attachment="RTC404Clientp2Install2.png" attr="h" comment=""
date="1386695498" path="RTC404Clientp2Install2.png" size="100495"
user="fpanaget" version="1"}
META:FILEATTACHMENT{name="RTC404Clientp2Install3.png"
attachment="RTC404Clientp2Install3.png" attr="h" comment=""
date="1386695550" path="RTC404Clientp2Install3.png" size="88760"
user="fpanaget" version="1"}
META:FILEATTACHMENT{name="RTC404Clientp2Install4.png"
attachment="RTC404Clientp2Install4.png" attr="h" comment=""
date="1386695593" path="RTC404Clientp2Install4.png" size="47065"
user="fpanaget" version="1"}
META:FILEATTACHMENT{name="RTC404Clientp2Install5.png"
attachment="RTC404Clientp2Install5.png" attr="h" comment=""
date="1386695630" path="RTC404Clientp2Install5.png" size="104061"
user="fpanaget" version="1"}
META:FILEATTACHMENT{name="RTC404Clientp2Install6.png"
attachment="RTC404Clientp2Install6.png" attr="h" comment=""
date="1386695661" path="RTC404Clientp2Install6.png" size="26438"
user="fpanaget" version="1"}
META:FILEATTACHMENT{name="RTC404Clientp2Install7.png"
attachment="RTC404Clientp2Install7.png" attr="h" comment=""
date="1386695687" path="RTC404Clientp2Install7.png" size="22194"
user="fpanaget" version="1"}
