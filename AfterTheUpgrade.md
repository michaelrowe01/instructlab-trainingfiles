# Common issues that occur after an upgrade

Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam) 
Build basis: CLM 4.x 

This page will discuss some troubleshooting steps to take when issues
are incurred after the upgrade.

## Known issues (application non-specific)

This section will discuss some known issues which occur after the
upgrade.

### Unable to create an LPA project

**Symptom:** When creating a new project, you may see errors such as the
following: Error instantiating the template: CRJCA0003E CRJCA0003E The
Lifecycle Project Administration (LPA) application made a request that
was answered by an unexpected response code. The request was:
<https://>.../ccm/clmSampleProject. The response was: HTTP/1.1 400 Bad
Request. **Cause:** Process templates need to be redeployed
**Resolution:** See [Redeploying Predefined
Templates](RedeployingPredefinedTemplates) for instructions on how to
redeploy the templates.

**Symptom:** Selecting 'save' button on LPA Creation page results in
nothing **Environment:** CLM in a distributed environment **Cause:** One
of the applications needs to be authorized **Resolution:** Navigate to
one of the other links under the admin context (members, projects). At
the top of the page, one of your applications should prompt for
authorization.

### Failing integrations

**Symptom:** After upgrading your CLM install, the previously configured
integrations (OSLC links, synchronization, connectors) are not
functioning as they did prior to the upgrade. **Cause:**

-   Versions are no longer supported
-   Configuration is incorrect
-   New connector version must be downloaded

**Resolution:** Before upgrading, ensure that the new versions of the
product are supported. Once the upgrade has occured, ensure that the
configuration is still accurate. For more information on troubleshooting
integrations, see the [Integrations
Troubleshooting](https://jazz.net/wiki/bin/view/Deployment/IntegrationsTroubleshooting)
section of the wiki.

### Failing Queries or Dashboard query issues

If you are unable to run a query, or see dashboards failing to load, you
may need to [Reindex the applications](ReindexingAfterUpgrade).

### Failing Reports or Dashboard reports issues

**Symptom:** After upgrading your CLM install, reports or dashboard
reports fail, or show incorrect information. **Environment:** Apache
Derby Database for Data Warehouse **Cause:** The Apache Derby Database
for Data Warehouse was not moved from the pre-upgrade directory into the
new directory. Therefore, the current Data Warehouse database is empty.
**Resolution:** Copy the Apache Derby Data Warehouse location in the
pre-upgrade directory (../server/conf/jts/derby/DataWarehouse) to the
new directory. Afterwards, complete the Data Warehouse upgrade again by
running [repotools-jts
-upgradeWarehouse](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.install.doc/topics/r_repotools_upgradewarehouse.html).

### Users unable to login

**Symptom:** After upgrading your CLM install, users are unable to login
to CLM. The following error may occur This user was not found in the
directory service. This user will not be able to login unless they have
an account in the directory service.ID CRJAZ1532I **Environment:** CLM
deployed on Apache Tomcat, using local file based authentication
(tomcat-users.xml) **Cause:** The file write behaviour for the
tomcat-users.xml file was changed between Tomcat 5.5 (RTC 3.x) and
Tomcat 7 (RTC 4.x) **Resolution:** See [Technote 1614661:
Tomcat-users.xml is file not updated after
Upgrade](http://www-01.ibm.com/support/docview.wss?uid=swg21614661)

**Symptom:** When accessing RRC (DOORS NG) when JTS has been upgraded to
5.x, users cannot access RRC/DOORS NG **Environment:** JTS at 5.0, RRC
at 4.x or 5.x **Cause:** RRC has changed to DOORS NG. **Resolution:**
You need to activate the DOORS NG licenses, or apply new licenses. These
licenses should already be assigned to your users, but the new CAL needs
to be applied.

### Unable to load or create work items

**Symptom:** After upgrade, work items cannot be viewed or created.
**Environment**: CLM versions 4.0.4 and below **Cause:** This is a known
defect in 4.0.4 **Resolution:** See [Creating or viewing a work item
results in a blank page and not an object error with RTC
4.0.4](http://www-01.ibm.com/support/docview.wss?uid=swg21652067)

## Known Issues (application specific)

Navigate to [Known
Issues](https://jazz.net/wiki/bin/view/Deployment/KnownIssues#Known_Workarounds)
and click on the application and version to see known issue and
workaround details (specific to application and version).

### RTC: Workspaces and Streams are disconnected

**Symptom:** After upgrade, workspaces and streams are disconnected. You
may see a NullPointerException. **Environment**: CLM versions 5.0,
Oracle backend database **Cause:** This is a known defect.
**Resolution:** See [NullPointerExceptions occur with Oracle DB after
migration to Rational Team Concert
5.0](http://www-01.ibm.com/support/docview.wss?uid=swg21676229)

## Where do I go from here? 
If you are unable to resolve your issue using the available online resources, please open a service request with IBM Rational Support. Refer to [Additional Troubleshooting Resources](DataCollectionandSupportResources) for further details.

## Recommended data gathering and subsequent analysis steps

When investigating problems that occur **after** the upgrade, collect
the following information: \* [ISALite Log
collection](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.team.concert.doc/topics/t_using_the_isal.html)
\* All upgrade repotools log files located in the following directory:
/server

-   screenshots or relevant errors

It will also be helpful to gather the following information:

-   What was the behaviour like before the upgrade?
-   Besides the upgrade, did any other configuration change occur?

##### Related topics: [related-topics]

  * For more troubleshooting topics, refer to [Upgrade
Troubleshooting](UpgradeTroubleshooting).

##### External links: [external-links]

-   None

##### Additional contributors: 
MainTwiki.StephanieBagot [additional-contributors-maintwiki.stephaniebagot]
