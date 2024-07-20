META:TOPICINFO{author="indhare" date="1702872902" format="1.1"
reprev="1.10" version="1.10"}
META:TOPICPARENT{name="CLMUsageModelBestPractices"}

# Report Builder Best Practices [report-builder-best-practices]

DKGRAY Authors: Main.KathrynFryer, Main.ErnestMah, Main.TimFeeney Build
basis: IBM Engineering Lifecycle Management 6.x and later ENDCOLOR

### Starting with ELM 7.0.3, this topic is moved to the **[Best practices for creating reports with Report Builder](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=builder-best-practices-creating-reports-report)** [starting-with-elm-7.0.3-this-topic-is-moved-to-the-best-practices-for-creating-reports-with-report-builder]

TOC{title="Page contents"}

This page describes best practices for building reports in the
Engineering Lifecycle Management (ELM) solution with the Jazz Reporting
Service (JRS) and Report Builder. Some practices are more generic,
related to good report design. Others are more specific to the ELM and
Report Builder capabilities. Following good practices is important to
ensure your reports are usable and perform with appropriate use of
system resources.

### General good reporting practices

#### Make each report "fit for purpose" [make-each-report-fit-for-purpose]

Clearly define who will consume the report, and what they will use it
for. What decision or action do they need to take? What information is
required? Scope your report to include only the needed data, so
consumers can quickly digest the results. Avoid "general purpose"
results intended for use by different consumers with different needs;
those reports tend to include a superset of data, which can result both
in a slower-running report, and more difficulty for user to filter out
the data they don't need. If your report is very complex and includes
large amounts of data, consider whether you could decompose it into a
set of smaller, more targeted reports that could be grouped on a
dashboard or consumed independently for specific needs.

#### Manage by exception [manage-by-exception]

An extension to tailoring a report for its purpose, focus on the data
that's important for that purpose. Structure reports to highlight where
action is needed. For example, if you need to tackle outstanding
defects, do you really need data on all the closed defects? Reports that
return large quantities of data make it hard for consumers to quickly
scan and locate the important information, especially in tables that
cross multiple pages. Including more data than necessary can impact
report performance as well as the consumer's ability to consume the
information.

#### Consider all the reporting technologies at your disposal, and which is most appropriate for your needs [consider-all-the-reporting-technologies-at-your-disposal-and-which-is-most-appropriate-for-your-needs]

JRS and Report Builder help you create traceability and statistical
reporting. Report Builder generates interactive tables and graphs, and
supports options to export results (or the query itself) to different
formats.

