META:TOPICINFO{author="lekandrade" date="1694545462" format="1.1"
version="1.4"} META:TOPICPARENT{name="ServerRename"}

# Case study: Server rename (version 4.0.1) [case-study-server-rename-version-4.0.1]

DKGRAY Authors: Main.HeatherSterling, Main.HuiBinShi, Main.EricSolomon
Build basis: Rational solution for Collaborative Lifecycle Management
4.0.1 ENDCOLOR

TOC{title="Page contents"}

This article describes the experience of our in-house Rational
Engineering Services (RES) team when they performed a successful server
rename in our internal production environment. Server rename is defined
as changing the public URL for the Jazz Team Server (JTS) and one or
more of its registered applications. The URL change can include any or
all of the following components: protocol, hostname, domain, port, or
context root. The scenario described in this article involves changing
the context root. For a good overview of server rename in version 4.0.1,
including supported scenarios, cautions, outage planning, and the
recommended sequence of operations, see [Renaming your Rational solution
for Collaborative Lifecycle Management server (version
4.0.1)](ServerRenameCLM401).

## Description of Environment

As shown in Figure 1, the rename scenario in our internal production
environment is complex and involves four Jazz Team Servers. The first
JTS, clmhost01, is the target server to be renamed. The clmhost01 server
also includes the Change and Configuration Management (CCM) application.
For this article, the context root of the JTS and CCM will be changed
from /jts01 and /ccm01 to /jts02 and /ccm02, respectively. In the next
table, the context root is highlighted in **bold**.

| URL before the rename | URL after the rename |
|:---|:---|
| https://clmhost01.example.org/ **jts01** | https://clmhost01.example.org/ **jts02** |
| https://clmhost01.example.org/ **ccm01** | https://clmhost01.example.org/ **ccm02** |

**Note** Although it is most common to change the host name during a
server rename, changing just the context root in a Tomcat environment
requires a new server installation that mirrors the old installation,
but with new context roots. In the WebSphere example that is described
in this article, we show how you can use symbolic links as a way to
avoid a new server installation. Make sure that you generate a mapping
file against the original server. For more information about changing
the context root when you perform a server rename, see the "Changing the
context root" topic in the Jazz Team Server Installing book in the [IBM
Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

In our example, the CCM application on clmhost01
(`clmhost01.example.org/ccm01`) has a friends relationship with another
CCM application (`ccm03.example.org/jazz`). As a result, the
`ccm03.example.org` repository stores URLs from clmhost01. When we
change the URLs on clmhost01, we also need to update the URLs that are
stored on `ccm03.example.org`. For more information about this scenario,
see Step 9 in the "Server rename checklist" section of [Renaming your
Rational solution for Collaborative Lifecycle Management server (version
4.0.1)](ServerRenameCLM401).

