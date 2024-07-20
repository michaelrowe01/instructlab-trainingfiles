META:TOPICINFO{author="sbagot" date="1432735276" format="1.1"
version="1.20"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandClearQuest"}

# Why does the wrong Rational ClearQuest record type form pop up when I create a defect from a Jazz product? [why-does-the-wrong-rational-clearquest-record-type-form-pop-up-when-i-create-a-defect-from-a-jazz-product]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: The
Rational solution for Collaborative Lifecycle Management (CLM) 4.x,
Rational ClearQuest 7.1.2.x ENDCOLOR

TOC{title="Page contents"}

This page describes how to configure your Rational solution for
Collaborative Lifecycle Management (CLM) and Rational ClearQuest Open
Services for Lifecycle Collaboration (OSLC) integration to use the form
you want.

## Initial assessment

### Symptoms

-   You are about to create a defect in Rational ClearQuest from a CLM
    application. After you click the **Create New Defect** icon, a
    Rational ClearQuest form pops up, but it is not the form you expect.

### Impact/scope

-   This issue should affect all users in the same Jazz project area who
    are selecting the same Rational ClearQuest artifact container.

### Timing (when?)

-   If this was working at one point and the form changed, the Rational
    ClearQuest administrator changed the schema. See [Possible
    solutions](#PossibleSolutions).

## Data gathering and subsequent analysis steps

Screen shots that identify the following will be helpful to the Rational
ClearQuest administrator:

-   In Jazz, which artifact container you selected to create the defect
-   In Jazz, the submit form
-   In Rational ClearQuest, the submit form
-   The Rational ClearQuest web URL, connection string, and user
    database you expect the defect to be created in

\#PossibleSolutions

## Possible solutions

\* There is only one form available to create a defect, and this is the
"Submit" form for the Rational ClearQuest default record type. \* The
default record type is set in the schema by the Rational ClearQuest
administrator. \* If the Rational ClearQuest administrator set the wrong
record type, then the administrator can change this in the schema. \*
After the Rational ClearQuest administrator upgrades the user database
to use the new schema, you may see a message stating that the database
has been upgraded and you need to log out and log back in. This message
is asking you to log in to Rational ClearQuest, not Jazz. \* To do that,
clear your browser cache. This will prompt you to log in to Rational
ClearQuest. \* After the new login, you will be able to use the new
form.

**Note:** A browser session time out might also prompt you to log in
again.

##### Related topics: [related-topics]

-   Still need help troubleshooting your integrations issue? Refer to
    [Integrations troubleshooting](IntegrationsTroubleshooting) for
    additional topics.

##### External links: [external-links]

-   ClearQuest Knowledge Center Topic [Setting the default record
    type](http://www.ibm.com/support/knowledgecenter/SSSH5A_8.0.1/com.ibm.rational.clearquest.schema.ec.doc/topics/t_mk_rectype_default.htm)

##### Additional contributors: Main.AntoinetteIacobo [additional-contributors-main.antoinetteiacobo]
