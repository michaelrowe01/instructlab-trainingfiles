Standards Track Work Product

# OSLC Core Version 3.0. Part 1: Overview

## OASIS Standard 26 August 2021

**This stage:**
[https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/oslc-core.html (Authoritative)](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/oslc-core.html)
[https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/oslc-core.pdf](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/oslc-core.pdf)

**Previous stage:**
[https://docs.oasis-open-projects.org/oslc-op/core/v3.0/ps02/oslc-core.html (Authoritative)](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/ps02/oslc-core.html)
[https://docs.oasis-open-projects.org/oslc-op/core/v3.0/ps02/oslc-core.pdf](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/ps02/oslc-core.pdf)
(published as Project Specification)

**Latest stage:**
[https://docs.oasis-open-projects.org/oslc-op/core/v3.0/oslc-core.html (Authoritative)](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/oslc-core.html)
[https://docs.oasis-open-projects.org/oslc-op/core/v3.0/oslc-core.pdf](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/oslc-core.pdf)

**Latest version:**
[https://open-services.net/spec/core/latest](https://open-services.net/spec/core/latest)

**Latest editor's draft:**
[https://open-services.net/spec/core/latest-draft](https://open-services.net/spec/core/latest-draft)

**Open Project:**
[OASIS Open Services for Lifecycle Collaboration (OSLC) OP](https://open-services.net/about/)

**Project Chairs:**
[Jim Amsden (jamsden@us.ibm.com), IBM](mailto:jamsden@us.ibm.com)
[Andrii Berezovskyi (andriib@kth.se), KTH](mailto:andriib@kth.se)

**Editors:**
[Jim Amsden (jamsden@us.ibm.com), IBM](mailto:jamsden@us.ibm.com)
[Andrii Berezovskyi (andriib@kth.se), KTH](mailto:andriib@kth.se)

**Additional components:**
This specification is one component of a Work Product that also includes:

_[OSLC Core Version 3.0. Part 1: Overview (this document). https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/oslc-core.html](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/oslc-core.html)_

_[OSLC Core Version 3.0. Part 2: Discovery. https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/discovery.html](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/discovery.html)_
_[OSLC Core Version 3.0. Part 3: Resource Preview. https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/resource-preview.html](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/resource-preview.html)_

_[OSLC Core Version 3.0. Part 4: Delegated Dialogs. https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/dialogs.html](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/dialogs.html)_
_[OSLC Core Version 3.0. Part 5: Attachments. https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/attachments.html](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/attachments.html)_
_[OSLC Core Version 3.0. Part 6: Resource Shape. https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/resource-shape.html](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/resource-shape.html)_
_[OSLC Core Version 3.0. Part 7: Vocabulary. https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/core-vocab.html](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/core-vocab.html)_
_[OSLC Core Version 3.0. Part 8: Constraints. https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/core-shapes.html](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/core-shapes.html)_


-----

Standards Track Work Product

_[OSLC Core Version 3.0. Machine Readable Vocabulary Terms. https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/core-](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/core-vocab.ttl)_
vocab.ttl
_[OSLC Core Version 3.0. Machine Readable Constraints. https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/core-shapes.ttl](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/core-shapes.ttl)_

**Related work:**
This specification is related to:

_[OSLC Core Version 3.0: Link Guidance. Work in progress. Current draft: https://oslc-op.github.io/oslc-specs/notes/link-guidance.html](https://oslc-op.github.io/oslc-specs/notes/link-guidance.html)_

**RDF Namespaces:**
[http://open-services.net/ns/core#](http://open-services.net/ns/core#)

**Abstract:**
Defines the overall approach to Open Services for Lifecycle Collaboration (OSLC) based specifications and capabilities that extend and
complement W3C Linked Data Platform [LDP]. OSLC Core 3.0 constitutes the approach outlined in this document and capabilities
referenced in other documents.

**Status:**
This document was last revised or approved by the membership of OASIS on the above date. The level of approval is also listed above.
Check the “Latest stage” location noted above for possible later revisions of this document. Any other numbered Versions and other
[technical work produced by the Open Project are listed at https://open-services.net/about/.](https://open-services.net/about/)

Comments on this work can be provided by opening issues in the project repository or by sending email to the project’s public comment list
[oslc-op@lists.oasis-open-projects.org.](mailto:oslc-op@lists.oasis-open-projects.org)

The English version of this specification is the only normative version. Non-normative translations may also be available. Note that any
[machine-readable content (Computer Language Definitions) declared Normative for this Work Product is provided in separate plain text](https://www.oasis-open.org/policies-guidelines/tc-process#wpComponentsCompLang)
files. In the event of a discrepancy between any such plain text file and display content in the Work Product's prose narrative document(s),
the content in the separate plain text file prevails.

**Citation format:**
When referencing this specification the following citation format should be used:

**[OSLC-Core-3.0-Part1]**
_OSLC Core Version 3.0. Part 1: Overview. Edited by Jim Amsden and Andrii Berezovskyi. 26 August 2021. OASIS Standard._

[https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/oslc-core.html. Latest stage: https://docs.oasis-open-projects.org/oslc-](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/oslc-core.html)
op/core/v3.0/oslc-core.html.


-----

Standards Track Work Product

## Notices

Copyright © OASIS Open 2021. All Rights Reserved.

All capitalized terms in the following text have the meanings assigned to them in the OASIS Intellectual Property Rights Policy (the "OASIS
[IPR Policy"). The full Policy may be found at the OASIS website.](https://www.oasis-open.org/policies-guidelines/ipr)

[This specification is published under the Attribution 4.0 International (CC BY 4.0). Portions of this specification are also provided under the](https://creativecommons.org/licenses/by/4.0/legalcode)
[Apache License 2.0.](https://www.apache.org/licenses/LICENSE-2.0)

[All contributions made to this project have been made under the OASIS Contributor License Agreement (CLA).](https://www.oasis-open.org/policies-guidelines/open-projects-process#individual-cla-exhibit)

For information on whether any patents have been disclosed that may be essential to implementing this specification, and any offers of
[patent licensing terms, please refer to the Open Projects IPR Statements page.](https://github.com/oasis-open-projects/administration/blob/master/IPR_STATEMENTS.md#open-services-for-lifecycle-collaboration-oslc-open-project)

This document and translations of it may be copied and furnished to others, and derivative works that comment on or otherwise explain it or
assist in its implementation may be prepared, copied, published, and distributed, in whole or in part, without restriction of any kind, provided
that the above copyright notice and this section are included on all such copies and derivative works. However, this document itself may not
be modified in any way, including by removing the copyright notice or references to OASIS, except as needed for the purpose of developing
any document or deliverable produced by an OASIS Open Project or OASIS Technical Committee (in which case the rules applicable to
copyrights, as set forth in the OASIS IPR Policy, must be followed) or as required to translate it into languages other than English.

The limited permissions granted above are perpetual and will not be revoked by OASIS or its successors or assigns.

This document and the information contained herein is provided on an "AS IS" basis and OASIS DISCLAIMS ALL WARRANTIES,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO ANY WARRANTY THAT THE USE OF THE INFORMATION HEREIN WILL
NOT INFRINGE ANY OWNERSHIP RIGHTS OR ANY IMPLIED WARRANTIES OF MERCHANTABILITY OR FITNESS FOR A
PARTICULAR PURPOSE.

OASIS requests that any OASIS Party or any other party that believes it has patent claims that would necessarily be infringed by
implementations of this OASIS Project Specification or OASIS Standard, to notify the OASIS TC Administrator and provide an indication of
its willingness to grant patent licenses to such patent claims in a manner consistent with the IPR Mode of the OASIS Technical Committee
that produced this specification.

OASIS invites any party to contact the OASIS TC Administrator if it is aware of a claim of ownership of any patent claims that would
necessarily be infringed by implementations of this specification by a patent holder that is not willing to provide a license to such patent
claims in a manner consistent with the IPR Mode of the OASIS Open Project that produced this specification. OASIS may include such
claims on its website, but disclaims any obligation to do so.

OASIS takes no position regarding the validity or scope of any intellectual property or other rights that might be claimed to pertain to the
implementation or use of the technology described in this document or the extent to which any license under such rights might or might not
be available; neither does it represent that it has made any effort to identify any such rights. Information on OASIS' procedures with respect
to rights in any document or deliverable produced by an OASIS Technical Committee can be found on the OASIS website. Copies of claims
of rights made available for publication and any assurances of licenses to be made available, or the result of an attempt made to obtain a
general license or permission for the use of such proprietary rights by implementers or users of this OASIS Open Project Specification or
OASIS Standard, can be obtained from the OASIS TC Administrator. OASIS makes no representation that any information or list of
intellectual property rights will at any time be complete, or that any claims in such list are, in fact, Essential Claims.

[The name "OASIS" is a trademark of OASIS, the owner and developer of this specification, and should be used only to refer to the](https://www.oasis-open.org)
organization and its official outputs. OASIS welcomes reference to, and implementation and use of, specifications, while reserving the right
[to enforce its marks against misleading uses. Please see https://www.oasis-open.org/policies-guidelines/trademark for above guidance.](https://www.oasis-open.org/policies-guidelines/trademark)


-----

Standards Track Work Product

## Table of Contents

1. Introduction

1.1 Terminology
1.2 References
1.3 RDF Namespaces
1.4 Typographical Conventions and Use of RFC Terms

2. Goals/Motivation
3. Architecture
4. OSLC Core 3.0 Capabilities

4.1 Resource Constraints
4.2 Version Compatibility
4.3 Conformance
4.4 Acknowledgements
4.5 Change History


-----

Standards Track Work Product

## 1. Introduction

_This section is non-normative._

Information Technology (IT) enterprises are constantly addressing demands to do more with less. To meet this demand they need more
efficient development processes and supporting tools. This has resulted in demand for better support of integrated system and software
processes. Enterprises want solutions (such as software or hardware development tools) from different vendors, open source projects and
their own proprietary components to work together. This level of integration, however, can become quite challenging and unmanageable. In
order to enable integration between a heterogeneous set of tools and components from various sources, there is a need for a sufficient
supporting architecture that is loosely coupled, minimal, and standardized. OSLC is based on World Wide Web and Linked Data principles,
such as those defined in the W3C Linked Data Platform [LDP], to create a cohesive set of specifications that can enable products, services,
and other distributed network resources to interoperate successfully [LDP].

Fig. 1 OSLC Core 3.0 Architecture

OSLC is motivated by domain-driven scenarios that inspire standardization of common capabilities across disciplines such as change
management, requirements management, and quality management, as well as by cross-domain scenarios such as Application Lifecycle
Management (ALM) & DevOps, Product Lifecycle Management (PLM), and Integrated Service Management (ISM). The OSLC approach
focuses on software lifecycle management to ensure it meets a core set of scenarios and requirements. Nonetheless, it can be used by
tools belonging to any other domains and cross-domain scenarios such as Internet of Things, back office application integration, and
customer relationship management.

The OSLC Core specifications provide additional capabilities that expand on the W3C LDP capabilities, as needed, to enable key
integration scenarios. These capabilities define the essential and common technical elements of OSLC domain specifications and offer
guidance on common concerns for creating, updating, retrieving, and linking to lifecycle resources based on W3C [LDP].


-----

Standards Track Work Product

Fig. 2 OSLC Core 3.0 Overview

As seen in Fig. 2 OSLC Core 3.0 Overview, there are a number of capabilities developed in different standards organizations and working
groups. The arrows represent either dependencies or extensions to some specifications or capabilities. OSLC domain specifications may
depend on OSLC Core 3.0 specifications as scenarios motivate. However, a leading goal is to minimize and eliminate unnecessary
dependencies to simplify adoption, which may result in no dependency on OSLC Core 3.0 specifications for some OSLC domains.

This work is an evolution from the OSLC Core 2.0 [OSLCCore2] efforts, taking the experience gained from that effort along with the
common foundation on W3C LDP, to produce an updated set of specifications that are simpler, built on layered capabilities and easier to
adopt.

**1.1 Terminology**

Terminology uses and extends the terminology and capabilities of W3C Linked Data Platform [LDP], W3C's Architecture of the World Wide
Web [WEBARCH] and Hyper-text Transfer Protocol [HTTP11].

OSLC Server

LDP Server that also supports capabilities defined by at least on OSLC-based specification. See Server [HTTP11] and LDP Server

[LDP].

OSLC Client

LDP Client that uses capabilities defined by some OSLC-based specifications. See Client [HTTP11] and LDP Client [LDP]. A
particular software component or application could be an OSLC Server supporting a set of domains, and an OSLC Client of other
domains depending on its needs.

Domain

A topic area of a specific focus area and/or collection of disciplines. Often OASIS OSLC-affiliated TCs are organized around a
domain.

OSLC Core Specifications

Specifications that cover specific capabilities that are often needed across various domains. They are created, authored and
endorsed by the OASIS OSLC Open Project. Can be abbreviated to Core Specifications.

OSLC Domain Specifications


-----

Standards Track Work Product

Specifications that cover a domain need, including existing open-services.net specifications and new specifications created and
authored by OASIS OSLC-affiliated TCs. Can be abbreviated to Domain Specifications

Resource Shape

The set of properties (triples) that constrain a resource for specific operations (i.e. creation, update or query), and for each property,
their value types, allowed values and cardinality.

**Some industry terms that are often referred to (not exhaustive):**

[Product Lifecycle Management (PLM)](https://en.wikipedia.org/wiki/Product_lifecycle_management)

The process of managing the entire lifecycle of a product from its conception, through design and manufacture, to service and
disposal.

[Systems Engineering](https://en.wikipedia.org/wiki/Systems_engineering)

An interdisciplinary field of engineering that focuses on how to design and manage complex engineering systems over their life cycles.

[Application Lifecycle Management (ALM)](https://en.wikipedia.org/wiki/Application_lifecycle_management)

The marriage of business management to software engineering made possible by tools that facilitate and integrate requirements
management, architecture, coding, testing, tracking, quality and release management.

[DevOps](https://en.wikipedia.org/wiki/DevOps)

A software development method that stresses communication, collaboration and integration between software developers and
Information Technology(IT) professionals in support of continuous delivery.

[IT Service Management (ITSM)](https://en.wikipedia.org/wiki/IT_service_management)

The implementation and management of quality information technology services. IT service management is performed by IT service
providers through people, process and information technology.

**1.1.1 Deprecated terms**

Previous revisions of OSLC-based specifications [OSLCCore2], used terminology that may no longer be relevant, accurate or needed any
more. Some of those deprecated terms are:

Provider (deprecated)

See Server [HTTP11].

Consumer (deprecated)

See Client [HTTP11].

**1.2 References**

**1.2.1 Normative references**

[ABNF]

[D. Crocker; P. Overell. Augmented BNF for Syntax Specifications: ABNF. IETF. Internet Standard. URL:](https://tools.ietf.org/html/rfc5234)
[https://tools.ietf.org/html/rfc5234](https://tools.ietf.org/html/rfc5234)

[CORS]

[WHATWG contributors. Fetch standard. WHATWG. Living Standard. URL: https://fetch.spec.whatwg.org/commit-](https://fetch.spec.whatwg.org/commit-snapshots/d070ea245c6eb66cf4196324f063dc6ab608d9e6/#http-cors-protocol)
snapshots/d070ea245c6eb66cf4196324f063dc6ab608d9e6/#http-cors-protocol

[HTTP11]

[R. Fielding, Ed.; J. Reschke, Ed.. Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing. IETF, June 2014.](https://httpwg.org/specs/rfc7230.html)


-----

Standards Track Work Product

[Proposed Standard. URL: https://httpwg.org/specs/rfc7230.html](https://httpwg.org/specs/rfc7230.html)

[LDP]

[Steve Speicher; John Arwe; Ashok Malhotra. Linked Data Platform 1.0. W3C, 26 February 2015. W3C Recommendation. URL:](https://www.w3.org/TR/ldp/)
[https://www.w3.org/TR/ldp/](https://www.w3.org/TR/ldp/)

[LDPPaging]

[S. Speicher; J. Arwe; A. Malhotra. Linked Data Platform Paging 1.0. http://www.w3c.org. W3C Working Group Note. URL:](https://www.w3.org/TR/ldp-paging/)
[https://www.w3.org/TR/ldp-paging/](https://www.w3.org/TR/ldp-paging/)

[OSLCCCM1]

[Nick Crossley. OSLC Configuration Management 1.0. OASIS. OASIS Working Draft. URL: https://oslc-op.github.io/oslc-](https://oslc-op.github.io/oslc-specs/specs/config/oslc-config-mgt.html)
specs/specs/config/oslc-config-mgt.html

[OSLCCore2]

[S. Speicher; D. Johnson. OSLC Core 2.0. http://open-services.net. Finalized. URL: https://open-](https://open-services.net/bin/view/Main/OslcCoreSpecification)
services.net/bin/view/Main/OslcCoreSpecification

[OSLCQuery]

[Jim Amsden; S. Padgett; S. Speicher; David Honey. OSLC Query Version 3.0. OASIS. Project Specification. URL:](https://docs.oasis-open-projects.org/oslc-op/query/v3.0/oslc-query.html)
[https://docs.oasis-open-projects.org/oslc-op/query/v3.0/oslc-query.html](https://docs.oasis-open-projects.org/oslc-op/query/v3.0/oslc-query.html)

[OSLCTRS3]

[Nick Crossley, Axel Reichwein. OSLC Tracked Resource Set 3.0. OASIS. OASIS Working Draft. URL: https://oslc-op.github.io/oslc-](https://oslc-op.github.io/oslc-specs/specs/trs/tracked-resource-set.html)
specs/specs/trs/tracked-resource-set.html

[OpenIDConnect]

_[OpenID Connect. openid.net. URL: http://openid.net/connect/](http://openid.net/connect/)_

[RFC2119]

[S. Bradner. Key words for use in RFCs to Indicate Requirement Levels. IETF, March 1997. Best Current Practice. URL:](https://www.rfc-editor.org/rfc/rfc2119)

[https://www.rfc-editor.org/rfc/rfc2119](https://www.rfc-editor.org/rfc/rfc2119)

[RFC8174]

[B. Leiba. Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words. IETF, May 2017. Best Current Practice. URL:](https://www.rfc-editor.org/rfc/rfc8174)

[https://www.rfc-editor.org/rfc/rfc8174](https://www.rfc-editor.org/rfc/rfc8174)

[rfc6749]

[D. Hardt, Ed.. The OAuth 2.0 Authorization Framework. IETF, October 2012. Proposed Standard. URL: https://www.rfc-](https://www.rfc-editor.org/rfc/rfc6749)

editor.org/rfc/rfc6749

**1.2.2 Informative references**

[HTML5]

[Ian Hickson; Robin Berjon; Steve Faulkner; Travis Leithead; Erika Doyle Navara; Theresa O'Connor; Silvia Pfeiffer. HTML5. W3C, 27](https://www.w3.org/TR/html5/)
[March 2018. W3C Recommendation. URL: https://www.w3.org/TR/html5/](https://www.w3.org/TR/html5/)

[LDBestPractices]

_[Linked Data Best Practices. jazz.net. URL: https://jazz.net/wiki/bin/view/LinkedData/BestPractices](https://jazz.net/wiki/bin/view/LinkedData/BestPractices)_

[SHACL]

[Holger Knublauch; Dimitris Kontokostas. Shapes Constraint Language (SHACL). http://www.w3.org/. W3C Recommendation. URL:](https://www.w3.org/TR/shacl/)
[https://www.w3.org/TR/shacl/](https://www.w3.org/TR/shacl/)


-----

Standards Track Work Product

[Turtle]

[Eric Prud'hommeaux; Gavin Carothers. RDF 1.1 Turtle. W3C, 25 February 2014. W3C Recommendation. URL:](https://www.w3.org/TR/turtle/)
[https://www.w3.org/TR/turtle/](https://www.w3.org/TR/turtle/)

[WEBARCH]

[Ian Jacobs; Norman Walsh. Architecture of the World Wide Web, Volume One. W3C, 15 December 2004. W3C Recommendation.](https://www.w3.org/TR/webarch/)
[URL: https://www.w3.org/TR/webarch/](https://www.w3.org/TR/webarch/)

[rdf11-concepts]

[Richard Cyganiak; David Wood; Markus Lanthaler. RDF 1.1 Concepts and Abstract Syntax. W3C, 25 February 2014. W3C](https://www.w3.org/TR/rdf11-concepts/)
[Recommendation. URL: https://www.w3.org/TR/rdf11-concepts/](https://www.w3.org/TR/rdf11-concepts/)

**1.3 RDF Namespaces**

OSLC Core defines the namespace URI of http://open-services.net/ns/core# with a namespace prefix of oslc.

OSLC Core uses the following prefixes:

|Prefix|Namespace|
|---|---|
|dcterms|http://purl.org/dc/terms/|
|foaf|http://xmlns.com/foaf/0.1/|
|ldp|http://www.w3.org/ns/ldp#|
|owl|http://www.w3.org/2002/07/owl#|
|prov|http://www.w3.org/ns/prov#|
|rdf|http://www.w3.org/1999/02/22-rdf-syntax-ns#|
|rdfs|http://www.w3.org/2000/01/rdf-schema#|
|vann|http://purl.org/vocab/vann/|
|vs|http://www.w3.org/2003/06/sw-vocab-status/ns#|
|xsd|http://www.w3.org/2001/XMLSchema#|



**1.4 Typographical Conventions and Use of RFC Terms**

As well as sections marked as non-normative, all authoring guidelines, diagrams, examples, and notes in this specification are nonnormative. Everything else in this specification is normative.

The key words "MUST", "MUST **NOT", "REQUIRED", "SHALL", "SHALL** **NOT", "SHOULD", "SHOULD** **NOT", "RECOMMENDED", "NOT** **RECOMMENDED", "MAY", and**

["OPTIONAL" in this specification are to be interpreted as described in BCP 14 [RFC2119] [RFC8174] when, and only when, they appear in all](https://tools.ietf.org/html/bcp14)
capitals, as shown here.


-----

Standards Track Work Product

## 2. Goals/Motivation

_This section is non-normative._

The primary goal of OSLC is to enable integration of federated, shared information across tools that support different, but related domains.
OSLC was initially focused on development of Information Technology (IT) solutions involving processes, activities, work products and
supporting tools for Application Lifecycle Management (ALM). However, OSLC capabilities could be applicable to other domains. The
specific goals for OSLC Core 3.0 are to build on the existing OSLC Core 2.0 specifications to further facilitate the development and
integration of domains and supporting tools that address additional integration needs. Specifically:

Integration is based on an open standard, and not controlled by any single vendor
OSLC 3.0 is based on the new W3C Linked Data Platform standard which provides a solid foundation for reading and writing linked
data resources
The specifications are simpler, more consistent and will potentially be more attractive to, and easier to consume by new integrations
There are some new capabilities including Attachments, inverse link labels, traceability and impact types
Domain vocabularies can be improved for data consistency and removing data gaps
All Resource Shapes are provided in machine readable [Turtle] files

The following guiding principles were used to govern the evolution of OSLC and guide the development of the OSLC Core 3.0
specifications.

_Scenario-driven_

Every capability should be linked back to key integration scenarios that motivate its need. These are important not only for knowing that the
correct specification content is being developed but also to assist with implementers understanding the intended usage and in developing
relevant test cases.

_Incremental_

Specifications should be developed in an incremental fashion that not only validates the technical approaches but also delivers integration
value sooner.

_Loose-coupling_

Specifications should support a model where clients have little to no knowledge about server implementation-specific behaviors in order to
support key integration scenarios. As a result, clients should be unaffected by any server application software or data model implementation
changes. Similarly, client software should be able to be independently changed without changes to server software.

_Minimalistic_

Specification authors should strive to find not only the simplest solution that would work for a given scenario but allows for easy adoption.
Authors should avoid solutions that offer additional capabilities which may inhibit adoption of necessary capabilities.

_Capability Based_

A capability is the ability to perform actions to achieve outcomes described by scenarios through the use of specific technologies.
Capabilities should be incrementally defined as independent focused specifications and independently discoverable at runtime. Even
though there may be some generally agreed upon best practices for capability publication and discovery, each capability should define how
it is published and discovered. The Core OSLC capabilities are defined in this specification.

_Vocabularies_

Various OSLC MS-affiliated TCs, or any specification development body that is authoring specifications for specific domains of knowledge,
should minimally define vocabularies and the semantics behind the various terms. Some consideration should be given for global reuse
when terms are used for cross domain queries and within other domain resource shape definitions. Domain specifications are the definition
of an OSLC capability, and how those vocabulary terms are used in LDP interactions by both the clients and servers of that capability. The
specification should include defining resource shapes that describe resources based on a set of vocabulary terms, which introduces any
domain specific constraints on the vocabulary's usage.

OSLC domain vocabularies should follow the recommended best practices for managing RDF vocabularies described at

[LDBestPractices].


-----

Standards Track Work Product

## 3. Architecture

_This section is non-normative._

In support of the previously stated goals and motivation, it is desired to have a consistent and recommended architecture. The architecture
needs to support scenarios requiring a protocol to access, create, update and delete resources. [LDP] is the foundation for this protocol.
Resources need to relate, or link, to one another utilizing a consistent, standard and web-scale data model. Resource Description
Framework (RDF) [rdf11-concepts] is the foundation for this. The ability to work with these data models over HTTP protocols, is based on

[LDP].

Some scenarios require the need to integrate user interface components: either within a desktop or mobile web-browser, mobile device
application, or rich desktop applications. For these scenarios the technology is rapidly evolving and changing. Priority should be based on
existing standards such as HTML5, with use of iframe and postMessage(). [HTML5]

OSLC Core specification documents elaborate on the conformance requirements leveraging these various technologies and approaches.

As the primary goals have been outlined around lifecycle integration, some scenarios may require exploration of new (or different)
approaches and technologies. As with all specification development efforts, the OSLC Open Project will advise, develop and approve such
efforts.


-----

Standards Track Work Product

## 4. OSLC Core 3.0 Capabilities

_This section is non-normative._

The following sections and referenced documents define the capabilities for OSLC Core 3.0. These documents comprise the multi-part
specification for OSLC Core 3.0. They represent common capabilities that servers may provide and that may be discovered and used by
clients. Although OSLC Core could be useful on its own, it is intended to specify capabilities that are common across many domains.
Servers will generally specify conformance with specific domain specifications, and those domain specifications will describe what parts of
OSLC Core are required for conformance. This allows servers to implement the capabilities they need in a standard way without the burden
of implementing capabilities that are not required. The purpose of the OSLC Core Discovery capability is to allow clients to determine what
capabilities are provided by a server. Any provided capability must meet all the conformance criteria for that capability as defined in the
OSLC Core 3.0 specifications.

This implies that any capability that is discoverable is essentially optional, and once discovered, the capability is provided as defined in the
applicable OSLC specifications. Servers should support OSLC Discovery, but Discovery itself is also an optional capability as servers
could provide other means of informing specific clients of supported OSLC capabilities that could be utilized directly. For example, a server
might provide only preview dialogs on specific resources and nothing else.

**4.1 Resource Constraints**

The shape of an RDF resource is a description of the set of triples it is expected to contain and the integrity constraints those triples are
required to satisfy. Applications of shapes include validating RDF data, documenting RDF APIs, and providing metadata to tools that handle
RDF data such as form and query builders.

Shapes are different than vocabularies in that shapes may change with new revisions of resource definitions, whereas vocabularies should
evolve in place in a compatible manner.

[Constraints on OSLC Core and Domain resources SHOULD be described using OSLC Core Version 3.0. Part 6: Resource Shape which is](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/resource-shape.html)
included as part of the OSLC Core multi-part specifications. Servers MAY use other constraint languages such as [SHACL] to define

resource constraints. [core-1]

OSLC Domain specifications SHOULD use the following URI pattern when publishing each individual resource shape: [core-2]

http://open-services.net/ns/[vocab-short-name]/shapes/[version]#[shape-name]

For example, for Change Management 3.0, a shape describing the base Change Request resource type might have the shape URI:

http://open-services.net/ns/cm/shapes/3.0#ChangeRequestShape

Not all shapes would necessarily be updated at the same time.

To allow different versions of individual shapes to be reused in different versions of a domain specification while still allowing a client to
browse the set of possible shapes, domains SHOULD provide an resource for all the shapes for a spec version, at a URI defined by the
following pattern:

http://open-services.net/ns/[vocab-short-name]/shapes/[SPEC-version]

[core-3]

For example, for Change Management, there should be a resource at: http://open-services.net/ns/cm/shapes with members such as:

http://open-services.net/ns/cm/shapes/3.0#TaskShape
http://open-services.net/ns/cm/shapes/3.1#WeaknessShape
http://open-services.net/ns/cm/shapes/2.0#ChangeRequestShape

**4.1.1 Authentication**

Authentication determines how a user of a client identifies themselves to a server to ensure the user has sufficient privileges to access
resources from that server, and provides a mechanism for servers to control access to resources.


-----

Standards Track Work Product

OSLC 3.0 servers MAY protect resources with HTTP Basic Authentication. OSLC Services that use HTTP Basic Authentication SHOULD do so

only via SSL. [core-4]

OSLC 3.0 servers SHOULD protect resources with [rfc6749] Authentication utilizing [OpenIDConnect]. [core-5]

**4.1.2 Resource Discovery**

Resource Discovery defines a common approach for HTTP/LDP-based servers to be able to publish their RESTful API capabilities and
how clients can discover and use them.

**4.1.3 Resource Representations**

OSLC resource representations come in many forms and are subject to standard HTTP and mechanisms for content negotiation.

OSLC domain specifications specify the representations needed for the specific scenarios that they are addressing, and should recognize
that different representations are appropriate for different purposes. For example, browser oriented scenarios might be best addressed by
JSON or Atom format representations.

OSLC domain specifications are also expected to follow common practices and conventions that are in concert with existing industry
standards and which offer consistency across domains. All of the OSLC specifications are built upon the standard RDF data model,
allowing OSLC to align with the Linked-Data Platform [LDP]. In addition, all OSLC specifications have adopted the convention to illustrate
most examples using Turtle and/or JSON-LD representations and will typically require these representations to enable consistency across
OSLC implementations.

OSLC Services MUST support at least one RDF resource serialization format, and SHOULD support as many serialization formats as possible
through content negotiation. [core-6]

OSLC Services SHOULD provide and accept RDF documents in Turtle format (identified by the MIME-type 'text/turtle') and in JSON-LD format
(identified by the MIME-type 'application/ld+json') representations for each OSLC resource for compatibility with LDP 1.0. [core-7]

OSLC Services SHOULD provide and accept RDF/XML representations for each OSLC resource to preserve compatibility with

[OSLCCore2]. [core-8]

OSLC Services MAY provide and accept existing standard or emerging standard formats such as XML, HTML, and the Atom Syndication

Format. [core-9]

OSLC servers SHOULD support the Accept header and whenever possible, respond with one of the content types requested by the client.
When the Accept header requests an unsupported RDF serialization, the OSLC server SHOULD return an RDF serialization format that it
does support, indicating what it is in the Content-Type header. If the server gets an Accept header for some non-RDF content type, say
ATOM, that it does not support, then it SHOULD return 406 Unacceptable. [core-10]

OSLC servers SHOULD support the CORS protocol [CORS] in order to allow browser-based OSLC clients to interact with the server. [core11] In addition to following the general practice, server implementers are recommended to apply the recommendations listed below:

OSLC servers SHOULD use the Access-Control-Allow-Headers header [CORS] to allow the use of the Content-Type header in OSLC
requests. Despite the Content-Type header being a CORS-safelisted request header, it needs to be explicitly allowed in order to
expand the range of its permitted values and allow OSLC clients to send RDF contents to the server. [core-12]
OSLC servers SHOULD use the Access-Control-Allow-Headers header [CORS] to allow the use of the OSLC-Core-Version header in
OSLC requests. [core-13]

**4.1.4 Common Vocabulary**

Common Vocabulary Terms defines a number of commonly used RDF vocabulary terms and resources (shapes), that have broad
applicability across various domains.

**4.1.5 Resource Operations**

Resource Operations specify how clients create, read, update and delete resources managed by servers.

OSLC Core defines a set of HTTP REST services for a set of capabilities that facilitate flexible, loosely coupled tool integration. These
services may be augmented by varous OSLC domain specifications that specify the capabilities, vocabularies and constraints that define
specific resources managed by these integration capabilities.


-----

Standards Track Work Product

OSLC Servers MUST implement standard HTTP protocols and MUST at least support GET requests that respond with resources in some RDF
serialization format. [core-14]

OSLC Services use HTTP for create, retrieve, update and delete operations on resources. OSLC Services MUST comply with the HTTP
specification [HTTP11]. [core-15]

Because the update process may involve first getting a resource, modifying it and then later putting it back to the server, there is the
possibility of a conflict, e.g. some other client may have have updated the resource since the GET. To mitigate this problem, OSLC Services
**SHOULD use the HTTP If-Match header on a PUT request: [core-16]**

If the HTTP If-Match header is missing OSLC Services SHOULD return HTTP Bad Request (400) status code to indicate that the
header is required. [core-17]
If the HTTP If-Match header is present OSLC Services MUST behave as described in the HTTP specification, returning an HTTP
Precondition Failed (412) error to indicate that the header does not match. [core-18]
If the HTTP If-Match header is present and it matches, but there is some other problem or conflict with the update then OSLC
Services MAY return an HTTP Conflict (409) to indicate that problem. [core-19]

An OSLC Service SHOULD preserve property values that are not part of the resource definition or Resource Shape known by the server
(unknown property values). An OSLC Service MUST return a 4xx status code if it decides not to persist any of the unknown property values (in
accordance with the LDP specification §4.2.4.4). [core-20]

An OSLC Client MUST preserve any unknown property values between requests to the OSLC Services for all HTTP verbs except PATCH (in
accordance with the LDP specification §4.3.1.11). [core-21]

**4.1.6 Selective Properties**

OSLC Services MAY support a technique called Selective Properties to enable clients to retrieve only selected property values. [core-22]

By adding the key=value pair oslc.properties, specified below, to a resource URI, a client can request a new resource with a subset of the
original resource's values. An additional key=value pair oslc.prefix can be used to define prefixes used to identify the selected properties.

The oslc.properties key=value pair lets you specify the set of properties to be included in the response. Both immediate and nested
properties may be specified. A nested property is a property that belongs to the resource referenced by another property. Nested properties
are enclosed in brace brackets, and this nesting may be done recursively, i.e. a nested property may contain other nested properties.

For example, suppose we have a bug report resource at the following URL:

EXAMPLE 1: Bug Report URL

http://example.com/bugs/4242

Suppose this bug resource has properties such as dcterms:title, dcterms:description, and dcterms:creator, and that dcterms:creator
refers to a person resource that has properties such as foaf:givenName and foaf:familyName. Suppose you want a representation of the
bug report that includes its dcterms:title and the foaf:givenName and foaf:familyName of the person referred to by its dcterms:creator.
The following URL illustrates the use of the oslc.properties query value to include those properties:

EXAMPLE 2: Selective Properties URL

http://example.com/bugs/4242?oslc.properties=dcterms:title,dcterms:creator{foaf:givenName,foaf:familyName}

The oslc.properties pair is defined by the oslc_properties term in the following BNF grammar:

oslc_properties ::= "oslc.properties=" properties
properties   ::= property ("," property)*
property    ::= identifier | wildcard | nested_prop
nested_prop   ::= (identifier | wildcard) "{" properties "}"
wildcard    ::= "*"
identifier   ::= PrefixedName
PrefixedName  ::= /* see "SPARQL Query Language for RDF", http://www.w3.org/TR/rdf-sparql-query/#rPrefixedName */

In our examples of oslc.properties, property names include a URI prefix, i.e. dcterms: or foaf:. Here we assume that OSLC has predefined
the Dublin Core ( dcterms:) and Friend of a Friend ( foaf:) prefixes. However, OSLC resources should also be open to new content, which
means that new properties may not have predefined URI prefixes. We therefore need a way to define new URI prefixes in resource requests.


-----

Standards Track Work Product

The oslc.prefix value lets you specify URI prefixes used in property names. For example, suppose the foaf: prefix was not predefined. The
following URL illustrates the use of the oslc.prefix value to define it:

EXAMPLE 3: Example URL with oslc.prefix

http://example.com/bugs/4242?oslc.prefix=foaf=<http://xmlns.com/foaf/0.1/>&oslc.properties=foaf:lastName,...

The syntax of the oslc.prefix is defined by the oslc_prefix term in the following BNF grammar:

oslc_prefix ::= "oslc.prefix=" prefix_defs
prefix_defs ::= prefix_def ("," prefix_def)*
prefix_def ::= prefix "=" uri_ref_esc
prefix   ::= PN_PREFIX
PN_PREFIX  ::= /* see "SPARQL Query Language for RDF", http://www.w3.org/TR/rdf-sparql-query/#rPN_PREFIX */
uri_ref_esc ::= /* an angle bracket-delimited URI reference in which > and \ are \-escaped. */

OSLC Core specifies a number of predefined PrefixDefinitions for convenience. OSLC Domain specifications may specify additional predefined PrefixDefinitions for their purposes.

An OSLC Server SHOULD support the following PrefixDefinitions:

dcterms: <http://purl.org/dc/terms/>
foaf: <http://xmlns.com/foaf/0.1/>
owl: <http://www.w3.org/2002/07/owl#>
rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
xsd: <http://www.w3.org/2001/XMLSchema#>
rdfs: <http://www.w3.org/2000/01/rdf-schema#>
ldp: <http://www.w3.org/ns/ldp#>
oslc: <http://open-services.net/ns/core#>
trs: <http://open-services.net/ns/core/trs#>

[core-23]

**4.1.7 Resource Preview**

Resource Preview specifies a technique to get a minimal HTML representation of a resource identified by a URL. Applications often use
this representation to display a link with an appropriate icon, a label, or display a small or large preview when a user makes some gesture
over a link.

**4.1.8 Delegated Dialogs**

Delegated Dialogs allow one application to embed a creation or selection UI into another using HTML iframe elements and JavaScript
code. The embedded dialog notifies the parent page of events using HTML5 postMessage.

**4.1.9 Query**

OSLC servers will often manage large amounts of potentially complex link-data entities. Practical use of this information will require some
query capability that minimally supports selection of matching elements, filtering of desired properties and ordering. OSLC Core defines a
query capability that is relatively simple, can be implemented on a wide range of existing server architectures, and provides a standard, data
source independent query mechanism. The purpose of this query capability is to support tool integration through a common query
mechanism.

OSLC Servers MAY support a Query Capability as defined in [OSLCQuery] to enable clients to perform selection and projection operations

in order to retrieve a selected subset of resources and property values from an LDPC. [core-24]

**4.1.10 Resource Paging**

When a client requests a resource, the client should expect that the entire resource will be returned in the response, with all property values.
This can be problematic because, in some cases, resources may be so large that a client might not want to retrieve the entire resource in
one HTTP response.


-----

Standards Track Work Product

One solution for clients that are sensitive to response size is to check the response size before loading. This method is described in the next
section. Another solution is to use Resource Paging.

Resource Paging specifies a capability for servers to make the state of large resources or long lists of resources available as a list of
smaller subset resources (pages) whose representation is easier to produce by the server and consume by clients. Resource paging is
particularly useful in handling results from the query capability or the contents of an LDP container.

**4.1.10.1 Checking Response Size**

Clients that do not wish to load large resources may use the HTTP HEAD method to determine the size of a resource.

When responding to an HTTP HEAD request, according to [HTTP11] the server SHOULD include an HTTP Content-Length header that
indicates the size of the resource as the "decimal number of octets." [core-25]

**4.1.10.2 Paging Stability**

Because HTTP is a stateless protocol and OSLC Services manage resources that can change frequently, OSLC clients should assume that
the resources returned on a given page are unstable and may change over time.

Some OSLC Servers might wish to guarantee stable paging, meaning that the sequence of pages returned from the server represent a
snapshot in time and will not change as the client pages through them. OSLC specifications that require stable paging should state this
requirement and specify to which resources it applies.

Note that because stable paging implementations are based on server-side state, it is possible that the state will expire. Implementations
**MAY use the HTTP response code 410 (Expired) to indicate to clients that the link they requested has expired. [core-26]**

**4.1.10.3 Response Information**

A response info resource representation describes information about a paged HTTP response body in which it appears.

Resource representations returned via Resource Paging MUST include a resource of type oslc:ResponseInfo, as defined in part 7 of this
multi-part specification: Vocabulary. [core-27]

The subject resource URI of the oslc:ResponseInfo resource representation MUST be the HTTP request URI or the URI from subsequent
redirects. The response representation MAY also include properties from subject resources different from the one identified by the request

URI. [core-28]

When responding to a request that includes oslc.pageSize in the URI, a server MAY divide the response into a number of pages and use the

value as a hint about the maximum number of RDF statements to be included in each page. Servers MAY return pages containing more or

fewer RDF statements than specified. [core-29]

Below is an example using the OSLC Core RDF/XML representation guidance, that illustrates how the oslc:ResponseInfo resource
representation is included in addition to the blog entry resource representation.

By adding oslc.pageSize to the query component of the resource URI, the client requests that the server break each response into pages
using the specified value as a hint for maximum number of RDF statements in each page. Clients should make no assumptions about the
maximum number of RDF statements returned in a page.

EXAMPLE 4: Resource Paging, partial response with response info resource representation

GET http://example.com/blogs/entry/1?oslc.paging=true&amp;pageSize=200&amp;pageno=2

<rdf:RDF
xmlns:oslc_blog="http://open-services.net/ns/bogus/blogs#"
xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:foaf="http://http://xmlns.com/foaf/0.1/"
xmlns:dcterms="http://purl.org/dc/terms/">

<oslc_blog:Entry
rdf:about="http://example.com/blogs/entry/1">
&lt;!-- partial property values of of the blog entry --&gt;
</oslc_blog:Entry>

<oslc:ResponseInfo rdf:about="http://example.com/blogs/entry/1?oslc.paging=true&amp;pageSize=200&amp;pageno=2">
<oslc:nextPage rdf:resource="http://example.com/blogs/entry/1?oslc.paging=true&amp;pageSize=200&amp;pageno=3" />
</oslc:ResponseInfo>


-----

Standards Track Work Product

</rdf:RDF>

Refer to the OSLC vocabulary specification for further information on the ResponseInfo resource.

**4.1.10.4 Using Resource Paging**

OSLC Services MAY support [LDPPaging] to enable clients to retrieve large LDP resources (LDPRs) a page at a time. [core-30]

OSLC Services SHOULD support OSLC paging as described in this section to ensure compatibility with OSLC 2.0 server implementations.

[core-31]

To request a paged version of a resource, a client MUST add at least one "key=value" pair to the query component of the resource URI: Either
oslc.paging=true, or oslc.pageSize, or both. [core-32]

When responding to a request that includes oslc.paging=true in the URI, a server MAY return a representation that contains a subset of the

resource's property values. [core-33]

By adding oslc.pageSize to the query component of the resource URI, the client requests that the server respond with a specific number of
property values. For example, oslc.pageSize=20 indicates to the server that the client would like 20 values per page.

When responding to a request that includes oslc.pageSize in the URI, a server SHOULD return a representation that contains the requested
number of property values. [core-34]

When Resource Paging is used, the values of a multi-valued property MAY be split across resource pages. [core-35]

When Resource Paging is used, each property value MUST be represented in its entirety and not split across multiple partial resource pages.

[core-36]

When a page is returned and it is NOT the last page in the sequence, then it SHOULD include an oslc:ResponseInfo (see above), which
contains a resource-valued property oslc:nextPage that links to a resource that represents the next page of property-values. [core-37]

When paging is unstable, by the time a client follows an oslc:nextPage link there may no longer be a next page, in this case the server MAY

respond with an HTTP 404 Page Not Found status code. [core-38]

**4.1.10.5 Provider Response Size Limitations**

When a client requests a resource that an OSLC Service considers to be too large to return in one response and the client has not indicated
that it desires paging (via oslc.paging or oslc.pageSize), the OSLC Service MAY redirect the client to a representation that contains partial

information about the resource. [core-39]

When the OSLC Service opts to redirect the client to a partial representation, it MUST return an HTTP Status 302 redirect to a URL that
includes either oslc.paging, or oslc.pageSize, or both. [core-40]

If the URL includes oslc.pageSize then the value should be a value that is acceptable to the service. The client may choose to follow the
redirect and receive a representation that contains partial information about the resource.

On receiving a resource representation, OSLC Clients should check for the presence of an oslc:nextPage value to determine if the
representation contains partial information about the resource. If the value is present, then paging is in effect and the representation contains
partial information about the resource.

**4.1.11 Attachments**

Attachments describes a minimal way to manage attachments related to web resources using LDP-Containers and Non-RDF Source

[LDP].

**4.1.12 Tracked Resource Sets**

OSLC defines a Tracked Resource Set capability that allows servers to expose a set of resources in a way that enables clients to discover
the exact set of resources in the set, to track ongoing changes affecting resources in the set. This allows OSLC servers to expose a live
feed of linked data in a way that permits clients to build, aggregate, and maintain live, searchable information based on that linked data.

OSLC Servers MAY support a Tracked Resources Set capability as defined in [OSLCTRS3] to enable OSLC data consumers and providers

flexible ways of sharing information. [core-41]


-----

Standards Track Work Product

**4.1.13 Configuration Management**

OSLC defines a Configuration Management capability for managing versions and configurations of linked data resources from multiple
domains. Using client and server applications that implement the configuration management capability, a team administrator can create
configurations of versioned resources contributed from tools and data sources across the lifecycle. These contributions can be assembled
into aggregate (global) configurations that are used to resolve references to artifacts in a particular and reproducible context.

OSLC Clients and Servers MAY support a Configuration Management capability as defined in [OSLCCCM1]. [core-42]

**4.1.14 Error Responses**

Error responses returned by servers in response to requests are defined in Common Vocabulary Terms, Errors.

**4.2 Version Compatibility**

**4.2.1 Overview**

_This section is non-normative._

OSLC is intended to provide a foundation for (lifecycle) application interoperability. A significant number of OSLC domains, and client and
server implementations already exist and are in common use. Interoperability issues between applications on incompatible OSLC versions
could result in negative impact to end users. One of the goals of the OSLC initiative is to mitigate or eliminate the need for lock-step version
upgrades, where clients or servers target one version of a specification and break when new versions are introduced -- requiring all services
to be upgraded simultaneously.

This section introduces a capability for the clients and servers to pass an OSLC version. However, exposing version numbers in OSLC
implementations could lead to interoperability issues. Ultimately each domain needs to decide its compatibility needs.

**4.2.2 Versioning support in clients and servers**

OSLC Clients and Servers SHOULD use the OSLC-Core-Version header to indicate what OSLC version they expect or support. [core-43]
When returning an RDF response, an OSLC Server MUST return the OSLC-Core-Version header set to the Core specification with which the
representation complies. [core-44]

The OSLC-Core-Version header consists of a major and minor version components and MUST conform to the following ABNF grammar

[ABNF]:

SP = " "
HTAB = %x09
WSP = SP / HTAB
DIGIT = %x30-39

header = oslc-version
MAJOR = 1*DIGIT
MINOR = 1*DIGIT
oslc-version = "OSLC-Core-Version:" *WSP MAJOR "." MINOR

[core-45]

Example:

OSLC-Core-Version: 3.0

The major version component in the OSLC-Core-Version header MUST be greater or equal to "2". [core-46] An OSLC Server SHOULD reject a
request with the OSLC-Core-Version header that has a major version value below "2" with a response 400 Bad Request. [core-47]

If the OSLC-Core-Version header is present in the request and set to a version that an OSLC Server can support, then the Server MUST return
a representation that is complies with the specified version. [core-48] If the OSLC-Core-Version header is present and indicates a
specification version that the Server cannot support, the Server SHOULD respond with what it determines is the most compatible version that it
can return; however, the server MAY reject the request with 400 Bad Request. [core-49] If the OSLC-Core-Version header is not present then

the Server SHOULD respond by returning a resource that conforms to the earliest or most compatible (as determined by the implementation)
specification version's representation. [core-50]

OSLC Core 3.0 Servers that comply with OSLC Core 2.0 requirements MAY continue to identify themselves as OSLC Core 2.0 servers with


-----

Standards Track Work Product

the OSLC-Core-Version: 2.0 headers in the response. [core-51]

If the OSLC-Core-Version header is not present, an OSLC Server MAY return an OSLC 1.0 response. [core-52]OSLC Clients SHOULD supply

the OSLC-Core-Version: 2.0 header (or newer version) in the request to avoid an OSLC 1.0 response. [core-53]

Machine-readable content SHALL have precedence over specification text if any discrepancy is discovered. [core-54] It is worth noting that in
OSLC 2.0 specifications, normative specification text had precedence over machine-readable content, as opposed to this specification.

**4.3 Conformance**

OSLC Servers MUST implement all the mandatory requirements in the normative sections of specification, and SHOULD follow all the
guidelines and recommendations in these specifications. [core-55]

OSLC Servers MAY implement any of the capabilities described in this specification, and if a capability is supported, all of the mandatory

requirements specified in the normative sections of the multi-part specification elaborating the capability MUST be implemented. [core-56]

[OSLC Servers MUST implement the OSLC Core vocabulary as defined in OSLC Core Version 3.0. Part 7: Vocabulary. [core-57]](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/core-vocab.html)

[Part 2 of this document defines the mandatory requirements for the OSLC discovery capability. OSLC Servers SHOULD provide the discovery](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/discovery.html)
capability in order for clients to determine what services are supported by the server and how to access them. OSLC Servers that
implement discovery MUST implement all of the mandatory requirements specified in the normative sections of part 2 of this multi-part
specification. [core-58]

[Part 3 of this document defines the mandatory requirements for the OSLC resource preview capability. OSLC Servers that implement](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/resource-preview.html)
resource preview MUST implement all of the mandatory requirements specified in the normative sections of part 3 of this multi-part
specification. [core-59]

[Part 4 of this document defines the mandatory requirements for the OSLC delegated creation and selection dialog capability. OSLC](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/dialogs.html)
Servers that implement delegated dialogs MUST implement all of the mandatory requirements specified in the normative sections of part 4 of
this multi-part specification. [core-60]

[Part 5 of this document defines the mandatory requirements for the OSLC attachments capability. OSLC Servers that implement](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/attachments.html)
attachments MUST implement all of the mandatory requirements specified in the normative sections of part 5 of this multi-part specification.

[core-61]

[Part 6 of this document defines the mandatory requirements for the OSLC resource shape constraints capability. OSLC Servers SHOULD](https://docs.oasis-open-projects.org/oslc-op/core/v3.0/os/resource-shape.html)
support resource shapes in order to describe OSLC server managed resources, and validate creation and update requests. OSLC Servers
that implement resources shapes MUST implement all of the mandatory requirements specified in the normative sections of part 6 of this
multi-part specification. [core-62]

All conformance clauses are summarized in the following table.




|Clause Number|Requirement|
|---|---|
|core-1|Constraints on OSLC Core and Domain resources SHOULD be described using OSLC Core Version 3.0. Part 6: Resource Shape which is included as part of the OSLC Core multi-part specifications. Servers MAY use other constraint languages such as [SHACL] to define resource constraints.|
|core-2|OSLC Domain specifications SHOULD use the following URI pattern when publishing each individual resource shape:|
|core-3|To allow different versions of individual shapes to be reused in different versions of a domain specification while still allowing a client to browse the set of possible shapes, domains SHOULD provide an resource for all the shapes for a spec version, at a URI defined by the following pattern: http://open-services.net/ns/[vocab-short-name]/shapes/[SPEC-version]|
|core-4|OSLC 3.0 servers MAY protect resources with HTTP Basic Authentication. OSLC Services that use HTTP Basic Authentication SHOULD do so only via SSL.|
|core-5|OSLC 3.0 servers SHOULD protect resources with [rfc6749] Authentication utilizing [OpenIDConnect].|
|core-6|OSLC Services MUST support at least one RDF resource serialization format, and SHOULD support as many serialization formats as possible through content negotiation.|


-----

Standards Track Work Product



|Clause Number|Requirement|
|---|---|
|core-7|OSLC Services SHOULD provide and accept RDF documents in Turtle format (identified by the MIME-type 'text/turtle') and in JSON-LD format (identified by the MIME-type 'application/ld+json') representations for each OSLC resource for compatibility with LDP 1.0.|
|core-8|OSLC Services SHOULD provide and accept RDF/XML representations for each OSLC resource to preserve compatibility with [OSLCCore2].|
|core-9|OSLC Services MAY provide and accept existing standard or emerging standard formats such as XML, HTML, and the Atom Syndication Format.|
|core-10|OSLC servers SHOULD support the Accept header and whenever possible, respond with one of the content types requested by the client. When the Accept header requests an unsupported RDF serialization, the OSLC server SHOULD return an RDF serialization format that it does support, indicating what it is in the Content-Type header. If the server gets an Accept header for some non-RDF content type, say ATOM, that it does not support, then it SHOULD return 406 Unacceptable.|
|core-11|OSLC servers SHOULD support the CORS protocol [CORS] in order to allow browser-based OSLC clients to interact with the server.|
|core-12|OSLC servers SHOULD use the Access-Control-Allow-Headers header [CORS] to allow the use of the Content-Type header in OSLC requests. Despite the Content-Type header being a CORS-safelisted request header, it needs to be explicitly allowed in order to expand the range of its permitted values and allow OSLC clients to send RDF contents to the server.|
|core-13|OSLC servers SHOULD use the Access-Control-Allow-Headers header [CORS] to allow the use of the OSLC-Core- Version header in OSLC requests.|
|core-14|OSLC Servers MUST implement standard HTTP protocols and MUST at least support GET requests that respond with resources in some RDF serialization format.|
|core-15|OSLC Services use HTTP for create, retrieve, update and delete operations on resources. OSLC Services MUST comply with the HTTP specification [HTTP11].|
|core-16|Because the update process may involve first getting a resource, modifying it and then later putting it back to the server, there is the possibility of a conflict, e.g. some other client may have have updated the resource since the GET. To mitigate this problem, OSLC Services SHOULD use the HTTP If-Match header on a PUT request:|
|core-17|If the HTTP If-Match header is missing OSLC Services SHOULD return HTTP Bad Request (400) status code to indicate that the header is required.|
|core-18|If the HTTP If-Match header is present OSLC Services MUST behave as described in the HTTP specification, returning an HTTP Precondition Failed (412) error to indicate that the header does not match.|
|core-19|If the HTTP If-Match header is present and it matches, but there is some other problem or conflict with the update then OSLC Services MAY return an HTTP Conflict (409) to indicate that problem.|
|core-20|An OSLC Service SHOULD preserve property values that are not part of the resource definition or Resource Shape known by the server (unknown property values). An OSLC Service MUST return a 4xx status code if it decides not to persist any of the unknown property values (in accordance with the LDP specification §4.2.4.4).|
|core-21|An OSLC Client MUST preserve any unknown property values between requests to the OSLC Services for all HTTP verbs except PATCH (in accordance with the LDP specification §4.3.1.11).|
|core-22|OSLC Services MAY support a technique called Selective Properties to enable clients to retrieve only selected property values.|
|core-23|An OSLC Server SHOULD support the following PrefixDefinitions: dcterms: <http://purl.org/dc/terms/> foaf: <http://xmlns.com/foaf/0.1/> owl: <http://www.w3.org/2002/07/owl#> rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> xsd: <http://www.w3.org/2001/XMLSchema#> rdfs: <http://www.w3.org/2000/01/rdf-schema#> ldp: <http://www.w3.org/ns/ldp#> oslc: <http://open-services.net/ns/core#> trs: <http://open-services.net/ns/core/trs#>|


-----

Standards Track Work Product

|Clause Number|Requirement|
|---|---|
|core-24|OSLC Servers MAY support a Query Capability as defined in [OSLCQuery] to enable clients to perform selection and projection operations in order to retrieve a selected subset of resources and property values from an LDPC.|
|core-25|When responding to an HTTP HEAD request, according to [HTTP11] the server SHOULD include an HTTP Content- Length header that indicates the size of the resource as the "decimal number of octets."|
|core-26|Implementations MAY use the HTTP response code 410 (Expired) to indicate to clients that the link they requested has expired.|
|core-27|Resource representations returned via Resource Paging MUST include a resource of type oslc:ResponseInfo, as defined in part 7 of this multi-part specification: Vocabulary.|
|core-28|The subject resource URI of the oslc:ResponseInfo resource representation MUST be the HTTP request URI or the URI from subsequent redirects. The response representation MAY also include properties from subject resources different from the one identified by the request URI.|
|core-29|When responding to a request that includes oslc.pageSize in the URI, a server MAY divide the response into a number of pages and use the value as a hint about the maximum number of RDF statements to be included in each page. Servers MAY return pages containing more or fewer RDF statements than specified.|
|core-30|OSLC Services MAY support [LDPPaging] to enable clients to retrieve large LDP resources (LDPRs) a page at a time.|
|core-31|OSLC Services SHOULD support OSLC paging as described in this section to ensure compatibility with OSLC 2.0 server implementations.|
|core-32|To request a paged version of a resource, a client MUST add at least one "key=value" pair to the query component of the resource URI: Either oslc.paging=true, or oslc.pageSize, or both.|
|core-33|When responding to a request that includes oslc.paging=true in the URI, a server MAY return a representation that contains a subset of the resource's property values.|
|core-34|When responding to a request that includes oslc.pageSize in the URI, a server SHOULD return a representation that contains the requested number of property values.|
|core-35|When Resource Paging is used, the values of a multi-valued property MAY be split across resource pages.|
|core-36|When Resource Paging is used, each property value MUST be represented in its entirety and not split across multiple partial resource pages.|
|core-37|When a page is returned and it is NOT the last page in the sequence, then it SHOULD include an oslc:ResponseInfo (see above), which contains a resource-valued property oslc:nextPage that links to a resource that represents the next page of property-values.|
|core-38|When paging is unstable, by the time a client follows an oslc:nextPage link there may no longer be a next page, in this case the server MAY respond with an HTTP 404 Page Not Found status code.|
|core-39|When a client requests a resource that an OSLC Service considers to be too large to return in one response and the client has not indicated that it desires paging (via oslc.paging or oslc.pageSize), the OSLC Service MAY redirect the client to a representation that contains partial information about the resource.|
|core-40|When the OSLC Service opts to redirect the client to a partial representation, it MUST return an HTTP Status 302 redirect to a URL that includes either oslc.paging, or oslc.pageSize, or both.|
|core-41|OSLC Servers MAY support a Tracked Resources Set capability as defined in [OSLCTRS3] to enable OSLC data consumers and providers flexible ways of sharing information.|
|core-42|OSLC Clients and Servers MAY support a Configuration Management capability as defined in [OSLCCCM1].|
|core-43|OSLC Clients and Servers SHOULD use the OSLC-Core-Version header to indicate what OSLC version they expect or support.|
|core-44|When returning an RDF response, an OSLC Server MUST return the OSLC-Core-Version header set to the Core specification with which the representation complies.|


-----

Standards Track Work Product





|Clause Number|Requirement|
|---|---|
|core-45|The OSLC-Core-Version header consists of a major and minor version components and MUST conform to the following ABNF grammar [ABNF]: SP = " " HTAB = %x09 WSP = SP / HTAB DIGIT = %x30-39 header = oslc-version MAJOR = 1*DIGIT MINOR = 1*DIGIT oslc-version = "OSLC-Core-Version:" *WSP MAJOR "." MINOR|
|core-46|The major version component in the OSLC-Core-Version header MUST be greater or equal to "2".|
|core-47|An OSLC Server SHOULD reject a request with the OSLC-Core-Version header that has a major version value below "2" with a response 400 Bad Request.|
|core-48|If the OSLC-Core-Version header is present in the request and set to a version that an OSLC Server can support, then the Server MUST return a representation that is complies with the specified version.|
|core-49|If the OSLC-Core-Version header is present and indicates a specification version that the Server cannot support, the Server SHOULD respond with what it determines is the most compatible version that it can return; however, the server MAY reject the request with 400 Bad Request.|
|core-50|If the OSLC-Core-Version header is not present then the Server SHOULD respond by returning a resource that conforms to the earliest or most compatible (as determined by the implementation) specification version's representation.|
|core-51|OSLC Core 3.0 Servers that comply with OSLC Core 2.0 requirements MAY continue to identify themselves as OSLC Core 2.0 servers with the OSLC-Core-Version: 2.0 headers in the response.|
|core-52|If the OSLC-Core-Version header is not present, an OSLC Server MAY return an OSLC 1.0 response.|
|core-53|OSLC Clients SHOULD supply the OSLC-Core-Version: 2.0 header (or newer version) in the request to avoid an OSLC 1.0 response.|
|core-54|Machine-readable content SHALL have precedence over specification text if any discrepancy is discovered.|
|core-55|OSLC Servers MUST implement all the mandatory requirements in the normative sections of specification, and SHOULD follow all the guidelines and recommendations in these specifications.|
|core-56|OSLC Servers MAY implement any of the capabilities described in this specification, and if a capability is supported, all of the mandatory requirements specified in the normative sections of the multi-part specification elaborating the capability MUST be implemented.|
|core-57|OSLC Servers MUST implement the OSLC Core vocabulary as defined in OSLC Core Version 3.0. Part 7: Vocabulary.|
|core-58|Part 2 of this document defines the mandatory requirements for the OSLC discovery capability. OSLC Servers SHOULD provide the discovery capability in order for clients to determine what services are supported by the server and how to access them. OSLC Servers that implement discovery MUST implement all of the mandatory requirements specified in the normative sections of part 2 of this multi-part specification.|
|core-59|Part 3 of this document defines the mandatory requirements for the OSLC resource preview capability. OSLC Servers that implement resource preview MUST implement all of the mandatory requirements specified in the normative sections of part 3 of this multi-part specification.|
|core-60|Part 4 of this document defines the mandatory requirements for the OSLC delegated creation and selection dialog capability. OSLC Servers that implement delegated dialogs MUST implement all of the mandatory requirements specified in the normative sections of part 4 of this multi-part specification.|
|core-61|Part 5 of this document defines the mandatory requirements for the OSLC attachments capability. OSLC Servers that implement attachments MUST implement all of the mandatory requirements specified in the normative sections of part 5 of this multi-part specification.|
|core-62|Part 6 of this document defines the mandatory requirements for the OSLC resource shape constraints capability. OSLC Servers SHOULD support resource shapes in order to describe OSLC server managed resources, and validate creation and update requests. OSLC Servers that implement resources shapes MUST implement all of the mandatory requirements specified in the normative sections of part 6 of this multi-part specification.|


**4.4 Acknowledgements**

_This section is non-normative._


-----

Standards Track Work Product

The following individuals have participated in the creation of this specification and are gratefully acknowledged:

**Participants:**

James Amsden, IBM (Chair)
Nick Crossley, IBM
Jad El-khoury, KTH Royal Institute of Technology
Ian Green, IBM
David Honey, IBM
Jean-Luc Johnson, Airbus Group SAS
Harish Krishnaswamy, Software AG, Inc.
Arnaud LeHors, IBM
Sam Padget, IBM
Martin Pain, IBM
Arthur Ryman, IBM
Martin Sarabura, PTC (Chair)
Steve Speicher, IBM

**4.5 Change History**

_This section is non-normative._






|Revision|Date|Editor|Changes Made|
|---|---|---|---|
|CSD03|31 May 2018|Jim Amsden|Added predefined prefixes for common namespaces. Relaxed RDF serialization format requirements. Added normative references to OSLC Query, TRS and Configuration Management specifications.|
|PSD04|20 December 2019|Jim Amsden|Added conformance section and migrated to Open Project|
|PS01|17 September 2020|Jim Amsden|Added vocabulary and constraints documents to additional content. Recommendations on URI patterns for published shapes now includes fragments. See Milestone Core v3.0 PS 01 for additional information.|


-----

