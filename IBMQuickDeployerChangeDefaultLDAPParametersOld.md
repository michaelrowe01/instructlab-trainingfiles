META:TOPICINFO{author="ktessier" date="1501278327" format="1.1"
reprev="1.18" version="1.18"}
META:TOPICPARENT{name="IBMQuickDeployerSetupAndRunOld"}

# IBM Quick Deployer change default LDAP parameters DKGRAY [ibm-quick-deployer-change-default-ldap-parameters-dkgray]

INCLUDE{"IBMQuickDeployerInsertAuthorBuildBasis"} ENDCOLOR

TOC{title="Page contents"}

Before you run the UrbanCode Deploy **Install Applications** application
process, you must set the default LDAP parameters. You can set these
parameters when you run the
[installer](IBMQuickDeployerInstallingIntoUCD) by entering the values in
the ldap.properties file, which is included in the Quick Deployer
package. Alternatively, you can set the parameters by running the
**Change Default LDAP Parameters** application process.

Once you have a working set of LDAP parameters, you can permanently
change the default values by following the instructions in the [Modify
Change Default LDAP Parameters
Defaults](IBMQuickDeployerModifyChangeDefaultLDAPParametersDefaults)
wiki page.

## Change default LDAP parameters 1. Open application **Rational_QD_60x** and run process **Change Default LDAP Parameters** on the target environment

1\. If you fixed the component versions on the process you will not be
prompted to choose versions. If offered to choose the component
versions, then select Latest Available.

1.  Modify the process property default values to match your LDAP
    server. Note - When an LDAP property contains a comma separated list
    of values there can not be any spaces in or between the values in
    the list.

More information about each property can be found at one of the
following external sites \* [Managing Jazz users with
LDAP](https://jazz.net/jazzdocs/index.jsp?topic=/com.ibm.team.install.doc/topics/c_plan_identity_management.html)
\* [Configuring WAS LDAP general registry
settings](http://www-01.ibm.com/support/knowledgecenter/SS7JFU_6.1.0/com.ibm.websphere.express.doc/info/exp/ae/tsec_ldap.html?cp=SS7JFU_6.1.02F1-7-9-9-0-1-0-2)
\* [Configuring WAS LDAP advanced registry
settings](http://www-01.ibm.com/support/knowledgecenter/SS7JFU_6.1.0/com.ibm.websphere.express.doc/info/exp/ae/usec_advldap.html?cp=SS7JFU_6.1.0)
The properties are as follows \* **LDAP Vendor** : TDS - IBM Tivoli
Directory Server *Default* : TDS \* **LDAP Hostname** : The fully
qualified hostname of the LDAP *Default* : localhost \* **LDAP Port** :
The port to use to connect to LDAP *Default* : 389 \* **Group member ID
map** : Specifies the LDAP filter that identifies user-to-group
relationships. *Default* : \*:member \* **User ID map** : Specifies the
LDAP filter that maps the short name of a user to an LDAP entry
*Default* : \*:uid \* **User filter** : Specifies the LDAP user filter
that searches the user registry for users *Default* :
(&(uid=v)(objectclass=inetOrgPerson)) \* **Group ID map** : Specifies
the LDAP filter that maps the short name of a group to an LDAP entry
*Default* : \*:cn \* **Group filter** : Specifies the LDAP group filter
that searches the user registry for groups *Default* :
(&(cn=v)(objectclass=groupOfUniqueNames)) \* **Bind distinguished name**
: The bind DN is required if anonymous binds are not possible on the
LDAP server to obtain user and group information. If the LDAP server is
set up to use anonymous binds, leave this field blank. *Default* : none
\* **Bind password** : the password corresponding to the bind DN
*Default* : none \* **Base distinguished name** : The base DN indicates
the starting point for searches in this LDAP directory server. *Default*
: ou=people,dc=jazz,dc=net \* **LDAP Registry Location** : The location
of the LDAP registry *Default* : <ldap://localhost:389> \* **Base User
DN** : Base distinguished name of users in the LDAP registry. *Default*
: ou=people,dc=jazz,dc=net \* **Base Group DN** : Base distinguished
name of the Jazz application groups in the LDAP registry *Default* :
ou=JazzGroups,dc=jazz,dc=net \* **Jazz to LDAP Group Mapping** : Mapping
between Jazz groups and LDAP groups. One Jazz group can be mapped to
multiple LDAP groups. The LDAP groups must be separated by a semi colon.
For example, JazzAdmins=LDAPAdmins1;LDAPAdmins2 maps JazzAdmins group to
LDAPAdmins1 and LDAPAdmins2. *Default* : JazzAdmins=JazzAdmins,
JazzUsers=JazzUsers, JazzProjectAdmins=JazzProjectAdmins,
JazzGuests=JazzGuests \* **Group Name Property** : Property to represent
the name of the Jazz groups in the LDAP registry. *Default* : cn \*
**Group Member Property** : Property to represent the members of a group
in the LDAP registry. *Default* : members \* **User Property Names
Mapping** : Mapping of Jazz user property names to LDAP registry entry
attribute names. The mapping should be represented as
{contributorAttributeName1}={LDAPEntryAttributeName1},
{contributorAttributeName2}={LDAPEntryAttributeName2}... *Default* :
userId=uid,name=cn,emailAddress=mail \* **findGroupsForUserQuery** :
Query String to find Groups containing a User *Default*:
member={USER-DN} \* **LDAP Jazz Admins Group** : Map the Jazz Admins
group to corresponding LDAP groups. *Default*: cn\\JazzAdmins,dc\\domain
\* **LDAP Jazz Users Group** : Map the Jazz Users group to corresponding
LDAP groups. *Default*: cn\\JazzUsers,dc\\domain \* **LDAP Jazz Guests
Group** : Map the Jazz Guests group to corresponding LDAP groups.
*Default*: cn\\JazzGuests,dc\\domain \* **LDAP Jazz Project Admins
Group** : Map the Jazz Project Admins group to corresponding LDAP
groups. *Default*: cn\\JazzProjectAdmins,dc\\domain \* **LDAP Registry
User** : User name to access LDAP registry. Anonymous mode is used if
user name and password are not specified. *Default* : none \* **LDAP
Registry Password** : Password to access LDAP registry. Anonymous mode
is used if user name and password are not specified. *Default* : none

1\. Click on **Submit** and wait for the process to run to completion

INCLUDE{"IBMQuickDeployerInsertMiscellaneous"}

META:FILEATTACHMENT{name="CDLP_1.png" attachment="CDLP_1.png" attr="h"
comment="run process" date="1443709611" path="CDLP_1.png" size="51920"
user="kenneth" version="1"} META:FILEATTACHMENT{name="CDLP_2.png"
attachment="CDLP_2.png" attr="h" comment="select Latest Available"
date="1443709631" path="CDLP_2.png" size="39542" user="kenneth"
version="1"} META:FILEATTACHMENT{name="CDLP_4.png"
attachment="CDLP_4.png" attr="h" comment="wait for completion"
date="1443709682" path="CDLP_4.png" size="26708" user="kenneth"
version="1"} META:TOPICMOVED{by="ktessier" date="1501276476"
from="Deployment.IBMQuickDeployerChangeDefaultLDAPParameters"
to="Deployment.IBMQuickDeployerChangeDefaultLDAPParametersOld"}
