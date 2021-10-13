# IBM Edge Application Manager 101

IEAM provides you with edge computing features to help you manage and deploy workloads from a management hub cluster to edge devices and remote instances of OpenShift Container Platform or other Kubernetes-based clusters.


## Architecture

The goal of edge computing is to harness the disciplines that have been created for hybrid cloud computing to support remote operations of edge computing facilities. IEAM is designed for that purpose.

The deployment of IEAM includes the management hub that runs in an instance of OpenShift Container Platform installed in your data center. The management hub is where the management of all of your remote edge nodes (edge devices and edge clusters) occurs.

These edge nodes can be installed in remote on-premises locations to make your application workloads local to where your critical business operations physically occur, such as at your factories, warehouses, retail outlets, distribution centers, and more.

The following diagram depicts the high-level topology for a typical edge computing setup:

  !["watson-twilio-sms"](docs/images/arch-01.png)

The IEAM management hub is designed specifically for edge node management to minimize deployment risks and to manage the service software lifecycle on edge nodes fully autonomously. A Cloud installer installs and manages the IEAM management hub components. Software developers develop and publish edge services to the management hub. Administrators define the deployment policies that control where edge services are deployed. IEAM handles everything else.


## Components

IBM Edge Application Manager (IEAM) includes several components that are bundled with the product. Below are the components in IEAM v4.3.

- IBM Cloud Platform Common Services(v3.6.x) - This is a set of foundational components that are installed automatically as part of the IEAM operator installation.
- Agbot(v2.29.0-595) - Agreement bot (agbot) instances are created centrally and are responsible for deploying workloads and machine learning models to IEAM.
- MMS(v1.5.3-338) - The Model Management System (MMS) facilitates the storage, delivery, and security of models, data, and other metadata packages needed by edge services. This enables edge nodes to easily send and receive models and metadata to and from the cloud.
- Exchange API(v2.87.0-531) - The Exchange provides the REST API that holds all the definitions (patterns, policies, services, and so on) used by all the other components in IEAM.
- Management console(v1.5.0-578) - The web UI used by IEAM administrators to view and manage the other components of IEAM.
- Secure Device Onboard(v1.11.11-441) - The SDO component enables technology that is created by Intel to make it simple and secure to configure edge devices and associate them with an edge management hub.
- Cluster Agent(v2.29.0-595) - This is a container image, which is installed as an agent on edge clusters to enable node workload management by IEAM.
- Device Agent(v2.29.0-595) - This component is installed on edge devices to enable node workload management by IEAM.
- Secrets Manager(v1.0.0-168) - The Secrets Manager is the repository for secrets deployed to edge devices, enabling services to securely receive credentials used to authenticate to their upstream dependencies.


## Pre-requisites

IEAM hub has been deployed on a OpenShift cluster and IEAM agent has been deployed on at least one edge node.

Deployment of IEAM hub and agent is not in the scope of this repo. Detail deployment instructions of IEAM v4.3 are available at
- [Installing the management hub](https://www.ibm.com/docs/en/edge-computing/4.3?topic=installing-management-hub)
- [Installing edge nodes](https://www.ibm.com/docs/en/edge-computing/4.3?topic=installing-edge-nodes)

IEAM v4.3 system is used while dveloping this repo.


## Steps

The exercise helps you understand
- deploy IEAM policies using patterns
- deploy IEAM policies using policies
- zero touch IEAM agent deployment and registering of SDO (Secure Device Onboard) device
- CI/CD process for edge services
- IEAM secret
- Cluster agent

IEAM hub should have been deployed before you start the exercise. VM machines running Ubuntu v20.x are used to simulate a edge node for the remaining of the exercise. For a full list of supported edge nodes, refer to [Supported architectures and operating systems](https://www.ibm.com/docs/en/edge-computing/4.3?topic=devices-preparing-edge-device).

This repo adopted the contents in the following repos
- [Horizon CPU To IBM Event Streams Service](https://github.com/open-horizon/examples/tree/master/edge/evtstreams/cpu2evtstreams#horizon-cpu-to-ibm-event-streams-service)
- 


### Step 1 - Preparing Working Environment on Edge Node

Before you can work with your edge node, you need to prepare a shell environment.

> Note: In case the shell terminal times out during your exercise, the steps in this section must be retaken.

1. Connect to your edge node.

  ```
  ssh root@<your edge node IP/hostname>
  ```

1. Login to your edge node when prompted.

1. Go to your IEAM agent deployment folder.

1. Three environment variables must be set in order to operate on your edge node successfully.
  - HZN_ORG_ID
  - HZN_FSS_CSSURL
  - HZN_EXCHANGE_USER_AUTH

  > Note: the value of environment variable `HZN_EXCHANGE_USER_AUTH` is in format of `iamapikey:<horizon-API-key>`.

1. As part of the infrasctucture installation process for IBM Edge Computing Manager, File `./agent-install.cfg` was created in the current folder of each edge node. It can contain the value for the above environment variables. For the values that are not available in the file, you can get them from your system administrator.

1. Set environment variables.

  ```
  export HZN_ORG_ID=[your org ID]
  export HZN_FSS_CSSURL=[your exchange and css url]
  export HZN_EXCHANGE_USER_AUTH=[your crenetial]
  ```

1. Verify environment variable `HZN_ORG_ID` and `HZN_FSS_CSSURL`.

  ```
  echo $HZN_ORG_ID
  echo $HZN_FSS_CSSURL
  echo $HZN_EXCHANGE_USER_AUTH
  ```

> Note: In case the shell terminal times out during your exercise, the steps in this section must be retaken.


### Step 2 - Cloning the Repo



### Step 3 - Deploying IEAM Policies using Patterns

Using a deployment pattern is a straightforward and simple way to deploy a service to your edge node. You specify the top-level service, or multiple top-level services, to be deployed to your edge node and IEAM handles the rest, including the deployment of any dependent services your top-level service might have.

1. Unregister your node. This ensures you start in a clean environment.

  ```
  hzn unregister -f
  ```

1. 

  ```
  hzn register -p IBM/pattern-ibm.cpu2evtstreams -f userinput.json -s ibm.cpu2evtstreams --serviceorg IBM -t 120 
  ```



### Step 3 - Deploying IEAM Policies using Policies




