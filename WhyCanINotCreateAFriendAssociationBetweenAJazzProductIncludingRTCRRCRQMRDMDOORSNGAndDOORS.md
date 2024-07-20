META:TOPICINFO{author="sbagot" date="1432736823" format="1.1"
reprev="1.23" version="1.23"}
META:TOPICPARENT{name="IntegrationsTroubleshootingJazzandDOORS"}

# Why can't I create a friend or project association between Rational DOORS and a Jazz product? [why-cant-i-create-a-friend-or-project-association-between-rational-doors-and-a-jazz-product]

DKGRAY Authors: IntegrationsTroubleshootingTeam Build basis: CLM 4.x and
later, Rational DOORS 9.3 and later as supported ENDCOLOR

TOC{title="Page contents"}

This page covers the basics and the pitfalls of creating a friend and
project association between IBM Rational DOORS and the Jazz products for
integrations that are based on Open Services for Lifecycle Collaboration
(OSLC). Those Jazz products include Rational Team Concert, Rational
Requirements Composer, Rational Quality Manager, Design Management, and
Rational DOORS Next Generation.

## Initial assessment

### Symptoms

-   When you add the Rational DOORS rootservices/consumer key and
    consumer secret to a Jazz product's Friends Outbound, it may give an
    error such as `CRJAZ1578E` or `CRJAZ1341E` or others
-   When you add a Jazz product rootservices/consumer key and consumer
    secret to the Remote Services tab, it may give an error such as
    `invalid_consumer_key` or `signature_invalid` or others
-   The list of projects in DOORS does not load, the dialog remains
    blank
-   Attempts to link a DOORS database or module with a Jazz project may
    fail in either tool

### Impact/scope/timing

Creating friend and project associations are first done at initial
setup. Project association may subsequently be necessary as new projects
are added. They prevent any further linking between the products.

## Data gathering and subsequent analysis steps

Ensure the servers involved can find each other and have their clocks
synchronized.

Ensure the Rational DOORS client can find the Jazz server in **Microsoft
Internet Explorer**. The Rational DOORS client only runs on Microsoft
Windows; therefore, Internet Explorer is always installed. Rational
DOORS is hardcoded to use Internet Explorer DLLs to load content from
OSLC providers. As a result, Internet Explorer must work. If, for
example, you want to link Rational DOORS and IBM Rational Team Concert
(RTC), it must be possible to login to RTC from Internet Explorer. This
is irrespective of whether Internet Explorer is the user's default or
preferred browser. For Rational DOORS to work with RTC, Internet
Explorer must be able to find RTC because if it cannot, neither can
Rational DOORS.

This Internet Explorer dependency adds a dimension which should always
be considered when security warnings are presented in Rational DOORS. If
the Jazz server does not have signed certificates or has expired
certificates, warnings to that effect will appear in Rational DOORS when
attempting to display Jazz content and they will look as they do in
Internet Explorer. If you click No (or sometimes Yes) to warnings, some
operations may fail. Be careful with security warnings.

## Possible causes

-   The Jazz application cannot find Rational DOORS Web Access.
-   The Rational DOORS Web Access server cannot find the Jazz server
    (and/or application server in a distributed setup).
-   The Rational DOORS and Jazz servers are not time synchronized.
-   The Rational DOORS client cannot find or access the Jazz product
    from Internet Explorer.
-   A pop-up blocker has prevented a login dialog from appearing for
    Rational DOORS in the Jazz product.
-   An incorrect consumer key or secret has been used. It can be
    confusing to know where to generate the consumer key.
-   Defects

## Possible solutions

-   Ensure the servers involved can find each other; check with the
    registered public URI (not ipaddress). It must be possible to find
    the application based on the URI registered in the setup of the Jazz
    product and in the published.url.prefix in the Rational DOORS Web
    Access **/server/festival/config/festival.xml**. This can be done by
    loading Rational DOORS Web Access in a web browser directly on the
    Jazz product's server and the reverse. If that is not possible (for
    example a browser is not installed), `ping`, `telnet`, `tracert` or
    other tools can be used.

