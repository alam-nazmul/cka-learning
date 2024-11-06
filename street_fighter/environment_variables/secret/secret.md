### Secret:
* A Secret object stores sensitive data such as credentials used by Pods to access services. For
  example, you might need a Secret to store the username and password needed to access a database.
* secret is namespace specific
* secret provide secrecy / base64 encoded data
* Not Shareable among namespaces.


### How to get secret
```Actionscript
kubectl get secrets
```

### How to create secrets by cmd
```Actionscript
kubectl create secrets generic <name> --from-literal key1=value1
```

### Need to convert the value from plain text to 64 bit encrypted
```Actionscript
echo nazmul | base64
```

### How to check the secrets keys and values
```Actionscript
kubectl get secrets <name> -o yaml
```