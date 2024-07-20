# API based automations 

Authors: Main.KrzysztofKazmierczyk, Main.PaulEllis 
Build basis: None 

With great power comes great responsibility. Using a supported IBM
Engineering Lifecycle Management (ELM) public API opens up many
possibilities to extend its functionality or allow new IBM Engineering
integrations. However, excessive usage of API can lead to unexpected
performance degradation, diminished user experience or frequent system
outages. There are three basic methods to cope with performance issues:

-   Rewrite your scripts,
-   Run them less frequently
-   Reduce their parallelism.

Below is the list of practices you should follow when using ELM public
APIs in custom automation:

## Put governance processes in place for custom script deployment

Deployment of custom scripts in a production deployment should be
reviewed and approved by a Change Control Board (CCB). If you do not
have CCB process in place, talk to your server administrators before
running automation against the server This allows your administrators to
be prepared and aware of potential performance impacts.

## Make your expectations reliable

Try to estimate the number of API calls or number of artifacts fetched
over time. If your estimates shows that the number of calls or artifact
fetches are too high, you should expect and plan for negative impact on
performance.

## Evaluate the functionality and performance impact on production equivalent test system first

The approach of your API requests depend strongly on result set and the
data shape of the requests and destination repository. For example, the
approach to fetch 1 attribute on 1 requirement, is very different to
fetching dozens of attributes across a project containing millions of
requirements. Therefore, before running on a production system, run it
first on a test system with production-sized data and resources.

## Start with small portion of data

If possible, try with small data set, and then extend it. For example,
you can limit your script only to one or few smaller project areas or
only for specific artifact types. If initial results are positive, and
you do not see a performance impact, extend the scope gradually.

## Consider increased load on other applications

Massive data modification from the scripts can also affect the Data
Collection Component (DCC), Lifecycle Query Engine (LQE) and Link Index
Provider (LDX) applications.

-   DCC component is used for gathering data for data warehouse reports.
    Your script can cause increased execution times of Data Collection
    jobs and storage used by your Data Warehouse database.
-   LQE and LDX applications store the data in their internal Jena
    index. Large updates of the applications increase the time needed
    for updating data sources related to an application. Reading the
    data (e.g. querying LQE for reports, fetching the backlinks from LDX
    in Engineering Workflow Management or DOORS Next applications) is
    much slower (in LQE/LDX with Jena store) when the index is being
    updated at the same time. See more recommendations on [Tips for
    administrators](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=builder-best-practices-creating-reports-report#c_best_practices_for_creating_reports_with_RB__best_prac3__title__1)
    page.
-   Since version 7.0.3 there is an option to [store LQE data in a
    relational
    database](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=overview-lqe-relational-store).
    Your script can impact performance of the database where the data is
    stored. More information available on [Whats new for IBM Engineering
    7.0.3
    administrators](https://jazz.net/blog/index.php/2023/12/06/whats-new-for-ibm-engineering-7-0-3-administrators/)
    page.

## Use monitoring

When using custom scripts extensively, monitor your system and take
action when your CPU, memory, disk usage or thread connection pool
grows, especially if diminished user experience is observed. If
necessary, stop the script and investigate if the script is the cause of
the performance issue. Address the issue before redeploying the script.
You can find more information about monitoring in [Deployment Wiki
article](DeploymentMonitoring).

## Close the connections in your client

After reading the response from a REST API call, remember to close the
response as this can lead to holding the connection to the server open
and exhaust the web server connection pool. While code inspection can
help find connections that are not closed, monitoring the "percentage of
the web container thread pool usage" while testing will identify the
growth of open connections followed by a sudden drop when the
application holding the connections ends. Other means of validating not
closing connections would be to have a very small connection pool
configured during testing and look for an error related to not being
able to establish a connection.

## Register your custom automation as a Resource-intensive Scenario

Link to the article: [Register Custom Automation As a Resource-intensive
Scenario](CreateCustomScenarios). Display the scenario in your monitor
dashboard to diagnose whether the script is the cause or contributing
factor of the performance degradation. As a best practice use a common
pattern for the naming of the scenario, as an example include the
automation name, version and other details e.g. the command name that
the automation executes. This makes it a lot easier to understand what
is going on. Example: use a scenario name like: myautomation v2.7
exportdata

## Consider running your scripts when the system has low usage

For example, run at night or during the weekend when usage is low and
there are no maintenance activities.

## Notice, that IBM is not able to provide you with specific limits of the system

Every environment is different. Therefore it is impossible to provide
specific limits, for example: What is maximum number of artifacts you
can fetch?, or What is the memory footprint for one artifact?, or How
many calls can you make concurrently?. You have to test your specific
data on your system.

##### Related topics: 
* [API Landing page](ELMProductAPILanding) [related-topics-api-landing-page]

##### Additional contributors: 
* Main.TimFeeney, 
* Main.DanielMoul, 
* Main.FarizSaracevic, 
* Main.RalphSchoon
