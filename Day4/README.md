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
In order to install prometheus and grafana into K8 cluster, you may run the below single manifest file

```
kubectl apply 
   -f https://raw.githubusercontent.com/giantswarm/prometheus/master/manifests-all.yaml
```

### Prometheus Dashboard
Check the node port services exposed for Prometheus
kubectl get svc

From Browser (For DIND K8 Cluster)
<pre>
http://10.192.0.2:30368
</pre>

## Grafana Dashboard
Check the node port services
```
kubectl get svc
```

From Browser (For DIND K8 Cluster)
</pre>
http://10.192.0.2:<node-port-of-grafana-service>
</pre>

For example:-
<pre>
	http://10.192.0.2:32561
	
	Default username - admin

	Default password - admin
</pre>

For deleting all prometheus and grafana related components from K8
kubectl delete namespace monitoring
