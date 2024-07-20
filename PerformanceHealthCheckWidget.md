META:TOPICINFO{author="michaelrowe" date="1702414427" format="1.1"
version="1.12"} META:TOPICPARENT{name="BrowserPerformance"}

# Performance health check widget [performance-health-check-widget]

DKGRAY Authors: Main.GrantCovell, Main.RosaNaranjo Build basis: ELM/CLM
ENDCOLOR

TOC{title="Page contents"}

New to CLM 4.0, the **Performance Health Check** widget runs a number of
tests to measure the performance of various systems in a CLM deployment
including the client, application server and database server.

|  |
|----|
| Disclaimer: The **Performance Health Check** widget is provided for informational purposes only. Licensee should not rely on this feature for any purpose, and is encouraged to continue to rely on any existing tests of Licensee's system that may be in place |

## How to Use the Performance Health Check Widget

The Performance Health Check Widget is included out of box, but you will
need to add the widget to your dashboard.

1\. Open your personal Dashboard by either:

\* Selecting the drop down next to your user name in the top right hand
corner of the web UI, and select "Open My Personal Dashboard (default)"
\* Navigate to the following link: <https://:/jts/dashboards/> 2. Click
on *Add Widget*

3\. Filter for *Performance Health Check*

4\. Once the widget is found, click *Add Widget* to add the Performance
Health Check Widget to your Browser

5\. Navigate to your dashboard by closing out the 'Add Widget' section,
and select Run Test

## How to Analyze the Performance Health Check Widget

Once the widget has finished running the tests, the output would look
similar to the widget contained below:

The following tests are run: Round Trip Latency, Database Latency,
Download Speed, Upload Speed. For more information on each test and some
tips, see the [Performance Health Check
Blog](https://jazz.net/blog/index.php/2012/05/15/running-slow-get-a-health-check/).

##### Related topics: None [related-topics-none]

##### External links: \* None [external-links-none]

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="Widget.jpg" attachment="Widget.jpg" attr="h"
comment="Performance Health Check Widget new" date="1362000747"
path="Widget.jpg" size="27054" user="sbagot" version="1"}
META:FILEATTACHMENT{name="PHCWidgetTest.jpg"
attachment="PHCWidgetTest.jpg" attr="h" comment="Performance Health
Check Widget after test is run" date="1362001360"
path="PHCWidgetTest.jpg" size="44314" user="sbagot" version="1"}
