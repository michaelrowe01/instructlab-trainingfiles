META:TOPICINFO{author="sbagot" date="1432743012" format="1.1"
version="1.4"}
META:TOPICPARENT{name="IntegrationsTroubleshootingRTCandIntegratedDevelopmentEnvironments"}

# Why do I get unexpected validation errors when RTC is installed together with an IDE? [why-do-i-get-unexpected-validation-errors-when-rtc-is-installed-together-with-an-ide]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: Rational
Team Concert 4.0.x and later, Rational Application Developer 7.5.x, 8.x,
9.x, Rational Software Architect for WebSphere 7.5.x, 8.x, 9.x. ENDCOLOR

TOC{title="Page contents"}

This page describes known defects that cause unexpected validation or
code generation errors to be reported by an IDE such as IBM Rational
Application Developer or IBM Rational Software Architect for WebSphere,
when they are installed in the same IBM Installation Manager Package
group as IBM Rational Team Concert Client for Eclipse IDE. This
configuration is also known as a "shell-sharing".

## Initial assessment

If the symptom is related to Validation errors:

-   Validate the projects in the shell-sharing configuration, with the
    projects shared in a Rational Team Concert Repository. Save the
    validation errors to a file.
-   Validate the same projects in another workspace, where they are not
    shared in a Rational Team Concert Repository. Save the validation
    errors to a file.
-   Validate the same projects in another installation of the IDE, which
    is not shell-sharing with IBM Rational Team Concert Client. Save the
    validation errors to a file.

If there are differences in the number of validation errors reported in
these three cases, then you are likely facing a product defect.

## Possible causes and solutions

### Unexpected validation errors

-   If both Rational Team Concert and Rational Application Developer are
    installed in a shell-sharing configuration, references from the soap
    envelope schema, `http://schemas.xmlsoap.org/soap/envelope/`, are
    unresolved. This is due to APAR
    [PM30397](http://www.ibm.com/support/docview.wss?uid=swg1PM30397)
    which was fixed in Rational Application Developer versions 7.5.5.4
    and 8.0.3.
-   If both Rational Team Concert and Rational Application Developer are
    installed in a shell-sharing configuration, validating a WSDL file
    contained in a project that is shared in Rational Team Concert gives
    unexpected validation errors if there are spaces in the Project
    names. This is due to APAR
    [PM92874](http://www.ibm.com/support/docview.wss?uid=swg1PM92874).
    As a workaround, you can rename the projects so that they do not
    contain any spaces.

### Unexpected code generation errors

-   Attempts to generate Java code from a XSD file might fail when the
    project is shared in Rational Team Concert Repository. This is due
    to the following APAR
    [PM63065](http://www.ibm.com/support/docview.wss?uid=swg1PM63065).
    This APAR was resolved in v8.0.4.2 and v8.5.1.

##### Related topics: [Deployment web home](WebHome), [IntegrationsTroubleshooting](IntegrationsTroubleshooting) [related-topics-deployment-web-home-integrationstroubleshooting]

##### External links: [external-links]

-   [PM30397: XSD:attribute reference in
    `'http://schemas.xmlsoap.org/soap/envelope/#actor'` is
    unresolved](http://www.ibm.com/support/docview.wss?uid=swg1PM30397)
-    [PM63065: Generating Java code from xsd files fails if the project
    is under Jazz/RTC source
    control](http://www.ibm.com/support/docview.wss?uid=swg1PM63065)

##### Additional contributors: Main.LaraZiosi [additional-contributors-main.laraziosi]
