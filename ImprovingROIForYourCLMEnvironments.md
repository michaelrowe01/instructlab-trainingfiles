META:TOPICINFO{author="sahilkmansuri" date="1700823084" format="1.1"
version="1.7"} META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Improving ROI for your CLM environments [improving-roi-for-your-clm-environments]

DKGRAY Authors: Main.HariVetsa Build basis: CLM ENDCOLOR

TOC{title="Page contents"}

## Introduction

Rational Engineering Services (RES) supports three major IBM Rational
Collaborative Lifecycle Management (CLM) environments. One for
Rational-brand development teams, one behind jazz.net, and another for
an Intranet application development team.

There are over 25,000 unique users across these three environments
working on over 1,800 projects. These projects hosted in three different
data centers consist of 64 different CLM applications and 79 individual
servers.

The cost of supporting such large environments is enormous. Since the
beginning, RES has been focusing on the cost reduction of hosting a CLM
environment. These efforts are in line with delivering value to our
organization and to our customers.

This article provides a list of investments, policy decisions and
methods RES has undertaken to reduce the cost footprint and improving
the overall quality of service. Not all of these items will produce the
same benefit to all CLM deployments. Different deployments (within IBM
or outside) will provide different benefits based on the deployment
characteristics. Therefore, during this article, I will try to stay away
from specifics of benefits or cost reduction. I will provide guidance
for various considerations to evaluate the benefits for each of them for
your own analyses.

## List of Topics

1\) Separation of database and application layers

2\) Standardization of application software

3\) Automatic user account provisioning

4\) Hosting multiple CLM servers in a single system

5\) Adoption of Virtualization technologies (Intel and Power platforms)

6\) Geographically distributed support staff

7\) Locate CLM projects that are geographically diverse on a CLM server

8\) Investment in automation

9\) Investment in monitoring

10\) Create shortcuts for most commonly used commands

11\) Streamline onboarding and off-boarding process.

This article discusses each of the above topics in detail as they apply
to our three CLM deployments.

### Separation of database and application layers

All three of our CLM deployments separate database and application
layers onto different systems. We have a set of systems that host DB2
services exclusively and another set of systems that exclusively host
CLM services.

While there is an argument that hosting database services on a remote
machine than the CLM system induce a network lag, we have not observed
any measurable performance lag in this regard. We recognize that this
model may be cost prohibitive for small installations that fit into
departmental topology. This model has worked very well for us.

By using this model, we were able to create enterprise policies to
manage these systems appropriately. The management and support of these
systems is more streamlined by this separation. The fact that the
database services are on a remote systems also allowed us to achieve
High Availability using DB2 High availability disaster recovery (HADR)
feature.

Since some of the software licenses are based on the processing power of
the entire host, you may also be able to save on IBM DB2 (or Oracle) and
WebSphere licensing costs. This is largely dependent on the licensing
model for your environment.

### Standardization of application software

For our first Jazz server, as it was known during version 1.0, we hosted
our services using Tomcat and DB2 on separate systems. Over a period of
time, we started the adoption of WebSphere for our application server.
We quickly realized the difficulties in hosting CLM services using a mix
of application server software. Our support processes became
complicated, because we had to keep track of which server was hosting
using Tomcat and which ones were using WebSphere. The application server
software determines commands to stop, start, deploy and debug. The log
files are also located in different locations. The troubleshooting
methods differed vastly.

We quickly standardized all of our servers to WebSphere. Now the
install, upgrade and support processes are identical. This benefit would
be identical if your choice of application server is Tomcat.

WebSphere also allows us to update the application software independent
of the CLM software and map multiple LDAP groups to a single Jazz role
(JazzUsers, JazzAdmins etc.).

### Automatic user account provisioning

CLM provides a rich set of user management interface. It provides a way
to import users from LDAP server and automatically assign licenses. Our
CLM installation had additional requirements over and above what is
offered by CLM out of the box.

Within enterprises like IBM, corporate governance may require additional
handling of the user accounts. For example, we are required to track
access of users to individual project areas, assign separate licenses
types for users, generate proper reporting of user subscriptions, and
control access to different project areas that belong to the same CLM
server.

During the initial stages, we could process about 100 users per day per
full-time administrator. This is an extremely high cost to manage user
access. To reduce the burden, we partnered with Tivoli and their IBM
Tivoli Identity Manager (ITIM) product team to create an adapter that
provision accounts on CLM servers including custom license assignments
and access to individual project areas.

This changed the entire process of user provisioning. We went from a
managed process to a self-service process. Today we dont have any
administrators working on user account provisioning. This ITIM CLM
adapter is responsible for the creation of up to 20,000 of our 25,000
user accounts. In addition there is no wait time for the user to gain
access to the CLM servers. Any user can gain access using the ITIM
service immediately once entitlement is complete.

It is easier for us because we already have an ITIM deployment that
manages other services in the enterprise. This item may not be suitable
for small deployments. More details on this adapter are available at the
IBM website: <http://www-01.ibm.com/support/docview.wss?uid=swg21396546>

