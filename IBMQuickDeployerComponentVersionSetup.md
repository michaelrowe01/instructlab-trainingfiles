META:TOPICINFO{author="ktessier" date="1501529000" format="1.1"
version="1.20"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRunOld"}

# IBM Quick Deployer component version setup DKGRAY [ibm-quick-deployer-component-version-setup-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

The scripts used by Quick Deployer are delivered as a single compressed
file for each component. This topic explains how to extract the scripts
from the compressed file and import them into UCD as a new UCD Component
version.

## Component script version setup

1.  On the UCD server expand the IBM Quick Deployer installation package
    into a temporary folder eg **/media/QD**
2.  Ensure the following files are present
    -   versionUnzip.sh
    -   Rational_QD_Application_60x_yyyymmdd-hhmm_artifacts.zip
    -   Rational_QD_ApplicationServer_60x_yyyymmdd-hhmm_artifacts.zip
    -   Rational_QD_Database_60x_yyyymmdd-hhmm_artifacts.zip
    -   Rational_QD_InstallationManager_60x_yyyymmdd-hhmm_artifacts.zip
    -   Rational_QD_SystemPre-Requisite_60x_yyyymmdd-hhmm_artifacts.zip
3.  Assign execute permission to the **{agent install
    dir}/agent/opt/udclient/udclient** script
4.  Assign execute permission to the **versionUnzip.sh** script
5.  ensure JAVA_HOME is set. If not export JAVA_HOME={location of your
    jre} (e.g. /usr/lib/jvm/jre)
6.  ensure UCDCLIEXE is set. If not export UCDCLIEXE={location of your
    udclient exe} (e.g. /opt/ibm-ucd/agent/opt/udclient/udclient)
7.  Execute the **versionUnzip.sh** script The script expects 3
    arguments as key=value pairs:
    -   **BASEFOLDER** =base folder for expanding the scripts into (e.g.
        /media/QD)
    -   **APPLICATIONVERSION** =ApplicationVersion (e.g. 602)
    -   **COMPONENTVERSION** =ComponentVersion (e.g. 6.0.2.0)

\- as lots of information is written to the screen it is recommended
that when executing the script the output should be **piped through the
tee program** for post processing. - when execution completes the
individual application artifacts will be found in
**/BASEFOLDER/APPLICATIONVERSION/COMPONENTVERSION/{application}** (e.g.
/media/QD/602/6.0.2.0/Application)

cd /media/QD chmod 755 {agent install dir}/agent/opt/udclient/udclient
chmod 755 versionUnzip.sh export JAVA_HOME={location of your jre} export
UCDCLIEXE={agent install dir}/agent/opt/udclient/udclient

sh versionUnzip.sh BASEFOLDER=/media/QD APPLICATIONVERSION=602
COMPONENTVERSION=6.0.2.0 \| tee console_versionUnzip.log \>\> deleted
console text \<\< SUCCESS \[versionUnzip.sh\]: Quick Deployer scripts
successfully unzipped

ls /media/QD/602/6.0.2.0 Application ApplicationServer Database
InstallationManager SystemPre-Requisite

1.  Ensure you are in the folder where you expanded the IBM Quick
    Deployer installation package eg **/media/QD**
2.  Ensure the following files are present
    -   componentVersionImport.sh
    -   versionImport.sh
3.  Assign execute permission to the **componentVersionImport.sh** and
    **versionImport.sh** scripts
4.  Execute the **versionImport.sh** script The script expects 6
    arguments as key=value pairs:
    -   **USERNAME** =UCDAdminUserName
    -   **USERPASSWORD** =UCDAdminUserPassword
    -   **UCDSERVER** =UCDURL (e.g. https://UCDHostName:8443)
    -   **BASEFOLDER** =base folder containing the expanded scripts to
        import (e.g. /media/QD)
    -   **APPLICATIONVERSION** =ApplicationVersion (e.g. 602)
    -   **COMPONENTVERSION** =ComponentVersion (e.g. 6.0.2.0)

\- as lots of information is written to the screen it is recommended
that when executing the script the output should be **piped through the
tee program** for post processing.

cd /media/QD chmod 755 componentVersionImport.sh chmod 755
versionImport.sh

sh versionImport.sh USERNAME=adminuser USERPASSWORD=adminpassword
UCDSERVER=ucdurl:port BASEFOLDER=/media/QD APPLICATIONVERSION=602
COMPONENTVERSION=6.0.2.0 \| tee console_versionImport.log \>\> deleted
console text \<\< SUCCESS \[versionImport.sh\]: Quick Deployer scripts
imported into UCD

1\. Confirm for each of the components listed that they have the correct
version \[e.g. 6.0.x.0\] and file content. \*
Rational_QD_Application_60x \* Rational_QD_ApplicationServer_60x \*
Rational_QD_Database_60x \* Rational_QD_InstallationManager_60x \*
Rational_QD_SystemPre-Requisite_60x

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="CVS_1.png" attachment="CVS_1.png" attr="h"
comment="confirm version" date="1443719785" path="CVS_1.png"
size="24130" user="kenneth" version="1"}
META:FILEATTACHMENT{name="CVS_2.png" attachment="CVS_2.png" attr="h"
comment="confirm content" date="1443719834" path="CVS_2.png"
size="36183" user="kenneth" version="1"}
META:FILEATTACHMENT{name="unzip01.png" attachment="unzip01.png" attr="h"
comment="extracted files" date="1443719858" path="unzip01.png"
size="27093" user="kenneth" version="1"}
META:FILEATTACHMENT{name="unzip01b.png" attachment="unzip01b.png"
attr="h" comment="extracted files" date="1445210106" path="unzip01b.png"
size="27313" user="tomp" version="1"}
