META:TOPICINFO{author="din" date="1707386301" format="1.1"
version="1.6"} META:TOPICPARENT{name="UpgradePlanning"}

# Expedite your WAS configuration to minimize down time for a CLM upgrade DKGRAY Authors: Main.MikeDelargy, Main.ShradhaSrivastav, Main.DineshKumar [expedite-your-was-configuration-to-minimize-down-time-for-a-clm-upgrade-dkgray-authors-main.mikedelargy-main.shradhasrivastav-main.dineshkumar]

Build basis: CLM Versions 3.x and later, up to and including ELM 7.0.2.
ENDCOLOR

TOC{title="Page contents"}

`Note: Support removed for IBM !WebSphere Application Server (Traditional WAS) with ELM version 7.0.3. Use !WebSphere Liberty, either embedded and installed with ELM applications, or separately installed`

Upgrading your CLM environment can be a time consuming process when
properly done. The process typically begins with good planning and
testing which can be used to help find challenges and minimize down time
during a production system upgrade.

A clm upgrade may involve upgrading a combination of things:

1.  The CLM Applications
2.  Operating Systems
3.  Browsers
4.  Database Versions
5.  WebSphere versions

Additionally, with any CLM upgrade when the application is hosted on
WebSphere Application Server (WAS) , part of the upgrade process is to
uninstall the old application war files, clean out the caches for these
war files, install the new war files, and reconfigure the security for
the new war files.

**Clearly, your applications must be down in order for this process to
occur.**

**The purpose of this article is to offer a configuration that minimizes
the downtime during an upgrade.**

## Typical war file steps during an upgrade.

-   From our CLM upgrade guide:

[Upgrading to version
5.0.2](http://www-01.ibm.com/support/knowledgecenter/SSYMRC_5.0.2/com.ibm.jazz.install.doc/topics/roadmap_clm_upgrade.html)

Step 5 Back up the WebSphere Application Server profile

Step 6 Uninstall the previously installed applications from WebSphere
Application Server

Step 7 Update the JAZZ_HOME and log4j.configuration custom properties

Step 8 Stop WebSphere Application Server

Step 9 Clean up the WebSphere Application Server temp directories

Step 10 Clean up the logs directory

Steps 11-14 are not related to WebSphere

Step 15 Deploy the version 5.x WAR files in WebSphere Application Server
I) Install the war files II) Map Security roles appropriately

**During each of these steps, your application server is down and cannot
be used.**

### Alternate route to minimize the down time of your application server during an upgrade:

An alternate approach to preparing for and implementing an upgrade is to
create a second Profile / jvm in WebSphere that can be used specifically
for your upgraded solution.

The benefits of using a second jvm for your upgraded solution:

1.  It can be prepared well in advance of your actual upgrade and your
    system can be up and running while the new jvm is being configured.
2.  You do not need to uninstall the old war files, clean up the old
    cache, nor remove the old logs.
3.  in the unlikely event that you need to abort the upgrade, you can
    easily revert to the pre-upgrade deployment.

**This can save a tremendous amount of time**

### Creating a second profile / jvm in WebSphere

1.  You can use the WebSphere Profile Management Tool to create your new
    profile.
2.  When you create the new profile, the tool will automatically
    increment the ports being used by one. Therefore, if your original
    deployment is using ports 9080 and 9443, your new profile will use
    ports 9081 and 9443. RED *(These must be changed at a later time
    when you are ready to do the upgrade.)* ENDCOLOR
3.  You can follow the steps outlined in the [Configuring CLM on
    WebSphere Application Server with
    LDAP](https://jazz.net/wiki/bin/view/Deployment/ConfigureCLMOnWASWithLDAP)
    to configure your new jvm. RED *(You want to make sure your custom
    property settings match your current production settings.)* ENDCOLOR
    \* Depending on the resources available on the Operating System you
    may have to minimize the initial settings for the min heap (-xms),
    max heap (-xmx), and nursery (-xmn) until it is time to switch over
    to the new jvm. If you have sufficient resources available, then you
    can set these custom settings to match your current deployment. \*
    After installing each of the new war files, you can manually set the
    security to user/group mapping, or you can run the python scripts to
    do this for you. More information on these can be found here:
    [Automatically deploying the Collaborative Lifecycle Management
    applications on WebSphere Application
    Server](https://jazz.net/wiki/bin/view/Deployment/AutomatedScriptsForDeployingCLMOnWAS)

## Changing port numbers for your new jvm

-   To change ports in WebSphere, go to the ibm admin console and select
    Servers / Server Types / WebSphere application server then click on
    your server. (my server is server1)

\*

-   Next, on the right, select Ports \*

<!-- -->

-   The port numbers from my 'new profile are 9444 and 9081 \*

<!-- -->

-   but my current deployment uses 9443 and 9080 so I need to change the
    values. \*

<!-- -->

-   When done, I need to save my changes and restart the profile \*

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]

META:FILEATTACHMENT{name="new_info.png" attachment="new_info.png"
attr="h" comment="" date="1423078729" path="new_info.png" size="34729"
user="msdelarg" version="1"} META:FILEATTACHMENT{name="old_value.png"
attachment="old_value.png" attr="h" comment="" date="1423078743"
path="old_value.png" size="40919" user="msdelarg" version="1"}
META:FILEATTACHMENT{name="port_section.png"
attachment="port_section.png" attr="h" comment="" date="1423078757"
path="port_section.png" size="48970" user="msdelarg" version="1"}
META:FILEATTACHMENT{name="save.png" attachment="save.png" attr="h"
comment="" date="1423078770" path="save.png" size="25571"
user="msdelarg" version="1"} META:FILEATTACHMENT{name="server1.png"
attachment="server1.png" attr="h" comment="" date="1423078784"
path="server1.png" size="44222" user="msdelarg" version="1"}
