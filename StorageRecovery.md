META:TOPICINFO{author="gcovell" date="1397684371" format="1.1"
version="1.2"} META:TOPICPARENT{name="ApproachesToImplementingHAAndDR"}

# Storage recovery [storage-recovery]

DKGRAY Authors: Main.StevenBeard Build basis: None ENDCOLOR

TOC{title="Page contents"}

### Minimize unplanned outages: Use storage area network (SAN) or Network Attached Storage (NAS) technology

The Jazz solution configuration should use SAN or NAS technologies if
possible, because these technologies provide a degree of fault tolerance
for disk storage resources. The Jazz repositories should reside on these
resources. If virtualization is being utilized for the Jazz servers,
then the virtual machine (VM) images should also be stored on this
media.

In addition, NAS solutions offer utilities for doing offline backups, by
breaking the disk mirror and then backing up the offline copy of the
disk storage. These systems will also provide the capability to store
these backups for quick restoration, as well as utilities to manipulate
these backups. Well-prepared Jazz installations will also make sure that
these backups are moved offsite at some interval; to mitigate the risks
of data loss should the data from an entire site be destroyed.

**Important:** The enterprise Jazz infrastructure is expected to support
the software development needs of an organization, and the consequences
of losing these software assets are quite severe. Use of SAN and NAS
technologies can help mitigate this risk, and will allow for backup of
the Jazz based artifacts with a minimum amount of down time. While NAS
may impact performance, when compared to a SAN implementation, it
provides hot swapping and is more reliable.

### Cross-volume data integrity and consistency groups

