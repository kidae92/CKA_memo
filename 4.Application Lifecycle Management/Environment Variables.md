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
     
   env:
     - name: APP_COLOR
       value: pink (Plain Key Value)
     
       name: APP_COLOR  
       valueFrom;
         configMapKeyRef:
           name: app-config
           key: APP_COLOR
         
         
       name: APP_COLOR  
       valueFrom;
         secretKeyRef(Secrets)
         
-----------------------------------
   envFrom:         
     - configMapRef:
         name: app=-config(이미 configmap pod이 있을 경우)
         
-----------------------------------------
   volumes:
   - name: app-config-volume
     configMap:
       name: app-config       
      
```
```
kubectl create configmap <config-name> --from-literal=APP_COLOR=blue
```

```
# config-map.yaml
apiVersionL v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_COLOR: blue
  APP_COLOR: prod
```
```
kubectl create -f config-map.yaml
```
