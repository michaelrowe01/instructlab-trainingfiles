META:TOPICINFO{author="sbeard" date="1368574160" format="1.1"
version="1.15"} META:TOPICPARENT{name="PerformanceTroubleshooting"}

# Understanding Jena and SPARQL [understanding-jena-and-sparql]

DKGRAY Authors: Main.GeraldMitchell Build basis: Collaboration Lifecycle
Management (CLM) 4.0 Jazz Team Server(JTS) 4.0 Rational Team
Concert(RTC) 4.0 ENDCOLOR

TOC{title="Page contents"}

This is guidance to understand the RDF, Jena and SPARQL relationships
with CLM (Jazz).

## RDF, Jena, SPARQL, and CLM basics

#### Why do I care about RDF, Jena and SPARQL?

CLM is built around the concepts of Semantic Web - the web of things.
CLM adheres to the W3C (World Wide Web Consortium) and IETF (Internet
Engineering Task Force) recommendations and specifications for modeling
and exchange. RDF, Jena and SPARQL form the basis for the relationship
between the data model, application usage, and data manipulation. Simply
put, to model the data effectively RDF is used, Jena is used as the
framework for understanding RDF, and Jena's transport is SPARQL.

#### What is RDF?

RDF (Resource Description Framework) is the basic component of the
semantic web as defined through the W3C. Specifically it is the data
model for the representation of a thing, place, object, time frame, etc.
used to build out a useful repository. The idea is to enable machine
understanding of a resource by providing the meta necessary to describe
the thing by providing a usable data model. CLM is built around semantic
web and so uses RDF as a fundamental concept. The singular data model
allows a common language for exchange between applications.

