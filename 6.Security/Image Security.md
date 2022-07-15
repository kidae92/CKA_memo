- private image를 yaml파일에 자격증명을 어떻게 할것인가?
```
# secret을 만든다
kubectl create secret docker-registry regcred
    --docker-server
    --docker-username
    --docker-password
    --docker-email
```
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
     image: private-nginx
  imagePullSecrets:
  - name: regcred

```