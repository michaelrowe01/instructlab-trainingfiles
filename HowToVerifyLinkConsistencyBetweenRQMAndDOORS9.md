META:TOPICINFO{author="sbagot" date="1432736805" format="1.1"
version="1.6"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandDOORS"}

# How to verify link consistency between RQM and DOORS 9 DKGRAY Authors: Main.MaeveOReilly Main.SudarshanRao [how-to-verify-link-consistency-between-rqm-and-doors-9-dkgray-authors-main.maeveoreilly-main.sudarshanrao]

Build basis: IBM Rational Quality Manager 4.x, 5.x and IBM Rational
DOORS 9.x ENDCOLOR

TOC{title="Page contents"}

The link model between IBM Rational DOORS and IBM Rational Quality
Manager (RQM) is based on the concept of two links. For example, for
every link from an RQM Test Case to a DOORS Requirement, there should
also be a link from the DOORS Requirement to the RQM Testcase. This
second link is called the 'backlink'. Not all OSLC integrations are
implemented this way, some use link discovery. However backlinks are the
implementation for DOORS 9 and RQM. See more details in: **Back links
and link discovery**,
<http://www.ibm.com/support/knowledgecenter/SSYQBZ_9.6.0/com.ibm.doors.install.doc/topics/c_backlinks_linkdiscovery.html?lang=en>

For the integration to work correctly and to ensure reporting is
accurate, it is important that two links are always maintained. A
failure to create or delete one **must** result in user action.

## The link is present in RQM but not in DOORS

The locking model of DOORS makes this the most common scenario. The user
in RQM tries to create a link to a requirement in DOORS but it fails as
someone in DOORS has the module open in edit mode. It will give a
message: The changes to the link cannot be saved because the link target
in the Rational DOORS project cannot be updated at this time.

There are three options:

1 **Cancel**: If you **Cancel**, nothing should happen. No link is
created in either application. 1 **Try again**: If you are the one who
has the module open in edit mode in DOORS, close it in DOORS and check
**Try again**. 1 **Save partial changes**: If you continue and **Save
the partial changes**, you have created a link from RQM to DOORS but not
from DOORS to RQM. In DOORS, you could create the link to the RQM object
with a right click, links, new validated by. But also in RQM there is a
way of checking the state of these links. See: **Ability to see back
link status in traceability view**:
<https://jazz.net/downloads/rational-quality-manager/milestones/4.0.1M4?p=news#backlink>.
The missing links are identified and can be fixed by the broken link
icon.

## The link is present in DOORS but not in RQM

This is less common but is seen most often if the RQM test case has been
deleted. It can be corrected manually in DOORS by removing the Test Case
link. Ideally this situation should be avoided by deleting the link to
the requirement before the test case is deleted. Access to deleting the
test case could be restricted to users who know to do this.

It may also occur if the requirement object in DOORS has been copied or
a module containing links to RQM artifacts has been copied.

The attached DXL can check all the validated_by links in a module and
create or delete them as directed by the user. The utility is untested
and available "as is," without technical support. You can post questions
about the utility on the Jazz.net forum, <https://jazz.net/forum>.

-   Screenshot of the Reconcile QM Backlinks utility:

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [Integrate Rational Quality Manager with Rational DOORS using Open
    Services Lifecycle
    Collaboration](https://jazz.net/library/article/1020/)
-   [How to increase the Rational DOORS Web Access logging
    levels](http://www.ibm.com/support/docview.wss?uid=swg21456938)
-   [How to enable logging for DWA Interoperation
    server](http://www.ibm.com/support/docview.wss?uid=swg21397464)
-   [IBM](https://www.ibm.com)

##### Additional contributors: IntegrationsTroubleshootingTeam [additional-contributors-integrationstroubleshootingteam]

META:FILEATTACHMENT{name="reconcileQMBackLinks.zip"
attachment="reconcileQMBackLinks.zip" attr="" comment="Utility to check
the status of validated_by links in DOORS" date="1423233808"
path="reconcileQMBackLinks.zip" size="59103" user="maeveoreilly"
version="1"}
META:FILEATTACHMENT{name="reconcileQMBackLinks_Screenshot.PNG"
attachment="reconcileQMBackLinks_Screenshot.PNG" attr="h"
comment="Screenshot of the Reconcile QM Backlinks utility"
date="1423235105" path="reconcileQMBackLinks_Screenshot.PNG"
size="48535" user="maeveoreilly" version="1"}
