META:TOPICINFO{author="michaelrowe" date="1700077068" format="1.1"
reprev="1.13" version="1.13"}
META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# You can't change the public URI of Jazz-based applications [you-cant-change-the-public-uri-of-jazz-based-applications]

DKGRAY Authors: Main.JimRuehlin Build basis: ELM ENDCOLOR

TOC{title="Page contents"}

**Update: You CAN change the public URI, but you must use the Server
Rename feature.**

A lot's happened in Engineering Lifecycle Management (ELM) since I wrote
this article. The ability to modify the public URI is one of them. There
are some things to be aware of when you're considering this. Please see
[this section of the Knowledge
Center](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.2/com.ibm.jazz.install.doc/topics/c_redeploy_server.html)
for instructions on the Server Rename feature.

**`========================================`**

So, heres the first thing you need to know when performing
administrative tasks on Jazz-based products:

You cannot change the public Uniform Resource Identifier (URI). You
cannot change the root context.

Many discussions long discussions have taken place with customers about
this, so it's important to emphasize this one thing:

Under no circumstances should you change the public URI. Under no
circumstances should you change the root context.

This instruction is designed to convince you that you cant change the
public URI or root context after it has been set during setup. Really.
You cant. Just stop thinking about it.

You can get around this constraint by using
\[<https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=topology-reverse-proxy-servers-in-topologies>\]\[reverse
proxies\]\] or [DNS
names](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.3?topic=topology-dns-names-in-topologies).
But this does not change the actual public URI or root context. DNS
names and reverse proxies just remap the URLs.

## You might be thinking: Why cant I change the public URI?

Architecturally, Jazz-based products use OSLC and RESTful interfaces.
This means that artifacts (data) is referenced with URLs. When a
dashboard shows information from a work item, its getting that work item
information by traversing a URL. When you get a list of dashboards to
choose from, each dashboard is referenced internally by a URL. When a
Engineering Workflow Management work item links to a Engineering Test
Management test case, it does so through a URL.

All those URLs are written into the database. Theyre not dynamically
calculated. The actual URL is placed into the database. Jazz-based
products construct these URLs by using the public URI and the root
context. So if your public URI is:

<https://my.server.com:9443>

and your root context is:

/ccm

then every URL that identifies information in the database starts with:

<https://my.server.com:9443/ccm>

**If you change the public URI or root context, you break all those
links.** And your heart will break too.

Now you might be thinking: Why not just search and replace the URLs in
the database when you change the public URI or root context? Ah, life is
not so simple.

The table structure in the database is optimized for reads. The result
is that item content is often stored as blobs (binary large objects),
not simple text. And some resource content is not directly interpretable
by the Jazz framework because the data is component specific. The URL in
these components might be stored as binary, .rdf, .xml, or another
format. So, identifying and replacing the links is not trivial.

That said, theres plenty of discussion going on among developers about
making public URIs more flexible. Stay tuned.

##### Related topics: [Deployment planning: Where to start?](DeploymentScenariosPlanning), [Planning your URIs](PlanningYourURIs), [Maintaining the public URL](MaintainingThePublicURL) [related-topics-deployment-planning-where-to-start-planning-your-uris-maintaining-the-public-url]

##### External links: \* [ELM Information Center](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management) [external-links-elm-information-center]

##### Additional contributors: Main.MichaelRowe [additional-contributors-main.michaelrowe]