### Hosting multiple CLM servers in a single system

Please note that this is a slightly different topic than virtualization.
Our first deployment was to host a single CLM service process on a
single operating system host. This host can be either virtual or
physical. Subsequently we realized that this is not the optimal use of
the hardware or operating system.

Both Tomcat and WebSphere allow us to run multiple processes on the same
operating system as long as the service ports dont conflict. This will
eliminate the overhead of running operating system processing for each
of the CLM server, as well as the operating system software licensing
costs.

The Rational deployment team never liked the idea of hosting different
CLM servers on different ports or being tied to the operating system for
any CLM server. In order to maintain independence from the operating
system, we allocated a separate IP address to each of the configured CLM
servers on any given host. This allows us to migrate the CLM servers
from one host to another without causing any inconvenience to end users.

By consolidating many CLM servers on a single host, we were also able to
reduce our operating system support personnel resources.

### Adoption of Virtualization technologies (Intel and Power platforms)

Most of our current CLM infrastructure was migrated from physical
systems to Virtual platforms. The application servers are standardized
on an xSeries virtual platform. The database servers use either xSeries
or pSeries virtualization. There are still some physical hosts for a
variety of reasons that are not related to the reduction of cost.

The benefits of virtualization are common knowledge in the IT industry.
The benefits we perceive are dynamic sizing of the hardware resources
and leveraging the automatic failover of the virtual images in an event
of hardware failures. Virtualization also provided us with a capability
to create a new CLM server with full configuration using templates.

We also dont need to provision full capacity hardware at the inception
of the service. We can start with a low capacity configuration and add
hardware resources like processors or memory as we grow. If we reach the
optimal capacity for a virtual machine configuration, we can migrate CLM
server(s) from one host to another using the best practice described in
Hosting multiple CLM servers in a single system section.

The above are in addition to the benefits our infrastructure maintenance
team realizes from virtualizing the hardware.

### Geographically distributed support staff

It is a common phenomenon to have development and test teams across the
world. This implicitly dictates the need to have the CLM servers to be
available around the clock. With continuous delivery practices this need
becomes more critical. Our CLM services are assumed to be supported
without interruption. In case of any unexpected service interruption,
services are expected to be restored with minimal downtime.

Two years into supporting the CLM services, we started leveraging the
support from different geographies. This enabled us to provide business
hours support during all weekdays, day and night. In essence, we have
business coverage of more than 80 hours in any given week. By adjusting
the workday shift before and after, we have business hours coverage from
9:00 PM EDT Sunday until 9:00 PM EDT on Friday.

Another big advantage which directly translates to business benefit is
that this support model allows us to schedule maintenance activities
during any CLM Servers off hours. For example, if RTC01 server is
heavily used by a US team, we can let the China support staff team
upgrade the server thereby reducing the business impact to the
development and support teams.

By reducing the amount of time our support staff needs to spend
off-hours to support, upgrade or maintain different software components
we have greatly improved the employee morale and dedication of the
support personnel.

### Locate CLM projects that are geographically dispersed on a CLM server

If you have multiple CLM servers and a large number of projects, you can
assign project areas on these CLM servers in a manner to spread the load
on these CLM servers around the clock.

For example, if you host US team projects on RTC01 and all India team
projects on RTC02, then entire processing resources allocated to RTC01
will be idle during night-time US hours and vice versa. Instead, you can
balance projects that are geographically dispersed across RTC servers
which to create a natural load balancer. This spread allows your
processing resources to be utilized around the clock.

This method will reduce the amount of hardware resources that needs to
be allocated to the entire CLM deployment across the enterprise. Within
Rational, we started out this way. Today, we loosely adhere to this
principle. The majority of our CLM servers have geographically dispersed
projects, but there are some CLM servers that have an affinity to users
from specific time zones.

### Investment in automation

This is one of our biggest value provider principles. Our approach is to
automate any process that is a repeatable activity and technologically
possible to automate. Most of our automation is based on scripting
languages like Shell, Perl, php.

One example of our automation is the deployment of a CLM software to an
existing WebSphere based CLM server. The script takes some input
parameters including the location of the new CLM software. It
automatically stops the CLM server, installs the new code, runs
addTables, deploys the new warfiles and starts the servers. We inform
our users ahead of time about the upgrade window. During the upgrade
window, we manually invoke the upgrade script. Upon completion of the
update, we manually verify the integrity of the upgraded CLM server and
send the completion notification to our users. This process has greatly
reduced the unavailability of our CLM Servers by reducing the time
required to upgrade as well as eliminate mistakes during the upgrade
process. As we all know, less downtime and improved quality translates
to increased benefit.

Among other things, we have the following tasks automated:

-   Backups of databases and application servers without interrupting
    the services

<!-- -->

-   CLM software upgrades

<!-- -->

-   Silent installation and upgrade of WebSphere and DB2 software.

Our collection of automated tasks has been increasing as we get more
experienced with CLM hosting. We want the administrators supporting the
CLM server to identify the need and solve it using automation. There is
no allocation of a separate resource pool for creating automation. Some
of these scripts have already been shared with the development team so
that they can convert them into a more generic format and deliver them
as part of CLM product suite.

