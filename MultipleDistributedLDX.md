META:TOPICINFO{author="rrakich" date="1706220411" format="1.1"
reprev="1.7" version="1.7"}
META:TOPICPARENT{name="StandardTopologyPatternsOverview"}

# Multiple Distributed LDX instances in a Modified Federated Topology Configuration DKGRAY Authors: Main.RichRakich [multiple-distributed-ldx-instances-in-a-modified-federated-topology-configuration-dkgray-authors-main.richrakich]

Build basis: ELM 7.0.2 and higher ENDCOLOR

TOC{title="Page contents"}

In some highly active environments, a single LDX server in the [modified
federated
topology](StandardTopologiesOverview#Modified_federated_topologies) may
not be sufficient. To alleviate this, one or more LDX servers can be
deployed to manage versioned links for individual business units to
isolate load on LDX for that business unit.

With multiple LDXs, it is typical to configure each to index the same
set of data providers as the original single LDX topology

-   Each instance can be made to handle the traffic of any other LDX
    server should that particular LDX server be down or undergo
    maintenance (e.g. Backup, compaction, validation)
-   Each instances backup can be restored on other LDX servers as the
    data they index and their context root is the same

If a business unit has a narrow focus for which links to other artifacts
are strictly constrained, an alternative configuration would be to index
the needed subset of data providers to fulfill queries. This can reduce
the resources required for the system. **Caution:** if a user creates a
link to an artifact outside the constraint, the link will not be seen by
other users and eventually will not be seen by the user creating the
link (temporary cache expires), the tool where the link is stored should
be added to the particular LDX server so that those links can be indexed
and shown to the end user in the expanded scope.

## Multiple Distributed LDX Servers in Modified Federated Topology

This document will provide the steps to configure a Modified Federated
Topology to include additional LDX servers which are scoped for a
particular business unit.

### Deploy additional LDX server

-   The additional LDX server should be deployed on its own server
-   Install LDX server per the
    [documentation](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/lifecycle-management/7.0.2?topic=management-interactive-installation-guide)
    -   If Jazz Authorization Server is configured in the environment,
        make sure to check the box in the install to enable Jazz SSO
        during install.

### Configure an additional LDX server for the business unit:

Configure the LDX Server in one of the following ways:

1.  The configuration files can be cloned from an existing LDX server.
    -   A restore using the backup of an existing LDX server can be used
        to make a clone.
2.  If an LDX instance will be used only for a single narrowly scoped
    business unit, a custom configuration is required.
    -   Configure LDX with the necessary subset of data providers.

Once the LDX Server is configured, you need to update other applications
to utilize it:

-   In both configurations, the application servers will need to point
    to an LDX server:
    -   Configure RM and QM application advanced properties to point to
        an LDX server.
        -   Change the value in the server **Advanced
            Properties-\>com.ibm.team.links.service.internal.LinkIndexService-\>Link
            index provider URL** as needed

### Validation and testing the configuration

Expectations:

-   Once configured the updated RM applications will only make link
    lookup requests to the LDX server configured in Advanced Properties.
-   For Configuration B (above) with only a subset of the data
    providers, it will only have link data for the RM, QM, and CCM
    applications that have links to or from the business unit RM
    application.
    -   A link to or from the RM application to another application
        server that is not indexed by the business unit LDX server will
        not be shown in an RM artifact.
    -   Links to or from the RM application from the application servers
        that are data providers in the business unit LDX server will be
        shown in RM artifacts.
    -   If all data providers are present in all LDX servers, the
        previous points will not apply.

Testing:

-   Open RM artifacts and verify all links are present.
-   Create new links between QM and RM to verify they are visible to
    other users after LDX index update.
    -   Link creator validates that new links are still visible after
        5-10 minutes (cache timeout)

##### Related topics: [StandardTopologyPatternsOverview](StandardTopologyPatternsOverview), [DeploymentPlanningAndDesign](DeploymentPlanningAndDesign) [related-topics-standardtopologypatternsoverview-deploymentplanninganddesign]
