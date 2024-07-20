META:TOPICINFO{author="michaelrowe" date="1659376747" format="1.1"
version="1.5"}
META:TOPICPARENT{name="IntegrationsTroubleshootingRTCandBuildforge"}

# Rational Team Concert build properties are not transferred to Rational Build Forge [rational-team-concert-build-properties-are-not-transferred-to-rational-build-forge]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: Rational
Team Concert 3.x, 4.x, 5.x, 6.x, Engineering Workflow Management 7.x
ENDCOLOR

TOC{title="Page contents"}

In Engineering Workflow Management (EWM), formerly known as Rational
Team Concert (RTC), for each Build definition for Rational Build Forge
integration , You set up the build properties.

In most cases you would need to setup the ones below:

-   Build_Engine_Path
-   Build_User
-   Build_Password
-   Build_Toolkit_path
-   Repository_Address

It might be necessary you would need to setup more of these properties,
depending on your need.

## Enabling Build Forge debug in the CCM log

For versions prior to EWM 7.0.1 SR1 / EWM 7.0.2 SR1: To verify if the
properties are updated in the Build Forge Project correctly we need to
enable the logging in Rational Team Concert for Build Forge Integration.
Enable the debugging in the CCM application log4j properties by changing
the line

log4j.logger.com.ibm.rational.buildforge= WARN

to

log4j.logger.com.ibm.rational.buildforge= ALL

