META:TOPICINFO{author="gcovell" date="1395078077" format="1.1"
reprev="1.20" version="1.20"}
META:TOPICPARENT{name="DeploymentPlanningAndDesign"}

# Principles of good virtualization [principles-of-good-virtualization]

DKGRAY Authors: Main.GrantCovell, Main.HarryIAbadi ENDCOLOR

TOC{title="Page contents"}

IBM supports
[virtualization](http://www.ibm.com/software/support/virtualization_policy.html)
and consequently, IBM Rational products are supported on virtualized
servers. In a properly managed VM, Rational software products can
perform properly. However, the virtualized infrastructure must be
properly managed and monitored. It is crucial to understand how your
virtualized infrastructure uses **affinity** and **overcommitment**, and
to be sure you are using affinity and overcommitment in a way that
ensures the best performance of your IBM Rational products.

## Affinity

**Affinity** (also called entitlement, pinning, and dedication) is the
ability to dedicate one or more resources on a virtual machine (for
example: memory, processor, etc.) to the corresponding resources on the
hypervisor. The host parcels out resources as the virtual machines need
them. Affinity ensures that the wanted resources are dedicated to that
virtual machine and are always available when the virtual machine
requires them. Remember that virtual machines share system resources
with all the other virtual machines on the same host.

## Overcommitment

**Overcommitment** is when the total amount of virtual image resource
allocation exceeds the physical resources of the hardware. In many
common configurations to satisfy a virtual machines peak needs, the
hypervisor may take resources from other virtual machines. Sometimes the
combined needs of all the virtual machines may exceed the actual
resources of the hypervisor. (When calculating the combined resources
used, be sure to count the hypervisor resources as well). Sometimes
over-commitment can cause all the virtual machines on a host to suffer.

## Virtualization advantages

-   Well-managed virtualized servers permit modifying CPU, RAM, and disc
    image sizes with much greater ease than physical servers.
-   A virtualized infrastructure can offer several capabilities of
    high-availability, such as the ability for the VM infrastructure to
    mirror standby servers in case of failure.

## Virtualization strategies

-   Virtualization must be managed and monitored.

<!-- -->

-   Ensure that CPU, memory, and network resources are dedicated and
    uncapped. Ensure that CPU, memory, and network resources have
    minimum allocations or reservations.

<!-- -->

-   For each hypervisor (VM host), the number of virtual CPUs should
    never exceed the number of physical CPUs. Be aware of the trick
    played by some hypervisors, which may count multi-threaded
    processors as separate processors (a dual-threaded 16-processor
    server may appear to the hypervisor as a 32-processor server and
    allocating 2 of these processors actually allocates half of a real
    processor).

<!-- -->

-   The CPU allocation for each VM corresponds to actual physical CPUs.

<!-- -->

-   There is ample access (bandwidth, network cards) to network and
    storage.

<!-- -->

-   If the server that is hosting your VMs (hypervisor or host) is not
    fully dedicated to your VMs, be aware of the usage and load of those
    other VMs.

##### Related topics: [related-topics]

-   [Troubleshooting problems in virtualized
    environments](VirtualizationTroubleshooting)

##### External links: \* IBM developerWorks article: [Be smart with virtualization: Part 1](http://www.ibm.com/developerworks/rational/library/smart-virtualization-1/) and [Be smart with virtualization: Part 2.](http://www.ibm.com/developerworks/rational/library/smart-virtualization-2/) [external-links-ibm-developerworks-article-be-smart-with-virtualization-part-1-and-be-smart-with-virtualization-part-2.]

-   VMware Knowledge Base: [Virtual machine memory limits and hardware
    versions](http://kb.vmware.com/kb/1014006)

##### Additional contributors: Main.MikeDonati, Main.RyanSmith [additional-contributors-main.mikedonati-main.ryansmith]
