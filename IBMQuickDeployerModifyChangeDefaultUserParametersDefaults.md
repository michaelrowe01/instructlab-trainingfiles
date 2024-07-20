META:TOPICINFO{author="kenneth" date="1462362501" format="1.1"
reprev="1.14" version="1.14"}
META:TOPICPARENT{name="IBMQuickDeployerSetupAndRun"}

# IBM Quick Deployer modify Change Default User Parameters defaults DKGRAY [ibm-quick-deployer-modify-change-default-user-parameters-defaults-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

Follow the instructions in this topic to permanently change the default
values used by the UCD **ChangeDefaultUserParameters** application
process. If you are changing any of the user parameters (such as
passwords) and you wish them to be obscured from the user you should
follow the instructions on the [Securing User
Passwords](IBMQuickDeployerSecuringUserPasswords) wiki page.

## Modify the Change Default User Parameters defaults

Be aware that once changed individual default values cannot easily be
reset. You should make a copy of the default values prior to making any
changes so that the defaults can be restored if needed.

1\. Open application **Rational_QD_60x**, select the **Processes** tab
and click on the **Change Default User Parameters** process.

1\. When the process opens select the **Configuration** tab and then
select **Application Process Properties**. Chose the property you wish
to change and click **Edit**. *You can change all fields except the
property name*.

1.  When your changes are complete click **Save**.
2.  Repeat for each property that you want to change.

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="MCDUPD_1.png" attachment="MCDUPD_1.png"
attr="h" comment="select Change Default User Parameters"
date="1443697741" path="MCDUPD_1.png" size="26648" user="kenneth"
version="1"} META:FILEATTACHMENT{name="MCDUPD_2.png"
attachment="MCDUPD_2.png" attr="h" comment="edit property"
date="1443697763" path="MCDUPD_2.png" size="44756" user="kenneth"
version="1"} META:FILEATTACHMENT{name="MCDUPD_2a.png"
attachment="MCDUPD_2a.png" attr="h" comment="edit property"
date="1462362500" path="MCDUPD_2a.png" size="59389" user="kenneth"
version="1"}
