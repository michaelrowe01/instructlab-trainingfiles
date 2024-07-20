META:TOPICINFO{author="dmmckinn" date="1437655882" format="1.1"
reprev="1.10" version="1.10"}
META:TOPICPARENT{name="DeploymentIntegratingReporting"}

# Report on custom attributes and enumerations DKGRAY Authors: Main.LuizSouza Build basis: IBM Rational Reporting for Development Intelligence (RRDI), IBM Rational Team Concert (RTC) [report-on-custom-attributes-and-enumerations-dkgray-authors-main.luizsouza-build-basis-ibm-rational-reporting-for-development-intelligence-rrdi-ibm-rational-team-concert-rtc]

ENDCOLOR

TOC{title="Page contents"}

This document provides a series of steps on how to report on RTC custom
attributes and enumerations on a customized RRDI/Insight report

## Background

Before proceeding with the instructions below, review the following
explanation of how custom attributes are set up:

In RRDI, when you open Report Studio, there are 2 main areas you have to
look for:

1.  **Requests** This holds the work items you want to use in your
    report
2.  **Request String Extension** This holds the custom attributes. The
    column **VALUE** contains the custom attribute value, or in the case
    of the custom attribute being an **ENUMERATION**, then the column
    **VALUE** contains the key of the table of enumeration, represented
    in Report Studio by **Request Enumeration**.

So basically, what you have to do is create a couple of query joins in
Report Studio to access your Custom Attributes.

**IMPORTANT**: You will find the package you are going to use in Report
Studio under **\> Operational Data Store \> Request Area \> Request
String Extension**.

## Step by Step process to report on Custom Attributes with Enumeration: 1. In the RTC interface where you define custom attributes, check the ID of the custom attribute you want. You are going to use this value later in the process. 1. While in this interface, check the type of this custom attribute. This type will tell you what table it is stored in RRDI. There are several kinds of tables with names such as **REQUEST_INT_EXT**, **REQUEST_STRING_EXT**, and others. These tables are represented in the package in Report Studio with names such as **Request String Extension**, and others. 1. In Report Studio, create three queries, one for **Request** (named Work_Item for this example), **Request String Extension** and another for **Request Enumeration**.

**Very Important:** Using the value of the ID of the custom attribute
from step \#1, create a filter in the **Request String Extension** query
associated with the **Name** column. In the example below \[Name\] =
'com.ibm.team.apt.attribute.complexity'

1\. Create a join with Work_Item and Request String Extension

Double click the Relationship node and set the relationship as
illustrated above. Under **Work_Item** select the **Request ID** column
name and again under **Request String Extension** you should also select
the **Request ID** column name. Then click **OK** and the join
relationship will be created. Do not forget to populate the query with
the columns from the two queries of the join.

1.  Now, create another join with the query above and the **Request
    Enumeration** query:

For this join, create the following relationship:

Under **Request_Req_String_Ext** select the **Value** column name and
under **Request Enumeration** select the **External ID** column name,
then click **OK** and the join relationship will be created. These
columns define the relationship of this join.

1.  Create your report Now, in Report Studio you might see something
    like this:

What you have to do now is to use the **REQ_ENUMERATION** query above in
your reports. Below is an example:

1.  The column **Literal Name** has the value of your custom attribute
    enumeration.

**Important:** Make sure the person running the report has the
appropriate access rights for the Project Area from which you want to
extract work items.

##### Related topics: [Deployment web home](WebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="three-queries.jpg"
attachment="three-queries.jpg" attr="h" comment="" date="1414596086"
path="three-queries.jpg" size="8847" user="dmmckinn" version="1"}
META:FILEATTACHMENT{name="request-string-extension.jpg"
attachment="request-string-extension.jpg" attr="h" comment=""
date="1414596364" path="request-string-extension.jpg" size="38617"
user="dmmckinn" version="1"}
META:FILEATTACHMENT{name="create-a-join.jpg"
attachment="create-a-join.jpg" attr="h" comment="" date="1414596525"
path="create-a-join.jpg" size="14227" user="dmmckinn" version="1"}
META:FILEATTACHMENT{name="join-relationships.jpg"
attachment="join-relationships.jpg" attr="h" comment=""
date="1414596722" path="join-relationships.jpg" size="36072"
user="dmmckinn" version="1"}
META:FILEATTACHMENT{name="populate-query.jpg"
attachment="populate-query.jpg" attr="h" comment="" date="1414597058"
path="populate-query.jpg" size="4941" user="dmmckinn" version="1"}
META:FILEATTACHMENT{name="join.jpg" attachment="join.jpg" attr="h"
comment="" date="1414597624" path="join.jpg" size="1889" user="dmmckinn"
version="1"} META:FILEATTACHMENT{name="create-relationship.jpg"
attachment="create-relationship.jpg" attr="h" comment=""
date="1414681815" path="create-relationship.jpg" size="54279"
user="dmmckinn" version="1"}
META:FILEATTACHMENT{name="create-another-join.jpg"
attachment="create-another-join.jpg" attr="h" comment=""
date="1414681838" path="create-another-join.jpg" size="14450"
user="dmmckinn" version="1"}
META:FILEATTACHMENT{name="example-table.jpg"
attachment="example-table.jpg" attr="h" comment="" date="1414682528"
path="example-table.jpg" size="41292" user="dmmckinn" version="1"}
META:FILEATTACHMENT{name="report-studio.jpg"
attachment="report-studio.jpg" attr="h" comment="" date="1414682556"
path="report-studio.jpg" size="35715" user="dmmckinn" version="1"}
META:FILEATTACHMENT{name="report-studio-package.jpg"
attachment="report-studio-package.jpg" attr="h" comment=""
date="1415906684" path="report-studio-package.jpg" size="46125"
user="dmmckinn" version="1"}
