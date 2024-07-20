META:TOPICINFO{author="syeshin" date="1421253370" format="1.1"
version="1.2"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Installing, updating, and scripting installations for IBM Installation Manager [installing-updating-and-scripting-installations-for-ibm-installation-manager]

DKGRAY Authors: Main.MarkGuertin Build basis: IBM Installation Manager
ENDCOLOR

## Installing, updating, and scripting installations for IBM Installation Manager

Level: Intermediate Contents: Overview Installing IBM Installation
Manager Updating the installed IBM Installation Manager Creating
response files to silently install packages Running IBM Installation
Manager in clean mode and temporary mode Installing packages Installing
package licenses Modifying packages Updating all installed packages
Uninstalling packages Uninstalling IBM Installation Manager

Overview The following article describes how to install and update
IBM(R) Installation Manager, as well as how to use it to install and
update packages using Windows(R) scripts. Installing and Updating IBM
Installation Manager First of all, you should understand the difference
between these two items:

IBM Installation Manager Kit: The kit provides a directory that contains
an instance of IBM Installation Manager that installs the IBM
Installation Manager. The file that starts Installation Manager is named
installc.exe. IBM Installation Manager: This item is the installed
version of IBM Installation Manager used for all package management
(install, uninstall, ...). The default install directory for Windows is
the C:\Program Files\IBM\Installation Manager directory.

You must use the IBM Installation Manager Kit to install IBM
Installation Manager on a client computer. You can also use the IBM
Installation Manager Kit to update it. If an older version of IBM
Installation Manager is installed, the IBM Installation Manager Kit can
update the IBM Installation Manager to that version. If the version of
the installed IBM Installation Manager is the same as that of the IBM
Installation Manager Kit or newer, the IBM Installation Manager on the
system will stay the same. The following fragment is from the main
installation script:

@set HOME=\~dp0 @set INSTALLDIR=C:\Program Files\IBM\Installation
Manager

echo Assert Installation Manager installed. It will be installed echo to
the INSTALLDIR if it is not yet installed @call HOME\assertInstaller.bat

The following fragment runs the IBM Installation Manager kit to install
the Installation Manager. The following fragment shows the content of
the assertInstaller.bat script:

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
:: This script runs IBM Installation Manager installer
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

@if exist HOME\InstallerImage\installc.exe ( echo Running IBM
Installation Manager installer HOME\InstallerImage\installc.exe
-acceptLicense ) else ( echo IBM Installation Manager installer has not
been found )

Note: To pass the installation location to IBM Installation Manager, you
can use -installationDirectory flag option in installc command. e.g.
installc.exe -installationLocation C:\MyInstallDir\MyIM -acceptLicense

Also, you need to add -acceptLicense option to state that you agree with
the Term of Use of IBM Installation Manager.

Creating response files to silently install packages

Use Installation Manager with the record option to create a response
file; you do not have to install a package. Select all the desired
options, and start the package installation.

Note: You can record a response file without installing or uninstalling
a product by adding the optional -skipInstall argument. Note that must
be a writable directory. The argument causes Installation Manager to
save the installation data without installing the product. You can use
the same in the next recording session to record updates or
modifications to the product, or to record license management. Note that
the products installed or any preferences, including repository
settings, that you set during installation without using the
-skipInstall argument are not stored. Using -skipInstall makes the
installation faster because Installation Manager is not installing the
product, it is only recording the installation data. If you need to
record an installation session of Installation Manager, you must add the
following argument to the recording command line: -vmargs
-Dcom.ibm.cic.agent.hidden=false.

The following fragment sets the IBM Installation Manager launcher and
starts a recording session:

@set HOME=\~dp0 @set INSTALLDIR=C:\Program Files\IBM\Installation
Manager

mkdir HOME\sessions\\

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
:: This script sets IBM Installation Manager launcher
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
@if exist "INSTALLDIR"\eclipse\IBMIMc.exe ( echo IBM Installation
Manager has been detected "INSTALLDIR"\eclipse\IBMIMc.exe -record
HOME\sessions\input.xml -skipInstall HOME\sessions\IM_DATA ) After you
close Installation Manager, the response file is stored to the location
that you specified during its creation.

Running IBM Installation Manager in clean mode and temporary mode The
following fragment is an example of setting clean and temporary modes in
a recorded response file:

...

If the clean option is set to false, which is the default setting,
Installation Manager uses the repository and other preferences from the
response file in addition to the existing Installation Manager settings.
If a preference is specified in both the response file and the current
Installation Manager settings, the response file takes precedence. If
the clean option is set to true, Installation Manager uses the
repository and other preferences from the response file; the existing
Installation Manager preference settings are not used. If a preference
has a default value and it is not specified in the response file, the
default value is used. If the temporary option is set to true, the
setting that Installation Manager uses in the current silent
installation session is not persisted. If the temporary option is set to
false, which is the default setting, the setting that Installation
Manager uses in the current silent installation session is persisted.
Installing packages You can use IBM Installation Manager to install
packages, and use IBM Packaging Utility to copy a package to your local
repository.

You must create an Installation Manager response file, which you can use
to silently install a recorded installation of a package. See Creating
response files to silently install packages.

The output is a typical response file that you need to make minor
changes to. Reference the following example:

Install the package by calling the installed IBM Installation Manager
Command Line Tool with the input option. The following fragment calls
the setInstallationManager function to set the IBM Installation Manager
silent launcher. NOTE: Never use the IBM Installation Manager kit for
installing packages. Always use the installed IBM Installation Manager

The following fragment is from the main installation script:

:::::::::::::::::::::::: MAIN SCRIPT FRAGMENT ::::::::::::::::::::::::
echo Install Rational Application Developer @call
:setInstallationManager call IM_LAUNCHER input "HOME\rad_install.xml"
-acceptLicense @set INSTALLERRORLEVEL=ERRORLEVEL @if NOT
INSTALLERRORLEVEL EQU 0 goto RAD_FAILED :::::::::::::::::::::::::: MAIN
SCRIPT FRAGMENT ENDS :::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
:: Function to set IBM Installation Manager launcher
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
:setInstallationManager @if exist "INSTALLDIR"\eclipse\tools\imcl.exe (
echo IBM Installation Manager has been detected @set
IM_LAUNCHER="INSTALLDIR"\eclipse\tools\imcl.exe ) else ( echo IBM
Installation Manager has not been detected @goto END ) GOTO :EOF

Note: The setInstallationManager function is used in all subsequent
script examples. Typically, script functions are placed at the very end
of a script file. To prevent the main script from going into the
function body, the main script should either exit beforehand or should
skip the functions block by using the GOTO command.

Installing package licenses After you install a package, you can install
a package license.

You must create an Installation Manager response file, which you can use
to silently install a recorded installation of a package. See Creating
response files to silently install packages.

The output is a typical response file that you need to make minor
changes to. Reference the following example:

Install the package license by calling IBM Installation Manager Command
Line Tool with the input option. The following fragment calls the
setInstallationManager function to set the IBM Installation Manager
silent launcher. The following fragment is from the main installation
script:

:::::::::::::::::::::::: MAIN SCRIPT FRAGMENT ::::::::::::::::::::::::

echo Install License Key for Rational Application Developer @call
:setInstallationManager call IM_LAUNCHER input
"HOME\rad_license_install.xml" -acceptLicense @set
INSTALLERRORLEVEL=ERRORLEVEL @set INSTALLERRORLEVEL=ERRORLEVEL @if NOT
INSTALLERRORLEVEL EQU 0 goto PEK_FAILED

Modifying packages You can use IBM Installation Manager to install or
uninstall certain features of packages.

You must create an Installation Manager response file, which you can use
to silently install a recorded installation of a package. See Creating
response files to silently install packages. This is an example of a
response file that installs a feature of a package. The following
example uses IBM Rational Application Developer 7.0.0.2:

This is an example of a response file that uninstalls a feature of a
package. The following example uses IBM Rational Application Developer
7.0.0.2:

Modify the package by calling IBM Installation Manager Command Line Tool
with the input option. The following fragment calls the
setInstallationManager function to set the IBM Installation Manager
silent launcher. The following fragment is from the main installation
script:

:::::::::::::::::::::::: MAIN SCRIPT FRAGMENT ::::::::::::::::::::::::

echo Modify (install feature) of Rational Application Developer @call
:setInstallationManager call IM_LAUNCHER input
"HOME\rad_modify_install.xml" -acceptLicense @set
INSTALLERRORLEVEL=ERRORLEVEL @if NOT INSTALLERRORLEVEL EQU 0 goto
RAD_MODIFY_INSTALL_FAILED

Updating all installed packages At the end of your main script, you can
add a call to Installation Manager to update all the currently installed
packages.

Use the following response file to update Installation Manager, and
replace \[Your repository location\] with your actual repository
location. This repository should be available to the computer that you
will use to access it.

The following fragment calls the setInstallationManager function to set
the IBM Installation Manager silent launcher. The following fragment is
from the main installation script:

:::::::::::::::::::::::: MAIN SCRIPT FRAGMENT ::::::::::::::::::::::::

echo Update all currently installed packages @call
:setInstallationManager call IM_LAUNCHER input "HOME\updateAll.xml"
-acceptLicense @set INSTALLERRORLEVEL=ERRORLEVEL @if NOT
INSTALLERRORLEVEL EQU 0 goto UPDATEALL_FAILED

Uninstalling packages You can use IBM Installation Manager to uninstall
packages.

You must create an Installation Manager response file, which you can use
to silently uninstall a package. See Creating response files to silently
install packages. This is an example of a response file that uninstalls
a package. The following example uses IBM Rational Application Developer
7.0.0.2:

Uninstall the package by calling IBM Installation Manager Command Line
Tool with the input option. The following fragment calls the
setInstallationManager function to set the IBM Installation Manager
silent launcher. The following fragment is from the main installation
script:

:::::::::::::::::::::::: MAIN SCRIPT FRAGMENT ::::::::::::::::::::::::

echo Uninstall Rational Application Developer @call
:setInstallationManager call IM_LAUNCHER input "HOME\rad_uninstall.xml"
@set INSTALLERRORLEVEL=ERRORLEVEL @if NOT INSTALLERRORLEVEL EQU 0 goto
RAD_UNINSTALL_FAILED

Uninstalling IBM Installation Manager You must use the IBM Installation
Manager uninstaller to uninstall IBM Installation Manager on a client
computer. The following fragment uses the uninstallInstallationManager
function to uninstall the IBM Installation Manager. The following
fragment is from the main installation script:

::::::::::::::::::::::::: MAIN SCRIPT BEGINS :::::::::::::::::::::::::

echo Uninstall Installation Manager @call :uninstallInstallationManager
@goto END

:END @exit

:::::::::::::::::::::::::: MAIN SCRIPT ENDS ::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
:: Function to run IBM Installation Manager uninstaller
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
:uninstallInstallationManager @if exist "INSTALLDIR"\eclipse\IBMIMc.exe
( echo Uninstalling IBM Installation Manager "C:\Documents and
Settings\All Users\Application Data\IBM\Installation
Manager\uninstall\uninstallc.exe" --launcher.ini "C:\Documents and
Settings\All Users\Application Data\IBM\Installation Manager\uninstall\\
silent-uninstall.ini" ) else ( echo IBM Installation Manager has not
been detected @goto END ) GOTO :EOF Note: Typically, script functions
are placed at the very end of a script file. To prevent the main script
from going into the function body, the main script should either exit
beforehand or should skip the functions block by using GOTO command.
