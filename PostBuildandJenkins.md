META:TOPICINFO{author="sbagot" date="1432744415" format="1.1"
version="1.6"} META:TOPICPARENT{name="JenkinsAndHudson"}

# When selecting Post Build activities in the Build definition, after the build is complete no Post Build activities are triggered. [when-selecting-post-build-activities-in-the-build-definition-after-the-build-is-complete-no-post-build-activities-are-triggered.]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: Rational
Team Concert 4.x and later ENDCOLOR

TOC{title="Page contents"}

## Subsequent analysis steps.

-   You need to invoke the Jazz ant participant
    com.ibm.team.build.autoDeliver in build.xml in a target after all
    the necessary build targets are completed.
-   The Jazz Build Engine participant step should be invoked from the
    Ant script using an EXEC block, so it will be able to access the
    variables necessary for the build.

Example command :

Use case Example: if you are using the sample provided in [Integrating
with Jazz SCM and Builds from Hudson and
Jenkins](https://jazz.net/wiki/bin/view/Main/JazzScmWithJenkins) you
need to modify build.xml to invoke the participant *autoDeliver*

Note: This participant does not get invoked when you define the Post
Build activities in the Build definition. This needs to be invoked in a
target for Post Build to work in RTC.

##### Related topics: [related-topics]

-   Still need help troubleshooting your integrations issue? Refer to
    [Integrations troubleshooting](IntegrationsTroubleshooting) for
    additional topics.

##### External links: [external-links]

##### Additional contributors: Main.ZeeshanChoudhry [additional-contributors-main.zeeshanchoudhry]
