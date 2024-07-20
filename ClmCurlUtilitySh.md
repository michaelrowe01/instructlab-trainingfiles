META:TOPICINFO{author="dmmckinn" date="1450473713" format="1.1"
version="1.2"} META:TOPICPARENT{name="WebPreferences"}

# Use ClmCurlUtility.sh to access CLM server functions from a command line. [use-clmcurlutility.sh-to-access-clm-server-functions-from-a-command-line.]

DKGRAY Authors: Main.ErikMats Build basis: 4.0.3, 6.0. ENDCOLOR

TOC{title="Page contents"}

ClmCurlUtility.sh is a script that allows you to access POST, GET, PUT,
DELETE operations on a CLM server from a command line. It handles logins
and cookie management (for X-Jazz-CSRF-Prevent).

The script uses "Curl" on Cygwin (Windows) or Linux systems.

It allows you to automatically iterate to create N users or projects,
which is handy for testing.

This script uses the same command line parameters as RqmUrlUtility. It
does add an -iterations N option to run the same invocation N times. It
adds special GET (stdout) and POST (stdin + stdout) options.

Unlike RqmUrlUtility, it does not require XML input.

## Examples

\# DB Ping time once \# 2\>/dev/null means: disregard errors. Remove
this from the end of the line to get more diagnostic output.
./ClmCurlUtility.sh -command GET -user jazzadmin -password jazzadmin
-context ccm -filepath GET -url
<https://clm.example.com:9443/ccm/service/com.ibm.team.repository.service.internal.IServerConnectionStatusRestService/databasePingTime>
2\>/dev/null

\# DB Ping time three times: \# -iterations 3 means: Run three times.
./ClmCurlUtility.sh -command GET -user jazzadmin -password jazzadmin
-context ccm -filepath GET -url
<https://clm.example.com:9443/ccm/service/com.ibm.team.repository.service.internal.IServerConnectionStatusRestService/databasePingTime>
-iterations 3 2\>/dev/null

\# DB Ping time Jazz.net Sandbox: \# Just to make sure this works on
multiple hosts ./ClmCurlUtility.sh -command GET -user jazzadmin
-password jazzadmin -context sandbox02-qm -filepath GET -url
<https://jazz.net/sandbox02-qm/service/com.ibm.team.repository.service.internal.IServerConnectionStatusRestService/databasePingTime>
2\>/dev/null

\# Create 50 users, Charlie10000 through Charlie10049 \# Echo data
fetched from a Firebug request body. \# The string REPLACEME will be
replaced with the number of each iteration; 10000, 10001, ... \#
-filePath POST causes DATA to be read from stdin, output to go to
stdout. echo
"itemId=new&name=CharlieREPLACEME&userId=CharlieREPLACEME&emailAddress=CharlieREPLACEME40clm.example.com&jsonRoles=5B22JazzUsers225D&jsonLicenses=7B22add223A5B5D2C22remove223A5B5D7D"
\| ./ClmCurlUtility.sh -command POST -user jazzadmin -password jazzadmin
-context jts -filepath POST -url
<https://clm.example.com:9443/jts/service/com.ibm.team.repository.service.internal.IAdminRestService/contributor>
-iterations 50 2\>/dev/null

\# Get all QM project areas \# Link grabbed from Firebug log of
performing the same operation in the web UI \# Note double quotes around
a URL that contains "&". \# Output is saved to projectAreas.xml.
./ClmCurlUtility.sh -command GET -user jazzadmin -password jazzadmin
-context qm -filepath projectAreas.xml -url
"<https://clm.example.com:9443/qm/service/com.ibm.team.process.internal.service.web.IProcessWebUIService/projectAreasPaged?hideArchivedProjects=true&owningApplicationKey=JTS-Sentinel-Id&pageNum=0&pageSize=1000>"
2\>/dev/null

## The script

... to follow

## System Requirements ---+++ Linux

Requires bash and Curl

### Windows

Requires Cygwin with bash and Curl.
