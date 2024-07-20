META:TOPICINFO{author="sbeard" date="1377690186" format="1.1"
version="1.26"} META:TOPICPARENT{name="WebHome"}

# Access control for the Deployment wiki [access-control-for-the-deployment-wiki]

DKGRAY Authors: Main.StevenBeard Build basis: None ENDCOLOR

TOC{title="Page contents"}

This topic outlines the different levels of access control to the wiki,
with supporting guidance on when and how to change the levels for
specific topic pages.

## Levels of access control to the Deployment wiki

Read access to the Deployment wiki is unrestricted. You do not even need
to log in with your Jazz.net user ID for full read access, which
facilitates external search engine indexing and search, such as Google.

Three groups are used to control write access to all topic pages:

-   **Technical leaders and senior editors:** This group consists of
    deployment experts that are nominated from customers, IBM Business
    Partners, and Rational. Membership in this group is based on
    nominations submitted for consideration to the community of
    [technical leaders and senior editors](DeploymentLeaders) by using
    the web-based [nomination
    process](DeploymentTechnicalLeadersAndSeniorEditorsNominationProcess).
    This group is enabled by Main.TWikiDeploymentAuthorsGroup for all
    members.

<!-- -->

-   **Deployment practitioners:** This group consists of Deployment
    practitioners that are nominated from customers and IBM Business
    Partners, and members of Rational teams. Membership in this group is
    based on nominations submitted for consideration to the community of
    [technical leaders and senior editors](DeploymentLeaders) by using
    the web-based [nomination
    process](DeploymentPractitionersNominationProcess). Anyone from a
    Rational team can request membership to this group (see [Deployment
    wiki request write access for
    IBMers](DeploymentRequestWriteAccessForIBMers)). This group is
    enabled by a combination of Main.TWikiExternalAuthorsGroup for
    customers and IBM Business Partners, and Main.TWikiAuthorsGroup for
    IBMers.

<!-- -->

-   **Jazz.net users:** All Jazz.net users have write access to open
    community topic pages by using their Jazz.net user ID and password.
    This group is enabled by the Jazz.net users LDAP group.

By default, write access to all wiki pages is restricted to the
Main.TWikiDeploymentAuthorsGroup. Subsequently the community or section
technical leaders and senior editors can open a page for wider write
access to the Deployment practitioners (Main.TWikiAuthorsGroup and
Main.TWikiExternalAuthorsGroup) or Jazz.net users (Jazz.net LDAP group).
The granting of wider write access must occur on a page-by-page basis.

Many topic pages will be created by the technical leaders and senior
editors, and then opened for wider write access to the Deployment
practitioners or Jazz.net users. However, some core pages that contain
fundamental or critical guidance and best practices will be editable
only by the technical leaders and senior editors. It is important to
strike the right balance between core pages that are editable only by
experts to maintain a high quality versus community pages that allow the
full community to contribute. Many of the core pages allow comments and
questions to be raised to enable wider community contribution.

## Changing the level of write access control for a topic page

The color of the title box at the top of each page denotes the level of
write access. This will give a clear visual cue as to who can edit a
page, and the provenance and quality of the guidance on that page. Below
are illustrations of the three title box colors and the verbatim Twiki
mark-up, with access control required for each:

# Technical leaders and senior editors [technical-leaders-and-senior-editors]

DKGRAY Authors: Main.StevenBeard Build basis: None ENDCOLOR

# Technical leaders and senior editors [technical-leaders-and-senior-editors-1]

DKGRAY Authors: Main.StevenBeard Build basis: None ENDCOLOR

# Deployment practitioners [deployment-practitioners]

DKGRAY Authors: Main.StevenBeard Build basis: None ENDCOLOR

# Deployment practitioners [deployment-practitioners-1]

DKGRAY Authors: Main.StevenBeard Build basis: None ENDCOLOR

# Jazz.net users [jazz.net-users]

DKGRAY Authors: Main.StevenBeard Build basis: None ENDCOLOR

# Deployment practitioners [deployment-practitioners-2]

DKGRAY Authors: Main.StevenBeard Build basis: None ENDCOLOR

RED **Note:** ENDCOLOR Be careful when you set the write access for a
topic (ALLOWTOPICCHANGE), because it is very easy to make the wrong
selection and remove write access for yourself and others.

| Write access groups | TWiki/LDAP group | Border color | Background image |
|:---|:---|:---|:---|
| Technical leaders and senior editors | Main.TWikiDeploymentAuthorsGroup | \#FFD28C | WebPreferences/TLASE.jpg |
| Deployment practitioners | Main.TWikiAuthorsGroup and Main.TWikiExternalAuthorsGroup | \#A8CEE4 | WebPreferences/DP.jpg |
| Jazz.net users | Jazz.net LDAP group | \#DFDFDF | WebPreferences/Users.jpg |

