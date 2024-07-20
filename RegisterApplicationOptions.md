META:TOPICINFO{author="rschoon" date="1561638728" format="1.1"
reprev="1.6" version="1.6"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# How to register applications to ELM deployments. DKGRAY Authors: [Krzysztof Kazmierczyk](Main.KrzysztofKazmierczyk), [Ralph Schoon](Main.RalphSchoon) Build basis: ELM 4.0 and later [how-to-register-applications-to-elm-deployments.-dkgray-authors-krzysztof-kazmierczyk-ralph-schoon-build-basis-elm-4.0-and-later]

ENDCOLOR

TOC{title="Page contents"}

The IBM Engineering Lifecycle Management Solutions (ELM) can be deployed
in different [topologies](StandardTopologiesOverview). ELM deployments
consist of a Jazz Team Server (JTS) and applications registered to the
JTS. This document explains how to [register applications to the JTS in
the initial
deployment](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.install.doc/topics/c_configuring_the_server.html)
and how to [add and register applications to an existing
deployment](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.repository.web.admin.doc/topics/t_register.html).

# Manual setup

The IBM Engineering Lifecycle Management Solution provides capabilities
to perform a [manual install and setup of an ELM
deployment](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.install.doc/topics/c_configuring_the_server.html).
It also provides capabilities to [manually register new applications to
an existing
deployment](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.repository.web.admin.doc/topics/t_register.html).
The following options are available when performing a manual install and
setup.

## Initial setup of a deployment

During the initial manual install process of a deployment the available
applications can be discovered and registered in the **Register
Applications** step of the initial JTS setup.

## Adding an application to an existing deployment

To manually register a new application to an existing deployment use the
**Add** button in the **Registered Applications** page of the JTS admin
web UI. The top of the page will show a prompt with a link to the setup
wizard for the application. To finalize the registration follow the link
and execute the setup wizard for the application.

## Manual setup best practices

\* Use the **Add** button in the **Registered Applications** page of the
JTS admin web UI to register a new application to an existing
deployment. Do not run the jts/setup again to register new applications
to an existing deployment.

# Automation for setup

The IBM Engineering Lifecycle Management Solution provides capabilities
to automate deploying the ELM solutions. It allows to [automate the
initial install and
setup](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.install.doc/topics/r_repotools_registerapp.html)
of ELM deployments. It also allows to automate installing and
[registering new
applications](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.install.doc/topics/r_repotools_setup.html)
to an existing deployment.

## Available commands

The following commands are available.

### repotools -setup

This command is used to setup the initial deployment of a JTS and to
register the applications initially available. This command was
introduced in version 4.0.

### repotools -registerApp

This command is used to register new applications to an ELM deployment.
This command was introduced in version 6.0.1.

## Automation Best Practices

-   Repotools -registerApp was introduced in version 6.0.1 to separate
    the registration of new applications to an existing deployment from
    the initial setup of a deployment. Since 6.0.1 repotools
    -registerApp is the only command that should be used to register a
    new application to an existing ELM deployment.

<!-- -->

-   Since 6.0.1 repotools -setup is meant to be only ever run once to
    setup the initial deployment of a JTS and associated applications.
    Do not run repotools -setup again. Especially do not run repotools
    -setup again subsequently to register new applications to an
    existing ELM deployment. Running this command again can cause
    undesired results.

# Additional information

##### Related topics: [related-topics]

-   [Standard topologies](StandardTopologiesOverview)
-   [Server rename](ServerRename)

##### External links: \* [Initial setup and configuring the server](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.install.doc/topics/c_configuring_the_server.html) [external-links-initial-setup-and-configuring-the-server]

-   [Register applications to an existing
    deployment](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.repository.web.admin.doc/topics/t_register.html).
-   [Repotools -registerApp
    command](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.install.doc/topics/r_repotools_registerapp.html)
-   [Repotools -setup
    command](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.install.doc/topics/r_repotools_setup.html)
-   [Interactive Guides for installing, upgrading, and adding
    applications](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.install.doc/topics/interactive_guides.html)
