META:TOPICINFO{author="jruehlin" date="1699473929" format="1.1"
reprev="1.33" version="1.33"}
META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Inside Jazz Licensing [inside-jazz-licensing]

DKGRAY Authors: Main.MichaelTabb, Main.JimRuehlin Build basis: IBM
Engineering Lifecycle Management (ELM) release 7.x and later ENDCOLOR

TOC{title="Page contents"}

This topic covers how the Jazz licensing subsytem works. It explains the
various license types that the server supports as well as some
interesting features that may impact users and admins alike.

## User roles and client access licenses

Each user is assigned roles based on team and/or project membership. For
example, there could be roles to read/write work items, perform source
code management (SCM) operations, etc. Each one of these roles is mapped
to an operation ID that is defined in a client access license (CAL). If
the user has the role, it does not mean they can perform that action
yet. The user must be assigned a CAL in order to enable the role. There
are 3 types of licenses that the Jazz server supports:

1 Perpetual 1 Term (via Tokens)

Each license type can be deployed as: 1 Authorized 1 Floating

## Capabilities

Licenses are designed to allow for overlapping capabilites while
maintaining an exlcusive set of its own capabilities. For example, an
Engineering Workflow Management (EWM) Developer license may provide SCM
capabilities as well as some work item read/write access. Meanwhile, an
Engineering Test Management (ETM) Professional license may provide some
test case authoring capabilities as well as some work item read/write
access. There is an intersection between the two licenses at the work
item read and write access. If a user was performing a work item read
operation, either of these licenses could be used to satisfy the
assertion request. The following figure illustrates the overlapping
capabilities of some sample product licenses:

ATTACHURL/Overlapping.png

Some licenses are perfect subsets of each other. This means that one
license contains exactly the same operations as another and additionally
unlocks some other capabilities. An example of this is the EWM Developer
license. The Developer license contains exactly the same operations as
the EWM Contributor license, but also provides additional capabilities.
For this reason, the Contributor license is considered a perfect subset
of the Developer license.

ATTACHURL/Subset.png

## License assertion

A license assertion is a check by the client to make sure a user has a
license to perform an operation. Different actions a user performs in an
application may result in the checking of a license for that action.
That action gets translated to an operation ID, as defined above. All
licensing assertions occur on Jazz Team Server (JTS). The applications
send the assertion requests to Jazz Team Server. In other words, all
license management is done on Jazz Team Server. In the illustration
below, a user may be performing an SCM action. That action will require
the user to have a license, so the following steps occur for a license
assertion:

1 The user on an EWM client performs an SCM action. The EWMt client code
requires a license for the action. It makes a call to the server to
perform the check 1 The license service on the server handles this
request, and performs the check. If the check fails, a
LicenseNotGrantedException is thrown, and the client receives the error
and is responsible for propogating it to the user.

ATTACHURL/Simple-license-flow.png

## Perpetual licenses

A Perpetual license does not expire. Perpetual licenses include
Authorized and Floating licenses.

## Term licenses

A Term license is good for a fixed time. After that time it will no
longer allow access to any ELM operations. Term licenses include
Authorized and Floating licenses, and they can be managed with Tokens.

## Authorized licenses

If assigned, a single user (and only that user) will always have this
license to perform the operations that are unlocked by it. The only way
a user will not be able to use this license is if it unassigned from the
user.

## Floating licenses

The floating license requires an additional step on top of the simple
license flow because it requires that the license be checked out. Unlike
an Authorized CAL, a single user is not assigned to the license. A
floating license is part of a pool of licenses and are provided to users
when requested (the request is handled by JTS and no user action is
required beyond accessing the normal ELM operations). If no licenses are
left in the pool the request for the license fails and the user
requesting the license cannot perform ELM operations. Floating licenses
are returned to the pool for use by others when a user logs off or is
inactive for a period of time. There is a difference between a license
assignment and a license checkout. An assignment is nothing more than a
record which is persisted that associates a license to a user. This does
not guarantee a license will be available when the user attempts to use
the product. A checkout occurs when the user which has an assignment
goes to actually use the product in a way that a license is required to
perform an operation. At that point, the license then needs to be
checked out from the license pool.

