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
<pre>
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
</pre>