References: [Wikipedia:
RDF](http://en.wikipedia.org/wiki/Resource_Description_Framework) [w3c
RDF primer](http://www.w3.org/TR/rdf-primer/) [RDF
spec](http://www.w3.org/TR/1999/REC-rdf-syntax-19990222/) [RDF
schema](http://www.w3.org/TR/2000/CR-rdf-schema-20000327/) [RDF XML
grammar](http://www.w3.org/TR/rdf-syntax-grammar/) [RFC
3870](http://tools.ietf.org/html/rfc3870)

##### What is a Triple/Triplestore?

The statement about an object in RDF is defined in a 3 word descriptor
(subject-predicate-object) called a triple. A triplestore is the storage
mechanism for a triple. The triplestores used for CLM 4.0 are over built
commercial relational database engines, which interact using SQL, by
using SPARQL as the intermediary.

#### What is Jena?

Jena is a framework for the semantic web written in Java. It is an open
source package obtained through Apache. CLM uses Jena API to interact
with RDF. References: [Wikipedia: Jena
Framework](http://en.wikipedia.org/wiki/Jena_28framework29) [Apache
Jena](http://jena.apache.org/)

#### What is Jena TDB?

Jazz Foundation Services use the Jena TDB database to store and query
over RDF data. TDB is a component of Jena implemented for fast RDF
storage. See the [Apache TDB
page](http://jena.apache.org/documentation/tdb/index.html) and for more
information. Specifics of the architecture can be found in the
\[\[<http://jena.apache.org/documentation/tdb/architecture.html>\]\[Jena
documentation on TDB\].

#### What is SPARQL?

SPARQL is actually used to store, retrieve, and manipulate triples over
SQL.

Beyond the syntax, the structure (nature) of the SPARQL query has a
direct impact on the resulting SQL query, which in turn finds and
returns the result in the relational database as efficiently as the
final request and the size and structure of the data tables allow.

References: [w3: SPARQL](http://www.w3.org/TR/rdf-sparql-query/)

***NOTE: There are changes and improvements to SPARQL and RDF that are
active proposals, see [SPARQL
1.1](http://www.w3.org/2009/sparql/wiki/Main_Page) for more
information.***

## Assessment of RDF, Jena and SPARQL in CLM

The best way to understand the nature of RDF, SPARQL, and Jena in CLM is
to look at a typical request for a work item, and see the flow from
request to retrieval, and also investigate a query to see the
similarities and differences.

#### Symptoms of a problem

#### Impact / Scope

#### Timing (When)

#### Environmental changes

### Using semantic web with CLM in DM

Here are some pointers to places where Sematic Web has visibility in DM:

-   The REST API [Article 1114](https://jazz.net/library/article/1114)
-   Domain Construction Toolkit <https://jazz.net/library/video/767>
    <https://jazz.net/library/video/768>
-   Model validation: <https://jazz.net/library/video/791>
    <https://jazz.net/library/video/792>
-   Query editor: <https://jazz.net/library/video/1085>

## Recommended analysis steps

#### Reviewing an RDF

Remember that RDF can represent many different things:

Here is a typical RDF file for RRC describing an Artifact.

12345

Mamba Number 3

IPyWED9U4oYSXbs3N9BSQkAiRNvckY42SmP1asx3udY=

\_c0YqUaUnEd-RB7K0TII4TA

"\_FNyfJb7VEeGro_Tz28rjsQ"

2012-06-25T14:50:18.514Z

hello world

2012-06-11T06:55:03.059Z application/rdf+xml Mamba Number 3

12345

This is a fairly simple graph (math term) of a simple artifact that I am
trying to envelope.

RDF is also used to denote the communications channels. Take for example
the jazz.net root services <https://jazz.net/jts/rootservices>

Rational Jazz Team Server

<https://jazz.net/jts> Jazz

#### Reviewing SPARQL in logs

The logging for SPARQL can be easily viewed through the application
server log files. Current logging for the SPARQL queries are shown when
the query takes a time over a particular threshold.

NOTE: some of the following examples are not actual issues, or are
issues from previous releases that have been resolved. These are used as
the basis of examples only, and the data has been changed to be entirely
fictional or implausible.

-   querying a lot of information in rdm.log

2013-02-29 22:21:20,191 \[ http-9443-Processor91\] \[74123569\] WARN
ng.server.services.query.internal.QueryServiceUtil Describe Query
(QueryServiceUtil) invoked with 512 urls by user:
<https://oldfakeserver.jazz.net:9443/jazz/users/ABCD0123> In this
example the query amount of 512 URLs by the user ABCD0123 is probably
excessive, and it may be a good idea to ask the user

-   what the user was doing, step by step
-   what were the results
-   is there another way of getting the correct results

<!-- -->

-   a review in rdm.log

2011-11-11 11:11:11,111 \[ http-9443-Processor82\] \[193452490\] ERROR
er.services.reviews.internal.ReviewServiceInternal Review service
invoked with no artifactURI by user:
<https://oldfakeserver.jazz.net:9443/jazz/users/CDEF1234> In this
example a review by the user ABCD0123 wasn't for a valid artifact id

-   what the user was doing, step by step
-   what were the results
-   is there another way of getting the correct results

<!-- -->

-   a query example in jazz.log of a very long query, no results. This
    resulted because of a long wait time not its own query.

2013-12-11 20:09:08,765 \[ http-9443-Processor16\] WARN sparqlLogger
query =\> DESCRIBE

unscoped, user belongs to =\> 0 context(s) execution time =\> 47.12 sec
(wait: 47.064 sec, sparql: 48 ms, match size: 0) In this example the
user would have seen a delay on the results, but wouldn't have any
returned results from the tags. Things to ask:

-   what the user was doing, step by step
-   what were the results
-   is there another way of getting the correct results
-   Examples of things to pay attention to in these logs
    -   Scoping: unscoped queries look through everything. Looking for
        more information than need will result in both more manual
        intervention in the results and a slower response with more
        information.
    -   Execution time: this is the time the query spent in the server.
        -   wait: the server was busy during or before query; this is
            the time where the query was not working
        -   sparql: the time spent on the sparql query
        -   match size is the amount of results returned to the query

## Possible Causes and Solutions

### The indices need to be re-indexed

Indices will be a direct correlation with the performance of the
application. Essentially, the index is a look-up table for the
information that can be more easily queried and result in faster
responses. The indices are explained
[here](https://jazz.net/wiki/bin/view/Deployment/UnderstandingIndicesInJazz).
You can re-index the individual indices or all at once and compact the
indices using the repotools commands.

##### Related topics: None [related-topics-none]

##### External links: \* None [external-links-none]

##### Additional contributors: None [additional-contributors-none]
