META:TOPICINFO{author="sbagot" date="1432664906" format="1.1"
version="1.22"} META:TOPICPARENT{name="PerformanceTroubleshooting"}

# My builds are slow, how can I speed them up? [my-builds-are-slow-how-can-i-speed-them-up]

DKGRAY Author: PerformanceTroubleshootingTeam Build basis: RTC 4.x and
later ENDCOLOR

TOC{title="Page contents"}

This topic addresses the concern of slow running builds and how to
improve the overall performance of builds launched by the Jazz Build
Engine within IBM Rational Team Concert.

## Initial assessment and analysis

Before taking actions to resolve slow running builds, you will need to
determine which part of the build is causing the performance
degradation.

### Understanding build phases

When you create a new build definition, you first choose a build
template, and then you typically choose pre-build and post-build
options. Generally, among the pre-build options you select "Jazz Source
Control" (or similar, depending on the selected build template). This
pre-build option allows you to fetch sources from the Rational Team
Concert repository to a local directory, where these sources will be
built. The build itself could use a variety of tools (ANT, Maven,
Command Line, and others). Post-build activities include publishing
results and automatically delivering components to a stream based on
build results.

To determine which part of the build is slow running, open the Build
Results and look at the Activities section. You will see the start time
and the Activity duration for each Activity. For example, the screenshot
below displays what would be seen if "Jazz Source Control" was selected
as pre-build option:

### Separating the build script in activities

You can split your own build script in Activities, which will help you
with identifying which parts of the build are slow. To do this, see the
ANT Tasks **startBuildActivity** and **completeBuildActivity** in
[Enabling progress
monitoring](http://pic.dhe.ibm.com/infocenter/clmhelp/v4r0/topic/com.ibm.team.build.doc/topics/r_enableprogressmonitor.html).

## Slow pre-build activities causes and solutions

The below topics address some causes and solutions during various phases
of the pre-build acivities.

### Using "incremental" builds instead of "clean" builds for continuous integration

In Eclipse, you can perform Clean or Incremental builds. A **Clean
Build** is where all build outputs are deleted and recreated, while an
**Incremental Build** will only re-build the changed sources. The
Rational Team Concert documentation does not refer to these terms,
because Rational Team Concert does not directly create the build output.
However, in the "Jazz Source Control" tab of the build definition, you
can specify the **Load directory**, and whether this directory should be
deleted before a new build is executed.

If you choose to delete the **Load directory**, or if you delete the
entire Build Workspace, you will perform what you could call a "Clean"
build.

If you are doing **Continuous Integration**, you will see improved
performance by preserving the Build Workspace, and by not deleting the
**Load directory**. This way, only source files that have changed will
be fetched from the repository. This constitutes what you could call an
"Incremental" build (this actually only means that the fetching of the
sources is done incrementally by Rational Team Concert. Whether the
actual build executes incrementally depends entirely on your build
script). At any rate, "Incremental" builds will be faster, but "Clean"
builds are certainly needed in some situations.

|  |
|----|
| **Note**: if you do not delete the Load directory, your build script will be responsible for cleaning up any build output files created by the previous build, that should not be present in the current build (such as any .class files, for which the corresponding .java files were deleted from the repository). |

### Pre-build: caching proxy

To speed up the process of fetching sources from the repository, you can
use a [caching proxy](https://jazz.net/library/article/325), which
ensures that only sources that have changed will be fetched from the
repository. Unchanged sources will be fetched from the caching proxy
itself. This is the recommended solution to adopt between a build site
and the build engines, if they are not co-located. Even if build site
and build engines are close, if you have large builds, a caching proxy
can help to reduce network and database traffic.

|  |
|----|
| **Note**: The article suggests changing the proxy settings in the Rational Team Concert Client for Eclipse IDE. If you would rather not modify each client, you can comply with the Public URI restrictions by redirecting the DNS server to resolve "myclmserver" to the IP address of the caching proxy. Next, edit the file "/etc/hosts" on the CLM server and make sure that "myclmserver" resolves to 127.0.0.1 or the local IP so that it does not go through the proxy to connect to itself. |

## Slow build execution causes and solutions

The topics below address some causes and solutions during the build
execution.

### Build execution: Split builds in smaller parts

Speeding up the actual build execution depends on the build script being
used. Some general suggestions can be found in section 6 of the article
*Continuous Integration Best Practices with Rational Team Concert*
([Keep the Build Fast](https://jazz.net/library/article/474#6)).

### Build execution: Load tools and artifacts only when needed

It is very common to have the build tools load the Eclipse Compiler for
Java (ECJ) in a component and load them during the build, but this is a
time-consuming operation if it is done every time in a "Clean" build. It
is advisable to have these tools in a special separate stream and have a
separate build definition that loads them to a relative location on the
build machine. You would run this build only once for each build engine
and then, only when the build tools versions change. The same
considerations apply to any artifacts that are unlikely to change
frequently.

Identify any components in the build that do not require loading. Modify
the workspace load rules to only load what is necessary for the build.
Also, determine if any large files can be referenced by the Build system
locally rather than adding them into the workspace. Reducing load time
of the workspace should significantly reduce total build time regardless
of the build system and toolkit.

## Slow post-build activities causes and solutions

The topics below address some causes and solutions during various phases
of the post-build activities.

### Post-build: managing the publication of large logs

As an alternative to publishing large logs to the repository, you can
post links to artifacts on an HTTP server (see [Build Artifacts
Publishing Using HTTP Servers](https://jazz.net/library/article/797)).
Using the recommendations in this article implies that you run a "Clean"
build every time since the output directory changes for each build in
order to preserve the build output.

##### Related topics: [related-topics]

-   Still need help troubleshooting your performance issue? Refer to
    [Performance troubleshooting](PerformanceTroubleshooting) for
    additional topics.

##### External links: [external-links]

-   Tutorial: Building with Jazz Team Build:
    <http://www.ibm.com/support/knowledgecenter/SSCP65_5.0.0/com.ibm.team.concert.tutorial.doc/topics/tut_rtc_build.html>
-   Enabling progress monitoring:
    <http://www.ibm.com/support/knowledgecenter/SSCP65_5.0.0/com.ibm.team.build.doc/topics/r_enableprogressmonitor.html>
-   Using content caching proxies for Jazz Source Control:
    <https://jazz.net/library/article/325>
-   Continuous integration using Rational Team Concert:
    <https://jazz.net/library/presentation/750>
-   Continuous Integration Best Practices with Rational Team Concert:
    <https://jazz.net/library/article/474>
-   Build Artifacts Publishing Using HTTP Servers:
    <https://jazz.net/library/article/797>
-   Automated Build Output Management Using the Plain Java Client
    Libraries: <https://jazz.net/library/article/807>
-   Rational Build Forge Performance test results: Evaluating the
    improved performance in 7.1.2 relative to 7.1.1.4:
    <https://jazz.net/library/article/585>

##### Additional contributors: None [additional-contributors-none]

META:FILEATTACHMENT{name="BuildActivities.jpg"
attachment="BuildActivities.jpg" attr="h" comment="" date="1362061858"
path="BuildActivities.jpg" size="30717" user="lziosi" version="1"}
META:FILEATTACHMENT{name="BuildIncremental.jpg"
attachment="BuildIncremental.jpg" attr="h" comment="" date="1362001542"
path="BuildIncremental.jpg" size="122437" user="lziosi" version="1"}
