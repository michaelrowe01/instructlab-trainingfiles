META:TOPICINFO{author="rnaranjo" date="1705520221" format="1.1"
version="1.44"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Upgrade Checklist DKGRAY Authors: Main.PaulEllis, Main.JeffreyBabylon Build basis: Release Agnostic. [upgrade-checklist-dkgray-authors-main.paulellis-main.jeffreybabylon-build-basis-release-agnostic.]

ENDCOLOR

TOC{title="Page contents"}

This Quick Checklist is provided for people performing an upgrade of any of the Engineering
Lifecycle Management (ELM) products.
It represents the minimum level of things to consider prior to upgrading,
focusing on the most important information that must be read prior to an
upgrade. The list is intentionally concise and does not attempt to
explain all the details behind each point, but instead provides links to
much more detailed information.

## The Deployment wiki and formal documentation

As you're reading this page, you are already in the deployment wiki. The
cornerstone of our documentation is the Interactive Upgrade Guide. This
allows you to build customized documentation and also includes many of
the known issues which can then be incorporated into your upgrade plan
and upgrade procedures.

If you are planning for your Engineering Lifecycle Management 7.0
upgrade, then please spend some time understanding how to [Get Ready for
IBM Engineering Lifecycle Management
v7.0](https://jazz.net/blog/index.php/2019/12/20/get-ready-for-ibm-engineering-lifecycle-management-v7-0/).

-   [ELM 7.0 Installation and Upgrade
    Notes](https://jazz.net/pub/new-noteworthy/install_upgrade/7.0/index.html)
-   [Interactive Upgrade
    Guide](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html) -
    change the release drop-down for releases other than 7.0
-   [Upgrading to IBM Engineering Lifecycle Management
    7.0](https://jazz.net/downloads/elm/releases/7.0?p=upgrading) - new
    overall summary of upgrade for ELM 7.0. As the Interactive Upgrade
    Guide is only updated at release delivery, this document now
    contains all the known additional steps required. It is very much a
    READ ME FIRST document.

However, if you entered the wiki here then please be aware of the main
sections which are useful to a successful upgrade.

-   [How to plan your upgrade to IBM Engineering Lifecycle Management
    version 7.x versus previous
    versions](https://www.ibm.com/support/pages/node/6156021) technote
    on what IBM Support will need in a conversation on upgrade to ELM
    7.x.
-   [Main Upgrade page of the deployment
    wiki](https://jazz.net/wiki/bin/view/Deployment/DeploymentInstallingUpgradingAndMigrating)
-   [Late breaking Upgrade
    information](https://jazz.net/wiki/bin/view/Deployment/UpgradeInsider)
-   [Planning and
    Design](https://jazz.net/wiki/bin/view/Deployment/DeploymentPlanningAndDesign) -
    in particular, sizing and performance metrics to guide you on what
    to expect from your upgraded system.
-   [Upgrading IBM Engineering Lifecycle Management - IBM Knowledge
    Center](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.3/com.ibm.jazz.install.doc/topics/c_upgrade_overview.html)
-   [Repotools Verify
    command](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.3/com.ibm.jazz.install.doc/topics/r_repotools_verify.html).
    Run this a week prior to the upgrade to ensure time to correct data
    issues & run again as part of your procedure and ensure nothing new.
-   [ Repotools Verify command - additional
    guidance](https://jazz.net/wiki/bin/view/Deployment/DeploymentTroubleshootingVerifyCommand).
    An explanation of common error messages

### Detailed Upgrade Planning

[Upgrade
Planning](https://jazz.net/wiki/bin/view/Deployment/UpgradePlanning),
this article is the summation of 5 years of conference presentations
regarding how to approach the upgrade of ELM. It is also
release-agnostic and details the lifecycle and best practice when you
upgrade. [Knowledge Center guide for Deployment and upgrade planning for
IBM Engineering Lifecycle
Management](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.3/com.ibm.jazz.install.doc/topics/c_planning_upgrade.html)

### Upgrade Testing

-   Did you test with your current production data?
-   [Setting up a Staging/Test
    Environment](https://www.ibm.com/support/knowledgecenter/SSYMRC_7.0.3/com.ibm.jazz.install.doc/topics/t_prepare_staging_env.html)

### Software and Licenses

-   [Passport
    Advantage](https://www-112.ibm.com/software/howtobuy/softwareandservices/registration/Registration?caller=PAC)
-   [Fix Central for the latest
    ifixes](https://www-945.ibm.com/support/fixcentral/) - also
    available from jazz.net [All Downloads - Interim
    Fixes](https://jazz.net/downloads/elm/releases/7.0?p=allDownloads)
-   Custom fixes specific to your environment. Were you sent a testfix
    for something unique? Fixes are generally rolled into an ifix, but
    for upgrades from older releases it is worth checking.

After you install the new version 7.0 applications, ensure to apply the
latest interim fix to your installation before you continue with the
upgrade. This ensures that your new version 7.0 applications are
up-to-date. To check if there are any interim fixes available for your
product, visit Fix Central on IBM Support Portal page.

### Server, Infrastructure and Performance Considerations

-   [System Requirements for the IBM Engineering Lifecycle Management
    (ELM)
    v7.0.1](https://jazz.net/wiki/bin/view/Deployment/ELMSystemRequirements701).
    For older releases see the main [Install and Upgrade
    page](https://jazz.net/wiki/bin/view/Deployment/DeploymentInstallingUpgradingAndMigrating).
-   [Sizing Strategy minimum specifications for CLM 6.0 (RTC, RDNG,
    RQM)](https://jazz.net/wiki/bin/view/Deployment/CLMSizingStrategy60)
-   [Sizing Strategy minimum specifications for pre-6.0 (RTC, RQM, RDNG,
    LQE)](https://jazz.net/wiki/bin/view/Deployment/CLMSizingStrategy#Minimum_requirements_and_practic)
-   [Performance datasheets per product, scenario and
    release](https://jazz.net/wiki/bin/view/Deployment/PerformanceDatasheetsAndSizingGuidelines).
    These are designed for enterprise administrators who need to know
    how to push well passed the minimum requirements.

### Latest Upgrade Flashes and News for Continuous Engineering products:

-   [News across all of the Collaborative Lifecycle Management
    products](https://www.ibm.com/support/entry/myportal/alerts/rational/rational_collaborative_lifecycle_management)
-   [Engineering Workflow Management specific flashes and
    news](https://www.ibm.com/support/pages/ibmsearch?q=&tc=SSUC3U&dc=D600+DB600&sortby=desc&dtm)
-   [Engineering Test Management flashes and
    news](https://www.ibm.com/support/pages/ibmsearch?q=&tc=SSUVV6&dc=D600+DB600&sortby=desc&dtm)
-   [Engineering Requirements Management DOORS Next flashes and
    news](https://www.ibm.com/support/pages/ibmsearch?q=&tc=SSUVLZ&dc=D600+DB600&sortby=desc&dtm)
-   [Rational DOORS specific flashes and
    news](https://www.ibm.com/support/entry/myportal/alerts/rational/rational_doors)
-   [Rhapsody Family, including Design Manager, specific flashes and
    news](https://www.ibm.com/support/entry/myportal/alerts/rational/rational_rhapsody_family)
-   [RELM specific flashes and
    news](https://www.ibm.com/support/entry/myportal/alerts/rational/rational_engineering_lifecycle_manager)

Product Pages

-   [Engineering Workflow
    Management](https://www.ibm.com/mysupport/s/topic/0TO50000000IVrQGAW/engineering-workflow-management?language=en_US&productId=01t50000004ufns)
-   [Engineering Test
    Management](https://www.ibm.com/mysupport/s/topic/0TO50000000IVrVGAW/engineering-test-management?language=en_US&productId=01t50000004ufnx)
-   [Engineering Requirements Management DOORS
    Next](https://www.ibm.com/mysupport/s/topic/0TO50000000IVraGAG/engineering-requirements-management-doors-next?language=en_US&productId=01t50000004ufo2)

If your product is not listed above, then you can use the **Product
Finder** field within [Continuous Engineering
Products](https://www.ibm.com/support/entry/myportal/support?brandind=rational).
Also note that the following are components of CLM and therefore do not
have their own alerts page. For Data Collection Component(DCC), Jazz
Reporting Service(JRS), Lifecycle Query Engine(LQE), see the [CLM
page](https://www.ibm.com/support/entry/myportal/alerts/rational/rational_collaborative_lifecycle_management)
above.

### Let us help

-   Contact your Technical Sales Representative or Accelerated Value
    Program(AVP), Representative
-   [Open a Service
    Request](https://www.ibm.com/support/servicerequest/Home.action)
    (also known as Problem Management Record (PMR)) with Technical
    Support for upgrade planning and support
-   [The jazz.net forum](https://jazz.net/forum/), which is ideal for
    those questions where crowd sourcing your peers for their experience
    is the preferred outcome.
-   [Links to all CLM technotes and other
    documentation](https://www.ibm.com/support/entry/myportal/all_troubleshooting_links/rational/rational_collaborative_lifecycle_management?productContext=-970758469) -
    non Upgrade specific. Simply add "upgrade" to the Search window to
    filter.

### Additional pertinent information

This section explicitly highlights issues which even after reading this
document could be missed in the various links. CLM 6.0.5/6.0.6:

-   [repotools -createTables command fails with ORA-01000 on Oracle
    12](http://www.ibm.com/support/docview.wss?uid=swg21990430)

CLM 6.0.4:

-   [Clicking the context menu results in no action when DOORS Next
    Generation is deployed with IBM HTTP
    Server](http://www.ibm.com/support/docview.wss?uid=swg22006305)
-   [Potential performance issues after upgrading to IBM Rational DOORS
    Next Generation 6.0.4 or 6.0.4
    iFix001](http://www.ibm.com/support/docview.wss?uid=swg22006095)

<!-- -->

-   [Post upgrade performance issues when moving to SQL Server
    2014](http://www.ibm.com/support/docview.wss?uid=swg22000848)
-   [DNG 6.x: SQL Server errors when RDNG optimization
    applied](http://www.ibm.com/support/docview.wss?uid=swg21980867)
-   [DNG 6.x: Oracle and SQL upgrade performance
    considerations](http://www.ibm.com/support/docview.wss?uid=swg21975746)
-   [DNG graphical artifacts are read-only after upgrading to 6.0.2 ifix
    4 or later](http://www.ibm.com/support/docview.wss?uid=swg21993072).
    Artifacts in 6.0.3 will be read-only. Don't upgrade to 6.0.3 if you
    need to edit graphical artifacts.

General:

-   Increase the size of your [repotools memory
    allocation](https://jazz.net/wiki/bin/view/Deployment/CollaborativeLifecycleManagementPerformanceReportRDNG60Migration#Repotools_JVM_heap_size)
-   Ensure you run with updated [database
    statistics](https://jazz.net/wiki/bin/view/Deployment/CollaborativeLifecycleManagementPerformanceReportRDNG60Migration#DatabaseStatistics)
    for RQM and RDNG
-   There were several issues reported with Rational DOORS Generation
    when migrating to 6.0, 6.0.1 and 6.0.2 which merited the [following
    flash](http://www-01.ibm.com/support/docview.wss?uid=swg21984203)

<!-- -->

-   [Known issues when upgrading to Rational Quality Manager
    6.0.2](http://www-01.ibm.com/support/docview.wss?uid=swg21983579)
-   [After upgrading to 6.0, the Requirements Management server is slow
    or times out](https://jazz.net/library/article/1516#00111)
-   [Email Notification may fail after upgrading to CLM
    6.0.3](http://www-01.ibm.com/support/docview.wss?uid=swg22001673)

##### Related topics: [Deployment web home](DeploymentWebHome), [Performance Datasheets and Sizing Guidelines](PerformanceDatasheetsAndSizingGuidelines) [related-topics-deployment-web-home-performance-datasheets-and-sizing-guidelines]

##### External links: [external-links]

-   [IBM](https://www.ibm.com), [Support
    Portal](https://www-947.ibm.com/support/entry/myportal/support?brandind=Rational)

##### Additional contributors: Main.DaleHobil, Main.PaulStrachan, Main.LewCote, Main.HelenHolohan, Main.SteveCoskie, Main.RosaNaranjo [additional-contributors-main.dalehobil-main.paulstrachan-main.lewcote-main.helenholohan-main.stevecoskie-main.rosanaranjo]
