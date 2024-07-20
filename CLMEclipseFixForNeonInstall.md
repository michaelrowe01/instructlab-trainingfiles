META:TOPICINFO{author="websmith" date="1508252679" format="1.1"
reprev="1.1" version="1.1"} META:TOPICPARENT{name="WebPreferences"}

# Installing Rational Team Concert from P2 on Eclipse Neon or later DKGRAY Authors: Main.LarrySmith [installing-rational-team-concert-from-p2-on-eclipse-neon-or-later-dkgray-authors-main.larrysmith]

Build basis: Rational Team Concert 6.0 and later, Eclipse 4.6 and later.
ENDCOLOR

TOC{title="Page contents"}

When installing the Rational Team Concert using the process of
downloading Eclipse then installing from the RTC P2 repository, a
special process must be followed to first install the Eclipse GEF
component.

------------------------------------------------------------------------

## Rational Team Concert installation

With Collaborative Lifecycle Manager the Rational Team Concert (RTC)
client can be installed in Eclipse either by using Installation manager,
or by adding features from an Eclipse P2 repository file into an
existing or new Eclipse installation. When the installed version is
Eclipse 4.6 (Neon), 4.7 (Oxygen), or later, the Eclipse GEF component
must be installed before installing RTC.

### Installing RTC into Eclipse 4.6 and later from P2

The steps to install are:

1\) Download Eclipse 4.6 (Neon) or 4.7 (Oxygen). Install Eclipse.

2\) Download the RTC P2 repository from the jazz.net or other site.

3\) Start Eclipse. Use the Install New Software action from the menu and
select the Eclipse update site such as
download.eclipse.org/releases/neon/ or
download.eclipse.org/releases/oxygen/.

4\) Select Eclipse GEF and install it. Restart Eclipse. Now it is
possible to install from the RTC P2 repository update site.

5\) Select Install New Software, Install From Archive, and select the P2
repository. Restart Eclipse.

Rational Team Concert should be available in the Eclipse client. To
verify, open the Work Items perspective.

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [CLM Download](https://jazz.net/downloads/clm)
-   [Eclipse Home](https://www.eclipse.org)

##### Additional contributors: Main.LarrySmith [additional-contributors-main.larrysmith]
