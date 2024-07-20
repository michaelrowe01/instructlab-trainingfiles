META:TOPICINFO{author="michaelrowe" date="1659376532" format="1.1"
version="1.4"} META:TOPICPARENT{name="DeploymentTroubleshooting"}

# Troubleshooting the Jazz Reporting Service DKGRAY Authors: Main.MatthieuLeroux, Main.PhilippeCheavlier, Main.FrancescoChiossi Build basis: Build basis: JRS 6.x and later ENDCOLOR [troubleshooting-the-jazz-reporting-service-dkgray-authors-main.matthieuleroux-main.philippecheavlier-main.francescochiossi-build-basis-build-basis-jrs-6.x-and-later-endcolor]

TOC{title="Page contents"}

This page is the starting point to find information and techniques that
you can use to diagnose and troubleshoot issues related to reporting,
Lifecycle Query Engine (LQE), Data Collection Component (DCC), Report
Builder.

## Where is the issue?

Reporting issue usually involve multiple products, for example when a
report shows the wrong data, is it an issue with the query in Report
builder, is it an issue with the datasource (LQE or DCC), does the
application exposes the right data to LQE or DCC?

### Data Warehouse Datasource

describe here a use case that involves a data warehouse report

### LQE Datasource

describe here a use case that involves an LQE report.

## Additional Log4j traces

Prior to versions 7.0.1 SR1 / 7.0.2 SR2: here are some traces that can
be added in log4j.properties per product

For versions 7.0.1 SR1 / 7.0.2 SR2 and beyond: traces are to be added in
log4j2.xml per product

-   Report Builder

[Report Builder Traces](Report Builder Traces)

-   Lifecycle Query Engine
-   Data Collection Component

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
