META:TOPICINFO{author="paulellis" date="1570181741" format="1.1"
version="1.5"} META:TOPICPARENT{name="WebHome"}

# Serviceability: Where to start? [serviceability-where-to-start]

DKGRAY Cross-cutting theme technical leaders and senior editors:
Main.PaulEllis Main.ShubjitNaik ENDCOLOR

TOC{title="Page contents"}

UNDER CONSTRUCTION

## What is serviceability?

### What does serviceability mean to me?

#### As an end user

#### As an administrator

#### As an implementer

## Self-servicing as a Jazz User

### Steps to take

Report any issues to the administrator. Gauge the severity of the issue
for need of contact.

-   Take a screen snapshot if appropriate and you have the capability.
-   If there is an error message, record the error message information,
    including the error message indicator.
-   If the problem is related to performance of the interface be
    specific as to what steps are being taken, and how long it takes to
    perform the step. If this process was at any time faster, also
    report the expected performance. Be sure to record the date, time
    and time length when this issue occurs.
-   If the problem is related to a specific activity being taken write
    down all of the steps to the activity including steps not yet taken,
    and mark where in the steps the problem occurs. If this activity was
    completed in the past, record the when the last time the activity
    was successful.

## Self-servicing as a Jazz Administrator

### Recognizing there is a problem

Assessing the scope of the situation can help you narrow down a list of
possible causes. Included below are some questions to keep in mind as
you investigate. These questions provide general guidance for getting
started and isolating the source of the problem. [How to start a
troubleshooting
assessment](https://jazz.net/wiki/bin/view/Deployment/HowToStartATroubleshootingAssessment)
will really assist in gathering the contextual information that IBM
Client Success will require.

### Steps to take

#### keep complete and consistent backups

Keeping good backups allows for quick restoration in the event of a
catastrophe.

-   Keep synchronized Database and index backups. The various indices
    and database information are directly related and should be saved
    and restored together.
-   Keep historically recorded backups. The problem that manifested may
    have not surfaced for some time. In the event of a problem like data
    corruption, it may be possible for an IBM Support engineer to aid in
    recovery if there is a comparable good and bad backup.
-   Test the backup process.

More information on Jazz Backup processes can be found
[here](https://jazz.net/wiki/bin/view/Deployment/BackupCLM).

#### Record everything during an issue.

There may not be time, capability, or awareness to diagnose and fix a
problem at the time of occurrence with a permanent solution. Some issues
become worse if not corrected, and others will possibly reoccur. It is
therefore important to gather and save the information, that can then be
reviewed and if necessary passed along to support at a later time.

-   Always create a backup of database, configuration, and indices
    before making changes to the system.
-   Also, make backup copies of the logs when the issue is first
    discovered, so that the logs do not roll over and the information is
    lost.
-   If possible, create a IBM Support Assistance bundle. More
    information can be found [here](#).
-   Document who first reported the problem, how, and when.
-   If the problem is re-creatable, document the steps to recreate, and
    the time of each recreation.

#### Places to look for more information

Error messages have a unique identifier. This identifier may be used to
search through documentation and support for more information on why the
error message occurred, more details into the error, and possible
actions to take to resolve the issue. The error message identifier may
also be used to search the logs for the occurrences of the the issue
that may not have been reported as well as finding the occurrence. The
occurrence in the logs may be preceded or followed by more information
related to the issue. The time stamp associated in the logs may also be
used to correlate the issue with other events such as Database or
Network outages, or events in other system logs.

There is also a very informative write-up in the [Common Jazz hardware
configuration and performance impact
overview](https://jazz.net/wiki/bin/view/Deployment/CommonJazzHWConfigPerfImpact).

## Involving IBM support

If you have a need to open a service request with [IBM Rational
Support](http://www.ibm.com/support/docview.wss?uid=swg27020747) for
further assistance, you can send the archive file with the data
collection so that they can help diagnose and fix problems.

#### Must-gather

Must-gather is the information absolutely necessary to resolve an issue
through IBM Support

-   If possible, create a IBM Support Assistance bundle.
    -   More information can be found
        [here](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.team.concert.doc/topics/t_using_the_isal.html).
-   There is a comprehensive [CLM must
    gather](https://jazz.net/wiki/bin/view/Deployment/MustgatherPerformanceProblemsInCLM)
    within this wiki.
-   There are specific must-gather information for each product
    -   [Troubleshooting the Requirements Management
        application](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.rational.rrm.help.doc/topics/c_compose_reqs.html&scope=null)
    -   [RTC Troubleshooting Basics and Data
        Collection](https://jazz.net/wiki/bin/view/Deployment/RTCTroubleshootingBasicsandDataCollection)
    -   [Support Portal for
        RQM](https://www-947.ibm.com/support/entry/myportal/product/rational/rational_quality_manager?productContext=-1981314478)
    -   [Diagnostic information for IBM Rational Reporting Development
        Intelligence and
        Insight](http://www-01.ibm.com/support/docview.wss?uid=swg21645071)

There is also a really helpful page containing [MustGather documents for
Rational Collaborative Lifecycle Management
products](http://www-01.ibm.com/support/docview.wss?uid=swg21634706),
focusing on key scenarios and integrations.

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   None

##### Additional contributors: Main.PaulEllis [additional-contributors-main.paulellis]
