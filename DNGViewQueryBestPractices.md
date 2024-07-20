META:TOPICINFO{author="rnaranjo" date="1560267567" format="1.1"
version="1.6"} META:TOPICPARENT{name="CLMUsageModelBestPractices"}

# DNG View Query Best Practices [dng-view-query-best-practices]

DKGRAY Authors: Main.HazelWoodcock, Main.TimFeeney, Main.VaughnRokosz
Build basis: The Rational solution for Collaborative Lifecycle
Management (CLM) and the Rational solution for systems and software
engineering (SSE) v6.0.1. ENDCOLOR

TOC{title="Page contents"}

# Overview

View Query search techniques ranked from the quickest to the slowest:

1.  Search on indexed data. This means searching within Modules, or
    Folders, searching on Tags, searching for specific Artifact types.
2.  Search on enumerated attributes. By looking at a value in an
    enumerated attribute the tool is doing a simple 'is this equal'
    operation.
3.  String searches. Searching for a string in an attribute (including
    title and description) takes much longer than an enumeration
    comparison. The full attribute content has to be searched for the
    string using something like a regular expression mechanism, this is
    resource hungry.
4.  Date searches. Searching for artifacts modified after a certain date
    takes time; in practice this is a slightly more complex version of
    the string search. Searching between dates requires first an 'after
    start date' search followed by a 'before end date' search on the
    results, so this is two date searches and therefore even slower.
5.  Link queries. Searching on whether artifacts have links of a certain
    type, and other link related queries take a long time because it
    requires the tool to go and investigate the other end of the link.
    For link types that can go external to DOORS Next Generation, such
    as 'Links To', 'References', 'Implemented By' etc, this can mean
    searching other repositories.

The tool automatically looks at the elements of the view query and finds
the most efficient order for running the query.

Ad hoc string search queries using the Quick Search box at the top of
the page are a quick way to find information.

Recommendations:

1.  For queries returning large quantities of data, Jazz Reporting
    Services is a better option than using views. The view will only
    show a few results per page, so there is limited value in a view
    that returns thousands of results. Insight offers better analysis
    tools for this type of query.
2.  The use of Modules and Folders to group artifacts, rather than
    collections, allows for more efficient searching within the scope of
    those groups.
3.  The use of tags on artifacts allows for efficient searching,
    although the tags have to be rigorously applied to ensure that
    artifacts are not missed out from a query.
4.  The use of the Quick Search box at the top of the page will give
    rapid results, although the search cannot be saved. Artifacts
    returned from a quick search can be tagged.

# Additional recommendations

## Use query filters that limit results

Maximize your use of query filters that place limits on the artifacts to
be returned. Queries which return smaller result sets will be faster.
Limits can also make queries more efficient by allowing them to rule out
entries and therefore make fewer checks.

Query filters which efficiently limit results include:

-   is any of
-   exists
-   is all of

The following query filters also place limits on the artifacts that are
returned, but these are slightly more expensive since the filtering
involves the execution of regular expressions:

-   starts with
-   ends with
-   contains
-   is
-   Date operations (is after, is before, between)

## Be cautious of the "not" filters

Use the following query filters with caution.

-   does not exist
-   not any of
-   does not contain
-   is unassigned

These filters may end up checking a large number of artifacts in order
to find things that don't match. It works best if you use these filters
with the filters that limit results, so that there are fewer candidates
to examine.

Where possible, use the positive checks instead of the negative checks.
Instead of using "not any of" and selecting just one item, use "any of"
and just leave out the one you don't want. That may not always be
possible, but when you can do it, the query will perform better.

Starting with 6.0.6.1 and 6.0.6 iFix008 or later, the Add Filter button
has been disabled for subconditions when the main condition is link type
does not exist. See [Modify the filter code to disable the "add filter"
button for subconditions when the main condition is link type does not
exist](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=125968)
and Maintenance Item [Slow query with "Not exists" on
links](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.viewWorkItem&id=126085)

## Other optimizations

-   Limit the number of columns added to your views. There is processing
    required for each column.
-   Organize your data into components and keep the number of artifacts
    in each component small.
-   There is a known problem when using "does not exist" with Link
    Types. Avoid combining "does not exist" for Link Type with "is not
    any of" for enumerated attributes.

##### Related topics: [Best Practices for CLM Usage Models](CLMUsageModelBestPractices) [related-topics-best-practices-for-clm-usage-models]
