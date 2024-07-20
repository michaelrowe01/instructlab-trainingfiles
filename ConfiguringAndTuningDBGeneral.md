META:TOPICINFO{author="sbeard" date="1422035663" format="1.1"
version="1.11"} META:TOPICPARENT{name="DeploymentAdminstering"}

# Configuring and tuning databases [configuring-and-tuning-databases]

DKGRAY Authors: [DanToczala](Main.DavidToczala) Build basis: CLM2012,
CLM 2011 ENDCOLOR

TOC{title="Page contents"}

## General guidance

The database server is the portion of most Jazz solutions that is often
out of the control of most solution architects and Jazz administrators.
Often, the choice of database vendor is a corporate directive and you
are told the database technology that you will use. If you decide to
support your own database, you can choose the database technology that
you want. Keep in mind that Jazz licenses also carry an entitlement for
the use of DB2 Workgroup edition as part of the Jazz licensing
agreement.

There are some general things that you can do to help improve the
performance of your Jazz solution. These suggestions are valid for all
the database technologies that support Jazz:

-   Make sure that your database has sufficient physical memory and
    enough allocated memory to perform a lot of data transfers. All of
    the REST-based objects will need to be stored and retrieved here,
    and the rest of the solution architecture depends on the repository.
    Do not try to cut costs: make sure that the foundation for your
    solution is solid.
-   Your database should be on a dedicated server. While it is
    technically possible to install the database software onto the same
    machine as other software, the load on the database is heavy
    (because almost every user action implies multiple database events,
    like queries, inserts, or modifications). Deploy the database on a
    dedicated database server.
-   The storage device for the database is also important. The database
    storage should be fast storage. The server should have many fast
    disks combined in a RAID configuration for optimal performance and
    reliability. See the [Jazz.net](https://jazz.net/) article about
    [Tuning the Rational Team Concert 3.0
    Server](https://jazz.net/library/article/557) for further details.
-   Monitor the performance of your database. Do not go overboard with
    monitoring, because excessive monitoring can lead to performance
    degradation of the database software. Monitor the amount of data
    (inbound and outbound), the number of queries over time, and some
    measure of the amount of time from the receipt of an SQL request to
    the time a response is generated.

##### Related topics: None [related-topics-none]

##### External links: \* None [external-links-none]

##### Additional contributors: None [additional-contributors-none]

##### Questions and comments: [questions-and-comments]

COMMENT{type="below" target="ConfiguringAndTuningDBGeneralComments"
button="Submit"}

INCLUDE{"ConfiguringAndTuningDBGeneralComments"}

META:TOPICMOVED{by="sbeard" date="1385832793"
from="Deployment.TuningDBGeneral"
to="Deployment.ConfiguringAndTuningDBGeneral"}
