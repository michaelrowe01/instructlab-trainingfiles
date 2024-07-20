META:TOPICINFO{author="aalaird" date="1389905004" format="1.1"
reprev="1.4" version="1.4"} META:TOPICPARENT{name="ServerRename"}

# Rational Synchronization Server: What to do when Rational Team Concert server is renamed [rational-synchronization-server-what-to-do-when-rational-team-concert-server-is-renamed]

DKGRAY Authors: Main.SuryaTripathi Build basis: Rational Synchronization
Server 1.4; Rational Team Concert 4.0; Rational Change 5.3.0.3 iFix001;
Rational Synergy 7.2.0.2 iFix002 ENDCOLOR

TOC{title="Page contents"}

This article is intended for Rational Synchronization Server users who
have or are going to rename the Rational Team Concert server.

## Why CLM server renames can cause problems for Rational Synchronization Server

You can use the Rational Synchronization Server to synchronize work
items and change requests between IBM Rational Team Concert and IBM
Rational Change. If a CLM server is renamed, the Rational
Synchronization Server cannot connect to Rational Team Concert and stops
the synchronization of work items and change requests. Also, users can
no longer navigate to work items from change requests in Rational
Change.

## What you need to do

For the Rational Synchronization Server to continue to synchronize data
between Rational Team Concert and Rational Change, you must perform the
following steps:

### Step 1: Update the Rational Team Concert server URL that is stored in Rational Synchronization Server

Edit the template file and update the URL:

1.  Stop the Rational Synchronization Server.
2.  Locate the adapter template file that contains the Rational Team
    Concert server URL. The template file is created in XML format and
    is located here:
    \webapps\TlogicIntegration\WEB-INF\conf\Templates\changertcadapter\adaptertemplates
3.  There is a template file for each RTC-Change synchronizer. You must
    update the Rational Team Concert server URL in each template file.
    Update the value of the `rtcservername` tag with the new Rational
    Team Concert server URL.
4.  For example, you could change: <https:///ccmto:https:///ccm>

### Step 2: Update the Rational Team Concert work item URLs that are stored in Rational Change

The Rational Synchronization Server links a change request to a work
item and keeps the two items synchronized. The system also stores the
URL of the work item in an attribute on the change request. So, each
change request contains the URL of the work item to which it is linked.
While configuring the URL mapping of the synchronizer, the system
determines which change request attribute stores the work item URL. Each
RTC-Change synchronizer has a different URL mapping attribute.

When the Rational Team Concert server is renamed, the work item URL
changes. So, for each synchronizer, you must replace the content of the
URL mapping attribute with the new work item URL for each change request
and for each Rational Synergy database.

Rational Synergy 7.2.0.2 Interim Fix 002 and Rational Change 5.3.0.3
Interim Fix 001 contain commands that you can use to update the URL. You
do not need to know the URL of every work item. All you need to know is
the new base URL of the Rational Team Concert server and the Rational
Change attributes that store the work item URL.

For each Rational Synergy database that contains URL mapping attributes,
perform the following steps:

1.  Ensure that you have the **ccm_admin** role.
2.  Stop the Rational Change server and the Rational Synchronization
    Server.
3.  Determine which attributes in Rational Change the Rational
    Synchronization Server uses to store work item URLs.
4.  Turn off DCM and process all pending receives to get DCM into a
    clean and stable state.
5.  Start a Synergy CLI session.
6.  Set your role to **ccm_admin**.
7.  Run the `ccm update_urls` command (see the [The update_urls
    command](#AboutUpdate) section below).
8.  Turn on DCM.

\#AboutUpdate

### The update_urls command

`ccm update_urls -change -old_url old_server_url -new_url new_server_url attribute_name...`

-   **-change**: Specifies it is a Rational Change command.
-   **-old_url**: Specifies the old server URL.
-   **-new_url**: Specifies the new server URL.
-   **-attribute_name**: Specifies the change request attribute names,
    separated by a space, whose value might contain a reference to an
    old URL that needs to be updated.

For example, you have five RTC-Change synchronizers and the five change
request attributes used for URL mapping are `rtc_url1`, `rtc_url2`,
`rtc_url3`, `rtc_url4` and `rtc_url5`.

The old work item URL is of the following form:
`https://MyRTCServer:9443/ccm/resource/itemName/com.ibm.team.workitem.WorkItem/68`

If **MyRTCServer** is renamed to **MyNewRTCServer**, the work item URL
changes to the following form:
`https://MyNewRTCServer:9443/ccm/resource/itemName/com.ibm.team.workitem.WorkItem/68`

Run the following command to update the URL:
`ccm update_urls -change -old_url !https://MyRTCServer:9443/ccm -new_url !https://MyNewRTCServer:9443/ccm rtc_url1  rtc_url2 rtc_url3 rtc_url4 rtc_url5`

## What happens to comments

The Rational Synchronization Server allows you to optionally synchronize
comments between work items and change requests. When the server is
renamed, Rational Team Concert updates all work item comments that
contain old work item URLs. You must run the `update_urls` command in
Rational Change to replace old work item URLs in change request comments
with new URLs to ensure that old change request comments do not
synchronize and add to work item comments again.

Run the following command to update the URLs in change request comments:
`ccm update_urls -change -old_url !https://MyRTCServer:9443/ccm -new_url !https://MyNewRTCServer:9443/ccm transition_log`

## How to test that the URL update is working

After you successfully run the `update_urls` command, start Rational
Change and open a change request that is linked to a work item. Locate
the URL mapping attribute. Copy the value, and then paste it into your
web browser. You should be prompted to log in to Rational Team Concert
to view the work item details.

Start the Rational Synchronization Server. Look in the synchronization
log. The log should indicate that Rational Synchronization Server is
able to connect to the Rational Team Concert interface and is
successfully synchronizing work items and change requests.

##### Related topics: [Server Rename](ServerRename) [related-topics-server-rename]

##### Additional contributors: Main.RosaNaranjo [additional-contributors-main.rosanaranjo]
