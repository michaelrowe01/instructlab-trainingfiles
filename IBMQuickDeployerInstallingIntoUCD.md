META:TOPICINFO{author="tomp" date="1513128175" format="1.1"
version="1.6"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRun"}

# Installing IBM Quick Deployer into IBM UrbanCode Deploy DKGRAY [installing-ibm-quick-deployer-into-ibm-urbancode-deploy-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

To install IBM Quick Deployer into IBM UrbanCode Deploy, run the
install.jar file that is included in the Quick Deployer .zip package. In
addition to installing the Quick Deployer application, the script
performs the following tasks:

-   Creates a team named Rational QD CLM and adds an admin user.
-   Creates the Team Member role.
-   Creates a user named ibm and assigns the Team Member role to that
    user.
-   Creates the Team Admin role.
-   Loads the component code.
-   Creates agent tags.
-   Creates a default resource group.
-   Creates default application blueprints.

## Prerequisites

To successfully install IBM Quick Deployer, you must have the following:

-   A running UrbanCode Deploy server. See [System
    requirements](https://jazz.net/wiki/bin/view/Deployment/IBMQuickDeployerSystemRequirements)
    for the supported version.
-   The URL to the UrbanCode Deploy server, and an authentication token
    with admin privileges.
-   A Windows or Linux system that has Java 7 or higher installed. You
    must specify the Java executable in the system path. This can be the
    same system upon which the UrbanCode Deploy server runs, or it can
    be another system.
-   The Quick Deployer .zip file, which you can download from the
    [Package Content
    page](https://jazz.net/wiki/bin/view/Deployment/IBMQuickDeployerPackageContent).

## About this task

The Quick Deployer .zip file includes the following properties files: \*
qd.properties: The properties file that the installer uses to configure
the Quick Deployer application in IBM UrbanCode Deploy. You must set
some basic parameters, such as the URL of the target UrbanCode Deploy
server, in this file. In addition, you can set optional parameters to
configure, for example, use of a Network Time Protocol (NTP) server, or
enablement of Configuration Management capabilities. You can also point
to the location of the ldap.properties, userCreds.properties, and
database properties files. \* ldap.properties: The file that contains
the properties that you define to connect to and use an LDAP server. To
have the installer configure the Quick Deployer application to use your
LDAP server properties, you must edit the values of the properties in
this file. Alternatively, after you run the installer, you can specify
your LDAP server properties by running the **Change Default LDAP
Parameters** application process. For details about running that
process, and for descriptions of all of the LDAP properties, see [IBM
Quick Deployer change default LDAP
parameters](IBMQuickDeployerChangeDefaultLDAPParameters). \*
userCreds.properties: The file that contains the user names and
passwords that are required to access and run the CLM or IoT CE
applications, the DB2, Oracle, or SQL Server database management system,
and middleware. To have the installer configure the Quick Deployer
application to use a default set of user credentials, you must edit the
values of the properties in this file. Alternatively, after you run the
installer, you can specify your default user credentials by running the
**Change Default User Parameters** application process. For details
about running that process, and for descriptions of all of the user
credential properties, see [IBM Quick Deployer change default user
parameters](IBMQuickDeployerChangeDefaultUserParameters). \* database
properties files (db2Parameter_linux.properties,
db2Parameter_windows.properties, oracleParameter_linux.properties,
oracleParameter_windows.properties, and
sqlserverParameter_windows.properties): Database
vendor-specific/OS-specific files that contain the parameters that
configure the connections between the installed CLM or IoT CE
applications and their databases. These property files also contain a
default set of parameters that are used to create the
database/tablespace for each product. Use one of these database property
files if you use an existing DB2, Oracle, or SQL Server database
instance instead of the one installed by the Quick Deployer. If you use
an existing DB2, Oracle, or SQL Server database instance, edit the
parameter values in the appropriate database property file to match your
database environment. For descriptions of the DB2, Oracle, or SQL Server
parameters, see [IBM Quick Deployer change default DB2 database
parameters](IBMQuickDeployerChangeDefaultDB2Parameters), [IBM Quick
Deployer change default Oracle database
parameters](IBMQuickDeployerChangeDefaultOracleParameters), and [IBM
Quick Deployer change default SQL Server database
parameters](IBMQuickDeployerChangeDefaultSQLServerParameters).

The package contains sample properties files which may be used as a
starting point.

## Installation steps

1\. On a system that has Java 7 or higher installed, extract the
contents of the Quick Deployer .zip file. Note: This can be the same
system upon which the UrbanCode Deploy server runs, or it can be another
system. 1. On the same system, ensure that the JAVA_HOME environment
variable is set to point to the location of the Java Runtime Environment
(JRE). \* On Windows, in a console window, use the set command. For
example: \* set JAVA_HOME=C:\Program Files\ibm\Java80\jre\bin \* On
Linux, if necessary, run the export command to set the JAVA_HOME
environment variable. For example: \* export
JAVA_HOME=/usr/lib/jvm/jre. 1. Open the qd.properties file in a text
editor and enter values for the following two properties: \* ucdUrl: URL
of the target UrbanCode Deploy server. \* ucdToken: UrbanCode Deploy
server authentication token with admin privileges. \* Specify either
mediaUrl or localPath. \* mediaUrl: URL of the FTP media server that
contains the installers for the IBM Rational solution for Collaborative
Lifecycle Management (CLM) or IoT Continuous Engineering (CE) solution
and necessary middleware. \* localPath: The local path of the media on
each machine. The path must be the same for all machines. **Note**: On
Windows, the local path cannot be a mapped network drive. \*
copyBeforeUnzip: **true** or **false**. Set this property to true if you
use localPath and the local path is a network mount, such as an NFS
mount. When this option is set to true, Quick Deployer copies the media
archive files from the network mount to each machine before extracting
those archive files, which improves performance. 1. Optionally enter
values for the following properties: \* dbVendor: **db2**, **oracle**,
or **sqlserver**. \* enableNtpClock: **true** or **false**. To configure
the system to use a Network Time Protocol (NTP) as a reference for each
server, set this property to true. If you set this to true, also specify
a value for the ntpClock property. \* ntpClock: URL of the NTP system
clock server. \* enableCm: **true** or **false**. To enable
Configuration Management (CM) capabilities in the IBM Internet of Things
(IoT) Continuous Engineering Solution and the IBM Rational solution for
Collaborative Lifecycle Management applications, set this property to
true. If you set this to true, also specify a value for the
cmActivationKey property. \* cmActivationKey: Configuration Management
activation key that you obtain from IBM Support. \* wasUserName:
Administrator user name as defined on the LDAP server. \* wasPassword:
Administrator password as defined on the LDAP server. \* ldapProperties:
Full or relative path to the LDAP properties file. The LDAP properties
file contains the property settings that are used to connect to and use
an LDAP server. The Quick Deployer package contains an ldap.properties
file. If you choose to use that file, you must edit it so that the
property values identify your LDAP server. \* userCredsPropertiesLinux:
Full or relative path to a user credentials properties file (Linux
deployments). The user credentials property file contains the user names
and passwords that are required to access and run the CLM or IoT CE
applications, the DB2 or Oracle database management system, and
middleware. The Quick Deployer package contains a userCreds.properties
file. If you choose to use that file, you must edit it so that the
property values identify your set of default user credentials. **Note**:
all the passwords must be base64 encoded. \* userCredsPropertiesWindows:
Full or relative path to a user credentials properties file (Windows
deployments). The user credentials property file contains the user names
and passwords that are required to access and run the CLM or IoT CE
applications, the DB2, Oracle, or SQL Server database management system,
and middleware. The Quick Deployer package contains a
userCreds.properties file. If you choose to use that file, you must edit
it so that the property values identify your set of default user
credentials. **Note**: all the passwords must be base64 encoded. \*
databaseProperties: Full or relative path to the database properties
file. The database properties file defines the parameters that configure
the connections between the installed CLM or IoT CE applications and
their databases. Specify these parameters if you use an existing DB2,
Oracle, or SQL Server database instance instead of the one installed by
the Quick Deployer. The Quick Deployer package contains the following
sample database properties files:

-   db2Parameter_linux.properties
-   db2Parameter_windows.properties
-   oracleParameter_linux.properties
-   oracleParameter_windows.properties
-   sqlserverParameter_windows.properties 1. In a command prompt or
    console window, navigate to the directory where you extracted the
    contents of the Quick Deployer .zip file. Run the installer by
    entering the following command: \* **java -jar install.jar
    qd.properties**

## Results

After the installer finishes, examine the console output to ensure that
it completed successfully. The output should look similar to this:

Creating team Rational QD CLM. Team created. Adding admin to Rational QD
CLM. Admin added to team. Creating role Team Member. Role created.
Creating user ibm and assigning role Team Member. User created. User
assigned role. Creating role Team Admin. Role created. Creating
temporary resource rational-qd-tag-resource. Creating tag DB. Success.
Creating tag IHS. Success. Creating tag JTS. Success. Creating tag CCM.
Success. Creating tag RM. Success. Creating tag QM. Success. Creating
tag GC. Success. Creating tag LDX. Success. Creating tag RELM. Success.
Creating tag DCC. Success. Creating tag RS. Success. Creating tag LQE.
Success. Creating tag DM. Success. Creating tag AM. Success. Creating
tag APPSERVER. Success. Deleting temporary resource
rational-qd-tag-resource. Importing application into UCD Application
imported successfully Publishing components. Publishing component
Rational_QD_ApplicationServer_605 version 20171206-1212. Success
Publishing component Rational_QD_Application_605 version 20171206-1212.
Success Publishing component Rational_QD_Database_605 version
20171206-1212. Success Publishing component
Rational_QD_InstallationManager_605 version 20171206-1212. Success
Publishing component Rational_QD_SystemPre-Requisite_605 version
20171208-1612. Success Creating default-resource-group and add it to
Rational QD CLM. Creating blueprint dept-vanilla. Created dept-vanilla
Created. Creating blueprint dept-CLM. Created dept-CLM Created. Creating
blueprint dept-CE. Created dept-CE Created. Creating blueprint dist-CLM.
Created dist-CLM Created. Creating blueprint dist-CE. Created dist-CE
Created. Quick Deployer install successful. Quick Deployer application
URL:
<https://ucd.ibm.com:8443/#application/1d4x58ea-2x42-47ca-b5db-c7x06c5a1534>

## Verify that the Quick Deployer application is set up correctly

In IBM UrbanCode Deploy, click the **Applications** tab. You should see
an entry for Rational_QD_60x.

Click the Rational_QD_60x entry, then click the **Components** tab. You
should see five components.

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:TOPICMOVED{by="ktessier" date="1513019874"
from="Deployment.IBMQuickDeployerInstallingIntoUCDV21"
to="Deployment.IBMQuickDeployerInstallingIntoUCD"}
