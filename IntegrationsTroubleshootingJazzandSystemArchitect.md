META:TOPICINFO{author="dmmckinn" date="1425924674" format="1.1"
reprev="1.3" version="1.3"}
META:TOPICPARENT{name="IntegrationsTroubleshooting"}

# Troubleshooting Jazz product integrations with System Architect [troubleshooting-jazz-product-integrations-with-system-architect]

DKGRAY Authors: Main.StefanHjalmarsson Build basis: Rational System
Architect 11.4.2.x and Rational Team Concert 4.0.x ENDCOLOR

TOC{title="Page contents"}

This page details some of the common error messages that you can
encounter and their solutions, when integrating Rational Team Concert
(RTC) with Rational System Architect (SA).

## .NET not installed

The following error will show up when you have not installed .NET 3.5.

When in the Service Providers window of System Architect, the error that
responds to this scenario is:

*The root service URL "<https://myserver:9443/ccm/rootservices>"
provided cannot be contacted. Please make sure the server is started and
a valid URL is specified for it.*

-   Setup SA to consume RTC:

### Set-up: RTC consuming System Architect

Specify the encyclopaedias that can be consumed. RTC consuming SA setup:

BR

### Start the SA publishing server

Ensure that the System Architect publishing server is running.

Start SA server problem II:

### Making friends - RTC consuming System Architect

There are 5 letters in this diagram, but I am not sure why? BR Make
Friends with RTC consuming SA:

### RTC consuming SA, associate RTC with SA:

### Trustworthiness with the integration

-   Cleaned up trust in Mozilla Firefox:

### Create a consumer in RTC

\* Create RTC consumer key: BR

Note the consumer key

\* Consumer key:

## Configuring the SA service provider

### SA consuming RTC part I:

### SA consuming RTC part II:

## Where are the diagrams, links and link symbols?

### RED Where are the diagrams?: ENDCOLOR

After completing all the above steps to configure the integration, one
of the last hurdles that you can fall over is where you cannot see your
diagrams in the OSLC rich hover.

### Let SA publish the diagrams:

### RED Why don't I see the links in SA? ENDCOLOR

### BLUE Let SA show link symbols: ENDCOLOR

**Note**: Detailed information about setting up the integration is
available in this article: Integrate Rational System Architect 11.4 and
CLM 2012 applications by using OSLC in addition to further
troubleshooting information.

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.MaeveOReilly, Main.PaulEllis [additional-contributors-main.maeveoreilly-main.paulellis]

META:FILEATTACHMENT{name="dotnet.jpg" attachment="dotnet.jpg" attr="h"
comment="System Architect error when .net 3.5 is not installed"
date="1425920932" path="dotnet.jpg" size="40667" user="dmmckinn"
version="3"} META:FILEATTACHMENT{name="setupconsumer.jpg"
attachment="setupconsumer.jpg" attr="h" comment="RTC consuming SA setup"
date="1383051901" path="setupconsumer.jpg" size="62022" user="paulellis"
version="1"} META:FILEATTACHMENT{name="setupconsumer2.jpg"
attachment="setupconsumer2.jpg" attr="h" comment="Setup SA to consume
RTC" date="1383052124" path="setupconsumer2.jpg" size="78224"
user="paulellis" version="1"}
META:FILEATTACHMENT{name="setupconsumer3.jpg"
attachment="setupconsumer3.jpg" attr="h" comment="SAPublishingServer"
date="1383052529" path="setupconsumer3.jpg" size="65984"
user="paulellis" version="1"}
META:FILEATTACHMENT{name="setupconsumer4.jpg"
attachment="setupconsumer4.jpg" attr="h" comment="MakeFriendswith RTC
consuming SA" date="1425921446" path="setupconsumer4.jpg" size="77581"
user="dmmckinn" version="3"}
META:FILEATTACHMENT{name="setupconsumer5.jpg"
attachment="setupconsumer5.jpg" attr="h" comment="RTC consuming SA,
associate RTC with SA" date="1425921596" path="setupconsumer5.jpg"
size="65791" user="dmmckinn" version="2"}
META:FILEATTACHMENT{name="setupconsumer6.jpg"
attachment="setupconsumer6.jpg" attr="h" comment="Start SA server
problem II" date="1383055624" path="setupconsumer6.jpg" size="25981"
user="paulellis" version="1"}
META:FILEATTACHMENT{name="creatertcconsumer.JPG"
attachment="creatertcconsumer.JPG" attr="h" comment="create rtc consumer
key" date="1383069900" path="creatertcconsumer.JPG" size="100045"
user="paulellis" version="1"} META:FILEATTACHMENT{name="consumerkey.png"
attachment="consumerkey.png" attr="h" comment="consumer key"
date="1383069976" path="consumerkey.png" size="2129" user="paulellis"
version="1"} META:FILEATTACHMENT{name="finalwhere.JPG"
attachment="finalwhere.JPG" attr="h" comment="Where are the diagrams"
date="1383070865" path="finalwhere.JPG" size="53216" user="paulellis"
version="1"} META:FILEATTACHMENT{name="diagram.JPG"
attachment="diagram.JPG" attr="h" comment="Let SA publish the diagrams"
date="1383070931" path="diagram.JPG" size="31025" user="paulellis"
version="1"} META:FILEATTACHMENT{name="whynolinksinsa.JPG"
attachment="whynolinksinsa.JPG" attr="h" comment="Ehy do I not see the
links in SA" date="1383070974" path="whynolinksinsa.JPG" size="40231"
user="paulellis" version="1"}
META:FILEATTACHMENT{name="OSLClinkchapter.JPG"
attachment="OSLClinkchapter.JPG" attr="h" comment="Let SA show link
symbols" date="1383071005" path="OSLClinkchapter.JPG" size="56358"
user="paulellis" version="1"} META:FILEATTACHMENT{name="trust2.jpg"
attachment="trust2.jpg" attr="h" comment="Cleaned up trust in firefox"
date="1425922027" path="trust2.jpg" size="63771" user="dmmckinn"
version="1"} META:FILEATTACHMENT{name="saconsumingrtc.jpg"
attachment="saconsumingrtc.jpg" attr="h" comment="SA consuming RTC"
date="1425922400" path="saconsumingrtc.jpg" size="56745" user="dmmckinn"
version="1"} META:FILEATTACHMENT{name="saconsumingrtc2.jpg"
attachment="saconsumingrtc2.jpg" attr="h" comment="SA consuming part II"
date="1425922910" path="saconsumingrtc2.jpg" size="86992"
user="dmmckinn" version="1"}
