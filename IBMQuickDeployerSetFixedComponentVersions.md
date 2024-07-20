META:TOPICINFO{author="tomp" date="1455138286" format="1.1"
version="1.11"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRun"}

# IBM Quick Deployer set fixed component versions DKGRAY [ibm-quick-deployer-set-fixed-component-versions-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

To prevent the user from having to select a version for the 5 components
each time they run the **Install Applications** process you can fix the
values on the process configuration tab. You can also fix the component
versions for the other application processes by switching which process
is selected in step 2 below. The remainder of the documentation will
assume you have fixed the component versions on all processes,
therefore, instructions for selecting components when running a process
typically will not be included.

## Setting fixed component versions

1\. Navigate to the **Applications** page and select the
**Rational_QD_60x** application

1\. Switch to the **Processes** tab and select the **Install
Applications** process

1\. On the process **Configuration** tab select **Basic Settings**

1\. Set all 5 components to a **Specific Version**, typically you would
select the latest version of each component from the version drop down
list. For the initial install of QD version 1.0 the latest should be
**6.0.0.0**. Once all versions are set press **Save**.

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="SFCV_1.png" attachment="SFCV_1.png" attr="h"
comment="select application" date="1443718134" path="SFCV_1.png"
size="21070" user="kenneth" version="1"}
META:FILEATTACHMENT{name="SFCV_2.png" attachment="SFCV_2.png" attr="h"
comment="select process" date="1443718151" path="SFCV_2.png"
size="41111" user="kenneth" version="1"}
META:FILEATTACHMENT{name="SFCV_3.png" attachment="SFCV_3.png" attr="h"
comment="basic settings" date="1443718169" path="SFCV_3.png"
size="20227" user="kenneth" version="1"}
META:FILEATTACHMENT{name="SFCV_4.png" attachment="SFCV_4.png" attr="h"
comment="set component versions" date="1443718200" path="SFCV_4.png"
size="37310" user="kenneth" version="1"}
