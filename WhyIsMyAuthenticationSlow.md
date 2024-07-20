META:TOPICINFO{author="michaelrowe" date="1659376675" format="1.1"
version="1.22"} META:TOPICPARENT{name="PerformanceTroubleshooting"}

# Why does it take so long to log in? DKGRAY Authors: Main.StephanieBagot Build basis: CLM 4.x, SSE 4.x, ELM 7.X and later [why-does-it-take-so-long-to-log-in-dkgray-authors-main.stephaniebagot-build-basis-clm-4.x-sse-4.x-elm-7.x-and-later]

ENDCOLOR

TOC{title="Page contents"}

This page provides potential reasons why latency occurs during user
authentication into the IBM solution for Engineering Lifecycle
Management (ELM) applications.

## Understanding authentication within ELM applications

The user registry in the Jazz Team Server has two roles: 1
Authentication 1 Source of data about users (or "contributors")

It is important to understand that **all authentication and
authorization comes from the application server** (Apache Tomcat or IBM
WebSphere Application Server) hosting the ELM applications, *NOT* the
Jazz Team Server itself. So any issues with Authentication should be
addressed from the web container side. The Jazz API has implemented a
way to pull data out of certain kinds of registries. Specifically, we
can currently interface with Lightweight Directory Access Protocol
(LDAP) and the Tomcat user registry. We use this to populate our user
database. Other APIs are used to keep the user database in sync with
that of the LDAP provider.

### Authentication process

After a user enters an ID and password at the log-in stage to the Jazz
Team Server, the web container starts an LDAP session by connecting to
an LDAP server. The BIND operation establishes the authentication state
for a session and sends the binding user's ID and password to the LDAP
server.

The LDAP server will then look up the LDAP registry tree to search for
the user. The base distinguished name setting determines the starting
point for LDAP searches in the directory services. For instance, if the
base DN is set to the root DC level, the search will search the entire
LDAP tree including all the sub level tree.

Once the user ID is found, the LDAP server typically checks the password
against the userPassword attribute in the named entry and then sends the
response back to the web container to indicate whether the
authentication is succeed or not. If the LDAP server allows anonymous
access and there is no binding ID and password provided, the
authentication for the binding user ID will be omitted.

Once the connection is made, the search operation is repeated to
authenticate the actual user's ID and send the response back to the
container. This response is then passed onto the Jazz Team Server and
reflected in the client.

## Initial assessment

### Symptoms

-   When the user logs in, it takes awhile to receive a response and
    move to the application indicating that the user has successfully
    logged in.
-   Alternatively, when the user logs in, it takes awhile to receive a
    response indicating that the authentication failed with "Invalid
    User ID or Password"

|  |
|----|
| **Note**: This article will not discuss common errors when logging in, but rather address commonly seen issues where the response time is delayed indicating that authentication was successful or failed. |

### Timing

The delay in response could occur any time that the user logs in, or
when the repository permissions or licenses are challenged.

## Recommended data analysis

\| **Before completing any LDAP trace or LDAP browser lookup, consult
your LDAP administrator for assistance.** \| Ensure you complete the
[Troubleshooting
Assessment](https://jazz.net/wiki/bin/view/Deployment/HowToStartATroubleshootingAssessment)
to assess where the performance issue might reside. For releases before
ELM 7.0.1 SR1 / 7.0.2 SR1:

-   You can turn on LDAP query trace from the Jazz Team Server to see if
    any of the responses are delayed. The trace is contained under the
    LDAP section in the log4j.properties file, located in
    ..server/conf/jts/log4j.properties To enable it, remove the \# side
    from the beginning of the log4j.logger line. \#Turn on query trace
    against the LDAP server

\#log4j.logger.com.ibm.team.repository.service.jts.internal.userregistry.ldap.LDAPUserRegistry=DEBUG

-   To turn on LDAP trace from Tomcat, open the following file:
    ../tomcat/conf/logging.properties and add the following trace
    org.apache.catalina.realm.level = ALL

org.apache.catalina.realm.useParentHandlers = true
org.apache.catalina.authenticator.level = ALL
org.apache.catalina.authenticator.useParentHandlers = true

-   Use an LDAP browser and take a look at your LDAP configuration.
    Verify if there are multiple levels or if your username is
    configured within a subtree indicating that the LDAP search is
    traversing many branches.

For release ELM 7.0.1 SR1 / 7.0.2 SR1 and later: \* You can turn on LDAP
query trace from the Jazz Team Server to see if any of the responses are
delayed. The trace is contained under the LDAP section in the
log4j.properties file, located in ..server/conf/jts/log4j2.xml To enable
it, change the logger entry from :

to:

-   To turn on LDAP trace from Tomcat, open the following file:
    ../tomcat/conf/logging.properties and add the following trace
    org.apache.catalina.realm.level = ALL

org.apache.catalina.realm.useParentHandlers = true
org.apache.catalina.authenticator.level = ALL
org.apache.catalina.authenticator.useParentHandlers = true

-   Use an LDAP browser and take a look at your LDAP configuration.
    Verify if there are multiple levels or if your username is
    configured within a subtree indicating that the LDAP search is
    traversing many branches.

## Possible causes or solutions

### Known issue accessing 4.0.5 server with 3.0.x client

When accessing a version 4.0.5 server with a 3.0.x Eclipse client, users
may experience severe performance issues logging in due to the changes
between protocols in 3.x and 4.x. This is detailed in [Defect 289275:
Performance impacted 100 by using 3.0.1 RTC client against RTC 4.0.5
server](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=289275).
**Solution:**

-   Ensure your users are using the same version of client as your
    server is running
-   To avoid issues such as this from occurring, Administrators can set
    the Version Compatibility Mode
    (com.ibm.team.repository.service.internal.VersionCompatibilityRestService)
    to STRICT in Advanced Properties to prevent older versions from
    connecting.

### Topology

The location of your LDAP server could contribute to latency and longer
time to authenticate. Ensure that your LDAP server and application
server hosting CLM applications are located relatively close to one
another to mitigate any latency. Keeping them on the same LAN or even
subnet is ideal.

### LDAP configuration

\| **Ensure that you consult with your LDAP administrator for
assistance.** \| In terms of the search operation, the more levels the
LDAP Search traverses to match the user ID, the longer time it will
take. Ideally, using one level searches instead of subtree ones are
faster. Since it is unlikely you would change the structure of your
LDAP, you can edit the user base configuration so that the search does
not begin at the top level and the scope is more narrowed.

### Tuning configuration

-   If using WebSphere Application Server, review the [LDAP
    settings](http://www.ibm.com/support/knowledgecenter/SSEQTP_7.0.0/com.ibm.websphere.base.doc/info/aes/ae/uwim_ldapperfsettings.html)
    article for recommendations on tuning.
-   Tuning can also be done from the LDAP server to improve performance.
    **Consult with your LDAP administrator before performing any
    tuning.**

##### Related topics: [related-topics]

-   Still need help troubleshooting your performance issue? Refer to
    [Performance Troubleshooting](PerformanceTroubleshooting) for
    additional topics.

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]
