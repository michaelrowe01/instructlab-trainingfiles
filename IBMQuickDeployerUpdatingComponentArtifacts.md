META:TOPICINFO{author="ktessier" date="1502126443" format="1.1"
version="1.4"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRun"}

# IBM Quick Deployer Updating Component Artifacts [ibm-quick-deployer-updating-component-artifacts]

DKGRAY INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

You might want to change the behavior of the IBM Quick Deployer by
making changes to scripts in IBM UrbanCode Deploy components. This topic
explains how to use the IBM UrbanCode Deploy command-line interface to
do this task. The task consists of the following steps:

-   Download the script artifacts of an existing component version.
-   Modify the script artifacts.
-   Create a new component version
-   Publish the artifacts to the new component version

## Prerequisites

-   The IBM UrbanCode Deploy command-line interface must be installed.
    For details, see [Installing the command-line
    client](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.1/com.ibm.udeploy.reference.doc/topics/cli_install.html).
-   The IBM Quick Deployer must be installed into an UrbanCode Deploy
    server.
-   You must have an UrbanCode Deploy authentication token that has
    permissions that let you download and create component versions.

## Download UrbanCode Deploy component version artifacts

1\. Identify the component name and version that you want to
download. 1. Run the udclient **downloadVersionArtifacts** command with
the following arguments: \* **authtoken**: UrbanCode Deploy
authentication token \* **weburl**: URL of UrbanCode Deploy server \*
**component**: Name of the component to download \* **version**: Version
of the component to download

For example:

C:\udclient\>udclient -authtoken 4196ab18-6bd6-76c5-c294-9648793gb418
-weburl <https://ucd-09.host.com:8443> downloadVersionArtifacts
-component Rational_QD_SystemPre-Requisite_604 -version 20170711-1432
Downloading... \[#######\] Completed.

Downloaded to
C:\udclient\Rational_QD_SystemPre-Requisite_604_20170711-1432_artifacts.zip

## Modify the component script artifacts

1.  Create a temporary directory.
2.  Extract the artifacts.zip file, which you previously downloaded,
    into the temporary directory.
3.  Make your changes to the scripts included in the artifacts.zip file.
    Optionally add files and delete obsolete files.

## Create new component version

1\. Choose a naming convention for the new version. For example, you
might want to use a date and time stamp. 1. Run the udclient
**createVersion** command with the following arguments: \*
**authtoken**: UrbanCode Deploy authentication token \* **weburl**: URL
of UrbanCode Deploy server \* **component**: Name of the component for
which you are creating a new version \* **name**: Name of the version to
be created

For example:

C:\udclient\>udclient -authtoken 4196ab18-6bd6-76c5-c294-9648793gb418
-weburl <https://ucd-09.host.com:8443> createVersion -component
Rational_QD_SystemPre-Requisite_604 -name 20170711-1442

## Publish the artifacts to the new component version

1\. Run the udclient **addVersionFiles** command with the following
arguments: \* **authtoken**: UrbanCode Deploy authentication token \*
**weburl**: URL of UrbanCode Deploy server \* **component**: Name of the
component \* **version**: Name of the version to which you are adding
the revised artifacts \* **base**: Temporary directory that you created
previously that contains the artifacts

For example:

C:\udclient\>udclient -authtoken 4196ab18-6bd6-76c5-c294-9648793gb418
-weburl <https://ucd-09.host.com:8443> addVersionFiles -component
Rational_QD_SystemPre-Requisite_604 -version 20170711-1442 -base tmp

## Confirm that the new component version has been published

1\. In the UrbanCode Deploy web client, click the **Components** tab;
click the component for which you created a new version; then click the
**Versions** tab. 1. Confirm that the new version is visible. For
example:

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="component-versionsv20.png"
attachment="component-versionsv20.png" attr="h" comment=""
date="1500502045" path="component-versionsv20.png" size="24765"
user="ktessier" version="1"} META:TOPICMOVED{by="ktessier"
date="1501532476"
from="Deployment.DeploymentIBMQuickDeployerUpdatingComponentArtifactsV20"
to="Deployment.IBMQuickDeployerUpdatingComponentArtifacts"}
