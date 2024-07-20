META:TOPICINFO{author="sbeard" date="1433875989" format="1.1"
reprev="1.13" version="1.13"}
META:TOPICPARENT{name="ApproachesToImplementingHAAndDR"}

# Implementing Jazz application HA using VMware HA DKGRAY Authors: Main.StevenBeard, Main.GrantCovell Build basis: Jazz products in CLM and SSE ENDCOLOR [implementing-jazz-application-ha-using-vmware-ha-dkgray-authors-main.stevenbeard-main.grantcovell-build-basis-jazz-products-in-clm-and-sse-endcolor]

TOC{title="Page contents"}

High availability (HA) at the application tier for the CLM and SSE
products can be achieved leveraging VMware technology and tools. VMware
technology and tools permit hosting and managing server assets in
private and cloud deployments that are deployed on x86 hardware
architecture.

## Assumptions

-   CLM and SSE topology uses a reverse proxy or other front-end
    hardware or software load balancer (links)
-   Topology has each CLM and SSE app on separate servers with distinct
    names (links)
-   Hardware and operating system are x86 compatible

## Approach

At a high level, these are the steps most of our VMware customers
follow:

-   Have ready a standby client virtual machine
    -   This may be achieved through cloning the virtual machine from
        within the VMware tools
-   Monitor the active VM and set triggers / alerts in case of failure
    -   This may be achieved through monitoring in the VMware toolset,
        or using other monitoring tools
-   Provision (activate) the standby VM
    -   This may be achieved automatically with the VMware toolset or
        manually (using scripts or actual human intervention)
-   Configure traffic to new VM
    -   This may be achieved automatically with the VMware toolset or
        manually (using scripts or actual human intervention)

## Implementation suggestions

-   **VMware vSphere ESXi** can manage virtual machines on a single
    hypervisor. In this context, a standby VM needs to be readied. This
    can be done through cloning the VM so that a separate server is
    ready but not active. There may be manual steps to activate the
    prepared VM and to ensure the front-ending load balancer routes
    traffic to the new VM.
-   **VMware vSphere vMotion** technology permits creating a cluster or
    group of multiple hypervisors whose resources are managed as a pool.
    Virtual machines may move transparently from one hypervisor to
    another without apparent end-user involvement or awareness. This
    technology compensates for variability in a hypervisor cluster due
    to changes in virtual machine load or unexpected hardware issues at
    the hypervisor level.
-   **VMware High Availability** (HA) technology automatically restarts
    the virtual machines elsewhere in the hypervisor cluster.

\#JazzApplicationRecovery

## Jazz application recovery

The Jazz applications can be monitored through external tools which
check uptime of the actual application or the virtual machine hosting
the jazz application.

Scripts can be written and can be run from a system outside of the
virtual machine hosting the jazz application.

\#WasRecovery

## WAS recovery

WAS can be monitored through external tools to check queues and threads.
Scripts can be written and can be run from a system external to the
virtual machine running WAS to determine health.

\#SingleVirtualServerRecovery

## Single virtual server recovery

VMware vSphere console can monitor the virtual machine to determine
health and alert or respond proactively.

## Other considerations

If there are additional specific failure scenario, please add a new
scenario to the parent page and new section within this page

##### Related topics: [Approaches to implementing high availability and disaster recovery for Rational Jazz environments](ApproachesToImplementingHAAndDR) [related-topics-approaches-to-implementing-high-availability-and-disaster-recovery-for-rational-jazz-environments]

##### External links: [external-links]

-   [VMware](http://www.vmware.com/)
-   [VMware vSphere
    ESXi](http://www.vmware.com/products/vsphere/features/esxi-hypervisor.html)
-   [VMware vSphere
    vMotion](http://www.vmware.com/products/vsphere/features/vmotion.html)
-   [VMware vCenter Site Recover
    Manager](http://www.vmware.com/products/site-recovery-manager/)

##### Additional contributors: None [additional-contributors-none]

META:TOPICMOVED{by="sbeard" date="1396110529"
from="Deployment.ImplementingApplicationHABasedUponVMwareHA"
to="Deployment.ImplementingApplicationHAUsingVMwareHA"}
