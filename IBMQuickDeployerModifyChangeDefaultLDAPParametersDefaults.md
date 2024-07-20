META:TOPICINFO{author="tomp" date="1462827428" format="1.1"
version="1.16"} META:TOPICPARENT{name="IBMQuickDeployerSetupAndRun"}

# IBM Quick Deployer modify Change Default LDAP Parameters defaults [ibm-quick-deployer-modify-change-default-ldap-parameters-defaults]

DKGRAY INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

Follow the instructions in this topic to permanently change the default
values used by the UCD **ChangeDefaultLDAPParameters** application
process.

## Modify the Change Default LDAP Parameters defaults

Be aware that once changed individual default values cannot easily be
reset. You should make a copy of the default values prior to making any
changes so that the defaults can be restored if needed.

1\. Open application **Rational_QD_60x**, select the **Components** tab
and click on the **Rational_QD_SystemPre-Requisite_60x** component

1\. When the component opens select the **Processes** tab and click on
the **ChangeDefaultLDAPParameters** process

1.  When the process opens select the **Configuration** tab and then
    select **Component Process Properties**. Chose the property you wish
    to change and click **Edit**.

Note - When an LDAP property contains a comma separated list of values
there can not be any spaces in or between the values in the list. *You
can change all fields except the property name.*

1.  When your changes are complete click **Save**.
2.  Repeat for each property that you want to change.

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="MCDLPD_1.png" attachment="MCDLPD_1.png"
attr="h" comment="select Rational_QD_SystemPre-Requisite_600 component"
date="1443699588" path="MCDLPD_1.png" size="31339" user="kenneth"
version="1"} META:FILEATTACHMENT{name="MCDLPD_2.png"
attachment="MCDLPD_2.png" attr="h" comment="select Change Default
LDAPParameters process" date="1443699611" path="MCDLPD_2.png"
size="39222" user="kenneth" version="1"}
META:FILEATTACHMENT{name="MCDLPD_3.png" attachment="MCDLPD_3.png"
attr="h" comment="edit Component Process Properties" date="1443699646"
path="MCDLPD_3.png" size="58857" user="kenneth" version="1"}
