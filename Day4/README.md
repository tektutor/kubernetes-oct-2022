# Day 4

## Installing multi-node Kubernetes in a laptop/desktop for learning purpose
<pre>
https://medium.com/@jegan_50867/kubernetes-lightweight-developer-setup-using-rancher-k3d-a3a94e9b5eb4
</pre>

## What is DaemonSet?
- Daemon is a Kubernetes object just like Deployment but managed by DaemonSet Controller
- Deployment is managed by Deployment Controller
- DaemonSet Controller ensures 1 Pod runs on every node. If your K8s cluster has 5 nodes, DaemonSet Controller will ensure 1 Pod runs on every node


## Monitoring Performance using Prometheus and Grafana
```
cd ~/kubernetes-oct-2022
git pull
cd Day4/prometheus-grafana
kubectl apply -f prometheus-grafana.yml

kubectl get all -n monitoring
kubectl get svc
```

Accessing Prometheus Dashboard
```
http://<minikube-node-ip>:<promotheus-nodeport-service-port>
http://192.169.49.2:30185
```
In the above url, you need replace 30185 with your prometheus service node-port.

Accessing Grafana Dashbaord
```
http://<minikube-node-ip>:<grafana-nodeport-service-port>
http://192.169.49.2:30500
```
In the above url, you need replace 30500 with your grafana service node-port.

## Kubernetes Network Model

Kubernetes Network addons
1. Flannel - Overlay ( Backends - VXLAN, UDP, etc., )
2.   - Doesn' support Network Policy
3. Calico - BGP 
4.   - Network Policy
5. Weave - Network Mesh
6.   - Network Policy

## Post Test & Feedback link

<pre>
Test link - https://app.mymapit.in/code4/tiny/wJWK5Y 

Feedback link : https://tcheck.co/nts8h9
</pre>
