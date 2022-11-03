# Day 4

## Installing multi-node Kubernetes in a laptop/desktop for learning purpose
<pre>
https://medium.com/@jegan_50867/kubernetes-lightweight-developer-setup-using-rancher-k3d-a3a94e9b5eb4
</pre>

## What is DaemonSet?
- Daemon is a Kubernetes object just like Deployment but managed by DaemonSet Controller
- Deployment is managed by Deployment Controller
- DaemonSet Controller ensures 1 Pod runs on every node. If your K8s cluster has 5 nodes, DaemonSet Controller will ensure 1 Pod runs on every node
