META:TOPICINFO{author="tfeeney" date="1484176955" format="1.1"
reprev="1.2" version="1.2"}
META:TOPICPARENT{name="CLMUsageModelBestPractices"}

# BIRT Reporting Best Practices [birt-reporting-best-practices]

DKGRAY Authors: Main.RafikJaouani, Main.ErnestMah, Main.TimFeeney Build
basis: The Rational solution for Collaborative Lifecycle Management
(CLM) and the Rational solution for systems and software engineering
(SSE) v6.0.1. ENDCOLOR

TOC{title="Page contents"}

Where possible, replace BIRT reports with reports constructed in Report
Builder against data from the Data Warehouse or LQE. Ensure that you
extensively test all BIRT reports before deploying them into production;
tests should include a worst-case scenario that causes the most data to
be fetched.

Scope your reports to include only the data required by the report
consumers. Reports that include more results or attributes take longer
to process and render.

Narrow the result set as early as possible in the query processing.
Retrieving large amounts of data, then applying filters or joins, can
increase the run time and the memory demands. If you require reports
that return a large number of results, run them during off-hours or when
server usage is light.

Widgets with multiple pages of results place additional demand on the
server, while dashboard users are unlikely to click through all of those
results. The same applies to widgets based on BIRT reports or those
returning a large number of results. Ensure your dashboard widgets
provide a relatively small result set. For dashboards with high or
frequent use, avoid including widgets based on BIRT reports or those
returning a large number of results; alternatively, put them on low use
tabs.

Data aggregation reports (such as the BIRT RTC Timesheet and RQM Test
Execution reports) and some time series or trend reports can take longer
to run, depending on the amount of historical data in the data source.
Using larger time intervals increases the load on the server, although
repository size can also be a factor. Limit the time interval for trend
reports, and ensure you test the performance in a worst-case scenario.

See [BIRT Reporting Guidelines](ATTACHURL/BIRT_Reporting_Guideline.pdf)
developed by Matthias Buettgen.

##### Related topics: [Best Practices for CLM Usage Models](CLMUsageModelBestPractices) [related-topics-best-practices-for-clm-usage-models]

META:FILEATTACHMENT{name="BIRT_Reporting_Guideline.pdf"
attachment="BIRT_Reporting_Guideline.pdf" attr="" comment="BIRT
Reporting Guidelines" date="1484176746"
path="BIRT_Reporting_Guideline.pdf" size="281582" user="tfeeney"
version="1"}
