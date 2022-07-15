- serviceaccount의 token은 Secret
- 일반적인 pod을 describe해보면 Volumes에 토큰을 포함하는 secret이 있음
- Mounts에 pod내 serviceaccount의 secret 경로가 적혀있음
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
  serviceAccountName: dashboard-sa
```