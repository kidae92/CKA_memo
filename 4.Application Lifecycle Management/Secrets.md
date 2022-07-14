```
kubectl create secret generic <secret-name> --from-literal=<key>=<value>
kubectl create secret generic <secret-name> --from-file=<file path>

```

```
# secret-data.yaml
apiVersionL v1
kind: Secret
metadata:
  name: app-secret
data:
  DB_Host: admin
  DB_User: root
  DB_Password: admin
```
- 이 또한 하드코딩 되어서 안전하지가 않다.
- echo -n 'mysql' | base64  (인코딩해서 넣어야 안전하다)
- echo -n 'bXlzcWw=' | base64 --decode (디코딩)
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
   ports:
     - containerPort: 8080
   envFrom:
     - secretRef:
         name: app-secret
```

- secret 파일 전체를 volume으로 넣을 수도 있음
```
volumes:
  - name: app-secret-volume
    secret:
      secretName: app-secret
```

```
# edit 명령이 안먹을때 
kubectl replace --force -f /tmp/ooo.yaml
```