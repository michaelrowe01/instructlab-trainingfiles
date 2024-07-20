META:TOPICINFO{author="sbeard" date="1402818367" format="1.1"
reprev="1.10" version="1.10"}
META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Implementation planning and deployment roadmap [implementation-planning-and-deployment-roadmap]

DKGRAY Authors: Main.JohnDuckmanton Build basis: The Rational solution
for Collaborative Lifecycle Management (CLM) and the Rational solution
for systems and software engineering (SSE) ENDCOLOR

TOC{title="Page contents"}

Adopting new systems or software engineering tools and practices on a
large scale is a significant technological and organizational challenge
that requires an appropriate level of coordination, collaboration, and
governance to be successful.

This article describes four best practices to ensure successful
deployment and user adoption:

-   Address all aspects of the solution
-   Build the right team
-   Deploy capabilities, not tools
-   Tackle larger deployments incrementally

## Address all aspects of the solution

Deploying software into the enterprise is more complicated than just
provisioning hardware and installing your software on it. There are many
aspects that require careful consideration and planning to ensure that
the software works correctly, performs as expected, integrates
effectively with other systems, and supports your business processes.
The software users must also receive the necessary training to know how
to use it effectively.

The **IBM Rational Development Environment Architecture (DEA)** is a
framework that you can use to address all aspects of deployment of new
tools, working practices, or both.

The DEA addresses:

-   The processes or working practices to be adopted or incorporated
    into the tools (method)
-   The tools to be deployed and their integrations to other systems
-   Enablement in methods and tools
-   The infrastructure required to support methods, tools and enablement
-   Organization (to use and support methods, tools, enablement and
    infrastructure)
-   The plan for adoption of the above elements

Across all of these areas are cross-cutting concerns, such as the
functionality to be provided and constraints placed on the solution such
as capacity, performance, and availability.

### Method [method]

A key element of any development environment is the method that is
followed, whether formally or informally, by practitioners. A method
defines project roles, tasks, work products, and processes. It is also
underpinned by guidelines, standards, templates, and examples that can
be applied on a project.

### Tools [tools]

Development tooling automates aspects of the method being followed. For
example, you might use a tool for storing and managing requirements on
the project, or use a tool for visually modeling architectures and
designs, or use particular tools for testing software, and so on.

### Enablement [enablement]

Enablement (training and mentoring) of practitioners in the use of the
development environment contributes to its successful adoption.
Therefore, an aspect of a development environment is the definition and
creation of training and mentoring materials that can be applied. The
enablement itself is focused on the use of the method and tools within
the environment.

### Infrastructure [infrastructure]

Method, tools, and enablement are supported by some infrastructure
(hardware and software). For example, you might want to web-enable the
method, and then deploy it on the company intranet, which would require
a web server and some hardware on which to run it. Development tools are
often run on practitioner workstations with an appropriate specification
in terms of CPU, memory, and disk. Training materials can be made
available via several mechanisms, over and above classroom training --
for example, web-based training would require the presence of a web
server and associated hardware.

### Organization [organization]

The right organization is critical to support the use of a development
environment. This might include providing specialists in certain aspects
of the environment (such as method experts, tool specialists, trainers,
and mentors), personnel to administer and support the environment, and
personnel to augment the existing set of skills available through the
company help desk. In addition to the environment itself, which requires
people, there is clearly a need to create (develop) the development
environment, which also requires people, including the development
environment architect.

### Adoption [adoption]

Adoption addresses the process of putting all of the above elements in
place in an organized way and ensuring that the benefits expected from
the development environment are being achieved. This is more than simply
acquiring the relevant hardware and software, installing and configuring
the environment, and training and mentoring end users. Adoption is
equally concerned with the migration of existing assets, such as work
products residing in a now-legacy tool set, and the collection of
measurements that allow the development environment to be assessed
against desired results. It is important to recognize that this adoption
represents a change in the organization and needs to be managed as such.

### Cross-cutting elements [cross-cutting-elements]

There are, of course, elements that cut across the areas described
above, and they represent functionality, qualities, or constraints. The
*functionality* provided by a development environment represents a
particular software engineering discipline, such as testing. A *quality*
represents a property that is exhibited by the development environment,
such as the ability for the development environment to scale to support
different numbers of concurrent users. A *constraint* represents a
restriction on the options that are available for implementing the
development environment, such as the need to accommodate a particular
operating system.

