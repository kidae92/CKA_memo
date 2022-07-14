```
kubectl api-resources --namespaced=true or false
```
- resource에 role, rolebinding이랑 똑같은 개념이다

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: cluster-administrator
rules:
- apiGroups: [""]
  resources: ["nodes"]
  verbs: ["list","get","create","update","delete"]
 
```
```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: devuser-developer-binding
subjects:
- kind: User
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io/v1
roleRef:
  kind: ClusterRole
  name: cluster-administrator
  apiGroup: rbac.authorization.k8s.io/v1
```

kubectl get clusterroles --no-headers | wc -l
갯수세는 명령어 외우기