# Add database tables (CCM, QM, JTS)

Authors: [UpgradeTroubleshootingTeam](UpgradeTroubleshootingTeam)
Build basis: CLM 4.x and later

This page will discuss troubleshooting techniques and known issues that
arise during the addTables step in the upgrade process.

## Troubleshooting

During this step in the upgrade process, a log file appended with
\_addTables will be created in the ../server directory of the
Collaborative Lifecycle Management (CLM) application installation
directory. An example of this file is: repotools-ccm_addTables.log

## Known Issues

Below are some known issues which arise during the addTables step in the
upgrade process

### Jazz Team Server errors

This section will discuss errors common when adding database tables to
the Jazz Team Server (JTS) database.

#### Invalid object name 'RIODS.TIMELINE'

**Version:** Upgrade to 4.0.0.1 **Error During Upgrade:** Invalid object
name 'RIODS.TIMELINE'. com.microsoft.sqlserver.jdbc.SQLServerException:
Invalid object name 'RIODS.TIMELINE'. **Cause:** This error is caused by
[defect
231471](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=231471)
which is fixed in 4.0.1. You will notice this errors if you do not have
a DW schema setup for your current JTS server before proceedng the
upgrade. **Resolution:** This error can be ignored as it does not block
your JTS from upgrading successfully.

### CCM-specific errors

This section will discuss errors common when adding Database tables to
the Rational Team Concert (CCM) database.

#### CRJAZ0350I Error fetching item values

**Version:** Upgrade to 4.x **Error During Upgrade:** CRJAZ0350I Error
fetching item values. statement = Select S.VAL_ENCODING, S.ITEM_VALUE
From REPOSITORY.ITEM_STATES S Join REPOSITORY.ITEM_TYPES T on
T.ITEM_UUID = S.ITEM_UUID Where S.KEY_UUID = ? parameter\[0\] = xxxxxxx
**Cause:** There are some corrupted item states in your current ccm
repository database. They need to be fixed first before procceding ccm
upgrade. **Resolution:** Run [Online Verify Tool
](https://jazz.net/wiki/bin/view/Main/L3DevTool) to try identifying the
problematic item state and fixing them. The best practice is to perform
data integrity check against your current jts and ccm repository DBs to
ensure data is in a consistent state **prior** to proceeding the
upgrade.

### QM-specific errors

|             |
|-------------|
| IN PROGRESS |

This section will discuss errors common when adding Database tables to
the Rational Quality Manager (QM) database.

### RM-specific errors

|             |
|-------------|
| IN PROGRESS |

This section will discuss errors common when adding Database tables to
the Rational Requirements Composer (RM) database.

### Errors that can occur with any CLM application

This section will discuss errors common when adding the Database tables
to any application within the CLM (they are not application specific).

#### CRJAZ1093I xxxx service class was not activated

**Version:** Any upgrade version 4.x **Error During Upgrade:**
CRJAZ1093I xxxx service class was not activated **Cause:** The server is
unable to connect to the repository database to perform the addTables
command. **Resolution:** Ensure the jdbc driver is in the proper
location according to upgrade instruction and it is compatible with the
JDK version repotools runs on. For example, when connecting to SQL
server DB, sqljdbc.jar works with the JDK 1.5, sqljdbc4.jar works with
the JDK 1.6. For Oracle, JDK 1.5 use ojdbc5.jar, JDK 1.6 use ojdbc6.jar.
The ojdbc14.jar driver will not connect to Oracle 11G etc.

#### ORA-01031: Insufficient privileges

**Version:** Any upgrade version 4.x **Error During Upgrade:**
java.sql.SQLException: ORA-01031: insufficient privileges **Cause:** The
JDBC Connection user does not have enough privileges to run the
necessary commands to add the tables to the database. **Resolution:**
Ensure the JDBC Connection user has DBO permissions on all CLM
applications, including databases for jts, qm, ccm, dw and rm. Note that
the creation of the warehouse on Oracle requires more permissions as
compared to other databases. When you specify the database user in the
connection spec for data warehouse, ensure that the database user has
DBA permissions. Then you can configure a smaller subset of permissions
after the original creation, as identified on [More Control Over the
Oracle DW
Setup](https://jazz.net/wiki/bin/view/Main/MoreControlOverTheOracleDataWarehouseSetup)
article.

#### Unable to create Index MARKERS_UNIQUE_MARKER

**Version:** 4.0.4, SQL Server DB (may also occur on Oracle DB) **Error
During Upgrade:** The following SQL query did not execute properly on
the server: CREATE UNIQUE INDEX MARKERS_UNIQUE_MARKER May be followed by
oracle error: ORA-01450: maximum key length (6398) exceeded **Cause:**
This is caused by a 900 byte limit on MS SQL DBs, where the UUIDs are
too long and hit the byte limit. **Resolution:** This is a known defect
tracked via [jazz.net Defect
280057](https://jazz.net/jazz/web/projects/Jazz20Foundation#action=com.ibm.team.workitem.viewWorkItem&id=280057),
planned to be resolved in 4.0.5. This is referenced in the following
techote: [Upgrading CLM products to version 4.0.4 fails when using
Microsoft SQL
Server](http://www-01.ibm.com/support/docview.wss?uid=swg21649768)

As a **workaround**, only upgrade to 4.0.3, or [contact IBM
Support](http://www-01.ibm.com/software/rational/support/contact.html)
for a hotfix on 4.0.4. On **Oracle** DB, a similar error may occur due
to the NLS_SEMANTICS_LENGTH configuration being *char*. Changing this to
*byte* will resolve the issue.

##### Related topics: [related-topics]

\* For more upgrade troubleshooting topics, refer to [Upgrade
Troubleshooting](UpgradeTroubleshooting).

##### External links: 
None 

##### Additional contributors: 
MainTwiki.StephanieBagot, MainTwiki.SusanWu [external-links-none-----additional-contributors-maintwiki.stephaniebagot-maintwiki.susanwu]
