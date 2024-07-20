META:TOPICINFO{author="geraldmi" date="1429070294" format="1.1"
version="1.3"} META:TOPICPARENT{name="ServiceabilityWhereToStart"}

# Working with CLM Log4j [working-with-clm-log4j]

DKGRAY Authors: Main.GeraldMitchell Build basis: All ENDCOLOR

TOC{title="Page contents"}

UNDER CONSTRUCTION / NOT VERIFIED !!!

This topic is to cover how to manipulate the existing log4j.properties
in order to control log type.

## What is Log4j

Apache Log4j, a logging library for Java, is an Apache Software
Foundation Project and developed by a dedicated team of Committers of
the Apache Software Foundation.

-   [Log4j 1.2 index](http://logging.apache.org/log4j/1.2/index.html)
-   [Log4j 1.2 manual](http://logging.apache.org/log4j/1.2/manual.html)

## Log4j and CLM

The log4j.properties file is in the install/server/conf/app folder of
each CLM application

Based on component you want to debug further, add the corresponding
logger to log4j.properties file to enable logging.

The jazz server produces a feed of log events. You can retrieve the log
from:
protocol://hostname:port/contextroot/service/com.ibm.team.repository.common.internal.IFeedService?category=SystemLog

You can reload the log settings by visiting
protocol://hostname:port/contextroot/admin?internal=true#action=com.ibm.team.repository.admin.reloadLoggingSettings
and clicking Reload Log Settings after you are logged into your CLM
server as a user with an Administrator role.

To reset the logging properties without restarting the server: Log into
the Web Administration interface and navigate to
protocol://hostname:port/contextroot/admin?internal=true. Click on the
Reload log settings link under Internal Tools in the menu on the left
side of the page. Click on the resulting Reload Log Settings button.

NOTE: when the logging is dynamically reloaded, deleting an added option
is not sufficient. The Logging is cumulative and hierarchical, so if you
added an Appender or Logger then that Appender or Logger must have its
threshold set to OFF. Simply deleting the line will not remove it from
current operations.

The log settings are also reloaded every time the server starts. Note
that repotools also has a log4j properties file,
repotools_log4j.properties, in the install/server/conf directory as of
CLM 4.0.5. There is also a "log4jproperties" argument for repotools that
can be set. this is useful for operations such as debugging SQL
connection issues with repotools.

There are three main components to the log4j that can be manipulated
through the log4j.properties: (1)Loggers which have (2)Appenders, which
can be manipulated with (3)Layouts.

The log4j.properties in CLM is able to be manipulated in order to gain
some flexibility in administration and management of CLM deployments.

## Further details into general log4j, with a CLM context

Breaking down the properties file, we can gain some insights into what
we can manipulate and how that will affect the deployment. Note that
because this is all standardized, the references at
<https://logging.apache.org/log4j/1.2/manual.html> along with the
comments in the file can be used to completely manipulate the logging.

\# WARNING: Log messages get persisted in the database as ChangeEvents
for some \# period of time determined by the "ChangeEvent Default
Expiration" setting. By \# default, they get stored for 14 days.
Changing these logging settings \# to cause excessive DEBUG logging
might cause your database to grow much larger \# than normal.

This is actually very important for many reasons. In the event the
database needs to be stored after being used for debugging, restoring
the database to a test system and changing the ChangeEvent Default
Expiration and the log settings to none will allow the log messages to
be removed from the backup, creating a smaller footprint for storage.

### Logger

\# Default logging is for WARN and higher log4j.rootLogger=WARN, stdout,
file

the log4j.rootLogger in the default file consists of 3 parts. The first,
WARN, is a threshold level setting. The second and third settings stdout
and file refer to appenders, the places where the WARN level messages
should be recorded.

#### Logger Threshold Levels

The set of possible threshold levels are in order TRACE, DEBUG, INFO,
WARN, ERROR, and FATAL. In this case, warnings, errors, and fatal
messages will be recorded to the loggers. The stdout logger actually
overrides this threshold level by only logging errors
(log4j.appender.stdout.Threshold=ERROR)

Loggers are chained by level, and the rootLogger is the base level of
that chain. All other loggers inherit from the previous link, so they
all inherit from rootLogger.

Note that logging to more than 1 appender means that you add a
multiplier the performance costs of each write. In a high utilization
scenario this may contribute to a performance degradation.

### Appenders

The following is a section found in all CLM products for describing the
file appender.

\################################################################ \#
File Appender - Threshold WARN \# \# The File attribute represents the
log file name and location \#
\################################################################
log4j.appender.file=org.apache.log4j.RollingFileAppender
log4j.appender.file.MaxFileSize=10MB
log4j.appender.file.MaxBackupIndex=5
log4j.appender.file.File=logs/qm.log
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=d{ISO8601} \[30t\] 5p
-50.50c - mn

This is the base logging file that is used to manage the CLM
application, in this case RQM.
log4j.appender.file=org.apache.log4j.RollingFileAppender

The type of Appender can be changed, including creating a custom
appender using the log4j SDK. The RollingFileAppender javadoc
<http://logging.apache.org/log4j/1.2/apidocs/org/apache/log4j/RollingFileAppender.html>
reveals the information about this appender: it extends the normal file
appender by

-   backing up the previous file and creating a new file after a
    MaxFileSize. (log4j.appender.file.MaxFileSize=10MB)
-   has a controllable MaxBackupIndex to show how far back the files
    will be backed up. (log4j.appender.file.MaxBackupIndex=5)

These capabilities extend the FileAppenders capabilities to have a File
destination (log4j.appender.file.File=logs/qm.log) .

This results in the code level generating a folder for logs 'log' in the
default directory of the running application and having qm.log filled
with messages. When those messages reach 10MB, the file is renamed
qm.log.1 and a new file qm.log is created and starts to be populated.
When there are 5 files, and qm.log needs to be created anew, qm.log.1 is
deleted to make room.

Note that instead of this configuration you could use a different
appender, like
<http://logging.apache.org/log4j/1.2/apidocs/org/apache/log4j/DailyRollingFileAppender.html>
which creates a log for any date pattern, and appends the day and time
to the file name as the file rolls over. The advantage is that every
interval has a new file, regardless of file content. This can be useful
for coordinating with administrator shift changes and backups, for
instance. Be aware that several of the appenders, including
DailyRollingFileAppender, have may have additional caveats. There are
several other appenders in the log4j extras as well, including
DBAppender. See
<http://logging.apache.org/log4j/extras/apidocs/index.html> for more
information. Be aware that you would need to provide the extras to the
log4j class loader as CLM does not provide those jars.

#### Appender Layout

The idea of a layout needs some consideration as well.

The Layout can have multiple types (or again can be customized with some
log4jSDK work and some CLM manipulation) By default we recommend to not
change the layout for CLM provided appenders, as support tooling are
calibrated to this layout. If creating your own appender or you find it
critical to change the layout,

The layout capability is inherited from the base AppenderSkeleton and
consists of a Layout with a specified Conversion Pattern

-   log4j.appender.file.layout=org.apache.log4j.PatternLayout
-   log4j.appender.file.layout.ConversionPattern=d{ISO8601} \[30t\] 5p
    -50.50c - mn

This conversion pattern results in a log message resembling

2014-03-06 19:33:23,753 \[ http-bio-9443-exec-19\] INFO
.repository.service.internal.rdb.ConnectionFactory - CRJAZ1365I The
server is attempting to connect to the following database:
"conf/qm/derby/repositoryDB"

-   d{ISO8601} is the date and time in the ISO8601 format, 2014-03-06
    19:33:23,753, or March 6, 2014 at 7:33PM
-   \[30t\] is the thread generating the message \[
    http-bio-9443-exec-19\]
-   5p is the level of the message INFO
-   -50.50c is the code class that generated the message
    .repository.service.internal.rdb.ConnectionFactory -
-   mn is the message content followed by a newline CRJAZ1365I The
    server is attempting to connect to the following database:
    "conf/qm/derby/repositoryDB"

## Example 1 - more information piped into a different file.

Here is also how to pipe to a different file so that it can be monitored
separately from the rest of the log data. In this example,
com.ibm.team.jfs classes are separated into a file named comibmjfs.log
in the normal logs directory in a JTS subdirectory. The appender will
create up to 20 individual files of 10MB. Note the "additivity" line,
which is crucial to not have the information included elsewhere.

\#log4j.logger.com.ibm.team.jfs=INFO \#commented out the original line
from before the change

\#only allow ERROR and FATAL level messages for the com.ibm.team.jfs
classes \#isolate the jfs log data to a special file file
log4j.logger.com.ibm.team.jfs=ERROR, JFSlog \#keep from propagating to
rootLogger and having dual logging
log4j.additivity.com.ibm.team.jfs=false

\#create a new rolling file appender for use with another file
log4j.appender.JFSlog=org.apache.log4j.RollingFileAppender
log4j.appender.JFSlog.MaxFileSize=10MB
log4j.appender.JFSlog.MaxBackupIndex=20

\#file the new log in a subdirectory
log4j.appender.JFSlog.File=logs/JTS/comibmteamjfs.log

\#follow the normal logging pattern ( could be changed to match relevant
data) log4j.appender.JFSlog.layout=org.apache.log4j.PatternLayout
log4j.appender.JFSlog.layout.ConversionPattern=d{ISO8601} \[30t\] 5p
-50.50c - mn

## Other Information

Coming soon -

-   Manipulating RTC log4j.properties
-   Manipulating RQM log4j.properties
-   Manipulating RRC log4j.properties
-   Manipulating LPA log4j.properties
-   Manipulating JTS log4j.properties

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

-   [Why is my authentication slow? - Recommended Data
    Analysis](https://jazz.net/wiki/bin/view/Deployment/WhyIsMyAuthenticationSlow#Recommended_data_analysis)
-   [How To Enable Verbose Logging For JBE And Ant Tasks To Get More
    Debug Information In Console And
    Logs](https://jazz.net/wiki/bin/view/Deployment/HowToEnableVerboseLoggingForJBEAndAntTasksToGetMoreDebugInformationInConsoleAndLogs)
-   [RTC Build Properties Are Not Transferred To Build Forge - Enabling
    Build Forge debug in the CCM
    log](https://jazz.net/wiki/bin/view/Deployment/RTCBuildPropertiesAreNotTransferredToBuildForge#Enabling_Build_Forge_debug_in_th)
-   [Data Collection and Support
    Resources](https://jazz.net/wiki/bin/view/Deployment/DataCollectionandSupportResources)

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
