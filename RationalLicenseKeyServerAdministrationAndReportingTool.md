META:TOPICINFO{author="rnaranjo" date="1464882083" format="1.1"
version="1.9"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Rational License Key Server Administration and Reporting Tool [rational-license-key-server-administration-and-reporting-tool]

DKGRAY Authors: Main.JaneBalin, Main.MichaelAfshar Build basis:
Collaborative Lifecycle Management 4.0.6 and later, Rational License Key
Server 8.1.4 and later ENDCOLOR

TOC{title="Page contents"}

The Rational License Key Server Administration and Reporting Tool
provides out-of-the-box license usage reports and capability to download
your license usage data into more customizable formats.

The Rational License Key Server Administration and Reporting Tool tracks
and reports license usage for IBM Rational products that are served by
the FLEXlm Rational Key License Server and the Collaborative Lifecycle
Management (CLM) License Server. The tool supports reporting on both
floating and token license models.

The tool does not track license usage for Atria licenses and node-locked
licenses. The 8.1.4 version of the tool, which was released in August
2013, does not report on CLM Authorized Users, and it does not
differentiate between the different CLM role-based licenses: Analyst,
Contributor, Developer, Quality Professional, and Stakeholder.

The 8.1.4 version of the tool provides these reports: Peak Usage, User
Based, Chargeback, and Token Distribution. Future plans include
developing the tools capacity to report against CLM Authorized Users,
extending the reporting capabilities of the tool to other IBM Rational
products that use Jazz Team Server, and eventually making CLM license
usage available by user role.

## Architecture of the Rational License Key Server Administration and Reporting Tool

The Rational License Key Server Administration and Reporting Tool is a
web-based application. The solution is based on a linked data model: the
[Resource Description
Framework](http://pic.dhe.ibm.com/infocenter/db2luw/v10r1/topic/com.ibm.swg.im.dbclient.rdf.doc/doc/c0059661.html).

Using a tracked resource set API as an active agent, the tool collects
usage data from the FLEXlm and Jazz Team Server logs. The agent converts
the log data into Resource Description Framework data, which is stored
in a Lifecycle Query Engine (LQE) database. The data is then available
to be queried by the tool by using SPARQL Protocol and RDF Query
Language (SPARQL). The tool uses [IBM Rapidly Adaptive Visualization
Engine (RAVE)](http://www-01.ibm.com/software/analytics/many-eyes/) to
render the data into out-of-the-box reports.

### High-level architecture of reporting

## CLM reports: Peak Usage, Token Distribution, User Based, and Chargeback

Peak Usage reports provide details on the maximum usage of product
licenses over a given period of time. The following parameters and
variables are defined for these reports:

-   **Frequency:** How often the data is sampled. Typically customers
    like to see daily peak usage reports.
-   **Duration:** The period of time over which the customer wants to
    see the usage data.
-   **Product:** The set of products on which the report is based.
-   **License types:** The various license types for which a report is
    needed (for example, floating or tokens). The report indicates the
    count of licenses, which is a sum of the selected types.
-   **License servers:** Users can select the license servers to report
    against. The report indicates the highest number of licenses used
    for each selected product from across the specified license servers.

### Peak Usage report

With Peak Usage reports, a license administrator can identify usage
patterns and thereby reduce license procurement costs. The following
examples show a Peak Usage report definition and a chart of the Peak
Usage report definition results.

#### Example: Peak Usage report definition

#### Example: Peak Usage report

### Token Distribution report

Token Distribution reports show the usage of tokens across products.
This report is based on the total number of tokens consumed across a
specified set of products for a selected period of time.

#### Example: Token Distribution report

### User Based report

User Based reports give information on the duration that product
licenses are used by a defined set of users. The **License Hours**
column data shown in the following example of a User Based report is
determined by multiplying the number of specific product licenses that a
user has checked out by the total amount of time the licenses were
checked out, and then dividing by 60. For example, if a user has checked
out two licenses for a specific product and has kept each license
checked out for a total of 90 minutes, the license hour calculation
would be the following: (2 x 90)/60 = 3.00 license hours. The
aggregation of the license usage data per product, per user is
advantageous because it results in less data to store in the LQE
database.

#### Example: User Based report

### Chargeback report

Chargeback reports associate license consumption with cost. A license
administrator can charge different departments in the organization for
the licenses that they consume. The Chargeback report enables
organizations to move to an environment in which licenses are consumed
and paid for on a pay-per-use basis.

The rate per product for Chargeback reports is defined in the **Costs**
section of the **Settings** tab in the Rational License Key Server
Administration and Reporting Tool. In the following example, the rates
per product are set to \$100.00 per license hour (see the previous
discussion of User Based reports for the definition of license hours).

The following chart shows an example of a Chargeback report based on the
rate settings noted in the above figure.

#### Example: Chargeback report

## Other capabilities

The Rational License Key Server Administration and Reporting Tool also
provides the capability to schedule reports and save the scheduled
reports. Future plans for the tool include the ability to email
scheduled reports.

The tool also includes a feature that enables the export of license
usage data from saved reports into commonly used formats such as PDF,
XML, JSON, CSV, and TSV. This capability enables administrators to
create custom reports and to provide license consumption data to other
reporting tools, including Microsoft Excel, for further customization.

Finally, the user-management side of the tool enables integration with
two types of user realms or databases that store user account details:
Apache Tomcat and LDAP. This functionality is employed for validating
user access and access privileges to the tool. By default, a predefined
set of users are created during the installation. The user IDs,
passwords, and access privileges are as follows:

| User ID | Password | Role description |
|:---|:---|:---|
| `rcladmin` | `rcladmin` | Administrator privileges are assigned to this user with access to all the features of the application. |
| `rclreportinguser` | `rclreportinguser` | User privileges are assigned to this user with access to the reporting feature of the application. |

## Downloading, installing, and system requirements

To download and install the tool, see the [Rational License Key Server
8.1.4 Download
Document](http://www-01.ibm.com/support/docview.wss?uid=swg24035648).
You do not need to download the Rational License Key Server 8.1.4 to
download and use the administration and reporting tool. As long as you
are at version 4.0.1 or later of the CLM server, you can download,
install, and configure the components that are associated with the tool
(which the download document specifies) and you can start reporting on
CLM license usage.

**Note:** Although not a requirement, if you are using tokens for your
CLM products, you might want to download and install the 8.1.4 version
of the Rational License Key Server, because it has the most up-to-date
defect fixes for serving CLM tokens. As long as your Rational License
Key Server for serving CLM tokens is at version 8.1.2 or later, you can
use the administration and reporting tool to report on token usage.

##### External links: [external-links]

-   [Rational Common Licensing Information
    Center](http://http://www.ibm.com/support/knowledgecenter/SSSTWP_8.1.4/com.ibm.rational.license.doc/helpindex_RCL.html)
-   [Rational Common Licensing Support
    Community](https://www.ibm.com/developerworks/community/groups/service/html/communityview?communityUuid=3073bdfa-c8f7-4af3-ae91-43f3fa0f0fa6)
-   [Releasenotesfor version
    8.1.4](http://www.ibm.com/support/knowledgecenter/SSSTWP_8.1.4/com.ibm.rational.license.doc/topics/readme_814.html)
-   [Best practices on deployment of IBM Rational License key
    server(RLKS) on Linux and Unix
    servers](http://www-01.ibm.com/support/docview.wss?uid=swg27046958&aid=1)

##### Youtube videos: [youtube-videos]

-   [GettingStartedwithRationalLicenseKeyServerAdministrationandReportingTool,v8.1.4](http://www.youtube.com/watch?v=EirNhQfdzSQ&feature=youtu.be)
-   [InstallingRationalLicenseKeyServerAdministrationandReportingToolv8.1.4](http://www.youtube.com/watch?v=E4CccvqsuEM&feature=youtu.be)

##### Additional contributors: Main.AmyLaird, Main.RosaNaranjo [additional-contributors-main.amylaird-main.rosanaranjo]

META:FILEATTACHMENT{name="peakUsage.jpg" attachment="peakUsage.jpg"
attr="h" comment="" date="1389643244" path="peakUsage.jpg" size="129933"
user="mafshar" version="1"} META:FILEATTACHMENT{name="peakReport.jpg"
attachment="peakReport.jpg" attr="h" comment="" date="1389643698"
path="peakReport.jpg" size="104071" user="mafshar" version="1"}
META:FILEATTACHMENT{name="userBasedreport.jpg"
attachment="userBasedreport.jpg" attr="h" comment="" date="1389644505"
path="userBasedreport.jpg" size="165746" user="mafshar" version="1"}
META:FILEATTACHMENT{name="globalSetting.jpg"
attachment="globalSetting.jpg" attr="h" comment="" date="1389647268"
path="globalSetting.jpg" size="134014" user="mafshar" version="1"}
META:FILEATTACHMENT{name="chargebackReport.jpg"
attachment="chargebackReport.jpg" attr="h" comment="" date="1389647511"
path="chargebackReport.jpg" size="186347" user="mafshar" version="1"}
META:FILEATTACHMENT{name="highLevelArchitectureOfReporting.jpg"
attachment="highLevelArchitectureOfReporting.jpg" attr="h" comment=""
date="1389657500" path="highLevelArchitectureOfReporting.jpg"
size="96922" user="mafshar" version="1"}
META:FILEATTACHMENT{name="TokenDistributionReportCLM.jpg"
attachment="TokenDistributionReportCLM.jpg" attr="h" comment=""
date="1390241109" path="TokenDistributionReportCLM.jpg" size="68567"
user="mafshar" version="1"}
