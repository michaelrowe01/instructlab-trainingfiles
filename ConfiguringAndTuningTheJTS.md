META:TOPICINFO{author="sbeard" date="1422035664" format="1.1"
version="1.12"} META:TOPICPARENT{name="DeploymentAdminstering"}

# Configuring and Tuning the Jazz Team Server (JTS) [configuring-and-tuning-the-jazz-team-server-jts]

DKGRAY Authors: [DanToczala](Main.DavidToczala) Build basis: CLM 2011
(product versions 3.x) and later ENDCOLOR

TOC{title="Page contents"}

Configuring JTS should be simple and straightforward for most initial
implementations. There should not be too many things to consider during
the initial configuration of JTS. After the server is deployed,
sometimes performance issues dictate that you consider [configuring and
tuning the Java Virtual Machine
(JVM)](https://jazz.net/wiki/bin/view/Deployment/ConfiguringAndTuningTheJVM)
for JTS.

## General concerns

When you consider how to configure JTS, it is critical to know the Jazz
applications that the server will support, and the expected user load on
the solution. Keep in mind that any single Jazz solution will contain a
single JTS. Some organizations deploy multiple JTS instances into their
enterprise solution, but, as an administrator, it is best for you to
consider each of these instances as a single stand-alone instance of a
Jazz solution. Each single JTS can support multiple CCM (RTC) instances,
multiple QM (Rational Quality Manager) instances, a single RM (Rational
Requirements Composer) instance, and a single data warehouse instance
(Rational Reporting for Development Intelligence or Rational Insight).

### Configuring the JVM settings

One of the most important things that you configure are the JVM settings
that are used when you deploy the JTS. These settings often have a large
impact on the performance of your JTS application, and you should have
these tracked somewhere as part of your solution architecture
description. Often, it is best to start with the [default JVM
settings](https://jazz.net/wiki/bin/view/Deployment/ConfiguringAndTuningTheJVM)
suggested by the development team.

##### Related topics: [Configuring and tuning the JVM](https://jazz.net/wiki/bin/view/Deployment/ConfiguringAndTuningTheJVM) [related-topics-configuring-and-tuning-the-jvm]

##### External links: \* None [external-links-none]

##### Additional contributors: None [additional-contributors-none]

META:TOPICMOVED{by="sbeard" date="1385847657"
from="Deployment.ConfigureJTS"
to="Deployment.ConfiguringAndTuningTheJTS"}
