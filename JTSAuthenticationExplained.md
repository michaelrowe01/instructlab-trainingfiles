META:TOPICINFO{author="sbeard" date="1394022908" format="1.1"
version="1.12"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Jazz Team Server (JTS) authentication explained [jazz-team-server-jts-authentication-explained]

DKGRAY Authors: Main.StevenBeard, Main.TimFeeney Build basis: The
Rational solution for Collaborative Lifecycle Management (CLM) ENDCOLOR

TOC{title="Page contents"}

## Security facilities

The Jazz Team Server application is packaged as a Java Enterprise
Edition (Java EE) web application and as such runs in a supported Java
EE container using a standard authentication, authorization, and
permission model. The application also uses a set of predefined roles
that are assigned to users, for authorization to access specific URLs or
to perform specific low-level operations (for example: read, write,
administer). The "container" is another term for "application server",
such as IBM WebSphere Application Server or Apache Tomcat. The
authentication itself is managed by the container; if a user fails to
authenticate by providing a valid user ID and password, the container
rejects the request without the request ever reaching the application.
When the user successfully authenticates, the container subsequently
forwards the successfully authenticated request to the application (Jazz
Team Server in this case) along with the current user's authorization
(group memberships or role) for processing. Within the operation that
processes the request, the application first checks that the user is
assigned a role with requisite authority to perform the operation.

The configuration of the authentication and authorization is done at the
container level, at login time the application server retrieves the user
information from the external user directory. Apache Tomcat Realm and
Lightweight Directory Access Protocol (LDAP) are external user
registries supported by the Jazz Team Server application. To support
authorization, the group membership of the users must be managed in the
user registry. LDAP may be used with both [Apache
Tomcat](http://jazz.net/library/article/457) and [WebSphere Application
Server](http://jazz.net/library/article/96). Jazz Team Server
authentication is further explained in this technote:
[TN0013](http://jazz.net/library/article/75). Finally, in Rational Team
Concert 3.0, support for Common Access Card (CAC) Smart Card and generic
certificate based authentication is provided. For more information, see
[Configuring certificate authentication in Rational Team Concert 3.0
using WebSphere Application Server
7.0](https://jazz.net/library/article/606).

After a user is authenticated and is authorized to access the Jazz
repository, the application (such as Rational Team Concert) performs
process-level authorization based on the user's role and the permissions
and operation behaviors that have been allowed for that role. Roles
identify the functions of team members and can be defined at the project
level or within a team area. Permissions are then assigned for specific
operations to roles at the project level or within a team area. A user
may be assigned more than one role. Behaviors define preconditions and
follow-up actions for individual operations. This behavior encourages or
enforces process rules for your project and your teams. Behavior is
defined in the project's process configuration and can be customized by
team areas. For a demonstration of permissions in Rational Team Concert,
see this [video](http://jazz.net/library/video/106). Permissions and
behaviors as described here is the general Jazz model; however, how it
is implemented and exposed to the user varies between the applications.

New to the Rational solution for Collaborative Lifecycle Management
(CLM) 2012 are a few additional security features at the individual
product levels to support finer read and write controls of project
artifacts. Rational Requirements Composer adds support for additional
fine-grained write access controls for artifacts and folders by project
and team for controlling write access to shared resources. Rational Team
Concert extends the component and stream level scoping adding support
for global folder level security within SCM to public, private, and
scoped. Rational Quality Manager adds support for finer grained access
control within project area and team areas.

Licensing also impacts the security model and whether an authenticated
user is able to perform actions they are authorized to do. The licensing
model used in the Rational solution for CLM 2012 is the same as
described in [Licensing in the Rational solution for Collaborative
Lifecycle Management (CLM) 2011](https://jazz.net/library/article/548).

For Jazz products to interact with each other, each server must add the
other server to its list of friends. Further, application project areas
must be linked together to enable artifact linking. In the Rational
solution for CLM 2012, this friend configuration is handled
automatically through the post-installation [setup
wizard](http://publib.boulder.ibm.com/infocenter/clmhelp/v3r0m1/topic/com.ibm.jazz.install.doc/topics/t_s_server_installation_setup_wizard.html)
and creation of [lifecycle
projects](http://jazz.net/blog/index.php/2011/05/12/countdown-to-clm-2011-part-1-administering-lifecycle-projects/).

##### Related topics: [Deployment planning and design](DeploymentPlanningAndDesign) [related-topics-deployment-planning-and-design]

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]

META:TOPICMOVED{by="sbeard" date="1384787658" from="Deployment.Security"
to="Deployment.JTSAuthenticationExplained"}
