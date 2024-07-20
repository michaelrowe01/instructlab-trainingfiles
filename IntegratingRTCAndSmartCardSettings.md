META:TOPICINFO{author="rrakich" date="1709327124" format="1.1"
version="1.13"} META:TOPICPARENT{name="RationalTeamConcertIntegrations"}

# How to Setup Smart Card Integration DKGRAY Authors: Main.ZeeshanChoudhry, Main.RichRakich Build basis: IBM Engineering Lifecycle Management 7.x [how-to-setup-smart-card-integration-dkgray-authors-main.zeeshanchoudhry-main.richrakich-build-basis-ibm-engineering-lifecycle-management-7.x]

ENDCOLOR

TOC{title="Page contents"}

This article explains how you can setup IBM Engineering Lifecycle
Management applications for Smart Card integration.

## Rational Team Concert Eclipse client settings

If the Engineering Workflow Management (EWM) Eclipse client was
installed in the following directory

C:\Program Files\IBM\TeamConcert

then the following JRE file would have to be modified:

C:\Program Files\IBM\TeamConcert\jdk\jre\lib\security\java.security

1\) Search for the following section, and make the modification below:

\# \# List of providers and their preference orders (see above): \#
security.provider.1=com.ibm.security.capi.IBMCAC
security.provider.2=com.ibm.jsse2.IBMJSSEProvider2
security.provider.3=com.ibm.crypto.provider.IBMJCE
security.provider.4=com.ibm.security.jgss.IBMJGSSProvider
security.provider.5=com.ibm.security.cert.IBMCertPath
security.provider.6=com.ibm.security.sasl.IBMSASL
security.provider.7=com.ibm.xml.crypto.IBMXMLCryptoProvider
security.provider.8=com.ibm.xml.enc.IBMXMLEncProvider
security.provider.9=org.apache.harmony.security.provider.PolicyProvider
security.provider.10=com.ibm.security.jgss.mech.spnego.IBMSPNEG

Note that IBM CAC (Common Access Card) support has been enabled.

2\) Search for the next section and make sure the following has been
specified as to the default keystore:

\# \# Default keystore type. \# keystore.type=Windows-MY

**The above sections show the correctly modified content within the
java.security file to enable the support for IBM CAC and thus Smart Card
Log-in ability within the Engineering Workflow Management Eclipse
client**

## Rational Team Concert Server settings

Refer to link [Configuring certificate authentication in Rational Team
Concert 3.0 using WebSphere Application Server
7.0](https://jazz.net/library/article/606) These instructions apply to
all versions since v3.0.

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

Instructions to enable debugging on the Eclipse Client [Smart Cards
Debugging](https://jazz.net/wiki/bin/view/Main/SmartCards)

##### External links: [external-links]

-   IBM
-   Prerequisites for using smart card authentication in Rational Team
    Concert

META:TOPICMOVED{by="dmmckinn" date="1418397404"
from="Deployment.IntegratiingRTCAndSmartCardSettings"
to="Deployment.IntegratingRTCAndSmartCardSettings"}
