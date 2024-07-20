META:TOPICINFO{author="sahilkmansuri" date="1702363346" format="1.1"
version="1.13"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Maintaining the public URL [maintaining-the-public-url]

DKGRAY Authors: Main.DavidChadwick, Main.DanToczala Build basis: The
Rational solution for Collaborative Lifecycle Management (CLM) and the
Rational solution for systems and software engineering ENDCOLOR

TOC{title="Page contents"}

One of the primary architectural principles of the Jazz architecture is
to maintain data or artifacts in only one place and link to it wherever
you need to access it. In this way you have fewer problems with copied
information being outdated or displayed in a less optimal way than the
application designed to display and interact with that type of
information. Viewers and editors are then provided by the primary
application and used wherever that data is displayed as a link. This is
known as the linked data concept. The links used to access these assets
are standard HTTP (Internet) URLs. There are a variety of development
wiki and blog entries that have been written about maintaining a stable
public URL for your Jazz repository data.

## Introduction

This explanation is meant to clear up some common questions and
misconceptions about the possibilities and issues surrounding the
movement of Jazz servers, issues surrounding URL stability, and how all
of this can impact your Rational Jazz CLM architecture. The basic issues
imposed by a RESTful architecture will have a definite impact on the
solution architecture that you put into place to host the Rational
solution for CLM. What you do will depend on your overall software
development tools strategy, as well as your user community.

Keep in mind in this discussion that while some things may be possible
from a technical standpoint, they are not good paths to go down due to
operational, organization scaling or performance concerns. So while it
may be technically possible to deploy the Rational solution for CLM with
a Derby database, the limitations of this approach make it an
intelligent thing to avoid for performance and scalability reasons. The
key here is to not just ask the technical questions ("Can I deploy with
Derby as my back-end database?"), but to instead ask intelligent
questions ("Can I support 1000 concurrent CLM users with a deployment on
a Derby database?"). The answer to the first question is "Yes", but
following this path will get you into trouble. Be sure to think in terms
of the solution for your end users, and not get too focused on the
technical questions with no context.

The rest of this article is posed as a series of frequently asked
questions, along with some answers and some explanation of the answer.
This article tries to focus on the intelligent questions, and provide
you with intelligent answers. You might note many links to the
[information center](InformationCenter), which is a very good source of
information.

## Basic concepts

Often an understanding of some of the basic concepts involved with a
Jazz solution make things much more clear.

**Why is the URL so important?**

The Jazz architecture is based on some basic concepts, like REST and
Internet addressable and discoverable resources. Search the web for
"REST explained", or see the
[platform](https://jazz.net/story/about/about-jazz-platform.jsp) entry
on Jazz.net. The Jazz RESTful architecture has the various artifacts
manipulated by the Jazz based tools. You can gain some basic
understanding by looking the information center topic about planning
your URIs.

In the Jazz environment, artifacts are considered resources, and these
resources are all accessible by using a URI (or web) reference. That is
how they are accessed. Relationships between artifacts are expressed as
hyper-links between these REST based artifacts. So think about this.
Changing the name of the base URI for your server would invalidate every
resource in your repository. It would also break any of the links to
your resources from other applications.

**Was the public URI required in the Jazz 2.x products?**

It was, but it was not enforced. There may be instances where a server
was configured without a public URI. It is important to set it, and
choose a common stable URL that users have been using to access the
server. You must configure a public URI prior to upgrade.

**Is a public URI required in the Jazz 3.x or later products?**

Yes. Better guidance has been added to the information center and in the
server setup user interface. Setup also performs more validation to
discourage configuring a potentially unstable URL; for example, IP
address, short name, localhost, etc. Unless you are setting up a
demonstration environment that you will not need the data from, do not
override these warnings, and make sure that you select a fully qualified
domain name as the basis for your public URI.

## Server moves and renames

Jazz customers often have questions about renaming and moving the
application servers supporting the Jazz tools.

**Can I move my Jazz/Rational Team Concert installation to another
server?**

The Jazz applications can be moved to different physical machines as
long as they keep the same public server root URI. A stable server URI
can be preserved by DNS or reverse proxy topology. Setting up a reverse
proxy server will allow you to retain the previous public server root
URI, while hosting the application on a server with a different name.
Remember to always use a fully qualified domain name for your public
server root URI.

**How can I change the public URI of my Jazz application server? Or my
Jazz Team Server?**

It is not currently supported to change the public URI in version 3.0 of
the CLM products; however, starting with version 4.0, there is a server
rename operation that can be performed which will change the public URI.
Support for server rename is initially limited to two scenarios in
version 4.0 and 4.0.0.x: moving a pilot deployment to production, and
copying a production deployment for the purpose of creating a staging
test environment. In version 4.0.1, support was added for renaming the
production environment and support for many of the integrations that are
not supported in version 4.0. (For details, see [Impact of Server Rename
and Integrated Products (Version
4.0.1)](https://jazz.net/library/article/1120). Even for the scenarios
supported in version 4.0, it is important that you understand the other
products that you integrate with:

-   If you are planning to move a pilot deployment to full production
    and your deployment includes unsupported integrations, do not
    perform a server rename. Your integrations will break.
-   If you are setting up a test staging environment, you must create
    "dummy mappings" in the mapping file for the URLs of any additional
    integrations in your deployment. This is to prevent contamination or
    linkages from the staging environment into production.

For customers that think that they may be good candidates for use of the
server rename functionality, it is best to review and understand the
[guidance article on Jazz.net](https://jazz.net/library/article/1081).

**Can I use repotools export and import to do a server move?**

This is not supported. Repotools export and import are for database
migration: for example, migrating from one database vendor to another,
or from one version or platform of a database to another, where native
backup and restore is not supported by the vendor. Generally the
off-line backup and restore facilities provided by an enterprise
database will be much faster than repotools export and import. There is
currently not any processing in repotools export or import that will fix
all of the URL references.

**I changed the public URI and it seemed to work. What's broken?**

There are numerous internal references within a Jazz repository. Some
examples of this are:

-   Links in opaque resources (dashboards, Rational Team Concert
    enterprise extensions)
-   Project area URLs
-   User URLs
-   Facts in the data-warehouse - The data-warehouse tables store hashed
    URLs as identifiers for resources
-   Fully qualified URLs in plans or work items

The development team is assessing the impact of a public URI change and
possible workarounds to some of the issues mentioned in this article.

**Can I change the public URI of a Rational Team Concert 2.x server?**

Officially this is not supported. However, the extent to which URLs are
stored in Rational Team Concert 2.x is not as pervasive as in Rational
Team Concert 3.x or in any of the linked CLM repositories, especially if
there are no cross-repository or C/ALM links. You can change the public
URL prior to upgrade, with some data loss:

-   Fully qualified URLs in work items will be broken
-   Work item links in emails will be broken
-   Artifact links across repositories (for example, to other Rational
    Team Concert servers or Rational Quality Manager or Rational
    Requirements Composer) will be broken
-   Facts in the data warehouse - In Rational Team Concert 2.x, this
    would only affect customers also using Rational Insight for
    reporting
-   Any integrations to other tools will be broken

**I saw the article on Jazz.net about [link
migration](http://jazz.net/library/article/558) - won't that fix
everything (<http://jazz.net/library/article/558>)?**

This was targeted to a specific use case where a Rational ClearQuest
server was moved, to allow fixing work item artifact links in the
Rational Team Concert repository. This is NOT a general purpose server
move solution, although it will likely be a part of any server move
solution that is made available in the future.

## Databases

Application servers are not the only servers supporting a Jazz solution.
People also often have questions about moving the database servers.

**Can I move my database from one database server to another?**

Yes you can. The database location is configured in the
teamserver.properties configuration file, and it is not persisted
anywhere else. Remember that you want to minimize latency between the
application server and the database server, and it not distribute it
over a WAN. The latency between the Jazz application servers and their
associated database repositories will have a direct impact on the
performance of the Rational solution for CLM, which is what you would
expect.

**Is there some set of SQL I can run in the database to fix
everything?**

The structure of the databases that support the Jazz applications is an
internal implementation detail. The table structure is optimized for
reads, and thus item contents are stored in blobs. Additionally, the
format of some resource content is opaque to the framework and component
specific (for example: binary, rdf, xml, etc). There is no trivial
solution mechanism to reliably process all the data in the database.

You can however take some steps to tune your database for better
performance. You can check the [general database configuring and tuning
section](https://jazz.net/wiki/bin/view/Deployment/ConfiguringAndTuningDBGeneral),
as well as the specific sections for
[DB2](https://jazz.net/wiki/bin/view/Deployment/ConfiguringAndTuningDB2)
and
[Oracle](https://jazz.net/wiki/bin/view/Deployment/ConfiguringAndTuningOracle).

## Testing and staging

Sometimes you just need a copy of the data that you already have, in
order to provide a testing or staging environment, or to provide a demo
environment. Here are some common questions on those topics.

**I need to replicate a repository to a testing and staging environment.
How can I do that if I can't change the public URI?**

if you are using version 3.x or earlier, you can set up an isolated
network where the hostnames are resolved to the test machine(s). Make
sure that your testing clients also resolve to the test machines. See
the [information center topic about creating a staging
environment](http://publib.boulder.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.install.doc/topics/c_upgrade_staging_env.html)
for more information.

If you are using version 4.0 or later, you can use the server rename
functionality. It is best to review and understand the [guidance article
on jazz.net](https://jazz.net/library/article/1081) before attempting to
use server rename for this purpose.

**I have a test database that I use to give demos. I thought I could use
export and import to put this on different machines or share it with
others. What can I do?**

Choose a test host name for your URL, e.g, rtcdemo.example.org. Anyone
executing the demo can add this entry to their local hosts file and
resolve it to the loopback address. This will allow you to run a demo on
a single machine, with all of the artifact links kept intact.

##### Related topics: [Server Rename](ServerRename) [related-topics-server-rename]

##### External links: [external-links]

-   [URL Guidance](https://jazz.net/wiki/bin/view/Main/URLGuidanceV2)
-   [You can't change the public URI of Jazz based
    applications](YouCantChangeThePublicURI)
-   [Planning your URIs](PlanningYourURIs)
-   [Public URLs are Casted in Stone How Do I Plan for the
    Future?](https://www.ibm.com/developerworks/community/blogs/dchadwick/entry/public_urls_are_casted_in_stone_how_do_i_plan_for_the_future4?lang=en)
-   [Renaming your Rational Solution for Collaborative Lifecycle
    Management server](https://jazz.net/library/article/1081).

##### Additional contributors: Main.JimRuehlin [additional-contributors-main.jimruehlin]
