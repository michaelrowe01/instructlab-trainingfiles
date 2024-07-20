META:TOPICINFO{author="rrakich" date="1604064477" format="1.1"
reprev="1.10" version="1.10"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Installing Link Index Provider (LDX) on its own Server DKGRAY Authors: Richard Watts Build basis: 6.0.6.1 and later [installing-link-index-provider-ldx-on-its-own-server-dkgray-authors-richard-watts-build-basis-6.0.6.1-and-later]

ENDCOLOR

TOC{title="Page contents"}

RED **This wiki article has been superseded by this tech note:
<https://www.ibm.com/support/pages/node/6348196>** ENDCOLOR

When we introduced the Link Index Provider (LDX) as part of the
Configuration Management (CM) feature set, we decided to reduce
complexity and install it along with the Jazz Team Server (JTS) on the
same server. By doing this, we made the configuration largely invisible
to our customers. This eliminated configuration complexity but it meant
that the two applications share the single server resources. If you have
a large CM enabled deployment, you might want to separate the two,
putting LDX on its own server. This document describes how to do that.

The Link Index Provider is a dedicated instance of Lifecycle Query
Engine (LQE) which has been configured to provide a subset of the
information that the traditional LQE provides. When moving LDX to its
own server, we are deploying LDX in exactly the same way we would deploy
LQE, but we tell the Jazz Team Server that we will be using it in an LDX
capacity.

## Implications

When you move LDX to its own server, the Jazz Team Server will not be
able to configure LDX automatically. You (the administrator) will need
to configure LDX yourself. This process is exactly the same as
configuring the [Lifecycle Query Engine
(LQE)](https://www.ibm.com/support/knowledgecenter/en/SSYMRC_6.0.6/com.ibm.team.jp.lqe2.doc/topics/t_lqe_admin.html).
Specifically, you will need to add the [TRS feeds
yourself](https://www.ibm.com/support/knowledgecenter/en/SSYMRC_6.0.6/com.ibm.team.jp.lqe2.doc/topics/t_lqe_data_sources.html).

If you are migrating an existing deployment, you should consider backing
up the existing data before moving LDX to its own server. These steps
are covered in migration steps (which is only required if moving from an
existing deployment).

## (Optional) Migration Steps

1.  [Backup
    LDX](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.team.jp.lqe2.doc/topics/t_lqe_backup.html)
2.  [Unregister
    LDX](https://www.ibm.com/support/knowledgecenter/en/SSYMRC_6.0.6.1/com.ibm.jazz.repository.web.admin.doc/topics/t_manage_reg_apps.html)
3.  Shutdown all servers
4.  Go to deployment steps below

## Deployment Steps

1.  [Install
    Liberty](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_inst_kernel_zip.html)
2.  [Install Security
    Certificates](https://www.ibm.com/support/knowledgecenter/en/SSYMRC_6.0.6/com.ibm.jazz.install.doc/topics/t_install_server_certificates.html)
3.  [Deploy LDX on
    Liberty](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_dep.html)
4.  (Optional) [Enable Single Sign On for
    LDX](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.team.jp.lqe2.doc/topics/t_lqe_enable_sso.html)
5.  Start all servers
6.  (Optional) [Restore
    LDX](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.team.jp.lqe2.doc/topics/t_lqe_backup.html)
    (See Restoring LQE from a backup directory)
7.  [Register
    LDX](https://www.ibm.com/support/knowledgecenter/en/SSYMRC_6.0.6.1/com.ibm.jazz.repository.web.admin.doc/topics/t_register.html)
    with the Jazz Team Server (where the discovery url would be
    `https://qualified.hostname.com:9443/ldx/scr`)
8.  (Optional) [Add TRS
    Feeds](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.team.jp.lqe2.doc/topics/t_lqe_data_sources.html)
    (where the LDX Admin url would be
    `https://qualified.hostname.com:9443/ldx/web/admin/data-sources`)

## Configure Jazz Team Server

One you have moved the Link Index Provider to its own server, you will
need to tell the Jazz Team Server (JTS) where you put it. By default, we
assume it is on the same server as the JTS. You will need to change that
in the advanced properties.

1.  Navigate to the Jazz Team Server Advanced Properties
    (`https://qualified.hostname.com:9443/jts/admin`)
2.  Select **Manage Server**
3.  Select **Advanced Properties**
4.  Locate (In your browser use the find feature to locate
    `com.ibm.team.links.service.internal.LinkIndexService`)
5.  Edit the property Link Index Provider URL
    (`https://qualified.hostname.com:9443/ldx`)
6.  Save your changes

## Resources

-   [Configuring LDX using Properties
    Files](https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.6.1/com.ibm.team.jp.lqe2.doc/topics/t_lqe_properties_files.html)

##### Related topics: [Installing & Upgrading](DeploymentInstallingUpgradingAndMigrating), [Deployment web home](DeploymentWebHome) [related-topics-installing-upgrading-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)
