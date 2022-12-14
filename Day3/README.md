# Day 3

## You might be interested in these blogs
<pre>
https://medium.com/@jegan_50867/kubernetes-3-node-cluster-using-k3s-d28b2c09e2f7

https://medium.com/@jegan_50867/kubernetes-3-node-cluster-using-k3s-with-docker-e325cc82fd50
</pre>


## Recommnended Projects to learn Kubernetes internals by doing the setup by hand
<pre>
https://github.com/kelseyhightower/kubernetes-the-hard-way
</pre>

## What are the options to install Kubernetes?
1. Minikube - Good for learning purpose but not production grade
2. MicroK8s - Lightweight setup,  good for learning and production 
3. K3S - Lightweight setup, good for learning and production grade
4. Kubernetes setup using kubeadm - https://medium.com/tektutor/kubernetes-3-node-cluster-setup-50943378be41
5. Kubespray - Ansible playbook - Production Grade

## Creating a ClusterIP Internal Service
```
kubectl create deployment nginx --image=bitnami/nginx:latest --replicas=5
kubectl expose deploy/nginx --type=ClusterIP --port=8080
kubectl describe svc/nginx
```

Let's create test pod that has curl utility
```
kubectl create deploy utils --image=tektutor/utils:latest
kubectl exec -it utils-7b4dcffbfd-w5cwg sh
curl http://nginx:8080
```

Expected output
```
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/CustomDockerImage# kubectl exec -it utils-7b4dcffbfd-w5cwg sh
kubectl exec [POD] [COMMAND] is DEPRECATED and will be removed in a future version. Use kubectl exec [POD] -- [COMMAND] instead.

# curl http://nginx:8080
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
# exit
```

## Creating an external NodePort service for nginx deployment
```
kubectl delete svc/nginx 
kubectl expose deploy/nginx --type=NodePort --port=8080
kubectl describe svc/nginx 
kubectl get nodes -o wide
```

Testing the NodePort external service from local machine
```
curl <node-ip>:<node-port>
```

Expected output
```
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/CustomDockerImage# kubectl delete svc/nginx
service "nginx" deleted
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/CustomDockerImage# kubectl expose deploy/nginx --type=NodePort --port=8080
service/nginx exposed
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/CustomDockerImage# kubectl get svc
NAME         TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
kubernetes   ClusterIP   10.43.0.1       <none>        443/TCP          104m
nginx        NodePort    10.43.120.145   <none>        8080:30303/TCP   3s
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/CustomDockerImage# kubectl get nodes -o wide
NAME                   STATUS   ROLES                  AGE    VERSION        INTERNAL-IP       EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
worker1.tektutor.org   Ready    <none>                 97m    v1.25.3+k3s1   192.168.167.135   <none>        Ubuntu 20.04.3 LTS   5.15.0-52-generic   docker://20.10.17
master.tektutor.org    Ready    control-plane,master   104m   v1.25.3+k3s1   192.168.167.152   <none>        Ubuntu 20.04.3 LTS   5.15.0-52-generic   docker://20.10.17
worker2.tektutor.org   Ready    <none>                 96m    v1.25.3+k3s1   192.168.167.136   <none>        Ubuntu 20.04.3 LTS   5.15.0-52-generic   docker://20.10.17
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/CustomDockerImage# curl 192.168.167.135:30303
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/CustomDockerImage# curl 192.168.167.152:30303
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/CustomDockerImage# curl 192.168.167.136:30303
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

The other way to access the nodeport service is within some Pod
```
curl http://<service-name>:<service-port>
curl http://nginx:8080
```

## Creating LoadBalancer external service

This type of service is normally used in public cloud.

```
kubectl delete svc/nginx
kubectl expose deploy/nginx --type=LoadBalancer --port=8080
kubectl get svc
kubectl describe svc/nginx
```

Accessing the LoadBalancer service
```
curl <load-balancer-ip>:8080
```

## Creating application deployment using declarative manifest file
```
kubectl create deployment nginx --image=bitnami/nginx:latest --replicas=5 --dry-run=client -o yaml
```

Expected output
<pre>
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# kubectl create deploy nginx --image=bitnami/nginx:latest --replicas=5 --dry-run=client -o yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: nginx
  name: nginx
spec:
  replicas: 5
  selector:
    matchLabels:
      app: nginx
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: nginx
    spec:
      containers:
      - image: bitnami/nginx:latest
        name: nginx
        resources: {}
status: {}
</pre>

We can redirect the above output to a file as shown below
```
kubectl create deploy nginx --image=bitnami/nginx:latest --replicas=5 --dry-run=client -o yaml > nginx-deploy.yml
```
Expected output
<pre>
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# <b>kubectl create deploy nginx --image=bitnami/nginx:latest --replicas=5 --dry-run=client -o yaml > nginx-deploy.yml</b>
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# <b>ls</b>
nginx-deploy.yml
</pre>

Creating the deployment in declarative style
```
kubectl create -f nginx-deploy.yml
```

Expected output
<pre>
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# kubectl create  -f  nginx-deploy.yml 
deployment.apps/nginx created
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# kubectl get deploy,rs,po
NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nginx   5/5     5            5           8s

NAME                               DESIRED   CURRENT   READY   AGE
replicaset.apps/nginx-66664d749f   5         5         5       8s

NAME                         READY   STATUS    RESTARTS   AGE
pod/dnsutils                 1/1     Running   0          135m
pod/nginx-66664d749f-dpwd6   1/1     Running   0          8s
pod/nginx-66664d749f-8f5rd   1/1     Running   0          8s
pod/nginx-66664d749f-srtk5   1/1     Running   0          8s
pod/nginx-66664d749f-5nwvc   1/1     Running   0          8s
pod/nginx-66664d749f-58gmh   1/1     Running   0          8s
</pre>

## Declaratively scaling up/down the deployment
Edit the nginx-deploy.yml file and update the replicas to whatever number of instances you need. In my case, I updated the replicas to 3 to scale down from 5 instances.
```
kubectl apply -f nginx-deploy.yml
```

Expected output
<pre>
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# kubectl apply -f nginx-deploy.yml 
Warning: resource deployments/nginx is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
deployment.apps/nginx configured
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# kubectl get po
NAME                     READY   STATUS    RESTARTS   AGE
dnsutils                 1/1     Running   0          141m
nginx-66664d749f-dpwd6   1/1     Running   0          6m5s
nginx-66664d749f-8f5rd   1/1     Running   0          6m5s
nginx-66664d749f-58gmh   1/1     Running   0          6m5s
</pre>

## Deleting kubernetes resource in declarative style
```
kubectl delete -f nginx-deploy.yml
```

Expected output
<pre>
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# kubectl delete -f nginx-deploy.yml 
deployment.apps "nginx" deleted
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# kubectl get all
NAME           READY   STATUS    RESTARTS   AGE
pod/dnsutils   1/1     Running   0          145m

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.43.0.1    <none>        443/TCP   3h38m
</pre>

## Updating labels to existing deployment in declarative style
Edit the nginx-deploy.yml as shown below
```
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: nginx
    tier: frontend
  name: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: nginx
        tier: frontend
    spec:
      containers:
      - image: bitnami/nginx:latest
        name: nginx
        resources: {}
