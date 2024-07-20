META:TOPICINFO{author="mattlrx" date="1668509045" format="1.1"
version="1.7"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Silently installing on Linux or UNIX systems [silently-installing-on-linux-or-unix-systems]

DKGRAY Authors: [DanToczala](Main.DavidToczala), Main.DavidCastellanos,
Main.MatthieuLeroux Build basis: The IBM Complex Engineering solution
for Engineering Lifecycle Management (ELM) 7.x and IBM Installation
Manager 1.9.2 ENDCOLOR

TOC{title="Page contents"}

This article outlines the steps to complete a command-line driven,
silent, non-root installation of version 7.0.2 of the The IBM Complex
Engineering solution for Engineering Lifecycle Management (ELM)
applications into a supported UNIX or Linux machine with no internet
connectivity. The default application server, IBM Webesphere Liberty,
will be installed. The guidance provided here might change over time.

**Note:** This article assumes the use of IBM Installation Manager
1.9.2. The steps in this procedure were done on a 64-bit Linux machine,
but they should be relevant for other UNIX systems.

## Prerequisites

Read the [System Requirements for IBM Engineering Lifecycle Management
7.0.2](https://jazz.net/wiki/bin/view/Deployment/ELMSystemRequirements702)
and [Planning to install on UNIX and Linux
systems](https://www.ibm.com/docs/en/elm/7.0.2?topic=pielmluizs-planning-install-engineering-lifecycle-management-unix-linux-systems).

## Procedure

The installation is a simple procedure. It consists of installing IBM
Installation Manager 1.9.2, editing a response file, and using it to
install the ELM 7.0.2 package. This response file will be customized to
specify ELM 7.0.2 installation and directory settings and then be fed to
IBM Installation Manager to install ELM 7.0.2.

-   Download and extract the following files from the All Downloads
    section on [Jazz.net](http://jazz.net):
    -   `ELM-Web-Installer-Linux-7.0.2SR1.zip`
    -   `JTS-CCM-QM-RM-JRS-ENI-repo-7.0.2SR1.zip`
    -   **Note:** Extracted paths are assumed to be
        *WebInstallerExtractedPath* and *ELM-7.0.2RepoExtractedPath*
        respectively.

<!-- -->

-   Install IBM Installation Manager:
    -   cd into \_WebInstallerExtractedPath/im/linux.gtk.x86*64/*
    -   Run
        `./userinstc -installationDirectory /u/rtcadmin/IBM/IM/ -svP -acceptLicense`
    -   **Note:** Change */u/rtcadmin/IBM/IM* to your IBM Installation
        Manager target installation directory.
    -   **Note:** Use ./installc when installing as root

<!-- -->

-   Edit the ELM 7.0.2 response file.
    1.  Open the following file in a text editor:
        `WebInstallerExtractedPath/im/linux.gtk.x86_64/silent-install-server.xml` 2.
        Review the following lines: \* Line 55: Repository location for
        ELM 7.0.2 Change *../repo* to *ELM-7.0.2RepoExtractedPath* \*
        Line 62: Target ELM 7.0.2 installation directory. Change
        */tmp/silent-install/JazzTeamServer* to your installation
        directory. \* Lines 98 - 116: Specify which applications to
        install.
        -   **Note:** If you are upgrading from an older version of
            Rational Team Concert (pre 3.0) or use non-default
            application URLs, read [Choosing a different context root
            than
            default](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m3/topic/com.ibm.jazz.install.doc/topics/t_choose_different_context_root.html).

<!-- -->

-   Install ELM 7.0.2
    -   Cd into */u/rtcadmin/IBM/IM/eclipse/tools*, or your equivalent
        IBM Installation Manager installation directory
    -   Run **./imcl -input
        WebInstallerExtractedPath/im/linux.gtk.x86_64/silent-install-server.xml
        -acceptLicense -sVP**

The 7.0.2 applications for the Rational solution for CLM are now
installed and ready for use.

## Troubleshooting

If you experience some issues with the install, you can try to install
installtion manager on its own:

-   [Installation Manager and Packaging Utility download
    documents](https://www.ibm.com/support/pages/installation-manager-and-packaging-utility-download-documents)
-   [Installing or updating Installation Manager silently by using the
    installer](https://www.ibm.com/docs/en/installation-manager/1.8.5?topic=mimism-installing-updating-installation-manager-silently-by-using-installer)

If that also fails, refer to the [Issues starting or running IBM
Installation
Manager](https://www.ibm.com/support/pages/issues-starting-or-running-ibm-installation-manager)

Finally, If there are no error messages, use strace command, for
example:

-   strace ./installc -log log_file -acceptLicense
-   If using a mounted volume, try a different location

##### Related topics: [Deployment web home](DeploymentWebHome), [System Requirements for IBM Engineering Lifecycle Management 7.0.2](https://jazz.net/wiki/bin/view/Deployment/ELMSystemRequirements702), [Planning to install on UNIX and Linux systems](https://www.ibm.com/docs/en/elm/7.0.2?topic=pielmluizs-planning-install-engineering-lifecycle-management-unix-linux-systems), [Issues starting or running IBM Installation Manager](https://www.ibm.com/support/pages/issues-starting-or-running-ibm-installation-manager) [related-topics-deployment-web-home-system-requirements-for-ibm-engineering-lifecycle-management-7.0.2-planning-to-install-on-unix-and-linux-systems-issues-starting-or-running-ibm-installation-manager]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.BenjaminTran [additional-contributors-main.benjamintran]
