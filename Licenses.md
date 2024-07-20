META:TOPICINFO{author="rnaranjo" date="1701191203" format="1.1"
version="1.19"} META:TOPICPARENT{name="CLMUpgradeTroubleshooting"}

# Licenses [licenses]

DKGRAY Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam)
Build basis: ELM 7.x and later ENDCOLOR

TOC{title="Page contents"}

This page discusses common issues seen with licenses when upgrading ELM
applications.

## License compatibility

All licenses are hosted by the Jazz Team Server in a deployment unless
you are using token licenses with the IBM Common Licensinging Server.
Jazz Team Server version 7.x can host floating, token and authorized
user licenses single install. Therefore, if you decide to do an
incremental upgrade, the JTS Application *must* be upgraded first.

ELM 7.0.3 improves security by upgrading the cyphers used in licenses.
Older licenses from ELM 7.0.2 and earlier will not work in ELM 7.0.3 and
you must obtain new licenses when you install or upgrade to ELM 7.0.3.
The names, types, and permissions of ELM 7.0.3 licenses are unchanged
from previous ELM 7.x licenses. Request new licenses through the IBM
License Key Center or Passport Advantage as you normally would. See [IBM
Support -
Licensing](https://www.ibm.com/support/pages/ibm-support-licensing-start-page)

## Upgrade process for licenses

Previous versions of ELM licenses (floating, token or authorized user
single install) can be upgraded to current versions by installing its
current version license counterpart. Essentially, this means importing
the new license JAR or ZIP file which will overwrite the existing older
license. Existing user assignments of each license are maintained after
upgrading except in the following situations:

-   If different license types (for example, token licenses) are
    installed, than the user license assignments must be manually
    updated for the license types used in the older license version (for
    example, floating).
-   License prior to ELM 7.0.3 cannot be installed in ELM 7.0.3 so the
    user assignments must be re-set when upgrading to 7.0.3.

##### External links: [external-links]

-   [Licensing in the Rational solution for Collaborative Lifecycle
    Management (CLM) 2012](https://jazz.net/library/article/825/)
-   [Token Licensing for Jazz based
    products](https://jazz.net/library/article/559)

##### Additional contributors: Main.SusanWu Main.JimRuehlin Main.RosaNaranjo [additional-contributors-main.susanwu-main.jimruehlin-main.rosanaranjo]
