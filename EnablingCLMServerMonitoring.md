META:TOPICINFO{author="tfeeney" date="1591111932" format="1.1"
version="1.9"} META:TOPICPARENT{name="CLMServerMonitoring"}

# Enabling CLM Server Monitoring RED(DEPRECATED: CLM Server Monitoring is no longer supported and was dropped in version 6.0.3.)ENDCOLOR [enabling-clm-server-monitoring-reddeprecated-clm-server-monitoring-is-no-longer-supported-and-was-dropped-in-version-6.0.3.endcolor]

DKGRAY Authors: Main.BorisKuschel Build basis: CLM 4.0.6+ ENDCOLOR

TOC{title="Page contents"}

By default, the CLM Server Monitoring feature is not enabled after
installation. To enable the feature, you use JConsole. If you have not
done so already, ensure that it is possible to connect with JConsole as
described in [Jazz monitoring through
JMX](https://jazz.net/wiki/bin/view/Deployment/JazzMonitoringThroughJMX).
Depending on what method was used to connect to JConsole, the
configuration is located in slightly different information.

For [WebSphere Application Server production
systems](https://jazz.net/wiki/bin/view/Deployment/JazzMonitoringThroughJMX#Using_JSR160RMI_Connector_for_JC),
the WebSphere Application Server configuration should be followed;
otherwise, follow the standard [JTS Server
Monitoring](https://jazz.net/wiki/bin/view/Deployment/JazzMonitoringThroughJMX#Setting_up_your_Jazz_Team_Server)
instructions.

## Enabling CLM Server Monitoring for WebSphere Application Server

When connecting with JConsole, one or more domains should be listed that
correspond to the applications that are installed on WebSphere
Application Server:

In all the domains you want to enable for monitoring, navigate to this
location:

team.server.\* \> Monitoring \> {WebSphere Application Server cell} \>
Configuration \> {WebSphere Application Server node} \> {WebSphere
Application Server name} \> Attributes

Ensure that the parameters are correct. Specifically, ensure that the
`CacheDiskStoreDirectory` contains enough space to accommodate both the
`CacheMaxBytesLocalDisk` and `ProblemCacheMaxBytesLocalDisk`. This
determines how much information is retained by the CLM Server Monitoring
before being evicted.

To collect all user activities, not just those that are problems (this
can be memory intensive), set `RegisterActivitywithSession` to `true`.

To turn on all monitors, set `AllMonitorsEnabled` to `true` and
`DiagnosticsEnabled` to `true`.

To enable monitors on a monitor-by-monitor basis, you must navigate to
each monitor. (`AllMonitorsEnabled` can be left `false` in this case.)
For each monitor, set `Enabled` to `true` to enable it. You can set the
`Threshold` (the default is 10s, an L is required after the number when
setting a new value, for example, `5000L` for 5 seconds), which
determines how long an execution should take before a problem is created
and whether aggregates should be collected. Set `RollupEnabled` to
`true`.

These attributes can be found in the monitors in these locations:

team.server.\* \> CORBA \> {WebSphere Application Server cell} \>
{WebSphere Application Server node} \> {WebSphere Application Server
name} \> Attributes team.server.\* \> Cache \> {WebSphere Application
Server cell} \> {WebSphere Application Server node} \> {WebSphere
Application Server name} \> Attributes team.server.\* \> DB Statement \>
{WebSphere Application Server cell} \> {WebSphere Application Server
node} \> {WebSphere Application Server name} \> Attributes
team.server.\* \> HTTP Client Request \> {WebSphere Application Server
cell} \> {WebSphere Application Server node} \> {WebSphere Application
Server name} \> Attributes team.server.\* \> Pool \> {WebSphere
Application Server cell} \> {WebSphere Application Server node} \>
{WebSphere Application Server name} \> Attributes team.server.\* \>
Request \> {WebSphere Application Server cell} \> {WebSphere Application
Server node} \> {WebSphere Application Server name} \> Attributes
team.server.\* \> SPARQL \> {WebSphere Application Server cell} \>
{WebSphere Application Server node} \> {WebSphere Application Server
name} \> Attributes team.server.\* \> Service \> {WebSphere Application
Server cell} \> {WebSphere Application Server node} \> {WebSphere
Application Server name} \> Attributes

## Enabling CLM Server Monitoring

When you connect with JConsole, one or more domains should be listed
that correspond to the applications installed on the application server.

In all the domains to enable for monitoring, navigate to this location:

team.server.\* \> Monitoring \> Configuration \> Attributes

Ensure that the parameters are correct. Specifically, ensure that the
`CacheDiskStoreDirectory` contains enough space to accommodate both the
`CacheMaxBytesLocalDisk` and `ProblemCacheMaxBytesLocalDisk`. This
determines how much information is retained by the CLM Server Monitoring
before being evicted.

To collect all user activities, not just those that are problems (this
can be memory intensive), set `RegisterActivitywithSession` to `true`.

To turn on all monitors, set `AllMonitorsEnabled` to `true` and
`DiagnosticsEnabled` to `true`.

To enable monitors on a monitor-by-monitor basis, you must navigate to
each monitor (`AllMonitorsEnabled` can be left `false` in this case).
For each monitor, set `Enabled` to `true` to enable. You can set the
`Threshold` (the default is 10s, an L is required after the number when
setting a new value, for example, `5000L` for 5 seconds), which
determines how long an execution should take before a problem is created
and whether aggregates should be collected. Set `RollupEnabled` to
`true`.

These attributes can be found in the monitors in these locations:

team.server.\* \> CORBA \> Attributes team.server.\* \> Cache \>
Attributes team.server.\* \> DB Statement \> Attributes team.server.\*
\> HTTP Client Request \> Attributes team.server.\* \> Pool \>
Attributes team.server.\* \> Request \> Attributes team.server.\* \>
SPARQL \> Attributes team.server.\* \> Service \> Attributes

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]

META:FILEATTACHMENT{name="Selection_408.png"
attachment="Selection_408.png" attr="h" comment="WebSphere MBean CLM
Server Configuration" date="1382890257" path="Selection_408.png"
size="11369" user="kuschel" version="1"}
META:FILEATTACHMENT{name="Selection_410.png"
attachment="Selection_410.png" attr="h" comment="MBean CLM Server
Configuration" date="1382890310" path="Selection_410.png" size="51366"
user="kuschel" version="1"} META:FILEATTACHMENT{name="Selection_407.png"
attachment="Selection_407.png" attr="h" comment="WebSphere MBean Monitor
Configuration" date="1382890354" path="Selection_407.png" size="2628"
user="kuschel" version="1"} META:FILEATTACHMENT{name="Selection_411.png"
attachment="Selection_411.png" attr="h" comment="MBean Monitor
Configuration" date="1382890394" path="Selection_411.png" size="8732"
user="kuschel" version="1"}
