META:TOPICINFO{author="sbagot" date="1432744802" format="1.1"
version="1.3"}
META:TOPICPARENT{name="IntegrationsTroubleshootingRTCandBuildforge"}

# When selecting Post Build activities in the Build definition , after the build is complete no Post Build activities are triggered [when-selecting-post-build-activities-in-the-build-definition-after-the-build-is-complete-no-post-build-activities-are-triggered]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: Rational
Team Concert 4.x and later ENDCOLOR

TOC{title="Page contents"}

## Subsequent analysis steps.

-   Check if the Jazz Build Engine (JBE) build engine path is defined OK
    in the environment of the Build Forge Project.
-   Check the properties are in sync with RTC build definition from
    Build Forge Project.
-   You also need to make sure that the jazz ant participant
    com.ibm.team.build.autoDeliver is invoked using the JBE.

Example command :

\${Build_Engine_Path}/jbe -userId \${Build_User} -pass
\${Build_Password} -repository \${Repository_Address} -buildResultUUID
\${buildResultUuid} -engineUUID \${engineUUID} -participants
com.ibm.team.build.autoDeliver -noComplete

Note: This participant does not get invoked when you define the Post
Build activities in the Build definition. This command should be added
as a last step in Build Forge Project for Post Build to work in RTC.

##### Related topics: [related-topics]

-   Still need help troubleshooting your integrations issue? Refer to
    [Integrations troubleshooting](IntegrationsTroubleshooting) for
    additional topics.

##### External links: [external-links]

##### Additional contributors: Main.ZeeshanChoudhry [additional-contributors-main.zeeshanchoudhry]
