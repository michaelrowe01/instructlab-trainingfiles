META:TOPICINFO{author="sbagot" date="1432737633" format="1.1"
version="1.7"}
META:TOPICPARENT{name="IntegrationTroubleshootingRationalRequirementsComposer"}

# Why can't I finalize the creation of a "Derives" link from Requirements Composer to Rational Design Manager? [why-cant-i-finalize-the-creation-of-a-derives-link-from-requirements-composer-to-rational-design-manager]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: Rational
Requirements Composer 4.0.x, IBM Rational Software Architect Design
Manager 4.0.x ENDCOLOR

TOC{title="Page contents"}

This page describes what to do if you cannot save a "Derives" link you
are creating from IBM Rational Requirements Composer (RRC) to IBM
Rational Software Architect Design Manager (RSA DM).

## Initial assessment

### Symptoms

1 When you try to add a new "Derives" link from (Rational Requirements
Composer) RRC to RSA DM, you receive the error:

In plain text: An error has occurred while processing a server request.
The server returned thie error: 400. If you look at the details, you can
see the following : ID CRRRW7553E A message that was received from the
server indicates an error with no specific handler. Unable to load
/rm/proxy?uri=http3A2F2F2Fdm2Fmodels2F739 status:400 (\[object
Object\])@http://:/rm/web/\_js/?include=I\~&etag=GOBS531L2x6_da&\_proxyURL=2Frm&ss=EFL0c&locale=en_US:2485_6@
http://:/rm/web/\_js/?include=I\~&etag=GOBS531L2x6_en_US&\_proxyURL=2Frm&ss=EFL0c&locale=en-us:6198_13@
<http://:/rm/web/_js/?include=I~&etag=GOBS531L2x6_en-US&_proxyURL=2Frm&ss=EFL0c&locale=en-us:6198>

URL: /rm/proxy?uri=http3A2F2F2Fdm2Fmodels2F739

403 :Permission to perform the operation was denied - OPERATION_DENIED
400

1 When a link is created from an artifact in RRC, the link creation
dialog is not automatically dismissed. The dialog remains instead open
showing **Saving links...** in the background (as shown below).

After manually canceling or clearing the window, refreshing the page
shows that the link was created (as shown below).

### Impact/scope

1 Does the behavior affect all the members of the RSA Design Manager
project area? 1 Does the behavior happen for every type of link or only
the Derives links ?

## Possible causes

1 Not all the **permissions** have been granted to the user who is
trying to add the link. 1 The version of Requirements Composer (RRC) is
4.0.3 and your are facing the known defect: [PI09726: (74723) Create
link dialog does not close when click on OK for Derives
links](http://www.ibm.com/support/docview.wss?uid=swg1PI09726)

## Possible solutions

1 Ask the administrator of the RSA DM project area to verify the
permissions for the **Resource Links** settings for the **role**
assigned to the user(s) who is receiving the error 400. Below is the
view on how the **Permissions'** page of the project area looks like for
the **Resource links** that you can access from
[https://host:port/dm/admin](https://host:port/dm/admin) -\> Active
Project Areas -\> Your project Area -\> Permissions

**NOTE:** As a Administrator, you can customize the message that is
provided to the users by editing the **operation properties** as shown
below:

1 Update your Requirements Composer (RRC) installation to 4.0.4 to get a
fix for the defect: [PI09726: (74723) Create link dialog does not close
when click on OK for Derives
links](http://www.ibm.com/support/docview.wss?uid=swg1PI09726).

## References

##### Related topics: [Integrations Troubleshooting](https://jazz.net/wiki/bin/view/Deployment/IntegrationsTroubleshooting) [related-topics-integrations-troubleshooting]

##### External links: \* [Modifying permissions for Design Management page of the RSA DM infocenter](http://pic.dhe.ibm.com/infocenter/rdmhelp/v4/index.jsp?topic=2Fcom.ibm.dm.admin.doc2Ftopics2Ft_linking_projperm.html) [external-links-modifying-permissions-for-design-management-page-of-the-rsa-dm-infocenter]

-   [PI09726: (74723) Create link dialog does not close when click on OK
    for Derives
    links](http://www.ibm.com/support/docview.wss?uid=swg1PI09726)

##### Additional contributors: Main.FrancoisPanaget [additional-contributors-main.francoispanaget]

META:FILEATTACHMENT{name="ErrorCreatingDerivesLinkFromRMtoDM.jpg"
attachment="ErrorCreatingDerivesLinkFromRMtoDM.jpg" attr="h"
comment="Error Creating Derives Link from RM to DM" date="1398957737"
path="ErrorCreatingDerivesLinkFromRMtoDM.jpg" size="470176"
user="fpanaget" version="2"}
META:FILEATTACHMENT{name="ResourLinkProjectAreaPermissions.jpg"
attachment="ResourLinkProjectAreaPermissions.jpg" attr="h" comment=""
date="1398959666" path="ResourLinkProjectAreaPermissions.jpg"
size="278485" user="fpanaget" version="1"}
META:FILEATTACHMENT{name="ProjectAreaPermissionsMessageCustomization.jpg"
attachment="ProjectAreaPermissionsMessageCustomization.jpg" attr="h"
comment="Project Area Permission operation message customization"
date="1399035294" path="ProjectAreaPermissionsMessageCustomization.jpg"
size="341781" user="fpanaget" version="1"}
META:FILEATTACHMENT{name="SavingLinkHanging.jpg"
attachment="SavingLinkHanging.jpg" attr="h" comment="Saving link hang"
date="1399046163" path="SavingLinkHanging.jpg" size="393020"
user="fpanaget" version="1"}
META:FILEATTACHMENT{name="RefreshShowsLink.jpg"
attachment="RefreshShowsLink.jpg" attr="h" comment="Refreshing the page
allows link to appear" date="1415723437" path="RefreshShowsLink.jpg"
size="48274" user="dmmckinn" version="2"}
