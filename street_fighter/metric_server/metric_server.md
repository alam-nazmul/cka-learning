The Kubernetes Metrics Server is a cluster-wide aggregator of resource usage data, such as CPU and memory, which can be used by components like kubectl top, Horizontal Pod Autoscaler, and Vertical Pod Autoscaler. Here’s a quick guide on how to install and use the Metrics Server on your Kubernetes cluster.

#### _Make sure the metrics server is installed on Master node_


### How to show current usage on nodes
```Actionscript
kubectl top node
```

### How to show current usage on pods
```Actionscript
kubectl top pod
```

### How to show current usage on nodes by sorting CPU
```Actionscript
kubectl top node --sort-by cpu
```

### How to show current usage on nodes by sorting RAM
```Actionscript
kubectl top node --sort-by memory
```

#### _By default Metrics server will update after 15 secs_


### How to show current usage on pods by sorting RAM with labels
```Actionscript
kubectl top pods --sort-by memory --selector dept=EEE --namespace alhua
```

