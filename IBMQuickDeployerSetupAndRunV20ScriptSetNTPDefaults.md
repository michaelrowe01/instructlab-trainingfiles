META:TOPICINFO{author="ktessier" date="1502126383" format="1.1"
version="1.3"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRun"}

# Setting NTP system clock default values DKGRAY [setting-ntp-system-clock-default-values-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

For a multi-server CLM system it is important that the reference clock
used by each server is accurate and consistent. One way to do this is to
configure the system to use a Network Time Protocol (NTP) as a reference
for each server. To configure IBM Quick Deployer so that the
applications that it installs use an NTP system clock, edit the
**Prepare System** step of the **Install Applications** process.

If the NTP system clock is disabled, you can be enable it after the CLM
applications have been installed. For details, see [Configuring the NTP
system clock](IBMQuickDeployerConfiguringTheNTPSystemClock).

## Configuring default NTP clock values

1\. Login to the target UCD server as an administrator. 1. Click
Applications, then select the Quick Deployer application.

1\. Click **Processes**, then select the **Install Applications
process**.

1\. On the process **Design** tab open the **Prepare System** step by
clicking on the pencil icon.

1\. Select **True** in the **EnableNTPclock** field. Note: If you leave
the value of the field cleared, Quick Deployer prompts you to enter a
value of True or False in the Run Process dialog when you select the
**Install Applications** process. 1. Enter the name of the NTP system
clock server in the **NTPclock** field.

1.  Click **OK** to close the **Edit Properties** window.
2.  Click the **Save** process icon to save your changes.

## Results

When you run the **Install Applications** process, the Quick Deployer
sets the NTP server address property in the CLM applications to the
value that you specify in the **NTPclock** field.

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="ntp-clock-setv20.png"
attachment="ntp-clock-setv20.png" attr="h" comment="" date="1498852838"
path="ntp-clock-setv20.png" size="33217" user="ktessier" version="1"}
META:FILEATTACHMENT{name="AS_11.png" attachment="AS_11.png" attr="h"
comment="" date="1498852851" path="AS_11.png" size="57161"
user="ktessier" version="1"} META:FILEATTACHMENT{name="AS_10v13.png"
attachment="AS_10v13.png" attr="h" comment="" date="1498852864"
path="AS_10v13.png" size="38144" user="ktessier" version="1"}
META:FILEATTACHMENT{name="AS_7.png" attachment="AS_7.png" attr="h"
comment="" date="1498852876" path="AS_7.png" size="21070"
user="ktessier" version="1"}
