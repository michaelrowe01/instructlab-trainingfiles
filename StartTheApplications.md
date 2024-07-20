META:TOPICINFO{author="sbagot" date="1432746321" format="1.1"
version="1.14"} META:TOPICPARENT{name="CLMUpgradeTroubleshooting"}

# Starting the applications [starting-the-applications]

Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam) Build
basis: CLM 4.x and later ENDCOLOR

TOC{title="Page contents"}

Use this topic for common issues that arise after the upgrade steps are
performed and when the applications are started for the first time.

## Troubleshooting

Typically, when an application is started and fails, this information
will be logged in the Tomcat or Websphere Application Server logs. An
example is: Tomcat, located in ../server/tomcat/logs folder of the
installation directory catalina.log Websphere, located in the
application profile directory stdout.log, stderr.log However, if the
application starts and the users experience an issue in testing, the
errors may be located in the application log files, such as: jazz.log,
jts.log, ccm.log, qm.log, rm.log

## Common issues when starting the applications after an upgrade

After the upgrade occurs, ensure that the following is completed:

-   Browser cache is cleared
-   Temporary directories and cache are deleted

The following sections identify some known issues which occur after the
upgrade, with information on the cause and solution.

### DBLock

**Symptom:** The following error might occur related to DBLock:
CRJAZ1770E The configured database lock id does not match the lock id in
the database. This can happen if 2 applications or Jazz Team Servers are
trying to access the same set of tables, or if the lock id was
overwritten or lost in the teamserver.properties configuration file.
Check the server configuration and the database connection spec and
ensure they are correct. **Cause:** The application will set a database
lock ID on the DB to ensure that only that application can access the
database. This prevents two applications from writing to the same
database, and possibly overwritting or corrupting the data. This error
can occur after the upgrade because of the following reasons: \* The
teamserver.properties file merged incorrectly \* The upgraded
application is trying to set a new Lock ID **Resolution:** Before
resetting the Lock ID, ensure that each of your teamserver.properties
files for the applications point to **seperate** databases. Once this is
confirmed, you can run repotools- resetRepoLockID Further information
can be found on the Information Center topic for the command
[resetRepoLockID](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fr_repotools_reindexrepolockid.html).

### Hanging 'Loading' screen

**Symptom:** When attempting to login to the CLM applications, the
splash screen never fully loads and appears to be hung at the 'Loading'
page. **Cause:** The Loading is often related to a mis-configuration in
the teamserver.properties file, or within the application server.
**Resolution:** The following technotes provide a resolution to this
behaviour:

-   [Completion of Setup hangs on Loading
    Screen](http://www-01.ibm.com/support/docview.wss?uid=swg21470574)
-   [Configuring the Public URI in Rational Team Concert setup menu
    hangs with the Loading configuration settings
    message](http://www-01.ibm.com/support/docview.wss?uid=swg21474026)
-   Validate in your JVM arguments: ensure that any custom variables are
    correct and the paths are not missing or incorrect, specially
    JAZZ_HOME value must be updated to point to the new version. In
    addition, check your heap configuration is accurate. For more
    information see the Information Center topic on [Setting up
    WebSphere](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Ft_s_server_installation_setup_WAS.html).

### Users unable to login

**Symptom:** After the upgrade, users are unable to login. If a user is
able to login, they may not obtain the correct repository permissions
similar as prior to the upgrade. **Cause:** The authentication and
authorization is controlled by the Application Server (Tomcat or
WebSphere). There may be a configuration setting which is incorrect, or
the LDAP configuration needs to be updated. **Resolution:** Validate
your LDAP configuration by referencing the following articles: \* [LDAP
Configuration for
Newbies](https://jazz.net/wiki/bin/view/Main/LDAP4Newbies) \* [Managing
Users by using
LDAP](https://jazz.net/help-dev/clm/index.jsp?topic=2Fcom.ibm.jazz.install.doc2Ftopics2Fc_plan_identity_management.html)
If you are using **Tomcat**, by default, the tomcat-users.xml file it
set to read-only in later versions. Follow [Technote 1474527:
Tomcat-users.xml is file not updated after
Upgrade](http://www-01.ibm.com/support/docview.wss?uid=swg21474527)

## Symptoms when trying to use the product

After the final steps of the upgrade have been completed, such as the
[Online migration of RM](MigratingRequirementsManagementApplication) and
[Redeploying the process templates](RedeployingPredefinedTemplates), you
may incur issues when trying to use the product functionality. For
information on troubleshooting and debugging common issues which occur
after the upgrade, navigate to [Known issues which occur after the
upgrade](AfterTheUpgrade).

## Recommended data gathering

-   If you are engaging IBM Support with regards to these issues, ensure
    that you run
    [ISALITE](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0m1/index.jsp?topic=2Fcom.ibm.team.concert.doc2Ftopics2Ft_using_the_isal.html)
    to gather the system information and pertinent log files.
-   In addition, including screenshots and upgrade steps are helpful in
    quick problem determination and resolution.

##### Related topics: [related-topics]

\* For more troubleshooting topics, refer to [Upgrade
Troubleshooting](UpgradeTroubleshooting)

##### External links: [external-links]

-   None

##### Additional contributors: Main.StephanieBagot [additional-contributors-main.stephaniebagot]
