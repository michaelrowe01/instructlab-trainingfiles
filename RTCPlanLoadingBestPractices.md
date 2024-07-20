META:TOPICINFO{author="tfeeney" date="1464972040" format="1.1"
reprev="1.2" version="1.2"}
META:TOPICPARENT{name="CLMUsageModelBestPractices"}

# RTC Plan Loading Best Practices [rtc-plan-loading-best-practices]

DKGRAY Authors: Main.DanielPool, Main.RalphSchoon, Main.TimFeeney Build
basis: The Rational solution for Collaborative Lifecycle Management
(CLM) and the Rational solution for systems and software engineering
(SSE) v6.0.1. ENDCOLOR

TOC{title="Page contents"}

Plan loading optimizations are in place for RTC 6.0.1. These
optimizations can significantly improve plan load performance for large
trees. These optimizations include "Fetch Outplaced Children On Demand"
and "Fetch Plan Item Children On Demand". With these optimizations
enabled you can configure your plans by creating new lightweight plans
and new lightweight plan views. Then use those whenever heavyweight plan
views are not required.

The key is to configure plans to show you relevant information, for the
items in that plan.

## Use high level plans to get broad overview of plan scope

High level plans have a set of high level plan items, such as Stories or
Epics. In the plan view settings, set Include children from other plans:
to 1 Level. Then switch to the narrowly focused plans when you need to
see the details of those nested trees.

## Use team level iteration plans to drill down on current work

Rather than using one monolithic plan and drilling down to a specific
team and iteration, create a plan that is scoped to what each team is
currently working on and have the teams work from those plans.

## Only Use Cross Project Plans for Scheduling Cross Project Items

Cross project plans should be used for calculating the schedule of items
that you want to track together, but that do not share a project area.

The work item scheduler is a main component of how planning works. Work
Items appear in the accumulated time view in the order they are
scheduled. Plan snapshots are used to calculate the schedule for cross
project plans. Because of the need to calculate schedules using work
items from multiple snapshots, cross project plans can be slower than
other plans. In general, if you are not tracking the schedule of a group
of items from different project areas, you should use another plan type.

If you have a cross project plan and want to continue to track these
items together, but you do not need scheduling information, then create
a new plan of type of some other type such as Release Backlog. Set the
Owner and Iteration for the new plan to those of the cross project plan.
Then in the new plan, create a new view that is a copied from the view
in the cross project plan.

## Getting the most out of delayed child loading.

Child elements will be loaded as needed when delayed child loading is
enabled and active. This allows large tree plans to only load top level
elements. And that can significantly improve performance.

*Outplaced Children* are children that are not directly part of this
plan, but are still shown as part of the tree.

*Plan Item Children* are children that are directly part of this plan.

Unfortunately, not all plans can take advantage of delayed load. These
plans will load all plan children, regardless of the settings. This
section describes plan options that can be modified to allow your plans
to use delayed loading of children.

----++ Ensure Delayed Load of Children is Enabled

Settings to enable delayed load of items are in the Application
Administration/Advanced Properties. When these settings are enabled
plans only load the top level items. Then when a plan item is expanded
in the plan view tree, the children for the plan item are loaded.

----++ Only show Accumulated Time when you specifically want that
Information.

In order to calculate accumulated time all plan items must be loaded by
the client.

If you are not using the accumulated time information, create a copy of
the view with all the other information you are using. Then remove the
accumulated time column from the copy.

----++ Only Group by Team when you specifically want that grouping.

The server does not have enough information to determine the team of
each item. The client fetches all plan items to calculate this grouping.

In the Scrum Project Template the Release Backlog/Team View is grouped
by Team.

Avoid this grouping if it is not specifically what you want.

----++ Only Group by Folder when you specifically want that grouping.

The server does not have enough information to determine the grouping
for the items. The client fetches all plan items to calculate the
grouping.

Avoid this grouping if it is not specifically what you want.

## Set a lightweight Default View

Once you have created your new lightweight plan view based on the
information above, you can set that view as the default plan view. Then
this plan will load more quickly when you or others view the plan.

## Switch Views for More Information

If you create a lightweight view that loads quickly you can open it to
work with. If after working with it you realize you want additional
information, toggle over to the heavyweight view. The existing data will
remain loaded as the plan pulls in the additional information you want
to work with. You don't pay the plan load penalty twice. Obviously if
you know you need the data initially, you can just open the heavyweight
view to begin with.

