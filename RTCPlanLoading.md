META:TOPICINFO{author="sbagot" date="1432664455" format="1.1"
version="1.31"} META:TOPICPARENT{name="PerformanceTroubleshooting"}

# Why does my RTC plan take so long to load? [why-does-my-rtc-plan-take-so-long-to-load]

Authors: PerformanceTroubleshootingTeam Build basis: RTC 4.x, 5.x
ENDCOLOR

TOC{title="Page contents"}

Depending on the size and complexity of the plan in IBM Rational Team
Concert (RTC), plans may take some time to load.

## Initial assessment

### Symptoms

Accessing large plans in Rational Team Concert results in a long loading
time.

## Impact/scope

-   On which type of client does it happen (Web UI, Eclipse, Microsoft
    Visual Studio)?
-   Does it happen for all or multiple plans?

## Recommended data gathering and subsequent analysis steps

-   You can use
    [HTTPWatch](https://jazz.net/wiki/bin/view/Deployment/HowToHTTPWatch)
    to determine exactly how long the plan takes to load. HTTPWatch will
    also gather and export information about the calls being made when
    loading the plan.
-   Browser efficiency with relation to the CLM applications is directly
    related to the JavaScript engine. Try to load the plan in a
    different browser and see if the performance increases. For
    information about different browsers, see [Browser
    Performance](https://jazz.net/wiki/bin/view/Deployment/BrowserPerformance).
-   Establish and document a baseline with HTTPWatch to measure any
    further progress against (document the poor behavior).

## Possible causes and solutions

### When using the Eclipse client

-   If you are experiencing performance issues when loading plans in the
    Eclipse client, consider testing the same behavior in the Web UI.
    Plans are best viewed in the Web UI because the Eclipse based plan
    editor does not have all the latest features.
-   In case you observe that the RTC Client runs out of memory while
    loading plans, you can attempt to increase heap size. If the RTC
    Client is installed standalone, you can make the changes in the
    file:

/client/eclipse/eclipse.ini file For example, to increase the maximum
heap size to 1GB, you can add or modify the parameter -xmx after the
parameter -vmargs. -Xms256m -Xmx1024m If the RTC Client (Extension
install) is installed in the same shell with other Eclipse-based IDEs,
the eclipse.ini file will be located in the installation directory of
the other IDE.

-   You may increase the Maximum thread pool for RTC client operations.
    Follow these steps: 1 Open the RTC Client and select **Window \>
    Preferences \> Team \> Jazz Source Control \> Content Transfer** 1
    Increase the value of **Maximum number of Threads** (the default is
    10); increasing the thread count in increments of 5 or less. View
    performance statistics on each incremental change to find a balance
    between system resources and server availability. 1 Select **Show
    traffic statistics in status bar** 1 You can now open the Jazz
    Metronome UI found in the lower right corner of the RTC Client. 1
    Metronome will collect statistics allowing you to tune the threads
    and heap to optimal performance. See: [RTC Client for Eclipse IDE:
    slow
    response](https://jazz.net/wiki/bin/view/Deployment/RTCClientPerformance#RTC_Client_for_Eclipse_IDE_slow)

### When using the Visual Studio client

The Rational Team Concert Client for Microsoft Visual Studio lets you
create new plans and edit existing ones from an embedded web browser
based plan editor. See: When using the Web UI.

### When using the Web UI

When using the Web UI, you can improve performance by tuning your plans
and by upgrading to version 4.0.1 or higher.

## Tuning your plans for increased loading performance

The size and the complexity of the data contained in the plan influences
performance and overall loading time. Tuning the plans for overall size,
top level work items, grouping and sorting will all affect how the plan
loads. You can reduce this size and complexity as described in technote
[How to Improve Performance while loading large plans in the Web
UI](http://www.ibm.com/support/docview.wss?uid=swg21612656).

There are also some product level enhancements in 4.0.3 which will
change the layout of your plan and thus, load it much faster. For
information on this tuning, see [Fine Tuning
Parameters](https://jazz.net/wiki/bin/view/Main/FineTuningParameters#Parameters)
for plans.

## Plan improvements in Rational Team Concert

-   In **Rational Team Concert 4.0.1**, significant improvements have
    been made to both loading work items in batch, as well as
    compressing the work item data which results in a [performance
    increase of up to 25 faster in the web
    UI](https://jazz.net/products/rational-team-concert/whatsnew/),
    especially in low bandwidth networks.
-   In **Rational Team Concert 4.0.2**, there were no additional
    improvements to the planning component, so you can expect typically
    the same performance with plan loading as observed in 4.0.1 if you
    upgrade.
-   In **Rational Team Concert 4.0.3**, you can expect to see an
    additional 40 improvement in plan loading due to the changes
    described in the article: [Plan performance improvements in Rational
    Team Concert, Version
    4.0.3](https://jazz.net/wiki/bin/view/Main/PlanLoading)

##### Related topics: [related-topics]

-   [Browser performance](BrowserPerformance)
-   [How to use
    HTTPWatch](https://jazz.net/wiki/bin/view/Deployment/HowToHTTPWatch)
-   [Why is the Rational Team Concert client
    slow?](https://jazz.net/wiki/bin/view/Deployment/RTCClientPerformance)
-   [Performance
    troubleshooting](https://jazz.net/wiki/bin/view/Deployment/PerformanceTroubleshooting)

##### External links: [external-links]

-   How to Improve Performance while loading large plans in the Web UI:
    <http://www.ibm.com/support/docview.wss?uid=swg21612656>
-   Getting Started with Planning in Rational Team Concert 4.0:
    <https://jazz.net/library/article/593/>
-   Effective Planning with Rational Team Concert 4.0:
    <https://jazz.net/library/article/594/>
-   Customizing the Agile Planning tools in Rational Team Concert 4.0:
    <https://jazz.net/library/article/587/>
-   What's new in Rational Team Concert:
    <https://jazz.net/products/rational-team-concert/whatsnew/>

##### Additional contributors: None [additional-contributors-none]
