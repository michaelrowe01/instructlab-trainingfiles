META:TOPICINFO{author="rwatts" date="1536779143" format="1.1"
version="1.3"} META:TOPICPARENT{name="DeploymentMonitoring"}

# CLM Managed Beans Overview DKGRAY Authors: Richard Watts, Vishwanath Ramaswamy, Vaughn Rokosz Build basis: 6.0.5 and Later [clm-managed-beans-overview-dkgray-authors-richard-watts-vishwanath-ramaswamy-vaughn-rokosz-build-basis-6.0.5-and-later]

ENDCOLOR

TOC{title="Page contents"}

This document outlines the managed beans available in the CLM product
suite.

### CLM Managed Beans

As part of improving the CLM serviceability, we added several classes of
managed bean to help give administrators a complete picture of what is
happening in the system. To leverage these managed beans, it is helpful
to understand the basic architecture and the serviceability strategy
that we used to approach the problem.

Below (figure 1) is a high level diagram of the CLM architecture.
Several of the applications share a common development framework, called
the Jazz Application Foundation SDK. The managed beans that have been
built have been built as part of this SDK so all applications that are
built on top of it get these managed beans by default. For parts of the
CLM suite that are not built on this framework, they have to build their
managed beans from scratch.

figure 1. The High Level CLM Architecture Overview

As the diagram shows, several applications (tan boxes) share a common
framework and these applications have managed beans. JTS, RTC, RQM,
RDNG, RDM, and GC all have managed beans.

Now that you understand what applications have managed beans, consider
the **Service Invocation Architecture** described in figure 2 and the
recommended attributes that should be considered when monitoring the
overall application health.

figure 2. Jazz Service Invocation Architecture

In addition to those attributes that we recommend monitoring, there are
optional attributes that you might want to consider as well, which we
show you in figure 3.

figure 3. Jazz Service Invocation Architecture - Optional Managed Beans

#### Enabling CLM Managed Beans

The managed beans are not enabled by default out of the box. You need to
consider your monitoring strategy and only turn on those managed beans
you will actually consume. These managed beans are enabled through the
advanced properties admin UI. To turn them on, you would locate the
background task in the table below and enable it by setting the enable
property to **true**. It is recommended that you take the default values
because these have been carefully considered and tuned for optimal
efficiency.

`https://<< host:port >>/<< context root >>/admin#action=com.ibm.team.repository.admin.configureAdvanced`

#### Background Tasks

Managed beans are enabled through scheduled background tasks. These
tasks enable one or more managed beans in specific categories.

META:FILEATTACHMENT{name="CLM_Architecture.png"
attachment="CLM_Architecture.png" attr="" comment="" date="1531303155"
path="CLM_Architecture.png" size="129410" user="rwatts" version="1"}
META:FILEATTACHMENT{name="CLM_Serviceability_Strategy2.png"
attachment="CLM_Serviceability_Strategy2.png" attr="" comment=""
date="1531303182" path="CLM_Serviceability_Strategy2.png" size="108268"
user="rwatts" version="1"}
META:FILEATTACHMENT{name="CLM_Serviceability_Strategy1.png"
attachment="CLM_Serviceability_Strategy1.png" attr="" comment=""
date="1531303205" path="CLM_Serviceability_Strategy1.png" size="165857"
user="rwatts" version="1"}
