META:TOPICINFO{author="rnaranjo" date="1488767896" format="1.1"
version="1.10"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Query and Search indices management in the Rational solution for Collaborative Lifecycle Management Part 1: Query, Search and indexing technologies in CLM [query-and-search-indices-management-in-the-rational-solution-for-collaborative-lifecycle-management-part-1-query-search-and-indexing-technologies-in-clm]

DKGRAY Authors: Main.JorgeAlbertoDiaz Build basis: Rational solution for
Collaborative Lifecycle Management - Rational Team Concert, Rational
Quality Manager, Rational Requirements Composer, Rational Design Manager
4.0.1 and 5.0. Content and information valid for: CLM 4.0.x and CLM
5.0.x products ENDCOLOR

TOC{title="Page contents"}

The purpose of this series of articles is to provide a basic
understanding of the indexing processes in Jazz used by information
query and search features, the technologies involved and to provide
guidance on the associated administering tasks. We will also briefly
review some details on the base architectural details, and how
information is stored and queried in the different CLM applications.

## **Querying and Indexing in your CLM deployment**

This first part focuses on providing a general context to the
discussion, introducing some of the terminology and supporting
technologies that leverage artifacts query and text search capabilities
for the [Rational Collaborative Lifecycle Management
solution](https://jazz.net/products/clm/). We will briefly discuss how
the different Jazz CLM applications index and query information, and how
all this is realized in your CLM deployment.

You can take a typcial [Departmental
Topology](https://jazz.net/wiki/bin/view/Deployment/StandardTopologiesOverview#Departmental_topologies)
as reference CLM deployment for the remainder of the article. For the
discussion that will follow it is recommended to check this [Knowledge
Center
topic](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.4/com.ibm.help.common.jazz.calm.doc/topics/c_node_overview.html)
or the blog article called [Building products from
applications](https://jazz.net/blog/index.php/2010/08/16/building-products-from-applications/).

### **A quick review of the architecture**

Before discussing how query and search is implemented in CLM we will
introduce some details around the CLM products architecture. Different
implementations of the query and search services exist based on how the
base architecture solves it and what frameworks are used; so we are
going to briefly review the building blocks that make up the
applications to provide some context on the features implementation
details to come.

*Don't get puzzled by the details, the relationship between these
architectural pieces and the query and search capabilities
implementation in CLM will become clearer as you read through the
article.*

The **Jazz Team Server** application provides the services for the
integration of applications both of the CLM solution, other IBM
offerings and third-party applications; leveraging the collaboration of
all these tools and the seamless integration between them to work as a
single logical server. It provides common user administration,
authentication services, licensing management, dashboards and data
warehousing for the applications that are associated with it.

The Jazz Team Server is also found in the form of a library integrated
in the CLM applications, in this case it is known as **Jazz Application
Frameworks (JAF)**. The JAF SDK provides the underlying architectural
pieces for building applications and is embedded in the CLM applications
that are built using this architecture: the **Change and Configuration
Management (CCM)**, **Quality Manager (QM)** and **Design Manager (DM)**
applications embed JAF inside them. **NOTE: the Requirements Management
(RM) application uses JAF starting in 5.0**.

A subset of the services provided by the Jazz Team Server (a subset of
JAF), are known as **Jazz Foundation Services (JFS)**. For our
discussion, it is important to note that part of the JFS services are:
Storage APIs, Query APIs and Indexing APIs. JFS are used as a framework
by **Requirements Management**, **Design Manager** and **Lifecycle
Project Administration (LPA)** applications, and for the dashboards
implementation.

Starting as of CLM version 4.0, Jazz applications are built using the
JAF frameworks as described, however given the evolution of the products
and their implementation technologies, we have to also take into account
the following building technologies and SDKs in use:

-   **Rational Team Concert (RTC)** and **Rational Quality Manager
    (RQM)** are based on the Jazz 0.6 SDK (also known as Repository).
    This framework provides storage and query services. We will discuss
    them in the following topic. One of the defining characteristics of
    applications based on this architecture is that they have their own
    repository (e.g. database).

<!-- -->

-   **Requirements Management (RM)** in CLM 4.0.x versions is
    implemented as what is called a JTS "fronting application" which
    means that it relies on the Jazz Team Server to which is associated
    for services such as storage, query and search. This is important to
    keep in mind for indices storage considerations as we will review
    later. Starting in CLM version 5.0, RM uses JAF and has its own
    storage.

<!-- -->

-   **Rational Design Management (DM)** is built using JAF framework as
    previously described. It has its own repository and uses JFS for
    querying and indexing.

### **Query and Search capabilities implementation**

The different frameworks that we have reviewed provide different
solutions for the query and search capabilities. This can be categorized
in three groups:

1.  Item Query Service: this service implementation provides an
    abstraction layer on top of SQL to store and query structured data,
    based on the underlying database technology. It belongs to the Jazz
    0.6 SDK and it is therefore used by RTC and RQM.
2.  JFS query and search services: the applications that make use of JFS
    framework take advantage of these services. The underlying
    technologies used in the services implementation are:
    1.  Query Service. The information about stored artifacts is indexed
        in form of RDF metadata (RDF/XML, N-Triples or Turtle format),
        based on Jena.
    2.  Text search Service. Text information indexing and search is
        based on Lucene technology
3.  FullText search service: this is a custom implemented text search
    service based on Lucene technology. This custom service is used by
    RTC and RQM. This service implementation in RTC is open to any
    component but currently being used by work items and plans.

### **Item Query Services**

These services allow the creation and execution of Item queries
providing an abstraction of the low level details for querying the
repository for Items; where an Item is the representation of an object
stored in the repository, with proper ways of accessing its information
and states.

Working with repository items in the context of item queries are based
on the following main building blocks:

-   Queries are modeled assuring access to queryable element and
    attributes in the component model is type-safe.
-   The different queryable elements provides type safe methods for
    performing valid query operations.
-   Using the previous elements, the Item Query API allows for building
    the query, its predicates and running it with isolation of storage
    details.
-   The result of queries are cached in the server and paged. Paged
    items are retrieved to the client in a next-page-request basis.

The following diagram outlines the main steps and interactions of a
client using the Item Query service for retrieving data with simplified
view of the transformation taking place for retrieving the items data
from the repository:

Where:

1.  Once the item query is built, it is passed to the query service for
    running it
2.  The service perform some initial validation of query parameters and
    calls the supporting repository API. This will transform it into
    actual SQL to run the query.
3.  The results are passed back to the service as a list of objects (the
    Items), which are paged and cached
4.  The client requests the result pages

### **JFS: storage, query and search services**

The following diagram describes the high-level interaction of elements
from information storage and contents indexing, to information look up
as they are implemented by the JFS services:

The Indexing Service (steps 3 and 4 in previous diagram), is responsible
of building the different indices as an asynchronous process. The
service stores information on the indexes of last updated state and
polls repository periodically for changes to be indexed.

From previous diagram you can also identify the importance of the
indexing mechanism from final client perspective and how it will
interact (steps 5 and 6 in the previous diagram), to retrieve the
desired content and artifacts.

These indexing contents are realized in your environment within folders
like the following:

We will review in the next part of this article series how indexing
storage can be configured along with some administration tips.

### **FullText search service**

We have already seen that this custom service is implemented in RTC and
RQM. But how content is indexed in this feature?

-   **Rational Team Concert**: this index in RTC is built in a
    synchronous way: as part of a save operation the index is updated
    with the plan, work item content or attachments information.

This indexing behavior has an exception: when CLM is deployed in a
clustered configuration, the RTC text indexer performs asynchronously to
be able to participate in the nodes information sharing and keep
consistency.

-   **Rational Quality Manager**: the indexing in RQM is built the
    following way:
    -   Index is updated at every edit
    -   Every \~300 saves a reindex is kicked off

### **Recap: Search and indexing in your CLM deployment**

From a deployment perspective, taking the Departmental Topology as
reference including the DM application; the following diagram summarizes
which of the discussed technologies would exist in each CLM application
(the diagram removes the databases for simplicity):

From the previous diagram note that:

-   LPA and Dashboards, although omitted in this diagram, are
    applications on top of JTS.
-   Dashboards for ALL the applications are hosted and stored in the JTS
    (including CCM and QM ones).
-   Theming: CCM, QM and JTS has its own theming handler which uses JFS
    for indexing and querying themes. Fronting applications use the
    theming information from JTS.
-   JFS in CCM application: when RTCEE features are used, JFS is used
    for the RTCEE related information storage, indexing and searching.
-   RM, in 4.0.x and earlier, uses JTS for the storage, querying,
    searching and indexing services. So RM uses JFS technology but in
    the context of JTS. In 5.0.x, RM uses JAF.

This first part has introduced the architectural details and the
different technologies involved in storing and querying artifacts, and
the indexing processes that are part of these features.

##### Related topics: [related-topics]

-   [Jazz Indices Storage](DeploymentJazzIndicesStorage)
-   [Understanding indices in Jazz ](UnderstandingIndicesInJazz)

##### External links: [external-links]

-   [RSC 2009: SDP22 - The IBM Jazz Foundation and the IBM Jazz
    Integration Architecture](https://jazz.net/library/presentation/182)
-   [Indexing and
    Query](https://jazz.net/wiki/bin/view/Main/IndexingAndQuery)
-   [Jazz Foundation Indexing RDF for
    Query](https://jazz.net/wiki/bin/view/Main/JFSRdfIndexingRules)
-   [Lucene Tutorial: Lucene Text File
    Indexer](http://www.lucenetutorial.com/sample-apps/textfileindexer-java.html)
-   [CLM Build Architecture -
    Overview](https://jazz.net/wiki/bin/view/Main/CLMBuildArchitecture)
-   [Introduction to Jazz Application Frameworks
    SDK](https://jazz.net/wiki/bin/view/Main/JAFSdkIntroduction)
-   [The Jazz Application
    Frameworks](https://jazz.net/wiki/bin/view/Main/JAFIntroduction)
-   [Jazz Foundation
    Specifications](https://jazz.net/wiki/bin/view/Main/JazzFoundation#Jazz_Foundation_Specifications)

##### Additional contributors: Main.MartinAeschlimann, Main.PhilippeMulet, Main.JohnWhitfield, Main.SimonHelson, Main.JeromeLanneluc, Main.TimFeeney [additional-contributors-main.martinaeschlimann-main.philippemulet-main.johnwhitfield-main.simonhelson-main.jeromelanneluc-main.timfeeney]

META:FILEATTACHMENT{name="allDiagram.png" attachment="allDiagram.png"
attr="h" comment="" date="1406041419" path="allDiagram.png" size="26910"
user="tfeeney" version="2"} META:FILEATTACHMENT{name="appWar.png"
attachment="appWar.png" attr="h" comment="" date="1404413629"
path="appWar.png" size="4732" user="tfeeney" version="1"}
META:FILEATTACHMENT{name="itemQuery.png" attachment="itemQuery.png"
attr="h" comment="" date="1404413645" path="itemQuery.png" size="53825"
user="tfeeney" version="1"} META:FILEATTACHMENT{name="jfsIndexing.png"
attachment="jfsIndexing.png" attr="h" comment="" date="1404413663"
path="jfsIndexing.png" size="36195" user="tfeeney" version="1"}
META:FILEATTACHMENT{name="jfsIndexingFolders2.png"
attachment="jfsIndexingFolders2.png" attr="h" comment=""
date="1404415051" path="jfsIndexingFolders2.png" size="8943"
user="tfeeney" version="1"} META:FILEATTACHMENT{name="workitemIndex.png"
attachment="workitemIndex.png" attr="h" comment="" date="1404413694"
path="workitemIndex.png" size="20105" user="tfeeney" version="1"}
