META:TOPICINFO{author="sahilkmansuri" date="1700821587" format="1.1"
version="1.13"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Recommendations when planning and implementing ELM DOORS Next 7.0.x upgrade project DKGRAY Authors: Main.TimFeeney, Main.DanielMoul, Main.PaulEllis Build basis: DOORS Next 7.x [recommendations-when-planning-and-implementing-elm-doors-next-7.0.x-upgrade-project-dkgray-authors-main.timfeeney-main.danielmoul-main.paulellis-build-basis-doors-next-7.x]

ENDCOLOR

TOC{title="Page contents"}

A major change in DOORS Next between V6.0.x and V7.0.x is the way data
is stored and queried. In our labs we have seen significant improvement
in scale and reliability on V7. We have also observed that there are
database queries that need further optimization (see [support flash
6391660](https://www.ibm.com/support/pages/node/6391660)).

These queries are sensitive to customers' data shape and volume which
can impact DOORS Next upgrade time as well as runtime performance.

## Recommended Path

Therefore we recommend the following:

-   Contact IBM Support by opening a case and asking for the latest
    information on fixes and open defects, if any, related to DOORS Next
    upgrades to V7.
-   Upgrade to V7.0.2 if possible rather than an earlier V7.0.x release,
    since there are optimizations V7.0.2 (and later releases) that
    cannot be backported to 7.0 or 7.0.1.
-   Apply the latest iFixes for your ELM applications.
-   With production-like data, ideally a recent production clone, test
    "day in the life", business critical scenarios that are part of a
    typical project lifecycle for your users. Be sure to include the
    scenarios outlined below. This should be done as part of a
    production readiness assessment before proceeding with a production
    upgrade.
    1.  Perform single-user testing of these scenarios.
    2.  Perform multi-user testing, for example, with five users
        exercising the system at the same time.
    3.  If any functional issues or performance regressions occur while
        running the tests, we recommend gathering the data described in
        [Troubleshooting DOORS Next 6.x to 7.x
        Upgrades](https://jazz.net/wiki/bin/view/Deployment/TroubleshootingDOORSNextUpgrades)
        (in particular the database metrics and ISADC output) and submit
        a case to IBM Support along with the gathered data.

## Scenarios to include in day in the life testing

The following requirements scenarios should be included in your 'day in
the life' testing. We have tested these scenarios ourselves with the
data shapes and volumes in our repositories. However, since the
scenarios have proven to be sensitive to organizations' particular data
shape and scale, it is important that you validate your usage patterns.
The scenarios assume RED\[a\]ENDCOLOR configuration management is
enabled and RED\[b\]ENDCOLOR your streams require explicit changesets.
If thats not the case, then some of the changeset, deliver and compare
operations below will not apply and should be adjusted accordingly.

From a project area that has extensive history and many changes over
time and within both local and global configuration contexts (as
applicable):

1.  Open your largest modules (under 10000 artifacts per
    [guidelines](RequirementsManagement70Performance#Data_limits_in_7_0))
    with your typical views (both simple and more complex) - from a
    stream, baseline, or changeset context. As applicable, include views
    with filters, columns with custom attributes (especially
    enumerations), traceability links. Repeat similarly from the All
    Artifacts tab, if used. *Simple view: displays a few standard
    attributes and has simple filter. Complex view: displays standard
    and custom attributes, especially enumerations, includes compound
    filters, traceability links.*
2.  Export these views to your common output formats
3.  Open the history of the largest modules
4.  Create a baseline then create a changeset RED\[a\]\[b\]ENDCOLOR and
    import a large set of requirements (e.g. ReqIF, CSV, Doc, as makes
    sense for your environment)
5.  Deliver the imported requirements to the stream
    RED\[a\]\[b\]ENDCOLOR
6.  Compare the stream to the previous baseline, optionally also to
    earlier baselines RED\[a\]ENDCOLOR
7.  Create baseline then compare it to the previous baseline, optionally
    also to earlier baselines.
8.  Deliver changes in the stream to another stream RED\[a\]ENDCOLOR
9.  Create 10 or more of your typical links to requirements artifacts
    (e.g. requirement to requirement, test artifact to requirement, work
    item to requirement) using your typical mechanisms (e.g. link by
    attribute, links panel, links explorer, import, etc.).
10. View those created links to requirements (e.g. requirement to
    requirement, link by attribute, test artifact to requirement, work
    item to requirement) as you typically would view them, e.g. hover
    over links, use links explorer, etc.
11. Generate a[traceability
    report](https://www.ibm.com/support/knowledgecenter/en/SSYMRC_7.0.2/com.ibm.rational.rrm.help.doc/topics/r_report_descriptions.html)document
    from the large module view(both within DOORS Next and from PUB, as
    applicable). This scenario can be inclusive of your typical customer
    deliverables that are created using RM publishing service (as
    opposed to data in LQE).
12. Make note of Link Validity status Pre and Post upgrade (in some
    instances the Link Validity does not display the correct status
    after an upgrade).

RED\[a\]ENDCOLOR configuration management enabled RED\[b\]ENDCOLOR
explicit changesets enabled

##### Related topics: [Interactive Upgrade Guide](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.2/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html), [Understanding DOORS Next Sizings in 6X](UnderstandingDOORSNextSizingsin6X), [Troubleshooting DOORS Next 6.x to 7.x](TroubleshootingDOORSNextUpgrades) [related-topics-interactive-upgrade-guide-understanding-doors-next-sizings-in-6x-troubleshooting-doors-next-6.x-to-7.x]
