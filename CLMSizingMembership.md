META:TOPICINFO{author="vrokosz" date="1494094637" format="1.1"
reprev="1.1" version="1.1"} META:TOPICPARENT{name="CLMSizingStrategy60"}

# Impact of project membership on performanace DKGRAY Authors: Main.VaughnRokosz Build basis: All [impact-of-project-membership-on-performanace-dkgray-authors-main.vaughnrokosz-build-basis-all]

ENDCOLOR

TOC{title="Page contents"}

In the CLM 6.0.1 release, the number of users added explicitly as
members of a project area can degrade performance. This effect is most
noticeable in Rational Quality Manager and Rational Team Concert, and
can have an impact as the number of project area members grows beyond
1000. In this article, I'll discuss the impact that project area
membership has on performance, and describe some options that you have
to reduce this impact. I'll also highlight performance improvements
available starting in the 6.0.1 ifix stream, and additional improvements
available in the 6.0.4 release.

## Overview

In Jazz releases prior to 6.0.1 ifix9, performance is impacted by
project and team area membership. The following factors impact
performance:

-   The number of users added as members to a project area
-   The number of users added as members to a team area
-   The number of team areas. This is a factor because the code that
    checks whether a user has permission to execute an operation
    iterates through the team areas. The combination of a large number
    of team areas with large membership magnifies the performance
    impact.
-   The number of roles

Under light load, the main symptom of degradation is an increase in
response times. Operations that take less than a second in a project
area with few members can take several seconds or more as the
mermbership increases past 1000 users. Under heavier load, you can see
much higher CPU utilization, with the server potentially reaching 100
CPU at low levels of concurrency. If the system is at 100 CPU usage for
sustained periods, the response times degrade significantly; the system
is effectively overloaded.

For additional details, please refer to the attached PDF.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]

META:FILEATTACHMENT{name="Membership.pdf" attachment="Membership.pdf"
attr="" comment="" date="1494094609" path="Membership.pdf" size="186923"
user="vrokosz" version="1"}
