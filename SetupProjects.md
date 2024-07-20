META:TOPICINFO{author="rschoon" date="1469092339" format="1.1"
version="1.10"} META:TOPICPARENT{name="DeploymentAdminstering"}

# Setting up projects for your CLM applications DKGRAY Authors: [Ralph Schoon](Main.RalphSchoon) Build basis: None. [setting-up-projects-for-your-clm-applications-dkgray-authors-ralph-schoon-build-basis-none.]

ENDCOLOR

TOC{title="Page contents"}

What needs to be considered and done, after the servers are up and
running? What are the next steps to start a new project with the
Rational Collaboration For Lifecycle Management solution? This section
will help with information about creating and maintaining projects in
the different applications. [This is the main entry point in the online
help](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.platform.doc/topics/c_getting_started_project_areas_and_lifecycle_projects.html)

## Project areas

All the the CLM applications organize the work in project areas.To work
with any of the CLM applications, you need to create a project area in
the specific application. Project areas can also be used to limit read
access e.g. to the members of the project area hierarchy.

### Team areas

In some of the CLM applications, you can use team areas within a project
area, to structure and organize work. Different CLM applications have a
slightly different approach to using team areas. Rational team concert
relies heavily on it. Other products often use other categories to
organize and structure work.

-   RTC - ToDo
-   RQM - [Managing teams using the Team Area in Rational Quality
    Manager](https://jazz.net/library/article/1239)

### Project areas vs. team areas

When should you use project areas and when should you use team areas to
organize the work? Read more about considerations for creating project
and team areas \[New Page - project areas vs team areas in different
applications\].

### Process templates for project areas

Each project area defines its own process. Project areas are initially
created using process templates which are provided by the applications.
Read more about the various process templates and their properties \[New
Page - process templates in different applications\].

### The project area process

All team areas within a project area share the same process. Team areas
within a project area can add new roles, set their permissions and tune
the operational behavior, but the general process and its artifacts is
shared across the whole hierarchy. To effectively use the CLM
application it is necessary to understand the fundamental concepts each
application uses in their process. See the following pages for more
details on these concepts.

\* [Rational Team Concert Process Fundamentals](RTCProcessFundamentals)
\* Rational Quality Manager Process Fundamentals - coming soon \*
Rational Doors Next Process Fundamentals - coming soon

Once a project area is created it is necessary to maintain the process
in the project area. In many organizations some members of the project
area are also administrators of their own project area. This gives the
members of the project area a lot of flexibility and independence and
sometimes the edge that is needed to be successful.

Once a project area is created from a process template, there is no more
connection between the two. Modifying the process template does not
modify the project areas process and vice versa. You can, and should,
create a custom process template from a project areas process and use it
for new project areas. This allows to slightly customize the standard
process and get to a template that has your customization already
included.

Since there is no connection between process templates and the project
areas process, it is necessary to maintain the process in each project
area independently. If there are a lot of project areas, it increases
the administrative effort. It is also sometimes desirable to have a
common process for all project areas. Some organizations use process
sharing to standardize on process across multiple project areas and
reduce the administrative overhead that way as well.

### Process sharing

Process sharing allows to provide a standardized process and share it
with multiple project areas. The project areas that want to share the
process of another project area are created from the ["Unconfigured
Process
template"](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.platform.doc/topics/r_unconfigured_process_template.html).
They are then set to share the process of another project area.

The project area that provides its process for sharing is created using
any other process template. This project area is then configured to
provide its process for sharing which also makes this project area
accessible by everyone. The process configuration is then provided to
any project area that shares this process. Also see [Managing Rational
Team Concert work item changes with process
sharing](https://jazz.net/library/article/1077) for more best practices.

[Process sharing works across
servers](https://jazz.net/library/article/1008), so it is possible to
have a CCM server just for this purpose or use it in highly distributed
environments that have multiple CCM applications deployed.

Process sharing works best for Rational Team Concert. It can however
also be used for other CLM applications. Other CLM applications just
don't necessarily store all information in the process template and have
different means to customize their process, but they all share a core
that allows process sharing.

## Lifecycle projects

Although it is possible to just work with one application, for example
Rational Team Concert, the Rational CLM solution provides the biggest
benefits if being used across the whole lifecycle and all the roles
involved. This usually requires different roles to work in different
project areas provided in multiple applications. As an example the
requirements engineers would work in a Rational Doors Next project area
most of the time. The development team would work in Rational Team
Concert and the quality team would work in Rational Quality Manager.
None of these roles work in isolation and referring to artifacts in
other domains is a requirement.

The CLM solution provides [Lifecycle
Projects](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.platform.doc/topics/c_getting_started_project_areas_and_lifecycle_projects.html)
in the Lifecycle Project Administration application (LPA) to support
managing this. The LPA application allows to Create lifecycle projects
that configure projects in multiple applications and tie them together.
It is possible to create lifecycle projects and automatically create the
related projects in the various applications. It is also possible to add
existing project areas in multiple applications to a lifecycle project.

If your deployment topology includes multiple [Jazz Team Server or Jazz
application instances](PlanForMultipleJazzAppInstances) keep in mind
that the LPA application is currently (version 6.x) only available for
project areas in applications that are registered to the same JTS. If
multiple instances of the same CLM application are registered to the
same JTS, the LPA application only supports creating project areas in
the first registered application of one kind. It is however possible to
manually create a project area on any instance and add it to the
lifecycle project.

### Lifecycle project templates

Similar to the applications, the LPA application comes with some
predefined process templates. It is possible to use the existing
templates. It is also possible to [manage and customize the process
template for your lifecycle
project](https://jazz.net/library/article/1427). It is possible to
export a template by selecting it in the template management section and
clicking the export button. Once downloaded it is just an XML file. It
is possible to modify the XML to adjust it and later import the modified
template. This is for instance of interest if you want to use process
sharing and want to use the ["Unconfigured Process
template"](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.platform.doc/topics/r_unconfigured_process_template.html)
in the applications.

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome), [RTC Process Fundamentals](RTCProcessFundamentals) [related-topics-deployment-web-home-deployment-web-home-rtc-process-fundamentals]

##### External links: [external-links]

-   [Process
    templates](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.platform.doc/topics/c_process_template.html)
-   [Working with process
    templates](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.platform.doc/topics/t_work_process_templates.html)
-   [Exporting and importing process
    templates](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.platform.doc/topics/t_export_import_process_templates.html)
-   [Migrating a project to a different process
    template](https://jazz.net/help-dev/clm/topic/com.ibm.jazz.platform.doc/topics/t_migrate_dif_process.html)
-   [Changing your Rational Team Concert Process Configuration - Best
    Practices](https://jazz.net/library/article/1002)
-   [Work Item Configuration and Shared Process in Rational Team
    Concert](https://jazz.net/library/article/1005)
-   [Process Enactment Workshop for the Rational solution for
    Collaborative Lifecycle Management
    2012](https://jazz.net/library/article/1093)
-   [Work Item and Foundation Articles, Wikis, and Tech Notes
    ](https://jazz.net/wiki/bin/view/Main/WorkItemArticlesAndTechNotes)
-   [Work Item Customization in Rational Team
    Concert](https://jazz.net/library/article/565)
-   [Customizing Attributes in Rational Team
    Concert](https://jazz.net/library/article/537)
-   [Customizing the Agile Planning tools in Rational Team
    Concert](https://jazz.net/library/article/587)
-   [Customizing a process template for formal project
    management](https://jazz.net/library/article/572)
-   [How to manage and customize the process template for your lifecycle
    project](https://jazz.net/library/article/1427)
-   [Cross Server Process
    Sharing](https://jazz.net/library/article/1008)
-   [Managing Rational Team Concert work item changes with process
    sharing](https://jazz.net/library/article/1077)

##### Additional contributors: [additional-contributors]
