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
- ReplicaSet manages Pod and the number instance of Pods that is supposed to be running
- Each ReplicaSet has one or more Pods

#### What is a Deployment ?
- generally we deploy our application as Kubernetes Deployment
- Kubernetes Deployment creates ReplicaSet to manage the Pods
- Deployment manages ReplicaSet
- Each Deployment has one or more ReplicaSet
- This is Kubernetes object that represents your application deployment within Kubernetes

#### What is a Service ?

#### What is an Ingress ?

#### What is a Route ?


## Installing Kubernetes using Minikube project
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube version
minikube start
```

Expected output
<pre>
jegan@tektutor.org:~$ <b>curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64</b>
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 73.0M  100 73.0M    0     0  8493k      0  0:00:08  0:00:08 --:--:-- 8880k
jegan@tektutor.org:~$ <b>ls</b>
Desktop    Downloads  kubernetes-oct-2022   Music     Public     Videos
Documents  git-token  minikube-linux-amd64  Pictures  Templates
jegan@tektutor.org:~$ <b>sudo install minikube-linux-amd64 /usr/local/bin/minikube</b>
[sudo] password for jegan: 
jegan@tektutor.org:~$ <b>ls</b>
Desktop    Downloads  kubernetes-oct-2022   Music     Public     Videos
Documents  git-token  <b>minikube-linux-amd64</b>  Pictures  Templates
jegan@tektutor.org:~$ <b>rm minikube-linux-amd64</b>
jegan@tektutor.org:~$ <b>ls</b>
Desktop  Documents  Downloads  git-token  kubernetes-oct-2022  Music  Pictures  Public  Templates  Videos
jegan@tektutor.org:~$ <b>minikube version</b>
minikube version: v1.27.1
commit: fe869b5d4da11ba318eb84a3ac00f336411de7ba
jegan@tektutor.org:~$ <b>minikube start</b>
😄  minikube v1.27.1 on Ubuntu 20.04
✨  Automatically selected the docker driver. Other choices: ssh, none
📌  Using Docker driver with root privileges
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
💾  Downloading Kubernetes v1.25.2 preload ...
    > preloaded-images-k8s-v18-v1...:  385.41 MiB / 385.41 MiB  100.00% 7.68 Mi
    > gcr.io/k8s-minikube/kicbase:  387.11 MiB / 387.11 MiB  100.00% 4.74 MiB p
    > gcr.io/k8s-minikube/kicbase:  0 B [________________________] ?% ? p/s 57s
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
🐳  Preparing Kubernetes v1.25.2 on Docker 20.10.18 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: default-storageclass, storage-provisioner
💡  kubectl not found. If you need it, try: 'minikube kubectl -- get pods -A'
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
</pre>

## Installing kubernetes client tool(kubectl) in Linux
```
curl -LO https://dl.k8s.io/release/v1.25.0/bin/linux/amd64/kubectl
ls
chmod +x ./kubectl
ls
sudo mv kubectl /usr/local/bin
kubectl get nodes
```

Expected output
<pre>
jegan@tektutor.org:~$ <b>curl -LO https://dl.k8s.io/release/v1.25.0/bin/linux/amd64/kubectl</b>
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   138  100   138    0     0    371      0 --:--:-- --:--:-- --:--:--   371
100 42.9M  100 42.9M    0     0  9125k      0  0:00:04  0:00:04 --:--:-- 10.1M
jegan@tektutor.org:~$ <b>ls</b>
Desktop  Documents  Downloads  git-token  <b>kubectl</b>  kubernetes-oct-2022  Music  Pictures  Public  Templates  Videos
jegan@tektutor.org:~$ <b>chmod +x ./kubectl</b>
jegan@tektutor.org:~$ <b>ls</b>
Desktop  Documents  Downloads  git-token  kubectl  kubernetes-oct-2022  Music  Pictures  Public  Templates  Videos
jegan@tektutor.org:~$ <b>sudo mv kubectl /usr/local/bin</b>
jegan@tektutor.org:~$ <b>kubectl get nodes</b>
NAME       STATUS   ROLES           AGE     VERSION
minikube   Ready    control-plane   6m18s   v1.25.2
</pre>

# Kubernetes Commands

## Listing the kubernetes cluster nodes
```
kubectl get nodes
```
Expected output
<pre>
jegan@tektutor.org:~$ <b>kubectl get nodes</b>
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   18m   v1.25.2
</pre>

## Listing the kubernetes components running in master node under kube-system namespace
```
kubectl get po -n kube-system
```

Expected output
<pre>
jegan@tektutor.org:~$ <b>kubectl get po -n kube-system</b>
NAME                               READY   STATUS    RESTARTS      AGE
coredns-565d847f94-h46zz           1/1     Running   0             18m
etcd-minikube                      1/1     Running   0             19m
kube-apiserver-minikube            1/1     Running   0             19m
kube-controller-manager-minikube   1/1     Running   0             19m
kube-proxy-lp2pb                   1/1     Running   0             18m
kube-scheduler-minikube            1/1     Running   0             19m
storage-provisioner                1/1     Running   1 (18m ago)   19m
</pre>
