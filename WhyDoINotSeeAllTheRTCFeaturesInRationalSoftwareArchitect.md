META:TOPICINFO{author="sbagot" date="1432742760" format="1.1"
version="1.18"}
META:TOPICPARENT{name="IntegrationsTroubleshootingRTCandIntegratedDevelopmentEnvironments"}

# Why can't I see all the Rational Team Concert features in Rational Software Architect? DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: Rational Team Concert 4.0.x, Rational Software Architect 8.5.x, Rational Software Architect for WebSphere 8.5.x. [why-cant-i-see-all-the-rational-team-concert-features-in-rational-software-architect-dkgray-authors-integrationstroubleshootingteam-build-basis-rational-team-concert-4.0.x-rational-software-architect-8.5.x-rational-software-architect-for-websphere-8.5.x.]

ENDCOLOR

TOC{title="Page contents"}

This page describes what to do if you do not see, for example, the Work
Items perspective after installing the Rational Team Concert Client for
Eclipse IDE (Extension) and Rational Software Architect for WebSphere in
the same IBM Installation Manager package group.

## Initial assessment

### Symptoms

\* After you install Rational Software Architect for WebSphere in the
same package group where you previously installed the Rational Team
Concert Client for Eclipse IDE, the Work Item perspective disappears.
Before the Rational Software Architect installation, the perspective was
visible. \* After you install Rational Team Concert for Eclipse IDE
(Extension install) in the same package group where you previously
installed Rational Software Architect for WebSphere, the Work Item
perspective is not visible. \* A NullPointerException with the stack
trace: java.lang.NullPointerException at
com.ibm.team.workitem.rcp.ui.WorkItemUI.openEditor(Unknown Source) at
com.ibm.team.workitem.rcp.ui.internal.explorer.view.AbstractWorkItemExplorer.openSelection(Unknown
Source) at
com.ibm.team.workitem.rcp.ui.internal.explorer.view.AbstractWorkItemExplorer\$7.open(Unknown
Source) at org.eclipse.jface.viewers.StructuredViewer\$2.run(Unknown
Source) may appear in the workspace log file when accessing Rational
Team Concert functionality while the Jazz Source Control Capability is
disabled, as reported in [APAR
PM72410](http://www.ibm.com/support/docview.wss?uid=swg1PM72410).

### Impact/scope

-   Does it affect multiple installations?

## Data gathering and subsequent analysis steps

### Installation Manager logs

**Note**: Performing these steps can be time consuming. Check first if a
capability is disabled, as that is faster (see "Possible causes" and
"Possible solutions").

1 Start IBM Installation Manager. 1 Collect the installation logs by
clicking **Help \> Export data for Problem Analysis** 1 Save the
resulting compressed file to a temporary folder. 1 Extract the files. 1
Check what exact products are installed by opening: `installed.xml`. 1
Look for installation errors by opening this file: `logs\index.xml`. 1
Compare the date and times of the installation logs with the
installation history: `histories\index.xml`. This helps in establishing
the phase during which the installation errors occurred.

### Workspace logs

1 Gather this file: workspace\\metadata\\log 1 In the file, look for any
exceptions that occurred at the time when you tried to access Rational
Team Concert features.

## Possible causes

### A capability is not enabled, but the product is correctly installed \* When you install Rational Team Concert in the same package group with Rational Software Architect, you will see a new capability called **Jazz Source Control**. This capability is not enabled by default. This capability is not visible in a standalone Rational Team Concert client installation.

### Installation errors

-   When installing two Eclipse-based products in the same Installation
    Manager package group, the Equinox P2 reconciler process runs. At
    times, this process fails to include all required components in the
    resulting Eclipse configuration.

### Incompatible product versions

-   Not all versions of Rational Team Concert and Rational Software
    Architect are compatible and can be installed in the same package
    group. The Rational Team Concert for Eclipse IDE (Extension install)
    is a smaller package designed specifically for installing on an
    existing Eclipse-based IDE, such as Rational Software Architect for
    WebSphere.

## Possible solutions

### Enable the Jazz Source Control capability

1 Start Rational Software Architect. 1 Click **Window \> Preferences \>
General \> Capabilities**. 1 Click **Advanced**. 1 Click **Team \> Jazz
Source Control**. 1 Try again to open the Work Items perspective by
clicking **Window \> Open Perspective \> Work Items**.

### Investigate any errors in the IBM Installation Manager logs

1 If the errors occur on only one machine, you might have to
uninstall/reinstall the two products. 1 If the same errors persist or
happen on multiple machines, it is possible that you have selected
incompatible product versions. If you have checked that the products are
compatible and the errors persist, contact [IBM Rational
Support](http://www.ibm.com/support/docview.wss?uid=swg27020747) and
supply the logs.

### Check for incompatible versions

1 Make sure that you have installed compatible versions of the two
products. 1 You can check for compatibility among IBM products using
this tool:
<http://www.ibm.com/software/reports/compatibility/clarity/softwarePrereqsMatrix.html>.
Note however, that FixPacks are currently not listed. 1 Check the
Rational Team Concert compatibility in the [Rational Software Architect
& Rational Software Architect for WebSphere Software v8.x - Supported
Integration Information
document](https://www.ibm.com/support/docview.wss?uid=swg27019498&wv=1#RTC)

##### Related topics: [related-topics]

-   Still need help troubleshooting your integrations issue? Refer to
    [Integrations Troubleshooting](IntegrationsTroubleshooting) for
    additional topics.

##### External links: \* <http://www.ibm.com/software/reports/compatibility/clarity/softwarePrereqsMatrix.html> [external-links-httpwww.ibm.comsoftwarereportscompatibilityclaritysoftwareprereqsmatrix.html]

-   <https://www.ibm.com/support/docview.wss?uid=swg27019498&wv=1#RTC>
-   The Work Items perspective is not available in Rational Team
    Concert: <http://www.ibm.com/support/docview.wss?uid=swg21455459>

##### Additional contributors: Main.LaraZiosi [additional-contributors-main.laraziosi]
