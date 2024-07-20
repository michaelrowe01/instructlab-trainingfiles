META:TOPICINFO{author="dmmckinn" date="1435178521" format="1.1"
version="1.18"}
META:TOPICPARENT{name="IntegrationsTroubleshootingRTCandClearCase"}

# My ClearCase import to Rational Team Concert failed. What can I do to understand why? [my-clearcase-import-to-rational-team-concert-failed.-what-can-i-do-to-understand-why]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: Rational
ClearCase 7.1.x, 8.x and later as supported with RTC 4.x and later
ENDCOLOR

TOC{title="Page contents"}

This page is intended to provide Rational ClearCase and Rational Team
Concert administrators with troubleshooting tips to use when a Rational
Team Concert and Rational ClearCase import fails.

## Initial assessment

### Prerequisites

Ensure that the Rational ClearCase Importer environment has been
configured correctly according to one of the following articles:

-   [Importing](http://www.ibm.com/support/knowledgecenter/SSR27Q_4.0.7/com.ibm.team.connector.scm.cc.doc/topics/c_import_history.html)
-   [Using the ClearCase Importer to import ClearCase
    history](https://jazz.net/library/article/50/)

### Symptoms

You can see your Rational ClearCase synchronized stream and request
synchronization but it says the sync engine is not available. The
synchronization operation starts and runs for a while but then
terminates with a message that the sync was blocked by an error.

## Possible causes

There are a variety of possible causes for the sync operation to fail.
Understanding where to look will help expedite a resolution.

-   Situations where the sync fails because the sync engine is not
    available are most often caused by the client requesting the sync
    not being able to contact the synchronization engine, or that the
    engine is not running.

<!-- -->

-   Situations where the sync fails with an exception that the sync was
    blocked with an error are typically more complex to resolve. Some
    investigation is usually required to determine cause.

## Investigation methods

When the sync is blocked by an error it is typically best to do the
following: Open the latest synchronization results for the synchronized
stream you are attempting to sync. To do this right click on the sync
stream in the eclipse client and select \> Open Latest Synchronization
Details. In the sync results there will be a logs tab. There will be two
logs that will provide the most useful information. The
build-\<######\>.log file and the synchronization stack trace. The
build-\<######\>.log file will have a complete record of the operation
whereas the synchronization stack trace file will contain the exception
that caused the sync to fail. Reading and understanding the exception
will be crucial to resolving the issue.

## Common causes for sync issues

The solution depends on the exception received, understanding the
exception and taking the appropriate action are imperative. The
exception can be received from either the Rational Team Concert or
Rational ClearCase side. Some common occurrences are listed below.

-   A list of known issues is listed in this Rational Team Concert
    Information Center topic: [Synchronization
    errors](http://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.5/com.ibm.team.connector.scm.cc.doc/topics/r_sync_errors.html)

<!-- -->

-   Rational ClearCase triggers can also potentially cause failures. The
    synchronizers issue cleartool commands against the Rational
    ClearCase elements and metadata. If these commands fire the trigger,
    it is possible this trigger firing can cause the sync to fail if the
    trigger criteria is not satisfied. The information center discusses
    this in greater detail in this topic: [Writing Rational ClearCase
    triggers for
    synchronization](http://www.ibm.com/support/knowledgecenter/SSR27Q_4.0.7/com.ibm.team.connector.scm.cc.doc/topics/t_sync_cc_triggers.html)

<!-- -->

-   Rational Team Concert mandatory attributes can also cause the
    synchronization to fail. The synchronization process will create a
    work item which, based on the process in use, may contain required
    attributes. If those attributes are not populated, the sync can
    fail. This issue can be addressed by using a work item template.

##### Related topics: [related-topics]

-   Still need help troubleshooting your integrations issue? Refer to
    [Integrations troubleshooting](IntegrationsTroubleshooting) for
    additional topics.

##### External links: \* Importing: <http://www.ibm.com/support/knowledgecenter/SSR27Q_4.0.7/com.ibm.team.connector.scm.cc.doc/topics/c_import_history.html> [external-links-importing-httpwww.ibm.comsupportknowledgecenterssr27q_4.0.7com.ibm.team.connector.scm.cc.doctopicsc_import_history.html]

-   Using the ClearCase Importer to Import ClearCase History:
    <https://jazz.net/library/article/50/>
-   Synchronization errors:
    <http://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.5/com.ibm.team.connector.scm.cc.doc/topics/r_sync_errors.html>
-   Writing Rational ClearCase triggers for synchronization:
    <http://www.ibm.com/support/knowledgecenter/SSR27Q_4.0.7/com.ibm.team.connector.scm.cc.doc/topics/t_sync_cc_triggers.html>

##### Additional contributors: None [additional-contributors-none]
