### Limit Ranges:

- The administrator creates a LimitRange in a namespace.
- Users create (or try to create) objects in that namespace, such as Pods or PersistentVolumeClaims.
- First, the LimitRange admission controller applies default request and limit values for all Pods (and their containers) that do not set compute resource requirements.
- Second, the LimitRange tracks usage to ensure it does not exceed resource minimum, maximum and ratio defined in any LimitRange present in the namespace.
- If you attempt to create or update an object (Pod or PersistentVolumeClaim) that violates a LimitRange constraint, your request to the API server will fail with an HTTP status code 403 Forbidden and a message explaining the constraint that has been violated.
- If you add a LimitRange in a namespace that applies to compute-related resources such as cpu and memory, you must specify requests or limits for those values. Otherwise, the system may reject Pod creation.
- LimitRange validations occur only at Pod admission stage, not on running Pods. If you add or modify a LimitRange, the Pods that already exist in that namespace continue unchanged.
- If two or more LimitRange objects exist in the namespace, it is not deterministic which default value will be applied.


#### _Default resource is NameSpace wise. Default value is applicable when we will not allocate any resources pn Pod definition file._

#### _Resource allocation will get more priority than Default resources._

#### _For best practice, default resource will be lower than resource allocation of Pod definition file_

### Show the limit ranges
```Actionscript
kubectl get limitrange
```

### Show the details of limit ranages
```Actionscript
kubectl describe limitranges
```