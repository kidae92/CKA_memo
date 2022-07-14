- kube proxy는 kubectl utility가 API server에 엑세스 위해 생성한 HTTP proxy임
```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: developer
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["list","get","create","update","delete"]
  resourceNames: ["blue","orange"]

- apiGroups: [""]
  resources: ["ConfigMap"]
  verbs: ["create"]
```

```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: devuser-developer-binding
subjects:
- kind: User
  name: dev-user
  apiGroup: rbac.authorization.k8s.io/v1

- kind: Role
  name: developer
  apiGroup: rbac.authorization.k8s.io/v1
```

```
kubectl auth can-i create deployments (--as dev-user)-> yes or no
```