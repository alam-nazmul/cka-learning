#### By set the affinity we can run a pod by multiple values of nodes. By using manual scheduling and nodeselector we can assign single label's of node to run a Pod.


### Classification:

1. Node affinity
2. Pod affinity


### Node Affinity:
```angular2html
requiredDuringSchedulingIgnoredDuringExecution
```
requiredDuringScheduling = When the pods are scheduled, it will fulfill the conditions.

IgnoredDuringExecution = Existing pods will not remove after create a label on Node. 


```Actionscript
preferredDuringSchedulingIgnoredDuringExecution
```
preferredDuringScheduling =  When the pods are scheduled, it will prefer the conditions. If it can not meet it then the Pods will deploy any nodes.
