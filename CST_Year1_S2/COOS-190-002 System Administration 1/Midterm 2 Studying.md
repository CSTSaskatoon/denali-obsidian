# Review Sheets
## Module 5

## Module 6
### What are Containers?
Containers are packages of software that contain all of the necessary elements to run in any environments
### What are the benefits of using containers?
Faster to start, smaller in size, doesn't need to run the whole OS (less resource-intensive), consistent development environment
### when deciding to use a VM or container, what are considerations?
Use a VM when:
- You need to use different OS
- More isolated than containers
- Preserve state (changes between starting and stopping)
- More secure

Use a Container when:
- multiple instances of an application
- lightweight application that you can deploy at any time
- Need to run an app that is non-persistent, or deployed on-demand
### What is a docker container?
Container using docker
### What is docker?
open-source software to manage containers
### What is docker hub?
A place where you can download container images
## Module 7
### What is High Availability?
Redundant systems, aiming for the least amount of downtime
### Briefly describe and define an Service Level Agreement (SLA)
agreement between client and provider, includes details of the service and standards of the vendor
### What is failover clustering
Having redundant servers so that if one goes down, traffic goes to the backup
### What is Host Clustering
physical servers as nodes available for failover
### What is Guest Clustering
VMs as nodes for failover in cluster (*Server is single point of failure*)
### What is Network Load Balancing (NLB)?
Network traffic is shared across servers in the cluster
*Round Robin* - distributes traffic in a circular motion
*Give and Take* - fills each server with traffic until it's soft cap
*Drain stop* - `while(!isTerminated) {}`
### How many nodes can a Windows Server 2016 NLB Cluster have?
32 computers
### Why must Nodes in a NLB Cluster have a dynamic or static IP set?
*Nodes must be under the same subnet*
When you're sending traffic to the server you don't want the IP to change
**IP Must be static**
### Is NLB a role or feature within the Windows Server 2022 OS?
feature
### Specify the correct order of steps
9. Click Install
6. Select Role-Based or Feature-Based Installation
1. Open Server Manager
3. Click Add Roles and Features
2. Click Manage
8. Click to Add features when prompted
7. Select the Network Load Balancing option
5. Click Next two more times
4. On the Before You Begin page of the Add Roles or Features Wizard, click Next
**May be wrong, no idea**
### What is the command to view or get information about nodes in a cluster?
```PowerShell
get -Nlbclusternode
```
### You host a very busy auction website for a local auction company who auctions off used restaurant equipment. You need to remove a node from the cluster so you can upgrade the physical memory. What command should you use?
```powershell
remove -Nlbclusternode
```
## Module 8
### Explain the concept of Quorum in the context of Server clusters?
Amount of nodes needed to be active for the cluster to stay available
*Like RAID needing a certain number of drives*
You specify what the quorum is
- Dynamic Quorum is also available
- *only nodes have votes*
- *only disk witness has votes*
- *nodes and disk witness have votes*
- *Nodes and file share majority*
### What port number do Cluster Nodes use for communication and to exchange heartbeats?
3343 - TCP and UDP
### What is shared cluster storage?
storage shared between all nodes in a cluster
allows multiple nodes to work together to *perform tasks, share resources, provide redundancy and fault tolerance*
Able to switch storage (*Hot swap*)
### What is a cluster witness disk?
Has an extra vote so it is never an even split
### Multi-site (Stretched Clusters) can be set up either as active-passive or active-active. What does each do?
#### Active-Active
Two or more Active Servers running applications, if one fails the other can take over
#### Active-Passive
One active server running applications and one passive server ready to take over for the active one if it fails
### In Event Viewer where can you search for events related to failover clustering?
failover clustering operations log
- Applications - Services - `logs/Microsoft/WindowsFolder`
### What is Cluster-Aware updating
Feature that allows admin to update cluster nodes with little to no loss
# Important Vocabulary
## Module 5

## Module 6
*Software Defined Infrastructure* - Everything on the computer is virtualized
*Containers* - package of software and libraries/dependencies
*Container Host* - Physical server, can have guest Containers on it (VMs)
*Sandbox* - Environment that is isolated from everything else
*Container Image* - Template for making a container
*Container OS Image* - small, minimalistic, **used ONLY for containers**, made to run other container applications
*Container Repository* - Collection of container images
*Kubernetes* - Automating the deployment and scaling of containers, alternative to docker, can be used across multiple networks
*Process Isolation* - Keeping different applications/processes separate
*Hyper-V Isolation* - process isolation for Hyper-V VMs
### Docker Vocabulary
*Image* - Template for making a container
*Container* - Environment to keep applications isolated
*Dockerfile* - Text file that contains the commands needed to build a docker image
*Build* - Process of building docker images from a dockerfile and any other files in the directory where the image is being built
#### Docker Toolbox
- *Docker Engine* - used for building and running docker containers
- *Docker Compose* - enables you to define a multiple container app together with any dependencies so that you can run it with a single command (*Linking everything*)
- *Docker Machine* - enables you to provision docker hosts by installing the docker engine on the computer in your datacenter or on a cloud provider
- *Docker Client* - includes a command shell that is preconfigured as a docker command line environment
- *Docker Registry* - serves as a central location where users can share docker images
- *Docker Swarm* - Enables you to combine multiple docker engines into a single virtual docker engine
### Docker Solutions Vocabulary
*Docker Hub* - Central docker repository (official)
*Docker Trusted Registry* - Registry in the hub, provides security
*Universal Control Panel* - Enables you to manage docker apps
*Docker Cloud* - enables you to deploy and manage docker apps
*Docker DataCenter* - integrated platform for implementing Containers As A Service (CAAS)
## Module 7
*Datacenter Infrastructure* - physical and virtual components that make up a server
*Server Hardware* - Server hardware
*Storage* - Storage
*Network Infrastructure* - Connections from workstation to workstation and server
*Internet Connectivity* - can you use google?
*Network Services* - don't care
*Business-Impact Analysis* - analysis of acceptable downtime
*Risk Analysis* - how likely is this to backfire?
*RAID* - Redundant Array of Independent Disks
*DAS* - Direct Access Storage - Drive plugs into server
*NAS* - Network Access Storage - Drive plugs into router
*SAN* - Server Access Storage - Drive has dedicated network, looks like they are just getting storage from the server
*Live Migration* - Changing hardware or software configurations while the service is running
*Hyper-V Replica* - image of Hyper-V VMs, can be used for shared cluster storage
*NLB* - Network Load Balancing
*Port Rules* - What inbound/outbound traffic you allow (firewall)
*Affinity* - NLB will sometimes implement this, you can set it to remember you from previous "visits", and decide how you distribute the network traffic
*VSS* - Volume Shadow Copy Service, creates snapshots of drives and such
*Quorum* - Limit of how many nodes can fail
*Unicast* - network connection from one device to another
*Multicast* - network connection from one device to as many devices that meet the specifications
*Node* - VM or physical server that can take over in the case of a failover
*Convergence* - isn't in textbook
## Module 8
*Cluster Partitioning* - if it doesn't meet quorum this happens
*RSS* - Receive Side Scaling - used in network adapters that can spread the traffic across multiple CPUs
*RDMA* - Remote Direct Memory Access - good throughput with low CPU utilization
*Multi-Site (Stretched) Cluster* - Highly available services in more than one location
*Non-Authoritative Restore* - Rollback if a single cluster node is damaged but the rest is functioning
*Authoritative Restore* - Rollback all nodes (change configuration)