and restarting the CCM logging infrastructure; see [Manipulating CLM
Log4j - Log4j and
CLM](https://jazz.net/wiki/bin/view/Deployment/ManipulatingCLMLog4j#Log4j_and_CLM)
for more information.

For versions EWM 7.0.1 SR1 / EWM 7.0.2 SR1 and later: To verify if the
properties are updated in the Build Forge Project correctly we need to
enable the logging in Rational Team Concert for Build Forge Integration.
Enable the debugging in the CCM application log4j2.xml by changing the
line

to

and restarting the CCM logging infrastructure; see [Manipulating CLM
Log4j - Log4j and
CLM](https://jazz.net/wiki/bin/view/Deployment/ManipulatingCLMLog4j#Log4j_and_CLM)
for more information.

The CCM log (ccm.log) will start filling up with Build Forge integration
debug data.

## Investigating the CCM log.

When you make a build request , you would see this log entry in ccm.log

2013-11-11 08:25:08,340 \[ccm: AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - buildDefInst:
<com.ibm.team.build.internal.common.model.impl.BuildDefinitionInstanceImpl@1eb91eb9>
(internalId: \[UUID \_rcvltErUEeOn_u3QK8c59g\]) (buildDefinitionId:
BuildForge_JBE build, label: , description: , ignoreWarnings: true)
2013-11-11 08:25:08,340 \[ccm: AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - configurationData:
Build definition: BuildForge_JBE build Project name: BF_Project_JBE
Project uuid: 5d0d75490c601000bdeea3917cfe7cfe Host name: localhost
Secure connection: true Port: 3966 Server key: localhost:3966 User id:
null All logs: true All logs not passed or skipped: false Custom BOM
enabled: true Num first logs:: 5 First logs enabled: false Num last
logs: 5 Last logs enabled: false 2013-11-11 08:25:08,340 \[ccm:
AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable -
engineConfigurationData: Engine ID: BF_engineEngine UUID:
\_5pI9YIG6EeKAxNIURYE-1w Has configuration: true Host name: 9.142.57.67
Secure connection: false Port: 3966 Server key: 9.142.57.67:3966 User
id: build 2013-11-11 08:25:08,774 \[ccm: AsynchronousTaskRunner-3 @@
08:25\] DEBUG .team.internal.service.BuildForgeBuildLoopRunnable -
buildPropsMap:
{scheduledBuild`false, buildEngineHostName=default, buildResultUuid=default, team.scm.deliver.componentsToDeliver=_jJuxEIG6EeKhEIJR9zCjrA, buildEngineId=default, team.scm.deliver.addNewComponentsToTarget=false, Build_Password=jazzadmin, personalBuild=false, Build_Engine_Path=c:\JazzBuild\jazz\buildsystem\buildengine\eclipse, buildRequesterUserId=default, team.scm.deliver.changeSnapshotOwner=false, team.scm.componentLoadRules`,
team.scm.deliver.enabled`true, team.scm.fetchDestination=C:\BF_Build, Build_Toolkit_Path=C:\JazzBuild\jazz\buildsystem\buildtoolkit, ANT_HOME=C:\Eclipse\jazz\client\eclipse\plugins\org.apache.ant_1.7.1.v20100518-1145, team.scm.deliver.targetUUID=_jITNsIG6EeKhEIJR9zCjrA, buildLabelPrefix=T, JAVA_HOME=C:\Program Files\Java\jdk1.7.0_15, team.scm.deliver.triggerPolicy=NO_ERRORS, buildLabel=Zee_build, buildResultUUID=default, com.ibm.team.build.internal.template.id=com.ibm.rational.connector.buildforge.ui.buildDefinitionTemplate, buildEngineID=BF_Engine, team.scm.workspaceUUID=_LaCWsIG8EeKhEIJR9zCjrA, team.scm.buildOnlyIfChanges=true, team.scm.deliver.abortOnIncompleteActivity=false, team.scm.acceptBeforeFetch=true, team.scm.createFoldersForComponents=false, team.scm.deleteDestinationBeforeFetch=true, team.scm.deliver.removeComponentsInTarget=false, team.scm.includeComponents=false, Build_User=jazzadmin, engineUUID=default, team.scm.deliver.deliverAllComponents=false, team.scm.loadComponents`,
Repository_Address=<https://9.142.63.252:9443/ccm>} 2013-11-11
08:25:08,774 \[ccm: AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - IBuildResult:
<com.ibm.team.build.internal.common.model.impl.BuildResultImpl@51d851d8>
(stateId: \[UUID \_ryhBYErUEeOn_u3QK8c59g\], itemId: \[UUID
\_rcvlsErUEeOn_u3QK8c59g\], origin: , immutable: true) (contextId:
\[UUID \_fTQ10IG6EeKAxNIURYE-1w\], modified: 2013-11-11 08:25:08.342,
workingCopy: false) (mergePredecessor: null, workingCopyPredecessor:
null, workingCopyMergePredecessor: null, predecessor: \[UUID
\_rhSHcErUEeOn_u3QK8c59g\]) (buildStatus: OK, buildState: IN_PROGRESS,
label: , buildTimeTaken: -1, buildStartTime: 1384176308340, summary: ,
ignoreWarnings: true, tags: , deleteAllowed: true, personalBuild: false)

Notice the buildPropsMap line above which has all the properties listed
for this particular build request.

Now these properties are updated to the Build Forge environment which
can be observed in the CCM.log.

2013-11-11 08:25:09,105 \[ccm: AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - build def
properties:
{scheduledBuild`false, buildEngineHostName=default, buildResultUuid=default, team.scm.deliver.componentsToDeliver=_jJuxEIG6EeKhEIJR9zCjrA, buildEngineId=default, team.scm.deliver.addNewComponentsToTarget=false, Build_Password=jazzadmin, personalBuild=false, Build_Engine_Path=c:\JazzBuild\jazz\buildsystem\buildengine\eclipse, buildRequesterUserId=default, team.scm.deliver.changeSnapshotOwner=false, team.scm.componentLoadRules`,
team.scm.deliver.enabled`true, team.scm.fetchDestination=C:\BF_Build, Build_Toolkit_Path=C:\JazzBuild\jazz\buildsystem\buildtoolkit, ANT_HOME=C:\Eclipse\jazz\client\eclipse\plugins\org.apache.ant_1.7.1.v20100518-1145, team.scm.deliver.targetUUID=_jITNsIG6EeKhEIJR9zCjrA, buildLabelPrefix=T, JAVA_HOME=C:\Program Files\Java\jdk1.7.0_15, team.scm.deliver.triggerPolicy=NO_ERRORS, buildLabel=Zee_build, buildResultUUID=default, com.ibm.team.build.internal.template.id=com.ibm.rational.connector.buildforge.ui.buildDefinitionTemplate, buildEngineID=BF_Engine, team.scm.workspaceUUID=_LaCWsIG8EeKhEIJR9zCjrA, team.scm.buildOnlyIfChanges=true, team.scm.deliver.abortOnIncompleteActivity=false, team.scm.acceptBeforeFetch=true, team.scm.createFoldersForComponents=false, team.scm.deleteDestinationBeforeFetch=true, team.scm.deliver.removeComponentsInTarget=false, team.scm.includeComponents=false, Build_User=jazzadmin, engineUUID=default, team.scm.deliver.deliverAllComponents=false, team.scm.loadComponents`,
Repository_Address=<https://9.142.63.252:9443/ccm>} 2013-11-11
08:25:09,105 \[ccm: AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - Checking build
environment name`value: B`, action=SET, vartype=STANDARD, mode=NORMAL,
include uuid=null 2013-11-11 08:25:09,106 \[ccm:
AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - Checking build
environment name`value: BF_T`, action=SET, vartype=STANDARD,
mode=NORMAL, include uuid=null 2013-11-11 08:25:09,106 \[ccm:
AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - Checking build
environment name`value: BF_D`, action=SET, vartype=STANDARD,
mode=NORMAL, include uuid=null 2013-11-11 08:25:09,106 \[ccm:
AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - Checking build
environment name`value: BF_W`, action=SET, vartype=STANDARD,
mode=NORMAL, include uuid=null 2013-11-11 08:25:09,106 \[ccm:
AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - Checking build
environment name`value: BF_J`, action=SET, vartype=STANDARD,
mode=NORMAL, include uuid=null ...

2013-11-11 08:25:09,116 \[ccm: AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - Checking build
environment name=value: buildResultUuid=default, action=SET,
vartype=STANDARD, mode=NORMAL, include uuid=null 2013-11-11 08:25:09,116
\[ccm: AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - Build property
value: default 2013-11-11 08:25:09,116 \[ccm: AsynchronousTaskRunner-3
@@ 08:25\] DEBUG .team.internal.service.BuildForgeBuildLoopRunnable -
buildResultUUID value updated with: \_rcvlsErUEeOn_u3QK8c59g 2013-11-11
08:25:09,116 \[ccm: AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - Updating build
environment name=value: buildResultUuid=\_rcvlsErUEeOn_u3QK8c59g, entry
uuid=36c2db620c651000b65ba39146ea46ea 2013-11-11 08:25:09,116 \[ccm:
AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
dforge.team.internal.service.BuildForgeDataManager - Connection returned
from pool for key:
9.142.57.67:3966:build:/DDDHXmTmkU=:bfBuildPollerThread =
<com.buildforge.services.client.api.APIClientConnection@b470b47>
2013-11-11 08:25:09,136 \[ccm: AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - Checking build
environment name=value: buildResultUUID=default, action=SET,
vartype=STANDARD, mode=NORMAL, include uuid=null 2013-11-11 08:25:09,136
\[ccm: AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - Build property
value: default 2013-11-11 08:25:09,136 \[ccm: AsynchronousTaskRunner-3
@@ 08:25\] DEBUG .team.internal.service.BuildForgeBuildLoopRunnable -
buildResultUUID value updated with: \_rcvlsErUEeOn_u3QK8c59g 2013-11-11
08:25:09,136 \[ccm: AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - Updating build
environment name=value: buildResultUUID=\_rcvlsErUEeOn_u3QK8c59g, entry
uuid=36c2db660c651000b663a39146ea46ea 2013-11-11 08:25:09,140 \[ccm:
AsynchronousTaskRunner-3 @@ 08:25\] DEBUG
.team.internal.service.BuildForgeBuildLoopRunnable - Build property
value: jazzadmin 2013-11-11 08:25:09,140 \[ccm: AsynchronousTaskRunner-3
@@ 08:25\] DEBUG .team.internal.service.BuildForgeBuildLoopRunnable -
Updating build environment name=value: Build_User=jazzadmin, entry
uuid=36c2db6a0c651000b66ba39146ea46ea ... ...

When a build is started in RTC, the Build Loop task will pull up the
Build Forge project environment and iterate through it replacing the RTC
defined properties, e.g. **buildResultUuid**. So without the variables
defined in Build Forge, RTC will not be able swap in the correct values
for those RTC defined variables. This swapping in of RTC properties into
Build Forge variables only affects those Build Forge variables at the
project environment level. Other environments set a lower levels, e.g.
step level, can still overwrite these variables again, setting them into
another value that will likely be an invalid value. Make sure that the
RTC specific variables are only set ONCE in the Build Forge project, at
the project environment level!

Using the above log entries you can identify what properties are sent to
Build Forge project.

Now you can check the Build Forge Step logs to see what values are set
for these properties

81 11/11/13 2:39 PM SET
Build_Toolkit_Path=C:\JazzBuild\jazz\buildsystem\buildtoolkit 82
11/11/13 2:39 PM SET
Build_Engine_Path=c:\JazzBuild\jazz\buildsystem\buildengine\eclipse 85
11/11/13 2:39 PM SET Build_Password=jazzadmin 94 11/11/13 2:39 PM SET
buildResultUuid=\_rcvlsErUEeOn_u3QK8c59g

152 11/11/13 2:39 PM ENV buildResultUuid=\_rcvlsErUEeOn_u3QK8c59g 153
11/11/13 2:39 PM ENV
Build_Engine_Path=c:\JazzBuild\jazz\buildsystem\buildengine\eclipse 155
11/11/13 2:39 PM ENV
Build_Toolkit_Path=C:\JazzBuild\jazz\buildsystem\buildtoolkit 156
11/11/13 2:39 PM ENV Build_User=jazzadmin

And then you can observe in the same step log what values of these
properties are getting used in the execution of a command:

Command Set Parsed To:
\[c:\JazzBuild\jazz\buildsystem\buildengine\eclipse/jbe -userId
jazzadmin -pass jazzadmin -repository <https://9.142.63.252:9443/ccm>
-buildResultUUID \_rcvlsErUEeOn_u3QK8c59g -engineUUID
\_5pI9YIG6EeKAxNIURYE-1w -participants com.ibm.team.build.jazzscm
-noComplete -verbose

If the values are passed correctly from RTC to Build Forge then problem
is probably at the Rational Build Forge side.

-   Check the step logs and verify if the values are getting overridden.
-   Make sure the "Environment" of the Build Forge Project is selected
    at the Project Level and no "step" environment is overidding the
    values.
-   If you determine that the build environments are getting interrupted
    in the middle of the update with an exception stack like , then the
    problem is with Build Forge sessions thrashing.

## Dedicated Rational Build Forge Users.

If you have multiple RTC instances pointing to the same Rational Build
Forge instance, but use the same Rational Build Forge userid between the
RTC instances, then the Rational Build Forge sessions will thrash. This
can cause problems where sometimes RTC will attempt to update Rational
Build Forge with an invalidated session that causes the environment
update to cease. This logic has been reinforced in 4.0 and 3.0.1.5, but
we still recommend that for all integrations that all RTC instances have
a unique Rational Build Forge userid to prevent the thrash from
occuring.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.ZeeshanChoudhry [additional-contributors-main.zeeshanchoudhry]
