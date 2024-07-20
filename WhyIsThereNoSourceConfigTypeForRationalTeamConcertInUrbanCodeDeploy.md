META:TOPICINFO{author="sbagot" date="1432737793" format="1.1"
version="1.3"}
META:TOPICPARENT{name="TroubleshootingRationalTeamConcertIntegrationWithIBMUrbanCodeDeploy"}

# Why is there no Source Config Type for Rational Team Concert in UrbanCode Deploy? [why-is-there-no-source-config-type-for-rational-team-concert-in-urbancode-deploy]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: Rational
Team Concert 4.0.5, IBM UrbanCode Deploy 6.0.x ENDCOLOR

TOC{title="Page contents"}

In IBM UrbanCode Deploy, Source Config Types are used to pull Versions
from various third party products, including Source Configuration
Management tools and Build tools. No such Source Config Type exists for
Rational Team Concert (RTC). How do you import Versions that contain
artifacts build by Rational Team Concert using the Jazz Build Engine,
for deployment with IBM UrbanCode Deploy?

## Where are Source Config Types in IBM UrbanCode Deploy?

In IBM UrbanCode Deploy, Source Config Types can be configured when
creating a new Component, as shown in the following image:

As you can see from the screenshot, there is no entry that refers to
Rational Team Concert (the screenshot was taken using IBM UrbanCode
Deploy 6.0.1.4 iFix001).

### What is the alternative to using a Source Config Type?

The general alternative to using Source Configuration Types consists of
pushing artifacts from an external source to IBM UrbanCode Deploy, using
the Command Line Interface (**udclient**).

-   Starting with Rational Team Concert 4.0.5 you can leverage new Post
    Build Deploy functionality that simplifies the creation of new
    versions in IBM UrbanCode Deploy.
-   The instructions can be found in the IBM Knowledge Center RTC 4.0.5
    documentation under the topic of Integrating Rational Team Concert
    and IBM UrbanCode Deploy
-   For later versions, check the corresponding pages under the newer
    RTC versions listed in the IBM Knowledge Center.
-   For a usage example, see this blog posting [Old dog, new trick: RTC
    and UrbanCode
    Deploy](http://sudhakarf.wordpress.com/2013/10/30/old-dog-new-trick-rtc-and-urbancode-deploy/).

<!-- -->

-   If you cannot yet upgrade to RTC 4.0.5 or higher, you would need to
    follow the same approach and use the **udclient** to create versions
    and add files after your RTC build has finished. Assuming that you
    already have a Component called Test1, you could add a new Version
    0.1 as follows:

C:\UDeploy60\udclient\>udclient.cmd -weburl <https://localhost:8443>
-username admin -password admin createVersion -component Test1 -name 0.1
{ "id": "005fe89f-b085-4769-be52-6757d394b3b1", "name": "0.1", "type":
"FULL", "created": 1396339808136, "active": true, "archived": false }

You could then add new files to the Version 0.1 of Component Test1 as
follows:

C:\UDeploy60\udclient\>udclient.cmd -weburl <https://localhost:8443>
-username admin -password admin addVersionFiles -component Test1
-version 0.1 -base C:\00000UrbanCode\12749 -verbose Uploading file
C:\00000UrbanCode\12749\New Rich Text Document.rtf

(You would of course have to change the **-weburl**, **-username** and
**-password** to match your server values). The **-base** parameter
refers to the directory that contains the file to upload.

## References

##### Related topics: [Integrations Troubleshooting](https://jazz.net/wiki/bin/view/Deployment/IntegrationsTroubleshooting) [related-topics-integrations-troubleshooting]

##### External links: [external-links]

-   Blog: Old dog, new trick: RTC and UrbanCode Deploy:
    <http://sudhakarf.wordpress.com/2013/10/30/old-dog-new-trick-rtc-and-urbancode-deploy/>
-   IBM UrbanCode Deploy 6.0.1 Knowledge Center topic: Command-line
    client (CLI) reference
    <http://www.ibm.com/support/knowledgecenter/SS4GSP_6.0.1/com.ibm.udeploy.reference.doc/topics/cli_ch.html?lang=en>

##### Additional contributors: Main.LaraZiosi [additional-contributors-main.laraziosi]

META:FILEATTACHMENT{name="Snap9.jpg" attachment="Snap9.jpg" attr="h"
comment="SourceConfigTypes" date="1398269885" path="Snap9.jpg"
size="147265" user="lziosi" version="1"}
