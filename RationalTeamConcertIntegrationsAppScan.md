META:TOPICINFO{author="dmmckinn" date="1392059809" format="1.1"
reprev="1.5" version="1.5"}
META:TOPICPARENT{name="RationalTeamConcertIntegrations"}

# How AppScan leverages Rational Team Concert [how-appscan-leverages-rational-team-concert]

DKGRAY Authors: Main.AbrahamSweiss Build basis: IBM Rational Team
Concert 4.0.x ENDCOLOR

TOC{title="Page contents"}

This article provides information about how IBM Rational AppScan
leverages Rational Team Concert (RTC) to provide a better understanding
of the basic architecture.

## Description of the architecture

-   The web application for AppScan Enterprise itself runs on IIS
    (Microsoft Internet Information Services). AppScan can use Jazz for
    User Management so Apache Tomcat is included with the AppScan
    Enterprise installer for Jazz to run on, in which case there would
    be 2 different web servers, one for each web application.
-   RTC runs on an Apache Tomcat application server (if desired RTC can
    run on WebSphere)
-   AppScan uses RTC for SSO (single sign on)

## Description of the integration

1.  When users log into the AppScan application, they are first
    redirected to Jazz Team Server (JTS) for log in
2.  Once the log in completes successfully, the user is redirected back
    to AppScan
3.  AppScan will handle the licensing
4.  No licenses are installed to RTC

## Description of how AppScan configures Rational Team Concert

1.  AppScan Server runs a JTS Auto Setup script **jtsautosetup.bat**
    located in the install folder (typically: C:\Program Files
    (x86)\IBM\AppScan Enterprise\Tools\jtsautosetup) which does the
    following:
    -    Creates a consumer key to allow communication between RTC and
        AppScan
    -    Configures RTC to run as a service
2.  Jazz configuration is accomplished by running the Jazz setup wizard
    /jts/setup

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: None [additional-contributors-none]