### Token license server (IBM Common License Server)

Tokens are a way to manage license use. When a term license is assigned,
a set number of tokens are consumed. Licenses can continue to be
assigned or checked out from the floating license pool until no more
tokens are available. Tokens are managed by the IBM Common License
Server.

### Checkout selection

Often a user has more than one floating license assigned to them. When
an operation is asserted by a client, that operation may be able to be
satisfied by more than one of the licenses assigned. This forces Jazz
Team Server to decide which license gets checked out. When there is more
than one, the license service sorts the list using the following
algorithm:

1.  Permanent CALs 2. Existing floating license checkouts (**version
    4.0.3:** non-token first, then token) 3. Subset first 4. Arbitrary

The list is compiled with all of the licenses in the list will be able
to satisfy the operation being asserted. **Note:** The list may contain
permanent CALs.

ATTACHURL/Assertion-sort.png

A breakdown of the ranking:

#### Permanent CALs

A user always has a permanent CAL assigned. No checkout is required.
Floating is limited, and on a shared basis. Using floating over
permanent reduces the amount available for everyone else.

#### Existing floating license checkouts

If the user already has a checkout, use the existing lease; otherwise,
another license has the potential to be checked out. Because of their
associated cost, token licenses are considered after "normal" floating
licenses.

#### Subset first

Floating licenses that are perfect subsets, or the most restrictive
licenses are used first before their more costly superset parents. For
example, the Rational Team Concert (RTC) Contributor license is a
perfect subset of the Rational Team Concert (RTC) Developer license. If
the user has both assigned, the Contributor license will come first in
the list.

#### Arbitrary

Licenses that have mutually exclusive operations and have no subset
licenses available are the last to be selected. For example, this would
happen if you have a Rational Team Concert Developer and a Requirements
Management (RM) Analyst CAL assigned.

### Checkout flow

After the license are sorted and it is determined that the license to
use is a floating license, the checkout process begins. The following
outline shows a flow from the license service that needs to check out a
floating license:

1.  The license service selects the license (floating, in this example)
    needed to satisfy the assertion request
2.  The license service uses its floating license client to determine
    how to get a lease from the floating license server. It does the
    following actions:
    1.  If the client has a reference to a lease for the license being
        checked out, it is placed on an asynch refresh queue, which runs
        peridocally to increase the lease timeout on the floating
        license server
    2.  Otherwise, the client sends a checkout request to the server,
        and if successful, caches the lease information.

ATTACHURL/Floating-license-flow.png

### Floating leases

When a license is successfully checked out from the available pool, a
lease record is persisted in the database which resides on the floating
license server. The lease contains some bits of information such as
user, license, and lease expiration time. With the lease persisted, in
the event of a server restart, the expiration time does not reset.

## Token licenses

Token licenses are built on top of floating CALs. The only difference in
their definition is that there is an associated token cost. The cost
translates to the number of tokens to check out. If two otherwise
equivalent (floating+token, supporting same operation) licenses are
being considered for checkout, the one with the lesser token count will
be selected. The checkout flow follows mostly the same flow as floating
licenses do. After the floating license service realizes that a token
checkout needs to occur, it delegates to the RCL token provider service,
which in turn calls to the FlexLM server to perform this checkout. The
tokens are not managed by Jazz, it is done so externally by a FlexLM
solution that integrates into Jazz. After the tokens are checked out
successfully, a lease is created and persisted in the same way that a
floating lease is persisted. Here is an illustration of a token
checkout:

ATTACHURL/Token-flow.png

### Token Consumption by Role

**Rational Team Concert**

-   Developer 8
-   Developer EP 9
-   Contributor 5
-   Stakeholder 1