The `ccm03.example.org` server is part of a distributed deployment,
where the JTS, CCM, QM, and RM applications are installed on different
systems. In our case, we did not utilize mapped network drives for this
server rename activity, which required us to perform an extra step. For
details, see [Performing the rename on the other Jazz Team
Servers](#PerformRenameOther).

Finally, all of the servers in the internal production environment are
running a version of the Linux operating system. All of the database
servers are running a version of DB2 on the AIX operating system, and
all of the Jazz Team Servers and applications are hosted on WebSphere
Application Server.BR

## Planning the Rename

Because server rename is a complex and potentially disruptive process,
it is very important that you plan the rename carefully and have a good
understanding of what you are trying to accomplish. Before you start,
review the risks and precautions, software version requirements, and
supported scenarios described in the "Planning for server rename"
section of the Jazz Team Server Installing book in the [IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

In addition, it is very important to plan for the amount of outage time
that is needed. In particular, do not underestimate the time needed to
perform verifications. You can reduce overall outage time by having
multiple people perform the verifications simultaneously. Also, if you
have multiple linked deployments, you must consider the outage time for
all deployments, which must be performed simultaneously and completed at
the same time. For further details about planning the outage time, see
the "Server rename outage Planning" section in [Renaming your Rational
solution for Collaborative Lifecycle Management server (version
4.0.1)](ServerRenameCLM401).

Following are the high-level steps in performing a server rename:

1.  Call IBM Software Support to obtain a "server rename feature key
    file".
2.  Get a complete list of the servers that are affected. For more
    information, see [Identifying the servers that are
    affected](#IdentifyServers). The list must include all Jazz Team
    Servers, all servers that are used for distributed CLM applications,
    and all servers that have friend relationships with the servers that
    you plan to rename. This list will help you identify the people that
    will be affected by the rename so you can notify them in advance of
    the planned outage and involve them in verifications on the rename
    day.
3.  Schedule a time to upgrade the servers to CLM version 4.0.1. We
    upgraded the servers well in advance of the rename, which allowed us
    to isolate and correct any upgrade issues from any rename issues and
    also helped us avoid having one big outage.
4.  Set up a staging environment. In our case, we decided to test the
    rename in a staging environment before making the changes to the
    production environment. Despite the investment in time and hardware
    that is required, we strongly recommend this approach.
5.  If there is a reverse proxy, firewall or allowlist involved,
    determine what needs to be changed and make the changes before
    performing the rename.
6.  Set up daily scrum meetings to check the status of the rename and
    resolve any issues that come up.
7.  On the target server to be renamed, in this case clmhost01, create a
    test work item that includes links with source URLs, as shown next.
    You will verify these URLs after the rename.BR

<https://clmhost01.example.org/jts01>
<https://clmhost02.example.org/ccm01>

1.  Identify any other stakeholders who should know about or may need to
    help with the rename. This may include network, database, and
    application administrators, infrastructure people, and developers.
    In our case, this also included IBM Support. It is also important to
    get management support and have relevant managers involved.
2.  Generate the mapping file against the original server by using the
    **repotools-jts -generateURLMappings** command, as shown next:

./repotools-jts.sh -generateURLMappings toFile=clmhost01_mappings.txt
repositoryURL=<https://clmhost01.example.org/jts01>
adminUserId=JazzAdmin adminPassword=JazzAdmin
additionalURLFile=additionalurl.txtFor further details, see the
"Preparing the mapping file" topic in the Jazz Team Server Installing
book in the [IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
The generated mapping file should like this:
\#clmhost01.example.org/jts01
source=<https://clmhost01.example.org:443/jts01>
target=<https://clmhost01.example.org:443/jts01>
\#clmhost01.example.org/jts01
source=<https://clmhost01.example.org/jts01>
target=<https://clmhost01.example.org/jts01> \#Additional Urls included
in rename by clmhost01.example.org/jts01 \#(CLM Help URL)
source=<https://clmhost01.example.org/clmhelp>
target=<https://clmhost01.example.org/clmhelp> \#/ccm01
source=<https://clmhost01.example.org:443/ccm01>
target=<https://clmhost01.example.org:443/ccm01> \#/ccm01
source=<https://clmhost01.example.org/ccm01>
target=<https://clmhost01.example.org/ccm01>

1.  Review and edit the generated mapping file carefully. Among other
    things, you will need to edit the `target=url` statements for the
    entries that you want to rename, as shown below:

\#clmhost01.example.org/jts01
source=<https://clmhost01.example.org:443/jts01>
target=<https://clmhost01.example.org:443/jts02>
\#clmhost01.example.org/jts01
source=<https://clmhost01.example.org/jts01>
target=<https://clmhost01.example.org/jts02> \#Additional Urls included
in rename by clmhost01.example.org/jts01 \#(CLM Help URL)
\#source=<https://clmhost01.example.org/clmhelp>
\#target=<https://clmhost01.example.org/clmhelp> \#/ccm01
source=<https://clmhost01.example.org:443/ccm01>
target=<https://clmhost01.example.org:443/ccm02> \#/ccm01
source=<https://clmhost01.example.org/ccm01>
target=<https://clmhost01.example.org/ccm02> For a complete list of what
to review in the generated mapping file, see Step 4 in the "Preparing
the mapping file" section of the Jazz Team Server Installing book in the
[IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).BR
**Note** In our case, the deployment includes a proxy server, and
therefore the JTS and/or CCM server have two URLs. Make sure to include
all URLs in this mapping file. For example, if there is a proxy server
(`proxy.example.org`) in front of clmhost01, both the JTS and CCM will
need to include the following additional mappings:
source=<https://proxy.example.org/jts01>
target=<https://proxy.example.org/jts02>

source=<https://proxy.example.org/ccm01>
target=<https://proxy.example.org/ccm02>

1.  Verify the mapping file by using the **repotools-jts
    -verifyURLMappings** command, as shown next. For details, see the
    "verifyURLMappings" topic in the Jazz Team Server Reference book in
    the [IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

./repotools-jts.sh -verifyURLMappings
mappingFile`clmhost01_mappings.txt repositoryURL`
<https://clmhost01.example.org/jts01> adminUserId=JazzAdmin
adminPassword=JazzAdmin

\#IdentifyServers

## Identifying the servers that are affected

The rename impacts not only the server itself, but also any servers that
have integrations with the server to be renamed. Here are the steps for
identifying the other servers that are impacted.

1.  Log in to clmhost01 as an administrator and type
    `https://clmhost01.example.org/jts01/admin`. Click **Server** to
    view the JTS Server Administration page. Click **Registered
    Applications** to find the URLs for all of the applications
    registered with the JTS. Click **Consumers (Inbound)** to view the
    list of internal consumers and click **Friends (Outbound)** to view
    the list of external outbound servers. For details, see the
    "Configuring OAuth" and "Configuring friends" sections in the Jazz
    Team Server Administering book in the [IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
2.  Categorize the applications by JTS and then identify the servers
    that are impacted. In our case, `ccm03.example.org` contains the
    links from clmhost01; thus, `jts02.example.org` is impacted.
3.  List the applications that are registered with jts02, in this case,
    ccm02, ccm03, qm02, and rm02. These servers are all impacted by this
    rename activity. Upgrade all of them to the same software version,
    back up the databases prior to the rename, and shutdown these
    servers during the rename.
4.  Repeat for any additional Jazz Team Servers.
5.  Identify the end users and project administrators who will be
    involved during the production server rename. They will need to
    verify things such as work item links, dashboards, builds, and so
    on.

## Setting up the staging environment

Even though it requires an investment in additional hardware, software,
and personnel, we decided to test the rename in a staging environment
before making the changes to the production environment. The staging
environment should be identical to the production environment, except
that the IP addresses are different.BR

The ideal situation is to use an isolated subnet for staging. If this is
not possible, add the IP hostname mapping in the `/etc/hosts` file.
Everyone working in the staging environment must be careful not to
contaminate production data or vice versa. You should also create
mappings to mask the servers that are not present in the staging
environment. For additional details about staging environments, see the
"Topologies and mapping files for setting up a test staging environment"
topic in the Jazz Team Server Installing book in the [IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).BR

Here is how you can set up the staging environment to avoid any
confusion with the existing production environment:BR

1.  Copy the database backups to the database servers in the staging
    environment.
2.  Install the identical version of CLM to the staging application
    servers and update the `teamserver.properties` files to point to the
    staging databases.
3.  Create an IP host name mapping list for all of the staging servers
    and send the list to everybody working on the staging servers,
    including the people who will help to do the verifications. For
    example, the IP address of `clmhost01.example.org` in production is
    `192.168.100.10`, while its IP address in staging is `172.16.0.18`.
    We added the following entry to `/etc/hosts` on all of the staging
    servers:172.16.0.18 clmhost01.example.org
4.  Set up dedicated machines to act as clients. This allows everyone to
    continue to connect to the production servers while working on the
    staging servers.
5.  Differentiate the staging servers from the production servers by
    uploading a theme. This updates the banner to indicate that the
    server is used for staging. For details, see Step 3a in the "Setting
    up a test staging environment with production data" topic of the
    Jazz Team Server Installing book in the [IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
6.  Follow the instructions in the next section to perform the rename in
    the staging environment. Write down the steps and the changes that
    you make in the staging environment. This information will be
    valuable when you perform the rename in production.
7.  Keep track of the time needed to perform the rename in the staging
    environment and the overall down time. This will be useful later
    when you need to communicate to the user community about the outage
    in the production environment. Be sure to include the recovery time
    to roll back the environment to the pre-rename state.

\#PerformRenameTarget

## Performing the rename on the target server (clmhost01)

This section provides the detailed steps for performing the rename. For
additional details, see the "Moving a pilot or full production
deployment by using server rename" topic in the Jazz Team Server
Installing book in the [IBM Knowledge
Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

1.  Shut down all servers involved in the rename and back up the Jazz
    Team Server database, the databases for the CCM and QM applications,
    the data warehouse database, and the RRDI content store database, if
    applicable.
2.  If you are using Tomcat as your application server, shut down the
    clmhost01 server and then install a new copy of version 4.0.1 using
    the new context root.
3.  If you are using WebSphere, you must first disable the application
    auto-start feature from the WebSphere administration console for
    both JTS and CCM, as shown next:BR BRBR
4.  (WebSphere) Using a command prompt, stop the WebSphere profile
    instance.

profile root/bin/stopServer server1 profileName profileName

1.  Copy the server rename feature key file to the
    InstallDir/server/conf directory and back up the
    `teamserver.properties` file for both the JTS and the CCM
    application.
2.  Review the updated mappings file that was generated during the
    planning phase. If significant time has passed since you generated
    the mappings file, you can regenerate it against the old
    installation and verify it again.
3.  Perform the offline portion of server rename against the new
    installation by importing the mappings file from the old
    installation into the clmhost01 Jazz Team Server, as shown next. For
    details about this part of the rename process, see Step 3 in the
    "Moving a pilot or full production deployment by using server
    rename" topic of the Jazz Team Server Installing book in the [IBM
    Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

./repotools-jts.sh -importURLMappings
fromFile="./clmhost01_mappings.txt"

1.  (WebSphere) Navigate to the directory where the WebSphere profile is
    located and remove the caches:

profile root/temp/node/server1/

1.  (WebSphere) Restart the WebSphere profile for
    `clmhost01.example.org` as shown next:

profile root/bin/startServer server1 profileName profileName

1.  (WebSphere) Change the context roots to /jts02 and /ccm02 in the
    WebSphere administration console and then save the configurations.BR
    BRBR Here is an example for /jts02:BR BRBR Here is an example for
    /ccm02:BR BRBR
2.  (WebSphere) When the import completes, navigate to the `server/conf`
    directory and create symbolic links to jts02 and ccm02,
    respectively, as shown below.BR **Note** By creating symbolic links,
    you avoid the need to reinstall CLM 4.0.1 with the new context root.

\# ln -s jts01 jts02 \# ln -s ccm01 ccm02 \# ls -l \*02 lrwxrwxrwx. 1
root root 5 Nov 17 08:24 ccm02 -\> ccm01 lrwxrwxrwx. 1 root root 5 Nov
17 08:23 jts02 -\> jts01

1.  Start both the JTS and CCM. (With WebSphere, start the JTS and CCM
    from the WebSphere administration console.) At this point, the CLM
    applications will synchronize with the Jazz Team Server to apply the
    URL mappings and update their data warehouse data. This should take
    about five minutes for a small data set and up to 30 minutes or more
    for a very large data set.
2.  Log into the Jazz Team Server at
    `https://clmhost01.example.org/jts02/serverRenameStatus`. This
    starts the actual renaming process. When the rename completes, you
    will see a green icon that indicates that the server rename is
    successful. The JTS and registered applications will be in read-only
    mode.BRBR BRBR
3.  Click **Next** to start the server rename verification wizard. Do
    not click **Finish** until the entire rename process has completed
    successfully and after you complete the steps in [Performing the
    rename on the other Jazz Team Servers](#PerformRenameOther). Leave
    the server in read-only mode for now. For details, see the
    "Verifying URLs and links after a server rename\]" topic in the Jazz
    Team Server Installing book in the [IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
4.  Look for the server alert message on the upper-right portion of the
    window, which indicates that the server is being validated and no
    write operations can be performed (read-only mode).BR BR
5.  Check Diagnostics. For details, see the "Verifying the Jazz Team
    Server" topic in the Jazz Team Server Installing book in the [IBM
    Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
6.  Check the test work item that you created earlier to see that the
    URLs are renamed successfully, as shown
    next:<https://clmhost01.example.org/jts02>

<https://clmhost02.example.org/ccm02>

1.  Be sure to have CCM users verify their project areas, work items,
    dashboards, and links. For details, see the "Verifying Change and
    Configuration Managment" topic in the Jazz Team Server Installing
    book in the [IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).

\#PerformRenameOther

## Performing the rename on the other Jazz Team Servers

Because the CCM application on clmhost01 has a friend relationships with
a CCM application on another Jazz Team Server, you also need to update
the URLs that are stored in the friends repositories by running the
**repotools-jts -importURLMappings** command.

1.  On `jts02.example.org`, copy the `clmhost01_mappings.txt` file that
    you previously imported to clmhost01 to `jts02.example.org`.
2.  Copy the server rename feature key file to the
    `jts02.example.org server/conf` directory.
3.  Shut down the `jts02.example.org` CLM instance and back up the
    databases.
4.  Import the `clmhost01_mappings.txt` file, as shown
    next:./repotools-jts.sh -importURLMappings
    fromFile="./clmhost01_mappings.txt"
5.  Copy the `.mappingEvent` file from the
    `JazzInstallDir_/server/conf/jts/` directory on `jts02.example.org`
    to each application `conf` directory, for example
    `server/conf/jazz/` on `ccm02.example.org` and `server/conf/jazz` on
    `qm02.example.org`.BR **Note** This step is necessary only if you do
    not map network drives. For details and alternatives, see Steps 3b
    and 3c in the "Moving a pilot or full production deployment by using
    server rename" topic of the Jazz Team Server Installing book in the
    [IBM Knowledge
    Center](http://www-01.ibm.com/support/knowledgecenter/SSYMRC/clm_family_welcome.html).
6.  Start the applications and Jazz Team Servers on jts02, ccm02, ccm03,
    qm02, and rm02.
7.  Repeat steps 13-18 in the [Performing the rename on the target
    server](#PerformRenameTarget) section for `jts02.example.org`. As
    mentioned previously, do not click **Finish** until the entire
    rename process is complete. The jts02 Jazz Team Server and the other
    applications registered on jts02 are now in read-only mode.
8.  When the verifications are complete on all servers, including the
    server that is being renamed, click **Finish** on the rename status
    page to exit read-only mode.BR BR BRBR Confirm that the following
    banner disappeared.BR BRBR
9.  Re-enable auto-start for clmhost01 from the WebSphere Administration
    console.

##### Related topics: [Deployment web home](ServerRename) [related-topics-deployment-web-home]

##### Additional contributors: Main.RosaNaranjo [additional-contributors-main.rosanaranjo]

META:FILEATTACHMENT{name="Figure3a.png" attachment="Figure3a.png"
attr="h" comment="" date="1383226297" path="Figure3a.png" size="66412"
user="rnaranjo" version="1"} META:FILEATTACHMENT{name="Figure1.png"
attachment="Figure1.png" attr="h" comment="" date="1383226317"
path="Figure1.png" size="218422" user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="Figure3.png" attachment="Figure3.png" attr="h"
comment="" date="1383226724" path="Figure3.png" size="35276"
user="rnaranjo" version="1"} META:FILEATTACHMENT{name="Figure4.png"
attachment="Figure4.png" attr="h" comment="" date="1383226736"
path="Figure4.png" size="48811" user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="Figure5.png" attachment="Figure5.png" attr="h"
comment="" date="1383226754" path="Figure5.png" size="45869"
user="rnaranjo" version="1"} META:FILEATTACHMENT{name="Figure8.png"
attachment="Figure8.png" attr="h" comment="" date="1383227672"
path="Figure8.png" size="132460" user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="Figure7.png" attachment="Figure7.png" attr="h"
comment="" date="1383227688" path="Figure7.png" size="25955"
user="rnaranjo" version="1"} META:FILEATTACHMENT{name="Figure6.png"
attachment="Figure6.png" attr="h" comment="" date="1383227705"
path="Figure6.png" size="135548" user="rnaranjo" version="1"}
