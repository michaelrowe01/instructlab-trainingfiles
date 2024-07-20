META:TOPICINFO{author="michaelrowe" date="1699549805" format="1.1"
version="1.83"} META:TOPICPARENT{name="WebHome"}

# Administering DKGRAY Section technical leaders and senior editors: Main.RalphSchoon, Main.TimFeeney, Main.PatrickRemington, Main.RichRakich [administering-dkgray-section-technical-leaders-and-senior-editors-main.ralphschoon-main.timfeeney-main.patrickremington-main.richrakich]

ENDCOLOR

Properly configuring and tuning the components of a Rational solution is
critical. The following sub-sections cover some of the issues and
concerns and provide guidance and best practice for configuring and
tuning a Rational solution.

For instructions on performing the basic installation and configuration
of the components of a Rational solution, see the relevant [knowledge
center](InformationCenter) documentation. This content is intended to
supplement and extend this basic documentation.

Tuning a Rational solution for optimal performance or other
non-functional requirements is challenging. User loads and usage
patterns are always changing, and the constant change affects how you
should tune your environment. In other words, you are dealing with a
moving target. You want to tune your environment to work efficiently for
the majority of the workload profiles that your solution will support.
For basic information to keep in mind when you tune your Rational
environment, see the [tuning general
guidance](https://jazz.net/wiki/bin/view/Deployment/TuningGeneralGuidance).

### Application servers

-    [WebSphere Application Server (WAS)](ConfiguringAndTuningWAS)
    -    [General WAS top tuning
        recommendations](WASTopTuningRecommendations)
-    [IBM HTTP Server
    (IHS)](https://jazz.net/wiki/bin/view/Deployment/ConfiguringAndTuningIBMHTTPServer)

### Databases

-    [Understanding Collaborative Lifecycle Management tuning settings
    for database connections](https://jazz.net/library/article/1484)
-    [Database general guidance](ConfiguringAndTuningDBGeneral)
-    [DB2](ConfiguringAndTuningDB2)
-    [Oracle](ConfiguringAndTuningOracle)
    -   [Performance Tuning Guide for Data Collection Component on
        Oracle DB](PerformanceTuningGuideForDCConOracle)

### Applications

-   [Jazz Team Server (JTS)](ConfiguringAndTuningTheJTS)
-   [Rational Team Concert(RTC)](ConfiguringAndTuningRTC)
-   [DOORS Next Generation (DNG)](ConfiguringAndTuningDNG)
-   [Rational Quality Manager (RQM)](ConfiguringAndTuningRQM)
-   [Java Virtual Machine (JVM)](ConfiguringAndTuningTheJVM)
-   [Data Collection Component (DCC)](ConfiguringAndTuningDCC)
-   [Lifecycle Query Engine](LifecycleQueryEngineBestPractices)

### Tool usage

\* [User Administration Landing Page](UserAdministration) - [Story
138789](https://jazz.net/jazz02/web/projects/Deployment20Wiki#action=com.ibm.team.workitem.viewWorkItem&id=138789)

\* [Setting up Projects Landing Page](SetupProjects) - [Story
138341](https://jazz.net/jazz02/web/projects/Deployment20Wiki#action=com.ibm.team.workitem.viewWorkItem&id=138341)

\* [Enacting your process with Rational Team Concert landing
page](EnactProcess) - [Story
92244](https://jazz.net/jazz02/web/projects/Deployment20Wiki#action=com.ibm.team.workitem.viewWorkItem&id=92244)

### Other considerations

\* [Lightweight Directory Access Protocol
(LDAP)](ConfiguringAndTuningLDAP) - [Work item
84266](https://jazz.net/jazz02/web/projects/Deployment20Wiki#action=com.ibm.team.workitem.viewWorkItem&id=84266)
\* [Configure CLM on Websphere Application Server with
LDAP](ConfigureCLMOnWASWithLDAP) \* [Configure LDAP for Websphere
Liberty Profile](ConfigureLDAPforLibertyProfile) \* [Extending and
customizing Jazz solutions](JazzAPI) \* [Proxy server installation
landing page](InstallProxyServers) - includes basic configuring and
tuning guidance \* [Administrative utilities, tools, and
scripts](AdminToolsScripts) - Jazz administrative utilities, tools, and
scripts \* [Listing project area membership in Rational Team Concert and
Rational Quality Manager](ListingProjectAreaMembershipinRTCRQM)

META:TOPICMOVED{by="sbeard" date="1422035662"
from="Deployment.DeploymentConfiguringAndTuning"
to="Deployment.DeploymentAdminstering"}
