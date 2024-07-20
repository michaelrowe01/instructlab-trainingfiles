META:TOPICINFO{author="zeech" date="1446825604" format="1.1"
reprev="1.12" version="1.12"}
META:TOPICPARENT{name="RationalTeamConcertIntegrations"}

# How to use Jazz Ant Tasks for Microsoft Visual Studio RTC builds DKGRAY Authors: Main.ZeeshanChoudhry Build basis: IBM Rational Team concert 4.x , 5.x and above. Microsoft Visual Studio 2012 and above. ENDCOLOR [how-to-use-jazz-ant-tasks-for-microsoft-visual-studio-rtc-builds-dkgray-authors-main.zeeshanchoudhry-build-basis-ibm-rational-team-concert-4.x-5.x-and-above.-microsoft-visual-studio-2012-and-above.-endcolor]

TOC{title="Page contents"}

## Introduction.

This articles explains how you can use the Jazz Ant Tasks in the IBM
Rational Team Concert (RTC) build for Microsoft Visual Studio (VS)
projects or solutions. For integration support and requirements details
please visit [System Requirements](CLMSystemRequirements60)

## Prerequisites

1.  Microsoft Visual Studio 2012
2.  RTC 5.0.2 plugin installed in VS [Download
    Here](https://jazz.net/downloads/rational-team-concert/)
3.  This article assumes you have already shared a VS project with RTC
    Source Control that you want to build with RTC Jazz Build Engine
    (JBE)
4.  Microsoft Windows SDK and .NET Framework 4 installed on the machine
    where you want to build your VS solutions/Projects.
5.  RTC Jazz Build Tool Kit [Download
    Here](https://jazz.net/downloads/rational-team-concert/)

### Creating the MSBuild project XML file.

-   We first create a MSBuild project file to hold common properties for
    re-usability such as the command to invoke Ant, the location of the
    Jazz build file in which you use the Jazz Ant Tasks and the location
    of the build properties file.

<!-- -->

-   Launch the Visual Studio IDE and open the solution you are
    interested in by setting the **Sandbox** current in **Team
    Artifacts** view or by loading the workspace which your project
    source code is shared in. Add a new XML File Item and name it
    **CommonProperties.xml**. Open the file for editing and add the
    following content to it.

C:\BuildToolKit\jazz\buildsystem\buildengine\eclipse\plugins\org.apache.ant_1.7.1.v20100518-1145\bin\ant.bat
-lib C:\BuildToolKit\jazz\buildsystem\buildtoolkit -propertyfile
\$(fetchDestination)\build.properties -f
\$(fetchDestination)\TBDForm\TBDForm\build.xml

Above

**AntCommand** uses the ant executable packaged with the Jazz Build Tool
Kit.

**propertyFile** This file is automatically created when the Build is
triggered. You can chose any location where you want this file to be
created. By default , if you specify just the file name as
"build.properties" in the Build Definition **Microsoft Build** tab, it
gets created in the directory where jbe.exe resides. Check addition
details in [Setting up Build Definition in
RTC](HowToUseJazzAntTasksForMicrosoftVisualStudioRTCBuilds#Setting_up_Build_Definition_in_R)
section of this article.

**jazzbuildxml** is the file in which you will define the Ant Targets to
build. See below.

**Please note** the paths mentioned above and in rest of article depends
on where you save the files in your Visual Studio Solution or where they
are located. In this article paths are used from the system where the
setup was created. So replace the paths according to your setup.

### Creating the Ant build XML file.

-   Next create the Ant build file which will hold the Jazz Ant tasks
    that you would like to use. Add a new XML File Item to your Visual
    Studio Solution and name it **build.xml**. Open the file for
    editing, and add the following content to it. The [Jazz build Ant
    Task
    Reference](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.team.build.doc/topics/r_ant-tasks.html&scope=null)
    pages detail the various Ant tasks that RTC provides. As an example
    in the build.xml file below we are using **startBuildActivity**,
    **artifactFilePublisher** and **linkPublisher** to contribute
    additional information to the build results.

<!-- -->

-   ICON{warning} **Note**: Do not use artifactFilePublisher task to
    publish artifacts that are larger than 10 megabytes. You must store
    and manage large artifacts outside of the repository. The
    artifactLinkPublisher task enables you to store a link in the
    repository, which points to your HTTP or FTP server where your large
    artifacts are stored.For more information refer to [Jazz build Ant
    Task
    Reference](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.team.build.doc/topics/r_ant-tasks.html&scope=null)

### Modifying the .csproj file.

-   Now we import the properties defined in **CommonProperties.xml**
    into one or more of the Visual Studio project files which will be
    used during the build process. You need to first unload the project
    to be able to edit its project file source in Visual Studio.You can
    also edit the **.csproj** file in note pad directly.

Find the following line the .csproj file

Add the following line after it:

Location of the MSbuild property file depends upon where you have
created it in the VS Project Directory.

-   Save the file.

## ICON{led-red}Creating conditions to execute Ant command only when a build is requested from RTC. ICON{wip}

There are two ways to achieve this.

### 1. Creating a new Visual Studio Build Configuration for RTC Builds.

-   Create a new build configuration for the project in Visual Studio
    IDE using **Configuration Manager**.

<!-- -->

-   In Visual Studio IDE , click Build \> Configuration Manager \>
    Active Solution Configuration \> New .

**Note:** Do not make a copy of the other Build configuration. Create a
new one from scratch. eg **RTCBuildDebug**.

**Add Pre-Build and Post-Build Event to the MSBuild**

\* Right click on the Project in VS **Solution Explorer** Tan and from
the context menu select **Properties**.

\* Under Build Events TAB add the following commands: \* **Pre-Build
Command**

if \$(Configuration) == RTCBuildDebug (\$(AntCommand)
-DactivityLabel=Starting\_\$(AssemblyName) \$(propertyFile)
\$(jazzbuildxml) startActivity)

\* **Post-Build Command**

if \$(Configuration) == RTCBuildDebug (\$(AntCommand)
-DactivityLabel=Finished\_\$(AssemblyName) \$(propertyFile)
\$(jazzbuildxml) publishActivity)

-   Save the .csproj file. In essence the MS Build Pre/Post-Build event
    commands call Ant on the **startActivity** or **publishActivity**
    targets in the **build.xml** file. The \*if \$(Configuration) ==
    RTCBuildDebug\* condition ensures that those tasks are only executed
    if we invoke the build using the Jazz Build Definition which is
    using **RTCBuildDebug** build configuration to build the project.
    Thus allowing the user to run build natively within Visual Studio
    using **Debug** or **Release** or any other configuration that is
    not used by RTC Build Definition.

### 2. Adding condition when fetchDestination has a value.

-   You can also use the following **if** conditions. There is no need
    to create a new Build Configuration in Visual Studio for your
    projects if you use this method. \* **Pre-Build Command** if
    \$(fetchDestination) NEQ '' (\$(AntCommand)
    -DactivityLabel=Starting\_\$(AssemblyName) \$(propertyFile)
    \$(jazzbuildxml) startActivity) \* **Post-Build Command** if
    \$(fetchDestination) NEQ '' (\$(AntCommand)
    -DactivityLabel=Finished\_\$(AssemblyName) \$(propertyFile)
    \$(jazzbuildxml) publishActivity) \* For the above condition to work
    you must add the **Additional Arguments** in the RTC Build
    Definition. Please see the section [Setting up Build Definition in
    RTC](HowToUseJazzAntTasksForMicrosoftVisualStudioRTCBuilds#2_Adding_condition_when_fetchDes)
    -   ICON{warning} **Note:** For the above condition you might need
        to setup the system environment variable **fetchDestination**
        and give it a value **\${team.scm.fetchDestination}** if you
        want to build your project within Visual Studio natively as
        well. This will resolve to invalid path to the xml file and Ant
        command will fail. Your Visual Studio build will be successful.
        This is only required if you build your solution/projects
        natively in Visual Studio with **devenv** compiler.

<!-- -->

-   ICON{choice-yes} **Note:** After creating and modifying all these
    files, they need to be checked-in and delivered to the Stream from
    which you build the Visual Studio project from. So that the Build
    workspace defined in the RTC Build Definition can accept them into
    the load directory.

## Setting up Build Engine in RTC.

-   Create a new Build Engine in RTC Eclipse client for Jazz Build
    Engine template :[Create Build
    Engine](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.team.build.doc/topics/tcreatebuildengine.html&scope=null)

\* Start this Build Engine on your Build machine where the Build
Definition will load the source code and MSBuild will run.

jbe -repository <https://server-vs.ibm.com:9443/ccm> -userId jazzadmin
-pass jazzadmin -engineId VS-Build-Engine -verbose

## Setting up Build Definition in RTC.

-   Create a new Build Defintion in RTC Eclipse client. [Create Build
    Definition](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.team.concert.dotnet.doc/topics/t_create_builddef.html&scope=null)

\* There are addition properties you need to set in the **Microsoft
Build** tab in the build definition based on the above configuration we
setup. \* **Build command** select `"msbuild.exe"` \* **Path to build
command** = `C:\Windows\Microsoft.NET\Framework\v4.0.30319` \*
**Solution/Project File Name** =
`${team.scm.fetchDestination}\TBDForm\TBDForm.sln` \* **Build
Configuration** = `RTCBuildDebug or Debug` \* **Build Log** =
`${team.scm.fetchDestination}\Compiler.log` \* **Additional Arguments**
= `/property:fetchDestination=${team.scm.fetchDestination}` \* **Working
Directory** = `${team.scm.fetchDestination}` \* **Properties file** =
`build.properties or ${team.scm.fetchDestination}\build.properties (The path is what you defined in *CommonProperties.xml* with *propertyFile* variable)`
\* **\${team.scm.fetchDestination}** =
`This is the location which you set in the Build Definition in *Jazz Source Control* tab for *Load directory*.`

Add the Build engine that you have created above to this Build
Definition under **Supporting Build Engines** section on **Overview**
tab. This setup is now complete. You can now execute the Microsoft
Visual Studio Builds from RTC which are going to use the Jazz Ant Task
you used in build.xml.

##### Related topics: [Deployment web home](WebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [Continuous Integration with Rational Team Concert and Microsoft
    Visual Studio](https://jazz.net/library/article/518)

##### Additional contributors: Main.ZeeshanChoudhry, [additional-contributors-main.zeeshanchoudhry]

META:FILEATTACHMENT{name="bevent.png" attachment="bevent.png" attr="h"
comment="Build Events tab" date="1441874106" path="bevent.png"
size="10230" user="zeech" version="1"}
META:FILEATTACHMENT{name="bdef.png" attachment="bdef.png" attr="h"
comment="Build Definition Settings" date="1441998910" path="bdef.png"
size="32817" user="zeech" version="1"}
