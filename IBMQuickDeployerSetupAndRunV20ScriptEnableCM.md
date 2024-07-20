META:TOPICINFO{author="ktessier" date="1502126331" format="1.1"
version="1.3"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRun"}

# Enabling Configuration Management DKGRAY [enabling-configuration-management-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

To enable Configuration Management (CM) capabilities in the IBM Internet
of Things (IoT) Continuous Engineering Solution and the IBM Rational
solution for Collaborative Lifecycle Management applications, you must
obtain an activation key from IBM Support. To configure IBM Quick
Deployer so that the applications that it installs are CM-enabled, edit
the **Prepare System** step of the **Install Applications** process.

## Enabling Configuration Management capabilities

1\. Login to the target UCD server as an administrator. 1. Click
Applications, then select the Quick Deployer application.

1\. Click **Processes**, then select the **Install Applications
process**.

1\. On the process **Design** tab open the **Prepare System** step by
clicking on the pencil icon.

1\. Select **True** in the **EnableCM** field, which causes Quick
Deployer to enable CM without prompting you when you run the **Install
Applications** process. If you select **False**, Quick Deployer disables
CM without prompting you when you run the **Install Applications**
process. If you leave the value of the field cleared, Quick Deployer
prompts you to enter a value of True or False in the Run Process dialog
when you select the **Install Applications** process. 1. Enter the
activation key that you receive from IBM Support in the
**CMActivationKey** field. If you leave the value of the field cleared,
Quick Deployer prompts you to enter a value in the Run Process dialog
when you select the **Install Applications** process.

1.  Click **OK** to close the **Edit Properties** window.
2.  Click the **Save** process icon to save your changes.

## Results

When you run the **Install Applications** process, the Quick Deployer
sets the activation key property in the Quality Management and
Requirements applications to the value that you specify in the
**CMActivationKey** field.

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="cm-enablev20.png"
attachment="cm-enablev20.png" attr="h" comment="" date="1498851830"
path="cm-enablev20.png" size="33506" user="ktessier" version="1"}
META:FILEATTACHMENT{name="AS_11.png" attachment="AS_11.png" attr="h"
comment="" date="1498851842" path="AS_11.png" size="57161"
user="ktessier" version="1"} META:FILEATTACHMENT{name="AS_10v13.png"
attachment="AS_10v13.png" attr="h" comment="" date="1498851855"
path="AS_10v13.png" size="38144" user="ktessier" version="1"}
META:FILEATTACHMENT{name="AS_7.png" attachment="AS_7.png" attr="h"
comment="" date="1498851867" path="AS_7.png" size="21070"
user="ktessier" version="1"}