**Rational Quality Manager**

-   Quality Professional 10
-   Contributor 5

**Rational Requirements Composer**

-   Analyst 9
-   Contributor 5

[Client Access Management
Overview](https://www.ibm.com/support/knowledgecenter/en/SSYMRC_7.0.1/com.ibm.jazz.repository.web.admin.doc/topics/c_managing_licenses.html)

## Subset/superset assignment - **version 4.0.1**

In version 4.0.1, the restriction to disallow assignment of subset
licenses was removed. Previously, as an example, a user could not have a
Rational Team Concert Contributor and Rational Team Concert Developer
assigned. These were looked at as 2 separate roles. This did not cover
the case where a user had split roles and spent most of their time as a
contributor and a small portion of their time as a developer. This would
force a user to have the more costly developer license. Starting in
version 4.0.1, the system provided more flexibility for this use case,
and allowed the user to have both licenses assigned. There are some
caveats, though. **Note: This applies to floating and token licenses
only.**

-   When a user performs an action that can be done by both the
    Contributor and Developer, the most restrictive or subset license is
    checked out. In this case, the Contributor would be used.
-   If the user performs an action that requires a Developer license and
    currently holds a Contributor license, both licenses are checked out
    and held onto until:
    1.  The user logs out
    2.  The lease expires due to inactivity

The rationale behind this is that users should only perform actions
defined by their assigned license(s) for their role(s). In other words,
if a person ever performs Developer actions, that person needs to be
assigned Developer license, not a Contributor license.

## Compatible license behavior - **version 4.0**

In version 4.0, a new concept to enforce compatiability between
applications and licenses was introduced. Jazz needed a way to prevent
licenses from a previous version of a product to work with a newer
version of a product. To accomplish this, an application can optionally
declare a compatible license version in its SCR document. Meanwhile, the
CAL must also declare what product versions it is compatible with. This
check is performed at run time when compiling a list of available
licenses to use upon a license assertion. A license is considered valid
if the application that is sending the request to assert is in the list
of compatible behaviors in the CAL. The figure below is an illustration
of the pieces that make up the license compatibility feature:

ATTACHURL/License-compatibility.png

##### Related topics: [Deployment planning and design](DeploymentPlanningAndDesign) [related-topics-deployment-planning-and-design]

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="Subset.png" attachment="Subset.png" attr="h"
comment="" date="1361811360" path="Subset.png" size="18330" user="mtabb"
version="1"} META:FILEATTACHMENT{name="License-compatibility.png"
attachment="License-compatibility.png" attr="h" comment=""
date="1361895713" path="License-compatibility.png" size="33687"
user="mtabb" version="1"}
META:FILEATTACHMENT{name="Simple-license-flow.png"
attachment="Simple-license-flow.png" attr="h" comment=""
date="1362589267" path="Simple-license-flow.png" size="41673"
user="mtabb" version="1"} META:FILEATTACHMENT{name="Overlapping.png"
attachment="Overlapping.png" attr="h" comment="" date="1362590174"
path="Overlapping.png" size="26016" user="mtabb" version="1"}
META:FILEATTACHMENT{name="Assertion-sort.png"
attachment="Assertion-sort.png" attr="h" comment="" date="1362780463"
path="Assertion-sort.png" size="66519" user="mtabb" version="1"}
META:FILEATTACHMENT{name="Floating-license-flow.png"
attachment="Floating-license-flow.png" attr="h" comment=""
date="1362781055" path="Floating-license-flow.png" size="47722"
user="mtabb" version="1"} META:FILEATTACHMENT{name="Token-flow.png"
attachment="Token-flow.png" attr="h" comment="" date="1362781388"
path="Token-flow.png" size="25412" user="mtabb" version="1"}
META:TOPICMOVED{by="sbeard" date="1371642705"
from="Deployment.LicensingExplained"
to="Deployment.JazzLicensingExplained"}