For more information about the *IBM Rational Development Environment*
see [The rise of the Development Environment
Architect](http://www.ibm.com/developerworks/rational/library/edge/08/apr08/eeles/)
on IBM developerWorks.

## Build the right team

Adopting new software or systems engineering tools and practices on a
large scale is a significant technological and organizational challenge
that requires an appropriate level of coordination, collaboration, and
governance in order to be successful. It will also impact, directly and
indirectly, a large number of people within the organization. These key
user groups are instrumental in the success of the adoption effort:

**Executive sponsorship**

Change will happen more smoothly with effective leadership. When the
vision, goals, and benefits are effectively communicated and understood,
and the adoption is correctly planned and managed, people will naturally
align the work that they do toward achieving those goals. Achieving
executive-level support for the change initiative within the target
organization is therefore critical.

**Solution deployment team**

Key to the success of any large-scale deployment is the deployment team
itself. Typically, this will be comprised of personnel in these roles:

-   **Project management** Personnel who are focused on planning and
    organization, day-to-day management, and status reporting for the
    deployment.

<!-- -->

-   **Solution architecture** One or more personnel who are focused on
    defining the overall solution technical architecture and providing
    architectural governance during the deployment.

<!-- -->

-   **Domain and product subject matter experts** Personnel with
    specialist knowledge in one of more of the domains affected; for
    example, requirements management; or specialists in particular
    aspects of the tooling solution. It is important to focus on
    identifying and growing these skills early during the deployment.

<!-- -->

-   **Trainers, coaches, and mentors** Internal personnel or external
    consultants with the skills and experience required to build the
    expertise of the SMEs initially, and support training and mentoring
    activities during the adoption.

<!-- -->

-   **External consultants** For example, experts from tool vendor
    organizations, management, or process consultants.

**IT support teams**

A large-scale tools deployment will require ongoing collaboration with
several other IT support teams, such as IT infrastructure support,
database support, network support, help desk support, and application
support. For example, collaboration is required to procure and provision
the required hardware and networking infrastructure to host the
solution, and to provide appropriate support for that infrastructure
throughout the deployment. It is important to understand the support
required and engage with these groups as early as possible.

**Stakeholders**

It is important to the success of the deployment to understand who all
the stakeholders are and their needs and expectations. You must
continually ensure that the stakeholder needs are being addressed and
that they are kept informed of progress throughout the adoption.

For more information, see [Establishing a systems and software
engineering ecosystem center of
excellence](DeploymentEstablishingACenterOfExcellence).

## Deploy capabilities, not tools

Organizations adopting IBM Rational products are typically not just
looking to install new tools, but are looking to them to provide one or
more capabilities, such as requirements management, source control, and
performance testing. Sometimes, the organization might already have the
capability and is looking to better tools or practices to help them to
increase their effectiveness.

Many IBM Rational tools support more than one capability. Therefore, it
is important when deploying a new solution to understand what
capabilities you want to deploy. Doing this will help you focus on the
short-term goals of the deployment, the scope of any tool configuration,
the impact on any existing methods or practices, and the associated
enablement needs. It will also help you ensure that you deliver
something of value to stakeholders. When you are deploying the solution
to a large number of users, a capability-based deployment can also
provide a means to organize incremental delivery of functionality in
discrete manageable chucks (See below).

## Tackle larger deployments incrementally

Deploying a new tooling solution can be a significant change effort
within an organization. Therefore, you must keep in mind that an
organization can effectively support only a given size of change effort.
There are many underlying reasons for this, including these reasons:

-   The time lag between initial purchase and realization of the benefit
    might be too large leading to loss of management focus

<!-- -->

-   The disruptive impact of the transition to new tools and working
    practices will become too great and will impact on core business
    activities

<!-- -->

-   The organization will have a limited capacity to enable and support
    new users

In addition, practitioners can cope with only a certain level of change;
beyond that point, productivity and enthusiasm levels begin to suffer
significantly. To avoid this, introduce the new capability incrementally
in a number of phases. When doing this, it is important to consider a
number of factors:

-   Carefully identifying the right capability to include in each
    increment, ensuring that practices and associated tooling are
    delivered together

<!-- -->

-   The value and priority of each increment to the stakeholders

<!-- -->

-   The implications of not having all the expected new capability at
    once. Often this can lead to temporary workarounds or duplication of
    effort. This needs careful communication in order not to impact on
    morale and expectations.

The diagram below illustrates a typical incremental deployment in a
series of "waves," each comprising a number of phases:

1\. **Assessment & planning** Where the activities to be performed in
the current wave are identified and planned 1. **Solution build** The
infrastructure is established, the tools are installed and configured,
and supporting materials, such as training and mentoring materials, are
created. 1. **Pilot and/or early adoption** The solution is trialed with
a small number of users in order to validate the technical solution and
the readiness of the deployment team and gain feedback. 1. **Large-scale
deployment & embedding** The capability is gradually rolled out to the
entire user community

When planning your adoption roadmap, many factors can influence the
adoption approach and the pace of the adoption effort. These are
summarized below:

It is important to consider each of these factors to determine if it
applies to your adoption, what impact it might have, and the steps you
can take to minimize that impact. For an analysis of these factors and
some practical measures that can be taken to minimize them, see
[Accelerating adoption of software tools &
practices](DeploymentAcceleratingAdoption).

##### Related topics: None [related-topics-none]

##### External links: \* [IBM Software Services for Rational](http://www.ibm.com/software/rational/services/) [external-links-ibm-software-services-for-rational]

-   [The rise of the Development Environment
    Architect](http://www.ibm.com/developerworks/rational/library/edge/08/apr08/eeles/)

##### Additional contributors: Main.PeterEeles (Development Environment Architecture) [additional-contributors-main.petereeles-development-environment-architecture]

META:FILEATTACHMENT{name="IBMRationalDEA.png"
attachment="IBMRationalDEA.png" attr="h" comment="" date="1367923449"
path="IBMRationalDEA.png" size="39697" user="jduckmanton" version="1"}
META:FILEATTACHMENT{name="WaveBasedDepoymentModel.png"
attachment="WaveBasedDepoymentModel.png" attr="h" comment=""
date="1367923479" path="WaveBasedDepoymentModel.png" size="28517"
user="jduckmanton" version="1"}
META:FILEATTACHMENT{name="AdoptionFactors.png"
attachment="AdoptionFactors.png" attr="h" comment="" date="1367923506"
path="AdoptionFactors.png" size="118621" user="jduckmanton" version="1"}
