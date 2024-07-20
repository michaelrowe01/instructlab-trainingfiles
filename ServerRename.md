META:TOPICINFO{author="rnaranjo" date="1502392984" format="1.1"
reprev="1.31" version="1.31"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Server rename landing page [server-rename-landing-page]

DKGRAY Authors: Main.DavidChadwick, Main.RitchieSchacher,
Main.HeatherSterling, Main.MikeDelargy Build basis: CLM products,
version 4.0.1 (and higher.4.x), 5.x,6.x ENDCOLOR

TOC{title="Page contents"}

This section supplements the information in the "Changing the public URL
by using server rename" section in the Jazz Team Server Installing book
in the [IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
Considerations are provided when deciding whether or not to use the
server rename functionality introduced in version 4.0.1 of the Rational
solution for Collaborative Lifecycle Management (CLM) products. A case
study and links to workarounds and limitations are discussed as well.

## Basic articles about server rename

-   [High Level Overview of Public URIs and Server
    Rename](https://jazz.net/wiki/bin/view/Deployment/Highleveloverviewofpublicuriandserverrename)
-   [Renaming your Rational solution for Collaborative Lifecycle
    Management server (version 4.0.1)](ServerRenameCLM401)
-   [Impact of server rename and integrated products (version
    4.0.1)](ServerRenameImpact401)

## Case study and best practices for deploying server rename

-   [Case study: Server rename (version 4.0.1)](ServerRenameCaseStudy)

## Server rename limitations and workarounds

-   Server Rename is not supported on a CLM deployment using Derby. Move
    off of Derby first before attempting the server rename operation.
-   [6.0.4 Impact of server rename on the Rational solution for
    Collaborative Lifecycle
    Management](https://www.ibm.com/support/knowledgecenter/en/SSYMRC_6.0.4/com.ibm.jazz.install.doc/topics/c_server_rename_limitations.html)
-   [Lifecycle Query Engine server names do not change after performing
    server rename](https://jazz.net/library/article/1553)
-   [6.0 - The Data Collection Component does not yet support server
    rename.](https://jazz.net/library/article/1519)
-   [What to do with Rational Synchronization Server if CLM server is
    renamed?](ServerRenameRationalSynchServer)
-   [Workarounds: Server rename problems in the Rational solution for
    Collaborative Lifecycle Management
    4.0.2](https://jazz.net/library/article/1268)
-   [Workarounds: Server rename problems in CLM 4.0.1 and
    4.0.2](https://jazz.net/library/article/1165)
-   [Workaround: Server rename Read-only mode
    limitations](https://jazz.net/library/article/1124)

##### Related topics: [Maintaining the public URL](MaintainingThePublicURL), [Proxy Servers](InstallProxyServers) [related-topics-maintaining-the-public-url-proxy-servers]

##### External links: [external-links]

-   None

##### Additional contributors: Main.RobinYehle, Main.HuiBinShi, Main.EricSolomon, Main.RosaNaranjo, Main.LisaFrankel [additional-contributors-main.robinyehle-main.huibinshi-main.ericsolomon-main.rosanaranjo-main.lisafrankel]
