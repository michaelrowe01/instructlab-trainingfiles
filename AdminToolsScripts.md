# Administrative utilities, tools, and scripts

Authors: Main.DanToczala 
Build basis: Varies for each asset

This page describes and links to more information about useful
utilities, tools, and scripts for Jazz administrators and Jazz users.
The tools are provided on an "as-is" basis.

## Administrator utilities

These utilities, tools, and scripts are intended to ease administrative
tasks.

-   [JTSMon](JTSMonTool) - JTSMon is a new tool that you can use to make
    more sense out of Jazz server traffic patterns based on web service
    reports. Also, check out the [FAQ for JTSMon](JTSMonFAQ), where you
    can download the utility.
-   [Automation
    server](https://rsjazz.wordpress.com/2013/07/15/boost-your-automation-performance-using-an-automation-server/) -
    This blog article describes the process of creating an automation
    server, which can complete the automation tasks that you might need
    for your CLM implementation. The automation server was originally
    created as a performance improvement to [automate the insertion of
    comments into a work item from the command
    line](http://rsjazz.wordpress.com/2013/07/12/work-item-command-line-client-to-add-a-comment/).
-   [Sample upgrade scripts](SampleUpgradeScripts) - These scripts are
    based on scripts that are used to upgrade Jazz.net and Rational
    functional verification test environments.

## Reporting utilities

These utilities, tools, and scripts are intended to provide simple
reports for various Jazz administrative needs.

-   [Simple baseline diff
    tool](http://dtoczala.wordpress.com/2011/01/14/simple-rtc-release-notes-script/) -
    This blog post by Main.DanToczala has a simple baseline diff tool
    for generating release notes. The tool is unsupported.
-   [Listing project area membership in Rational Team Concert and
    Rational Quality
    Manager](https://jazz.net/wiki/bin/view/Deployment/ListingProjectAreaMembershipinRTCRQM) -
    This paper, written by Carl Girourd, describes how to list a set of
    users that have membership to a project area in an easily consumable
    format. The procedure in this paper is unsupported.

### How are my project areas configured?

You want a list of how your projects are organized, and everything
inside of them. How do you do it? In the Eclipse client, open the Team
Organization view, right-click a project area, and click **Generate
Runtime Report**. A .zip file is exported that contains the project and
team area hierarchy, member assignments, and the process XML
configuration. However, the .zip file does not contain the work item
categories ("filed against" values). This technique is useful for
assessing how your project is organized.

## Miscellaneous utilities

These utilities, tools, and scripts do not easily fit into one of the
other categories.

-   [Workflow
    Visualizer](http://blog.stastnarodina.com/honza-en/spot/rational-team-concert-workflow-visualiser/) -
    This blog contains a workflow visualizer, which takes the Process
    XML from Rational Team Concert as an input, and produces simple
    images of the workflow for the various work item types. The workflow
    visualizer is unsupported.

##### Related topics: 
None [related-topics-none]

##### External links: 
  * [Ralph Schoon Blog](https://rsjazz.wordpress.com/) [external-links-ralph-schoon-blog]

##### Additional contributors: 
None [additional-contributors-none]