**Note:** This section is derived from the IBM Systems Magazine article,
[Disaster Recovery
levels](http://www.ibmsystemsmag.com/mainframe/administrator/backuprecovery/Disaster-Recovery-Levels/),
by Robert Kern and Victor Peltz (November 2003).

Computers must write data to disks with full integrity, even in the
event of hardware failures and power failures. To accomplish this,
environment designers employ many techniques, such as:

-   Mirrored storage subsystem cache to prevent data loss in the event
    of a cache hardware failure
-   Battery backup to prevent cache data loss in the event of a power
    failure
-   Mirrored disk or parity-based RAID schemes for protecting against
    hard-disk drive failures

Another, more subtle, requirement for preserving the integrity of data
being written is making sure that "dependent writes" are executed in the
applications intended sequence. Many years ago, application developers
developed various dependent write sequences to preserve data
integrity/data consistency for data being written to disk across power
failures. Consider this typical sequence of writes for a database update
transaction:

1 Execute a write to update the database log, indicating that a database
update is about to take place. 1 Execute a second write to update the
database. 1 Execute a third write to update the database log, indicating
that the database update has completed successfully.

These "dependent writes" must be written to remote mirrored disk in the
same sequence in which the application issued them. In the previous
example, there are no guarantees that the database log and the database
are on the same storage subsystem. Failure to execute the write sequence
correctly may result in writes (1) and (3) being executed, followed
immediately by a system failure. When it is time to recover the
database, the database log would incorrectly indicate that the
transaction completed successfully. The transaction would be lost, and
the integrity of the database would be questionable.

When considering the RTOs and RPOs in any disaster-recovery solution
involving data replication, it is critical to understand the need for
cross-volume data integrity and data consistency. Essential elements for
creating cross-volume data integrity and data consistency include the
ability to:

-   Create RPiT copies of the data as necessary
-   Provide a site "Data Freeze" causing all data at the remote site to
    be consistent with a RPiT
-   Use a consistent timestamps across all write updates to order all
    writes at the remote site
-   Create data set/file consistency groups

Cross-volume data integrity and data consistency enable database
RESTARTs if the second copy of the data is actually used. Solutions that
employ cross-volume mirroring and remote-disk mirroring must address the
issue of data consistency to support cross-volume and cross-storage
subsystem data integrity.

Most customers, when designing a multi-site solution, must minimize the
time it takes to restart applications once the data at the secondary
site has been recovered.

### Tiers of multi-site service availability

In the late 1980s, the
[SHARE](http://en.wikipedia.org/wiki/SHARE_28computing29) Technical
Steering Committee, working with IBM, developed a white paper that
described levels of service for disaster recovery using Tiers 0 through
6. Since then, a number of businesses using IBM zSeries have moved
toward an IBM TotalStorage solution called the Geographically Dispersed
Parallel Sysplex, which allows an installation to manage end-to-end
application and data availability across multiple geographically
separate sites. This resulted in an additional seventh tier representing
the industry's highest level of availability driven by technology
improvements.

-   **Tier 0: No disaster recovery** - Most customers today understand
    the need for disaster recovery of their development environments, as
    well as the need for backup of critical data. However, Tier 0 is
    still common in practice because to many organizations do not fully
    test their disaster recovery properly, resulting it it failing in
    the event of a disaster. Also the design and implementation of
    disaster recovery is often differed to later resuting in a poor or
    never implemented solution.

<!-- -->

-   **Tiers 1 and 2: Physical transport** - The majority of today's
    customers use a traditional method of creating tapes nightly and
    transporting them to a remote site overnight. Tier 1 users send the
    tapes to a warehouse or "cold" site for storage. Tier 2 users send
    the tapes to a "hot" site where the tapes can be quickly restored in
    the event of a disaster. Various schemes have been developed to
    improve the process of offloading data nightly from production sites
    and production volumes to tapes. Some of these solutions provide
    full integration with various databases (Oracle, DB2 SQL, etc.).
    Here are some of the names created to describe these off-line backup
    solutions:
    -   Server-less backup
    -   LAN-less backup
    -   Split mirroring
    -   SNAP/SHOT\* Hardware vendors have created products to fit into
        this marketplace. For example, the IBM Enterprise Storage Server
        (ESS) FlashCopy function provides this capability and, when
        coupled with ESS disk mirroring solutions, can create a RPiT
        copy of data within the same ESS logical storage subsystem
        without impacting applications.

<!-- -->

-   **Tier 3: Electronic vault transport** - This is usually achieved by
    copying the tape from the primary site directly into a tape storage
    subsystem located at the remote secondary site. This replaces the
    need to physically transport tapes, with the tradeoff of the added
    network bandwidth.

<!-- -->

-   **Tier 4: Two active sites with application software mirroring** -
    Various database, file system or application-based replication
    techniques also have been developed to replicate current data to a
    second site, but these techniques are limited to data contained in
    the particular database or file system for which they were designed.
    An example of this in the open systems world is software mirroring
    at the file-system level. If all of your data resides within the
    file system, these techniques can be a fast and efficient method of
    replicating data locally or remotely. Software-based file system
    mirroring can also be fully integrated with various host-base server
    clustering schemes like AIX High Availability Geographic Cluster
    (HAGEO). Host failover causes the software mirroring to failover as
    well.

<!-- -->

-   **Tier 5: Two-site, two-phase commit** - This technique is specific
    to the database and its configuration used in conjunction with the
    application environment. Various databases provide specific data
    replication of database logs, coupled with programs to apply the log
    changes at the secondary site. Typically, one only gets data
    consistency within the specific database, and transactions across
    multiple databases are not supported.

<!-- -->

-   **Tier 6: Disk and tape storage subsystem mirroring** - This
    technique includes two types of mirroring:
    -   Disk mirroring - Disk mirroring is popular because it can be
        implemented in the storage subsystem and, as a result, is
        independent of the host applications, databases and file systems
        that utilize the storage subsystem.
    -   Tape mirroring - You can mirror tape data via various hardware
        and software solutions. Typically this data is non-critical but
        still needs to be recovered in the event of a disaster that
        prevents moving back to the primary site for an extended period
        of time.

<!-- -->

-   **Tier 7: IBM GDPS** - Use GDPS to implement the highest level in
    the multi-site availability hierarchy. GDPS can enable an
    installation to provide the means to support the highest level of
    application availability. GDPS combines software and hardware as the
    means for managing a complete switch of all resources from one site
    to another automatically, providing continuous operations as well as
    disaster recovery support for both planned and unplanned outages.

##### Related topics: [Approaches to implementing high availability and disaster recovery for Rational Jazz environments](ApproachesToImplementingHAAndDR) [related-topics-approaches-to-implementing-high-availability-and-disaster-recovery-for-rational-jazz-environments]

##### External links: [external-links]

-   [Disaster Recovery
    levels](http://www.ibmsystemsmag.com/mainframe/administrator/backuprecovery/Disaster-Recovery-Levels/),
    by Robert Kern and Victor Peltz (November 2003).

##### Additional contributors: None [additional-contributors-none]