<!-- -->

-   Ensure the user can login to the Jazz product on the Rational DOORS
    client machine using Internet Explorer. Check proxy and security
    settings in Internet Explorer if the login is not possible.

<!-- -->

-   If you began the process and at some later time discovered popups
    were disabled, clear your browser cache and begin the process again.
    Incorrect information might have been stored and some browsers may
    not display any subsequent message or the message may be unclear.
    Similarly, if you discover that you have tried to enter the wrong
    user name or password (for example: you entered the Jazz user for
    Rational DOORS), clear the cache and start again.

<!-- -->

-   Ensure the servers have their clocks synchronized.

<!-- -->

-   Open a new tab in the same browser. Login to DOORS Web Access. Then
    try again from the original tab.

<!-- -->

-   Add the Jazz and DOORS Web Access sites to Internet Explorer's
    trusted sites.

<!-- -->

-   If, in DOORS Web Access, any interop has been started with the
    -lightserver parameter, try removing that parameter. Ref \*[
    **CANNOT ADD DOORS RELATED ASSOCIATIONS IN CLM PRODUCTS WHEN DWA
    INTEROP IS STARTED IN LIGHT MODE**
    ](http://www.ibm.com/support/docview.wss?uid=swg1PI16585)

<!-- -->

-   [ **CRJAZ1578E & CRJAZ1341E errors when trying to add Rational DOORS
    as a Rational Design Manager Friend**
    ](http://www.ibm.com/support/docview.wss?uid=swg21613729)

<!-- -->

-   [ **GET failed with http code 401 and invalid_consumer_key when
    adding a service link type in Rational DOORS**
    ](http://www.ibm.com/support/docview.wss?uid=swg21580704)

<!-- -->

-   [ **PM79924: Adding Collaboration Link type for RQM / RTC fails with
    401 signature_invalid**
    ](http://www.ibm.com/support/docview.wss?uid=swg1PM79924)

<!-- -->

-   [ **Http 500 error trying to associate a DOORS module with a
    Rational Quality Manager project**
    ](http://www.ibm.com/support/docview.wss?uid=swg21615699)

<!-- -->

-   [ **Registering the Rational Quality Manager server in Rational
    DOORS Remote Services, the OSLC version is detected as 1.0**
    ](http://www.ibm.com/support/docview.wss?uid=swg21619169)

##### Related topics: [related-topics]

-   Still need help troubleshooting your integrations issue? Refer to
    [Integrations Troubleshooting](IntegrationsTroubleshooting) for
    additional topics.

##### External links: [external-links]

-   [ **Integrate Rational Quality Manager with Rational DOORS using
    Open Services Lifecycle Collaboration**
    ](https://jazz.net/library/article/1020/)
-   [ **Configure DOORS and Rational Team Concert for globally
    distributed workers**
    ](http://www.ibm.com/developerworks/rational/library/doors-rational-team-concert-globally-distributed-workers/)
-   [ **Configuring Rational DOORS and Rational Team Concert to
    integrate with one another**
    ](https://jazz.net/library/LearnItem.jsp?href=content/articles/rtc/3.0/configuring-doors-and-rtc-to-integrate/index.html)
-   [ **Integrating Design Management capabilities with Rational DOORS**
    ](http://www.ibm.com/support/knowledgecenter/SSB2MU_8.1.0/com.ibm.rcam.linking.doc/topics/t_dm_doors_int_ov.html)
-   [ **Integrating the Requirements Management application and Rational
    DOORS**
    ](http://www.ibm.com/support/knowledgecenter/SSYMRC_4.0.5/com.ibm.rational.rrm.help.doc/topics/t_config_doors.html)
-   [ **How to increase the Rational DOORS Web Access logging levels**
    ](http://www.ibm.com/support/docview.wss?uid=swg21456938)
-   [ **How to enable logging for DWA Interoperation server**
    ](http://www.ibm.com/support/docview.wss?uid=swg21397464)

##### Additional contributors: Main.MaeveOReilly [additional-contributors-main.maeveoreilly]
