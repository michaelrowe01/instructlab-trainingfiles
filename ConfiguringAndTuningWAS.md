META:TOPICINFO{author="din" date="1704367360" format="1.1"
version="1.32"} META:TOPICPARENT{name="DeploymentAdminstering"}

# Configuring and tuning WebSphere Application Server (WAS) [configuring-and-tuning-websphere-application-server-was]

DKGRAY Authors: Main.StevenBeard, Main.GrantCovell, Main.TimFeeney Build
basis: Jazz applications and environments ENDCOLOR

TOC{title="Page contents"}

`Note: Support removed for IBM !WebSphere Application Server (Traditional WAS) starting with ELM version 7.0.3. Use !WebSphere Liberty, either embedded and installed with ELM applications, or separately installed`

This page covers specific guidance and best practices for tuning WAS for
Jazz applications and environments. See [General WAS top tuning
recommendations](WASTopTuningRecommendations) for information about
non-Jazz specific WAS tuning.

## Monitor, Monitor, Monitor

The recommendations made should be vetted and regularly reviewed based
on data collected by systematic [deployment
monitoring](DeploymentMonitoring).

## Review the default WAS settings

Review the instructions at [Setting up
WAS](https://jazz.net/help-dev/clm/index.jsp?re=1&topic=/com.ibm.jazz.install.doc/topics/t_configure_was_jython.html&scope=null).

## Review the default JVM settings

Be sure you start with the minimum recommended JVM settings.

-   **-Xmx4G** - The maximum JVM heap setting. It should be set to no
    more than half of the available memory on the computer that hosts
    the Jazz application. In this example, it is set to 4 GB, which
    assumes that you have at least 8 GB of memory on the computer that
    hosts this Jazz application instance.
-   **-Xms4G** - The minimum JVM heap setting. It should be set to the
    same value as the maximum JVM heap setting.
-   **-Xmn512M** - The maximum "nursery" size. Add this setting for
    older versions of WAS (7.X and lower). Beginning with WAS 8.0, the
    JVM makes very good decisions on nursery size, so this should not
    generally be set.
    -   **Older versions of WAS (7.X and lower)** - This should be set
        to 1/8 of the value that your settings for the maximum and
        minimum JVM heap are set. In some situations (usually validated
        by close examination of JVM garbage collection logs), this value
        may be increased to 1/4 of the value of the maximum and minimum
        JVM heap settings.
    -   There are customers whose first tuning action is to add RAM to
        their server and correspondingly increase the JVM heap settings.

<!-- -->

-   **-Xgcpolicy:gencon** - The garbage collection policy that the JVM
    uses. Use "gencon", and don't make changes unless you have read
    about and fully understand [JVM garbage
    collection](http://www.ibm.com/developerworks/java/library/j-ibmjava2/)
    and how it impacts the performance of the Jazz applications. This is
    the default for WAS 7 and newer.
-   **-Xcompressedrefs** - Indicates use of compressed references in the
    JVM. Use this setting unless explicitly told otherwise.

Additionally, on all platforms except AIX:

-   **-Xgc:preferredHeapBase=0x100000000** - The preferred base address
    of the heap. Use this setting unless explicitly told otherwise.

If you are not using IPv6, consider disabling IPv6 support in the JVM:

-   **-Djava.net.preferIPv4Stack=true** - This setting tells the JVM to
    only use IPv4.

Consider enabling large page sizes if your version of WAS does not
already support them by default. If you are using Java 7 in WAS 8.5.0.2
or greater this setting is automatic.

-   **-Xlp** - Note that if your operating system doesn't also support
    large pages, Java does not start with this setting enabled. For
    example, on Linux, large pages must be configured both in the Linux
    kernel and in the JVM.

## Review the WebContainer thread pool settings

-   The default WAS WebContainer thread pool settings are a minimum and
    maximum size of 50. Set the minimum and maximum size to 200 for Jazz
    applications. Realize that increase threads might increase memory
    consumption and push a greater amount of load onto the database. As
    is the case whenever you change any setting, be sure to monitor the
    rest of the environment in case there are side effects.

## Review the JDBC connection and mediator pool settings

-   Set the JDBC Connection pool size and mediator pool size to the
    value of `max_clients` \* 25. `max_clients` is the estimated number
    of concurrent users making requests. `max_clients` is not equivalent
    to the estimated number of concurrent (or actively logged in) users.
    `max_clients` is usually around 10 of the estimated number of
    currently logged in users. The default value is 128.

## Adjust the LPTA token timeout

Sometimes you might see many LPTA token timeout errors in the WAS logs
(systemOut.log). These are caused by the LTPA (which provides SSO
authentication capabilities) tokens being either expired or corrupted.
These errors can be addressed in three different ways:

1.  Force the token to be reestablished
2.  Adjust the LTPA timeout
3.  Do nothing and live with the errors

For more information, see [LTPA Token Expired error in WebSphere Logs
with Rational Team
Concert](http://www-01.ibm.com/support/docview.wss?uid=swg21590961) on
the IBM Support website. The reason why you might want to address this
issue is that the WebSphere logs can grow quite large as multiple
entries are produced every second.

### Solution 1: Force token

To eliminate duplicate messages, you can remove the LTPA Tokens by using
the following steps:

-   Stop WAS
-   Remove the LTPA key at
    `WAS_HOME/profiles/profileName/config/cells/cellName/nodes/nodeName/ltpa`
-   Restart WAS.

### Solution 2: Adjust LTPA timeout

Adjust the LPTA timeout by following these steps:

-   Launch WebSphere Admin Console to start the WAS Console.
-   In the WAS Console navigation pane, click Security \> Global
    security.
-   In the Authentication area of the Global security page, click the
    LTPA link.
-   In the LTPA timeout area of the LTPA page, edit the value for the
    LTPA timeout from the default of 120 minutes to an arbitrarily large
    number and click OK.
-   In the Messages area at the top of the Global security page, click
    the Save link and log out of the WAS Console.

Follow these steps only on the application nodes.

## Setting the WAS WebContainer to synchronous mode

### *Problem (abstract)*

*The WebContainers use of asynchronous data transfer might use a large
number of buffers in native memory to write an application response.
This predominately occurs when large application responses are being
transferred (for example a PDF, large images, the DMGR updating the
nodeagents, etc.) but can also occur with normal size application
responses. If the amount of native memory used by this is too large, you
can enable synchronous mode, which reduces the amount of memory used to
store responses.*

Most instances, where it has been necessary to set channelwritetype to
synchronous, have involved addressing performance issues related to
Rational Team Concert SCM and Build. It is not the case that all Team
Concert environments need this setting.

For further information, see the [Setting the WAS WebContainer to
synchronous
mode](http://www-01.ibm.com/support/docview.wss?uid=swg21317658)
troubleshooting technote on the IBM Support Portal.

##### Related topics: [General WAS top tuning recommendations](WASTopTuningRecommendations) [related-topics-general-was-top-tuning-recommendations]

##### External Links: [external-links]

-   [Case Study: Examining Rational Team Concert performance with WAS
    and Tomcat](https://jazz.net/library/article/790)
-   [Administering WAS by using
    Jython](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m4/index.jsp?re=1&topic=/com.ibm.jazz.install.doc/topics/c_admin_was_jython.html&scope=null) -
    CLM information center.
-   [Collaborative Lifecycle Management 2012 Sizing Report (Standard
    Topology E1)](SizingReportCLM2012)
-   IBM developerWorks article [Case study: Tuning WAS V7 and V8 for
    performance](http://www.ibm.com/developerworks/websphere/techjournal/0909_blythe/0909_blythe.html)

##### Additional contributors: [DanToczala](Main.DavidToczala), Kevin Arhelger, Main.KevinZemanek [additional-contributors-dantoczala-kevin-arhelger-main.kevinzemanek]

META:TOPICMOVED{by="sbeard" date="1385831341"
from="Deployment.TuningWAS" to="Deployment.ConfiguringAndTuningWAS"}
