META:TOPICINFO{author="paulellis" date="1461768832" format="1.1"
reprev="1.17" version="1.17"}
META:TOPICPARENT{name="PerformanceDatasheetsAndSizingGuidelines"}

# Rational Requirements Composer Project Sizing Recommendations [rational-requirements-composer-project-sizing-recommendations]

DKGRAY Authors: Main.ShubjitNaik, Main.ErikCraig Build basis: Rational
Requirements Composer and Rational DOORS Next Generation 4.x Date: April
14, 2014 ENDCOLOR

TOC{title="Page contents"}

This article provides information about IBM Rational Requirements
Composer (RRC) 4.x project sizing in terms of number of artifacts in
projects.

Sizing guidelines for Rational DOORS Next Generation have appeared as
part of the [Performance Datasheets And Sizing
Guidelines](https://jazz.net/wiki/bin/view/Deployment/PerformanceDatasheetsAndSizingGuidelines)
since the 4.x release of Rational Requirements Composer. Also see [the
RDNG migration
guide](https://jazz.net/wiki/bin/view/Deployment/DOORSToDNGMigrationSizingGuide#Sizing_recommendations_for_Ratio)
for equivalent guidance for the 6.x release.

## Artifact numbers, Queries and Performance

Data being displayed in the RRC application is fetched using
[SPARQL](https://jazz.net/wiki/bin/view/Deployment/UnderstandingJenaAndSPARQL#What_is_SPARQL)
queries. These queries are requested by the RRC application and are
executed on the Jazz Team Server (JTS). RRC takes care of working with
the result set.

The scope of any query in RRC is a **project**. This optimizes time and
resource consumption. However, if all the data is placed in one project,
this scoping has very little effect. The resource consumption and
processing time of queries is directly proportional to the size of the
project it is being run against. The size depends on the number of
requirement artifacts like heading, text, images, tables, modules,
folders, etc.

Keeping this in mind, having the right partition of data into multiple
projects and folders in the repository is important to get optimal
performance out of Rational Requirements Composer.

## Project Size

A good size for a project, module, and folder would be:

**50,000 artifacts per project** BRArtifacts per project should not
exceed 50,000 and these include folders, modules, module artifacts and
collections. In case there are a high number of images, tables which in
turn increase size of artifacts, consider a lower artifact number per
project.

**4000 artifacts per module and folder** BRThis also helps to improve
readability. As a best practice start with creating a folder structure
in the project and avoid adding too many artifacts directly in the root
folder.

There are other artifact types that need consideration, number of links
within project and cross project that could increase as well (based on
the above project, module and folder size limits an average of 4
links-per-requirement is considered good).

### Identifying Project Size

You can periodically monitor the number of artifacts/resources in the
repository/project. The quickest way to identify that the number of
artifacts in the repository is based on the artifact ID of the most
recently created artifact. However, since the ID is unique across the
entire repository, it would not give you the right information if you
looking for number of artifacts within the project.

To identify the number of artifacts within a specific project you can
run a SPARQL query. SPARQL queries can be executed on the RRC built-in
administration panel `https://:/rm/rmadmin`, Under Debug \> SPARQL Query

In the query window, set the custom SPARQL query scope to the project
and check pre-count. Run the following query PREFIX dc: PREFIX rdf:
PREFIX rdfs: PREFIX rm: PREFIX rmTypes: PREFIX rrmReview: PREFIX nav:
PREFIX jfs: SELECT (count (distinct \*) as ?count) WHERE { ?resource
rdf:type rm:Artifact }LIMIT 1

Under the results column you would see `1/xxxxx` where `xxxxx` is the
number of resources in the project the query is being run against.
Following is a snapshot of the results BR

BRBRThis includes artifacts, artifacts in modules, modules, collections,
and folders. If the number is above 50,000, it would be a first
indication for you to start with a new project area.

To determine the number of links replace `rm:Artifact` with `rm:Link` in
the above query.

## Repository Limit

There is no theoretical limit on the number of artifacts that can be
created in projects/modules. The largest current tested limit is 315,000
artifacts in a repository. These artifacts were spread across 75
projects.

The test data used for these sizing tests represents an extremely large
repository compared to most customer environments. We chose this data
size to test the limits of the RRC application with unusually large data
volume. The data shape details are shown in the table below.

| Artifact type              |       Number |
|:---------------------------|-------------:|
| **Projects**               |           75 |
| **Modules**                |          600 |
| **Collections**            |          950 |
| **Folders**                |       38,400 |
| **Module artifacts**       |      127,500 |
| **Non-module artifacts**   |      187,200 |
| **Comments**               |      659,800 |
| **Links**                  |      467,700 |
| **Reviews**                |        5,400 |
| **Views (public/private)** |  7,500/7,500 |
| **Tags (public/private)**  | 22,500/3,750 |
| **Terms**                  |        9,900 |
| **Index size on disk**     |        51 GB |

For details on the results of the scalability and performance tests
conducted in an RRC-only deployment, with record of hardware/topology
used along with the data volume tested against, see the following Sizing
and Tuning Guides:

-   [Rational Requirement Management 4.0.1 Sizing and Tuning
    Guide](https://jazz.net/library/article/1267)
-   [Rational Requirement Management 5.0 Sizing and Tuning
    Guide](https://jazz.net/wiki/bin/view/Deployment/SizingAndTuningGuideForRationalDOORSNextGenerationVersion50)

Also see

-   [DOORS Next Generation 4.0.1 Performance
    report](https://jazz.net/library/article/1216) which was based on a
    data volume of 200,000 artifacts spread across 10 projects with 22
    modules in each project.
-   [DOORS Next Generation 5.0.1 Performance
    report](https://jazz.net/wiki/bin/view/Deployment/CollaborativeLifecycleManagementPerformanceReportRDNG501Release)
    based on similar data sizes

## Topology Selection

Consider the enterprise topology where the Jazz Team Server (JTS) and
the RRC application resides in their own JVM.

Look up the [Recommended Topologies](RecommendedCLMDeploymentTopologies)
described in the deployment wiki

##### Related topics: [RDNG Migration guide Sizing Guidelines](https://jazz.net/wiki/bin/view/Deployment/DOORSToDNGMigrationSizingGuide#Sizing_recommendations_for_Ratio), [Performance Datasheets And Sizing Guidelines](https://jazz.net/wiki/bin/view/Deployment/PerformanceDatasheetsAndSizingGuidelines) ---+++++! External links: [related-topics-rdng-migration-guide-sizing-guidelines-performance-datasheets-and-sizing-guidelines-----external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.BenSilverman, Main.PaulStrachan, Main.StefDijk [additional-contributors-main.bensilverman-main.paulstrachan-main.stefdijk]

--------------------

##### Questions and comments: [questions-and-comments]

-   What other performance information would you like to see here?
-   Do you have performance scenarios to share?
-   Do you have scenarios that are not addressed in documentation?
-   Where are you having problems in performance?

COMMENT{type="below" target="PerformanceDatasheetReaderComments"
button="Submit"}

INCLUDE{"PerformanceDatasheetReaderComments"}

META:FILEATTACHMENT{name="sparql-result.jpg"
attachment="sparql-result.jpg" attr="h" comment="SPARQL Result"
date="1397564719" path="sparql-result.jpg" size="34945" user="shubjit"
version="2"}
