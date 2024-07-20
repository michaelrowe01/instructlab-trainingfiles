META:TOPICINFO{author="sbagot" date="1432736723" format="1.1"
version="1.4"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandDOORS"}

# Why does the DOORS Web Access requirement selection picker display as a blank blue page when initiating a link request using the RTC Eclipse client? DKGRAY Authors: Main.IntegrationsTroubleshootingTeam [why-does-the-doors-web-access-requirement-selection-picker-display-as-a-blank-blue-page-when-initiating-a-link-request-using-the-rtc-eclipse-client-dkgray-authors-main.integrationstroubleshootingteam]

Build basis: RTC 5.0 and later, Rational DOORS Web Access version
9.6.0.1 and later

ENDCOLOR

TOC{title="Page contents"}

This page provides details and workaround instructions for an issue that
occurs when using the DOORS Web Access (DWA) requirement selection
picker.

## Symptoms

When using DOORS Web Access requirement selection picker, a blank blue
page is displayed when attempting to initiate a link request using the
IBM Rational Team Concert (RTC) Eclipse client.

## Cause

The issue is reported and discussed in defect work item 322762 and is
the result of a bug in the Eclipse base code.

## Solution

### Workarounds

Below are different configurations where the problem occurs along with
instructions to workaround the issue.

First, determine the Eclipse version for your RTC Eclipse client.

-   From the RTC Eclipse client, click **Help -\> About Rational Team
    Concert**
-   Click on the **eclipse.org** icon to view version information about
    the Eclipse environment. There may be multiple icons to represent
    different Eclipse features that are installed in the environment.
    Locate the version for the Eclipse RCP feature, and complete the
    instructions associated with your Eclipse version.

#### Eclipse 3.6.x

1\) Update the **eclipse.ini** -vm setting to use the IBM J9 JVM. The
directory path may vary depending on the file location of your Java
Runtime Environment (JRE).

-vm jdk\jre\bin

2\) Save the **eclipse.ini** changes and restart Eclipse

#### Eclipse 4.2.x and Eclipse 4.3.x

1\) Add the line below under the **-vmargs** identifier in
**eclipse.ini**.

-Dorg.eclipse.swt.browser.IEVersion=

The value for the IEVersion setting must match the browser version
installed on the system. The workaround will not help if the specified
version string does not match the installed version. Settings for the
different Microsoft Internet Explorer versions are listed in the
Microsoft MSDN documentation under Browser Emulation

2\) Save the **eclipse.ini** changes and restart Eclipse

#### Eclipse 4.4 or higher

Issue is resolved

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Bryan Hogan [additional-contributors-bryan-hogan]
