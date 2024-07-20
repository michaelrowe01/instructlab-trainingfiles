META:TOPICINFO{author="shubjit" date="1697463959" format="1.1"
version="1.16"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Configuring Single Sign On (SSO) across WebSphere Liberty Profiles [configuring-single-sign-on-sso-across-websphere-liberty-profiles]

DKGRAY Authors: Main.ShubjitNaik Build basis: Engineering Lifecycle
Management 6.0.x and 7.x ENDCOLOR

TOC{title="Page contents"}

BR

Single Sign-On (SSO) authentication is a mechanism where multiple
related but independent software applications are configured so that a
user logs in once and gains access to all systems, without the need to
re-authenticate. Rational solution for Collaborative Lifecycle
Management (CLM) supports several types of single sign-on authentication
which is listed on our online help, including our new solution
introduced with 6.x, [Jazz Security
Architecture](https://jazz.net/downloads/jazz-foundation/releases/6.0?p=news#jsa).

BRThis article will focus on configuring SSO on [WebSphere Liberty
Profile](https://developer.ibm.com/wasdev/blog/2013/03/29/introducing_the_liberty_profile).
Users can configure SSO in a distributed environment on WebSphere
Liberty by using the LTPA authentication protocol. With LTPA, a user's
login credentials are stored in a session cookie that is available for
the current browser session only. This cookie contains the LTPA token.
Users can share authentication tokens on multiple CLM applications that
are installed on different servers within the same domain.

BRFrom CLM version 6.0.1 onwards, we bundle WebSphere Liberty as the
default application server with CLM. There would be instances where
users would setup multiple Liberty Profiles to distribute CLM
applications. Following are a few scenarios :

-   *Deploy a distributed setup using WebSphere Liberty where each CLM
    application is setup on its own Liberty Profile*
-   *Deploy one or a set of applications (example DCC and JRS) on a
    separate Liberty Profile and the core CLM applications resides on
    WAS Full Profile*
-   *Adding additional application instances such as CCM1 / RQM1 / RM1
    with the bundled Liberty server connecting to JTS/CCM/RQM residing
    on WAS Full Profile or on the bundled Liberty Profile*

In the above Scenarios, it is critical to configure Single Sign-On
between these application servers such that a user only needs to log
into one of the application and subsequent access to the other
applications will not require re-authentication. BR

## Prerequisites and Assumptions

-   CLM Applications are installed and configured on WebSphere Liberty /
    Full Profiles
-   Make sure that each instance of WebSphere Liberty/Full Profile is
    using the same user registry (ideally LDAP). The user registry
    settings must be identical on all servers for SSO to work.
-   [Click here for instructions to configure the bundled Liberty
    Profile with
    LDAP](https://jazz.net/wiki/bin/view/Deployment/ConfigureLDAPforLibertyProfile)
-   [Click here for instructions to configure the WAS Full Profile with
    LDAP](https://jazz.net/wiki/bin/view/Deployment/ConfigureCLMOnWASWithLDAP)

BR

## Scenario: CLM distributed on multiple Liberty Profiles

By default Single Sign On is enabled on Liberty Profiles and when all
applications are on a single Liberty Profile there is no additional
configurations needed. If you are installing the JTS or other CLM
applications on separate Liberty servers, the servers must use the same
LTPA keys and share the same user registry BR For the bundled Liberty
instance with CLM installations, the default LTPA keys filename is
`ltpa.keys`, password is `WebAS` and location is
`[JAZZ_HOME]/server/liberty/servers/clm/resources/security`. The
ltpa.keys from Liberty server hosting JTS needs to be copied over to all
other Liberty servers running other CLM applications.

### Export/Import LTPA keys from Liberty

-   Export or copy the LTPA keys (`ltpa.keys`) from Liberty Profile
    hosting the JTS Application
-   Default Location:
    `[JAZZ_HOME]/server/liberty/servers/clm/resources/security/ltpa.keys`
-   Backup and rename the `ltpa.keys` on the Liberty Profiles hosting
    rest of the CLM applications
-   Import/Copy the `ltpa.keys` exported from the JTS server into all
    other profiles under the location
    `[JAZZ_HOME]/server/liberty/servers/clm/resources/security`
-   Restart the Liberty server

BR

In addition, review [LIberty Customizing SSO
Cookies](https://www.ibm.com/docs/en/was-liberty/nd?topic=auil-customizing-sso-configuration-using-ltpa-cookies-in-liberty)
to check if `ssoDomainNames` or `ssoUseDomainFromURL` parameters are to
be included in all your Liberty deployments. This might be needed if you
modify the default SSO cookie name.

## Scenario: CLM Distributed on WAS Full Profile and Liberty Profile

In this scenario we consider CLM is installed on WAS Full Profile and we
are now including DCC/JRS which installed using the default Liberty
Profile. Following is the procedure:

1.  *Enable SSO on WAS Full Profile hosting CLM applications* 2. *Export
    LTPA Keys from WAS Full Profile hosting the JTS application* 3.
    *Import/Replace LTPA keys to the Liberty Profile*

### Enable SSO on WAS Profile/s hosting CLM (JTS)

-   Login to the WebSphere Application Server Integration Solutions
    Console
-   Open the Global Security section from the Security menu in the left
    sidebar
-   In the Authentication section, expand Web and SIP Security
-   Click Single sign-on
-   Enter and make a note of the domain name (`example.com`)
-   Select Requires SSL
-   Click OK; then, click Save

### Export LTPA Keys from WAS Profile hosting JTS

-   Login to the WebSphere Application Server Integration Solutions
    Console
-   Open the Global Security section from the Security menu in the left
    sidebar
-   Click LTPA under the Authentication section
-   Create a new password and confirm it (example `WebAS`)
-   Enter a name for the LTPA keys (example `jtsltpa.keys`)
-   Click Export Keys to export the keys to the file system.
-   Click OK; then, click Save.
-   Move these keys to the Liberty server hosting DCC/JRS

### Import/Copy the LTPA keys to Liberty Profile

\* Copy the `jtsltpa.keys` file to the default location on Liberty
Profile hosting DCC/JRS \* Location:
`[JAZZ_HOME]/server/liberty/servers/clm/resources/security/` \* Rename
the file to ltpa.keys and restart the Liberty server \* Add the
following line in server.xml file to be able to enter the password

In addition, review [Customizing SSO Cookies in Liberty
](https://www.ibm.com/docs/en/was-liberty/nd?topic=auil-customizing-sso-configuration-using-ltpa-cookies-in-liberty)
to check if `ssoDomainNames` or `ssoUseDomainFromURL` parameters are to
be included in all your Liberty deployment. This might be needed if you
modify the default SSO cookie name.

## General Guidelines for SSO Configurations with Liberty Profile

-   Each instance of WebSphere Liberty/Full Profile server must use the
    same LTPA keys and share the same user registry.
-   The LTPA keys from the Profile hosting **JTS** application is the
    one that needs to be exported/imported into other profiles
-   If the Liberty Profiles are installed on 2 different filesystem
    types, example Windows and Linux, you may have to remove the hidden
    Windows characters post copying over the ltpa.keys on the Linux
    machine. Try one of the following:
    -   Instead of copying the file over, edit the ltpa.keys file on the
        Windows machine using Notepad, copy the content and paste it to
        a new file on the Linux machine OR
    -   If you unable to copy the contents and are forced to copy the
        file to the Linux machine, run `dos2unix` or similar commands on
        the file post copy

BR

##### Related topics: [Configure SSO on WebSphere Application Server Full Profile](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.install.doc/topics/t_deploy_single_sign-on.html), [Configure LDAP on Liberty Profile](ConfigureLDAPforLibertyProfile), [CLM Distributed Setup on Liberty Profiles](CLMDistributedSetupUsingLibertyProfile) [related-topics-configure-sso-on-websphere-application-server-full-profile-configure-ldap-on-liberty-profile-clm-distributed-setup-on-liberty-profiles]

##### External links: [IBM](https://www.ibm.com) [How to setup LTPA SSO with Liberty profile for CLM jazz.net forum post](https://jazz.net/forum/questions/224877/how-to-setup-ltpa-sso-with-liberty-profile-for-clm) [external-links-ibm-how-to-setup-ltpa-sso-with-liberty-profile-for-clm-jazz.net-forum-post]

##### Additional contributors: Main.DineshKumar, Main.PaulEllis [additional-contributors-main.dineshkumar-main.paulellis]
