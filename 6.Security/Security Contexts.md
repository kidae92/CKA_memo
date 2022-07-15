```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
    tier: frontend
spec:
//  securityContext:
//    runAsUser: 1000
  containers:
  -  name: nginx
     image: nginx
     securityContext:
       runAsUser: 1000
       capabilityes:
         add: ["MAX_ADMIN"]
  
```

```
# pod user 알아보는법
kubectl exec pod/ubuntu-sleeper -- whoami
```