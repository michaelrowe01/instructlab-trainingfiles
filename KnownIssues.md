META:TOPICINFO{author="d3v3r1tt" date="1437760609" format="1.1"
version="1.29"} META:TOPICPARENT{name="CLMUpgradeTroubleshooting"}

# Items to consider before upgrading [items-to-consider-before-upgrading]

Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam) Build
basis: CLM 4.x, CLM 5.x ENDCOLOR

TOC{title="Page contents"}

Before upgrading, it is important to consider known issues on each
version to validate if this will cause any issues.

# Items to consider before upgrading

It is important to understand the defects associated with your
deployment that might not be resolved or included in the version you are
upgrading to. Ensure that this will not affect your users after you
upgrade.

## Defects fixed in specific product release

Below is a list of queries you can run on Jazz.net to validate which
defects were resolved in the latest releases. \| \| **Rational Team
Concert** \| **Rational Quality Manager** \| **Rational DOORS NG** \|
**Rational Jazz Foundation** \| \| APAR related Defects resolved in the
release \| [RTC
4.0.7](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.workitem.runSavedQuery&id=_3OWRrgd4EeScusBHOj7kTg)[RTC
5.0.2](https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.runSavedQuery&id=_72kPoC3oEeSv1PLrFzJHAg&tq)[RTC
6.0](https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.runSavedQuery&id=_zm2XUXDzEeSXbqAAJhWI1g)
\| [RQM
4.0.7](https://jazz.net/jazz02/web/projects/Rational20Quality20Manager#action=com.ibm.team.workitem.runSavedQuery&id=_HIVN4KUoEeOv35RHgfafDw)[RQM
5.0.2](https://jazz.net/jazz02/web/projects/Rational20Quality20Manager#action=com.ibm.team.workitem.runSavedQuery&id=_CVd8JTPQEeSp3ZV9kbQyqg)[RQM
6.0](https://jazz.net/jazz02/web/projects/Rational20Quality20Manager#action=com.ibm.team.workitem.runSavedQuery&id=_3ASJsEhhEeSxz--A8sIA7g)
\| [RRC
4.0.7](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.runSavedQuery&id=_6zcgsP4PEeO8_eJPOih81Q)[RDNG
5.0.2](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.runSavedQuery&id=_hFVqoTdxEeSuD-k_WiY3-A)[RDNG
6.0](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.runSavedQuery&id=_Yy-AkXp0EeShILBQkrF6Hw)\|
[JFS
4.0.7](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.runSavedQuery&id=_BUqgrghFEeScusBHOj7kTg)[JFS
5.0.2](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.runSavedQuery&id=_6dirK2anEeSXbqAAJhWI1g)[JFS
6.0](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.runSavedQuery&id=_2y-9kALqEeWFGcjYk3ZxAA)
\|

|  |  |  |  |  |
|----|----|----|----|----|
| Non-APAR related Defects resolved in the release | [RTC 4.0.7](https://jazz.net/jazz/web/projects/Jazz20Collaborative20ALM#action=com.ibm.team.workitem.runSavedQuery&id=_sSytkgd5EeScusBHOj7kTg)[RTC 5.0.2](https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.runSavedQuery&id=_P8ZVcC3pEeSv1PLrFzJHAg)[RTC 6.0](https://jazz.net/jazz/web/projects/Rational20Team20Concert#action=com.ibm.team.workitem.runSavedQuery&id=_KSGAMnD0EeSXbqAAJhWI1g) | [RQM 4.0.7](https://jazz.net/jazz02/web/projects/Rational20Quality20Manager#action=com.ibm.team.workitem.runSavedQuery&id=_iCtxNggDEeS0ddSSMadJWA)[RQM 5.0.2](https://jazz.net/jazz02/web/projects/Rational20Quality20Manager#action=com.ibm.team.workitem.runSavedQuery&id=_QRm_wDgWEeSSFt3nsbDiuQ)[RQM 6.0](https://jazz.net/jazz02/web/projects/Rational20Quality20Manager#action=com.ibm.team.workitem.runSavedQuery&id=_ITWM8UhiEeSxz--A8sIA7g) | [RRC 4.0.7](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.runSavedQuery&id=_UTzVgP4QEeO8_eJPOih81Q)[RDNG 5.0.2](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.runSavedQuery&id=_OehEATdyEeSuD-k_WiY3-A)[RDNG 6.0](https://jazz.net/jazz03/web/projects/Requirements20Management#action=com.ibm.team.workitem.runSavedQuery&id=_uXiVRXp0EeShILBQkrF6Hw) | [JFS 4.0.7](https://jazz.net/jazz/resource/itemOid/com.ibm.team.workitem.query.QueryDescriptor/_d4PZcAeCEeScusBHOj7kTg)[JFS 5.0.2](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.runSavedQuery&id=_m0TlQGaoEeSXbqAAJhWI1g)[JFS 6.0](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.runSavedQuery&id=_M5Ob8ALrEeWFGcjYk3ZxAA) |

For defects resolved in other versions, check the release notes for that
particular release.

|  |  |  |
|----|----|----|
| [Rational Team Concert](https://jazz.net/downloads/rational-team-concert/releases/) | [Rational Quality Manager](https://jazz.net/downloads/rational-quality-manager/releases/) | [Rational Requirements Composer/ Rational DOORS NG](https://jazz.net/downloads/rational-requirements-composer/releases/) |

## Known issues

### Known issues when upgrading to 4.0.1 or later

#### Incorrect indexes in 4.0.1 (resolved in 4.0.2)

There is a known defect with indexes upon upgrading to **4.0.1** as
identified in [Technote 1620879: Upgrades to 4.0.1 create a
significantly larger, incorrect
index](http://www-01.ibm.com/support/docview.wss?uid=swg21620879). A
Testfix is required before upgrading, but this defect has been resolved
in [version
4.0.2](https://jazz.net/downloads/rational-team-concert/releases/4.0.2).
Upgrade to the latest release of the Rational solution for Collaborative
Lifecycle Management (CLM) to ensure that defects to all known issues
have been resolved.

#### Upgrade Scripts fail with Microsoft SQL Server and CLM Upgrade to 4.0.4 (resolved in 4.0.5)

There is a known issue where the upgrade scripts will fail during an
upgrade to CLM **4.0.4**. This is documented in [Technote 1649768:
Upgrading CLM products to version 4.0.4 fails when using Microsoft SQL
Server](http://www-01.ibm.com/support/docview.wss?uid=swg21649768). This
defect has been resolved in [version
4.0.5](https://jazz.net/downloads/rational-team-concert/releases/4.0.5).

#### Work Items can not be loaded in RTC web client after upgrade to CLM **4.0.5** and above (resolved in 5.0.2)

After upgrading to CLM 4.0.5 or above, some Work Items can not be loaded
in RTC web client. This problem only occurs in the web client and is
caused by too many attributes in the Work Item type. This is due to the
change made to the way to batch value sets starting in version 4.0.5.
This defect has been resolved in [version
5.0.2](https://jazz.net/downloads/rational-team-concert/releases/5.0.2).

### Known issues when upgrading to 5.0 or later

#### All Project Areas are deleted after upgrade from RRC or RDNG release 4.0.x

There is a known defect that all project areas are deleted upon
upgrading RRC or RDNG 4.0.x to **5.0.x**. Refer to [Technote 1695623:
All Project Areas are deleted after upgrade from RRC or RDNG release
4.0.x](http://www.ibm.com/support/docview.wss?uid=swg21695623) for more
information.

#### LPA templates may not be retrieved after an upgrade to 5.0.2 (fixed in 5.0.2 iFix002)

There is a known defect affecting sites where a server rename was
performed on the upgrade server before being upgraded to CLM **5.0.2**
as described in [Technote 1693288: CLM LPA templates may not be
retrieved after a migration from older release to
5.0.2](http://www.ibm.com/support/docview.wss?uid=swg21693288). The
defect has been resolved in [version 5.0.2
iFix002](http://www.ibm.com/support/docview.wss?uid=swg21695923).

## Known Workarounds

Known workarounds when upgrading to 4.0.7 or later are discussed below.
\| \| **Rational Team Concert** \| **Rational Quality Manager** \|
**Rational Requirements Composer** \| **Rational Jazz Foundation** \| \|
Documented Workarounds \| [RTC
4.0.7](https://jazz.net/library/#q=&tag=workaround,4.0.7&project=rational-team-concert)[RTC
5.0.2](https://jazz.net/library/#q=&tag=workaround2C5.0.2&project=rational-team-concert&sort=pubDate)[RTC
6.0](https://jazz.net/library/#q=&tag=workaround2C6.0&project=rational-team-concert&sort=pubDate)
\| [RQM
4.0.7](https://jazz.net/library/#q=&tag=workaround,4.0.7&project=rational-quality-manager)[RQM
5.0.2](https://jazz.net/library/#q=&tag=workaround2C5.0.2&project=rational-quality-manager&sort=pubDate)[RQM
6.0](https://jazz.net/library/article/1509) \| [RRC
4.0.7](https://jazz.net/library/#q=&tag=workaround,4.0.7&project=rational-requirements-composer)[RDNG
5.0.2](https://jazz.net/library/#q=&tag=workaround2C5.0.2&project=rational-doors-next-generation&sort=pubDate)[RDNG
6.0](https://jazz.net/library/article/1516) \| [JFS
4.0.7](https://jazz.net/library/#q=&tag=workaround,4.0.7&project=jazz-foundation)[JFS
5.0.2](https://jazz.net/library/#q=&tag=workaround2C5.0.2&project=jazz-foundation&sort=pubDate)[JFS
6.0](https://jazz.net/library/#q=&tag=workaround2C6.0&project=jazz-foundation&sort=pubDate)
\|

##### Related topics: [related-topics]

\* For more upgrading troubleshooting topics, refer to [Upgrade
troubleshooting](UpgradeTroubleshooting).

##### External links: \* IBM: None [external-links-ibm-none]

##### Additional contributors: Main.StephanieBagot, Main.DianeEveritt [additional-contributors-main.stephaniebagot-main.dianeeveritt]
