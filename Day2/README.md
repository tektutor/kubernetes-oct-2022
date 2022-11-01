# Day 2

## What is an Orchestration Platform?
- a container management tool
- self-healing platform
  - attempts to repair its components when they are faulty or when they stop responding
- manages containerized applications
  - deploy containerized applications
  - on demand you can scale up/down your application instances
  - it can monitor the health of your application and repair when they don't respond
- rolling updates
  - upgrading your currently deployed applications to latest version without any downtime
  - could also download your application version to lower version in case of instability
- service discovery
- provides an eco-system that helps make your application highly availble(HA)
- Examples
  - Docker SWARM ( Good for Dev/QA or personal learning purpose ) - generally not used in 
  - Google Kubernetes ( Open source - production grade )
  - Red Hat OpenShift ( Enterpise product - production grade )
  - AWS ROSA (RedHat  OpenShift ) - Managed OpenShift as a Service (SaaS)  - production grade
  - Azure RedHat OpenShift (ARO) - Managed OpenShift as a Service (SaaS) - production grade
  - OpenShift Origin (OKD) - Opensource variant of Red Hat Openshift - production grade

## What are different Container Orchestration Platform available?
1. Docker SWARM
   - only supports Docker
2. Kubernetes
   - support many different containers runtimes
3. Red Hat OpenShift ( It is developed on top of Kubernetes with many additional features )
   - only supports CRI-O Container Runtime


## Kubernetes
- is an Container Orchestration Platform developed by Google using Go Programming Language
- it is an opensource project
- it works as a cluster of nodes
- nodes are servers/virtual machines/cloud virtual machines
- there are two type of nodes
  1. Master 
     - Control Plane components runs only in Master Node
     - Control Plane components are the one which implement Kubernestes Orchestration features
     - Generally has Master Role
     - Optionally Master Node can also be configured to support Worker Role
  2. Worker
     - Supports only Worker Role
     - User applications are deployed
