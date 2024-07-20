META:TOPICINFO{author="sbeard" date="1389528198" format="1.1"
version="1.4"} META:TOPICPARENT{name="DeploymentIntegrating"}

# Install the Rational Team Concert client for Eclipse 3.0.1 into an existing Eclipse 3.6.x using Installation Manager [install-the-rational-team-concert-client-for-eclipse-3.0.1-into-an-existing-eclipse-3.6.x-using-installation-manager]

DKGRAY Author: Main.SergioDeras Build basis: Rational Team Concert 3.0.1
ENDCOLOR

TOC{title="Page contents"}

The Rational Team Concert client for Eclipse 3.0.1 is built on top of
Eclipse 3.5.2 and bundles this version. It is also possible to install
the RTC 3.0.1 client into an existing Eclipse 3.6 with IBM Installation
Manager (IM), as RTC tolerates the Eclipse 3.6 features. This scenario
works with the Eclipse Classic 3.6 package. Other Eclipse packages
(e.g., Eclipse JEE and Eclipse RCP) do not contain all the features
required by RTC and they do not accept the Eclipse 3.5.2 features
packaged by RTC. RTC does support higher versions of these features,
which can be added to the Eclipse environment in order to install the
RTC components.

Note that Eclipse 3.7 (Indigo) is now available. RTC 3.0.1 does not
officially support this version but you can find the pieces that must be
installed in 3.7 too.

This guide uses the Web Installer to start the installation of the
Eclipse Client 3.0.1 over an existing Eclipse 3.6.x. If you want to use
IM plus a local repository, first check the Required Features in the
Eclipse environment **TODO** section and install the features needed by
your Eclipse package. Then start IM and select to install the RTC
Eclipse Client. You can now start from step 3 **TODO**.

## Considerations

-   If a different Rational product has been installed and you want to
    share the same Eclipse shell, this is not the correct guide. You
    need to install RTC in the same package group.
-   The steps in this guide were tested in Microsoft Windows 7 with the
    Eclipse 3.6.2 32 bits packages and Installation Manager 1.4.3
    (included in the RTC 3.0.1 Web Install).

## Prerequisites

You are using a win32 or linux32 Eclipse package. Installation Manager
1.4.3 do not install RTC into an Eclipse 64 bit package. Your existing
Eclipse environment has a valid JVM ready to use (indicated in the
eclipse.ini file or a JVM is set in the environment). Check
<https://jazz.net/wiki/bin/view/Main/CLMWorkbenchSystemRequirements> to
verify that you have a supported JVM. Your Eclipse environment should
contain all the features required by RTC to install into an existing
Eclipse. The Eclipse classic package contains all the required features.
To know what you are going to need in other editions, see the following
section on identifying required features in the Eclipse environment.

## Steps

### 1. Identify required features in the Eclipse Environment

The Classic Eclipse package contains all the features required by RTC.
However, packages like the CPP or JEE will not accept the install of the
Eclipse 3.5.2 features that RTC packages. RTC does support the Eclipse
3.6.2 features, so you can install the correct pieces into the existing
Eclipse environment in order to install RTC.

The three packages that need to be available in the Eclipse environment
are EMF & XSD, PDE and JDT. Make sure that you have them installed
before you install RTC. If you have these components in your environment
jump to Get the Web Installer and start Installation Manager **TODO**.
There you will find the links to the zips containing the required
features according to your Eclipse package.

Follow these steps to identify and install the Eclipse features that you
need:

Download the zips that correspond to your Eclipse package and extract
the content to a temporary location.

Package **JEE and RCP**

Features you need to install for 3.6.x: Eclipse Modeling Framework SDK
Update (EMF) 2.6.1

Features you need to install for 3.7: Eclipse Modeling Framework SDK
Update (EMF) 2.7

Package: **CPP**

Features you need to install for 3.6.x: Eclipse Plug-in Development
Environment (PDE) 3.6.2 and Eclipse Java Development Tools (JDT) 3.6.2

