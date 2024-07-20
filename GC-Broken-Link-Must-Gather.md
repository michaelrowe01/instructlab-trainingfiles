META:TOPICINFO{author="rnaranjo" date="1706110067" format="1.1"
version="1.13"}
META:TOPICPARENT{name="LifecycleQueryEngineBestPractices"}

# Must Gather to troubleshoot Broken Links in GC enabled Project Areas DKGRAY Authors: Main.NatarajanThirumeni [must-gather-to-troubleshoot-broken-links-in-gc-enabled-project-areas-dkgray-authors-main.natarajanthirumeni]

Build basis: ELM (formally known CLM - Collaborative Life-cycle
Management) 6.0.6 / 6.0.6.1 / 7.0 / 7.0.1 / 7.0.2 ENDCOLOR

TOC{title="Page contents"}

### Introduction

This document explains if a broken link issue is reported in Global
Configuration (GC) enabled project areas of IBM Engineering Test
Management (ETM) and IBM Engineering Requirements Management DOORS Next
(RDNG) then what kind of logs you would have to collect to debug this
issue. Please note, this document does not explain [where links are
stored](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.2?topic=overview-understand-linking-across-project-areas-in-configurations#c_links_in_cm__sec_aftr_enbl_config)
or details about [Link Indexing Service
(LDX)](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.2?topic=applications-links-across-project-areas-in-configurations#c_cm_linking_admin__section_reqrd_apps__title__1).
This is a high-level guide to explain what kind of logs should be
collected to investigate the broken link issues in GC context. Although
most of the logs could be collected as a Jazz User we would recommend
using a Jazz administrator role user.

## Example use case

Troubleshooting broken links in GC enabled project area is complex and
this document will explain what kind of logs are needed to debug a
broken configuration. The broken links could be classified in several
ways, lets us consider the following two use cases:

-   Creating a link from ETM Test Case (TC) to RDNG requirement is
    expected to establish a link between TC and requirement. In some
    cases, you'd see a link of TC in RDNG requirement but not in TC
    (Forward link missing) or vice-versa (Backlink missing).

<!-- -->

-   Populating artifacts from a GC baseline into a GC stream. In GC
    baseline link between Test case and RDNG requirement exist as
    expected, however, GC stream created out that baseline contains
    broken links.

## Pre-Requisite

Before collecting all the information below, please make sure that LDX
is up and running and that the relevant datasource is indexing
successfully.

Go to

<https://:/ldx/web/admin/data-sources>

and check the status is "Up-to-date"

## Log Collections : Steps

1\. Output of Configuration tree, copy outcome into a text file called
GC-ID.txt

<https://:/rm/gcsdk/tree?configurationUri=https://:/gc/configuration/>

GC-ID : is a URL to where configuration exist e.g

<https://:/gc/configuration/3>

2\. Local configuration URI of ETM. This can be obtained from the
Configuration Management (CM) enabled Project Area where Test Case
exist. From the Configuration context menu, hover over Local
Configuration name and copy link, e.g

<https://:/qm/oslc_config/resources/com.ibm.team.vvc.Configuration/_1QceYBSuEequ-JEash4SxA>

3\. GC versioned Test Case URL. From Test Case view, click on "Copy link
for this page" and then select Copy OSLC URL. e.g

<https://:/qm/oslc_qm/contexts/>\<\_0VIssRSuEequ-JEash4SxA\>/resources/com.ibm.rqm.planning.VersionedTestCase/\_Ggks8xSwEequ-JEash4SxA/\_4dfh2xSxEequ-JEash4SxA

-   \_Ggks8xSwEequ-JEash4SxA : VersionedTestCase Item ID
-   \_4dfh2xSxEequ-JEash4SxA : VersionedTestCase State ID

4\. Local configuration URI of RDNG. This can be obtained from the CM
enabled Project Area where RDNG Requirement exist, e.g

<https://:/rm/cm/stream/_xQvHkBSuEeqCl9XOGtTvzQ>

5\. RDNG requirement link that was added to TC. From requirement use
"more actions" icon and pick up "Share Link to Artifact" option and then
copy the link , e.g

<https://:/rm/resources/_-5ElgxSuEeqCl9XOGtTvzQ>

6\. ETM TC history PDF. From TC menu, go to History, click on Export
History to save TC history.

7\. TRS Feed. To download TRS, go to ETM trsConsole. Its important can
get the TRS feed as soon as the problem is reported, the feed contains
all the orders for the past 7 days.

<https://:/qm/trsConsole>

Click on download, this should download a ZIP of the TRS2 feed (RQM
Resources (TRS 2.0)) including all base page(s) and change log page(s)

8\. LDX SPARQL query output for Test Case version state in the
configuration. To run this query go to LDX query page and run,

prefix dcterms: prefix oslc_config: prefix rdf:

SELECT ?selected WHERE {
:/qm/oslc_config/resources/com.ibm.team.vvc.Configuration//selections\>

?selected FILTER regex(str(?selected), "") }

Note: : this is UUID of the local config, see step 2) :
VersionedTestCase Item ID, see step 3)

