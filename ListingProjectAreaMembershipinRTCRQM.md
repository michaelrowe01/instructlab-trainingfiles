META:TOPICINFO{author="sbeard" date="1402820978" format="1.1"
reprev="1.5" version="1.5"} META:TOPICPARENT{name="AdminToolsScripts"}

# Listing project area membership in Rational Team Concert and Rational Quality Manager [listing-project-area-membership-in-rational-team-concert-and-rational-quality-manager]

DKGRAY Author: Carl Girouard - (<cgiroua@us.ibm.com>) Build basis:
Rational Team Concert and Rational Quality Manager, 4.0.x ENDCOLOR

TOC{title="Page contents"}

## Introduction

The Collaborative Lifecycle Management server provides a rich set of
capabilities to report the details of its configuration and the usage by
various components. Based on our experience, we realized reporting of
some custom usage patterns are not available in the product. An example
of such a feature is to list a set of users that have membership to a
particular project area in Rational Team Concert and Rational Quality
Manager in an easily consumable format.

In the project area administration page, the Rational Team Concert or
Rational Quality Manager server lists the project area members. There
could be additional team members that can have access to the project
area, without being listed in the project area administration page. For
example, if a member is directly added into a team area in a particular
project area, he or she is not listed at the project level, but may have
access to all the project area artifacts.

In this article, we will use the REST API and XML framework supported by
the Rational Team Concert and Rational Quality Manager server to extract
the list of users that belong to each project area, including the
project team areas.

There are many benefits for such a report. The following describes few
important use cases:

1.  If you want to limit access to a particular project area to its
    hierarchy. You need to know which users belong to the project area.
    Since there is no single place in Rational Team Concert that can
    show this list, this tool can be useful to verify the read
    compartmentalization of a Rational Team Concert or Rational Quality
    Manager project area.
2.  If you are changing some key features to a project area process
    specification or similar structural changes to a project area, this
    tool can be used to list the only users that will be impacted. This
    will eliminate an email to all the users on the CLM Jazz Team Server
    server, since it is now possible to target only those users who will
    be impacted by the action.

## Script functionality

The script itself has two main branches, the first one being able to
pull all the active project areas and second one is to list all the
users that belong to a particular project area. First we will login to
the Rational Team Concert or Rational Quality Manager Server, list the
project areas. Subsequently, we iteratively traverse through each of the
project area hierarchy to report the users. Usage of this script
requires membership to the jazzAdmin group on the service you wish to
execute it against.

The script, clmProjectUsersPull.pl, (see attachment) which is written in
PERL, requires the following modules:

LWP::UserAgent XML::Simple  

It is possible to install these Perl modules in several ways and the
installation method varies based on operating system. The CPAN modules
installation page can help get you started:
<http://www.cpan.org/modules/INSTALL.html>

## REST API calls

There are several REST API calls that the script invokes in order to
gather the required data. They are listed here along with a short
description of why each is called.

You can step through these calls manually in a web-browser using an
appropriate 'UUID' obtained from the content in the call previous to it.
This will allow for a better understanding of how the data is structured
and open the door to leverage this script in order to pull other data.

Note: The REST call is highlighted in **bold**.

The first REST call is made to verify credentials being used to pull the
data.

[https://url.of.server:port/appContextRoot/secure/service/com.ibm.team.repository.service.internal.webuiInitializer.IWebUIInitializerRestService/initializationData](https://url.of.server:port/appContextRoot/secure/service/com.ibm.team.repository.service.internal.webuiInitializer.IWebUIInitializerRestService/initializationData)

The next call is made to pull the project areas on the service.

[https://url.of.server:port/appContextRoot/service/com.ibm.team.process.internal.common.service.IProcessRestService/allProjectAreas](https://url.of.server:port/appContextRoot/service/com.ibm.team.process.internal.common.service.IProcessRestService/allProjectAreas)

The call is made for each project area (uuid) to pull hierarchy of the
projects team areas.

https://url.of.server:port/appContextRoot/service/com.ibm.team.process.internal.service.web.IProcessWebUIService/projectHierarchy?uuid=

This call is made to pull the admins/members of each main project area
(processAreaItemId).

https://url.of.server:port/appContextRoot/service/com.ibm.team.process.internal.service.web.IProcessWebUIService/projectAreaByUUIDWithLimitedMembers?processAreaItemId=

This call is made to pull the admins/members of each team area
(processAreaItemId).

https://url.of.server:port/appContextRoot/service/com.ibm.team.process.internal.service.web.IProcessWebUIService/teamAreaByUUIDWithLimitedMembers?processAreaItemId=

## Script innvocation

This script can be invoked as follows:

clmProjectUsersPull.pl \[admins\|users\|both\]

Example 1:

clmProjectUsersPull.pl <https://clm.ibm.com:9443/ccm> adminUser
'adminPass'

Output 1:

Project1

Project2

...

ProjectN

 

Example 2:

clmProjectUsersPull.pl <https://clm.ibm.com:9443/ccm> adminUser
'adminPass' both

Output 2:

Project1,userId1,admin

Project1,userId1,member

Project1,userId2,member

Project2,userId1,member

Project2,userId3,member

...

ProjectN,userIdN,admin

ProjectN,userIdN,member

 

## Advanced editing

With the Rational organization, we have had great success using this
tool to report the users by project area. We could also generate a list
of the unique users on any particular Rational Team Concert or Rational
Quality Manager application. As noted above, this list will be a subset
of all users reported at the Jazz Team Server level. We have used the
list of users extracted by the tool notify relevant constituents during
Rational Team Concert and Rational Quality Manager server upgrades, and
any sporadic outages to servers.

Sometimes, the report you want may not be exactly what the script
provides. In those cases, the script can be easily modified to suite
your needs. This requires a basic knowledge of Perl, and the exact XML
value type to be gathered. This is changed in the 'getProjectTeamUsers'
subroutine. For instance, a common change might be changing 'userId' to
'emailAddress'. See the 'REST API Calls' section for the process on how
to obtain the specific XML values that can be used.

Subsequently, the data printed out can be modified to suit your needs.
This is done in the 'printUserData' subroutine by changing the values in
each print statement.

Alternatively, you can export the output of the tool into any
spreadsheet program to modify the report.

## Summary

In summary, you can use the above tool as is, easily modify or export
the data to a spreadsheet program as it fits your needs. In addition,
you can extend the framework used in the tool to create an entirely
different report all by yourself.

## About the author

Carl Girouard is part of the Rational Enginering Services Jazz
Operations team which is responsible for two site environments operating
several CLM deployments in various configurations and have an IBM base
of over 7000 active users. He works for Rational Engineering Services in
providing CLM and Infrastructure services to the entire Rational Brand.
Carl's background is mostly in operations providing UNIX, automation,
and database services.

##### Related topics: None [related-topics-none]

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]

-   [clmProjectUsersPull.pl.txt](ATTACHURL/clmProjectUsersPull.pl.txt):
    PERL source for examples in ListingProjectAreaMembershipinRTCRQM

META:FILEATTACHMENT{name="clmProjectUsersPull.pl.txt"
attachment="clmProjectUsersPull.pl.txt" attr="" comment="PERL source for
examples in ListingProjectAreaMembershipinRTCRQM" date="1368820881"
path="clmProjectUsersPull.pl.txt" size="9149" user="recogan"
version="1"}
