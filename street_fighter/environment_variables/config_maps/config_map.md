### ConfigMap:
* A ConfigMap is an API object used to store non-confidential data in key-value pairs.
  Pods can consume ConfigMaps as environment variables, command-line arguments, or as
  configuration files in a volume.
* ConfigMap is namespace specific
* ConfigMap does not provide secrecy or encryption.
* Not Shareable among namespaces


### How to show configMap
```Actionscript
kubectl get configmap
```

### How to create a configMap by a commandline
```Actionscript
kubectl create configmap <name> --from-literal key1=value1
```

