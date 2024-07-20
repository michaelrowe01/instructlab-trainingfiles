META:TOPICINFO{author="gcovell" date="1418086892" format="1.1"
reprev="1.2" version="1.2"}
META:TOPICPARENT{name="PerformanceDatasheetsAndSizingGuidelines"}

# Plan Loading Performance Improvements in RTC 5.0.2 DKGRAY Authors: Filip Wieladek, Kevin Garsjo Date: December 8, 2014 Build basis: RTC 5.0.2 [plan-loading-performance-improvements-in-rtc-5.0.2-dkgray-authors-filip-wieladek-kevin-garsjo-date-december-8-2014-build-basis-rtc-5.0.2]

ENDCOLOR

TOC{title="Page contents"}

In Rational Team Concert 5.0.2, plan loading performance has been
drastically improved for specific data sets, stemming from
investigations on specific planning REST calls. The investigation
allowed the team to identify wasteful server-side processing, and
replace the problem implementations with more performant ones. The REST
calls in question are responsible for resolving and returning references
to work item links, potential work item owners, categories and team
areas. Any plan view displaying a category, owner, or link attribute
will benefit from this work.

The team used the time taken to open specific plans as the testing
metric for performance. For our testing purposes, time taken is measured
as the elapsed time between refreshing a plan and the last plan loading
message ("Loading additional data...") to disappear. In all refresh
instances, the browser's local storage was cleared to prevent skewed
data due to caching.

## Testing Methodology

The plans tested contain views and data-sets specifically chosen to
exercise the investigated service calls. Each plan is given a size,
representing the relative size of its data set. The Small plan data-set
is defined as follows:

-   The plan's process area contains 50 contributors
-   The plan's process area contains 5 team areas, with defined
    categories for each
-   The plan contains 1 work item, which in turn tracks 50 out-of-scope
    items

The medium plan scales the small plan by 10. The large plan scales the
small plan by 100. Each plan uses a flat view, with no other options.
The following columns are the only ones displayed:

-   Summary
-   Owned By
-   Filed Against
-   Tracks

When collecting results, 5 plan refreshes were made for each plan size.
The highest and lowest outliers were discarded, and the remaining times
were averaged together to form the final measurement.

## Results

For the specific plans, testing between 5.0.1 and 5.0.2 saw improvements
ranging from 42 to 75.

The small plan saw 75 improvement, while the medium plan saw 67.

The large plan saw 42 improvement.

## Technical Details

Prior to the investigation, the getWorkItemAttributes() REST call
delegated to methods that collected handles for contributors that were
potential owners of work items in a plan. These handles were sorted
before return. The comparator for this sort resolved the handles
one-by-one to compare name values, a wasteful process that caused a
repository round-trip for each individual handle per comparison. Plans
with larger contributor sets suffered proportionally worse. The solution
was to resolve all handles in a batch prior to sorting, requiring only 1
round-trip to the repository. This problem was also present while
fetching team areas, and the solution was the same.

The getLinks() REST call also had handle issues, where handles were
being resolved twice. The solution was to encapsulate the handle in an
accessor method, which would resolve once and cache the result for
future access.

-------------------------------------

#### For more information [for-more-information]

-   [Performance Datasheets: CLM
    5.x](PerformanceDatasheetsAndSizingGuidelines#CLM_5_x)

#### About the authors [about-the-authors]

Filip Wieladek and Kevin Garsjo are members of the RTC Tracking and
Planning team. They led the 5.0.2 planning performance investigations,
fixes, and testing. Fil may be contacted at <filip_wieladek@ch.ibm.com>,
and Kevin may be contacted ad <krgarsjo@us.ibm.com>.
--------------------

##### Questions and comments: [questions-and-comments]

-   What other performance information would you like to see here?
-   Do you have performance scenarios to share?
-   Do you have scenarios that are not addressed in documentation?
-   Where are you having problems in performance?

COMMENT{type="below" target="PerformanceDatasheetReaderComments"
button="Submit"}

INCLUDE{"PerformanceDatasheetReaderComments"}

META:FILEATTACHMENT{name="largePlanLoadData_rc1.png"
attachment="largePlanLoadData_rc1.png" attr="h" comment=""
date="1413827202" path="largePlanLoadData_rc1.png" size="18090"
user="kgarsjo" version="1"}
META:FILEATTACHMENT{name="smallMediumPlanLoadData_rc1.png"
attachment="smallMediumPlanLoadData_rc1.png" attr="h" comment=""
date="1413827214" path="smallMediumPlanLoadData_rc1.png" size="22369"
user="kgarsjo" version="1"}