## Detailed steps required to gain different levels of write access

### Open community topic page write access for Jazz.net users

For this level of write access, no additional steps are required other
than to register as a Jazz.net user. This level of write access will be
enabled for all existing Jazz.net users and any newly registered
Jazz.net users going forward. You must log in with your Jazz.net
credentials to edit an open community topic page.

\#DeploymentPractitionerIBMers

### Deployment practitioner topic page write access for IBMers

IBMers only need to follow the steps to [Request write access for
IBMers](RequestWriteAccessForIBMers). No additional approval steps are
required, and write access to deployment practitioner topic pages and
membership of the [Deployment wiki project on Rational Team
Concert](https://jazz.net/jazz02/web/projects/Deployment20Wiki#action=com.ibm.team.dashboard.viewDashboard)
should be enabled within a few days.

This user will be added to these groups:

1 The jazzwriter's LDAP group 1 The Main.TWikiUsers list 1 The
Main.TWikiAuthorsGroup 1 The membership of the [Deployment wiki project
on Rational Team
Concert](https://jazz.net/jazz02/web/projects/Deployment20Wiki#action=com.ibm.team.dashboard.viewDashboard)

### Deployment practitioner topic page write access for customers and IBM Business Partners

To request this level of write access, all customers and IBM Business
Partners must follow the deployment practitioner [nomination
process](DeploymentPractitionersNominationProcess). The nomination will
then be approved or rejected by a combination of the IBM sponsor for the
nomination and one of the community [technical leaders and senior
editors](DeploymentLeaders).

If approved, the user is emailed that the nomination was accepted and
that the user is set up for this level of write access.

This user will be added to theses groups:

1 The jazzwriter's LDAP group 1 The Main.TWikiUsers list 1 The
Main.TWikiExternalAuthorsGroup 1 The membership of the [Deployment wiki
project on Rational Team
Concert](https://jazz.net/jazz02/web/projects/Deployment20Wiki#action=com.ibm.team.dashboard.viewDashboard)

### Technical leader and senior editor topic page write access for IBMers

RED **Note:** ENDCOLOR To request this level of write access, IBMers
must first request [Deployment practitioner topic page write
access](#DeploymentPractitionerIBMers).

Then, IBMers must follow the deployment technical leaders and senior
editors [nomination
process](DeploymentTechnicalLeadersAndSeniorEditorsNominationProcess).
The nomination will then be approved or rejected by the full community
[technical leaders and senior editors](DeploymentLeaders).

If approved, the user will be added to the
Main.TWikiDeploymentAuthorsGroup.

### Technical leader and senior editor topic page write access for customers and IBM Business Partners

To request this level of write access, customers and IBM Business
Partners must follow the deployment technical leaders and senior editors
[nomination
process](DeploymentTechnicalLeadersAndSeniorEditorsNominationProcess).
The nomination will then be approved or rejected by a combination of the
IBM sponsor for the nomination and the full community [technical leaders
and senior editors](DeploymentLeaders).

If approved, the user will be emailed that the nomination was accepted
and that the user is set up for this level of write access.

This user will be added to these groups:

1 The jazzwriter's LDAP group 1 The Main.TWikiUsers list 1 The
Main.TWikiExternalAuthorsGroup 1 The Main.TWikiDeploymentAuthorsGroup 1
The membership of the [Deployment wiki project on Rational Team
Concert](https://jazz.net/jazz02/web/projects/Deployment20Wiki#action=com.ibm.team.dashboard.viewDashboard)

##### Related topics: [Deployment Wiki Request Write Access for IBMers](DeploymentRequestWriteAccessForIBMers), [Deployment technical leaders and senior editors nomination process](DeploymentTechnicalLeadersAndSeniorEditorsNominationProcess), [Deployment practitioners nomination process](DeploymentPractitionersNominationProcess) [related-topics-deployment-wiki-request-write-access-for-ibmers-deployment-technical-leaders-and-senior-editors-nomination-process-deployment-practitioners-nomination-process]

##### External links: \* None [external-links-none]

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="access1.png" attachment="access1.png" attr="h"
comment="" date="1365881997" path="access1.png" size="31504"
user="sbeard" version="1"} META:FILEATTACHMENT{name="access2.png"
attachment="access2.png" attr="h" comment="" date="1365882016"
path="access2.png" size="25254" user="sbeard" version="1"}
META:FILEATTACHMENT{name="access3.png" attachment="access3.png" attr="h"
comment="" date="1365882036" path="access3.png" size="20979"
user="sbeard" version="1"}
