```
kubectl get pods --kubeconfig config
# KubeConfig File($HOME/.kube/config)
1. Cluster
--server
--certificate-authority
2. Context (default namespace를 지정해줄 수 있음)
3. Users
--client-key
--client-certificate
```
```
kubectl config use-context prod-user@production
```