META:TOPICINFO{author="rwatts" date="1539200099" format="1.1"
version="1.5"}
META:TOPICPARENT{name="DeploymentInstallingUpgradingAndMigrating"}

# Upgrading a cluster of Change and Configuration Management applications [upgrading-a-cluster-of-change-and-configuration-management-applications]

DKGRAY Authors: Main.MichaelAfshar, Main.AlexBernstein,
Main.ChrisAustin, Main.PrabhatGupta, Main.YanpingChen, Main.BreunReed
Build basis: Change and Configuration Management 6.0.5 and later
ENDCOLOR

TOC{title="Page contents"}

Upgrading clustered application requires very little custom steps.
Essentially, it boils down to unclustering the application (see below),
performing an upgrade, replicating the settings from the upgraded node
and then re-enabling the cluster.

## Upgrade Steps

-   Stop all Liberty profiles in order (applications first, then JTS and
    Distributed Cache Microservice (DCM) last).
-   Leave the load-balancer (HAProxy) running and unmodified (unless
    changes are specifically needed for the new version).
-   Remove the `com.ibm.team.repository.mqtt.broker.address` line from
    teamserver.properties of any clustered apps (*This is optional, only
    do this if `repotools -addTables` fails to execute*).
-   Upgrade CLM normally (JTS first, microservice and apps last).
    -   Install the new release (using Installation Manager, or
        unzipping the build) on all servers, including all nodes of a
        cluster.
    -   Manually review/update to ensure any Liberty JVM options and
        keystores are preserved.
    -   For clustered applications, run the upgrade script(s) on only
        one node of each cluster (though if you accidentally upgrade on
        both nodes, nothing will break - the second "upgrade" won't
        actually change anything on the database).
-   Re-add the original `com.ibm.team.repository.mqtt.broker.address`
    line to teamserver.properties (*if removed*).
-   On any additional clustered nodes, copy the teamserver.properties
    from the upgraded node.
-   Make sure the new server startup scripts of clustered applications
    have cluster-related entries, such as **unique cluster Node IDs**.
-   Manually review/update `distributedCache.cfg` to preserve any
    customizations as well as new values needed by the new version. Copy
    the keystore.
    -   **Note** in 6.0.6.1, we changed the version of jetty we are
        using for DCM and the following property in the
        `distributedCache.cfg` file changed **from** `allowRenegotiate`
        **to** `renegotiationAllowed`. With the **default value** still
        being **false**
-   Start all profiles in order (DCM and JTS first; verify they are
    working, then start the other apps).
-   Run all diagnostics and test all applications.

### Notes on Distributed Cache Microservice (DCM)

#### Persisted cached data

When persistence is enabled, DCM backs up in-memory distributed caches
to disk. This persisted backup is used to initialize local caches on a
node that is being brought back online after going offline in an
unplanned manner. This allows the node to be initialized to the current
state. If persistence is disabled, the node will initialize itself, as
it would also do after planned shutdown sequence, to default values
which it can calculate or otherwise obtain from the database or other
appropriate mechanisms.

-   Prior to CLM version 6.0.5 there was no Distributed Cache
    Microservice; its functionality was part of JTS. If upgrading from
    6.0.4 simple follow instructions for installing and registering
    fresh DCM from scratch.
-   DCM version **6.0.5** does not, by default, persists cached data on
    disk. Therefore, while upgrading from that version, there is no need
    to clean out distributedData folder, as it will not be there.
-   In DCM version **6.0.6 and later** persistence is enabled. Also, in
    these newer versions DCM monitors the online status of the
    applications' nodes. When a server on a node machine is shut down,
    the signal is sent to DCM. After all nodes of a cluster went offline
    gracefully, the DCM clears out all persisted distributed data for
    that cluster. The cluster specific storage is just a sub-folder
    under the folder specified in the configuration file (the
    `distributedData` by default). The name of that sub-folder is the
    same as the name of the cluster. This is implemented so that when
    applications' nodes are coming up after planned downtime, they
    initialize their distributed data from scratch instead of using
    obsolete and potentially stale persisted copy. The persisted copy is
    used only by the node that is coming up after a crash or another
    unplanned outage and needs the current copy (a snapshot) of the
    distributed data. \* The following property in the DCM configuration
    file is used to specify the location of the persisted data:
    \[Cache\] \# Relative or absolute location on the file system to
    save cache data when the microservice is offline. \# This persisted
    data is only needed if DCM is restarted while clustered applications
    are running. \# When a planned shutdown of a clustered application
    using the cache is underway, it is advisable to delete the persisted
    data. persistentStore = \$E{PERSISTENT_STORE, distributedData} \*
    While performing the upgrade it is always a good idea to ensure that
    while everything is shut down, no persisted data is left behind. If
    there is anything in the folder that represents your cluster, you
    can safely delete its contents. Only do this while the application
    server is offline. This is little trickier when the same DCM is used
    centrally for several clusters (this is not an endorsed or
    recommended practice). Bringing down and upgrading "shared" DCM may
    affected applications that are not to be upgraded.

#### Merging configuration settings

Never use DCM from the prior release with the newer CLM. Always copy
customized settings from an existing DCM into the one that came with the
newer CLM. Run DCM distributed with the new CLM.

## Related

##### Related topics: [Deployment web home](DeploymentWebHome), [Mode details about clustered configurations](ChangeAndConfigurationManagementClusteredEnvironmentVersion605) [related-topics-deployment-web-home-mode-details-about-clustered-configurations]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser, Main.TWikiUser [additional-contributors-main.twikiuser-main.twikiuser]
