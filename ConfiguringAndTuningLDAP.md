META:TOPICINFO{author="sbeard" date="1422035663" format="1.1"
version="1.10"} META:TOPICPARENT{name="DeploymentAdminstering"}

# Configuring and tuning Lightweight Directory Access Protocol (LDAP) [configuring-and-tuning-lightweight-directory-access-protocol-ldap]

DKGRAY Authors: [DanToczala](Main.DavidToczala) Build basis: CLM 2011
(product versions 3.x) and later ENDCOLOR

TOC{title="Page contents"}

LDAP configuration should be relatively straightforward in most cases.

## Common LDAP mistakes

-   Some customers have seen poor performance when they use LDAP
    authentication using an LDAP resource that is remote and has a poor
    connection to the Jazz infrastructure. Long latency between your
    LDAP resource and the Jazz deployment can lead to lengthy login
    times, and odd Jazz application "stalls", when the user needs to be
    reauthenticated.
-   Keep in mind that you have the ability to modify the LDAP queries
    used to authenticate users in the Jazz Team Server (JTS)
    administration console.
-   The nightly synchronization of user data between the LDAP repository
    and the JTS uses the LDAP queries specified in the JTS
    administration console

## Debugging LDAP issues

Seeing strange LDAP behavior? If you are on Windows, try the [free
Softera LDAP browser](http://www.ldapbrowser.com/download.htm). It will
allow you to see and visualize what is going on with the LDAP in the
customer environment. If your customer is using Linux, try the [Luma
LDAP browser](http://luma.sourceforge.net/download.html) out on
SourceForge.

##### Related topics: None [related-topics-none]

##### External links: \* None [external-links-none]

##### Additional contributors: None [additional-contributors-none]

META:TOPICMOVED{by="sbeard" date="1385850681"
from="Deployment.TuningLDAP" to="Deployment.ConfiguringAndTuningLDAP"}
