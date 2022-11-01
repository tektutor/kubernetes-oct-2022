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
- Kubernetes in shorts is also reffered as k8s
- it works as a cluster of nodes
- Kubernetes cluster may have 1 or more master nodes and 1 or more worker nodes
- Kubernetes cluster that has many master nodes are considered more stable and production grade
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
- Some importants tools
  - kubectl (client tool used by end-users to interact with Kubernetes cluster)
  - kubeadm ( is an administrative tool that helps in bootstrapping master node and adding/removing worker nodes from Kubernetes cluster)
  - kubelet ( is Kubernetes Container Agent that interacts with Container Runtime via Container Runtime Interface )

## What are the Control Plan Components?
1. API Server ( implements all orchestrations functionality as REST API )
2. etcd ( key/value pair data-store )
3. Scheduler
4. Controller Managers ( it is a collection many Controllers )

### What does the API Server do?
- API Server is the critical component of Control Plane in the master node
- All the k8s components communicate only to API Server
- API Server is the only component allowed to talk to etc data-store
- API Server save the cluster state ( include application status ) into the etcd database
- each time API Server updates something in etcd datastore, it trigger some specific events

### What is etcd ?
- is an independent opensource project used by Kubernetes
- this is where the Control Plane and application status is recorded and maintained
- even if the Kubernetes cluster goes unstable, we can recover the Kubernetes cluster based on etcd data
- though single etcd datastore is sufficient, generally in a production K8s cluster, a cluster etcd datastores are created
- when a cluster of etcd data-store, each etcd is connected to one master node

### What is Scheduler ?
- this is component responsible to identify a health node where user application can be deployed
- scheduler identifies node(s) to deploy user applications and nofifies the API Server with its recommendation

### What is Controller Manager(s)
- collection of many Controllers
- some controllers
  - Deployment Controller
  - ReplicaSet Controller
  - Job Controller
  - Endpoint Controller
  - Storage Controller

### Kubernetes Objects(Resources)
- Pod
- ReplicaSet
- Deployment
- Service
- Ingress
- Route

#### What is a Pod ?
- In Kubernetes applications are managed as Pod
- Pod is a group of related containers
- the smallest unit that can be deployed and managed within K8s is Pod
- IP address is assigned on a Pod level not on the container level.  If 2 containers are part of a single Pod, they share the same IP Address

#### What is a ReplicaSet ?

#### What is a Deployment ?

#### What is a Service ?

#### What is an Ingress ?

#### What is a Route ?
