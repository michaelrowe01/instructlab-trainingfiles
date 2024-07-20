META:TOPICINFO{author="syeshin" date="1536872355" format="1.1"
reprev="1.2" version="1.2"} META:TOPICPARENT{name="RTC605Beans"}

# ProjectMetricsCollectorTask [projectmetricscollectortask]

Build basis: 6.0.5 ENDCOLOR

TOC{title="Managed Beans"}

# Project Area Information

Along with the common attributes, we have a Rational Team Concert
specific attribute for development lines of code in the SCM system. See
the Common [ProjectMetricsCollectorTask](ProjectMetricsCollectorTask)
for details on the common attributes.

### Advanced Property [advanced-property]

You enable this bean by setting **Enable Project Metrics MBean** to
**true**

### Object Name [object-name]

com.ibm.team.foundation.projectarea:name=\<\>, type=projectMetrics,
projectNameAndId=\*

### Default Frequency for Publishing [default-frequency-for-publishing]

1 Week

### Attributes [attributes]

TABLE{ sort="on" tableborder="1" cellpadding="3" cellspacing="3"
headerbg="#D5CCB1" headercolor="#666666" databg="#FAF0D4, \#F3DFA8"
headerrows="1" footerrows="1" }

| Attribute | Description | Type |
|:---|:---|:---|
| developmentLines | This is the total number of development time lines within this project area (RTC Only) | Integer |

##### Related topics: \* [Common Project Metrics Collector Task Beans](ProjectMetricsCollectorTask) [related-topics-common-project-metrics-collector-task-beans]

-   [Rational Team Concert 6.0.5 Managed Beans](RTC605Beans)
