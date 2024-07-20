# Why is browser performance slow?

Authors: Main.StephanieBagot 

Build basis: CLM 4.x and later


This page will help determine why there is performance degradation
within the web UI of IBM Rational Collaborative Lifecycle Management
(CLM) applications.

## Why does performance vary between browsers?

The performance of the browser's JavaScript engine has a direct impact
on the perceived end-user performance in web applications. The entire
Rational Team Concert web UI is run in JavaScript (except some Flash
reports), so the browser must load the dojo toolkit plus thousands of
JavaScript classes. The JavaScript engine must parse and execute this
information. Most browser vendors and versions have different JavaScript
engines, each with different abilities to interpret and run the
JavaScript, thus resulting in varying browser performance when loading
the CLM applications. Therefore, excluding network latency and
relatively short server response times, the performance of the CLM web
UI is directly proportional to the browser JavaScript engine speed.

Many resources are available online that provide browser comparisons
like the following article: (NOTE: this link will take you to an
external page) [The Big Browser Benchmark
Test](http://www.zdnet.com/the-big-browser-benchmark-all-the-latest-browsers-tested-7000007401/).

## Browser performance with CLM applications

The CLM web UI is optimized to improve performance in the code, by
compressing and pre-processing the JavaScript to be optimized, but the
web UI performance is still restricted based on the JavaScript engine
capabilities.

Based on our experience, the performance of Mozilla Firefox or Google
Chrome when running CLM applications can be significantly better than
the performance of Microsoft Internet Explorer.

Some performance testing has been done against 3.x and 4.x and can be
viewed under [WAN Performance
Testing](https://jazz.net/wiki/bin/view/Main/Jazz_wan_perf_40). Some
additional example measurements from our tests with CLM 4.0.1 are
provided below. These tests were gathered using a combination of
[HTTPWatch](http://www.httpwatch.com/) (Firefox and Internet Explorer)
and [Speed
Tracer](https://developers.google.com/web-toolkit/speedtracer/)
(Chrome).

**NOTE:** The measurements provided should not be used as a baseline for
browser performance in your environment. Your results might vary based
on your environment: hardware, operating system, other running software,
network, application server, database, authentication mechanism you use,
etc. All measurements are in seconds. Below is an average sample of
loading times gathered between different browsers using a small set of
functionality within Rational Team Concert. In order to validate this
information in your environment, see the section below to determine how
to run the comparative tests in your environment.

| Scenario | Internet Explorer 8 | Firefox 19 | Chrome 26 |
|:---|---:|:---|:---|
| Login without project area specified | 3.93 | 3.70 | 3.60 |
| Loading small work item | 9.27 | 5.30 | 4.54 |

## Possible causes

There are generally two causes for slow browser performance:

**1. User browser related issue** Performance from the web UI can be
cause by the browser JavaScript engine as discussed above

**2. Server performance issue** When overall browser performance is:

-   reported by all users
-   happens consistently at a certain time

The slow browser performance might be caused by a server-related issue
such as network latency, database response time etc. This type of
performance degradation will also be viewed in a rich client such as
Eclipse. For this type of performance issue, navigate to [How to Start a
Troubleshooting
Assessment](https://jazz.net/wiki/bin/view/Deployment/HowToStartATroubleshootingAssessment)
to identify possible causes to further investigate. Various performance
situations will be discussed on the [Performance
Troubleshooting](https://jazz.net/wiki/bin/view/Deployment/PerformanceTroubleshooting)
page.

## Recommended analysis steps

If you have experienced browser performance issues, navigate to [Browser
Performance](https://jazz.net/wiki/bin/view/Deployment/BrowserPerformance)
to determine if the issue is related to the server/client configuration,
or the actual browser itself.

### Questions to identify the problem

1 What URLs are being accessed? (Are you going through a proxy or
directly to the CLM server?) 1 Are the browsers being run on the same
LAN as the CLM server? If not, keep in mind that the location of your
user may cause some latency 1 When does the performance degradation
occur? (At peak hours or when there is a light user load?)

### Analysis steps

To investigate and analyze the performance degradation from within a
browser, take the following steps:

-   Ensure that the browser cache is clean before running any browser
    tests for performance

<!-- -->

-   Open your process monitor and see how much memory or CPU usage your
    browser is taking. On the machine running the client browser, take a
    look at the memory utilization to determine if your browser is
    running as 'lean' as possible. Closing down tabs or the entire
    browser itself and restarting it might release some of the consumed
    memory if it is too high.

<!-- -->

-   Deploy the Performance Health Check Dashboard widget [The
    Performance Health Check Dashboard
    widget](https://jazz.net/wiki/bin/view/Deployment/PerformanceHealthCheckWidget)
    runs a number of tests to measure the performance of various systems
    in a CLM deployment including the client, application server and
    database server. If the widget displays reasonable response times
    for each of the tests (green), then the latency and throughput of
    your connection with the server is within reasonable times and is
    indicative of a healthy server. Looking at the two possible causes
    above, browser or server, green response times rule out server as a
    root cause for performance degradation, leaving the browser as a
    possible culprit for the slow loading times. Alternatively, if the
    tests display red or slow response times, this shows that the
    connection with the server is not strong, leading to overall server
    performance (and not the specific browser) as the root cause. If
    this is the case, navigate back to the [Performance
    Troubleshooting](https://jazz.net/wiki/bin/view/Deployment/PerformanceTroubleshooting)
    main page to begin investigating other possible causes for the slow
    performance.

<!-- -->

-   Execute a comparative browser test In analyzing browser performance
    issues, it is important to determine if the product is causing the
    performance degradation, or the browser itself based on the
    limitations of the JavaScript engine as noted above. Running a
    comparative browser test will help identify if browser A is causing
    the problem, since the same function is displaying better
    performance in browser B. [HTTPWatch](http://www.httpwatch.com/) is
    a useful tool to inspect and monitor CSS, HTML, JavaScript and
    Internet requests in any web page and can help when investigating
    browser-related performance issues. To learn how to use HTTPWatch in
    your analysis, navigate to [How to Use
    HTTPWatch](https://jazz.net/wiki/bin/view/Deployment/HowToHTTPWatch).
    Another useful tool is the
    \[\[<http://www.webkit.org/perf/sunspider/sunspider.html>\]\[SunSpider
    JavaScript Benchmark\] webkit, which will compare the overall
    browser performance related to the JavaScript engine for the core
    JavaScript language only (not touching on DOM or browser APIs).
    Using the tools mentioned above, or others such as
    [Firebug](http://getfirebug.com/), or
    [SpeedTracer](https://developers.google.com/web-toolkit/speedtracer/),
    will trace the actual calls being made when loading a page within
    CLM. This information can be compared for varying performance across
    browsers (various browser add-ons might be needed for different
    vendors). See [How to Use
    HTTPWatch](https://jazz.net/wiki/bin/view/Deployment/HowToHTTPWatch)
    for more instructions on using the tool.

## Possible solutions

If the browser performance degradation is identified to be a **browser
issue**, then: Test the performance using a new browser (same vendor
with different version or different vendor all together) to determine if
the behavior is the same.

-   For example, if using Internet Explorer, try testing in Firefox or
    Chrome, as long as the browser is a [supported
    version](https://jazz.net/library/article/1109). If you are unable
    to test using a different browser, try to test using a different
    *version* of the browser, such as Internet Explorer 8 or 9. In our
    experience, Firefox and Chrome have increased performance over
    Internet Explorer.
-   If using a different browser did not result in increased
    performance, navigate back to the [Performance
    Troubleshooting](https://jazz.net/wiki/bin/view/Deployment/PerformanceTroubleshooting)
    main page to begin investigation into other possible causes for the
    slow performance and perhaps look into tuning the overall server for
    better performance.

If the browser performance degradation was actually identified to be a
**server issue**, then navigate to [Performance
Troubleshooting](PerformanceTroubleshooting) for additional topics on
troubleshooting and tuning.

### Tips to making Internet browsers run faster

-   Keep your browser up-to-date and patched
-   Make sure any plug-ins or extensions are up-to-date and patched
-   Remove any plug-ins or extensions you do not use
-   Think twice before customizing your browser
-   Run as lean as possible (no customizations, don't open multiple
    tabs)
-   Ensure you keep the cache for any CLM application information as it
    will speed up the loading time of the web UI
-   Cookies will maintain your authentication, but can be deleted after
    your user session to keep your browser lean. Keep in mind that
    removing the cookies will also remove the saved username from the
    login splash screen (if you have it selected).

##### Related topics: [related-topics]

-   Still need help troubleshooting your performance issue? Refer to
    [Performance Troubleshooting](PerformanceTroubleshooting) for
    additional topics.

##### External links: [external-links]

-   [Firebug add-on to Firefox browser slows Rational Quality Manager
    performance significantly
    ](http://www.ibm.com/support/docview.wss?uid=swg21322693)
-   [How to Improve Performance while loading large plans in the web
    UI](http://www.ibm.com/support/docview.wss?uid=swg21612656)

##### Additional contributors: 
* None [additional-contributors-none]
