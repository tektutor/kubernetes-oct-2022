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
<b>etcd-minikube                      1/1     Running   0             19m</b>
<b>kube-apiserver-minikube            1/1     Running   0             19m</b>
<b>kube-controller-manager-minikube   1/1     Running   0             19m</b>
kube-proxy-lp2pb                   1/1     Running   0             18m
<b>kube-scheduler-minikube            1/1     Running   0             19m</b>
storage-provisioner                1/1     Running   1 (18m ago)   19m
</pre>

The highlighted pods are the Control Plane Components that runs in a master node.

## Creating your first Kubernetes Deployment(application)
```
kubectl create deployment nginx --image=nginx:latest
```

Expected output
<pre>
jegan@tektutor.org:~$ <b>kubectl create deployment nginx --image=nginx:latest</b>
deployment.apps/nginx created
</pre>

## Listing the deployment under default namespace
```
kubectl get deployments
kubectl get deployment
kubectl get deploy
```

Expected output
<pre>
jegan@tektutor.org:~$ kubectl get deployments
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   1/1     1            1           9m3s
jegan@tektutor.org:~$ kubectl get deployment
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   1/1     1            1           9m5s
jegan@tektutor.org:~$ kubectl get deploy
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   1/1     1            1           9m7s
</pre>

## Listing Replicasets under default namespace
```
kubectl get replicasets
kubectl get replicaset
kubectl get rs
```

Expected output
<pre>
jegan@tektutor.org:~$ kubectl get replicasets
NAME               DESIRED   CURRENT   READY   AGE
nginx-6d666844f6   1         1         1       19m
jegan@tektutor.org:~$ kubectl get replicaset
NAME               DESIRED   CURRENT   READY   AGE
nginx-6d666844f6   1         1         1       19m
jegan@tektutor.org:~$ kubectl get rs
NAME               DESIRED   CURRENT   READY   AGE
nginx-6d666844f6   1         1         1       19m
</pre>

## Listing pods under default namespace
```
kubectl get pods
kubectl get pod
kubectl get po
```

Expected output
<pre>
jegan@tektutor.org:~$ kubectl get pods
NAME                     READY   STATUS    RESTARTS   AGE
nginx-6d666844f6-hk2jg   1/1     Running   0          20m
jegan@tektutor.org:~$ kubectl get pod
NAME                     READY   STATUS    RESTARTS   AGE
nginx-6d666844f6-hk2jg   1/1     Running   0          20m
jegan@tektutor.org:~$ kubectl get po
NAME                     READY   STATUS    RESTARTS   AGE
nginx-6d666844f6-hk2jg   1/1     Running   0          21m
</pre>

## Scale up nginx deployment to 5 Pods
```
kubectl scale deploy/nginx --replicas=5
```

## What happens internally within Kubernetes cluster when we create a deployment
```
kubectl create deployment nginx --image=nginx:latest
```

<pre>
1. kubectl makes a REST API call to API Server request the API Server to create a Deployment by name 'nginx' with the docker image 'nginx:latest'

2. API Server receives the request from kubectl, it then creates a record in etcd database for the deployment with the name nginx.

3. API Server triggers a broadcasting event something like "New Deployment Created"

4. Deployment Controller is registered to be notified for Deployment related events.  Deployment Controller receives the event and then it will send a REST call to API Server requesting it to create a ReplicaSet for the nginx deployment.

5. API Server receives the request from Deployment Controller, it then creates a ReplicaSet record in etcd database for the nginx deployment.

6. API Server triggers a broadcasting event something like "New ReplicaSet Created"

7. ReplicaSet Controller is registered to be notified for ReplicaSet related events.  ReplicaSet controller receives the event and then it will send a REST call to API Server requesting it to create Pod entries.

8. API Server receives the request from ReplicaSet Controller, it then creates so many Pod records in etcd database for the nginx deployment.

9. API Server triggers a broadcasting event something like "New Pod Created"

10. Scheduler receives the New Prod Created event, it identifies healthy nodes where those pods can be deployed and makes a REST call to API Server with its Scheduling recommendations.

11. API Server receives the request from Scheduler, it then retrieves the corresponding Pod records from the etcd database and updates the Scheduling information(ie node where they can be deployed).

12. API Server will trigger broadcasting events that "Pod Schedule" kind of events.

13. kubelet running on each node will receive that event, if the node mentioned the node where kubelet is running.  Kubelet then interacts with the Container Runtime installed on the local machine, pull the docker image and creates the containers for the Pod.  Kubelet monitors the status and keeps updating the API Server via REST call. Kubelet sends this kind heart-beat status event frequently to API Server.

14. API Server receives those events from kubelet, it retrieves the Pod entries from etcd database and then it updates with the current status of the Pod.  This is repeated for every Pod it received an event from respective kubelet.
</pre>

## Deploy a python microservice into Kubernetes cluster
```
kubectl create deployment/hello --image=tektutor/hello-ms:3.0  --replicas=5
```

Listing the deployment, replicaset and pods
```
kubectl get deploy,rs,po
```

Creating an internal(ClusterIP) service
```
kubectl expose deploy/hello --type=ClusterIP --port=80
```

Listing the service
```
kubectl get services
kubectl get service
kubectl get svc
```

Finding more details about the service
```
kubectl describe svc/hello
```
