META:TOPICINFO{author="sbeard" date="1436383329" format="1.1"
version="1.7"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# System Requirements for IBM Rational Collaborative Lifecycle Management (CLM) 6.0 DKGRAY ***CLM includes the Rational Team Concert, Rational Quality Manager, and Rational DOORS Next Generation products*** Build basis: CLM 6.0 [system-requirements-for-ibm-rational-collaborative-lifecycle-management-clm-6.0-dkgray-clm-includes-the-rational-team-concert-rational-quality-manager-and-rational-doors-next-generation-products-build-basis-clm-6.0]

TOC{title="Page contents"}

**Always up-to-date system requirement reports can be dynamically
generated using the [Software Product Compatibility Reports (SPCR)
tool](http://www-969.ibm.com/software/reports/compatibility/clarity/index.html).**

This is the list of system requirements for **Collaborative Lifecycle
Management (CLM)** 6.0 incorporating:

-   **Rational Team Concert (RTC)**, **Rational Quality Manager (RQM)**
    and **Rational DOORS Next Generation (RDNG)** products
-   **Jazz Reporting Service (JRS)** including Data Collection Component
    (DCC), Data Warehouse (DW), Lifecycle Query Engine (LQE), Report
    Builder (RB) and ALM Cognos Connector
-   **Jazz Foundation (JAF)**
-   The system requirements are broken down into various components
    including the server-based CLM applications that are deployed on one
    or more servers and various optional tools and clients
-   ***Please Note:*** From CLM 5.0 onward, Rational Requirements
    Composer (RRC) has been renamed to Rational DOORS Next Generation
    (RDNG)

RED **Please Note: New configuration management capabilities are
available in CLM 6.0 and the associated Rational solution for systems
and software engineering (SSE) 6.0, which include RDNG, RQM, RTC and
Rational Rhapsody Design Manager. To activate the configuration
management capabilities, Rational DOORS Next Generation and Rational
Quality Manager require a special, no-cost activation key. Please see
[Enabling configuration management in CLM 6.0
applications](https://jazz.net/servlet/clm-cm/request-key) for more
information.** ENDCOLOR

## CLM system requirements by platform

[Linux](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=8436FFC07A6511E4A5D05AF6B8E6E27F&osPlatforms=Linux&duComponentIds=D005|D007|D006|D008|S002|S009&mandatoryCapIds=30|9|24|35|13|132|42|16|26|40&optionalCapIds=133|135|7|5|12|1|187|19|137|27|4)

[Windows](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=8436FFC07A6511E4A5D05AF6B8E6E27F&osPlatforms=Windows&duComponentIds=D005|D007|D006|D008|S002|S009&mandatoryCapIds=30|9|24|35|13|132|42|16|26|40&optionalCapIds=133|135|7|5|12|1|187|19|137|27|4)

[AIX](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=8436FFC07A6511E4A5D05AF6B8E6E27F&osPlatforms=AIX&duComponentIds=D005|D007|D006|D008|S002|S009&mandatoryCapIds=30|9|24|35|13|132|42|16|26|40&optionalCapIds=133|135|7|5|12|1|187|19|137|27|4)

[z/OS](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=8436FFC07A6511E4A5D05AF6B8E6E27F&osPlatforms=z/OS&duComponentIds=D005|D007|D006|D008|S002|S009&mandatoryCapIds=30|9|24|35|13|132|42|16|26|40&optionalCapIds=133|135|7|5|12|1|187|19|137|27|4)

[IBM
i](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=8436FFC07A6511E4A5D05AF6B8E6E27F&osPlatforms=IBM20i&duComponentIds=D005|D007|D006|D008|S002|S009&mandatoryCapIds=30|9|24|35|13|132|42|16|26|40&optionalCapIds=133|135|7|5|12|1|187|19|137|27|4)

[All
platforms](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=8436FFC07A6511E4A5D05AF6B8E6E27F&osPlatforms=AIX|IBM20i|Linux|Mac20OS|Windows|z/OS&duComponentIds=D005|D007|D006|D008|S002|S009&mandatoryCapIds=30|9|24|35|13|132|42|16|26|40&optionalCapIds=133|135|7|5|12|1|187|19|137|27|4)

## CLM system requirements by component

[RTC](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=5B7106B07BF711E4823A55714FDB4202&osPlatforms=AIX|IBM20i|Linux|Mac20OS|Windows|z/OS&duComponentIds=D005|D004|D002|D003|S001|S006&mandatoryCapIds=30|9|24|35|13|132|42|19|16|26|40&optionalCapIds=133|135|7|5|12|1|242|187|74|136|19|137|27|4|223)

[RQM](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=B440AF90807311E4823A55714FDB4202&osPlatforms=AIX|IBM20i|Linux|Mac20OS|Windows|z/OS&duComponentIds=D002|S001|S003&mandatoryCapIds=30|9|24|35|13|132|42|19|16|26|40&optionalCapIds=133|135|7|5|12|19|137|27|4)

[RDNG](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=DA8F9FE0860D11E49803C6F06C4301C6&osPlatforms=spcrAllValues)

[JRS](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=1415739590414&osPlatforms=AIX|IBM20i|Linux|Windows|z/OS&duComponentIds=D004|S005|S002|S003|S001&mandatoryCapIds=30|9|24|13|25|26&optionalCapIds=5|242|188|19|137)

## Related system requirements

[Rational Software Architect Design Manager
5.0](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=1400472901488&osPlatforms=AIX|Linux|Mac20OS|Solaris|Windows&duComponentIds=D000|S000&mandatoryCapIds=30|9|24|13|132|42|26&optionalCapIds=133|7|19)

[Rational Engineering Lifecycle Manager (RELM)
6.0](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=AE76E920B26F11E4BF417B0BC8E5108A&osPlatforms=AIX|IBM20i|Linux|Windows|z/OS&duComponentIds=D002|S001&mandatoryCapIds=30|9|24|13|25|42|26&optionalCapIds=7|22|20|40)

[Rational Insight
1.1.1](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=1414436063649&osPlatforms=IBM20i|Linux|Windows|z/OS&duComponentIds=D005|D002|D001|S004|S008|S010|S003|S006|S009|S007&mandatoryCapIds=30|9|24|13|25|42|19|26&optionalCapIds=22|1|35)

[Rational Publishing Engine
2.0](http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=1413564938593&osPlatforms=Linux|Windows&duComponentIds=D002|D003|S006|S005|S001|S004|S007&mandatoryCapIds=30|24|13|132|42|26&optionalCapIds=125|22|186|223)

## General notes

RED **Please Note: Starting in CLM 5.0.2, Lifecycle Project
Administration (LPA) is now a component of the Jazz Team Server (JTS).
Prior to 5.0.2, it was a separate application. Because of this change,
some steps of the upgrade procedure have changed. Please see [Migrating
the LPA application from 4.0.x, 5.0 or 5.0.1 to 5.0.2 or
higher](https://jazz.net/wiki/bin/view/Main/LifecycleProjectAdmin#Migrating_the_LPA_application_to).**
ENDCOLOR

For prior release requirements please see the specific articles for each
version listed below:

-   [Rational CLM 5.0, 5.0.1 and 5.0.2](CLMSystemRequirements50)
-   [Rational CLM 4.0.5, 4.0.6 and 4.0.7](CLMSystemRequirements405406)
-   [Rational CLM 4.0.3 and 4.0.4](CLMSystemRequirements403)
-   [Rational CLM 4.0.1 and
    4.0.2](https://jazz.net/library/article/1109)
-   [Rational CLM 4.0](https://jazz.net/library/article/811)
-   [Rational CLM 3.0.1.x](https://jazz.net/library/article/632)

For platform pressures (enhancements and more) please see the [CLM
Platform Plans and Pressures
Dashboard](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.dashboard.viewDashboard&tab=_79).

## Related articles

-   [CLM Sizing Strategy](CLMSizingStrategy)
-   [Standard deployment topologies
    overview](StandardTopologiesOverview)
-   [Enabling configuration management in CLM 6.0
    applications](https://jazz.net/servlet/clm-cm/request-key)
