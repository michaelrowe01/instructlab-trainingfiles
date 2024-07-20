META:TOPICINFO{author="sbeard" date="1422040054" format="1.1"
version="1.11"} META:TOPICPARENT{name="DeploymentAdminstering"}

# Top tuning tips [top-tuning-tips]

DKGRAY Authors: Main.DanToczala, Main.GrantCovell, Main.BriannaSmith
Build basis: CLM 2012 ENDCOLOR

TOC{title="Page contents"}

The relevant sections of the [administering
section](DeploymentAdminstering) include these tips, as well as more
information about why these tips work and what you should consider
before you apply any of these tuning changes.

## Top tuning tips

### Get the WAS JVM right

Make sure that your JVM has the correct settings for the computer that
your Jazz application is deployed on. This is one of the most frequent
causes of issues in Jazz deployments. There are a series of options, and
you need to set each appropriately.

-   **-Xmx4G** - This is the maximum JVM heap setting. It should be no
    more than half of the available memory on the computer that hosts
    the Jazz application. In this example, it is set to 4 GB, which
    assumes that you have 8 GB of memory on the computer that hosts this
    Jazz application instance.
-   **-Xms4G** - This is the minimum JVM heap setting. It should be set
    to the same value as the maximum JVM heap setting.
-   **-Xmn512M** - This is the heap "nursery" setting, and this should
    be set to 1/8 of what your settings for the maximum and minimum JVM
    heap are. In some situations (usually validated by close examination
    of JVM garbage collection logs), this value may be increased to 1/4
    the max and min JVM heap settings.
-   **-Xgcpolicy:gencon** - This is the garbage collection policy that
    the JVM uses. Use "gencon", and don't make changes unless you have
    read about and fully understand [JVM garbage
    collection](http://www.ibm.com/developerworks/java/library/j-ibmjava2/)
    and how it impacts the performance of the Jazz applications.
-   **-Xcompressedrefs** - This indicates use of compressed references
    in the JVM. Use this setting unless explicitly told otherwise.
-   **-Xgc:preferredHeapBase=0x100000000** - This is the preferred base
    address of the heap. Use this setting unless explicitly told
    otherwise.

### Ulimit, baby!

If you're using Linux, be sure to increase the the limit of open files
and user processes:

-   As a root user add the following lines to the
    `/etc/security/limits.conf` file:

\* hard nofile 65536 \* soft nofile 65536 \* hard nproc 10000 \* soft
nproc 10000

-   Restart the Linux system after the `limits.conf` file is modified.
-   An individual user can increase the limits within a running shell
    with the following commands:

ulimit -n 65536 ulimit -u 10000

### Validate the NIC settings

Double-check that your network cards and interfaces are set to
full-duplex.

##### Related topics: [Deployment web home](DeploymentWebHome), [administering section](DeploymentAdminstering) [related-topics-deployment-web-home-administering-section]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)
-   [JVM garbage
    collection](http://www.ibm.com/developerworks/java/library/j-ibmjava2/)

##### Additional contributors: None [additional-contributors-none]