Features you need to install for 3.7: Eclipse Plug-in Development
Environment (PDE) 3.7 and Eclipse Java Development Tools (JDT) 3.7

Package: **Java**

Features you need to install for 3.6.x: Eclipse Modeling Framework SDK
Update (EMF) 2.6.1 and Eclipse Plug-in Development Environment (PDE)
3.6.2

Features you need to install for 3.7: Eclipse Modeling Framework SDK
Update (EMF) 2.7 and Eclipse Plug-in Development Environment (PDE) 3.7

Package: **Testing**

Features you need to install for 3.7: Eclipse Plug-in Development
Environment (PDE) 3.7

Start your Eclipse package. Click Help \> Install New Software Click Add
Select each directory containing the update sites that you created in
step 1 After you have added all the local folders, unmark the checkbox
"Group items by category." Select to "Work with --OnlyLocal Sites--".
Click **Select All** to install. Restart Eclipse when prompted.

(Click for full size image) Proceed with the installation of RTC using
IM.

### 2. Get the Web Installer and start Installation Manager

Get the RTC Web Installer zip for your OS platform from
<https://jazz.net/downloads/rational-team-concert/releases/3.0.1?p=allDownloads>
(Windows or Linux are the operating systems supported by the RTC Eclipse
client). (Click for full size image) Extract the content of the zip into
your preferred location. Go to the directory where you extracted the
content. Start the Launchpad with launchpad.exe or launchpad.sh. The RTC
Launchpad should open. You can install RTC in a shared location
(administrator privileges are required). Use the checkbox at the bottom
of the Launchpad to start or install IM with administrative privileges.

(Click for full size image) To start IM, click the link "Rational Team
Concert - Client for Eclipse IDE" located under the "Install Optional
Tools" section in the Launchpad .

(Click for full size image) Use your Jazz.net ID and password if
credentials are requested.

### 3. Install over an Existing Eclipse

The first Install Packages panel lists the products for installation. If
IM needs to be updated or installed, this panel lists that too. Click
Next. (Click for full size image) Accept the license and click Next
again. If IM is being installed for the first time, accept the defaults
in the next panel and click Next.

(Click for full size image) The next panel gives details about the
Package group. If it is not selected, choose "Create a new package
group" and click Next.

(Click for full size image) A panel opens that enables you to install
RTC into an existing Eclipse instance.

(Click for full size image) Select the Extend an existing Eclipse
checkbox. Click the Browse... button to select the directory that
contains your eclipse executable.

(Click for full size image) IM searches for the JVM used by this Eclipse
environment. As indicated in the prerequisites, your Eclipse environment
must have a valid JVM available. If the folder does not contain a valid
Eclipse environment or the JVM is not valid nor set, IM might not allow
you to continue until the problem is fixed (depending on the IM
version). Click Next if the validation was successful. Do not select to
install other languages. Native Eclipse does not include language packs
and the installation fails if any language content is selected. Click
Next. Select to install Sametime Integration if you need it. Click Next.
Select the way you want to install the Help. Click Next. Start the
installation by clicking Install. When the installation completes, close
IM and the Launchpad. Start your Eclipse environment and verify that the
WorkItems perspective is available.

## Related links

-   [The older version of this
    guide](https://jazz.net/library/article/708/)
-   [Install RTC Eclipse Client 2.x into Eclipse
    3.4.2](https://www-304.ibm.com/support/docview.wss?uid=swg21391058&wv=1)
-   [Installing Rational Eclipse-based (7.5 and 8.0) products within an
    existing
    Eclipse](https://www.ibm.com/developerworks/wikis/display/rationalinstall/Install+into+an+existing+Eclipse+instance)
-   [Technote to install RTC 3.0.x over Eclipse
    3.6.x](https://www-304.ibm.com/support/docview.wss?rs=3488&uid=swg21502374&wv=1)
