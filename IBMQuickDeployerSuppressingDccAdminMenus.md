META:TOPICINFO{author="ktessier" date="1501278329" format="1.1"
version="1.6"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRunOld"}

# IBM Quick Deployer suppressing dcc admin menus DKGRAY [ibm-quick-deployer-suppressing-dcc-admin-menus-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

After CLM has been installed by Quick Deployer v1.0 and v1.1 the
**Application Administration - Data Collection Component (/dcc/admin)**
page contains the following menus: Application, Users, Project Areas,
Templates and Reports. Starting with Quick Deployer v1.2 the menus
Project Areas and Templates are hidden because they are not relevant to
the Data Collection Component application. To avoid confusion with prior
versions of Quick Deployer the menus Project Areas and Templates can be
hidden by following the instructions below.

## Suppressing dcc admin menus

To suppress the **\[Project Areas and Templates\]** menus do the
following on the dcc admin page.

1\. Open the dcc admin page and click on **Advanced Properties**

1\. Scroll down the **Advanced Properties** page to the
*com.ibm.team.repository.service.internal.webuiInitializer.ConfigPropertyInitializer*
section and click **Edit**

1\. To hide the \[Project Areas and Templates\] menus enter the
following value for the **Suppressed Web Pages** property
*{"com.ibm.team.repository.web.admin":
\["com.ibm.team.repository.provision"\], "com.ibm.team.app.web.admin":
\["com.ibm.team.process.ProjectAreaManagement",
"com.ibm.team.process.ProcessTemplateManagement",
"com.ibm.team.process.AccessGroupManagement"\]}*

1\. Click **Preview** and exit edit mode, the new value for the
**Suppressed Web Pages** property will be displayed

1\. Scroll back to the top of the **Advanced Properties** page and click
**Save** and wait till the configuration change is saved

1\. Reload the page and the menus will have been disabled

NOTE: if you want all the menus displayed again enter the following in
step 3 *{"com.ibm.team.repository.web.admin":
\["com.ibm.team.repository.provision"\]}*

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="dcc1.png" attachment="dcc1.png" attr="h"
comment="display dcc advanced properties" date="1457348779"
path="dcc1.png" size="64501" user="kenneth" version="1"}
META:FILEATTACHMENT{name="dcc2.png" attachment="dcc2.png" attr="h"
comment="open editor for suppress pages property" date="1457348830"
path="dcc2.png" size="10522" user="kenneth" version="1"}
META:FILEATTACHMENT{name="dcc4.png" attachment="dcc4.png" attr="h"
comment="save suppress pages property" date="1457349853" path="dcc4.png"
size="78977" user="kenneth" version="2"}
META:FILEATTACHMENT{name="dcc5.png" attachment="dcc5.png" attr="h"
comment="reload dcc pages" date="1457348942" path="dcc5.png"
size="32433" user="kenneth" version="1"}
META:FILEATTACHMENT{name="dcc6.png" attachment="dcc6.png" attr="h"
comment="edit suppress pages property" date="1457372110" path="dcc6.png"
size="11436" user="kenneth" version="2"}
META:FILEATTACHMENT{name="dcc7.png" attachment="dcc7.png" attr="h"
comment="close editor for suppress pages property" date="1457372126"
path="dcc7.png" size="13209" user="kenneth" version="2"}
