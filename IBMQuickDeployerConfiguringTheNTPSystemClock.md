META:TOPICINFO{author="ktessier" date="1496871798" format="1.1"
version="1.12"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRun"}

# IBM Quick Deployer configuring the NTP system clock DKGRAY [ibm-quick-deployer-configuring-the-ntp-system-clock-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

For a multi server CLM system it is important that the reference clock
used by each server is accurate and consistent. One way to do this is to
configure the system to use a Network Time Protocol (NTP) as a reference
for each server. This topic explains how to do this.

## Configuring the NTP system clock If the **Install Applications** process was not configured to enable the System Clock to use an NTP server then a **CRJAZ2108W diagnostic warning** will appear on each applications admin page. To clear this warning do the following on each admin page.

1\. Open the applications admin page and click on **Advanced
Properties**

1\. Scroll down the **Advanced Properties** page to the
***com.ibm.team.repository.service.diagnostics.basic.internal.SystemClockDiagnostic***
section and click **Edit**.

1\. Enter the a value for the **NTP server address property** and click
**Preview** to exit edit mode.

1\. Scroll back to the top of the **Advanced Properties** page and click
**Save**, then wait until the configuration change is saved.

1\. Navigate to the applications diagnostics page and **Run** the
**System Clock** diagnostic to confirm the configuration change was
successful.

1.  Repeat for each application.

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="NTP_1.png" attachment="NTP_1.png" attr="h"
comment="diagnostic clock warning" date="1443696098" path="NTP_1.png"
size="72260" user="kenneth" version="1"}
META:FILEATTACHMENT{name="NTP_2.png" attachment="NTP_2.png" attr="h"
comment="advanced properties clock section" date="1443696315"
path="NTP_2.png" size="7080" user="kenneth" version="1"}
META:FILEATTACHMENT{name="NTP_3.png" attachment="NTP_3.png" attr="h"
comment="enter ntp server address" date="1443696148" path="NTP_3.png"
size="7936" user="kenneth" version="1"}
META:FILEATTACHMENT{name="NTP_4.png" attachment="NTP_4.png" attr="h"
comment="save changes" date="1443696177" path="NTP_4.png" size="62393"
user="kenneth" version="1"} META:FILEATTACHMENT{name="NTP_5.png"
attachment="NTP_5.png" attr="h" comment="rerun clock diagnostics"
date="1443696200" path="NTP_5.png" size="32790" user="kenneth"
version="1"} META:TOPICMOVED{by="tomp" date="1443819267"
from="Deployment.IBMQuickDeployerConfiguringTheNtpSystemClock"
to="Deployment.IBMQuickDeployerConfiguringTheNTPSystemClock"}
