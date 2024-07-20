META:TOPICINFO{author="ktessier" date="1502126356" format="1.1"
version="1.3"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRun"}

# Enabling installation of iFix releases DKGRAY [enabling-installation-of-ifix-releases-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

## Enabling installation of iFix releases

1\. Login to the target UCD server as an administrator. 1. Click
Applications, then select the Quick Deployer application.

1\. Click **Processes**, then select the **Install Applications
process**.

1\. When the process opens select the **Configuration** tab and then
select **Application Process Properties**. Chose the **enableIFIX**
property and click **Edit**.

1\. Select **FALSE** to disable iFix support by default or **TRUE** to
enable iFix support by default.

1\. *You can also change the description and label if desired*. Be sure
to press **Save** when changes are complete.

1\. The Default Value is now changed

1\. Select the **Design** tab open the **Prepare System** step by
clicking on the **Pencil** icon

1\. To specify the iFix version of CLM applications to be installed,
select a version in the **CLMiFixVersion** field. If you do not select a
version, you will be prompted to enter a value in the **Run Process**
dialog when you select the **Install Applications** process. To specify
iFix versions for Design Management or Rhapsody Design Management,
select a version in the **DMiFixVersion** or **DMMSiFixVersion** field,
respectively.

Note: after pressing OK on the Edit Properties dialog you must press the
**Save** process icon or the changes will not be committed

## Results

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="AS_13.png" attachment="AS_13.png" attr="h"
comment="" date="1498849730" path="AS_13.png" size="19021"
user="ktessier" version="1"} META:FILEATTACHMENT{name="AS_11.png"
attachment="AS_11.png" attr="h" comment="" date="1498849746"
path="AS_11.png" size="57161" user="ktessier" version="1"}
META:FILEATTACHMENT{name="enableifix-property-set.png"
attachment="enableifix-property-set.png" attr="h" comment=""
date="1498849759" path="enableifix-property-set.png" size="59505"
user="ktessier" version="1"}
META:FILEATTACHMENT{name="enableifix-save.png"
attachment="enableifix-save.png" attr="h" comment="" date="1498849772"
path="enableifix-save.png" size="18423" user="ktessier" version="1"}
META:FILEATTACHMENT{name="enableifix-false.png"
attachment="enableifix-false.png" attr="h" comment="" date="1498849784"
path="enableifix-false.png" size="18593" user="ktessier" version="1"}
META:FILEATTACHMENT{name="enableifix-property-edit.png"
attachment="enableifix-property-edit.png" attr="h" comment=""
date="1498849799" path="enableifix-property-edit.png" size="61167"
user="ktessier" version="1"} META:FILEATTACHMENT{name="AS_10v13.png"
attachment="AS_10v13.png" attr="h" comment="" date="1498849814"
path="AS_10v13.png" size="38144" user="ktessier" version="1"}
META:FILEATTACHMENT{name="AS_7.png" attachment="AS_7.png" attr="h"
comment="" date="1498849830" path="AS_7.png" size="21070"
user="ktessier" version="1"}
META:FILEATTACHMENT{name="act-cm-ntp-ldap-ifix-selectv20a.png"
attachment="act-cm-ntp-ldap-ifix-selectv20a.png" attr="h" comment=""
date="1498849847" path="act-cm-ntp-ldap-ifix-selectv20a.png"
size="33185" user="ktessier" version="1"}
