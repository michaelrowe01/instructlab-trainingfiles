# Automating collection of querystats and counters - examples 

Authors: Main.IanBarnard, Main.WilliamChatham 
Build basis: IBM Engineering Requirements Management DOORS Next 7.x.


When collecting must-gather information for DOORS Next, you are asked to
collect Foundation Counters as html and to start querystats collection,
then reproduce the problem, then collect counters and querystats html
pages. This information is an important part of the
[MustGather](https://www.ibm.com/support/pages/ibm-doors-next-generation-performance-mustgather),
particularly for performance issues.

This page gives you some examples of how the html collection and
querystats steps might be automated using a command-line approach which
invokes curl to login and then collect the needed information.

The attached scripts are provided as as-is illustrative samples only,
i.e. without any support or warranty. You use them at your own risk.

## Background

To collect these diagnostics pages from DOORS Next you have to be
authenticated as a JazzAdmin user. It's no different if you want to
automate the page collection, which will make basically the same HTTP
GET operations as using the RM admin UI.

The examples attached to this page are for Windows (cmd) and for Linux
(bash). They both start by using curl to login, and these examples use
hard-coded credentials. You may be able to implement more secure
authentication than the methods in the script using curl.

But if you do use the scripts they authenticate as the specified user
and save the authentication cookie to a file cookies.txt which is then
used to authenticate the subsequent requests. The cookies are valid for
whatever is the authentication expiry timeout of your deployment - this
is commonly two or six hours but may have been configured differently in
your deployment. The scripts do delete cookies.txt, but again you may
want to improve this handling.

NOTE these scripts have only been tried with Form-based authentication;
they may not authenticate for deployments using JAS or other forms of
authentication.

## Pre-requisites

1\. To use the scripts attached you must have curl available - the same
sequence of operations could be implemented using a different
programmatic way of accessing your DOORS Next server, but that is
outside the scope of this article.

2\. You must enable repodebug - this has to be done manually, and can be
done once and left enabled or manually enabled/disabled around the
script run. Steps: Browse to
[https://SERVER:PORT/rm/admin](https://SERVER:PORT/rm/admin) \> Advanced
Properties, set"Enable repodebug service" to 'true' and then Save. NOTE
that restart is not required when changing this setting.

### Collection steps:

Once you have configured the scripts for your environment - in
particular the server URL, JazzAdmin user name and password, you can run
the script.

The collection scripts have the following steps:

1\. Login using hard-coded user/password to create a saved
authentication cookie

2\. Collect counters html (before) to counters_before.html

3\. Stop/reset/start querystats collection

4\. Wait for user to press a key - this is when the issue is reproduced,
then a key pressed

5\. Collect counters html (after) to counters_after.html

6\. Collect querystats html to querystats_after.html

7\. Delete the saved authentication cookie

Following this you can attach the three html files to the support case.

The example scripts are attached to htis page:

\* For Windows (cmd)

\* For Linux (bash)

### Customizing the scripts

The examples have in the first few lines some variables which must be
configured for your environment: they are for the JazzAdmin user name,
password and server URL. The examples in the script are illustrative and
are not for a publicly accessible server.

##### Related topics:

* [DOORS Next MustGather](https://www.ibm.com/support/pages/ibm-doors-next-generation-performance-mustgather), 
* [Oracle Must Gather](OracleMustGather), 
* [Db2 Must Gather with repodebug](CollectingDB2SectionActualsUsingRepodebug) 
* [related-topics-doors-next-mustgather-oracle-must-gather-db2-must-gather-with-repodebug]

-   [getstats.bat](ATTACHURL/getstats.bat): Example of a Windows cmd
    batch file to collect counters and querystats

<!-- -->

-   [getstats.sh](ATTACHURL/getstats.sh): Example of a Linux bash script
    file to collect counters and querystats
