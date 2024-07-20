META:TOPICINFO{author="shubjit" date="1625033661" format="1.1"
version="1.4"} META:TOPICPARENT{name="JazzAuthorizationServer"}

# Jazz Authorization Server and SCIM - Federating LDAP and Basic User Registry (DRAFT) DKGRAY Authors: Main.ShubjitNaik [jazz-authorization-server-and-scim---federating-ldap-and-basic-user-registry-draft-dkgray-authors-main.shubjitnaik]

Build basis: IBM Engineering Lifecycle Management and Jazz Authorization
Server 7.0.2 and higher ENDCOLOR

TOC{title="Page contents"}

IBM WebSphere Liberty Profile allows configuring Multiple federated
users registries. Jazz Authorization Server (JAS) is based on WebSphere
Liberty Profile and can leverage the feature of configuring federated
Registries. However, for it work with ELM, you would have to configure
[JAS with
SCIM](https://jazz.net/wiki/bin/view/Deployment/JASSCIMFederatedRepositories)

WebSphere Liberty also allows federating LDAP registries with a file
based User Registry. Th focus of this article to enable SCIM in such a
scenario and map SCIM attributes in a way it is consumable for an ELM
setup.

## High Level Instructions

-   Configure LDAP User Registry in JAS
-   Configure Basic or File based user registry in JAS
-   Configure JAS with SCIM
-   Configure SCIM attributes for Federated Registries
-   Import Local Users into ELM

## Heading 1 (use sentence-style capitalization)

Section text Section text Section text Section text Section text Section
text Section text Section text Section text Section text Section text
Section text Section text Section text Section text Section text Section
text Section text Section text Section text Section text Section text
Section text Section text Section text Section text Section text Section
text Section text Section text Section text Section text Section text
Section text Section text

### Heading 2 (use sentence-style capitalization)

Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text

### Heading 2 (use sentence-style capitalization)

Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text Sub-Section text Sub-Section text Sub-Section text
Sub-Section text

## Heading 1

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
