META:TOPICINFO{author="ktessier" date="1496863319" format="1.1"
version="1.20"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRun"}

# IBM Quick Deployer securing user passwords DKGRAY [ibm-quick-deployer-securing-user-passwords-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

You should make a copy of the default values prior to making any changes
so that the defaults can be restored if needed. Once changed individual
default values cannot automatically be restored.

By default all UCD parameters are displayed in clear text. This means
that all passwords used by Quick Deployer are visible on the process
screen and recorded in the process execution log file. This affects the
following QD processes

-   **UCD Change Default User Parameters** (user passwords)
-   **Install Applications** (admin password)

This topic explains how to obscure QD passwords from the user without
affecting the behavior of the **Install Applications** process.

Be aware that selecting the secure type for the password clears the
default value. You need to change the default password after selecting
the secure type or the installation will fail.

## Securing user passwords

Securing the passwords does not affect the behavior of the **Install
Applications** process.

1\. Open application **Rational_QD_60x**, select the **Processes** tab
and click on the **Change Default User Parameters** process.

1\. When the process opens select the **Configuration** tab and then
select **Application Process Properties**. Choose the password you wish
to secure and click **Edit**.

1\. Click on **Type** and select **Secure**

1\. The default value can be set here so that the user will not need to
enter a value each time the change default users process is run. You can
also change the description and label if desired. Be sure to press
**Save** when changes are complete.

1\. The **Default Value** is now obscured by Urban Code and displayed as
\*\*\***\***.

1.  Repeat for each password that you want secured.

## Securing admin password

1\. Open application **Rational_QD_60x**, select the **Processes** tab
and click on the **Install Applications** process

1\. When the process opens select the **Configuration** tab and then
select **Application Process Properties**. To secure the admin password
click **Edit**.

1\. Click **Type** and select **Secure**

1\. Enter the new **Default Value** for the property.

1\. You can also change the description and label if desired. Be sure to
press **Save** when changes are complete.

1\. The **Default Value** is now obscured by Urban Code and displayed as
\*\*\***\***.

1\. To set the default admin user name, **Edit** the property and enter
a default value.

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="SUP1.png" attachment="SUP1.png" attr="h"
comment="click on Change Default User Parameters" date="1443693806"
path="SUP1.png" size="41134" user="kenneth" version="1"}
META:FILEATTACHMENT{name="SAP1.png" attachment="SAP1.png" attr="h"
comment="select InstallApp" date="1444409327" path="SAP1.png"
size="41111" user="kenneth" version="1"}
META:FILEATTACHMENT{name="SAP3.png" attachment="SAP3.png" attr="h"
comment="edit defaults" date="1444409399" path="SAP3.png" size="13995"
user="kenneth" version="1"} META:FILEATTACHMENT{name="SAP4.png"
attachment="SAP4.png" attr="h" comment="select secure" date="1444409417"
path="SAP4.png" size="22054" user="kenneth" version="1"}
META:FILEATTACHMENT{name="SAP5.png" attachment="SAP5.png" attr="h"
comment="save changes" date="1444409437" path="SAP5.png" size="12973"
user="kenneth" version="1"} META:FILEATTACHMENT{name="SAP2b.png"
attachment="SAP2b.png" attr="h" comment="edit password"
date="1444757214" path="SAP2b.png" size="54543" user="tomp" version="1"}
META:FILEATTACHMENT{name="SAP6b.png" attachment="SAP6b.png" attr="h"
comment="dispolay obscured text" date="1444757676" path="SAP6b.png"
size="53181" user="tomp" version="1"}
META:FILEATTACHMENT{name="SAP7.png" attachment="SAP7.png" attr="h"
comment="dispolay user name" date="1444757815" path="SAP7.png"
size="54003" user="tomp" version="1"}
META:FILEATTACHMENT{name="SUP2a.png" attachment="SUP2a.png" attr="h"
comment="edit property" date="1462361826" path="SUP2a.png" size="59389"
user="kenneth" version="1"} META:FILEATTACHMENT{name="SUP3a.png"
attachment="SUP3a.png" attr="h" comment="select secure"
date="1462361867" path="SUP3a.png" size="26186" user="kenneth"
version="1"} META:FILEATTACHMENT{name="SUP4a.png" attachment="SUP4a.png"
attr="h" comment="save changes" date="1462361897" path="SUP4a.png"
size="13847" user="kenneth" version="1"}
META:FILEATTACHMENT{name="SUP5a.png" attachment="SUP5a.png" attr="h"
comment="display obscured text" date="1462361922" path="SUP5a.png"
size="14385" user="kenneth" version="1"}
META:FILEATTACHMENT{name="SAP3a.png" attachment="SAP3a.png" attr="h"
comment="edit defaults" date="1462437687" path="SAP3a.png" size="13389"
user="kenneth" version="1"}
