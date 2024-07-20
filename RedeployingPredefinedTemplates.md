META:TOPICINFO{author="sbagot" date="1432746498" format="1.1"
version="1.9"} META:TOPICPARENT{name="CLMUpgradeTroubleshooting"}

# Redeploying the predefined process templates [redeploying-the-predefined-process-templates]

Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam) Build
basis: CLM 4.x and later ENDCOLOR

TOC{title="Page contents"}

This topic discusses the final upgrade step which in some cases requires
the user to redeploy the predefined process templates after the upgrade
succeeded.

## Redeploying the predefined process templates

## Changes in 4.0.1

There are some project area changes in 4.0.1 which need to be addressed
prior to upgrading.

### Rational Requirements Composer base template

In releases prior to 4.0.1, the predefined requirements management
lifecycle project templates included support for the Base project
template. As of release 4.0.1, the Base template has been replaced with
the Requirements Template for Testers project template.

In order to prevent issues from incurring when creating Lifecycle
Applications, you must re-deploy the predefined templates . For more
information, see [Creating lifecycle projects from a
template](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/index.jsp?topic=2Fcom.ibm.jazz.platform.doc2Ftopics2Ft_creating_aggregate_projects_from_template.html).

## Errors which can occur when redeploying the templates

### Symptoms

Redeploying the predefined process templates failed with the following
error: Error deploying predefined process templates to the repository.

### Possible causes and solutions

#### Permission errors

The following error can occur: An error response was received from the
Jazz Team Server. Status=400. Message: CRJAZ1848E To do the
"com.ibm.team.process.server.saveProcessTemplate" operation, you must
have one of the following licenses that are installed on the server:
Analyst, Contributor, Practitioner-Floating, Contributor, Stakeholder,
Stakeholder, Developer for IBM Enterprise Platforms, Developer-Floating,
Quality Professional, Practitioner, Developer, Contributor, Contributor,
User. The server administrator can assign licenses. The user attempting
to redeploy the process templates is required to have JazzProjectAdmin
or JazzAdmin repository permissions, and must have a CLM Client Access
License such as Analyst, Contributor, Practitioner-Floating,
Stakeholder, Developer for IBM Enterprise Platforms, Developer-Floating,
Quality Professional, Practitioner, or Developer.

##### Related topics: [related-topics]

\* For more upgrade troubleshooting topics, refer to [Upgrade
Troubleshooting](UpgradeTroubleshooting).

##### External links: \* [Workarounds: Lifecycle Project Administration problems in Jazz Foundation 4.0.1](https://jazz.net/library/article/1161#215689) [external-links-workarounds-lifecycle-project-administration-problems-in-jazz-foundation-4.0.1]

##### Additional contributors: Main.StephanieBagot [additional-contributors-main.stephaniebagot]