### Investment in monitoring

If a particular CLM server is not functioning as expected the
administrator on call will be notified in less than 15 minutes.
Historically the admin response time is no more than 15-30 minutes.
Including troubleshooting, problem determination and resolution, the
impacted CLM server could be up with in matter of another few minutes.
In an extremely favorable situation, like during business hours, the
time to detect, react and restore the service has been less than 10
minutes.

We achieved this through aggressive monitoring of our CLM servers.

The current monitoring system is a set of simple Perl scripts that
programmatically simulate browser calls, parse the return responses and
notify admins using an email to SMS method. The example script is
provided on jazz.net article Monitoring your Rational solution for
Collaborative Lifecycle Management servers in your environment at the
link: <https://jazz.net/library/article/1017>.

The overall benefit is for our end users to have as minimal amount of
downtime as possible and to provide confidence with regards to the
overall availability and stability of the hosted CLM services. This
allows them to plan their deliverables with less contingency time
factored in.

On the same note, we are close to deploying our next generation
monitoring using the IBM Tivoli OMNIbus tool. OMNIbus will provide more
tools and features to administrators to reduce the mean time to recovery
(MTTR) and be transparent about our application availability status to
all our end users.

### Create shortcuts for most commonly used commands

Any administrator supporting CLM on WebSphere would know the long
commands to stop and start WebSphere. These commands are more complex in
our environment because we have multiple instances of WebSphere servers
running at any given time.

It takes time to construct these commands and any typographical mistakes
will result in delay in execution of those commands. This is especially
important when critical CLM services are unavailable.

To help alleviate this we have created short cuts (shell aliases) for
many of these commands. For example, to stop RTC01, you can create an
alias as below

\$ alias stopRTC01="/opt/IBM/WebSphere/AppServer/bin/stopServer.sh
server1 -profileName RTC01 -<username=hvetsa@us.ibm.com> -password=\$1"

Subsequently, you can invoke the command with your password as shown
below

\$ stopRTC01

There is a onetime setup activity to load all your aliases into your
shell profile file like .profile or .bash_profile or .cshrc. The above
example works in bash shell.

### Streamline onboarding and off-boarding processes

We gather a set of important operational information from each of the
project teams that want to use our hosted CLM services before the
project area is created. This information is pretty basic and listed
below:

1\) Expected disk storage allocation

2\) Expected team size

3\) Expected number concurrent users

Based on the above input, we choose which one of our CLM servers is best
suited as the location for their project area. Our objective is to find
a way to distribute users, storage and load across all CLM servers
evenly. We dont keep track these metrics as much as we should. The work
around for us is to let a single person handle the onboarding tasks, so
he/she knows the recent history of onboarding and choose where the next
project area should be created.

We keep other metrics like repository sizes, active project area count
and active user count for each of the CLM servers, to help us identify
the location of the next CLM project.

## Summary

As you may have seen, we leveraged the principles mentioned in this
article to maintain an efficient CLM hosting service for our users. All
the above methods have helped us in reducing the cost of operation
and/or increase the overall quality of the CLM Hosting area.

By no means does the Rational CLM deployment team consider this process
complete. We continuously try to push the envelope to create or improve
efficiencies. As these efficiencies evolve, we may choose to update our
community using an addendum or post another topic.

If you have any questions, feedback or suggestions of any future topics
or an in depth discussion on any of the above methods, Feel free to
contact the author.

## Reference Environment Diagrams

The following are the high level application level diagrams for the
three environments to which the above methods were applied.

### Jazz.net

### Rational Brand CLM Hosting

### IBM Account

## About the Author

Hari Vetsa is the architect/team lead responsible for three successful
CLM deployments with in IBM with a combined user base of approximately
25,000. He works for Rational Engineering Services, which is responsible
for providing Application and Infrastructure services to the Rational
Brand. His team also holds the webmaster responsibilities for the
<https://jazz.net> site and has been hosting Jazz Services for Rational
and Jazz.net for the last 5 1/2 years. Hari's background is mostly in
operations providing database, UNIX and LDAP services.

## Heading 1

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]

META:FILEATTACHMENT{name="ROI_Jazz.net.png"
attachment="ROI_Jazz.net.png" attr="" comment="Jazz.net Architecture"
date="1381242715" path="ROI_Jazz.net.png" size="78634" user="hvetsa"
version="3"}
META:FILEATTACHMENT{name="ROI_Rational_Brand_CLM_Hosting.png"
attachment="ROI_Rational_Brand_CLM_Hosting.png" attr=""
comment="Rational Brand CLM Hosting Architecture" date="1381242826"
path="ROI_Rational_Brand_CLM_Hosting.png" size="131163" user="hvetsa"
version="2"} META:FILEATTACHMENT{name="ROI_IBM_Account.png"
attachment="ROI_IBM_Account.png" attr="" comment="IBM Account
Architecture" date="1381198124" path="ROI_IBM_Account.png" size="122290"
user="hvetsa" version="1"}
