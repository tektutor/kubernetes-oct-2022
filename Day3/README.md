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
4. Kubernetes setup using kubeadm
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
