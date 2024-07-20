META:TOPICINFO{author="shaileesinha" date="1710319383" format="1.1"
version="1.66"}

# WEB Web Preferences [web-web-preferences]

ENDCOLOR

The following settings are ***web preferences*** of the
[WEB](WEB.HOMETOPIC) web. These preferences overwrite the ***site-level
preferences*** in [TWIKIWEB.WIKIPREFSTOPIC](TWIKIWEB.WIKIPREFSTOPIC) and
[LOCALSITEPREFS](LOCALSITEPREFS), and can be overwritten by ***user
preferences*** (your personal topic, eg: MAINWEB.TWikiGuest in the
[MAINWEB](MAINWEB.HOMETOPIC) web).

TOC

## Web Preferences Settings

These settings override the defaults for this web only. See [full list
of defaults with
explanation](TWIKIWEB.TWikiPreferences#DefaultWebPreferences).

-   Web settings:
    -   Set SKIN = pattern
    -   Set WEBTOPICLIST = [Users](WIKIUSERSTOPIC) SEP
        [Groups](TWikiGroups) SEP [Changes](WebChanges) SEP
        [Index](WebIndex) SEP [Search](WebSearch) SEP Go
    -   Set WEBBGCOLOR = \#FFF0CE
    -   Set SITEMAPWHAT = Welcome to WIKITOOLNAME...
        [Users](WEB.WIKIUSERSTOPIC), [Groups](WEB.TWikiGroups)
    -   Set SITEMAPUSETO = ...see who is registered on this TWiki
    -   Set SITEMAPLIST = on
    -   Set BROADCASTMESSAGE =
    -   Set USERSTYLEURL =
        <https://jazz.net/wiki/pub/Deployment/WebPreferences/deployment.css>
    -   Set DISABLEDPLUGINS = WysiwygPlugin,SmiliesPlugin
    -   Set EXTERNALLINKSICON = off

<!-- -->

-   Default template for **new topics** for this web:
    -   WebTopicEditTemplate: Default template for new topics in this
        web. (Site-level is used if topic does not exist)
    -   [TWIKIWEB.WebTopicEditTemplate](TWIKIWEB.WebTopicEditTemplate):
        Site-level default topic template

<!-- -->

-   Comma separated list of **forms** that can be attached to topics in
    this web. See TWIKIWEB.TWikiForms for more information.
    -   Set WEBFORMS = UserForm

<!-- -->

-   Color preferences:
    -   Set DKGRAY =

<!-- -->

-   Copyright notice:
    -   Set WEBCOPYRIGHT = MAKETEXT{"Copyright &© by IBM and non-IBM
        contributing authors. All material on this collaboration
        platform is the property of the contributing authors."
        args="1999-GMTIME{\$year}"} Contributions are governed by our
        Terms of Use. Please read the following
        [disclaimer](https://jazz.net/wiki/bin/view/Deployment/DeploymentWikiDisclaimer).

<!-- -->

-   Users or groups who ***are not*** / ***are*** allowed to ***view***
    / ***change*** / ***rename*** topics in the WEB web: (See
    TWIKIWEB.TWikiAccessControl). Remove the \# to enable any of these
    settings. Remember that an empty setting is a valid setting; setting
    DENYWEBVIEW to nothing means that anyone can view the web.
    -   Set DENYWEBVIEW =
    -   Set ALLOWWEBVIEW =
    -   Set DENYWEBCHANGE =
    -   Set ALLOWWEBCHANGE = Main.TWikiDeploymentAuthorsGroup,
        Main.TWikiAdminGroup
    -   Set DENYWEBRENAME =
    -   Set ALLOWWEBRENAME = Main.TWikiAdminGroup,
        Main.TWikiDeploymentAuthorsGroup

<!-- -->

-   Users or groups allowed to change or rename this TOPIC topic: (e.g.,
    MAINWEB.TWikiAdminGroup)
    -   Set ALLOWTOPICCHANGE = Main.TWikiAdminGroup, Main.StevenBeard,
        Main.MichaelAfshar
    -   Set ALLOWTOPICRENAME = Main.TWikiAdminGroup, Main.StevenBeard,
        Main.MichaelAfshar
    -   Set ATTACHFILESIZELIMIT = 50000

<!-- -->

-   Web preferences that are **not** allowed to be overridden by user or
    topic preferences:
    -   Set FINALPREFERENCES = NOSEARCHALL, WIKIWEBMASTER, WEBCOPYRIGHT,
        WEBTOPICLIST, DENYWEBVIEW, DENYWEBCHANGE, ALLOWWEBCHANGE,
        DENYWEBRENAME, ALLOWWEBRENAME

INCLUDE{TWIKIWEB.WebPreferencesHelp}

META:FILEATTACHMENT{name="deployment.css" attachment="deployment.css"
attr="" comment="" date="1385165415" path="deployment.css" size="1664"
user="sbeard" version="38"}
META:FILEATTACHMENT{name="home-bottom-clouds2.jpg"
attachment="home-bottom-clouds2.jpg" attr="h" comment=""
date="1367508257" path="home-bottom-clouds2.jpg" size="61222"
user="sbeard" version="4"} META:FILEATTACHMENT{name="blue-wash-box.png"
attachment="blue-wash-box.png" attr="h" comment="" date="1366398492"
path="blue-wash-box.png" size="19288" user="sbeard" version="1"}
META:FILEATTACHMENT{name="TLASE.jpg" attachment="TLASE.jpg" attr="h"
comment="" date="1368035542" path="TLASE.jpg" size="30577" user="sbeard"
version="4"} META:FILEATTACHMENT{name="DP.jpg" attachment="DP.jpg"
attr="h" comment="" date="1368035564" path="DP.jpg" size="30866"
user="sbeard" version="7"} META:FILEATTACHMENT{name="Users.jpg"
attachment="Users.jpg" attr="h" comment="" date="1368035594"
path="Users.jpg" size="24917" user="sbeard" version="4"}
META:FILEATTACHMENT{name="rational-team-concert-52.png"
attachment="rational-team-concert-52.png" attr="h" comment=""
date="1366414835" path="rational-team-concert-52.png" size="9145"
user="sbeard" version="1"} META:FILEATTACHMENT{name="community-img.gif"
attachment="community-img.gif" attr="h" comment="" date="1366416295"
path="community-img.gif" size="4111" user="sbeard" version="1"}
META:FILEATTACHMENT{name="contentuser_banner.gif"
attachment="contentuser_banner.gif" attr="h" comment=""
date="1366455352" path="contentuser_banner.gif" size="3542"
user="sbeard" version="1"} META:FILEATTACHMENT{name="information.png"
attachment="information.png" attr="h" comment="" date="1366455805"
path="information.png" size="4256" user="sbeard" version="1"}
META:FILEATTACHMENT{name="jazz.png" attachment="jazz.png" attr="h"
comment="" date="1367067141" path="jazz.png" size="4305" user="sbeard"
version="1"} META:FILEATTACHMENT{name="todo.png" attachment="todo.png"
attr="h" comment="" date="1367975735" path="todo.png" size="5990"
user="sbeard" version="4"} META:FILEATTACHMENT{name="new.png"
attachment="new.png" attr="h" comment="" date="1367975635"
path="new.png" size="4651" user="sbeard" version="2"}
META:FILEATTACHMENT{name="uc.png" attachment="uc.png" attr="h"
comment="" date="1367975610" path="uc.png" size="5861" user="sbeard"
version="2"} META:FILEATTACHMENT{name="constantchange.png"
attachment="constantchange.png" attr="h" comment="" date="1367975709"
path="constantchange.png" size="6883" user="sbeard" version="2"}
META:FILEATTACHMENT{name="updated.png" attachment="updated.png" attr="h"
comment="" date="1367975591" path="updated.png" size="5673"
user="sbeard" version="2"} META:FILEATTACHMENT{name="RTC_48.png"
attachment="RTC_48.png" attr="h" comment="" date="1367662085"
path="RTC_48.png" size="2821" user="sbeard" version="1"}
META:FILEATTACHMENT{name="constantchange16.png"
attachment="constantchange16.png" attr="h" comment="" date="1368035977"
path="constantchange16.png" size="1148" user="sbeard" version="1"}
META:FILEATTACHMENT{name="new16.png" attachment="new16.png" attr="h"
comment="" date="1368035994" path="new16.png" size="1202" user="sbeard"
version="1"} META:FILEATTACHMENT{name="todo16.png"
attachment="todo16.png" attr="h" comment="" date="1368036012"
path="todo16.png" size="1079" user="sbeard" version="1"}
META:FILEATTACHMENT{name="uc16.png" attachment="uc16.png" attr="h"
comment="" date="1368036033" path="uc16.png" size="1168" user="sbeard"
version="1"} META:FILEATTACHMENT{name="updated16.png"
attachment="updated16.png" attr="h" comment="" date="1368036050"
path="updated16.png" size="1148" user="sbeard" version="1"}
META:FILEATTACHMENT{name="deploy_50.png" attachment="deploy_50.png"
attr="h" comment="" date="1386204528" path="deploy_50.png" size="5475"
user="sbeard" version="1"} META:FILEATTACHMENT{name="topology.png"
attachment="topology.png" attr="h" comment="" date="1417552408"
path="topology.png" size="78300" user="mafshar" version="1"}
META:FILEATTACHMENT{name="GrayExtendingIcon.png"
attachment="GrayExtendingIcon.png" attr="h" comment="" date="1417552824"
path="GrayExtendingIcon.png" size="3634" user="mafshar" version="1"}
META:FILEATTACHMENT{name="GrayPerformanceIcon.png"
attachment="GrayPerformanceIcon.png" attr="h" comment=""
date="1417552839" path="GrayPerformanceIcon.png" size="6278"
user="mafshar" version="1"}
META:FILEATTACHMENT{name="GraySecurityIcon.png"
attachment="GraySecurityIcon.png" attr="h" comment="" date="1417552856"
path="GraySecurityIcon.png" size="4181" user="mafshar" version="1"}
META:FILEATTACHMENT{name="GrayServiceabilityIcon.png"
attachment="GrayServiceabilityIcon.png" attr="h" comment=""
date="1417552872" path="GrayServiceabilityIcon.png" size="5314"
user="mafshar" version="1"} META:FILEATTACHMENT{name="cellBG.gif"
attachment="cellBG.gif" attr="h" comment="" date="1418064335"
path="cellBG.gif" size="1386" user="mafshar" version="1"}
META:FILEATTACHMENT{name="topology2.png" attachment="topology2.png"
attr="h" comment="" date="1418065314" path="topology2.png" size="79311"
user="mafshar" version="1"}
