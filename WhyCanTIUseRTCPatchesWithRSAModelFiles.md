META:TOPICINFO{author="sbagot" date="1432743300" format="1.1"
version="1.5"}
META:TOPICPARENT{name="IntegrationsTroubleshootingRTCandIntegratedDevelopmentEnvironments"}

# Why can't I use Rational Team Concert patches with Rational Software Architect model files? [why-cant-i-use-rational-team-concert-patches-with-rational-software-architect-model-files]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: Rational
Team Concert 4.0.3, Rational Software Architect 9 ENDCOLOR

TOC{title="Page contents"}

This article explains how Rational Software Architect (RSA) model files
are affected if you attempt to include them in Rational Team Concert
(RTC) patches.

## How do you create Rational Team Concert Patches for Rational Software Architect Models?

The Rational Team Concert documentation describes how to create Patches:
Creating and applying Rational Team Concert source control patches

To reproduce the issue, you can proceed as follows: 1 Create an empty
model and share it in Rational Team Concert. 1 Add one class to the
Model, called Class1. 1 Create a Patch. 1 Save the Patch on the file
system. 1 Delete Class1 from the model. 1 Add some different model
elements, for example an Actor and a UseCase. 1 Save the model. 1
Check-In and Deliver the model. 1 Now, attempt to Apply the Patch and
select Auto Resolve.

## What is the effect of creating Patches of Rational Software Architect Models?

You will see this message:

"None of these changes could be accepted. You will have to merge them
manually.The Text in brackets should explain why the change could not be
accepted."

The text in brackets states:

"Model1.emx - 29 lines (unable to match context lines)."

If you open the patch file in a text editor, you will see that it
contains a textual diff of the model files, as in the following code
snippet:

diff -u -N MyModelToPatch/Model1.emx MyModelToPatch/Model1.emx ---
MyModelToPatch/Model1.emx 2014-04-09 15:02:46.000000053 +0200 +++
MyModelToPatch/Model1.emx 1970-01-01 01:00:00.000000006 +0100 @@ -1,14
+1,29 @@

+?\> ?\> -?\>

Rational Software Architect models are very specialized types of XML
files. They can only be compared or merged using tooling provided by
Rational Software Architect itself. This tooling needs to receive the
complete model file (and its fragments) so that it can compare it with
another version. For this reason, it cannot be used by patches, which
contains just a textual diff of the model versions.

##### Related topics: [related-topics]

-   Still need help troubleshooting your integrations issue? Refer to
    [Integrations Troubleshooting](IntegrationsTroubleshooting) for
    additional topics.

##### External links: [external-links]

-   Creating and applying Rational Team Concert source control patches

<!-- -->

-   Integrating Rational Software Architect with Rational Team Concert

##### Additional contributors: Main.LaraZiosi [additional-contributors-main.laraziosi]
