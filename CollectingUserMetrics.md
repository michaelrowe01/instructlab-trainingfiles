META:TOPICINFO{author="tfeeney" date="1612994238" format="1.1"
version="1.4"} META:TOPICPARENT{name="MBeansUsage"}

# Collecting user related metrics using JMX MBeans DKGRAY Authors: Main.TimFeeney Build basis: 7.0 and later [collecting-user-related-metrics-using-jmx-mbeans-dkgray-authors-main.timfeeney-build-basis-7.0-and-later]

ENDCOLOR

TOC{title="Page contents"}

There a few different MBeans to assist with tracking user related
metrics that are useful for measuring adoption trends/growth as well
usage that can be a factor in system load/performance. Consider adding
these to available dashboards created to monitor your ELM applications.
Complete details on their object names, attributes, collections, etc.
can be found in the appropriate release's [reference
documentation](MBeansReference).

## Contributor Information MBean

This MBean includes attributes for

-   ***totalCount*** - the total registered users in the repository
-    ***unarchivedCount*** - how many of those users are active, that is
    not archived
-   ***archivedCount*** - how may have been archived

This can help determine the extent to which your user population has
been given access to a repository. If access is given gradually, that
is, when needed, then the growth trend in this number can help measure
adoption rate. Some clients find it easier to add all or large portions
of their users en masse, though not necessarily assign them a license
until needed; that method would make the measurement less helpful in
showing adoption rate.

Comparing active user counts to license usage can provide good ratio
metrics to help determine if you have sufficient licenses for future
growth.

## Active Services Summary MBean

This MBean includes an attribute for

-   ***concurrentUsers*** - represents the number of unique users
    associated with an application's active services running at the time
    the bean data is collected

Concurrent users is an important data point to collect over time for
growth planning/projection, to ensure you stay within known user scale
maximums and to give insight into the load on an application when
triaging an performance anomaly.

## Server Activity Summary Metrics MBean

This MBean includes an attribute for

-   ***activeUsersCount*** - represents the number of unique users
    associated with all of an application's active services that were
    running some time during the bean's collection interval (not the
    same as concurrent users)
-   ***userWithMostServicesInInterval*** - of those active users, which
    one was the most active, in terms of total running services, during
    the collection interval

It is useful to track *activeUsersCount* to get a sense of what the
'normal' range of activity is for an application. When usage varies
significantly beyond the normal range, look at other usage metrics, eg.
CPU/memory utilization, to gauge whether the server is still running
well within its constraints.

Monitoring *userWithMostServicesInInterval* may provide insight as to
what user may be contributing to a performance anomaly or high load.
