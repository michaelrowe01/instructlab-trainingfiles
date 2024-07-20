# Calculating your requirements metrics 

Authors: Main.PaulEllis, Main.BrianSteele, Main.ErikCraig, Main.BenjaminSilverman, Main.MartinHenderson 

Build basis: DOORS 9, Rational DOORS Next Generation 4, 5, 6. 


When discussing the planning of deployment topologies appropriate for
your requirements management system, it is important to understand your
existing system. Below details how you would calculate these numbers in
order to help you decide on how to deploy your servers. This topic is
tightly integrated with [planning for multiple requirements management
instances](https://jazz.net/wiki/bin/view/Deployment/PlanForMultipleJazzAppInstances#Multiple_Requirements_Management)
and the [sizing
strategies](https://jazz.net/wiki/bin/view/Deployment/CLMSizingStrategy60)
which are intended to be used to calculate the maximum sizes of each
instance. In November 2015, [a white
paper](http://www.ibm.com/developerworks/rational/library/rational-migrate-doors-data-to-doors-next-generation-trs/index.html?cm_mc_uid=36410414050514450077320&cm_mc_sid_50200000=1455104530)
was published on how to migrate data from Rational DOORS to Rational
DOORS Next Generation. This should be studied alongside this page,
indeed, this page is supplementary information on how to derive your
existing data shape when approaching a migration.

**Note:** The architecture of DOORS Next 7.x no longer uses the [Apache
Jena TDB](https://jena.apache.org/documentation/tdb/), so this article
is no longer relevant once you migrate to that release.

## Using Migration Metrics with Rational DOORS 9

As documented in [the developerWorks
article](http://www.ibm.com/developerworks/rational/library/rational-migrate-doors-data-to-doors-next-generation-trs/index.html?cm_mc_uid=36410414050514450077320&cm_mc_sid_50200000=1455104530),
the DOORS migration metrics utility is used to perform harmonization and
consolidation of types. Reports of attributes and enumerations are
examined and those that are similar or vary only by case of name must be
identified and classified as intentional or in need of harmonization.
Our needs at this point though are purely to derive the outlines of the
data shape in terms of numbers of requirements objects.

To achieve this, then simply download the DOORS 9.6.1.3 (or later)
client and install this on a machine which doesn't currently have a
DOORS 9 client. This restriction is due to DOORS 9 only supporting one
client per machine. If you only have access to one machine, then you can
uninstall your existing client and then reinstall after completing this
procedure.

There are further options available within the Migration Metrics with
later releases of DOORS 9, so it is advisable to download the latest to
avail of the latest possibilities. See [Gathering migration
metrics](http://www-01.ibm.com/support/knowledgecenter/SSYQBZ_9.6.1/com.ibm.doors.administering.doc/topics/t_get_module_metrics.html?lang=en-us)
for the latest and complete instructions if desired.

Use the Migration Metrics utility in IBM Rational DOORS to gather
information on whole projects or selected modules within a project. In
the DOORS 9.6.1.3 client select:

1.  Select a project in the database explorer. 2. Click **File \>
    Migration \> Migration Metrics.** 3. In the Migration Metrics
    window, select the project and scope, including the entire project
    or selected modules. 4. Click Go to create the migration metrics
    output

Note: The Migration Metrics utility is not for an entire DOORS database.
This allows analysis per project or per sub-partition which in turn
allows you to size the migration into Rational DOORS Next Generation
more easily. This page though is not intended to discuss the migration
process in detail, merely how you would count your requirements metrics.

## Using SPARQL queries to obtain your metrics from DOORS Next Generation

Firstly, before running these queries please note that some of these may
take some time to complete. Whilst they will not interfere too much with
your production service, it is recommended that you run these during
quieter periods where few users are likely to compete for query
resources. Where repositories are large, then these queries could take
10 minutes. Therefore warnings of queries exceeding 45-second limits may
be recorded in the rm.log.

To identify the number of artifacts within a specific project you can
run a SPARQL query. SPARQL queries can be executed on the RDNG built-in
administration panel `https://:/rm/rmadmin`, Under Debug \> SPARQL
Query. Alternatively, you can go immediately to
<https://:/rm/admin#action=com.ibm.rdm.fronting.server.web.debugQuery>

In the query window, set the custom SPARQL query scope to the project
and check pre-count. Run the following query

Under the results column, you would see `1/xxxxx` where `xxxxx` is the
number of resources in the project the query is being run against.

To determine the number of links replace `rm:Artifact` with `rm:Link` in
the above query.

### SPARQL query to count number of artifacts in your repository for indication on your position within the [performance datasheet guidance](https://jazz.net/wiki/bin/view/Deployment/PerformanceDatasheetsAndSizingGuidelines)

\* The most holistic query that you can use is one which will count all
the artifacts in your repo, based on what resides in your index. This is
specifically relevant from Requirements Management 6.0.6 where
[CleanupUnreferencedVersions](https://www.ibm.com/support/knowledgecenter/en/SSYMRC_6.0.6/com.ibm.jazz.install.doc/topics/r_repotools_repairincorrectunrefversions.html)
task has been re-enabled and will reduce the size of the index.

PREFIX dc: PREFIX rdf: PREFIX rdfs: PREFIX rm: PREFIX rmTypes: PREFIX
rrmReview: PREFIX nav: PREFIX jfs: PREFIX owl: SELECT DISTINCT ?context
( count(?artifact) as ?artifactCount ) ( count(?binding) as
?bindingCount ) ( count (?link) as ?linkCount ) WHERE { {?artifact
rdf:type rm:Artifact . OPTIONAL{?artifact rm:boundArtifact ?boundArt .}
FILTER (BOUND(?boundArt)) . ?artifact jfs:resourceContext ?context }
UNION {?binding rdf:type rm:Artifact . ?binding rm:boundArtifact
?boundArt . ?binding jfs:resourceContext ?context } UNION { ?link
rdf:type rm:Link . ?link jfs:resourceContext ?context } } GROUP BY
?context ORDER BY ASC (?context )

**For types, ordered rdf:type descending**, append the PREFIX statements
above to the following SPARQL SELECT statement:

Check 'pre-count' and run: \< br /\> SELECT ?type (count(?type) as ?foo
) WHERE { ?resource rdf:type ?type . } GROUP BY ?type ORDER BY
DESC(?foo)

**For a count for a specific Artifact Type**, substitute the following.
Ensure that "Artifact" is replaced with the name of your artifact type.
SELECT (COUNT(\*) AS ?no ) WHERE { ?resource rdf:type . ?resource ?p ?o
}

Alternatively, **select all by Artifact Type:**

SELECT ?type (COUNT(\*) AS ?no ) WHERE { ?resource rdf:type ?type .
?resource ?p ?o } GROUP BY ?type ORDER BY DESC(?no)

**Resources and Triples by Artifact Type:** SELECT ?type (COUNT(\*) AS
?no ) (COUNT(distinct ?resource ) AS ?graphs ) WHERE { ?resource
rdf:type ?type . ?resource ?p ?o } GROUP BY ?type ORDER BY DESC(?no)

**Full triple count:**

SELECT (COUNT(\*) AS ?no ) WHERE { ?s ?p ?o }

**Total number of artifacts:**

PREFIX rm: PREFIX rdf: PREFIX dc: PREFIX jfs: PREFIX rrmNav:

SELECT ( count (distinct \*) as ?count ) WHERE { ?Resource rdf:type
rm:Artifact . ?Resource rrmNav:parent ?Parent } LIMIT 1

**Artifact and link count by project:**

PREFIX dc: PREFIX rdf: PREFIX rdfs: PREFIX rm: PREFIX rmTypes: PREFIX
rrmReview: PREFIX nav: PREFIX jfs: PREFIX owl: SELECT DISTINCT ?context
( count(?artifact) as ?artifactCount ) ( count(?binding) as
?bindingCount ) ( count (?link) as ?linkCount ) WHERE { {?artifact
rdf:type rm:Artifact . OPTIONAL{?artifact rm:boundArtifact ?boundArt .}
FILTER (BOUND(?boundArt)) . ?artifact jfs:resourceContext ?context }
UNION {?binding rdf:type rm:Artifact . ?binding rm:boundArtifact
?boundArt . ?binding jfs:resourceContext ?context } UNION { ?link
rdf:type rm:Link . ?link jfs:resourceContext ?context } } GROUP BY
?context ORDER BY DESC (?artifactCount )

**Total number of artifacts, including module bindings:**

PREFIX rm: PREFIX rdf: PREFIX dc: PREFIX jfs: PREFIX rrmNav:

SELECT ( count (distinct \*) as ?count ) WHERE { ?Resource rdf:type
rm:Artifact } LIMIT 1

**Number of reviews:**

PREFIX rdf: PREFIX jfs: PREFIX dcterms: PREFIX rrm: PREFIX dc:

SELECT ( count (distinct \*) as ?count ) WHERE { ?uri rdf:type
rrm:Review . }

**List of formal reviews (useful for calculating additional baselines
for 5.x -\> 6.x upgrades):**

PREFIX rdf: PREFIX jfs: PREFIX dcterms: PREFIX rrm: PREFIX dc: SELECT
DISTINCT ?uri ?reviewState ?modified ?title ?lastModifiedBy ?dueDate
?creator ?resourceContext ?Formal WHERE { { ?uri rdf:type rrm:Review .
?uri dcterms:creator ?creator . ?uri jfs:resourceContext
?resourceContext . ?uri dcterms:modified ?modified . ?uri dcterms:title
?title . ?uri dcterms:contributor ?lastModifiedBy . ?uri dcterms:creator
?creator . ?uri rrm:reviewDueDate ?dueDate . ?uri jfs:resourceContext
?resourceContext . ?uri rrm:reviewStatus ?reviewState . ?uri rrm:formal
?Formal } FILTER regex(str(?Formal), "true") . }

**Number of module baselines:**

`PREFIX rdf: PREFIX jfs: PREFIX rm: PREFIX dc:`

```
SELECT ?url ?uniqueId ?title ?module WHERE { ?url rdf:type
rm:BaselineMetadata . ?url rm:module ?module . ?url rm:uniqueId
?uniqueId . ?url dc:title ?title }
```

**Number of stamped users on all reviews:**

`PREFIX rdf: PREFIX jfs: PREFIX rrm: SELECT ?uri WHERE { ?uri rdf:type
rrm:ParticipantResult . }`

**Number of reviews in the system**

`PREFIX rdf: PREFIX jfs: PREFIX dcterms: PREFIX rrm: PREFIX dc: SELECT
?uri WHERE { ?uri rdf:type rrm:Review . }`

##### Related topics: 
* [Deployment web home](DeploymentWebHome)

##### External links:

-   [IBM](https://www.ibm.com)

##### Additional contributors:
-   Main.MartinHenderson, 
-   Main.WilliamChatham