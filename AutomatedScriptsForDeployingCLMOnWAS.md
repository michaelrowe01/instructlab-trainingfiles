# Automatically deploying the Collaborative Lifecycle Management applications on WebSphere Application Server

Authors: Main.MichaelAfshar, Main.SudarshaWijenayake 
Build basis: The Rational solution for Collaborative Lifecycle Management (CLM) 4.0 and later, up to and including ELM 7.0.2

`Note: Support removed for IBM !WebSphere Application Server (Traditional WAS) starting with ELM version 7.0.3. Use !WebSphere Liberty, either embedded and installed with ELM applications, or separately installed`

By using Jython scripting, you can reduce the effort and resources
associated with common administration tasks in WebSphere Application
Server.

The following scripts are provided out of the box and can be used:

-   `clm_was_config.py` This script configures WebSphere Application
    Server settings.
-   `clm_deploy.py` This script deploys CLM applications on a single
    server.
-   `clm_deployed_distributed.py` This script deploys CLM applications
    in a distributed environment.
-   `clm_undeploy.py` This script removes previously deployed CLM
    applications.
-   `clm_undeploy_distributed.py` This script removes previously
    deployed CLM applications in a distributed environment.

**General Restriction:** The deploy and undeploy scripts are meant to be
used together. If you deploy the .WAR files in the WebSphere Integrated
Solutions Console without using the deploy script, then you must
undeploy the .WAR files by using the Integrated Solutions Console. If
the undeploy script is not working as expected, check the application
names in the WebSphere Integrated Solutions Console. The deploy and
undeploy scripts use the application names with a dot, such as jts.war,
whereas Integrated Solutions Console may assign names with an
underscore, such as jts_war.

**IBM i and z/OS Restriction:** These WebSphere Application Server
Jython scripts are not supported on IBM i or z/OS operating systems.

## Topics in this series

-    [Setting up WebSphere Application Server by using the
    clm_was_config.py script](SetupWASJython)
-    [Deploying web applications on one server by using the
    clm_deploy.py script](DeployWASJython)
-    [Deploying web applications in a distributed environment by using
    the clm_deploy_distributed.py script](DeployWASJythonDistributed)
-    [Uninstalling web applications by using the clm_undeploy.py
    script](UninstallWebApps)
-    [Uninstalling web applications in a distributed environment by
    using the clm_undeploy_distributed.py
    script](UninstallWebAppsDistributed)
-    [CLM Deployment Automation for WAS - Departmental Topology
    ](CLMAutomationScriptsforWASDepartmentalTopology)

##### Related topics: 
[related-topics]

##### External links: 
[external-links]

##### Additional contributors: 
[additional-contributors]
