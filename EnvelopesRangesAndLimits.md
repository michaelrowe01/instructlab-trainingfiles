META:TOPICINFO{author="michaelrowe" date="1702415060" format="1.1"
version="1.7"} META:TOPICPARENT{name="CLMSizingStrategy"}

# Envelopes, ranges and limits DKGRAY Authors: Main.StephaneLeroy, Main.GrantCovell Build basis: CLM and SSE 3.X to 5.X [envelopes-ranges-and-limits-dkgray-authors-main.stephaneleroy-main.grantcovell-build-basis-clm-and-sse-3.x-to-5.x]

ENDCOLOR

TOC{title="Page contents"}

**In progress; nothing here has been proofread, validated or confirmed**

TRL = Technical Runtime Limit

LTL = Logical Technical Limit

## Topologies

|  |  |  |  |  |
|----|----|----|----|----|
| Dimension | ORANGE TRL ENDCOLOR | BLUE LTL ENDCOLOR | GREEN Recommendation ENDCOLOR | Notes, References |
| Registered Users | 1 to unlimited | 13,000 | 6000 per single JTS | Also see [CLMSizingStrategy](CLMSizingStrategy) |
| Concurrent Users | 1 to unlimited | 1300 | see note | Perhaps the most difficult dimension to express simply, see [CLMSizingStrategy](CLMSizingStrategy) |
| Application server disc space | unlimited | \## | 100GB min | We don't generally size hard-drives; use common sense |
| Database disc space | unlimited | \## | 500GB min | We don't generally size hard-drives; consult your DBAs |

## JTS

|  |  |  |  |  |
|----|----|----|----|----|
| Dimension | ORANGE TRL ENDCOLOR | BLUE LTL ENDCOLOR | GREEN Recommendation ENDCOLOR | Notes, References |
| Registered users |  |  |  |  |
| Concurrent users |  |  |  |  |
| Repository size |  |  |  |  |
| Index size |  |  |  |  |
| Jazz user ID length | 250 bytes | 250 bytes | no more than 250 bytes | <https://jazz.net/forum/questions/123433/is-there-any-known-limitation-of-the-length-of-login-id> |
| Instances of RTC per JTS |  | 2 |  |  |
| Instances of RRC 4.x per JTS | 1 | 1 | 1 | <https://jazz.net/forum/questions/123433/is-there-any-known-limitation-of-the-length-of-login-id> |
| Instances of RDNG 5.x per JTS | \## | 3 | as needed | sizing article |
| Instances of RQM per JTS | \## | 2 | as needed | sizing article |

## RTC

\| Dimension \|ORANGE TRL ENDCOLOR\|BLUE LTL ENDCOLOR\|GREEN
Recommendation ENDCOLOR\| Notes, References \| \|Concurrent
users\|1-500\| 1200 \|300-500\| \| \|JVM size\| \| \| \| \| \|Repository
size\|600 GB\| \| \| \| \|Index size\|16+ GB (jazz.net)\| \| \| \|
\|Workitems in a plan\|1 to 2048\|\|1 to 200\| \| \|Workitems in a
project area\|unlimited\| \|
\|<https://jazz.net/library/content/articles/rtc/2.0/enterprise-configuration/sizing-guide/index.html>
\| \|Project areas in a repository\|unlimited\| \|
\|<https://jazz.net/library/content/articles/rtc/2.0/enterprise-configuration/sizing-guide/index.html>
\| \|Team areas in a project\| 1 to 1024?\| \| \| \| \|Workitem
attachment size\|50MB\|
\|0-50MB\|<http://www-01.ibm.com/support/docview.wss?uid=swg21641142> \|
\|Artifacts in a repository\|Unlimited \|888,000\|
\|<https://jazz.net/library/article/984/>\| \|Filesize for an SCM
artifact\|unlimited\| \|\<
4GB\|<http://www-01.ibm.com/support/docview.wss?uid=swg21419931>
<http://www-01.ibm.com/support/docview.wss?uid=swg21421926>\| \|Workitem
custom attribute length: Small String\|250 bytes\| \|
\|<https://jazz.net/library/article/1003#customattributes> \| \|Workitem
custom attribute length: Medium String\|1000 bytes\| \|
\|<https://jazz.net/library/article/1003#customattributes> \| \|Workitem
custom attribute length: Large String\|32768 bytes\| \|
\|<https://jazz.net/library/article/1003#customattributes> \| \|Workitem
custom attribute length: Medium HTML\|1000 bytes\| \|
\|<https://jazz.net/library/article/1003#customattributes> \| \|Workitem
custom attribute length: Large HTML\|32768 bytes\| \|
\|<https://jazz.net/library/article/1003#customattributes> \| \|Results
of a query \| 1 to 1000 \| \| less than 1000 \|
<https://jazz.net/forum/questions/126270/rtc-eclipse-client-query-results-limitted-to-1000-rows-how-to-retrieve-rows-after-1000?redirect=2Fforum2Fquestions2F1262702Frtc-eclipse-client-query-results-limitted-to-1000-rows-how-to-retrieve-rows-after-1000>\|
\|Timelines in a plan\|1 to 2048\| \|
\|<https://jazz.net/forum/questions/65670/timeline-limitation> \| \|\<
5.0: Files/folders in a single component\|50K\| \|
\|<https://jazz.net/library/article/641/> \| \|\>= 5.0: Files/folders in
a single component\|100K\| \| \|<https://jazz.net/library/article/814/>
\| \|Suspended change-sets by individual user\|1 to
300\|\|300\|<https://jazz.net/library/article/641/>\| \|Components in
workspaces and streams\|1 to 2500\| 2500 \| less than 2500
\|<https://www.ibm.com/support/knowledgecenter/en/SSYMRC_7.0.0/com.ibm.team.scm.doc/topics/t_component_bestpractices.html>
\| \|Components loaded in an Eclipse workspace\|1 to 2500\| 2500 \| less
than 2500 \|\| \|Data on a dashboard\|1 to 32KB\|
\|32KB\|<https://jazz.net/library/article/641/>\| \|\<= 4.0.3: Build
definitions associated with a build engine \| 1 to 2048 \| \| less than
2048 \| <http://www-01.ibm.com/support/docview.wss?uid=swg21626864> \|