The query output normally should match the version of the TC you
collected in Step 3.

9\. In the same LDX query page, you'd need to run RDNG resource SPARQL
query against LDX, this query should be scoped to GC where the link
exists (eg gcStream1) in LDX. Its the query that RDNG uses to fetch the
links from LDX.

**`NOTE:  must be run without oslc.config context. The correct URL will be:/rm/resources/MB_90d3406c5b60a4ccda60279e63ceaf278>`**

**`NOTE: Starting with ELM v702 iFix026, the GC URL can be placed in the text field in the LDX query page`**

prefix dcterms: prefix oslc_config: prefix rdf: prefix owl: prefix
rtc_cm: SELECT DISTINCT ?sURL ?linkType ?tURL ?indLinkType WHERE { {
VALUES ?linkType {

} VALUES ?tURL {

} VALUES ?config {

} { ?sURL ?linkType ?tURL. BIND( ?linkType as ?indLinkType ) . } UNION {
?indLinkType owl:sameAs ?linkType . ?sURL ?indLinkType ?tURL . } }
OPTIONAL { ?reification rdf:subject ?sURL . ?reification rdf:predicate
?indLinkType . ?reification rdf:object ?tURL . ?reification
rtc_cm:deliverable ?release . ?reification rtc_cm:deliverable
?linkRelease . } OPTIONAL { ?config
rtc_cm:deliverable/rtc_cm:releasePredecessor\* ?configRelease . } FILTER
(BOUND(?reification) \|\| (BOUND(?linkRelease) && BOUND(?configRelease)
&& ?linkRelease = ?configRelease))} LIMIT 1000

-   RDNG resource URI - you'd need to substitute requirement URL (See
    step 5)

10\. We'd verify if selections page contain if the state ID of the
versioned test case, you can go to selection page

<https://:/qm/oslc_config/resources/com.ibm.team.vvc.Configuration//selections>
: is UUID of the local configuration (see step 2)

11\. From LDX get the status page of Skipped Resources for ETM Data
Source (links-qm data Source) if any skipped resources are present.

12\. From LDX get the status page of Invalid Updates for ETM Data Source
(links-qm data Source) if any invalid updates are present.

13\. Get ETM logs (qm.log) and LDX log (ldx.log)

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)
-   [Query Not Available In Configuration
    Picker](https://jazz.net/wiki/bin/view/Deployment/QueryNotAvailableInConfigurationPicker)

##### Additional contributors: Main.ZeeshanChoudhry, Main.TadeuszJanasiewicz, Main.RosaNaranjo [additional-contributors-main.zeeshanchoudhry-main.tadeuszjanasiewicz-main.rosanaranjo]
