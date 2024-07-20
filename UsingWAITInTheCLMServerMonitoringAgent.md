META:TOPICINFO{author="geraldmi" date="1422299085" format="1.1"
reprev="1.1" version="1.1"}
META:TOPICPARENT{name="CLMServerMonitoringAgent"}

# Using WAIT in the CLM Server Monitoring Agent DKGRAY Authors: Gerald.Mitchell Build basis: CLM 5.0.2, CSM Agent 5.0.2 [using-wait-in-the-clm-server-monitoring-agent-dkgray-authors-gerald.mitchell-build-basis-clm-5.0.2-csm-agent-5.0.2]

ENDCOLOR

TOC{title="Page contents"}

This page is for basic information for how to enable WAIT for use with
CLM Server Monitoring Agent (CSM Agent).

## Setting The CLM Server Monitoring Agent To Use WAIT

Before being able to use the CLM Server Monitoring Agent with WAIT, the
WAIT capability must be configured. In the CLM Server Monitoring Agent,
the settings for WAIT are in the advanced properties of the CLM Server
Monitoring Agent administration page.

## Viewing The WAIT information in a CLM Server Monitoring Agent Project Dashboard.

In the default Project Dashboard for the project you are looking at in
the in the CLM Server Monitoring Agent, you will see a section titled
"WAIT Reports" in the top right-most (First row, third column) part of
the dashboard. The java cores themselves are under this section in a
section titled "Javacores" (Second row, third column) of the dashboard.

If this section is not in your Dashboard, it can be added by adding the
widget, available under the "/csm" widgets.

## Accessing WAIT information in CLM Server Monitoring Agent

In the WAIT Report work items, The Activities contain, in the links
section, a link to the WAIT site where the Agent server was configured
to create the work items.

## How WAIT Links Work

First, there needs to exist a WAIT server that can be accessed directly
by the CLM and Agent servers, on which exists a single account
accessible by the Agent users needing to access the WAIT data.

Second, the settings in the advanced properties of the Agent needs to be
configured to point at the WAIT server with the single account
information.

Third, the rules for the CLM Server monitoring need to be configured so
that, on an issue that requires looking at the java activity for an
instant in time, a java core is generated.

When a Javacore is generated on the CLM server being monitored, that
Javacore is uploaded to the WAIT server indicated in the Agent advanced
properties using the user id indicated in the Agent advanced properties,
at which point the WAIT server schedule to do the analysis. That will
result in a link being generated in the work item that will be a direct
external link to the WAIT server analysis of that Javacore on the WAIT
server.

The link may require the WAIT account user and password in order to
access the information.

The link generated for the WAIT report points to the location the WAIT
settings were configured for when the specific Javacore occurred.
Changing the WAIT properties will not move the Javacores to the new WAIT
server nor change the generated links in the existing Work items.

##### Related topics: [CLMServerMonitoringAgent](CLMServerMonitoringAgent) [related-topics-clmservermonitoringagent]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]

META:FILEATTACHMENT{name="image002.jpg" attachment="image002.jpg"
attr="h" comment="" date="1422297948" path="image002.jpg" size="29740"
user="geraldmi" version="1"} META:FILEATTACHMENT{name="image004.jpg"
attachment="image004.jpg" attr="h" comment="" date="1422297985"
path="image004.jpg" size="63728" user="geraldmi" version="1"}
META:FILEATTACHMENT{name="image006.jpg" attachment="image006.jpg"
attr="h" comment="" date="1422298139" path="image006.jpg" size="47027"
user="geraldmi" version="1"} META:FILEATTACHMENT{name="image008.jpg"
attachment="image008.jpg" attr="h" comment="" date="1422298160"
path="image008.jpg" size="29139" user="geraldmi" version="1"}
META:FILEATTACHMENT{name="image010.jpg" attachment="image010.jpg"
attr="h" comment="" date="1422298181" path="image010.jpg" size="26938"
user="geraldmi" version="1"} META:FILEATTACHMENT{name="image012.jpg"
attachment="image012.jpg" attr="h" comment="" date="1422298199"
path="image012.jpg" size="10034" user="geraldmi" version="1"}
META:FILEATTACHMENT{name="image014.jpg" attachment="image014.jpg"
attr="h" comment="" date="1422298219" path="image014.jpg" size="19056"
user="geraldmi" version="1"} META:FILEATTACHMENT{name="image016.jpg"
attachment="image016.jpg" attr="h" comment="" date="1422298243"
path="image016.jpg" size="19622" user="geraldmi" version="1"}