status: {}
```

Expected output
<pre>
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# kubectl create -f nginx-deploy.yml --save-config
deployment.apps/nginx created
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# kubectl nginx-deploy.yml 
error: unknown command "nginx-deploy.yml" for "kubectl"
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# vim nginx-deploy.yml 
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# kubectl apply -f nginx-deploy.yml 
The Deployment "nginx" is invalid: spec.selector: Invalid value: v1.LabelSelector{MatchLabels:map[string]string{"app":"nginx", "tier":"frontend"}, MatchExpressions:[]v1.LabelSelectorRequirement(nil)}: field is immutable
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# vim nginx-deploy.yml 
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# kubectl apply -f nginx-deploy.yml 
deployment.apps/nginx configured
</pre>

Checking the label applied on deployment, resplicaset and pods
<pre>
root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# kubectl get deploy --show-labels
NAME    READY   UP-TO-DATE   AVAILABLE   AGE     LABELS
nginx   3/3     3            3           5m10s   app=nginx,tier=frontend

root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# kubectl get rs --show-labels
NAME               DESIRED   CURRENT   READY   AGE     LABELS
nginx-7cbfdf6bd9   3         3         3       3m35s   app=nginx,pod-template-hash=7cbfdf6bd9,tier=frontend
nginx-66664d749f   0         0         0       5m22s   app=nginx,pod-template-hash=66664d749f

root@master.tektutor.org:~/kubernetes-oct-2022/Day3/declarative# kubectl get po --show-labels
NAME                     READY   STATUS    RESTARTS   AGE     LABELS
dnsutils                 1/1     Running   0          152m    <none>
nginx-7cbfdf6bd9-pdrbr   1/1     Running   0          3m48s   app=nginx,pod-template-hash=7cbfdf6bd9,tier=frontend
nginx-7cbfdf6bd9-q49q6   1/1     Running   0          3m43s   app=nginx,pod-template-hash=7cbfdf6bd9,tier=frontend
nginx-7cbfdf6bd9-6k2m9   1/1     Running   0          3m38s   app=nginx,pod-template-hash=7cbfdf6bd9,tier=frontend
</pre>

### Creating a ClusterIP internal service for nginx deployment
```
kubectl expose deploy/nginx --type=ClusterIP --port=8080 --dry-run=client -o yaml > nginx-clusterip-svc.yml
kubectl apply -f nginx-clusterip-svc.yml
kubectl get svc
kubectl describe svc/nginx
kubectl delete -f nginx-clusterip-svc.yml
```

### Creating a NodePort external service for nginx deployment
```
kubectl expose deploy/nginx --type=NodePort --port=8080 --dry-run=client -o yaml > nginx-nodeport-svc.yml
kubectl apply -f nginx-nodeport-svc.yml
kubectl get svc
kubectl describe svc/nginx
kubectl delete -f nginx-nodeport-svc.yml
```

### Creating a LoadBalancer external service for nginx deployment
```
kubectl expose deploy/nginx --type=LoadBalancer --port=8080 --dry-run=client -o yaml > nginx-lb-svc.yml
kubectl apply -f nginx-lb-svc.yml
kubectl get svc
kubectl describe svc/nginx
kubectl delete -f nginx-lb-svc.yml
```

## Deploying multipod application - Wordpress with mysql database

```
cd ~/kubernetes-oct-2022
git pull
cd Day3/declarative/wordpress

kubectl apply -f mysql.yml
kubectl apply -f wordpress.yml

kubectl get po,svc
```

Accessing the wordpress web page from your web browser on the lab machine
```
http://<node-id>:<node-port>
```

You might find this interesting
<pre>
https://kubernetes.io/docs/concepts/storage/persistent-volumes/

https://www.tecmint.com/install-nfs-server-on-ubuntu/
</pre>