Other tools such as IBM Engineering Lifecycle Optimization Publishing
(PUB) can generate formatted documents; for some reports, a document
might be easier to consume than an interactive online report. PUB also
provides capabilities different from Report Builder, including style
sheets to control format on the page, document comparison, and
scripting. For more details on PUB, including the web-based Document
Builder interface for users to generate documents, see
[Jazz.net](https://jazz.net/products/elo-publishing/).

#### Manage what you include on dashboards [manage-what-you-include-on-dashboards]

Minimize the number of reports and widgets on common "landing" dashboard
pages, or those with high or frequent use, so the system isn't
constantly running those reports as each user opens the dashboard. To
manage dashboard load time and load against your reporting server, put a
small number of widgets on each tab; to help users, you can group them
by consumer or purpose. Ideally dashboard reports return a relatively
small result set. Put reports with large result sets or long run times
on a separate tab, so they are run only as needed. You might even
exclude some reports from the dashboard catalog, so users run them only
via the Report Builder interface, or [schedule](#ScheduleReports) them.

#### Establish experts in your organization Report Builder allows users to write their own reports. It's important that all report creators understand the reporting best practices to ensure the reports they create consume appropriate amount of resources. If you can establish one or more experts within your organization, users can contact those experts for additional guidance or assistance in improving their reports. ---+++ Practices related to ELM capabilities [establish-experts-in-your-organization-report-builder-allows-users-to-write-their-own-reports.-its-important-that-all-report-creators-understand-the-reporting-best-practices-to-ensure-the-reports-they-create-consume-appropriate-amount-of-resources.-if-you-can-establish-one-or-more-experts-within-your-organization-users-can-contact-those-experts-for-additional-guidance-or-assistance-in-improving-their-reports.-----practices-related-to-elm-capabilities]

\#ScheduleReports

#### Consider scheduling and sharing reports [consider-scheduling-and-sharing-reports]

Both Report Builder and Document Builder provide the capability to
schedule reports and store the generated output. Schedule reports that
consume more resources (due to large result sets, complexity, and so on)
to run during times of lower system demands. One example is "the Monday
morning status report" that everyone on the team wants to see; schedule
it to run Sunday night so it is both ready and the team all see the same
results from the same point in time. Note: The Lifecycle Query Engine
(LQE) server does need some occasional quiet times where no queries are
running, so it can complete all write-to-disk operations.

#### Define your type system consistently (with URIs) to facilitate reuse [define-your-type-system-consistently-with-uris-to-facilitate-reuse]

You likely want some reports to be reusable, so you can run them for
different organizations with the same need (for example, different teams
can run the "Outstanding Defects" report for their set of artifacts). In
that case, those organizations need some consistency in the attributes
and attribute values they use, and also that you define the reports to
support reuse, instead of tailoring them to the values of a specific
team.

If you are using global configuration management, it is critical to
define URIs for artifact types, attributes, and attribute values, to
improve ease of building reports as well as reusing across teams. (See
also [Maintaining your DOORS Next type system in a
configuration-management-enabled
environment](https://jazz.net/library/article/92352).). If teams do have
variant type systems or specific needs, consider defining separate
reports. Balance between reuse and 'fit for purpose', team consistency
vs team variance.

### Building reports with Report Builder

#### Choose the right data source [choose-the-right-data-source]

The first step in Report Builder is selecting your data source;
depending what is deployed in your environment, the list might include
the Data Warehouse (DW), LQE, LQE scoped by a configuration, or one or
more configuration-based data sources. If you are using global
configuration management, you must use LQE scoped by a configuration (or
a configuration-based data source) to report on versioned artifacts; use
LQE to report on configurations and components themselves. For
unversioned artifacts (including work items, and all artifacts NOT using
global configuration management), the DW provides a richer set of
time-based metrics. For more information on which data source to choose,
see the [ELM Knowledge
Center](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.0/com.ibm.team.jp.jrs.doc/topics/c_jrs_choose_ds.html).

#### Start simple and add complexity Reports can get very complicated as you build conditions and relationships. A good rule of thumb is to start with a very simple version of the report you want, and ensure it runs correctly. Then gradually layer on relationships, conditions, calculations, custom expressions, and so on, verifying at each step that your results are as expected. (Note that the Report Builder preview shows only a sampling of data; you need to run the report to view actual results.) ---++++! Use filters to narrow scope of results [start-simple-and-add-complexity-reports-can-get-very-complicated-as-you-build-conditions-and-relationships.-a-good-rule-of-thumb-is-to-start-with-a-very-simple-version-of-the-report-you-want-and-ensure-it-runs-correctly.-then-gradually-layer-on-relationships-conditions-calculations-custom-expressions-and-so-on-verifying-at-each-step-that-your-results-are-as-expected.-note-that-the-report-builder-preview-shows-only-a-sampling-of-data-you-need-to-run-the-report-to-view-actual-results.-----use-filters-to-narrow-scope-of-results]

Use project scoping, specific artifact types, relationships, and
conditions to limit the amount of data returned. Retrieving large
amounts of data, then applying filters or joins, can increase the run
time and the memory demands.

-   Where appropriate, set project area scope
-   Use [traceability paths](#TraceabilityPaths) and
    [conditions](#SetConditions) to scope the artifacts returned.
    -   Use container-like relationships, for example, to scope
        requirements by a module, test results by a test plan, work
        items by an iteration.
    -   Constrain scope as early as possible in the traceability path,
        which limits the number of results to evaluate for the rest of
        the path. You can continue to add conditions for artifacts later
        in the path.

\#TraceabilityPaths

#### Keep traceability paths as simple as possible [keep-traceability-paths-as-simple-as-possible]

Large, complex traceability paths can increase the time and resources
required to run a report. In general, wherever possible:

Avoid optional relationships 
:   Optional relationships take much longer to evaluate, especially if
    they lead to other relationships and multiple paths to trace. The
    more optional relationships you include, the more paths there are to
    consider, and typically that causes the report to run longer or even
    time out. As an alternative, use two paths: one where the
    relationship doesn't exist, and one where it is required. You can
    then further extend the traceability for the case where the
    relationship is required. If you *must* have an optional
    relationship, put it at the end of the traceability path to reduce
    the number of paths to evaluate.

Minimize many-to-many relationships, and one-to-many relationships 
:   These take longer to evaluate, and you can sometimes run into issues
    with conditions applied at an early point in the path, which no
    longer apply later. For an example, see the [example on scoping
    relationship paths](#ScopingRelationshipPaths).

Append results instead of merging 
:   For multiple paths, appending results is faster than merging, which
    requires additional operations. That said, there are cases where you
    need to merge results. As described above, it is better to merge two
    paths than to use an optional relationship.

If your report requires complex traceability paths, keep it as simple as
possible while still achieving your goals. Test your reports for
performance. If you encounter problems, simplify your paths and add back
on. Consider whether there are alternative paths to access the same
data. Some reports might take longer to run, in which case you might
consider scheduling them to run during times of low server usage. See
[the ELM Knowledge
Center](https://www.ibm.com/support/knowledgecenter/en/SSYMRC_7.0.0/com.ibm.team.jp.jrs.doc/topics/t_trace_multiple_rel_paths_merging.html)
for more details on traceability paths. \#SetConditions

#### Set conditions to further limit the result set [set-conditions-to-further-limit-the-result-set]

Use conditions to further filter the set of data that is returned. You
can save the conditions as part of the report, or allow (or require)
users to change them at run time.

-   In traceability paths, apply conditions as early in the path as
    possible, to limit results to be evaluated later in the path.
-   Minimize exclusion conditions (where the value "is not" or "none
    of"), which take longer to process. Where possible, re-frame the
    condition to search for the values that you **do** want or that
    **do** exist.
-   Minimize combining conditions with OR. It takes longer to process an
    OR condition, because it has to be applied near the end of all
    processing. Report Builder can break down AND conditions to run more
    efficiently.
-   For time series or trend reports, limit the time interval to manage
    the size of result sets. Larger time intervals increase the load on
    the server.
-   For versioned artifacts (using global configuration management), to
    scope results to a specific component or set of components, set a
    condition for the artifact type based on its Component value. Note
    that the generic OSLC artifact type (for example, "Requirement")
    does not include a Component attribute.

#### Eliminate data columns you don't need to see [eliminate-data-columns-you-dont-need-to-see]

On the Formatting tab, remove data columns that you don't need in the
final report. For example, you might not need to see the project area
value, or if you have a condition to show a single specific status
value, you might not need to show the value in the report itself. If you
remove a column with condition data, the system still evaluates the
condition to run the report, but it doesn't need to return and render
that data.

#### To build a graph, get the table right first [to-build-a-graph-get-the-table-right-first]

Use the table view to ensure you have the right data and any necessary
calculations, before you switch to the graph design view. It is usually
easier to debug data issues from the table view.

#### Use meaningful labels [use-meaningful-labels]

For both tables and graphs, the default labels generated by Report
Builder might not be meaningful to report consumers. Where appropriate,
replace labels for data columns with more meaningful text. Provide
useful labels for graph axes and legends. For graphs, ensure colours are
easy to differentiate (and remember those who are colour-blind).

#### Understand your data model The Data Warehouse data model is reasonably well-documented in the Knowledge Centre; you can also use database tools to query the tables. LQE builds a dynamic schema based on the data it indexes from your organization. Understand how your organization defines artifact types, attributes, and relationships. Sometimes there is more than one approach to reporting on artifacts in a relationship. Examples of possible impacts: [understand-your-data-model-the-data-warehouse-data-model-is-reasonably-well-documented-in-the-knowledge-centre-you-can-also-use-database-tools-to-query-the-tables.-lqe-builds-a-dynamic-schema-based-on-the-data-it-indexes-from-your-organization.-understand-how-your-organization-defines-artifact-types-attributes-and-relationships.-sometimes-there-is-more-than-one-approach-to-reporting-on-artifacts-in-a-relationship.-examples-of-possible-impacts]

-   Base and module artifacts in DOORS Next Generation. Because base and
    module instances have unique URIs, you can get multiple results for
    a single artifact. Conversely, if you filter based on module, an
    artifact or its metadata might be included or excluded. Use a
    consistent strategy for modules, linking requirements, and
    reporting.

\#ScopingRelationshipPaths

-   Scoping in relationship paths. A scoping or filtering condition set
    on one artifact does not necessarily scope artifacts later in the
    traceability path. For example, you might query a QM Test Plan with
    all of its QM Test Cases, and all of the Test Case Results. However,
    the Test Case could have Results that are associated with multiple
    Test Plans; those would all be returned because the relationship is
    valid. Understand the relationships between the artifacts and where
    scope might change, and build your path accordingly. In this
    example, you would query the Test Plan and its Results (which are
    associated to only one Test Plan), and then the Test Cases (a Result
    has only one Test Case).

#### Remember you might need to refresh data [remember-you-might-need-to-refresh-data]

If you are building reports in a pre-production environment, you might
be creating data as you build your report. If you are using the Data
Warehouse, the data will only be available after the next data
collection job completes. If you are using LQE, you might need to
manually [refresh the
metamodel](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.0/com.ibm.team.jp.jrs.doc/topics/t_jrs_mng_ds.html?view=kc#t_metamodel)
to reflect changes to metadata.

#### If you need to modify the generated query, use custom expressions or make a copy [if-you-need-to-modify-the-generated-query-use-custom-expressions-or-make-a-copy]

In some cases, you might want to further manipulate the data returned by
Report Builder, for example to change the display format or perform more
complex calculations. Where possible, use Custom Expressions to include
custom SQL (for DW) or SPARQL (LQE) operations within the Report Builder
UI. If that is not sufficient, you can edit the generated query
directly; however, be aware that this means you can no longer use the
Report Builder UI to modify that report, filtering options for the
report will be constrained, and you won't be able to drill down within
the report results. If you must edit the generated query directly: 1 Do
as much as you can in Report Builder first. 1 Save your report, and make
a copy. 1 In the copy, edit the query in the Advanced section. 1 If you
are making extensive changes, ensure you narrow scope as soon as
possible in the query. 1 Ensure you test your query thoroughly, with
representative result size, and optimize for performance.

#### Test report performance [test-report-performance]

Especially for reports with large result sets or time series, complex
traceability or calculations, test the performance with a representative
sample size. You might find ways to optimize the report to improve
performance, or manage how the report is run (for example, scheduled and
not included on a dashboard).

### For administrators

#### Define a tagging and folder taxonomy [define-a-tagging-and-folder-taxonomy]

Both Report Builder and Document Builder use tags to group reports into
a folder-like structure; you can also search/filter based on tags.
Allowing all report creators to define their own tags can lead to
confusion (typos, near duplicates, and so on) and make it difficult to
locate reports. Define a taxonomy that makes sense for your organization
so users can easily locate the reports they need, and report creators
dont have to make up their own tags.

#### Ensure appropriate LQE server size [ensure-appropriate-lqe-server-size]

The LQE server operates as both data source and query executor, and
requires adequate resources to handle report demands as well as indexing
data updates. For details on sizing your LQE server, see [Best practices
for configuring LQE for performance and
scalability](LifecycleQueryEngineBestPractices).

#### Monitor LQE performance [monitor-lqe-performance]

Use the Health page in the LQE application administration and the other
ELM monitoring capabilities (including MBeans) to monitor the health and
performance of the LQE server. You can identify reports and queries that
are consuming system resources, and in some cases, stop them.
Capabilities vary depending on the ELM version you are using. For more
details on monitoring, see [Monitoring](DeploymentMonitoring),
[Monitoring Jazz applications using JMX
MBeans](https://jazz.net/blog/index.php/2018/05/25/monitoring-jazz-applications-using-jmx-mbeans/),
and [Monitoring LQE using
MBeans](https://jazz.net/library/article/90785). Administrators can also
limit query results and use other LQE properties to manage performance;
see [LQE
Properties](https://jazz.net/wiki/bin/view/Main/LQEAdvancedProperties)
for details.

#### Set property to optimize for large project areas (6.0.6 and later) [set-property-to-optimize-for-large-project-areas-6.0.6-and-later]

When reporting against very large project areas, Report Builder (LQE?)
can optimize the query differently to improve performance. To enable
this run-time optimization, edit the `conf/rs/app.properties` file and
set `large.project.query.optimization=true`. Save the file and restart
JRS to apply the change. You don't need to modify any reports. Note:
This property is supported as of 6.0.6 iFix15, 6.0.6.1 iFix9, 7.0, or
later. It is not available in earlier versions.

### Tips for reporting on configurations

#### Reports for multiple configurations on same dashboard [reports-for-multiple-configurations-on-same-dashboard]

Dashboard report widgets default to using your current configuration
context. However, you can change that default. To show the same report
for multiple configurations at once, you can add multiple instances of
the report widget, and set the filter of each one to a different
specific configuration context. Ensure that you also consider the
overall content of the dashboard tab. You can also use PUB to create a
template that iterates through multiple configuration contexts to
collect the specified data for each.

### Related topics

-   [Best Practices for CLM Usage Models](CLMUsageModelBestPractices)
-   [Reporting topic in the Knowledge
    Center](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.0/com.ibm.rational.reporting.overview.doc/topics/c_nav_cont.html)
-   [Jazz Reporting Service
    wiki](https://jazz.net/wiki/bin/view/Main/JazzReportingService)
-   [Trend and aging reports in JRS Report
    Builder](https://jazz.net/library/article/1562)
-   [Reporting on configurations and versioned artifacts
    (video)](https://www.youtube.com/watch?v=9eR6GF2Xlow&feature=youtu.be)
-   [Monitoring Jazz applications using JMX
    MBeans](https://jazz.net/blog/index.php/2018/05/25/monitoring-jazz-applications-using-jmx-mbeans/)
-   [Set up load balancing for multiple
    LQEs](SetupLoadBalancingForMultipleLQEs)
