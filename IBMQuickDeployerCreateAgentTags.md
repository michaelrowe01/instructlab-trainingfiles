META:TOPICINFO{author="ktessier" date="1501529284" format="1.1"
version="1.17"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRunOld"}

# IBM Quick Deployer create agent tags DKGRAY [ibm-quick-deployer-create-agent-tags-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

Quick Deployer makes use of **tagging** to ensure it only installs and
executes the required scripting and middleware on the individual servers
in the environment. By following this topic it ensures that when you
create a [UCD Environment](IBMQuickDeployerEnvironmentConstruction) all
the required tags are available.

## Create agent tags

1.  Ensure you are in the folder where you previously expanded the IBM
    Quick Deployer installation package eg **/media/QD**
2.  Ensure the following files are present
    -   tagsCreate.sh
    -   tagsCreate.json
3.  Assign execute permission to the **tagsCreate.sh** script
4.  ensure JAVA_HOME is set. If not export JAVA_HOME={location of your
    jre} (e.g. /usr/lib/jvm/jre)
5.  ensure UCDCLIEXE is set. If not export UCDCLIEXE={location of your
    udclient exe} (e.g. /opt/ibm-ucd/agent/opt/udclient/udclient)
6.  Execute the **tagsCreate.sh** script The script expects 3 arguments
    as key=value pairs:
    -   **USERNAME** =UCDAdminUserName
    -   **USERPASSWORD** =UCDAdminUserPassword
    -   **UCDSERVER** =UCDURL (e.g. https://UCDHostName:8443)

\- as lots of information is written to the screen it is recommended
that when executing the script the output should be **piped through the
tee program** for post processing.

cd /media/QD chmod 755 tagsCreate.sh export JAVA_HOME={location of your
jre} export UCDCLIEXE={agent install dir}/agent/opt/udclient/udclient

sh tagsCreate.sh USERNAME=adminuser USERPASSWORD=adminpassword
UCDSERVER=ucdurl:port \| tee console_tagsCreate.log \>\> deleted console
text \<\< end of file \[tagsCreate.sh\]

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}
