META:TOPICINFO{author="sbagot" date="1432736404" format="1.1"
reprev="1.3" version="1.3"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandDOORS"}

# Why is the RQM-Test Report in DOORS not showing my test case and test results? [why-is-the-rqm-test-report-in-doors-not-showing-my-test-case-and-test-results]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: CLM 4.x,
IBM Rational DOORS 9.4 and later as supported ENDCOLOR

TOC{title="Page contents"}

This page covers what to do if you cannot see test cases and test
results in the IBM Rational DOORS Test Report. This is related to the
OSLC based integration from DOORS 9.4 on-wards. It does not cover the
legacy IBM Rational Quality Manager Interface (RQMI) interface of DOORS
9.3 and earlier.

## Initial assessment

Is it working for any objects?

### Symptoms

The report runs but the relevant columns are missing any values. However
the object is associated with a test case which itself is associated
with test case execution records.

### Impact

This impacts all users.

## Possible causes and solutions

-   The Test Report will only function where Object Text exists. Add
    text in DOORS and run it again.
-   The Test Case Execution Record must be associated with the Test
    Plan.

##### Related topics: [Deployment web home](https://jazz.net/wiki/bin/view/Deployment/WebHome), [Integrations Troubleshooting](https://jazz.net/wiki/bin/view/Deployment/IntegrationsTroubleshooting) [related-topics-deployment-web-home-integrations-troubleshooting]

##### External links: \* [Integrate Rational Quality Manager with Rational DOORS using Open Services Lifecycle Collaboration](https://jazz.net/library/article/1020/) [external-links-integrate-rational-quality-manager-with-rational-doors-using-open-services-lifecycle-collaboration]

-   [How to increase the Rational DOORS Web Access logging
    levels](http://www.ibm.com/support/docview.wss?uid=swg21456938)
-   [How to enable logging for DWA Interoperation
    server](http://www.ibm.com/support/docview.wss?uid=swg21397464)
-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.MaeveOReilly [additional-contributors-main.maeveoreilly]