## Plan Scope

Eliminate unnecessary item loading by using Plan Scope.

Other plan exclusions work by filtering plan items after the plan has
loaded. Plan Scope keeps items that do not need to be displayed from
being fetched by the client by filtering on the server. Plan Scope can
be particularly helpful in removing resolved items, or items whose type
is not appropriate for this plan (e.g. release items vs. plan items).

For more information on configuring plan scope see: [Plan
Performace/Plan
Scope](https://jazz.net/downloads/rational-team-concert/releases/6.0?p=news#plan_performance)

## Optimal Plan Size

It is difficult to come up with a single number of elements that work
best for planning. A plan shows some set of information about a group of
elements. Performance is highly dependent on what is being shown. In
general plans with 300 to 400 elements should load quickly. You can
continue to increase plan size up to 1,000 to 1,500 elements. Once you
start getting above this you may find performance degrading.

## Use Quick Planner

In addition, releases of RTC (5.0.2 and forward) include a new planning
tool, called [RTC Quick
Planner](http://www.ibm.com/support/knowledgecenter/SSCP65_6.0.1/com.ibm.team.concert.tutorial.doc/topics/tut_quick_planner_lesson.html)
which allows teams to edit plans in a fast and fluid manner. RTC Quick
Planner is fast and lightweight; plans load much faster, as it only
loads only a few screens of the plan at a time and then loads additional
plan items as you page through the plan and ask to display them.
Developers, Scrum Masters and other users who need to load plans quickly
and create new work items dynamically, should be encouraged to use RTC
Quick Planner for their daily plan scenarios.

##### Related topics: [Best Practices for CLM Usage Models](CLMUsageModelBestPractices) [related-topics-best-practices-for-clm-usage-models]

META:FILEATTACHMENT{name="PlanConfigOptions1.png"
attachment="PlanConfigOptions1.png" attr="" comment="" date="1464969765"
path="PlanConfigOptions1.png" size="51300" user="tfeeney" version="1"}
META:FILEATTACHMENT{name="PlanLightweightView.png"
attachment="PlanLightweightView.png" attr="" comment=""
date="1464969887" path="PlanLightweightView.png" size="31026"
user="tfeeney" version="1"}
META:FILEATTACHMENT{name="PlanConfigOptions2.png"
attachment="PlanConfigOptions2.png" attr="" comment="" date="1464969951"
path="PlanConfigOptions2.png" size="36509" user="tfeeney" version="1"}
META:FILEATTACHMENT{name="PlanGroupByFolder.png"
attachment="PlanGroupByFolder.png" attr="" comment="" date="1464969978"
path="PlanGroupByFolder.png" size="39617" user="tfeeney" version="1"}
META:FILEATTACHMENT{name="PlanGroupByTeam.png"
attachment="PlanGroupByTeam.png" attr="" comment="" date="1464969999"
path="PlanGroupByTeam.png" size="67113" user="tfeeney" version="1"}
META:FILEATTACHMENT{name="PlanAccumulatedTime.png"
attachment="PlanAccumulatedTime.png" attr="" comment=""
date="1464970016" path="PlanAccumulatedTime.png" size="75350"
user="tfeeney" version="1"}
META:FILEATTACHMENT{name="PlanDelayLoading.png"
attachment="PlanDelayLoading.png" attr="" comment="" date="1464970032"
path="PlanDelayLoading.png" size="13643" user="tfeeney" version="1"}
META:FILEATTACHMENT{name="PlanChildren.png"
attachment="PlanChildren.png" attr="" comment="" date="1464970049"
path="PlanChildren.png" size="36271" user="tfeeney" version="1"}
META:FILEATTACHMENT{name="PlanViewCopy.png"
attachment="PlanViewCopy.png" attr="" comment="" date="1464970066"
path="PlanViewCopy.png" size="41691" user="tfeeney" version="1"}
META:FILEATTACHMENT{name="PlanDetails.png" attachment="PlanDetails.png"
attr="" comment="" date="1464970084" path="PlanDetails.png" size="39733"
user="tfeeney" version="1"}
META:FILEATTACHMENT{name="PlanSwitchViews.png"
attachment="PlanSwitchViews.png" attr="" comment="" date="1464970337"
path="PlanSwitchViews.png" size="34487" user="tfeeney" version="1"}
