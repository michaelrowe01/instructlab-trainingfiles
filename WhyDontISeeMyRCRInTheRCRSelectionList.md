META:TOPICINFO{author="sbagot" date="1432736682" format="1.1"
version="1.5"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandDOORS"}

# Why don't I see my RCR in the RCR selection list? DKGRAY Authors: Main.BindiMandava Build basis: RTC 4.x and later, Rational DOORS 9.4 and later as supported [why-dont-i-see-my-rcr-in-the-rcr-selection-list-dkgray-authors-main.bindimandava-build-basis-rtc-4.x-and-later-rational-doors-9.4-and-later-as-supported]

ENDCOLOR

TOC{title="Page contents"}

This page provides information about what to do if you cannot see the
Requirement Change Request (RCR) in the select default window in IBM
Rational DOORS. Attempts to open the Select Default RCR results in an
empty window when using the IBM Rational DOORS with OSLC interface.

Note: The information below applies to all the Change Management
products (Rational Change, Rational Team Concert, Rational ClearQuest).

## How to select default RCR

In Rational DOORS, when you open the applicable module on the main menu
and select Change Management \> Requirements Change Request \> Select
Default, you will see the Select Default RCR window and the default RCR
that is already selected is highlighted.

## Rational DOORS configured using OSLC Integration

You have Rational DOORS configured using the OSLC Integration and you
have the default RCR assigned to you. While opening a Select Default RCR
window does not display assigned RCR. This window is blank and you
cannot see the RCRs in the list.

These are possible reasons the default RCR is not listed in the Select
Default RCR window:

1.  Make sure the RCR is assigned to the user.
2.  The first time you open a Change Management configured Formal
    Module, the log in window will prompt. Ensure the user name and
    password entered into the log in prompt matches with the Change
    Management log in credentials.
3.  Log into DOORS and navigate to the Defined Configuration Template
    menu.
4.  Select the template and make sure the template is pointing to the
    correct database.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: None [additional-contributors-none]
