

- Pod 생성하면서 node를 정해줌
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
    tier: frontend
spec:
  containers:
  -  name: nginx
     image: nginx
     
  nodeName: node02
    
```

- Binding object를 생성하여 연결
```
apiVersion: v1
kind: Binding
metadata:
  name: nginx
  
target:
  apiVersion: v1
  kind: Node
  name: node02
    
```

- Pod이 Pending 상태인 경우, Scheduler가  없는 경우가 있을 수 있음
- 