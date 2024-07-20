META:TOPICINFO{author="michaelrowe" date="1659376433" format="1.1"
version="1.7"} META:TOPICPARENT{name="JenkinsAndHudson"}

# Jenkins and Hudson builds stay in pending state. [jenkins-and-hudson-builds-stay-in-pending-state.]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: Products,
editions, or versions that apply to the content. If no build basis
applies to this content, set the build basis to None. ENDCOLOR

TOC{title="Page contents"}

Jenkins/Hudson and Engineering Workflow Management (EWM), formerly
Rational Team Concert (RTC), integration has two task loops that run
continuously,

-   Build Loop

The build loop's responsibility is to continuously check for a EWM build
request. This tasks runs normally every 15 secs. When such a request is
found, EWM will flip the build request from the Pending state to the
Running state. This will also connect to Jenkins and starts
corresponding the build there.

-   Sync loop

The sync loop will poll Jenkins/Hudson looking for EWM events that have
been generated in Jenkins/Hidson. When those events are found it will
parse the event and change the state of the build correspondingly.

## How do we troubleshoot the build requests become stuck in a state?

Knowing this basic concept how do we troubleshoot the build requests
become stuck in a state?

If you are using RTC 4.0.4 or earlier, it is likely you are hitting a
[Defect
287317](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/287317)
with how the connection logic was handled. There was an issue with when
the Jenkins/Hudson server is not usable for a certain period of time,
these both task will get stuck, which will cause builds to never
process. The tasks then never quits with connection timeout to
Jenkins/Hudson server and keeps on running until the server restart. Any
new build request that are sent to that same Jenkins/Hudson server will
stay in pending state for ever. It can also happen that the build
requested is sent to Jenkins/Hudson server but they are stuck at some
state where as the job is actually finished in the Jenkins/Hudson
server. This symptom is observed when Sync loop task is stuck contacting
the Jenkins/Hudson server. The Sync Loop task hang status is more likely
to happen when it tries to contact every build engine defined for
Jenkins/Hudson which is configured as active and monitoring last contact
time (the default). It takes just 1 unresponsive Jenkins server to hang
this task.

This defect will be fixed in future releases where you can configure in
the server properties a timeout value for these tasks.

## Investigating the problem.

Prior to ELM versions 7.0.1 SR1 / 7.0.2 SR1: To enable Build and Sync
Loop tracing, enable the debugging in the Change and Configuration
Management (CCM) log4j.properties file by adding the line

log4j.logger.com.ibm.rational.connector.hudson=DEBUG

For ELM versions 7.0.1 SR1 / 7.0.2 SR1 and beyond: To enable Build and
Sync Loop tracing, enable the debugging in the Change and Configuration
Management (CCM) log4j2.xml file by adding the entry

The CCM log will start filling up with Jenkins/Hudson integration debug
data.

Example:

2013-10-15 00:34:03,209 \[ccm: AsynchronousTaskRunner-4 @@ 00:34\] DEBUG
com.ibm.rational.connector.hudson - queryPendingBuildRequests enter
2013-10-15 00:34:03,240 \[ccm: AsynchronousTaskRunner-4 @@ 00:34\] DEBUG
com.ibm.rational.connector.hudson - queryPendingBuildRequests exit,
found 5 requests, took 31 ms 2013-10-15 00:34:03,381 \[ccm:
AsynchronousTaskRunner-4 @@ 00:34\] DEBUG
com.ibm.rational.connector.hudson - personalBuildFilterMatches enter
2013-10-15 00:34:03,381 \[ccm: AsynchronousTaskRunner-4 @@ 00:34\] DEBUG
com.ibm.rational.connector.hudson - personalBuildFilterMatches
personalBuildFilter: null 2013-10-15 00:34:03,381 \[ccm:
AsynchronousTaskRunner-4 @@ 00:34\] DEBUG
com.ibm.rational.connector.hudson - personalBuildFilterMatches exit
with: true

Above you see poll was executed to find the build requests.

Please note: This logging is not very detailed as of now in Rational
Team Concert 4.0.4. In later releases this trace will increase the
amount of debug information put in the log.

In case if you encounter the problem with build loop or sync loops are
stuck you can verify this in the "Active Services" page of CCM
application admin page. The services names are

com.ibm.rational.hudson.team.internal.service.HudsonBuildLoopScheduledTask.executeTask

com.ibm.rational.hudson.team.internal.service.HudsonSyncLoopScheduledTask.executeTask

If you click at "Show Details" on that "Active Services" page against
the service running you can see the call stack of the running service.
This can help you identify the problem with the Builds.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.ZeeshanChoudhry [additional-contributors-main.zeeshanchoudhry]
