META:TOPICINFO{author="sbagot" date="1432746130" format="1.1"
version="1.12"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# How to validate integrity of Collaborative Lifecycle Management applications after performing an upgrade [how-to-validate-integrity-of-collaborative-lifecycle-management-applications-after-performing-an-upgrade]

DKGRAY Authors: Main.SudarshaWijenayake Build basis: CLM 4.x and later
ENDCOLOR

TOC{title="Page contents"}

Collaborative Lifecycle Management (CLM) applications such as Jazz Team
Server (JTS), Rational Team Concert (RTC), Rational Quality Manager
(RQM) and Rational Requirement Composer (RRC) may require to be upgraded
to a newer version not only to receive enhancements, but also to address
issues such as security vulnerabilities. Upgrade instructions for CLM
applications are provided via the [Interactive Upgrade
Guide](https://www.ibm.com/support/knowledgecenter/api/content/SSYMRC_4.0.7/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html).
This document on the other hand discusses test scenarios that one may
utilize to validate the integrity of CLM applications after performing
an upgrade. These test scenarios are listed below in ascending order
depending on their complexity and length.

## Test Scenario 1

1\. Navigate to the administrative console of the Jazz Team Server (JTS)
application at http://hostname:9443/jts/admin, open the Diagnostics page
by clicking the "Diagnostics" link in the left hand pane and run all
diagnostics by clicking the "Run All Diagnostics" link as shown below.

The diagnostics are capable of analyzing many aspects of the CLM
application to quickly identify problems. Ensure all diagnostics
complete successfully.

*If you perform this step after completing the upgrade of just the JTS,
then it is normal to see errors relating to inability to see the root
services of the registered applications yet to be upgraded.*

2\. Repeat step 1.1 by navigating to the administrative console of the
Rational Team Concert (RTC) application at
http://hostname:9443/ccm/admin

3\. Repeat step 1.1 one more time by navigating to the administrative
console of the Rational Quality Manager (RQM) application at
http://hostname:9443/qm/admin

4\. Navigate to the Lifecycle Project Administration application at
http://hostname:9443/admin/web and create a project by applying the
"Analyst, Developer, Quality Professional" template. You may refer to
the following document for information: [Creating lifecycle projects
from a
template](https://www.ibm.com/support/knowledgecenter/api/content/SSYMRC_4.0.7/com.ibm.jazz.platform.doc/topics/t_creating_aggregate_projects_from_template.html)

5\. Add the current user to each container of the newly created project.
You may refer to the following document for details: [Adding members to
lifecycle
projects](https://www.ibm.com/support/knowledgecenter/api/content/SSYMRC_4.0.7/com.ibm.jazz.platform.doc/topics/t_adding_members_to_projects.html)

6\. Assign project level roles to the current user. You may refer to the
following document for details: Assigning roles to members from within
lifecycle projects

7\. Navigate to the newly created project in the Rational Requirement
Composer (RRC) application at http://hostname:9443/rm/web. You may refer
to the following document for information: [Opening requirements
projects](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m2/topic/com.ibm.rational.rrm.help.doc/topics/t_open_proj.html)

7.1. Create a new requirement as stated in the following document:
[Creating requirement
artifacts](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.rrm.help.doc/topics/t_create_reqs.html)

7.2. Link a new work item in the Rational Team Concert (RTC) and a new
test case in the Rational Quality Manager application (RQM) to the
requirement as stated in the following document: [Linking to new
artifacts to work item in lifecycle
applications](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.rrm.help.doc/topics/t_calm_link_new.html)

7.3. Create a new collection and add the requirement created in step 1.8
to the newly created collection as stated in the following document:
[Creating
collections](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.rrm.help.doc/topics/t_create_collections.html)

7.4. Link an existing development plan in the RTC application and a new
test plan in the RQM application to the collection as stated in the
following document: [Linking collections and modules to development and
test
plans](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.rrm.help.doc/topics/t_calm_link_collection.html)

7.5. Navigate to the project dashboard as stated in the following
document: [RRC Project
Dashboard](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.rrm.help.doc/topics/r_project_dashboard.html)

7.6. Add new widgets to the dashboard and ensure both the existing and
newly added widgets are operational. Please refer to the following
document for information: [Working with widgets in Project
Dashboard](https://www.ibm.com/support/knowledgecenter/api/content/SSYMRC_4.0.7/com.ibm.jazz.dashboard.doc/topics/t_work_viewlets.html)

8\. Navigate to the project created in the Rational Team Concert (RTC)
application at http://hostname:9443/ccm/web.

8.1. Create a new work item in the RTC application as stated in the
following document: [Creating work
items](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.team.workitem.doc/topics/t_creating_work_items_web.html)

8.2. Link a new requirement in the RRC application and a new test case
in the RQM application to the newly created work item. Please refer to
the following documents for information: [Linking work items to
requirements](https://www.ibm.com/support/knowledgecenter/api/content/SSYMRC_4.0.7/com.ibm.team.workitem.doc/topics/t_linking_work_items_to_requirements_web.html)
and [Linking work items to test
cases](https://www.ibm.com/support/knowledgecenter/api/content/SSYMRC_4.0.7/com.ibm.team.workitem.doc/topics/t_linking_work_items_to_test_cases_web.html)

8.3. Create a new development plan as stated in the following document:
[Creating development
plans](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m2/topic/com.ibm.team.apt.doc/topics/t_creating_an_iteration_plan_web.html)

8.4. Link a new collection in the RRC application and a new test plan in
the RQM application to the development plan. Please refer to the
corresponding sections within the following document for details:
[Linking development
plans](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.team.apt.doc/topics/c_linking_plans_web.html)

8.5. Navigate to the project dashboard as stated in the following
document: [RTC project or team
dashboard](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.jazz.dashboard.doc/topics/t_create_dashboard_public.html)

8.6. Add new widgets to the dashboard and ensure both the existing and
newly added widgets are operational. Please refer to the following
document for information: [Working with widgets in project
dashboard](https://www.ibm.com/support/knowledgecenter/api/content/SSYMRC_4.0.7/com.ibm.jazz.dashboard.doc/topics/t_work_viewlets.html)

9\. Navigate to the project created in the Rational Quality Manager
(RQM) application at http://hostname:9443/qm/web. You may refer to the
following document for information: [Logging in to the Rational Quality
Manager
application](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m2/topic/com.ibm.rational.test.qm.doc/topics/t_startrqm.html)

9.1. Create a new test case as stated in the following document:
[Creating test
cases](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_create_testcase.html)

9.2. Link a new requirement in the RRC application and a new work item
in the RTC application to the test case. Please refer to the following
documents for information: [Associating test cases with
requirements](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_assoc_reqs_tcs.html)
and [Linking a test case to a development work
item](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_link_to_plan_item.html)

9.3. Create a new test plan as stated in the following document:
[Creating test
plans](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_create_testplan.html)

9.4. Add the test case created in step 1.9.1 to the newly created test
plan as stated in the following document: [Adding existing test cases to
a test
plan](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_add_existing_testcase_to_plan.html)

9.5. Link a new collection in the RRC application and an existing
development plan in the RTC application to the test plan. Please refer
to the following documents for information: [Linking test plan to
requirement
collections](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_link_reqcolls_tps.html)
and [Linking test plan to development
plans](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_link_to_devplan.html)

9.6. Create an execution record in the test case as stated in the
following document: [Creating test case execution
record](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_create_ewi_single.html)

9.7. Run the newly created test case execution record and link a new
defect in the RTC application to the execution result as stated in the
following document: [Running a test case execution
record](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_run_ter.html)

9.8. Navigate to the project dashboard as stated in the following
document: [RQM project
dashboard](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/m_additohomepage.html)

9.9. Add new widgets to the dashboard and ensure both the existing and
newly added widgets are operational. Please refer to the following
document for information: [Working with widgets in project
dashboard](https://www.ibm.com/support/knowledgecenter/api/content/SSYMRC_4.0.7/com.ibm.jazz.dashboard.doc/topics/t_work_viewlets.html)

10\. Navigate to the administrative console of the Jazz Team Server
(JTS) application at http://hostname:9443/jts/admin, run all data
collection jobs and ensure each data collection job in the JTS, RTC and
RQM applications complete successfully. Please refer to the following
document for details: [Running data collection
jobs](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.reporting.admin.doc/topics/t_running_the_data_collection_jobs.html)

11\. Revisit the project dashboards as in step 1.7.5, 1.8.5, and 1.9.8
and ensure all widgets are still operational.

## Test Scenario 2

Please refer to the following document for this test scenario: [Money
that matters
sample](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.help.common.jazz.calm.doc/topics/s_mtm_sample.html)

##### Related topics: None [related-topics-none]

##### External links: \* [Interactive Upgrade Guide](https://www.ibm.com/support/knowledgecenter/api/content/SSYMRC_4.0.7/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html) [external-links-interactive-upgrade-guide]

-   [Creating lifecycle projects from a
    template](https://www.ibm.com/support/knowledgecenter/api/content/SSYMRC_4.0.7/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html)
-   [Adding members to lifecycle
    projects](https://www.ibm.com/support/knowledgecenter/api/content/SSYMRC_4.0.7/com.ibm.jazz.platform.doc/topics/t_adding_members_to_projects.html)
-   [Assigning roles to members from within lifecycle
    projects](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.jazz.platform.doc/topics/t_assigning_roles_lpa.html?lang=en)
-   [Opening requirements
    projects](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m2/topic/com.ibm.rational.rrm.help.doc/topics/t_open_proj.html)
-   [Creating requirement
    artifacts](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.rrm.help.doc/topics/t_create_reqs.html)
-   [Linking to new artifacts to work item in lifecycle
    applications](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.rrm.help.doc/topics/t_calm_link_new.html)
-   [Creating
    collections](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.rrm.help.doc/topics/t_create_collections.html)
-   [Linking collections and modules to development and test
    plans](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.rrm.help.doc/topics/t_calm_link_collection.html)
-   [RRC Project
    Dashboard](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.rrm.help.doc/topics/r_project_dashboard.html)
-   [Working with widgets in Project
    Dashboard](https://www.ibm.com/support/knowledgecenter/api/content/SSYMRC_4.0.7/com.ibm.jazz.dashboard.doc/topics/t_work_viewlets.html)
-   [Creating work
    items](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.team.workitem.doc/topics/t_creating_work_items_web.html)
-   [Linking work items to
    requirements](https://www.ibm.com/support/knowledgecenter/api/content/SSYMRC_4.0.7/com.ibm.team.workitem.doc/topics/t_linking_work_items_to_requirements_web.html)
-   [Linking work items to test
    cases](https://www.ibm.com/support/knowledgecenter/api/content/SSYMRC_4.0.7/com.ibm.team.workitem.doc/topics/t_linking_work_items_to_test_cases_web.html)
-   [Creating development
    plans](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m2/topic/com.ibm.team.apt.doc/topics/t_creating_an_iteration_plan_web.html)
-   [Linking development plans with requirements
    collections](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.team.apt.doc/topics/c_linking_plans_web.html)
-   [Linking development plans with test
    plans](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.team.apt.doc/topics/c_linking_plans_web.html)
-   [RTC project or team
    dashboard](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.jazz.dashboard.doc/topics/t_create_dashboard_public.html)
-   [Logging in to the Rational Quality Manager
    application](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m2/topic/com.ibm.rational.test.qm.doc/topics/t_startrqm.html)
-   [Associating test cases with
    requirements](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_assoc_reqs_tcs.html)
-   [Linking a test case to a development work
    item](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_link_to_plan_item.html)
-   [Creating test
    plans](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_create_testplan.html)
-   [Adding existing test cases to a test
    plan](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_add_existing_testcase_to_plan.html)
-   [Linking test plan to requirement
    collections](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_link_reqcolls_tps.html)
-   [Linking test plan to development
    plans](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_link_to_devplan.html)
-   [Creating test case execution
    record](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_create_ewi_single.html)
-   [Running a test case execution
    record](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/t_run_ter.html)
-   [RQM project
    dashboard](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.test.qm.doc/topics/m_additohomepage.html)
-   [Running data collection
    jobs](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.rational.reporting.admin.doc/topics/t_running_the_data_collection_jobs.html)
-   [Money that matters
    sample](https://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.7/com.ibm.help.common.jazz.calm.doc/topics/s_mtm_sample.html)

##### Additional contributors: Main.PaulEllis [additional-contributors-main.paulellis]

META:FILEATTACHMENT{name="diagnostics.png" attachment="diagnostics.png"
attr="h" comment="" date="1366994389" path="diagnostics.png"
size="177575" user="swijenay" version="1"}
