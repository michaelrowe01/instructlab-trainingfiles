META:TOPICINFO{author="paulellis" date="1708427785" format="1.1"
version="1.16"} META:TOPICPARENT{name="DeploymentTroubleshooting"}

# Deployment Patterns and Anti-patterns when using Cloud Services DKGRAY Authors: Main.PaulEllis, Main.StevenBeard [deployment-patterns-and-anti-patterns-when-using-cloud-services-dkgray-authors-main.paulellis-main.stevenbeard]

Build basis: Engineering Lifecycle Management 7.0.x ENDCOLOR

TOC{title="Page contents"}

This article clarifies our Support policy and also documents issues that
we see when deploying the Engineering Lifecycle Management software on
Cloud Services such as: Microsoft Azure; Amazon Web Services; IBM Cloud;
Google; and others. This article will not cover any issues for those
hosted by ClearObject.

## Clarification of our existing support when deploying on Cloud Services

IBM is happy to support you deploying our IBM Engineering Lifecycle
Management (ELM) solution on Cloud Services such as IBM Cloud, AWS,
Google or Microsoft Azure under our existing Support Terms and
Conditions as long as it conforms to the [System Requirements for
ELM](https://jazz.net/wiki/bin/view/Deployment/ELMSystemRequirements702).

In the interest of clarity and effective operational management,
additional comments on the use of the database services such as AWS
Relational Data Service for Oracle service may be helpful:

1\. The database service must be running a version of Oracle or Db2
conforming to the ELM System Requirements for 7.02+ If your Cloud
provider stops providing a version of a database which is supported by
ELM, then it becomes your responsibility to install, support, and
migrate to a supported database version 2. If IBM recommends measures to
improve tuning, monitoring, or debugging of the database within the
Cloud Service, you are responsible to implement these measures, working
with your Cloud Service provider if necessary For further guidance and
best practice when deploying on Public Cloud Services, please see the
following page in the Deployment wiki: Deployment Patterns and
Anti-patterns when using Cloud Services

In addition, the [Server Virtualization Policy for IBM
Software](https://www.ibm.com/support/docview.wss?uid=ibm10719833)
states: "In response to the significant increase in Cloud and PureSystem
technologies now available to its clients, IBM has established a set of
virtualization environments for servers that we will support across our
multi-platform product portfolio for servers. These virtualization
environments consist of the operating system and hypervisor technology.
This information is intended to help clients plan their strategic
deployment environments for applications and achieve the economic
benefits available through server consolidation."

## Frequently Asked Questions

### Is CLM is supported when running in Hyper-V, which is used in the Azure environment?

Yes.

Note that if using Azure you will still need to bring perpetual licenses
and provide admin services. If you would rather move to SaaS and/or have
someone take care of the administrative services, you could move to and
IBM cloud offering. To learn more see the following:

<https://www.ibm.com/marketplace/cloud/application-lifecycle-management>
<https://www.ibm.com/marketplace/cloud/engineering-solutions-on-cloud/>"

### Is the full stack supported by IBM?

As stated above in the Support policy clarification, we don't support
stacks or any specific Public Cloud services, such as the AWS Oracle RDS
database or EC2 services. We only support the platforms and middleware
in the CLM/ELM System Requirements. If the Public Cloud Service uses
platforms/middleware that we support, a customer can use it to support a
CLM/ELM environment.

### If I create my containers vs. IBM provided containers?

We don't provide any supported Docker containers at present and we don't
support Docker as the platform to run CLM/ELM at present, so if a
customer built their own containers they would not be Supported. ii.

### What if in a public cloud vs. IBM-managed cloud?

Who's cloud and where the cloud is, is irrelevant as long as it supports
the platforms/middleware CLM/ELM supports.

## Windows restarts

If Windows patches are set to deploy automatically, you MUST shut down
the indices and CLM services, cleanly, before this is scheduled in case
of the Windows patch requiring a restart.

## [Amazon Web Services Relational Database Service - Oracle](https://aws.amazon.com/rds/oracle/)

### When creating Oracle tables using the commands that are prescribed in the Knowledge Center or Interactive Installation Guide, on Amazon RDS, you may encounter the following issue(s).

"The data warehouse tables could not be created. Try the action again.ID
CRJAZ1745E

CRRTC8030E The creation of the data warehouse failed.

com.ibm.team.repository.common.TeamRepositoryException: CREATE
TABLESPACE VNF_IDX LOGGING DATAFILE '/rdsdbbin/oracle/VNF_IDX_1.ora'
SIZE 200M AUTOEXTEND ON NEXT 50M MAXSIZE UNLIMITED EXTENT MANAGEMENT
LOCAL SEGMENT SPACE MANAGEMENT AUTO"

and

java.sql.SQLException: ORA-00604: error occurred at recursive SQL level
1 ORA-20900: RDS only supports Oracle Managed Files. Check ddl and
remove any named identifiers ORA-06512: at "RDSADMIN.RDSADMIN", line 160
ORA-06512: at line 2 at

**\*** What is AWS RDS telling you?

Tablespaces can be created this way: CREATE TABLESPACE JTS DATAFILE
'ORACLE_BASE/oradata/CLMDB/JTS.DBF' SIZE 1G AUTOEXTEND ON EXTENT
MANAGEMENT LOCAL AUTOALLOCATE;

What the DW is doing: CREATE TABLESPACE VNF_IDX LOGGING DATAFILE
c:\somepath\VNF_IDX.ora' ALTER TABLESPACE VNF_IDX ADD DATAFILE
c:\somepath\VNF_IDX.ora'

Change the SQL so that it just specifies the DATAFILE option itself. For
example, CREATE BIGFILE TABLESPACE VNF_IDX LOGGING DATAFILE SIZE 200M
AUTOEXTEND ON NEXT 50M MAXSIZE UNLIMITED EXTENT MANAGEMENT LOCAL SEGMENT
SPACE MANAGEMENT AUTO

Specifying the paths (emboldened) is the problem here. The DBA will need
to work within the Oracle command's syntax to create these tablespaces
manually and allow the Managed File System to allocate the datafiles.
Use the "noAdmin" option when generating the scripts as described in [
Create Oracle data warehouse without DBA
permissions](https://jazz.net/wiki/bin/view/Deployment/CreateOracleDataWarehouseWithoutDBAPermissions).

### Data Collection Component startup reports SQL Message: ORA-00942: table or view does not exist using Oracle server for Jazz Reporting Service

Attempts to start the Data Collection Component (DCC) are successful,
but the following message "SQL Message: ORA-00942: table or view does
not exist" is reported in the dcc.log after installing IBM Jazz
Reporting Service on Oracle.

This is documented in [Data Collection Component startup fails with SQL
Message: ORA-00942: table or view does not exist using Oracle server for
Jazz Reporting
Service](https://supportcontent.ibm.com/support/pages/data-collection-component-startup-fails-sql-message-ora-00942-table-or-view-does-not-exist-using-oracle-server-jazz-reporting-service).

The DCC service reports the following in the dcc.log

11/07/2018 19:17:26,254 \[Default Executor-thread-81\] INFO
sqlExceptionLogger - Syntax error or access rule violation SQL: DROP
TABLE DCC_DB_USER.REPOSITORY_GTT_STRING SQL Exception \#1 SQL Message:
ORA-00942: table or view does not exist SQL State: 42000 Error Code: 942

java.sql.SQLSyntaxErrorException: ORA-00942: table or view does not
exist

........ Caused by: Error : 942, Position : 23, Sql = DROP TABLE
DCC_DB_USER.REPOSITORY_GTT_STRING, OriginalSql = DROP TABLE
DCC_DB_USER.REPOSITORY_GTT_STRING, Error Msg = ORA-00942: table or view
does not exist at
oracle.jdbc.driver.T4CTTIoer11.processError(T4CTTIoer11.java:498) ...
199 more

The table name in the error above is DCC_DB_USER.REPOSITORY_GTT_STRING
but the DCC is is the user name; the table name is created based on the
user name and the Global Temporary Tables Type. The table name in your
log may, therefore, be different.

This is a known issue discussed in the following: 478063: [Silent
Upgrade
606iFix006-6061RC3](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/478063)
Error observed in DCC logs after upgrade 478089: [Internal API to drop a
table should not throw SQLException if the table does not
exist](https://jazz.net/jazz/resource/itemName/com.ibm.team.workitem.WorkItem/478089)

These issues were initially suspected to be related to the Amazon Web
Services RDS due to the [alternative technique required to create the
Data
Warehouse](https://jazz.net/wiki/bin/view/Deployment/CreateOracleDataWarehouseWithoutDBAPermissions).
This procedure has been confirmed to still be correct and these errors
are benign and can be ignored. They relate to temporary tables that are
being removed and in this instance, they do not exist anyway.

### Uploading models to Rhapsody Model Manager/Rhapsody Design Manager issues

When uploading a Rhapsody model with the "RTC-Client" to the Model
Manager.

1.  CRRTC5038W "The versioned content service temp directory has been
    deleted."

This error was fixed by changing the temp directory.

2\. CRJAZ0098E error, after fixing 1st error CRJAZ0098E following
service not running:
com.ibm.team.scm.common.IScmService{/am1/service/com.ibm.team.scm.common.IScmService}

The server returned the HTTP error 504 with the following error message:
Gateway time out.

See the Amazon Web Services help page for [Timeout issue is resolved
after changing timeout variables on AWS
server](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/ts-elb-error-message.html#ts-elb-errorcodes-http504).

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.ValerieLampkin, Main.MirkoHartwig, Main.GertWinderlich [additional-contributors-main.valerielampkin-main.mirkohartwig-main.gertwinderlich]
