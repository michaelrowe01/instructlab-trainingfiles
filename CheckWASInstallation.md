# Check WebSphere Application Server 8.5.5 Installation 

Authors: [Dr. Hans-Joachim Pross](Main.HaJoPross) 

Build basis: Websphere Application Server 8.5.5 

`Note: Support removed for IBM !WebSphere Application Server (Traditional WAS) starting with ELM version 7.0.3. Use !WebSphere Liberty, either embedded and installed with ELM applications, or separately installed`

A small guide, how to check IBM WebSphere Application Server 8.5.5
Installation for the IBM Rational Collaborative Lifecycle Management
(CLM) Platfrom or the IBM Engineering Lifecycle Management (ELM). This
guide is part of the [Configuring Enterprise CLM Reverse Proxies
guide](ConfigureCLMEnterpriseReverseProxy855).

## Prerequisites and Assumptions

For the following the WebSphere Application Server 8.5.5 bits are
assumed to be installed.

|  |  |
|----|----|
|  | **Sofware Versions used** \* IBM WebSphere Application Server V 8.5.5 **Installation Directory** Installation root folder **C:\IBM**. |

## First Steps Console

Start the **First steps console** with Start / IBM WebSphere / IBM
WebSphere Application Server V8.5 / Profiles / / First steps.

Check if the server is running. If it is not running, the Stop the
server link will be a **Start the server** link. Click on **Installation
verification** to run the verification. An output window will be opened.

Although there are 2 warnings reported, the installation is ok. After
the test you can close the output window.

## Check default Application

Now open a browser and enter as address <http://localhost:9080/snoop>.
If you haven't done the Installation verification before, you might need
to start the application server manually. The result should look similar
to the screen shot below.

Now try the same with the fully qualified host name
<http://hajo-clm4.local.int:9080/snoop>.

##### Related topics: 
-   [Configuring Enterprise CLM Reverse Proxies: WebSphere 8.5 and IHS 8.5](ConfigureCLMEnterpriseReverseProxy855) 

##### External links: 

-   [IBM](https://www.ibm.com)

##### Additional contributors: 
-   Main.TWikiUser,
-   Main.TWikiUser