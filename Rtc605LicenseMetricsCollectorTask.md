META:TOPICINFO{author="syeshin" date="1536872582" format="1.1"
version="1.2"} META:TOPICPARENT{name="RTC605Beans"}

# Rational Team Concert Specific LicenseMetricsCollectorTask [rational-team-concert-specific-licensemetricscollectortask]

Build basis: 6.0.5 ENDCOLOR

TOC{title="Managed Beams"}

# Compatible Client Login Details Number of logins

This facet captures the number of login attempts from different versions
of the client. This MBean is only available in RTC.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Compatible Client Logins
MBean** to **true**

### Object Name [object-name]

com.ibm.team.foundation.counters:name=\<\>, type=counterMetrics, group=
Compatible client logins, facet=Number of logins, counterName=\*

### Default Frequency for Publishing [default-frequency-for-publishing]

15 minutes

### Attributes [attributes]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| creationTimeStamp | This is the time when the MBean was updated with a snapshot of the relevant data | Timestamp |
| host | This is the host name where the CLM application is running | String |
| port | This is the port number where the CLM application is accessible on the host. The value is -1 if the port is not set. | int |
| contextRoot | This is the application root context for the CLM application | String |
| nodeId | This is the application node id in case the CLM application is clustered | String |
| Domain | This is the namespace for the application under which the MBean data is published | String |
| name | This is the name of specific counter | String |
| group | This is the group that the counter belongs to | String |
| facet | This represents a particular aspect of this counter | String |
| id | This represents a unique id for this counter | String |

##### Related topics: [related-topics]

-   [Common LicenseMetricsCollectorTask
    Beans](LicenseMetricsCollectorTask)
-   [Rational Team Concert 6.0.5 Managed Beans](RTC605Beans)
