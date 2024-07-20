META:TOPICINFO{author="trushank19" date="1702891031" format="1.1"
version="1.2"}

# Configuring Eclipse with a VM parameter to avoid "unconfigured" project area editors DKGRAY Authors: Main.LarrySmith Build basis: CLM 6.0+, Eclipse 4.4+, Java 8 [configuring-eclipse-with-a-vm-parameter-to-avoid-unconfigured-project-area-editors-dkgray-authors-main.larrysmith-build-basis-clm-6.0-eclipse-4.4-java-8]

ENDCOLOR

TOC{title="Page contents"}

This article discusses how to configure recent Eclipse (e.g. Eclipse 4.4
Neon) versions to remove an issue where the project area is shown with
all sections "Unconfigured".

## VM Argument to Enable Access to External Schema

The issue is caused by a new Java VM parameter that requires opt-in to
allow the client to access external schema, which is required to
configure the project area. When opening a project area editor in
Eclipse, all sections are shown as "Unconfigured".

In addition, an error in the process configuration.xml flags to the
access to external schema. The failing "Schema Error" line in the
process.xml is like:

The fix for this is to add a VM argument to the eclipse.ini file. In
Windows this file is the Eclipse installation directory; in Mac you must
select eclipse.app and use the menu item "Show Package Contents" then
update the /Content/MacOS/eclipse.ini file.

The change is to add a line at the end:

-Djavax.xml.accessExternalSchema=all

A final eclipse.ini file may look like this:

-startup
../../../plugins/org.eclipse.equinox.launcher_1.3.0.v20140415-2008.jar
--launcher.library
../../../plugins/org.eclipse.equinox.launcher.cocoa.macosx.x86_64_1.1.200.v20150204-1316
-product org.eclipse.epp.package.java.product --launcher.defaultAction
openFile -showsplash org.eclipse.platform --launcher.XXMaxPermSize 512m
--launcher.defaultAction openFile --launcher.appendVmargs -vmargs
-Dosgi.requiredJavaVersion=1.8 -XstartOnFirstThread
-Dorg.eclipse.swt.internal.carbon.smallFonts -XX:MaxPermSize=2048m
-Xms120m -Xmx2048m -Xdock:icon=../Resources/Eclipse.icns
-Djavax.xml.accessExternalSchema=all

----++ External Links

-   [Stack Overflow
    Discussion](http://stackoverflow.com/questions/23011547/webservice-client-generation-error-with-jdk8)
-   [Oracle Documentation on Access External
    Schema](http://docs.oracle.com/javase/7/docs/api/javax/xml/XMLConstants.html#ACCESS_EXTERNAL_SCHEMA)
