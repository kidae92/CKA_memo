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
     
  schedulerName: my-custom-scheduler


```

```
#pod이 어떤 scheduler에의해 만들어지는지 확인 할 수 있음. 노드 위치도 알 수 있음
kubectl get event
kubectl logs my-custom-scheduler --name-space=kube-system
```