## RQM

|  |  |  |  |  |
|----|----|----|----|----|
| Dimension | ORANGE TRL ENDCOLOR | BLUE LTL ENDCOLOR | GREEN Recommendation ENDCOLOR | Notes, References |
| Concurrent users |  |  |  |  |
| Repository size |  |  |  |  |
| Index size |  |  |  |  |
| Test Case Execution Record (TCER) name length | 250 bytes |  |  | <https://jazz.net/forum/questions/123433/is-there-any-known-limitation-of-the-length-of-login-id> |
| TCERs bulk generated from test plan wizard | \## | \## | 500 | <https://jazz.net/library/article/899> |
| TCERs bulk changed/removed at once | \## | \## | \## |  |
| Records in a datapool / test data | 1 to 2000 |  |  | <https://jazz.net/jazz02/web/projects/Rational20Quality20Manager#action=com.ibm.team.workitem.viewWorkItem&id=67995> |
| Character limit: Description field of a Lab Resource | 1 to 250 |  |  | <https://jazz.net/jazz02/web/projects/Rational20Quality20Manager#action=com.ibm.team.workitem.viewWorkItem&id=106052> |
| Number of categories defined on an artifact type | 50 |  |  | <https://jazz.net/jazz02/web/projects/Rational20Quality20Manager#action=com.ibm.team.workitem.viewWorkItem&id=107113> |
| Feed entries per page \<= 4.0.4 | 500 |  |  | <https://jazz.net/forum/questions/120291/max-feed-entries-pages-cannot-be-more-than-500> |
| Feed entries per page \> 4.0.4 | 512 |  |  | <https://jazz.net/jazz02/web/projects/Rational20Quality20Manager#action=com.ibm.team.workitem.viewWorkItem&id=90564> |
| Large Record Count (SQL query result set generated by OOTB BIRT reports) ( \>= 4.0.5) |  |  | 10,000 | <http://www-01.ibm.com/support/docview.wss?uid=swg21668221> |
| Attachment size (using GUI) |  |  |  | <https://jazz.net/jazz02/web/projects/Rational20Quality20Manager#action=com.ibm.team.workitem.viewWorkItem&id=92107> |
| Attachment size (using CLI) \>=4.0 | 50 MB |  |  | <https://jazz.net/library/article/809> |
| TCERs runnable off-line and at once (\>=4.0) | 1 to 50 |  |  |  |

## RRC / RDNG

|  |  |  |  |  |
|----|----|----|----|----|
| Dimension | ORANGE TRL ENDCOLOR | BLUE LTL ENDCOLOR | GREEN Recommendation ENDCOLOR | Notes, References |
| Concurrent users \< 4.0.1 | 1 to 200 |  | less than 200 |  |
| Concurrent users \> 4.0.1 | 1 to 400 | 400 | less than 400 | <https://jazz.net/wiki/bin/view/Deployment/RationalRequirementsComposer404PerformanceReport> |
| Projects per RM/JTS instance | 1 to 200 |  | 200 | <https://jazz.net/library/article/844/> |
| Number of displayable links \> 4.0.1 | 60 (using IE7); 100 (other browsers) |  |  | <https://jazz.net/forum/questions/117541/limitation-about-the-number-of-linked-artifacts-to-be-displayed-in-rrc-403> |
| Number of artifacts selectable in the Artifact view | 50 |  |  | <https://jazz.net/forum/questions/142865/is-there-a-way-to-select-all-artifacts-in-rrc-when-you-have-more-than-50> |
| Imports to DNG from DOORS using ReqIF (\>=4.0.1) |  |  | 5000 modules; 200K objects (total) | <https://jazz.net/library/article/1243> |
| Maximum supported depth for ReqIF import | 3 | 3 | 3 | <https://jazz.net/forum/questions/93843/reqif-import-how-many-embedded-artifact-levels-are-supported> |

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: , Main.TWikiUser [additional-contributors-main.twikiuser]
